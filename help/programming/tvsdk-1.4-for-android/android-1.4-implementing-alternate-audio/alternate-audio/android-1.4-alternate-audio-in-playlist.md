---
description: La lista de reproducción de un vídeo puede especificar un número ilimitado de pistas de audio alternativas para el contenido de vídeo principal. Por ejemplo, es posible que desee añadir diferentes idiomas al contenido de vídeo o permitir al usuario cambiar entre diferentes pistas en su dispositivo mientras se reproduce el contenido.
title: Pistas de audio alternativas en la lista de reproducción
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Pistas de audio alternativas en la lista de reproducción{#alternate-audio-tracks-in-the-playlist}

La lista de reproducción de un vídeo puede especificar un número ilimitado de pistas de audio alternativas para el contenido de vídeo principal. Por ejemplo, es posible que desee añadir diferentes idiomas al contenido de vídeo o permitir al usuario cambiar entre diferentes pistas en su dispositivo mientras se reproduce el contenido.

Las pistas de audio alternativas, o el audio de enlace en tiempo real, permiten a los usuarios cambiar entre pistas de varios idiomas para secuencias de vídeo HTTP (directo/lineal y VOD), y no es necesario modificar, duplicar ni volver a empaquetar el vídeo para cada pista de audio. Puede proporcionar varias pistas de idioma para un recurso de vídeo antes o después del empaquetado inicial del recurso.

>[!TIP]
>
>Para que el audio alternativo se mezcle con la pista de vídeo del medio principal, las marcas de tiempo de la pista alternativa deben coincidir con las marcas de tiempo del audio de la pista principal.

La pista de audio principal se incluye en la colección de pistas de audio con el `default` etiqueta. Los metadatos de los flujos de audio alternativos se incluyen en la lista de reproducción de `#EXT-X-MEDIA` etiquetas con `TYPE=AUDIO`.

Por ejemplo, un manifiesto M3U8 que especifica varios flujos de audio alternativos podría tener el siguiente aspecto:

```
#EXTM3U
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 1",
 AUTOSELECT=YES,DEFAULT=YES
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 2",
 AUTOSELECT=NO,DEFAULT=NO,URI="alternate_audio_aac/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="eng",URI="subtitles/eng/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English (Forced)",DEFAULT=YES,
 AUTOSELECT=YES,FORCED=YES,LANGUAGE="eng",URI="subtitles/eng_forced/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="Français",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="fra",URI="subtitles/fra/prog_index.m3u8"
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=263851,CODECS="mp4a.40.2, avc1.4d400d",
 RESOLUTION=416x234,AUDIO="bipbop_audio",SUBTITLES="subs" 
gear1/prog_index.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=577610,CODECS="mp4a.40.2, avc1.4d401e",
 RESOLUTION=640x360,AUDIO="bipbop_audio",SUBTITLES="subs"
gear2/prog_index.m3u8
...
```
