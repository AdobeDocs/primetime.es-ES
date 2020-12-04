---
description: El audio alternativo permite cambiar entre las pistas de audio disponibles para una pista de vídeo. Los usuarios pueden seleccionar la pista de idioma que prefieran cuando se reproduce el vídeo.
seo-description: El audio alternativo permite cambiar entre las pistas de audio disponibles para una pista de vídeo. Los usuarios pueden seleccionar la pista de idioma que prefieran cuando se reproduce el vídeo.
seo-title: Audio alternativo
title: Audio alternativo
uuid: d1af1ea9-2516-4835-baff-3577ad5b705e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Información general {#alternate-audio-overview}

El audio alternativo permite cambiar entre las pistas de audio disponibles para una pista de vídeo. Los usuarios pueden seleccionar la pista de idioma que prefieran cuando se reproduce el vídeo.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Cuando TVSDK crea la instancia `MediaPlayerItem` para el vídeo actual, crea un elemento `AudioTrack` para cada pista de audio disponible. El elemento contiene una propiedad `name`, que es una cadena que generalmente contiene una descripción reconocible por el usuario del idioma de esa pista. El elemento también contiene información sobre si se utiliza esa pista de forma predeterminada. Cuando es hora de reproducir el vídeo, puede solicitar una lista de las pistas de audio disponibles, si lo desea, permitir al usuario seleccionar una pista y configurar el vídeo para que se reproduzca con la pista seleccionada.

>[!TIP]
>
>Aunque no es habitual, si hay disponible una pista de audio adicional después de que TVSDK cree el `MediaPlayerItem`, TVSDK activa un evento `MediaPlayerItem.AUDIO_TRACK_UPDATED`.

## API añadidas {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Se han agregado las siguientes API para admitir audio alternativo:

**`hasAlternateAudio`**

Si el medio especificado tiene una pista de audio alternativa, distinta de la pista predeterminada, esta función booleana devuelve `true`. Si no hay una pista de audio alternativa, la función devuelve `false`.

```java
boolean hasAlternateAudio();
```

**`getAudioTracks`**

Esta función devuelve la lista de todas las pistas de audio disponibles en un medio especificado.

```java
List<AudioTrack> getAudioTracks();
```

**`getSelectedAudioTrack`**

Esta función devuelve la pista de audio alternativa seleccionada y propiedades como idioma. También se puede extraer la selección automática de la pista.

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
