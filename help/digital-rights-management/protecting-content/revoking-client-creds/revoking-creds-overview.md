---
title: Información general
description: Información general
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Información general{#overview}

Es posible que deba revocar las credenciales de un cliente o comprobar si un conjunto determinado de credenciales ya se ha revocado en determinadas condiciones. Las credenciales pueden revocarse si se encuentran en peligro. Cuando se producen estos problemas, ya no se emiten licencias para clientes comprometidos.

Adobe mantiene listas de revocación de certificados (CRL) para revocar clientes comprometidos. El SDK aplica automáticamente estas CRL. Los servidores de licencias pueden restringir aún más a los clientes al rechazar credenciales de equipo concretas o versiones particulares de DRM y credenciales de tiempo de ejecución. Se puede crear un `RevocationList` que se puede pasar al SDK para revocar las credenciales del equipo. Las versiones específicas de DRM/tiempo de ejecución se pueden revocar en el nivel de directiva de DRM estableciendo restricciones de módulo en la derecha de reproducción o globalmente estableciendo restricciones de módulo en `HandlerConfiguration`.

La discusión se centra en revocar las credenciales del cliente.
