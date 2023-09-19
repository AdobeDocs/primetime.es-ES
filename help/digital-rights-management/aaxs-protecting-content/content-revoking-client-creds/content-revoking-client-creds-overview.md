---
title: Revocar credenciales de cliente
description: Revocar credenciales de cliente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Revocar credenciales de cliente{#revoking-client-credentials}

En ciertas condiciones, es necesario revocar las credenciales de un cliente o comprobar si un conjunto determinado de credenciales ya se han revocado. Las credenciales se pueden revocar si están en peligro. Cuando esto sucede, las licencias ya no se emiten a clientes comprometidos.

El Adobe mantiene listas de revocación de certificados (CRL) para revocar clientes comprometidos. El SDK aplica automáticamente estas CRL. Los servidores de licencias pueden restringir aún más a los clientes si no permiten credenciales de equipo concretas o versiones concretas de credenciales de DRM y de tiempo de ejecución. A `RevocationList` se pueden crear y pasar al SDK para revocar las credenciales del equipo. Las versiones particulares de DRM/runtime se pueden revocar ya sea en el nivel de directiva (estableciendo restricciones de módulo en el derecho de reproducción) o globalmente (estableciendo restricciones de módulo en el `HandlerConfiguration`).

La discusión de este capítulo se centrará en revocar las credenciales del cliente.
