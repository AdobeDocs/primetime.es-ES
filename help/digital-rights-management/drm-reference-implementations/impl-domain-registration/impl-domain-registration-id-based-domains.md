---
title: Lógica de registro de dominio basada en identidad
description: Lógica de registro de dominio basada en identidad
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Lógica de registro de dominio basada en identidad{#identity-based-domain-registration-logic}

## Lógica de registro de dominio {#section_149C247458954877AF158B4A09A8526B}

La implementación de referencia aplica la siguiente lógica para el registro de dominios basados en la identidad:

1. Determine el nombre de dominio que desea asignar a un usuario designado.

   El nombre de dominio ( `namequalifier:username`) se extrae del token de autenticación. Si un token no está disponible, se produce un error.
1. Busque el nombre de dominio en la `DomainServerInfo` tabla.

   Si no se encuentra ninguna entrada, inserte una entrada. Los valores predeterminados son:

   * `authentication required`
   * `max domain membership=5`

   .

1. Para comprobar que el dispositivo se ha registrado con el dominio:

   1. Busque la variable `domainname` en el `UserDomainMembership` tabla:

      1. Para cada ID de equipo que se encuentra, compare el ID de con el ID de equipo en la solicitud.
      1. Si se trata de un equipo nuevo, agregue una entrada al `UserDomainMembership` tabla.
      1. Busque los registros coincidentes en `UserDomainRefCount` tabla.
      1. Si no existe ninguna entrada para este GUID de equipo, agregue un registro.

   1. Si es un dispositivo nuevo y la variable `Max Membership` se ha alcanzado el valor de, error devuelto

1. Busque todas las claves de dominio de este dominio en la `DomainKeys` tabla:

   1. If `DomainServerInfo` indica que es necesario renovar las claves, generar un nuevo par de claves,
   1. Guarde el par en el `DomainKeys` , con una versión de clave superior a la clave existente más alta.
   1. Restablecer el `Key Rollover Required` marcar en `DomainServerInfo`.

   1. Para cada clave de dominio, genere una credencial de dominio.

## Lógica de anulación de registro del dominio {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

La implementación de referencia aplica la siguiente lógica para la anulación de registro de dominios basados en la identidad:

1. Determine el nombre de dominio que desea asignar a este usuario.

   El nombre de dominio es `namequalifier:username`, que se extrae del token de autenticación. Si no hay ningún token disponible, devuelve un error `DOM_AUTHENTICATION_REQUIRED (503)` ocurre.
1. Busque el nombre de dominio solicitado en la variable `DomainServerInfo` tabla.
1. Busque el nombre de dominio en la `UserDomainMembership` tabla.
1. Compare cada ID de equipo que encuentre con el ID de equipo de la solicitud.
1. Busque la entrada correspondiente en la `UserDomainRefCount` tabla.

   Si no se encuentra ninguna entrada coincidente, devuelve el error

1. Si no se trata de una solicitud de previsualización, elimine la entrada de la `UserDomainRefCount` tabla.
1. Si no hay entradas adicionales en esa tabla para el equipo, elimine la entrada de `UserDomainMembership` y configure el [!DNL Key Rollover Required] indicador en la `DomainServerInfo` propiedad.

Cada usuario puede registrar un pequeño número de equipos, por lo que puede utilizar el ID de equipo completo y el `matches()` método para contar máquinas. Dado que un usuario puede registrarse varias veces, a través de varias aplicaciones de AIR o reproductores en distintos navegadores, el servidor debe mantener un recuento de referencia para que también se pueda contar la anulación de registro.

>[!NOTE]
>
>La anulación del registro no se completa hasta que se entreguen todos los tokens de dominio del equipo.
