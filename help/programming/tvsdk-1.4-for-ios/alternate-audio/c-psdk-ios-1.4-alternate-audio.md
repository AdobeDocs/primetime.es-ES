---
description: El audio alternativo o de enlace tardío le permite conmutar entre las pistas de audio disponibles para una pista de vídeo. De este modo, los usuarios pueden seleccionar una pista de idioma cuando se reproduce el vídeo.
title: Audio alternativo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Información general {#alternate-audio-overview}

El audio alternativo o de enlace tardío le permite conmutar entre las pistas de audio disponibles para una pista de vídeo. De este modo, los usuarios pueden seleccionar una pista de idioma cuando se reproduce el vídeo.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Cuando TVSDK crea la instancia `MediaPlayerItem` para el vídeo actual, crea un elemento `AudioTrack` para cada pista de audio disponible. El elemento contiene una propiedad `name`, una cadena que generalmente contiene una descripción reconocible por el usuario del idioma de la pista. El elemento también contiene información sobre si usar esa pista de forma predeterminada.

Cuando es hora de reproducir el vídeo, puede solicitar una lista de pistas de audio disponibles, opcionalmente dejar que el usuario elija una y configurar el vídeo para que se reproduzca con la pista seleccionada.

Aunque no es habitual, si hay disponible una pista de audio adicional después de crear el `MediaPlayerItem`, TVSDK activa un evento `MediaPlayerItem.AUDIO_UPDATED`.

## API agregadas {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Se han añadido las siguientes API para admitir audio alternativo:

`hasAlternateAudio`

Si el medio especificado tiene una pista de audio alternativa distinta de la predeterminada, esta función booleana devuelve `true`. Si no hay ninguna pista de audio alternativa, la función devuelve `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const 
{ 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`**

Esta función devuelve la lista de todas las pistas de audio disponibles actualmente en un medio especificado.

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const 
    { 
        if (_audioTracks) 
        { 
            out = _audioTracks; 
            out->addRef(); 
            return kECSuccess; 
        } 
        return kECDataNotAvailable; 
    }
```

`getSelectedAudioTrack`

Esta función devuelve la pista de audio alternativa seleccionada actualmente y propiedades como idioma. También se puede extraer la selección automática de la pista.

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const 
{ 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

`selectAudioTrack`

Esta función selecciona una pista de audio alternativa para reproducir.

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) 
{ 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) 
    { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) 
        { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```

