---
description: El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) de Primetime es el Administrador de DRM.
title: Información general sobre la interfaz DRM Primetime
exl-id: dee420cf-8aad-42e8-965d-9fd9395f2c45
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Información general sobre la interfaz DRM Primetime {#primetime-drm-interface-overview}

Puede utilizar las funciones del sistema de Digital Rights Management de Primetime (DRM) para proporcionar acceso seguro al contenido de vídeo. Como alternativa, puede utilizar soluciones de DRM de terceros como alternativa a la solución de DRM de Primetime integrada de Adobe.

Consulte con su representante de Adobes la información más actualizada sobre la disponibilidad de soluciones de DRM de terceros.

El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) de Primetime es el Administrador de DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM proporciona un flujo de trabajo escalable y eficaz para implementar la protección de contenido en aplicaciones TVSDK. Protege y administra los derechos del contenido de vídeo creando una licencia para cada archivo multimedia digital.

TVSDK admite la integración de DRM de Primetime como flujos de trabajo de DRM personalizados. Esto significa que la aplicación debe implementar los flujos de trabajo de autenticación DRM antes de reproducir el flujo mediante el Flash Administrador DRM. Para habilitar esto, MediaPlayer le proporciona el administrador de DRM para la autenticación.

Consulte el código del reproductor de muestras DRM incluido en el paquete TVSDK.

Estos son los elementos de API más importantes para trabajar con DRM:

* Referencia en el reproductor de contenido al objeto del administrador de DRM que implementa el subsistema de DRM:

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

Problemas de TVSDK a `PTMediaPlayerItemDRMMetadataChanged` notificación cuando cambian los metadatos de DRM. Estos metadatos se utilizan como entrada para casi todas las funciones del `DRMManager` clase.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Si el flujo protegido por DRM tiene codificación de tasa de bits múltiple (MBR), los metadatos DRM que se utilizan para la lista de reproducción de variante deben ser los mismos que los metadatos que se utilizan en todos los flujos de tasa de bits.

>[!TIP]
>
>Al hacer referencia a direcciones URL de recursos protegidos por DRM en la aplicación de iOS, el parámetro de cadena de consulta `?faxs=1` debe añadirse a la URL M3U8 de nivel de conjunto (MBR). Por ejemplo:
>
>
```
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```
>
>El `faxs=1` El parámetro de cadena de consulta indica que el contenido está protegido por DRM y almacena en déclencheur el flujo de trabajo de descifrado de DRM en consecuencia en el TVSDK de iOS. También puede anexar el `faxs=1` en URL de recursos HLS protegidos por DRM que están destinados a otras plataformas; se observa como obligatorio en iOS o se trata como una operación no operativa en reproductores de otras plataformas.

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obtener más información sobre DRM, consulte la [Documentación de Adobe Primetime DRM](https://help.adobe.com/en_US/primetime/drm).

## Implementación de DRM de Primetime en una aplicación TSVDK {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM está integrado en TVSDK, lo que simplifica la implementación de la protección de contenido en una aplicación TVSDK.

Para obtener información general y detalles sobre el uso de Primetime DRM para implementar la protección de contenido en una aplicación TVSDK, consulte:

* [Flujo de trabajo TVSDK-DRM de Adobe Primetime (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)
