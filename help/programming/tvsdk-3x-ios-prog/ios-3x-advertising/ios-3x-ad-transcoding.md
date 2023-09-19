---
description: Algunos anuncios de terceros (o creativos) no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime ad insertion y TVSDK pueden intentar opcionalmente volver a empaquetar anuncios incompatibles en vídeos M3U8 compatibles.
title: Reempaquetar anuncios incompatibles con el servicio de reempaquetado creativo de Adobe
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Reempaquetar anuncios incompatibles con el servicio de reempaquetado creativo de Adobe {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Algunos anuncios de terceros (o creativos) no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime ad insertion y TVSDK pueden intentar opcionalmente volver a empaquetar anuncios incompatibles en vídeos M3U8 compatibles.

Los anuncios ofrecidos por terceros, como un servidor de publicidad de una agencia, su partner de inventario o una red de publicidad, suelen entregarse en formatos incompatibles, como MP4 de descarga progresiva.

Cuando TVSDK encuentra por primera vez un anuncio incompatible, el reproductor ignora el anuncio y envía una solicitud al servicio de reempaquetado creativo (CRS), que forma parte del back-end de inserción de anuncios de Primetime, para que vuelva a empaquetar el anuncio en un formato compatible. CRS intenta generar varias representaciones M3U8 de velocidad de bits de la publicidad y almacena estas representaciones en la red de entrega de contenido de Primetime (CDN). La próxima vez que TVSDK reciba una respuesta de anuncio que apunte a ese anuncio, el reproductor utilizará la versión M3U8 compatible con HLS de la CDN.

Para habilitar esta función opcional, póngase en contacto con el representante del Adobe.

## Compatibilidad con varias CDN para la entrega de anuncios CRS {#section_900FDDA5454143718F1EB4C9732C8E1C}

Aunque el escenario predeterminado del servicio de reempaquetado creativo (CRS) es utilizar una red de datos de contenido (CDN), puede implementar recursos CRS en más de una CDN.

Puede utilizar varias CDN por los siguientes motivos:

* Necesidad de ampliación para grandes eventos de visualización.
* Un requisito para hacer coincidir el origen de CDN del recurso CRS con el origen de CDN del contenido principal.

Puede transformar la URL predeterminada proporcionada por CRS mediante las API del transformador de URL de TVSDK.

Estas son las adiciones de la API en TVSDK:

* `PTURLTransformer` Protocolo que describe los métodos necesarios para transformar el CRS y las direcciones URL que solicita TVSDK. Las aplicaciones pueden implementar este protocolo y proporcionar implementaciones para los métodos necesarios.

* `PTDefaultURLTransformer` La instancia del transformador de URL predeterminada que se crea en TVSDK y que implementa `PTURLTransformer` protocolo. Las aplicaciones pueden anular esta clase o agregar un controlador de transformación de URL posterior. Este controlador es útil cuando la aplicación desea realizar cambios en la solicitud de URL después de aplicar la transformación predeterminada.

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` Un método de establecedor que se proporciona en la variable `PTNetworkConfiguration` instancia de metadatos para establecer `PTURLTransformer` implementación.

>[!IMPORTANT]
>
>Las implementaciones de la aplicación deben comprobar la `PTURLTransformerInputType` enumeración y solo transformar URL de tipo `PTURLTransformerInputTypeCRSCreative` para CRS.

El siguiente ejemplo de código muestra cómo la aplicación puede cambiar el componente host predeterminado a una cadena diferente (por ejemplo, `cdn.mycrsdomain.com`):

```
// The sample code below uses Non-ARC code 
PTNetworkConfiguration *networkConfiguration = [[[PTNetworkConfiguration alloc] init] autorelease]; 
   
PTDefaultURLTransformer *defaultTransformer = [[[PTDefaultURLTransformer alloc] init] autorelease]; 
    [defaultTransformer addPostURLTransformHandler:^NSString *(NSString *url, PTURLTransformerInputType type) { 
        if (type == PTURLTransformerInputTypeCRSCreative) { 
            return [url stringByReplacingOccurrencesOfString:[NSURL URLWithString:url].host  
              withString:@"cdn.mycrsdomain.com"]; 
        } 
            return url; 
    }]; 
  
[networkConfiguration setURLTransformer:defaultTransformer]; 
   
// metadata is the PTMetadata instance set on a PTMediaPlayerItem instance. 
[metadata setMetadata:[self getNetworkConfiguration] forKey:PTNetworkConfigurationMetadataKey];
```
