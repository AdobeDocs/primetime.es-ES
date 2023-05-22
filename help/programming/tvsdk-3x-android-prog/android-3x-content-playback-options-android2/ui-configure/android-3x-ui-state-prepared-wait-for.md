---
description: Para poder utilizar la mayoría de los métodos de reproductor de TVSDK, el reproductor debe estar en un estado válido.
title: Esperar un estado válido
exl-id: bfd77163-7ca8-41e1-8b97-2d6a765f5ccd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
