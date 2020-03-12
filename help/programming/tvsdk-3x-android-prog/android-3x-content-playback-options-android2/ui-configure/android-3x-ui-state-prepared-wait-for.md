---
description: Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
seo-description: Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
seo-title: Esperar un estado válido
title: Esperar un estado válido
uuid: 7a86b4cf-f7a0-4d90-9ff2-401640a395c5
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Esperar un estado válido {#wait-for-a-valid-status}

Con TVSDK, puede controlar la experiencia de reproducción básica para vídeo en directo y vídeo a petición (VOD). TVSDK proporciona métodos y propiedades en la instancia del reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.

Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.

Esperar a que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no tiene al menos el estado requerido, muchos métodos de reproductor `MediaPlayerException`.

El estado requerido suele estar PREPARADO. Cuando esto sucede, se ejecuta la rutina de llamada de retorno para `StatusChangeEventListener.onStatusChanged()` .

Para confirmar que el estado es `PREPARED`, marque `MediaPlayer.MediaPlayerStatus`.