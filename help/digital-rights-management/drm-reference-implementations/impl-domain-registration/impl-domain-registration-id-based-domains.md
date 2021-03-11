---
title: Lógica de registro de dominio basada en identidad
description: Lógica de registro de dominio basada en identidad
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Lógica de registro de dominio basada en identidad{#identity-based-domain-registration-logic}

## Lógica de registro de dominio {#section_149C247458954877AF158B4A09A8526B}

La implementación de referencia aplica la siguiente lógica para el registro de dominios basados en identidad:

1. Determine el nombre de dominio que se va a asignar a un usuario designado.

   El nombre de dominio ( `namequalifier:username`) se extrae del token de autenticación. Si un token no está disponible, se produce un error.
1. Busque el nombre de dominio en la tabla `DomainServerInfo`.

   Si no se encuentra ninguna entrada, inserte una entrada. Los valores predeterminados son:

   * `authentication required`
   * `max domain membership=5`

   .

1. Para verificar que el dispositivo se ha registrado con el dominio :

   1. Busque `domainname` en la tabla `UserDomainMembership`:

      1. Para cada ID de equipo que se encuentre, compare el ID con el ID de equipo de la solicitud.
      1. Si se trata de un equipo nuevo, agregue una entrada a la tabla `UserDomainMembership`.
      1. Busque los registros coincidentes en la tabla `UserDomainRefCount`.
      1. Si no existe una entrada para este GUID de equipo, agregue un registro.
   1. Si es un dispositivo nuevo y se ha alcanzado el valor `Max Membership` , se devuelve el error .


1. Busque todas las claves de dominio para este dominio en la tabla `DomainKeys`:

   1. Si `DomainServerInfo` indica que es necesario mover las claves, genere un nuevo par de claves,
   1. Guarde el par en la tabla `DomainKeys`, con una versión clave que sea una más alta que la clave existente más alta.
   1. Restablezca el indicador `Key Rollover Required` en `DomainServerInfo`.

   1. Para cada clave de dominio, genere una credencial de dominio.

## Lógica de anulación del registro del dominio {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

La implementación de referencia aplica la siguiente lógica para el desregistro de dominios basado en identidad:

1. Determine el nombre de dominio que se va a asignar a este usuario.

   El nombre de dominio es `namequalifier:username`, que se extrae del token de autenticación. Si no hay ningún token disponible, se produce el error `DOM_AUTHENTICATION_REQUIRED (503)` de retorno.
1. Busque el nombre de dominio solicitado en la tabla `DomainServerInfo`.
1. Busque el nombre de dominio en la tabla `UserDomainMembership`.
1. Compare cada ID de equipo que encuentre con el ID de equipo de la solicitud.
1. Busque la entrada correspondiente en la tabla `UserDomainRefCount`.

   Si no se encuentra una entrada coincidente, devuelve el error .

1. Si no se trata de una solicitud de vista previa, elimine la entrada de la tabla `UserDomainRefCount` .
1. Si no hay entradas adicionales en esa tabla para el equipo, elimine la entrada de `UserDomainMembership` y establezca el indicador [!DNL Key Rollover Required] en la propiedad `DomainServerInfo`.

Cada usuario puede registrar un pequeño número de máquinas, por lo que puede utilizar el ID completo del equipo y el método `matches()` para contar los equipos. Dado que un usuario puede registrarse varias veces, a través de varias aplicaciones de AIR o reproductores en distintos navegadores, el servidor debe mantener un recuento de referencia para que también se pueda contar la anulación de registro.

>[!NOTE]
>
>La anulación del registro no está completa hasta que se hayan entregado todos los tokens de dominio del equipo.

