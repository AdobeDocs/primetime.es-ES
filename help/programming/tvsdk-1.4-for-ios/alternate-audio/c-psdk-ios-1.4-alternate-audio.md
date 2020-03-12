---
description: El audio alternativo o de enlace tardío le permite alternar entre las pistas de audio disponibles para una pista de vídeo. De este modo, los usuarios pueden seleccionar una pista de idioma cuando se reproduce el vídeo.
seo-description: El audio alternativo o de enlace tardío le permite alternar entre las pistas de audio disponibles para una pista de vídeo. De este modo, los usuarios pueden seleccionar una pista de idioma cuando se reproduce el vídeo.
seo-title: Audio alternativo
title: Audio alternativo
uuid: 9dc3bec6-2135-4083-8db2-50a492e6bd67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Información general {#alternate-audio-overview}

El audio alternativo o de enlace tardío le permite alternar entre las pistas de audio disponibles para una pista de vídeo. De este modo, los usuarios pueden seleccionar una pista de idioma cuando se reproduce el vídeo.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Cuando TVSDK crea la `MediaPlayerItem` instancia para el vídeo actual, crea un `AudioTrack` elemento para cada pista de audio disponible. El elemento contiene una `name` propiedad, una cadena que generalmente contiene una descripción reconocible por el usuario del idioma de esa pista. El elemento también contiene información sobre si se utiliza esa pista de forma predeterminada.

Cuando es hora de reproducir el vídeo, puede solicitar una lista de las pistas de audio disponibles, dejar que el usuario elija una y configurar la reproducción del vídeo con la pista seleccionada.

Aunque no es habitual, si una pista de audio adicional está disponible después de crear el `MediaPlayerItem`, TVSDK activa un `MediaPlayerItem.AUDIO_UPDATED` evento.

## API agregadas {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Se han agregado las siguientes API para admitir audio alternativo:

`hasAlternateAudio`

Si el medio especificado tiene una pista de audio alternativa, distinta de la pista predeterminada, se devuelve esta función booleana `true`. Si no hay una pista de audio alternativa, la función devuelve `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const 
{ 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`**

Esta función devuelve una lista de todas las pistas de audio disponibles en un medio especificado.

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

Esta función devuelve la pista de audio alternativa seleccionada y propiedades como idioma. También se puede extraer la selección automática de la pista.

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

