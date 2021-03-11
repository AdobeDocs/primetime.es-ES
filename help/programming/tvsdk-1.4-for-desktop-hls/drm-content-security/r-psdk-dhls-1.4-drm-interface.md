---
description: El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) de Primetime es el administrador de DRM.
title: Información general sobre la interfaz de DRM de Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Descripción general de la interfaz de DRM de Primetime{#primetime-drm-interface-overview}

El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) de Primetime es el administrador de DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM proporciona un flujo de trabajo escalable y eficiente para implementar la protección de contenido en aplicaciones TVSDK. Para proteger y administrar los derechos del contenido de vídeo, debe crear una licencia para cada archivo multimedia digital.

TVSDK admite la integración de DRM de Primetime como flujos de trabajo DRM personalizados. Esto significa que la aplicación debe implementar los flujos de trabajo de autenticación DRM antes de reproducir el flujo mediante el Flash `DRMManager`. Para habilitarlo, el `MediaPlayer` le proporciona el administrador de DRM para la autenticación.

Estos son los elementos API más importantes para trabajar con DRM:

* Referencia en el reproductor de medios al objeto de administrador de DRM que implementa el subsistema DRM:

   ```
   public function get drmManager():DRMManager 
   ```

<!--<a id="section_4204CE2731A44F67A3664AEDE8CCCA47"></a>-->

Elementos de API relevantes adicionales:

* [flash.net.drm.DRMManager](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html)
* [flash.net.drm.DRMContentData](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMContentData.html)
* [flash.net.drm.DRMVoucher](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMVoucher.html)
* [flash.net.drm.AuthenticationMethod](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/AuthenticationMethod.html)
* [flash.events.DRMStatusEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMStatusEvent.html)
* [flash.events.DRMErrorEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMErrorEvent.html)

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obtener más información sobre DRM, consulte la documentación de Adobe Primetime DRM.
