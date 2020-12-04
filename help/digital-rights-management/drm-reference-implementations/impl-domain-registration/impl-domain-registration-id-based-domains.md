---
description: 'null'
seo-description: 'null'
seo-title: Lógica de registro de dominio basada en la identidad
title: Lógica de registro de dominio basada en la identidad
uuid: bc13f7c2-9a20-4f80-b96f-05f7a0fcc343
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---


# Lógica de registro de dominio basada en identidad{#identity-based-domain-registration-logic}

## Lógica de registro de dominio {#section_149C247458954877AF158B4A09A8526B}

La implementación de referencia aplica la siguiente lógica para el registro de dominios basados en la identidad:

1. Determine el nombre de dominio que se asignará a un usuario designado.

   El nombre de dominio ( `namequalifier:username`) se extrae del token de autenticación. Si un token no está disponible, se genera un error.
1. Busque el nombre de dominio en la tabla `DomainServerInfo`.

   Si no se encuentra ninguna entrada, inserte una entrada. Los valores predeterminados son:

   * `authentication required`
   * `max domain membership=5`

   .

1. Para comprobar que el dispositivo se ha registrado en el dominio:

   1. Busque `domainname` en la tabla `UserDomainMembership`:

      1. Para cada ID de equipo que se encuentre, compare el ID con el ID de equipo de la solicitud.
      1. Si se trata de una máquina nueva, agregue una entrada a la tabla `UserDomainMembership`.
      1. Busque los registros coincidentes en la tabla `UserDomainRefCount`.
      1. Si no existe una entrada para este GUID de equipo, agregue un registro.
   1. Si es un dispositivo nuevo y se ha alcanzado el valor `Max Membership`, se mostrará el error return .


1. Busque todas las claves de dominio de este dominio en la tabla `DomainKeys`:

   1. Si `DomainServerInfo` indica que es necesario pasar el ratón por encima de las claves, genere un nuevo par de claves,
   1. Guarde el par en la tabla `DomainKeys`, con una versión clave que sea una más alta que la clave existente más alta.
   1. Restablezca el indicador `Key Rollover Required` en `DomainServerInfo`.

   1. Para cada clave de dominio, genere una credencial de dominio.

## Lógica de desregistro de dominio {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

La implementación de referencia aplica la siguiente lógica para la anulación del registro de dominios basados en la identidad:

1. Determine el nombre de dominio que se va a asignar a este usuario.

   El nombre de dominio es `namequalifier:username`, que se extrae del token de autenticación. Si no hay ningún token disponible, se produce el error `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Busque el nombre de dominio solicitado en la tabla `DomainServerInfo`.
1. Busque el nombre de dominio en la tabla `UserDomainMembership`.
1. Compare cada ID de equipo que encuentre con el ID de equipo de la solicitud.
1. Busque la entrada correspondiente en la tabla `UserDomainRefCount`.

   Si no se encuentra una entrada coincidente, se devuelve el error .

1. Si no se trata de una solicitud de previsualización, elimine la entrada de la tabla `UserDomainRefCount`.
1. Si no hay entradas adicionales en esa tabla para la máquina, elimine la entrada de `UserDomainMembership` y defina el indicador [!DNL Key Rollover Required] en la propiedad `DomainServerInfo`.

Cada usuario puede registrar un pequeño número de equipos, por lo que puede utilizar el identificador completo del equipo y el método `matches()` para contar los equipos. Dado que un usuario puede registrarse varias veces, a través de varias aplicaciones de AIR o reproductores en distintos navegadores, el servidor debe mantener un recuento de referencia para que también se pueda contar la anulación del registro.

>[!NOTE]
>
>La anulación del registro no se completa hasta que se entreguen todos los tokens de dominio del equipo.

