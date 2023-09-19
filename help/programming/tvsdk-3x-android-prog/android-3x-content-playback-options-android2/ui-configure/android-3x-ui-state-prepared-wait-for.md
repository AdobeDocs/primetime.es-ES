---
description: Para poder utilizar la mayoría de los métodos de reproductor de TVSDK, el reproductor debe estar en un estado válido.
title: Esperar un estado válido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Esperar un estado válido {#wait-for-a-valid-status}

Con TVSDK, puede controlar la experiencia de reproducción básica de vídeo en directo y vídeo bajo demanda (VOD). TVSDK proporciona métodos y propiedades en la instancia de reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.

Para poder utilizar la mayoría de los métodos de reproductor de TVSDK, el reproductor debe estar en un estado válido.

Esperar a que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está en al menos el estado requerido, se lanzarán muchos métodos de reproductor `MediaPlayerException`.

El estado requerido suele ser PREPARADO. Cuando esto sucede, la rutina de llamada de retorno para `StatusChangeEventListener.onStatusChanged()` ejecuta.

Para confirmar que el estado es `PREPARED`, marque `MediaPlayer.MediaPlayerStatus`.
