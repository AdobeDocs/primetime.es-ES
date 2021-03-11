---
description: Con TVSDK, puede controlar la experiencia de reproducción básica para vídeo en directo y vídeo bajo demanda (VOD). TVSDK proporciona métodos y propiedades en la instancia del reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.
title: Espere un estado válido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Espere un estado válido {#wait-for-a-valid-state}

Con TVSDK, puede controlar la experiencia de reproducción básica para vídeo en directo y vídeo bajo demanda (VOD). TVSDK proporciona métodos y propiedades en la instancia del reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.

Para poder usar la mayoría de los métodos del reproductor TVSDK, el reproductor debe estar en un estado válido.
El reproductor se mueve por varios estados. Esperar que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está en al menos el estado requerido, muchos métodos del reproductor arrojan `IllegalStateException`.

El estado requerido suele estar PREPARADO.
