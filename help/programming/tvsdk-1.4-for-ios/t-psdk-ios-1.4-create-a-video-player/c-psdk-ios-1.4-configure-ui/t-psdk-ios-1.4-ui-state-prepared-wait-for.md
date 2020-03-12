---
description: Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
seo-description: Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
seo-title: Esperar un estado válido
title: Esperar un estado válido
uuid: e13201d7-b217-4d01-bdb7-a71855e3500e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Esperar un estado válido{#wait-for-a-valid-state}

Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.

El reproductor pasa por varios estados. Esperar a que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no tiene al menos el estado requerido, muchos métodos de reproductor `IllegalStateException`.

El estado requerido suele ser `PTMediaPlayerStatusReady`.
