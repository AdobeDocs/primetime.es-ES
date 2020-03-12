---
description: 'null'
seo-description: 'null'
seo-title: Lógica de dominio anónimo
title: Lógica de dominio anónimo
uuid: bd0e8e51-27dc-4ccf-b285-a80c2ab9e260
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lógica de dominio anónimo{#anonymous-domain-logic}

## Lógica de registro de dominio {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

La implementación de referencia aplica la siguiente lógica para el registro de dominios anónimos:

1. Analice el nombre de dominio desde la dirección URL de la solicitud.
1. Busque el nombre de dominio en la `DomainServerInfo` tabla.
1. Si no puede localizar una entrada, inserte una entrada en la tabla.

   Los valores predeterminados son:

   * `authentication is not required`
   * `no membership maximum`
   Si se requiere autenticación para el dominio solicitado, asegúrese de que la solicitud incluye un token de autenticación válido. Si se especifica el espacio de nombres Auth en la base de datos, el token debe coincidir con el espacio de nombres Auth especificado.
1. Si se requiere autenticación, pero no hay disponible un autentificador válido, se mostrará el error `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Compruebe si el dispositivo está registrado en el dominio:

   1. Busque el nombre de dominio en la `DomainMembership` tabla.
   1. Compare el GUID del equipo que encuentra con el GUID del equipo en la solicitud.
   1. Si se trata de una máquina nueva, agregue una entrada en la `DomainMembership` tabla.
   1. Si se trata de un dispositivo nuevo y se ha alcanzado `Max Membership` un valor, se mostrará el error `DOM_LIMIT_REACHED (502)`.

1. Busque todas las claves de dominio de este dominio en la `DomainKeys` tabla:

   1. Si `DomainServerInfo` indica que es necesario pasar las teclas por encima, genere un nuevo par de claves.
   1. Guarde el par de claves en la `DomainKeys` tabla, con una versión de clave que sea un número mayor que la clave existente más alta.
   1. Restaure el `Key Rollover Required` indicador en `DomainServerInfo`.

   1. Para cada clave de dominio, genere una credencial de dominio.

## Lógica de anulación del registro del dominio {#section_C968BBFCBFAB4510A903D169F38C9FCE}

La implementación de referencia aplica la siguiente lógica para el desregistro de dominios anónimos:

1. Analice el nombre de dominio desde la dirección URL de la solicitud.
1. Busque el nombre de dominio solicitado en la `DomainServerInfo` tabla.
1. Si se requiere autenticación para el dominio solicitado, asegúrese de que la solicitud incluye un token de autenticación válido.

   El token también debe coincidir con el espacio de nombres Auth especificado en la base de datos.
1. Busque el nombre de dominio y el GUID del equipo en la `DomainMembership` tabla.

   Si no encuentra una entrada coincidente, devuelva el error `DEREG_DENIED (401)`.

1. Si no se trata de una solicitud de vista previa, elimine la entrada de `DomainMembership`y, en `DomainServerInfo`, establezca el `Key Rollover Required` indicador.

Dado que un gran número de equipos pueden unirse al dominio, no puede simplemente coincidir con el ID del equipo. En su lugar, se aplica el GUID de equipo aleatorio asignado al equipo durante la individualización.
