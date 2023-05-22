---
description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
title: Métodos MediaPlayerItem para acceder a la información de MediaResource
exl-id: d6a547f3-0267-4a49-93a4-628b4879aef4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Métodos MediaPlayerItem para acceder a la información de MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.

| Método | Descripción |
|--- |--- |
| **Etiquetas de publicidad** |  |
| Lista`<String>` getAdTags() | Proporciona la lista de etiquetas de anuncio que se utilizan en el proceso de colocación de anuncios. |
| **Emisión en directo** |  |
| booleano isLive(); | True si el flujo está activo; False si es VOD. |
| **Protegido por DRM** |  |
| booleano isProtected(); | True si el flujo está protegido mediante DRM. |
| Lista`<DRMMetadataInfo>` getDRMetadataInfos(); | Enumera todos los objetos de metadatos DRM detectados en el manifiesto. |
| **Subtítulos opcionales** |  |
| booleano hasClosedCaptions(); | True si están disponibles las pistas de subtítulos. |
| Lista`<ClosedCaptionsTrack>` getClosedActionsTracks(); | Proporciona una lista de las pistas de subtítulos opcionales disponibles. |
| ClosedCaptionsTrack get SelectedCaptionsTrack(); | Recupera la pista de subtítulos seleccionados con SelectClosedCaptionsTrack |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) | Define una pista de subtítulos para que sea la pista de subtítulos cerrados actual. |
| **Pistas de audio alternativas** |  |
| booleano hasAlternateAudio(); | True si el flujo tiene pistas de audio alternativas. Nota: La pista de audio principal (predeterminada) también forma parte de la lista de pistas de audio alternativas.  TVSDK para Android considera que la pista de audio principal es uno de los elementos de la lista de pistas de audio alternativas. Debido a esto, el único caso en el que MediaPlayerItem.hasAlternateAudio devuelve false es cuando el flujo no tiene audio. Si el contenido solo tiene una pista de audio, este método devuelve true y  `MediaPlayerItem.getAudioTracks`  devuelve una lista con un solo elemento (la pista de audio predeterminada). |
| Lista`<AudioTrack>` getAudioTracks(); | Proporciona una lista de pistas de audio alternativas disponibles. |
| AudioTrack getSelectedAudioTrack(); | Recupera la pista de audio seleccionada con selectAudioTrack . |
| selectAudioTrack ( AudioTrack audioTrack ) | Selecciona una pista de audio para que sea la pista de audio actual. |
| **Metadatos cronometrados** |  |
| booleano hasTimedMetadata(); | True si el flujo tiene metadatos sincronizados asociados. |
| Lista`<TimedMetadata>` getTimedMetadata(); | Proporciona una lista de los objetos de metadatos cronometrados asociados a la secuencia. |
| **Varios perfiles (tasas de bits)** |
| booleano isDynamic(); | True si el flujo es un flujo de velocidad de bits múltiple (MBR). |
| Lista`<Profile>` getProfiles(); | Proporciona una lista de los perfiles de velocidad de bits asociados. Para cada perfil, puede recuperar su velocidad de bits y la altura y anchura del perfil. |
| Perfil getSelectedProfile() | Recupera el perfil seleccionado actualmente. |
| **Juego de trucos** |  |
| booleano isTrickPlaySupported(); | True si el reproductor admite avance rápido, rebobinado y reanudación. |
| Lista`< Float>` getAvailablePlaybackRates() | Proporciona la lista de velocidades de reproducción disponibles en el contexto de la función de truco. |
| Flotante getSelectedPlaybackRate() | Recupera la velocidad de reproducción seleccionada actualmente. |
| MediaPlayerItemConfig getConfig() | Devuelve la instancia de MediaPlayerItemConfig asociada a este elemento. |
| **Recurso de medios** |  |
| MediaResource.getResource(); | Devuelve el recurso multimedia asociado a este elemento. |
| int getResourceId() | Devuelve el identificador de medios asociado con este elemento. Este ID se establece cuando el elemento se carga mediante MediaPlayerItemLoader.load |
