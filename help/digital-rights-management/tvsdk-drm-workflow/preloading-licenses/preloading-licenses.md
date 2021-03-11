---
title: Información general sobre las licencias de precarga para la reproducción sin conexión
description: Información general sobre las licencias de precarga para la reproducción sin conexión
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# Licencias de precarga para reproducción sin conexión {#pre-loading-licenses-for-offline-playback}

Puede cargar previamente las licencias necesarias para reproducir contenido protegido por Primetime DRM. Las licencias precargadas permiten a los usuarios ver el contenido tanto si tienen una conexión a Internet activa como si no.

El proceso de precarga en sí *sí* requiere una conexión a Internet. Puede utilizar `DRMManager.loadVoucher()` con antelación para precargar las licencias. Posteriormente, cuando el cliente desea reproducir el contenido deseado, el sistema DRM se preimprimió y puede reproducir el contenido protegido inmediatamente.
