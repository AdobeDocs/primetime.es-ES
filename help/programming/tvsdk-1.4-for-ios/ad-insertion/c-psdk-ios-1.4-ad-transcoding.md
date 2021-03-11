---
description: Algunos anuncios (o elementos creativos) de terceros no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo es incompatible con HLS. La inserción de anuncios de Primetime y TVSDK pueden, opcionalmente, intentar volver a empaquetar anuncios incompatibles en vídeos compatibles de M3U8.
title: Volver a empaquetar anuncios incompatibles mediante el servicio de reempaquetado creativo de Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Volver a empaquetar anuncios incompatibles mediante el servicio de reempaquetado creativo de Adobe{#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Algunos anuncios (o elementos creativos) de terceros no se pueden vincular al flujo de contenido HTTP Live Streaming (HLS) porque su formato de vídeo es incompatible con HLS. La inserción de anuncios de Primetime y TVSDK pueden, opcionalmente, intentar volver a empaquetar anuncios incompatibles en vídeos compatibles de M3U8.

Los anuncios publicados por terceros, como un servidor de publicidad de agencia, su socio de inventario o una red de publicidad, suelen entregarse en formatos incompatibles, como MP4 de descarga progresiva.

Cuando TVSDK encuentra por primera vez un anuncio incompatible, el reproductor ignora el anuncio y envía una solicitud al servicio de reempaquetado creativo (CRS), que forma parte del back-end de inserción de anuncio de Primetime, para volver a empaquetar el anuncio en un formato compatible. CRS intenta generar representaciones M3U8 de tasa de bits múltiple del anuncio y almacena estas representaciones en la red de entrega de contenido (CDN) de Primetime. La próxima vez que TVSDK reciba una respuesta de anuncio que apunte a ese anuncio, el reproductor utilizará la versión M3U8 compatible con HLS de la CDN.

Para habilitar esta función opcional, póngase en contacto con el representante de su Adobe.

Para obtener más información sobre CRS, consulte [Servicio de paquete creativo (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Compatibilidad con múltiples CDN para el envío de anuncios CRS {#section_900FDDA5454143718F1EB4C9732C8E1C}

Aunque el escenario predeterminado del servicio de reempaquetado creativo (CRS) es utilizar una red de datos de contenido (CDN), puede implementar recursos CRS en más de una CDN.

Puede utilizar varias CDN por los siguientes motivos:

* Requisito de ampliación para eventos de visualización grandes.
* Requisito para hacer coincidir la fuente de CDN del recurso CRS con la fuente de CDN del contenido principal.

Puede transformar la URL predeterminada que proporciona el CRS mediante las API de transformador de URL del TVSDK.

Estas son las adiciones a la API en TVSDK:

* `PTURLTransformer` Protocolo que describe los métodos necesarios para transformar las URL de anuncio CRS que solicita TVSDK. Las aplicaciones pueden implementar este protocolo y proporcionar implementaciones para los métodos requeridos.

* `PTDefaultURLTransformer` Instancia de transformador de URL predeterminada que se crea en TVSDK y que implementa el  `PTURLTransformer` protocolo . Las aplicaciones pueden anular esta clase o agregar un controlador de transformación de URL posterior. Este controlador es útil cuando la aplicación desea realizar cambios en la solicitud de URL después de aplicar la transformación predeterminada.

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` Método de configuración que se proporciona en la instancia de  `PTNetworkConfiguration` metadatos para establecer la  `PTURLTransformer` implementación.

>[!IMPORTANT]
>
>Las implementaciones de la aplicación deben comprobar la enumeración `PTURLTransformerInputType` y solo transformar las URL de tipo `PTURLTransformerInputTypeCRSCreative` para CRS.

El siguiente ejemplo de código muestra cómo la aplicación puede cambiar el componente de host predeterminado a una cadena diferente (por ejemplo, `cdn.mycrsdomain.com`):

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

