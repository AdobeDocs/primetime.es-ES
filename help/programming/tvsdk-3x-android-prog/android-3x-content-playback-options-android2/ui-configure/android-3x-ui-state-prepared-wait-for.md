---
description: Para poder usar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
title: Espere a que aparezca un estado válido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Espere a que aparezca un estado válido {#wait-for-a-valid-status}

Con TVSDK, puede controlar la experiencia de reproducción básica para vídeo en directo y vídeo bajo demanda (VOD). TVSDK proporciona métodos y propiedades en la instancia del reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.

Para poder usar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.

Esperar que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está en al menos el estado requerido, muchos métodos del reproductor arrojan `MediaPlayerException`.

El estado requerido suele estar PREPARADO. Cuando esto sucede, se ejecuta la rutina de llamada de retorno para `StatusChangeEventListener.onStatusChanged()`.

Para confirmar que el estado es `PREPARED`, marque `MediaPlayer.MediaPlayerStatus`.