---
description: Algunos anuncios (o elementos creativos) de terceros no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo es incompatible con HLS. La inserción de anuncios de Primetime y TVSDK pueden, opcionalmente, intentar volver a empaquetar anuncios incompatibles en vídeos compatibles de M3U8.
title: Volver a empaquetar anuncios incompatibles mediante el servicio de reempaquetado creativo de Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Volver a empaquetar anuncios incompatibles mediante el servicio de reempaquetado creativo de Adobe {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Algunos anuncios (o elementos creativos) de terceros no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo es incompatible con HLS. La inserción de anuncios de Primetime y TVSDK pueden, opcionalmente, intentar volver a empaquetar anuncios incompatibles en vídeos compatibles de M3U8.

Los anuncios publicados por terceros, como un servidor de publicidad de agencia, su socio de inventario o una red de publicidad, suelen entregarse en formatos incompatibles, como MP4 de descarga progresiva.

Cuando TVSDK encuentra por primera vez un anuncio incompatible, el reproductor ignora el anuncio y envía una solicitud al servicio de reempaquetado creativo (CRS), que forma parte del back-end de inserción de anuncio de Primetime, para volver a empaquetar el anuncio en un formato compatible. CRS intenta generar representaciones M3U8 de tasa de bits múltiple del anuncio y almacena estas representaciones en la red de entrega de contenido (CDN) de Primetime. La próxima vez que TVSDK reciba una respuesta de anuncio que apunte a ese anuncio, el reproductor utilizará la versión M3U8 compatible con HLS de la CDN.

Para habilitar esta función opcional, póngase en contacto con el representante de su Adobe.

Para obtener más información sobre CRS, consulte [Servicio de paquete creativo (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Compatibilidad con múltiples CDN para el envío de anuncios CRS {#multiple-cdn-support-for-crs-ad-delivery}

Aunque el escenario predeterminado del servicio de reempaquetado creativo (CRS) es utilizar una red de datos de contenido (CDN), puede implementar recursos CRS en más de una CDN.

Puede utilizar varias CDN por los siguientes motivos:

* Requisito de ampliación para eventos de visualización grandes.
* Requisito para hacer coincidir la fuente de CDN del recurso CRS con la fuente de CDN del contenido principal.

Puede transformar la URL predeterminada que proporciona el CRS mediante las API de transformador de URL del TVSDK.

Estas son las adiciones a la API en TVSDK:

* `URLTransformer` Una interfaz que describe los métodos necesarios para transformar las URL de anuncio CRS solicitadas por TVSDK. Las aplicaciones pueden implementar esta interfaz y proporcionar implementaciones para los métodos requeridos.

* `DefaultURLTransformer` Instancia de transformador de URL predeterminada que se crea en TVSDK y que implementa la  `URLTransformer` interfaz . Las aplicaciones pueden anular esta clase o agregar un controlador de transformación de URL posterior. Este controlador es útil cuando la aplicación desea realizar cambios en la solicitud de URL después de aplicar la transformación predeterminada.

* `NetworkConfiguration.urlTransformer` Método de configuración que se proporciona en la instancia de  `NetworkConfiguration` metadatos para establecer la  `URLTransformer` implementación.

>[!IMPORTANT]
>
>Las implementaciones de la aplicación deben comprobar la enumeración `URLTransformerInputType` y solo transformar las URL de tipo `URLTransformerInputType.CRSCreative` para CRS.

El siguiente ejemplo de código muestra cómo la aplicación puede cambiar el componente de host predeterminado a una cadena diferente (por ejemplo, `cdn.mycrsdomain.com`):

```
var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   
var urlTransformer:DefaultURLTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(function (url:String, type:String) { 
    if (type == URLTransformerInputType.CRSCreative) { 
        return url.replace(URLUtil.getServerName(url), "cdn.mycrsdomain.com"); 
    } 
    return url; 
}); 
  
networkConfiguration.urlTransformer = urlTransformer; 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                     networkConfiguration);
```
