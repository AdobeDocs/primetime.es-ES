---
description: Con TVSDK puede controlar la experiencia de reproducción básica de vídeo en directo y vídeo bajo demanda (VOD). TVSDK proporciona métodos y propiedades en la instancia de reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.
title: Esperar a un estado válido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Esperar a un estado válido {#wait-for-a-valid-state}

Con TVSDK puede controlar la experiencia de reproducción básica de vídeo en directo y vídeo bajo demanda (VOD). TVSDK proporciona métodos y propiedades en la instancia de reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.

Para poder utilizar la mayoría de los métodos de reproductor de TVSDK, el reproductor debe estar en un estado válido.
El reproductor se desplaza por varios estados. Esperar a que el reproductor esté en el estado correcto garantiza que el recurso multimedia se haya cargado correctamente. Si el reproductor no se encuentra en el estado requerido, se activan muchos métodos de reproductor `IllegalStateException`.

El estado requerido suele ser PREPARADO.
