---
description: Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.
title: Métodos MediaPlayerItem para acceder a la información de MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# Métodos MediaPlayerItem para acceder a la información de MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

Los métodos de la clase MediaPlayerItem permiten obtener información sobre el flujo de contenido representado por un MediaResource cargado.

| Método | Descripción |
|--- |--- |
| **Etiquetas de publicidad** |  |
| List`<String>` getAdTags() | Proporciona la lista de etiquetas de publicidad que se usan en el proceso de colocación de publicidad. |
| **Emisión en directo** |  |
| boolean isLive(); | True si el flujo está activo; false si es VOD. |
| **Protegido por DRM** |  |
| boolean isProtection(); | True si el flujo está protegido por DRM. |
| List`<DRMMetadataInfo>` getDRMMetadataInfos(); | Enumera todos los objetos de metadatos DRM descubiertos en el manifiesto. |
| **Subtítulos** |  |
| booleano hasClosedCaptions(); | True si hay disponibles pistas de subtítulos. |
| List`<ClosedCaptionsTrack>` getClosedCationsTracks(); | Proporciona una lista de las pistas de subtítulos cerrados disponibles. |
| ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); | Recupera la pista de subtítulos cerrados actual seleccionada con SelectClosedCaptionsTrack . |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack ) | Define una pista de subtítulos para que sea la pista de subtítulos actual. |
| **Pistas de audio alternativas** |  |
| boolean hasAlternateAudio(); | True si el flujo tiene pistas de audio alternativas. Nota:  La pista de audio principal (predeterminada) también forma parte de la lista de pistas de audio alternativas.  TVSDK para Android considera que la pista de audio principal es uno de los elementos de la lista de pistas de audio alternativas. Debido a esto, el único caso en el que MediaPlayerItem.hasAlternateAudio devuelve false es cuando el flujo no tiene audio. Si el contenido tiene una sola pista de audio, este método devuelve el valor &quot;True&quot; y `MediaPlayerItem.getAudioTracks` devuelve una lista con un solo elemento (la pista de audio predeterminada). |
| List`<AudioTrack>` getAudioTracks(); | Proporciona una lista de pistas de audio alternativas disponibles. |
| AudioTrack getSelectedAudioTrack(); | Recupera la pista de audio seleccionada con selectAudioTrack . |
| selectAudioTrack ( AudioTrack audioTrack ) | Selecciona una pista de audio para que sea la pista de audio actual. |
| **Metadatos temporizados** |  |
| boolean hasTimedMetadata(); | True si el flujo tiene metadatos temporizados asociados. |
| List`<TimedMetadata>` getTimedMetadata(); | Proporciona una lista de los objetos de metadatos temporizados asociados al flujo. |
| **Varios perfiles (tasas de bits)** |
| boolean isDynamic(); | True si el flujo es un flujo de velocidad de bits múltiple (MBR). |
| List`<Profile>` getProfiles(); | Proporciona una lista de los perfiles de velocidad de bits asociados. Para cada perfil, puede recuperar su velocidad de bits y la altura y anchura del perfil. |
| Perfil getSelectedProfile() | Recupera el perfil seleccionado actualmente. |
| **Reproducción complicada** |  |
| booleano isTrickPlaySupported(); | True si el reproductor admite el avance rápido, el rebobinado y la reanudación. |
| List`< Float>` getAvailablePlaybackRates() | Proporciona la lista de tasas de reproducción disponibles en el contexto de la función de reproducción mediante trucos. |
| Float getSelectedPlaybackRate() | Recupera la tasa de reproducción seleccionada actualmente. |
| MediaPlayerItemConfig getConfig() | Devuelve la instancia MediaPlayerItemConfig asociada a este elemento. |
| **Recurso de medios** |  |
| MediaResource getResource(); | Devuelve el recurso de medios asociado a este elemento. |
| int getResourceId() | Devuelve el identificador de medios asociado a este elemento. Este ID se establece cuando el elemento se carga mediante MediaPlayerItemLoader.load . |