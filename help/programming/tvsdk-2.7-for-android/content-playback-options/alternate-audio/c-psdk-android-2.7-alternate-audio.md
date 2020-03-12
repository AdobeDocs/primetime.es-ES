---
description: El audio alternativo permite cambiar entre las pistas de audio disponibles para una pista de vídeo. Los usuarios pueden seleccionar la pista de idioma que prefieran cuando se reproduce el vídeo.
seo-description: El audio alternativo permite cambiar entre las pistas de audio disponibles para una pista de vídeo. Los usuarios pueden seleccionar la pista de idioma que prefieran cuando se reproduce el vídeo.
seo-title: Audio alternativo
title: Audio alternativo
uuid: 86aa5393-6a9e-49db-807b-7299e6b4ab2b
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Información general {#alternate-audio-overview}

El audio alternativo permite cambiar entre las pistas de audio disponibles para una pista de vídeo. Los usuarios pueden seleccionar la pista de idioma que prefieran cuando se reproduce el vídeo.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Cuando TVSDK crea la `MediaPlayerItem` instancia para el vídeo actual, crea un `AudioTrack` elemento para cada pista de audio disponible. El elemento contiene una `name` propiedad, que es una cadena que generalmente contiene una descripción reconocible por el usuario del idioma de esa pista. El elemento también contiene información sobre si se utiliza esa pista de forma predeterminada. Cuando es hora de reproducir el vídeo, puede solicitar una lista de las pistas de audio disponibles, si lo desea, permitir al usuario seleccionar una pista y configurar el vídeo para que se reproduzca con la pista seleccionada.

>[!TIP]
>
>Aunque no es habitual, si una pista de audio adicional está disponible después de que TVSDK cree el `MediaPlayerItem`, TVSDK activa un `MediaPlayerItem.AUDIO_TRACK_UPDATED` evento.

## API agregadas {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Se han agregado las siguientes API para admitir audio alternativo:

`hasAlternateAudio`

Si el medio especificado tiene una pista de audio alternativa, distinta de la pista predeterminada, se devuelve esta función booleana `true`. Si no hay una pista de audio alternativa, la función devuelve `false`.

```java
boolean hasAlternateAudio();
```

** `getAudioTracks`**

Esta función devuelve una lista de todas las pistas de audio disponibles en un medio especificado.

```java
List<AudioTrack> getAudioTracks();
```

`getSelectedAudioTrack`

Esta función devuelve la pista de audio alternativa seleccionada y propiedades como idioma. También se puede extraer la selección automática de la pista.

```java
AudioTrack getSelectedAudioTrack();
```

`selectAudioTrack`

Esta función selecciona una pista de audio alternativa para reproducir.

```java
void selectAudioTrack(AudioTrack audioTrack);
```

Por ejemplo:

```java
private void onPrepared() { 
    // Select the AA track in PREPARED State 
    boolean hasAlternateAudio = _mediaPlayer.getCurrentItem().hasAlternateAudio(); 
    if(hasAlternateAudio) { 
        AudioTrack selectedAudioTrack =  
          _mediaPlayer.getCurrentItem().getSelectedAudioTrack(); 
 
        if (selectedAudioTrack == null) {  
            // Selecting default audio track  
            // If index is 1 it will select alternate audio track  
            selectedAudioTrack = _mediaPlayer.getCurrentItem().getAudioTracks().get(0);  
        } 
    } 
    _mediaPlayer.getCurrentItem().selectAudioTrack(selectedAudioTrack); 
} 
```

