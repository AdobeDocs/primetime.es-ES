---
seo-title: Información general sobre las licencias de precarga para reproducción sin conexión
title: Información general sobre las licencias de precarga para reproducción sin conexión
uuid: 71e5169b-7f70-4723-9f9b-fdff822c5876
translation-type: tm+mt
source-git-commit: 9bbcb228d3367fbf53de811bf2941ca653ce3b0e
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# Licencias de precarga para reproducción sin conexión {#pre-loading-licenses-for-offline-playback}

Puede cargar previamente las licencias necesarias para reproducir contenido protegido por Primetime DRM. Las licencias precargadas permiten a los usuarios realizar vistas en el contenido tanto si tienen una conexión a Internet activa como si no.

El propio proceso de precarga *requiere* una conexión a Internet. Puede utilizar `DRMManager.loadVoucher()` con antelación para precargar las licencias. Más tarde, cuando el cliente desea reproducir el contenido deseado, el sistema DRM se preimprimió y puede reproducir el contenido protegido inmediatamente.
