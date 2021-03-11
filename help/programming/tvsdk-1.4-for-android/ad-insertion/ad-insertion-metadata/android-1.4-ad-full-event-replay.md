---
description: La reproducción de eventos completos (FER) es un recurso de VOD que actúa como activo/DVR, por lo que la aplicación debe tomar medidas para garantizar que los anuncios se coloquen correctamente.
title: Habilitar anuncios en reproducción de eventos completos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# Habilitar anuncios en reproducción de eventos completos{#enable-ads-in-full-event-replay}

La reproducción de eventos completos (FER) es un recurso de VOD que actúa como activo/DVR, por lo que la aplicación debe tomar medidas para garantizar que los anuncios se coloquen correctamente.

Para el contenido en directo, TVSDK utiliza los metadatos/indicaciones del manifiesto para determinar dónde colocar los anuncios. Sin embargo, a veces el contenido en directo/lineal puede parecerse al contenido de VOD. Por ejemplo, cuando el contenido en directo se completa, se añade una etiqueta `EXT-X-ENDLIST` al manifiesto en directo. Para HLS, la etiqueta `EXT-X-ENDLIST` significa que el flujo es un flujo de VOD. TVSDK no puede diferenciar automáticamente este flujo de un flujo de VOD normal para insertar anuncios correctamente.

La aplicación debe indicar a TVSDK si el contenido está activo o VOD; para ello, especifique `AdSignalingMode`.

Para un flujo FER, el servidor de Adobe Primetime ad decisioning no debe proporcionar la lista de pausas publicitarias que deben insertarse en la cronología antes de iniciar la reproducción. Este es el proceso típico del contenido de VOD. En su lugar, al especificar un modo de señalización diferente, TVSDK lee todos los puntos de referencia del manifiesto FER y va al servidor de publicidad de cada punto de referencia para solicitar una pausa publicitaria. Este proceso es similar al contenido en directo/DVR.

Además de cada solicitud asociada a un punto de referencia, TVSDK realiza una solicitud de anuncio adicional para anuncios previos a la emisión.

1. Desde una fuente externa, como vCMS, obtenga el modo de señalización que debe utilizarse.
1. Cree los metadatos relacionados con la publicidad.
1. Si se debe sobrescribir el comportamiento predeterminado, especifique `AdSignalingMode` utilizando `AdvertisingMetadata.setSignalingMode`.

   Los valores válidos son `DEFAULT, SERVER_MAP` y `MANIFEST_CUES`.

   Debe establecer el modo de señalización de publicidad antes de llamar a `prepareToPlay`. Una vez que TVSDK empiece a resolver y a colocar anuncios en la cronología, se omiten los cambios en el modo de señalización de anuncios. Establezca el modo cuando cree el objeto `AuditudeSettings`.

1. Continúe con la reproducción.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->

