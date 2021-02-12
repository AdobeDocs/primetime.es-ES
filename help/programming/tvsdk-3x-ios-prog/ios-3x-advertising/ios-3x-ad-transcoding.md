---
description: Algunos anuncios (o elementos creativos) de terceros no se pueden incluir en el flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime y TVSDK pueden intentar, opcionalmente, volver a empaquetar anuncios incompatibles en vídeos compatibles con M3U8.
seo-description: Algunos anuncios (o elementos creativos) de terceros no se pueden incluir en el flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime y TVSDK pueden intentar, opcionalmente, volver a empaquetar anuncios incompatibles en vídeos compatibles con M3U8.
seo-title: Volver a empaquetar anuncios incompatibles con el servicio de reempaquetado de Adobe Creative
title: Volver a empaquetar anuncios incompatibles con el servicio de reempaquetado de Adobe Creative
uuid: 56a2405d-b395-4fea-820d-343590be7c19
translation-type: tm+mt
source-git-commit: cecc559480b9b52c412fefff4361603d6f14caf7
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Volver a empaquetar anuncios incompatibles con el servicio de reempaquetado creativo de Adobe {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Algunos anuncios (o elementos creativos) de terceros no se pueden incluir en el flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo no es compatible con HLS. Primetime y TVSDK pueden intentar, opcionalmente, volver a empaquetar anuncios incompatibles en vídeos compatibles con M3U8.

Las publicidades que se proporcionan desde varios terceros, como un servidor de publicidad de agencia, su socio de inventario o una red de publicidad, se entregan a menudo en formatos incompatibles, como el MP4 de descarga progresiva.

Cuando TVSDK encuentra por primera vez una publicidad incompatible, el reproductor ignora la publicidad y envía una solicitud al servicio creativo de reempaquetado (CRS), que forma parte del back-end de inserción y Primetime, para volver a empaquetar la publicidad en un formato compatible. CRS intenta generar representaciones M3U8 de velocidad de bits múltiple del anuncio y almacena estas representaciones en la red de Envío de contenido (CDN) de Primetime. La próxima vez que TVSDK reciba una respuesta de publicidad que apunte a esa publicidad, el reproductor utilizará la versión M3U8 compatible con HLS de la CDN.

Para activar esta función opcional, póngase en contacto con el representante de Adobe.

## Compatibilidad con varios CDN para el envío de anuncios de CRS {#section_900FDDA5454143718F1EB4C9732C8E1C}

Si bien el escenario predeterminado del servicio de reempaquetado creativo (CRS) es utilizar una red de datos de contenido (CDN), puede implementar recursos CRS en más de una CDN.

Puede utilizar varias CDN por las siguientes razones:

* Requisito de ampliación para eventos de visualización grandes.
* Requisito para hacer coincidir el origen CDN del recurso CRS con el origen CDN del contenido principal.

Puede transformar la URL predeterminada proporcionada por el CRS mediante las API de transformador de URL de TVSDK.

Estas son las adiciones a la API en TVSDK:

* `PTURLTransformer` Protocolo que describe los métodos necesarios para transformar las direcciones URL de anuncios CRS solicitadas por TVSDK. Las aplicaciones pueden implementar este protocolo y proporcionar implementaciones para los métodos requeridos.

* `PTDefaultURLTransformer` La instancia de transformador de URL predeterminada que se crea en TVSDK y que implementa el  `PTURLTransformer` protocolo. Las aplicaciones pueden anular esta clase o agregar un controlador de transformación de URL de anuncio. Este controlador es útil cuando la aplicación desea realizar cambios en la solicitud de URL después de aplicar la transformación predeterminada.

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` Método setter que se proporciona en la instancia de  `PTNetworkConfiguration` metadatos para establecer la  `PTURLTransformer` implementación.

>[!IMPORTANT]
>
>Las implementaciones de la aplicación deben buscar la lista desglosada `PTURLTransformerInputType` y transformar solo las direcciones URL de tipo `PTURLTransformerInputTypeCRSCreative` para CRS.

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
