---
description: El audio alternativo o de enlace tardío le permite alternar entre las pistas de audio disponibles para una pista de vídeo. De este modo, los usuarios pueden seleccionar una pista de idioma cuando se reproduce el vídeo.
seo-description: El audio alternativo o de enlace tardío le permite alternar entre las pistas de audio disponibles para una pista de vídeo. De este modo, los usuarios pueden seleccionar una pista de idioma cuando se reproduce el vídeo.
seo-title: Pistas de audio alternativas en la lista de reproducción
title: Pistas de audio alternativas en la lista de reproducción
uuid: 6241d3e4-6e07-44fb-bc0e-5d49d1a76824
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Pistas de audio alternativas en la lista de reproducción {#section_BC8C1C74A5A24A8CA68C1E7E721EE742}

La lista de reproducción de un vídeo puede especificar un número ilimitado de pistas de audio alternativas para el contenido del vídeo principal. Por ejemplo, es posible que desee agregar idiomas diferentes al contenido del vídeo o permitir que el usuario cambie entre distintas pistas del dispositivo mientras se reproduce el contenido.

Las pistas de audio alternativas, o el audio de enlace tardío, permiten a los usuarios cambiar entre varias pistas de idioma para flujos de vídeo HTTP (en directo/lineal y VOD) y no es necesario modificar, duplicado ni volver a empaquetar el vídeo para cada pista de audio. Puede proporcionar varias pistas de idioma para un recurso de vídeo antes o después del empaquetado inicial del recurso.

>[!TIP]
>
>Para que el audio alternativo se mezcle con la pista de vídeo del medio principal, las marcas de hora de la pista alternativa deben coincidir con las marcas de hora del audio de la pista principal.

Los siguientes requisitos se aplican si utiliza pistas de audio alternativas e incorpora publicidad:

* Si el contenido principal tiene pistas de audio alternativas, las publicidades deben tener al menos un flujo de solo audio.
* Cada duración de segmento del flujo de solo audio de un anuncio debe ser igual a la duración del segmento del flujo de vídeo de un anuncio.

La pista de audio principal se incluye en la colección de pistas de audio con la etiqueta `default`. Los metadatos de los flujos de audio alternativos se incluyen en la lista de reproducción de las etiquetas `#EXT-X-MEDIA` con `TYPE=AUDIO`.

Por ejemplo, un manifiesto M3U8 que especifica varios flujos de audio alternativos puede tener este aspecto:

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
