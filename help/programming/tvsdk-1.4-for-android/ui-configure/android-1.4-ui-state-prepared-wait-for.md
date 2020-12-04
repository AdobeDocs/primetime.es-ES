---
description: Con TVSDK puede controlar la experiencia de reproducción básica para vídeo en directo y vídeo a petición (VOD). TVSDK proporciona métodos y propiedades en la instancia del reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.
seo-description: Con TVSDK puede controlar la experiencia de reproducción básica para vídeo en directo y vídeo a petición (VOD). TVSDK proporciona métodos y propiedades en la instancia del reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.
seo-title: Esperar un estado válido
title: Esperar un estado válido
uuid: 22b68162-1625-4e8a-8566-b0c198155622
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Esperar un estado válido {#wait-for-a-valid-state}

Con TVSDK puede controlar la experiencia de reproducción básica para vídeo en directo y vídeo a petición (VOD). TVSDK proporciona métodos y propiedades en la instancia del reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.

Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
El jugador se mueve por varios estados. Esperar a que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está al menos en el estado requerido, muchos métodos del reproductor generan `IllegalStateException`.

El estado requerido suele estar PREPARADO.
