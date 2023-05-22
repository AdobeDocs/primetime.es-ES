---
description: El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) de Primetime es el Administrador de DRM.
title: Información general sobre la interfaz DRM Primetime
exl-id: 8d6b9416-5d8a-4d1e-b8e6-47c43389f079
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Información general sobre la interfaz DRM Primetime{#primetime-drm-interface-overview}

El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) de Primetime es el Administrador de DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM proporciona un flujo de trabajo escalable y eficaz para implementar la protección de contenido en aplicaciones TVSDK. Protege y administra los derechos del contenido de vídeo creando una licencia para cada archivo multimedia digital.

TVSDK admite la integración de DRM de Primetime como flujos de trabajo de DRM personalizados. Esto significa que la aplicación debe implementar los flujos de trabajo de autenticación DRM antes de reproducir el flujo utilizando el Flash `DRMManager`. Para habilitar esto, se debe usar la variable `MediaPlayer` proporciona el administrador de DRM para la autenticación.

Estos son los elementos de API más importantes para trabajar con DRM:

* Referencia en el reproductor de contenido al objeto del administrador de DRM que implementa el subsistema de DRM:

   ```
   public function get drmManager():DRMManager 
   ```

<!--<a id="section_4204CE2731A44F67A3664AEDE8CCCA47"></a>-->

Elementos de API adicionales relevantes:

* [flash.net.drm.DRManager](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html)
* [flash.net.drm.DRMContentData](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMContentData.html)
* [flash.net.drm.DRMVoucher](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMVoucher.html)
* [flash.net.drm.AuthenticationMethod](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/AuthenticationMethod.html)
* [flash.events.DRMStatusEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMStatusEvent.html)
* [flash.events.DRMErrorEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMErrorEvent.html)

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obtener más información sobre DRM, consulte la Documentación de DRM de Adobe Primetime.
