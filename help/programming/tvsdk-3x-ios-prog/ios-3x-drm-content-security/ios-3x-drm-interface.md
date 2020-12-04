---
description: Puede utilizar las funciones del sistema Primetime Digital Rights Management (DRM) para proporcionar un acceso seguro al contenido del vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como alternativa a la solución DRM integrada de Primetime de Adobe.
keywords: DRM;DASH;HLS
seo-description: Puede utilizar las funciones del sistema Primetime Digital Rights Management (DRM) para proporcionar un acceso seguro al contenido del vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como alternativa a la solución DRM integrada de Primetime de Adobe.
seo-title: Información general sobre la interfaz de DRM de Primetime
title: Información general sobre la interfaz de DRM de Primetime
uuid: 5e794147-cc58-448c-b8ec-065e80ef01fd
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# Información general de la interfaz DRM de Primetime {#primetime-drm-interface-overview}

Puede utilizar las funciones del sistema Primetime Digital Rights Management (DRM) para proporcionar un acceso seguro al contenido del vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como alternativa a la solución DRM integrada de Primetime de Adobe.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Consulte con su representante de Adobe la información más actualizada sobre la disponibilidad de soluciones DRM de terceros.

El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) Primetime es el Administrador de DRM.

Primetime DRM proporciona un flujo de trabajo escalable y eficaz para implementar la protección de contenido en aplicaciones TVSDK. Para proteger y administrar los derechos del contenido de vídeo, cree una licencia para cada archivo de medios digitales.

TVSDK admite la integración de DRM Primetime como flujos de trabajo DRM personalizados. Esto significa que la aplicación debe implementar los flujos de trabajo de autenticación DRM antes de reproducir el flujo mediante Flash DRMManager. Para habilitarlo, MediaPlayer le proporciona el administrador de DRM para la autenticación.

Consulte el código del reproductor de muestra DRM incluido en el paquete TVSDK.

Estos son los elementos de API más importantes para trabajar con DRM:

* Referencia en el reproductor de medios al objeto del administrador de DRM que implementa el subsistema de DRM:

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK emite una notificación `PTMediaPlayerItemDRMMetadataChanged` cuando cambian los metadatos de DRM. Estos metadatos se utilizan como entrada para casi todas las funciones de la clase `DRMManager`.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Si el flujo protegido por DRM está codificado con varias velocidades de bits (MBR), los metadatos DRM que se utilizan para la lista de reproducción variante deben ser los mismos que los metadatos que se utilizan en todos los flujos de velocidad de bits.

>[!TIP]
>
>Al hacer referencia a las URL de recursos protegidos por DRM en la aplicación de iOS, el parámetro de cadena de consulta `?faxs=1` debe añadirse a la URL M3U8 de nivel de conjunto (MBR). Por ejemplo:

```
https://your.domain.com/hls/[...]/index.m3u8?faxs=1
```

El parámetro de cadena de consulta `faxs=1` indica que el contenido está protegido con DRM y activa el flujo de trabajo de descifrado de DRM en consecuencia en el SDK de TVSDK para iOS. También puede anexar la etiqueta `faxs=1` en las URL de recursos HLS protegidos por DRM que estén destinadas a otras plataformas; se observa como requerido en iOS o se trata como no activo en reproductores en otras plataformas.

## Implementar Primetime DRM en una aplicación TSVDK {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM está integrado en TVSDK, que simplifica la implementación de la protección de contenido en una aplicación TVSDK.

Para obtener información general y detalles sobre el uso de Primetime DRM para implementar la protección de contenido en una aplicación TVSDK, consulte:

* [Flujo de trabajo de Adobe Primetime TVSDK-DRM (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)