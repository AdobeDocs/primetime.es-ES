---
description: El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) Primetime es el Administrador de DRM.
seo-description: El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) Primetime es el Administrador de DRM.
seo-title: Información general sobre la interfaz de DRM de Primetime
title: Información general sobre la interfaz de DRM de Primetime
uuid: 3aae7c7a-fd0c-430e-9018-fd72801ab778
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b

---


# Información general sobre la interfaz de DRM de Primetime {#primetime-drm-interface-overview}

Puede utilizar las funciones del sistema Primetime Digital Rights Management (DRM) para proporcionar un acceso seguro al contenido de vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como alternativa a la solución DRM integrada de Adobe Primetime.

Consulte con su representante de Adobe la información más actualizada sobre la disponibilidad de soluciones DRM de terceros.

El elemento clave del lado del cliente del sistema de administración de derechos digitales (DRM) Primetime es el Administrador de DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM proporciona un flujo de trabajo escalable y eficaz para implementar la protección de contenido en aplicaciones TVSDK. Para proteger y administrar los derechos del contenido de vídeo, cree una licencia para cada archivo de medios digitales.

TVSDK admite la integración de DRM Primetime como flujos de trabajo de DRM personalizados. Esto significa que la aplicación debe implementar los flujos de trabajo de autenticación DRM antes de reproducir el flujo mediante Flash DRMManager. Para habilitarlo, MediaPlayer le proporciona el administrador de DRM para la autenticación.

Consulte el código del reproductor de muestra DRM incluido en el paquete TVSDK.

Estos son los elementos de API más importantes para trabajar con DRM:

* Referencia en el reproductor de medios al objeto del administrador de DRM que implementa el subsistema de DRM:

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK emite una `PTMediaPlayerItemDRMMetadataChanged` notificación cuando cambian los metadatos de DRM. Estos metadatos se utilizan como entrada para casi todas las funciones de la `DRMManager` clase.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Si el flujo protegido por DRM está codificado con varias velocidades de bits (MBR), los metadatos DRM que se utilizan para la lista de reproducción variante deben ser los mismos que los metadatos que se utilizan en todos los flujos de velocidad de bits.

>[!TIP] {important=&quot;high&quot;}
>
>Al hacer referencia a direcciones URL de recursos protegidos por DRM en la aplicación de iOS, el parámetro de cadena de consulta `?faxs=1` debe agregarse a la dirección URL M3U8 de nivel de conjunto (MBR). Por ejemplo: >
>
```>
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```>
>The `faxs=1` query string parameter signals that the content is DRM protected, and triggers the DRM decryption workflow accordingly in the iOS TVSDK. You can also append the `faxs=1` tag on DRM-protected HLS asset URLs that are destined for other platforms; it is observed as required on iOS or treated as a non-op in players on other platforms.



<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Para obtener más información sobre DRM, consulte la documentación [de DRM de](https://help.adobe.com/en_US/primetime/drm)Adobe Primetime.

## Implementar Primetime DRM en una aplicación TSVDK {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM está integrado en TVSDK, que simplifica la implementación de la protección de contenido en una aplicación TVSDK.

Para obtener información general y detalles sobre el uso de Primetime DRM para implementar la protección de contenido en una aplicación TVSDK, consulte:

* [Flujo de trabajo de Adobe Primetime TVSDK-DRM (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)