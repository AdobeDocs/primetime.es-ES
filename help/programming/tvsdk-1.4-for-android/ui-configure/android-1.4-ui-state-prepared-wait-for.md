---
description: Con TVSDK puede controlar la experiencia de reproducción básica de vídeo en directo y vídeo bajo demanda (VOD). TVSDK proporciona métodos y propiedades en la instancia de reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.
title: Esperar a un estado válido
exl-id: ab9da066-429f-44ca-b2e7-2bde9e5c0f90
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Esperar a un estado válido {#wait-for-a-valid-state}

Con TVSDK puede controlar la experiencia de reproducción básica de vídeo en directo y vídeo bajo demanda (VOD). TVSDK proporciona métodos y propiedades en la instancia de reproductor que puede utilizar para configurar la interfaz de usuario del reproductor.

Para poder utilizar la mayoría de los métodos de reproductor de TVSDK, el reproductor debe estar en un estado válido.
El reproductor se desplaza por varios estados. Esperar a que el reproductor esté en el estado correcto garantiza que el recurso multimedia se haya cargado correctamente. Si el reproductor no se encuentra en el estado requerido, se activan muchos métodos de reproductor `IllegalStateException`.

El estado requerido suele ser PREPARADO.
