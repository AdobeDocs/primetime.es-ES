---
title: Dominios anónimos
description: Dominios anónimos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Dominios anónimos {#anonymous-domains}

En este caso de uso, un gran número de dispositivos pertenecen a un único dominio y es posible que no se requiera autenticación. Para utilizar este tipo de dominio con la implementación de referencia, cree la directiva que especifique que se requiere el registro de dominio. Especifique la URL del servidor de dominio como `https:// host:port/flashaccess/domainserver/domainname/` y la autenticación anónima.

La implementación de referencia implementa la siguiente lógica para el registro de dominios:

1. Analice el nombre de dominio desde la dirección URL de la solicitud.
1. Busque el nombre de dominio en la tabla `DomainServerInfo`. Si no se encuentra una entrada, inserte una entrada en la tabla (valores predeterminados: no es necesaria la autenticación y no hay un máximo de pertenencia).
1. Si se requiere autenticación para el dominio solicitado, asegúrese de que se haya incluido un token de autenticación válido en la solicitud y que coincida con el área de nombres de autenticación, si se especifica en la base de datos.

   1. Si se requiere autenticación pero no se ha proporcionado ningún token de autenticación válido, se devuelve el error `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Compruebe si el dispositivo ya se ha registrado con el dominio :

   1. Busque el nombre de dominio en la tabla `DomainMembership`. Para cada GUID de equipo encontrado, compare con el GUID de equipo en la solicitud. Si se trata de un equipo nuevo, agregue una entrada a la tabla `DomainMembership`.

   1. Si se trata de un dispositivo nuevo y ya se ha alcanzado la pertenencia máxima, devuelva el error `DOM_LIMIT_REACHED (502)`.

1. Busque todas las claves de dominio para este dominio en la tabla `DomainKeys` .

   1. Si `DomainServerInfo` indica que es necesario pasar el ratón por encima de las claves, genere un nuevo par de claves, guárdelo en la tabla `DomainKeys` (con la versión de clave uno más alta que la clave existente más alta) y restablezca el indicador `Key Rollover Required` en `DomainServerInfo`.

   1. Para cada clave de dominio, genere una credencial de dominio.

La implementación de referencia implementa la siguiente lógica para la anulación del registro de dominios:

1. Analice el nombre de dominio desde la dirección URL de la solicitud.
1. Busque el nombre de dominio solicitado en la tabla `DomainServerInfo`.
1. Si se requiere autenticación para el dominio solicitado, asegúrese de que se haya incluido un token de autenticación válido en la solicitud y que coincida con el área de nombres de autenticación, si se especifica en la base de datos.
1. Busque el nombre de dominio y el GUID del equipo en la tabla `DomainMembership`. Si no se encuentra una entrada coincidente, devuelva el error `DEREG_DENIED (401)`.

1. Si no se trata de una solicitud de vista previa, elimine la entrada de `DomainMembership` y establezca el indicador `Key Rollover Required` en `DomainServerInfo`.

En este caso de uso, dado que un gran número de equipos podría unirse al dominio, no es posible que coincida completamente con el ID del equipo. En su lugar, se utiliza el GUID de máquina aleatorio asignado a la máquina durante la individualización.
