---
description: Puede utilizar las funciones del sistema de Digital Rights Management Primetime (DRM) para proporcionar acceso seguro al contenido de vídeo. Alternativamente, puede utilizar soluciones DRM de terceros como una alternativa a la solución DRM integrada de Primetime de Adobe.
keywords: DRM;DASH;HLS
title: Información general sobre la interfaz de DRM de Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Resumen de la interfaz de DRM de Primetime {#primetime-drm-interface-overview}

Puede utilizar las funciones del sistema de Digital Rights Management Primetime (DRM) para proporcionar acceso seguro al contenido de vídeo. Alternativamente, puede utilizar soluciones DRM de terceros como una alternativa a la solución DRM integrada de Primetime de Adobe.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Consulte con su representante de Adobe para obtener la información más actualizada sobre la disponibilidad de soluciones DRM de terceros.

El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) de Primetime es el administrador de DRM.

Primetime DRM proporciona un flujo de trabajo escalable y eficiente para implementar la protección de contenido en aplicaciones TVSDK. Para proteger y administrar los derechos del contenido de vídeo, debe crear una licencia para cada archivo multimedia digital.

TVSDK admite la integración de DRM de Primetime como flujos de trabajo DRM personalizados. Esto significa que la aplicación debe implementar los flujos de trabajo de autenticación DRM antes de reproducir el flujo mediante el Flash DRMManager. Para habilitarlo, MediaPlayer le proporciona el administrador de DRM para la autenticación.

Consulte el código del reproductor de muestra de DRM incluido en el paquete TVSDK.

Estos son los elementos API más importantes para trabajar con DRM:

* Referencia en el reproductor de medios al objeto de administrador de DRM que implementa el subsistema DRM:

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK envía una notificación `PTMediaPlayerItemDRMMetadataChanged` cuando cambian los metadatos de DRM. Estos metadatos se utilizan como entrada para casi todas las funciones de la clase `DRMManager`.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Si el flujo protegido por DRM está codificado con varias tasas de bits (MBR), los metadatos DRM que se utilizan para la lista de reproducción de variantes deben ser los mismos que los metadatos utilizados en todas las emisiones de velocidad de bits.

>[!TIP]
>
>Al hacer referencia a URL de recursos protegidos por DRM en su aplicación iOS, el parámetro de cadena de consulta `?faxs=1` debe añadirse a la URL M3U8 de nivel de conjunto (MBR). Por ejemplo:

```
https://your.domain.com/hls/[...]/index.m3u8?faxs=1
```

El parámetro de cadena de consulta `faxs=1` indica que el contenido está protegido con DRM y déclencheur el flujo de trabajo de descifrado DRM en consecuencia en el TVSDK para iOS. También puede anexar la etiqueta `faxs=1` en las URL de recursos HLS protegidos por DRM que estén destinadas a otras plataformas; se observa según sea necesario en iOS o se trata como una actividad no activa en reproductores en otras plataformas.

## Implemente Primetime DRM en una aplicación TSVDK {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM está integrado en TVSDK, que simplifica la implementación de la protección de contenido en una aplicación TVSDK.

Para obtener información general y detalles sobre el uso de Primetime DRM para implementar la protección de contenido en una aplicación TVSDK, consulte:

* [Flujo de trabajo TVSDK-DRM de Adobe Primetime (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)