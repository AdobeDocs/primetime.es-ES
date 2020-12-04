---
description: Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
seo-description: Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
seo-title: Esperar un estado válido
title: Esperar un estado válido
uuid: ffa63ad6-84d3-4eb2-aa99-026418d86528
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# Esperar un estado válido {#wait-for-a-valid-state}

Con TVSDK, puede controlar la experiencia de reproducción básica para vídeo en directo y vídeo a petición (VOD). TVSDK proporciona métodos y propiedades en la instancia del reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.

Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.

Esperar a que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no tiene al menos el estado requerido, muchos métodos del reproductor generan `MediaPlayerException`.

El estado requerido suele estar PREPARADO. Cuando esto sucede, se ejecuta la rutina de llamada de retorno para `StatusChangeEventListener.onStatusChanged()`.

1. Para confirmar que el estado es `PREPARED`, marque `MediaPlayer.MediaPlayerStatus`.
