---
title: Lógica de dominio anónimo
description: Lógica de dominio anónimo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Lógica de dominio anónimo{#anonymous-domain-logic}

## Lógica de registro de dominio {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

La implementación de referencia aplica la siguiente lógica para el registro de dominios anónimos:

1. Analice el nombre de dominio desde la dirección URL de la solicitud.
1. Busque el nombre de dominio en la tabla `DomainServerInfo`.
1. Si no encuentra ninguna entrada, inserte una entrada en la tabla.

   Los valores predeterminados son:

   * `authentication is not required`
   * `no membership maximum`

   Si se requiere autenticación para el dominio solicitado, asegúrese de que haya un token de autenticación válido en la solicitud. Si el área de nombres de autenticación se especifica en la base de datos, el token debe coincidir con el área de nombres de autenticación especificada.
1. Si la autenticación es necesaria, pero no hay un token de autenticación válido disponible, devuelva el error `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Compruebe si el dispositivo está registrado en el dominio:

   1. Busque el nombre de dominio en la tabla `DomainMembership`.
   1. Compare el GUID del equipo que encuentra con el GUID del equipo en la solicitud.
   1. Si se trata de una máquina nueva, añada una entrada en la tabla `DomainMembership`.
   1. Si es un dispositivo nuevo y se ha alcanzado el valor `Max Membership` , se devuelve el error `DOM_LIMIT_REACHED (502)`.

1. Busque todas las claves de dominio para este dominio en la tabla `DomainKeys`:

   1. Si `DomainServerInfo` indica que es necesario mover las claves, genere un nuevo par de claves.
   1. Guarde el par de claves en la tabla `DomainKeys`, con una versión de clave que sea un número mayor que la clave existente más alta.
   1. Restablezca el indicador `Key Rollover Required` en `DomainServerInfo`.

   1. Para cada clave de dominio, genere una credencial de dominio.

## Lógica de anulación del registro del dominio {#section_C968BBFCBFAB4510A903D169F38C9FCE}

La implementación de referencia aplica la siguiente lógica a la anulación de registro de dominios anónimos:

1. Analice el nombre de dominio desde la dirección URL de la solicitud.
1. Busque el nombre de dominio solicitado en la tabla `DomainServerInfo`.
1. Si se requiere autenticación para el dominio solicitado, asegúrese de que haya un token de autenticación válido en la solicitud.

   El token también debe coincidir con el área de nombres de autenticación especificada en la base de datos.
1. Busque el nombre de dominio y el GUID del equipo en la tabla `DomainMembership`.

   Si no encuentra una entrada coincidente, devuelva el error `DEREG_DENIED (401)`.

1. Si no se trata de una solicitud de vista previa, elimine la entrada de `DomainMembership` y, en `DomainServerInfo`, establezca el indicador `Key Rollover Required`.

Dado que un gran número de equipos puede unirse al dominio, no puede coincidir con el ID del equipo. En su lugar, se aplica el GUID de máquina aleatorio asignado al equipo durante la individualización.
