---
title: Información general sobre la precarga de licencias para reproducción sin conexión
description: Información general sobre la precarga de licencias para reproducción sin conexión
copied-description: true
exl-id: 0d49c0e4-821b-4354-b92d-bbe2c07e467b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Precarga de licencias para la reproducción sin conexión {#pre-loading-licenses-for-offline-playback}

Puede precargar las licencias necesarias para reproducir contenido protegido por Primetime DRM. Las licencias precargadas permiten a los usuarios ver el contenido independientemente de si tienen o no una conexión a Internet activa.

El proceso de precarga en sí *hace* requieren una conexión a Internet. Puede utilizar `DRMManager.loadVoucher()` antes de tiempo para cargar previamente las licencias. Más tarde, cuando el cliente desee reproducir el contenido deseado, el sistema DRM se ha precebado y puede reproducir el contenido protegido inmediatamente.
