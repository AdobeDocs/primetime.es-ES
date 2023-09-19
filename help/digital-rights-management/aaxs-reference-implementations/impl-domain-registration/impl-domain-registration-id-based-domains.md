---
title: Dominios basados en identidad
description: Dominios basados en identidad
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Dominios basados en identidad {#identity-based-domains}

En este caso de uso, cada usuario autenticado tiene su propio dominio y se permite que un determinado número de dispositivos se una al dominio. Para utilizar este tipo de dominio con la implementación de referencia, cree una directiva que especifique que se requiere el registro de dominios. Especifique el host y el puerto del servidor para la URL del servidor de dominio y especifique que se requiere autenticación de nombre de usuario y contraseña.

La implementación de referencia implementa la siguiente lógica para el registro de dominios:

1. Determine el nombre de dominio que desea asignar a este usuario. El nombre de dominio será * `namequalifier:username`* extraído del token de autenticación. Si no hay ningún token de autenticación, devuelve el error DOM_AUTHENTICATION_REQUIRED (503).
1. Busque el nombre de dominio en la `DomainServerInfo` tabla. Si no se encuentra ninguna entrada, inserte una entrada en la tabla (los valores predeterminados son la autenticación necesaria, el número máximo de miembros del dominio es 5).
1. Compruebe si el dispositivo ya se ha registrado con el dominio:

   1. Busque el nombre de dominio en la `UserDomainMembership` tabla. Para cada ID de equipo encontrado, compárelo con el ID de equipo de la solicitud. Si se trata de un equipo nuevo, agregue una entrada al `UserDomainMembership` tabla. A continuación, busque los registros coincidentes en `UserDomainRefCount` tabla. Si no existe ninguna entrada para este GUID de equipo, agregue un registro.

   1. Si es un dispositivo nuevo y ya se ha alcanzado la pertenencia máxima, devuelve el error DOM_LIMIT_REACHED (502).

1. Busque todas las claves de dominio de este dominio en la tabla DomainKeys.

   1. If `DomainServerInfo` indica que es necesario renovar las claves, generar un nuevo par de claves y guardarlo en `DomainKeys` (con una versión de clave superior a la clave existente más alta) y restablezca el indicador &quot;Se requiere sustitución de clave&quot; en `DomainServerInfo`.

   1. Para cada clave de dominio, genere una credencial de dominio.

La implementación de referencia implementa la siguiente lógica para la anulación de registro de dominios:

1. Determine el nombre de dominio que desea asignar a este usuario. El nombre de dominio es *calificador de nombres:nombre de usuario* extraído del token de autenticación. Si no hay ningún token de autenticación, devuelve el error DOM_AUTHENTICATION_REQUIRED (503).
1. Busque el nombre de dominio solicitado en la variable `DomainServerInfo` tabla.
1. Busque el nombre de dominio en la `UserDomainMembership` tabla. Para cada ID de equipo encontrado, compárelo con el ID de equipo de la solicitud. Busque la entrada correspondiente en la `UserDomainRefCount` tabla. Si no se encuentra ninguna entrada coincidente, devuelve el error DEREG_DENIED (401).

1. Si no se trata de una solicitud de previsualización, elimine la entrada de `UserDomainRefCount` tabla. Si no hay más entradas en esa tabla para el equipo, elimine la entrada de `UserDomainMembership` y establezca el indicador &quot;Rollover de clave obligatorio&quot; en `DomainServerInfo`.

En este caso de uso, cada usuario puede registrar un pequeño número de máquinas, por lo que podemos utilizar el ID de máquina completo y el `matches()` para contar con precisión las máquinas. Sin embargo, dado que el usuario puede registrarse varias veces en este equipo (a través de varias aplicaciones de AIR o reproductores en diferentes navegadores), el servidor también debe mantener un recuento de referencia para que el anulación de registro se pueda contar con precisión. La anulación del registro no se puede considerar completa hasta que se entreguen todos los tokens de dominio del equipo.
