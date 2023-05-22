---
title: Lógica de dominio anónima
description: Lógica de dominio anónima
copied-description: true
exl-id: 4a6c3485-cde7-403f-89d8-f6420df3539a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Lógica de dominio anónima{#anonymous-domain-logic}

## Lógica de registro de dominio {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

La implementación de referencia aplica la siguiente lógica para el registro de dominios anónimos:

1. Analice el nombre de dominio desde la dirección URL de solicitud.
1. Busque el nombre de dominio en la `DomainServerInfo` tabla.
1. Si no encuentra una entrada, inserte una en la tabla.

   Los valores predeterminados son:

   * `authentication is not required`
   * `no membership maximum`

   Si se requiere autenticación para el dominio solicitado, asegúrese de que haya un token de autenticación válido en la solicitud. Si el área de nombres de autenticación se especifica en la base de datos, el token debe coincidir con el área de nombres de autenticación especificada.
1. Si se requiere autenticación, pero no hay un token de autenticación válido disponible, devuelve un error `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Compruebe si el dispositivo está registrado con el dominio:

   1. Busque el nombre de dominio en la `DomainMembership` tabla.
   1. Compare el GUID de equipo que encuentra con el GUID de equipo de la solicitud.
   1. Si se trata de un equipo nuevo, agregue una entrada en la `DomainMembership` tabla.
   1. Si es un dispositivo nuevo y `Max Membership` se ha alcanzado el valor, error de retorno `DOM_LIMIT_REACHED (502)`.

1. Busque todas las claves de dominio de este dominio en la `DomainKeys` tabla:

   1. If `DomainServerInfo` indica que es necesario renovar las claves y generar un nuevo par de claves.
   1. Guarde el par de claves en `DomainKeys` , con una versión de clave un número superior a la clave existente más alta.
   1. Restablecer el `Key Rollover Required` marcar en `DomainServerInfo`.

   1. Para cada clave de dominio, genere una credencial de dominio.

## Lógica de anulación de registro del dominio {#section_C968BBFCBFAB4510A903D169F38C9FCE}

La implementación de referencia aplica la siguiente lógica para la anulación de registro de dominios anónimos:

1. Analice el nombre de dominio desde la dirección URL de solicitud.
1. Busque el nombre de dominio solicitado en la variable `DomainServerInfo` tabla.
1. Si se requiere autenticación para el dominio solicitado, asegúrese de que haya un token de autenticación válido en la solicitud.

   El token también debe coincidir con el área de nombres de autenticación especificada en la base de datos.
1. Busque el nombre de dominio y el GUID de equipo en la `DomainMembership` tabla.

   Si no encuentra una entrada que coincida, devolverá un error `DEREG_DENIED (401)`.

1. Si no se trata de una solicitud de previsualización, elimine la entrada de `DomainMembership`, y en `DomainServerInfo`, configure el `Key Rollover Required` Indicador.

Dado que un gran número de equipos puede unirse al dominio, no puede coincidir simplemente con el ID del equipo. En su lugar, se aplica el GUID de equipo aleatorio asignado al equipo durante la individualización.
