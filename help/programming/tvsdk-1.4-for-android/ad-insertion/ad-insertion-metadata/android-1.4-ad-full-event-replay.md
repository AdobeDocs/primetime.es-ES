---
description: La reproducción de eventos completos (FER) es un recurso de VOD que actúa como recurso de directo/DVR, por lo que la aplicación debe tomar los pasos necesarios para garantizar que los anuncios se coloquen correctamente.
seo-description: La reproducción de eventos completos (FER) es un recurso de VOD que actúa como recurso de directo/DVR, por lo que la aplicación debe tomar los pasos necesarios para garantizar que los anuncios se coloquen correctamente.
seo-title: Habilitar publicidades en la reproducción de eventos completos
title: Habilitar publicidades en la reproducción de eventos completos
uuid: 70e463bd-332c-4f91-ac05-03e79c0939a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Habilitar publicidades en la reproducción de eventos completos{#enable-ads-in-full-event-replay}

La reproducción de eventos completos (FER) es un recurso de VOD que actúa como recurso de directo/DVR, por lo que la aplicación debe tomar los pasos necesarios para garantizar que los anuncios se coloquen correctamente.

Para el contenido en directo, TVSDK utiliza los metadatos/indicaciones del manifiesto para determinar dónde colocar los anuncios. Sin embargo, a veces el contenido en directo o lineal puede parecerse al contenido de VOD. Por ejemplo, cuando se completa el contenido activo, se agrega una `EXT-X-ENDLIST` etiqueta al manifiesto activo. Para HLS, la `EXT-X-ENDLIST` etiqueta significa que el flujo es un flujo VOD. TVSDK no puede diferenciar automáticamente este flujo de un flujo de VOD normal para insertar correctamente anuncios.

La aplicación debe indicar a TVSDK si el contenido está activo o VOD especificando el `AdSignalingMode`.

Para un flujo FER, el servidor de decisiones y primetime de Adobe no debe proporcionar la lista de los saltos de publicidad que deben insertarse en la línea de tiempo antes de iniciar la reproducción. Este es el proceso habitual para el contenido de VOD. En su lugar, al especificar un modo de señalización diferente, TVSDK lee todos los puntos de referencia del manifiesto FER y va al servidor de publicidad para cada punto de referencia para solicitar una pausa publicitaria. Este proceso es similar al contenido en directo/DVR.

Además de cada solicitud asociada a un punto de referencia, TVSDK realiza una solicitud de publicidad adicional para anuncios previos.

1. Desde un origen externo, como vCMS, obtenga el modo de señalización que debe utilizarse.
1. Cree los metadatos relacionados con la publicidad.
1. Si se debe sobrescribir el comportamiento predeterminado, especifique el `AdSignalingMode` mediante `AdvertisingMetadata.setSignalingMode`.

   Los valores válidos son `DEFAULT, SERVER_MAP`, y `MANIFEST_CUES`.

   Debe establecer el modo de señalización de publicidad antes de llamar `prepareToPlay`. Después de que TVSDK empiece a resolver y colocar anuncios en la línea de tiempo, se omiten los cambios en el modo de señalización de publicidad. Establezca el modo cuando cree el `AuditudeSettings` objeto.

1. Continúe con la reproducción.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->

