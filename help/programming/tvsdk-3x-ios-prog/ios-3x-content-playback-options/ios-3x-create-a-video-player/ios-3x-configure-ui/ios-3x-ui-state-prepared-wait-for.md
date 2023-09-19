---
description: Para poder utilizar la mayoría de los métodos de reproductor de TVSDK, el reproductor debe estar en un estado válido.
title: Esperar a un estado válido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Esperar a un estado válido {#wait-for-a-valid-state}

Para poder utilizar la mayoría de los métodos de reproductor de TVSDK, el reproductor debe estar en un estado válido.

El reproductor se mueve a través de varios estados. Esperar a que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está en al menos el estado requerido, se lanzarán muchos métodos de reproductor `IllegalStateException`.

El estado requerido suele ser `PTMediaPlayerStatusReady`.
