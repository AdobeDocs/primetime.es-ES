---
title: Información general
description: Información general
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Información general{#overview}

Es posible que tenga que revocar las credenciales de un cliente o comprobar si un conjunto determinado de credenciales ya se ha revocado bajo ciertas condiciones. Las credenciales se pueden revocar si están en peligro. Cuando se producen estos problemas, ya no se emiten licencias a clientes comprometidos.

El Adobe mantiene listas de revocación de certificados (CRL) para revocar clientes comprometidos. El SDK aplica automáticamente estas CRL. Los servidores de licencias pueden restringir aún más a los clientes si no permiten credenciales de equipo concretas o versiones concretas de credenciales de DRM y de tiempo de ejecución. A `RevocationList` se pueden crear y pasar al SDK para revocar las credenciales del equipo. Las versiones particulares de DRM/runtime se pueden revocar ya sea en el nivel de política de DRM estableciendo restricciones de módulo en el derecho de reproducción o globalmente estableciendo restricciones de módulo en el `HandlerConfiguration`.

La discusión se centra en revocar las credenciales del cliente.
