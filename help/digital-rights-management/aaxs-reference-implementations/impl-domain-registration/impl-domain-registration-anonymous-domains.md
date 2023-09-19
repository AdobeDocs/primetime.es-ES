---
title: Dominios anónimos
description: Dominios anónimos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Dominios anónimos {#anonymous-domains}

En este caso de uso, un gran número de dispositivos pertenecen a un único dominio y es posible que no se requiera autenticación. Para utilizar este tipo de dominio con la implementación de referencia, cree la directiva que especifique que se requiere el registro del dominio. Especifique la URL del servidor de dominio como `https:// host:port/flashaccess/domainserver/domainname/` y especifique la autenticación anónima.

La implementación de referencia implementa la siguiente lógica para el registro de dominios:

1. Analice el nombre de dominio desde la dirección URL de solicitud.
1. Busque el nombre de dominio en la `DomainServerInfo` tabla. Si no se encuentra ninguna entrada, inserte una entrada en la tabla (valores predeterminados: no se requiere autenticación ni máximo de pertenencia).
1. Si se requiere autenticación para el dominio solicitado, asegúrese de que se haya incluido un token de autenticación válido en la solicitud y haga coincidir el Área de nombres de autenticación, si se especifica en la base de datos.

   1. Si se requiere autenticación pero no se proporcionó ningún token de autenticación válido, devuelve un error `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Compruebe si el dispositivo ya se ha registrado con el dominio:

   1. Busque el nombre de dominio en la `DomainMembership` tabla. Para cada GUID de equipo encontrado, compárelo con el GUID de equipo de la solicitud. Si se trata de un equipo nuevo, agregue una entrada al `DomainMembership` tabla.

   1. Si es un dispositivo nuevo y ya se ha alcanzado la pertenencia máxima, devuelve un error `DOM_LIMIT_REACHED (502)`.

1. Busque todas las claves de dominio de este dominio en la `DomainKeys` tabla.

   1. If `DomainServerInfo` indica que es necesario renovar las claves, generar un nuevo par de claves y guardarlo en `DomainKeys` (con la versión de clave uno más alta que la clave existente más alta) y restablezca la `Key Rollover Required` marcar en `DomainServerInfo`.

   1. Para cada clave de dominio, genere una credencial de dominio.

La implementación de referencia implementa la siguiente lógica para la anulación de registro de dominios:

1. Analice el nombre de dominio desde la dirección URL de solicitud.
1. Busque el nombre de dominio solicitado en la variable `DomainServerInfo` tabla.
1. Si se requiere autenticación para el dominio solicitado, asegúrese de que se haya incluido un token de autenticación válido en la solicitud y haga coincidir el Área de nombres de autenticación, si se especifica en la base de datos.
1. Busque el nombre de dominio y el GUID de equipo en la `DomainMembership` tabla. Si no se encuentra ninguna entrada coincidente, devuelve el error `DEREG_DENIED (401)`.

1. Si no se trata de una solicitud de previsualización, elimine la entrada de `DomainMembership` y configure el `Key Rollover Required` marcar en `DomainServerInfo`.

En este caso de uso, dado que un gran número de equipos podrían unirse al dominio, no es posible hacer coincidir completamente el ID de equipo. En su lugar, se utiliza el GUID de equipo aleatorio asignado al equipo durante la individualización.
