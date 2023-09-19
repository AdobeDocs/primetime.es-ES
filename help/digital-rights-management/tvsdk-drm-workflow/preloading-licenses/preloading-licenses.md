---
title: Información general sobre la precarga de licencias para reproducción sin conexión
description: Información general sobre la precarga de licencias para reproducción sin conexión
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Precarga de licencias para la reproducción sin conexión {#pre-loading-licenses-for-offline-playback}

Puede precargar las licencias necesarias para reproducir contenido protegido por Primetime DRM. Las licencias precargadas permiten a los usuarios ver el contenido independientemente de si tienen o no una conexión a Internet activa.

El proceso de precarga en sí *hace* requieren una conexión a Internet. Puede utilizar `DRMManager.loadVoucher()` antes de tiempo para cargar previamente las licencias. Más tarde, cuando el cliente desee reproducir el contenido deseado, el sistema DRM se ha precebado y puede reproducir el contenido protegido inmediatamente.
