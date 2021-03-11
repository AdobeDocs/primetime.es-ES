---
description: El audio alternativo le permite conmutar entre las pistas de audio disponibles para una pista de vídeo. Los usuarios pueden seleccionar la pista de idioma que prefieran cuando se reproduce el vídeo.
title: Audio alternativo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Información general {#alternate-audio-overview}

El audio alternativo le permite conmutar entre las pistas de audio disponibles para una pista de vídeo. Los usuarios pueden seleccionar la pista de idioma que prefieran cuando se reproduce el vídeo.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Cuando TVSDK crea la instancia `MediaPlayerItem` para el vídeo actual, crea un elemento `AudioTrack` para cada pista de audio disponible. El elemento contiene una propiedad `name`, que es una cadena que generalmente contiene una descripción reconocible por el usuario del idioma de esa pista. El elemento también contiene información sobre si usar esa pista de forma predeterminada. Cuando es hora de reproducir el vídeo, puede solicitar una lista de pistas de audio disponibles, opcionalmente permitir que el usuario seleccione una pista y configurar el vídeo para que se reproduzca con la pista seleccionada.

>[!TIP]
>
>Aunque no es habitual, si hay disponible una pista de audio adicional después de que TVSDK cree el `MediaPlayerItem`, TVSDK activa un evento `MediaPlayerItem.AUDIO_TRACK_UPDATED` .

## API agregadas {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Se han añadido las siguientes API para admitir audio alternativo:

**`hasAlternateAudio`**

Si el medio especificado tiene una pista de audio alternativa distinta de la predeterminada, esta función booleana devuelve `true`. Si no hay ninguna pista de audio alternativa, la función devuelve `false`.

```java
boolean hasAlternateAudio();
```

**`getAudioTracks`**

Esta función devuelve la lista de todas las pistas de audio disponibles actualmente en un medio especificado.

```java
List<AudioTrack> getAudioTracks();
```

**`getSelectedAudioTrack`**

Esta función devuelve la pista de audio alternativa seleccionada actualmente y propiedades como idioma. También se puede extraer la selección automática de la pista.

```java
AudioTrack getSelectedAudioTrack();
```

**`selectAudioTrack`**

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
