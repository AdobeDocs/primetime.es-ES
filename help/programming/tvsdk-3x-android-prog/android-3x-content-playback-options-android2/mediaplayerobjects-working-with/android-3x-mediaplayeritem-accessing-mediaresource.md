---
description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
seo-description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
seo-title: Métodos de MediaPlayerItem para acceder a la información de MediaResource
title: Métodos de MediaPlayerItem para acceder a la información de MediaResource
uuid: 46845583-0a76-4411-a8bc-0a16ebfe8e6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Métodos de MediaPlayerItem para acceder a la información de MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.

| Método | Descripción |
|--- |--- |
| **Etiquetas de publicidad** |  |
| List`<String>` getAdTags() | Proporciona la lista de etiquetas de publicidad que se utilizan para el proceso de colocación de la publicidad. |
| **Flujo en vivo** |  |
| boolean isLive(); | True si el flujo está activo; false si es VOD. |
| **DRM protegido** |  |
| boolean isProtected(); | True si el flujo está protegido con DRM. |
| List`<DRMMetadataInfo>` getDRMMetadataInfos(); | Enumera todos los objetos de metadatos DRM detectados en el manifiesto. |
| **Subtítulos opcionales** |  |
| boolean hasClosedCaptions(); | True si hay pistas de subtítulos opcionales disponibles. |
| List`<ClosedCaptionsTrack>` getClosedCationsTracks(); | Proporciona una lista de las pistas de subtítulos opcionales disponibles. |
| ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); | Recupera la pista de subtítulos opcionales actual seleccionada con SelectClosedCaptionsTrack . |
| selectClosedCaptionsTrack (ClosedCaptionsTrack ClosedCaptionsTrack) | Define una pista de subtítulos cerrados como la pista de subtítulos opcionales actual. |
| **Pistas de audio alternativas** |  |
| boolean hasAlternateAudio(); | True si el flujo tiene pistas de audio alternativas. Nota:  La pista de audio principal (predeterminada) también forma parte de la lista de pistas de audio alternativas.  TVSDK para Android considera que la pista de audio principal es uno de los elementos de la lista de pistas de audio alternativas. Debido a esto, el único caso en el que MediaPlayerItem.hasAlternateAudio devuelve false es cuando el flujo no tiene audio. Si el contenido solo tiene una pista de audio, este método devuelve true y `MediaPlayerItem.getAudioTracks` devuelve una lista con un solo elemento (la pista de audio predeterminada). |
| List`<AudioTrack>` getAudioTracks(); | Proporciona una lista de pistas de audio alternativas disponibles. |
| AudioTrack getSelectedAudioTrack(); | Recupera la pista de audio seleccionada con selectAudioTrack . |
| selectAudioTrack ( AudioTrack audioTrack ) | Selecciona una pista de audio para que sea la pista de audio actual. |
| **Metadatos temporizados** |  |
| boolean hasTimedMetadata(); | True si el flujo tiene metadatos temporizados asociados. |
| List`<TimedMetadata>` getTimedMetadata(); | Proporciona una lista de los objetos de metadatos temporizados asociados al flujo. |
| **Varios perfiles (velocidades de bits)** |
| boolean isDynamic(); | True si el flujo es un flujo de velocidad de bits múltiple (MBR). |
| List`<Profile>` getProfiles(); | Proporciona una lista de los perfiles de velocidad de bits asociados. Para cada perfil, puede recuperar su velocidad de bits y la altura y anchura del perfil. |
| Perfil getSelectedProfile() | Recupera el perfil seleccionado actualmente. |
| **Juego de trucos** |  |
| boolean isTrickPlaySupported(); | True si el reproductor admite avance rápido, rebobinado y reanudación. |
| List`< Float>` getAvailablePlaybackRates() | Proporciona la lista de las tasas de reproducción disponibles en el contexto de la función de reproducción mediante trucos. |
| Float getSelectedPlaybackRate() | Recupera la velocidad de reproducción seleccionada actualmente. |
| MediaPlayerItemConfig getConfig() | Devuelve la instancia de MediaPlayerItemConfig asociada a este elemento. |
| **Recurso multimedia** |  |
| MediaResource getResource(); | Devuelve el recurso de medios asociado a este elemento. |
| int getResourceId() | Devuelve el identificador de medios asociado a este elemento. Este ID se establece cuando el elemento se carga mediante MediaPlayerItemLoader.load. |