---
seo-title: Dominios anónimos
title: Dominios anónimos
uuid: ee29ae4d-65b2-48de-b441-18c8cf55de32
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Dominios anónimos {#anonymous-domains}

En este caso de uso, un gran número de dispositivos pertenece a un único dominio y puede que no se requiera autenticación. Para utilizar este tipo de dominio con la implementación de referencia, cree la directiva que especifique que se requiere el registro del dominio. Especifique la URL del servidor de dominio `https:// host:port/flashaccess/domainserver/domainname/` y la autenticación anónima.

La implementación de referencia implementa la siguiente lógica para el registro de dominios:

1. Analice el nombre de dominio desde la dirección URL de la solicitud.
1. Busque el nombre de dominio en la `DomainServerInfo` tabla. Si no se encuentra una entrada, inserte una entrada en la tabla (valores predeterminados: no es necesaria la autenticación y no hay un máximo de miembros).
1. Si se requiere autenticación para el dominio solicitado, asegúrese de que se ha incluido un token de autenticación válido en la solicitud y de que coincide con la Área de nombres Auth, si se especifica en la base de datos.

   1. Si se requiere autenticación pero no se ha proporcionado ningún token de autenticación válido, se mostrará el error `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Compruebe si el dispositivo ya se ha registrado en el dominio:

   1. Busque el nombre de dominio en la `DomainMembership` tabla. Para cada GUID de equipo encontrado, compare con el GUID de equipo en la solicitud. Si se trata de una máquina nueva, agregue una entrada a la `DomainMembership` tabla.

   1. Si se trata de un dispositivo nuevo y ya se ha alcanzado la pertenencia máxima, se mostrará el error `DOM_LIMIT_REACHED (502)`.

1. Busque todas las claves de dominio de este dominio en la `DomainKeys` tabla.

   1. Si `DomainServerInfo` indica que es necesario pasar el cursor por encima, genere un nuevo par de claves, guárdelo en la `DomainKeys` tabla (con la versión de clave uno más alta que la clave existente más alta) y restablezca el `Key Rollover Required` indicador en `DomainServerInfo`.

   1. Para cada clave de dominio, genere una credencial de dominio.

La implementación de referencia implementa la siguiente lógica para la anulación del registro de dominios:

1. Analice el nombre de dominio desde la dirección URL de la solicitud.
1. Busque el nombre de dominio solicitado en la `DomainServerInfo` tabla.
1. Si se requiere autenticación para el dominio solicitado, asegúrese de que se ha incluido un token de autenticación válido en la solicitud y de que coincide con la Área de nombres Auth, si se especifica en la base de datos.
1. Busque el nombre de dominio y el GUID del equipo en la `DomainMembership` tabla. Si no se encuentra una entrada coincidente, devuelve un error `DEREG_DENIED (401)`.

1. Si no se trata de una solicitud de previsualización, elimine la entrada de `DomainMembership` y defina el `Key Rollover Required` indicador en `DomainServerInfo`.

En este caso de uso, dado que un gran número de equipos podría unirse al dominio, no es posible que coincida completamente con el ID del equipo. En su lugar, se utiliza el GUID de equipo aleatorio asignado al equipo durante la individualización.
