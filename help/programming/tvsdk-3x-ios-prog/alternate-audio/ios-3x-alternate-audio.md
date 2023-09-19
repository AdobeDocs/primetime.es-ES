---
title: Audio alternativo
description: Audio alternativo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Audio alternativo {#alternate-audio}

El audio alternativo o de enlace tardío le permite alternar entre las pistas de audio disponibles para una pista de vídeo. De este modo, los usuarios pueden seleccionar una pista de idioma cuando se reproduce el vídeo.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Cuando TVSDK crea el `MediaPlayerItem` para el vídeo actual, crea un `AudioTrack` para cada pista de audio disponible. El elemento contiene un `name` propiedad, una cadena que generalmente contiene una descripción reconocible por el usuario del idioma de esa pista. El elemento también contiene información sobre si se debe utilizar esa pista de forma predeterminada.

Cuando sea el momento de reproducir el vídeo, puede solicitar una lista de pistas de audio disponibles, si lo desea, permitir que el usuario elija una y configurar el vídeo para que se reproduzca con la pista seleccionada.

Aunque no es habitual, si una pista de audio adicional está disponible después de que cree el `MediaPlayerItem`, TVSDK activa una `MediaPlayerItem.AUDIO_UPDATED` evento.

## API añadidas {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Se han agregado las siguientes API para admitir audio alternativo:

**hasAlternateAudio**

Si el medio especificado tiene una pista de audio alternativa que no sea la pista predeterminada, esta función booleana devuelve `true`. Si no hay pistas de audio alternativas, la función vuelve `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const { 
    return _hasAlternateAudio; 
}
```

**getAudioTracks**

Esta función devuelve la lista de todas las pistas de audio disponibles actualmente en un medio especificado.

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const { 
    if (_audioTracks) { 
        out = _audioTracks; 
        out->addRef(); 
        return kECSuccess; 
    } 
    return kECDataNotAvailable; 
} 
```

**getSelectedAudioTrack**

Esta función devuelve la pista de audio alternativa seleccionada actualmente y propiedades como el idioma. También se puede extraer la selección automática de pistas.

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const { 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

**selectAudioTrack**

Esta función selecciona la reproducción de una pista de audio alternativa.

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) { 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```
