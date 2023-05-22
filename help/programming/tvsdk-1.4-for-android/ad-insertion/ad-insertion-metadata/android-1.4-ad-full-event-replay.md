---
description: La reproducción de evento completo (FER) es un recurso de VOD que actúa como un recurso activo/DVR, por lo que la aplicación debe tomar medidas para garantizar que los anuncios se coloquen correctamente.
title: Habilitar los anuncios en la reproducción de evento completo
exl-id: d6f7efc9-48f4-4101-a425-c354557cdd4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Habilitar los anuncios en la reproducción de evento completo{#enable-ads-in-full-event-replay}

La reproducción de evento completo (FER) es un recurso de VOD que actúa como un recurso activo/DVR, por lo que la aplicación debe tomar medidas para garantizar que los anuncios se coloquen correctamente.

Para el contenido en directo, TVSDK utiliza los metadatos y las indicaciones del manifiesto para determinar dónde colocar los anuncios. Sin embargo, a veces el contenido en directo/lineal puede parecerse al contenido de VOD. Por ejemplo, cuando el contenido en directo termina, una `EXT-X-ENDLIST` la etiqueta se anexa al manifiesto en directo. Para HLS, la variable `EXT-X-ENDLIST` significa que el flujo es un flujo de VOD. TVSDK no puede diferenciar automáticamente este flujo de un flujo de VOD normal para insertar correctamente los anuncios.

La aplicación debe indicar a TVSDK si el contenido está activo o es VOD especificando la variable `AdSignalingMode`.

Para un flujo FER, el servidor de Adobe Primetime ad Decisioning no debe proporcionar la lista de pausas publicitarias que deben insertarse en la cronología antes de iniciar la reproducción. Este es el proceso típico del contenido de VOD. En su lugar, al especificar un modo de señalización diferente, TVSDK lee todos los puntos de referencia del manifiesto FER y va al servidor de publicidad para cada punto de referencia a fin de solicitar una pausa publicitaria. Este proceso es similar al contenido en directo/DVR.

Además de cada solicitud asociada a un punto de referencia, TVSDK realiza una solicitud de anuncio adicional para anuncios previos a la emisión.

1. Desde una fuente externa, como vCMS, obtenga el modo de señalización que debe utilizarse.
1. Cree los metadatos relacionados con la publicidad.
1. Si el comportamiento predeterminado debe sobrescribirse, especifique el `AdSignalingMode` mediante `AdvertisingMetadata.setSignalingMode`.

   Los valores válidos son `DEFAULT, SERVER_MAP`, y `MANIFEST_CUES`.

   Debe establecer el modo de señalización de anuncio antes de llamar a `prepareToPlay`. Una vez que TVSDK empieza a resolver y a colocar los anuncios en la cronología, se omiten los cambios en el modo de señalización de publicidad. Configure el modo cuando cree la variable `AuditudeSettings` objeto.

1. Continuar con la reproducción.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->
