---
description: El audio alternativo permite alternar entre las pistas de audio disponibles para una pista de vídeo. Los usuarios pueden seleccionar la pista de idioma que prefieran cuando se reproduzca el vídeo.
title: Audio alternativo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Información general {#alternate-audio-overview}

El audio alternativo permite alternar entre las pistas de audio disponibles para una pista de vídeo. Los usuarios pueden seleccionar la pista de idioma que prefieran cuando se reproduzca el vídeo.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Cuando TVSDK crea el `MediaPlayerItem` para el vídeo actual, crea un `AudioTrack` para cada pista de audio disponible. El elemento contiene un `name` propiedad, que es una cadena que generalmente contiene una descripción reconocible por el usuario del idioma de esa pista. El elemento también contiene información sobre si se debe utilizar esa pista de forma predeterminada. Cuando sea el momento de reproducir el vídeo, puede solicitar una lista de pistas de audio disponibles, si lo desea, permitir que el usuario seleccione una pista y configurar el vídeo para que se reproduzca con la pista seleccionada.

>[!TIP]
>
>Aunque no es habitual, si una pista de audio adicional está disponible después de que TVSDK cree la variable `MediaPlayerItem`, TVSDK activa una `MediaPlayerItem.AUDIO_TRACK_UPDATED` evento.

## API añadidas {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Se han agregado las siguientes API para admitir audio alternativo:

`hasAlternateAudio`

Si el medio especificado tiene una pista de audio alternativa que no sea la pista predeterminada, esta función booleana devuelve `true`. Si no hay pistas de audio alternativas, la función vuelve `false`.

```java
boolean hasAlternateAudio();
```

** `getAudioTracks`**

Esta función devuelve la lista de todas las pistas de audio disponibles actualmente en un medio especificado.

```java
List<AudioTrack> getAudioTracks();
```

`getSelectedAudioTrack`

Esta función devuelve la pista de audio alternativa seleccionada actualmente y propiedades como el idioma. También se puede extraer la selección automática de pistas.

```java
AudioTrack getSelectedAudioTrack();
```

`selectAudioTrack`

Esta función selecciona la reproducción de una pista de audio alternativa.

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
