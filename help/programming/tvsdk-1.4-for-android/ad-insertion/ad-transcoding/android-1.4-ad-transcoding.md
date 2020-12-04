---
description: Algunos anuncios (o elementos creativos) de terceros no se pueden incluir en el flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime y TVSDK pueden intentar, opcionalmente, volver a empaquetar anuncios incompatibles en vídeos compatibles con M3U8.
seo-description: Algunos anuncios (o elementos creativos) de terceros no se pueden incluir en el flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime y TVSDK pueden intentar, opcionalmente, volver a empaquetar anuncios incompatibles en vídeos compatibles con M3U8.
seo-title: Volver a empaquetar anuncios incompatibles con el servicio de reempaquetado de Adobe Creative
title: Volver a empaquetar anuncios incompatibles con el servicio de reempaquetado de Adobe Creative
uuid: eea3651f-2598-4efa-ba4d-dbd7afa7cb95
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Volver a empaquetar anuncios incompatibles con el servicio de reempaquetado creativo de Adobe {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Algunos anuncios (o elementos creativos) de terceros no se pueden incluir en el flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime y TVSDK pueden intentar, opcionalmente, volver a empaquetar anuncios incompatibles en vídeos compatibles con M3U8.

Las publicidades que se proporcionan desde varios terceros, como un servidor de publicidad de agencia, su socio de inventario o una red de publicidad, se entregan a menudo en formatos incompatibles, como el MP4 de descarga progresiva.

Cuando TVSDK encuentra por primera vez una publicidad incompatible, el reproductor ignora la publicidad y envía una solicitud al servicio creativo de reempaquetado (CRS), que forma parte del back-end de inserción y Primetime, para volver a empaquetar la publicidad en un formato compatible. CRS intenta generar representaciones M3U8 de velocidad de bits múltiple del anuncio y almacena estas representaciones en la red de Envío de contenido (CDN) de Primetime. La próxima vez que TVSDK reciba una respuesta de publicidad que apunte a esa publicidad, el reproductor utilizará la versión M3U8 compatible con HLS de la CDN.

Para activar esta función opcional, póngase en contacto con el representante de Adobe.

Para obtener más información sobre CRS, consulte [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Compatibilidad de varios CDN con CRS y envío{#multiple-cdn-support-for-crs-ad-delivery}

Si bien el escenario predeterminado del servicio de reempaquetado creativo (CRS) es utilizar una red de datos de contenido (CDN), puede implementar recursos CRS en más de una CDN.

Puede utilizar varias CDN por las siguientes razones:

* Requisito de ampliación para eventos de visualización grandes.
* Requisito para hacer coincidir el origen CDN del recurso CRS con el origen CDN del contenido principal.

Puede transformar la URL predeterminada proporcionada por el CRS mediante las API de transformador de URL de TVSDK.

Estas son las adiciones a la API en TVSDK:

* `URLTransformer` Interfaz que describe los métodos necesarios para transformar las URL de anuncios CRS solicitadas por TVSDK. Las aplicaciones pueden implementar esta interfaz y proporcionar implementaciones para los métodos requeridos.

* `DefaultURLTransformer` La instancia de transformador de URL predeterminada que se crea en TVSDK y que implementa la  `URLTransformer` interfaz. Las aplicaciones pueden anular esta clase o agregar un controlador de transformación de URL de anuncio. Este controlador es útil cuando la aplicación desea realizar cambios en la solicitud de URL después de aplicar la transformación predeterminada.

* `NetworkConfiguration.setURLTransformer` Método setter que se proporciona en la instancia de  `NetworkConfiguration` metadatos para establecer la  `URLTransformer` implementación.

>[!IMPORTANT]
>
>Las implementaciones de la aplicación deben buscar la lista desglosada `URLTransformerInputType` y transformar solo las direcciones URL de tipo `URLTransformerInputType.CRSCreative` para CRS.

El siguiente ejemplo de código muestra cómo la aplicación puede cambiar el componente host predeterminado a una cadena diferente (por ejemplo, `cdn.mycrsdomain.com`):

```java
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
DefaultURLTransformer urlTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(new DefaultURLTransformer.URLTransformHandler() { 
    @Override 
    public String call(String url, URLTransformerInputType type) { 
        if (type == URLTransformerInputType.CRSCreative) { 
            try { 
                return url.replaceAll(new java.net.URI(url).getHost(), "cdn.mycrsdomain.com"); 
            } catch (URISyntaxException e) { 
            } 
        } 
        return url; 
    } 
}); 
   
networkConfiguration.setURLTransformer(urlTransformer); 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(), networkConfiguration);
```
