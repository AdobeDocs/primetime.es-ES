---
description: Algunos anuncios de terceros (o creativos) no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime ad insertion y TVSDK pueden intentar opcionalmente volver a empaquetar anuncios incompatibles en vídeos M3U8 compatibles.
title: Reempaquetar anuncios incompatibles con el servicio de reempaquetado creativo de Adobe
exl-id: 8c3e5baf-1941-4330-a4b7-61ed623dfd5e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Reempaquetar anuncios incompatibles con el servicio de reempaquetado creativo de Adobe {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Algunos anuncios de terceros (o creativos) no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime ad insertion y TVSDK pueden intentar opcionalmente volver a empaquetar anuncios incompatibles en vídeos M3U8 compatibles.

Los anuncios ofrecidos por terceros, como un servidor de publicidad de una agencia, su partner de inventario o una red de publicidad, suelen entregarse en formatos incompatibles, como MP4 de descarga progresiva.

Cuando TVSDK encuentra por primera vez un anuncio incompatible, el reproductor ignora el anuncio y envía una solicitud al servicio de reempaquetado creativo (CRS), que forma parte del back-end de inserción de anuncios de Primetime, para que vuelva a empaquetar el anuncio en un formato compatible. CRS intenta generar varias representaciones M3U8 de velocidad de bits de la publicidad y almacena estas representaciones en la red de entrega de contenido de Primetime (CDN). La próxima vez que TVSDK reciba una respuesta de anuncio que apunte a ese anuncio, el reproductor utilizará la versión M3U8 compatible con HLS de la CDN.

Para habilitar esta función opcional, póngase en contacto con el representante del Adobe.

Para obtener más información sobre CRS, consulte [Servicio Creative Packaging (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Compatibilidad con varias CDN para la entrega de anuncios CRS{#multiple-cdn-support-for-crs-ad-delivery}

Aunque el escenario predeterminado del servicio de reempaquetado creativo (CRS) es utilizar una red de datos de contenido (CDN), puede implementar recursos CRS en más de una CDN.

Puede utilizar varias CDN por los siguientes motivos:

* Necesidad de ampliación para grandes eventos de visualización.
* Un requisito para hacer coincidir el origen de CDN del recurso CRS con el origen de CDN del contenido principal.

Puede transformar la URL predeterminada proporcionada por CRS mediante las API del transformador de URL de TVSDK.

Estas son las adiciones de la API en TVSDK:

* `URLTransformer` Una interfaz que describe los métodos necesarios para transformar el CRS y las direcciones URL que solicita TVSDK. Las aplicaciones pueden implementar esta interfaz y proporcionar implementaciones para los métodos necesarios.

* `DefaultURLTransformer` La instancia del transformador de URL predeterminada que se crea en TVSDK y que implementa `URLTransformer` interfaz. Las aplicaciones pueden anular esta clase o agregar un controlador de transformación de URL posterior. Este controlador es útil cuando la aplicación desea realizar cambios en la solicitud de URL después de aplicar la transformación predeterminada.

* `NetworkConfiguration.setURLTransformer` Un método de establecedor que se proporciona en la variable `NetworkConfiguration` instancia de metadatos para establecer `URLTransformer` implementación.

>[!IMPORTANT]
>
>Las implementaciones de la aplicación deben comprobar la `URLTransformerInputType` enumeración y solo transformar URL de tipo `URLTransformerInputType.CRSCreative` para CRS.

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
