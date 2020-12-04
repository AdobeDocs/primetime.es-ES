---
description: Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
seo-description: Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
seo-title: Esperar un estado válido
title: Esperar un estado válido
uuid: ad9df366-c443-4e6b-a7ab-658d5691eb94
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Esperar un estado válido {#wait-for-a-valid-state}

Para poder utilizar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.

El reproductor pasa por varios estados. Esperar a que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no tiene al menos el estado requerido, muchos métodos del reproductor generan `IllegalStateException`.

El estado requerido suele ser `PTMediaPlayerStatusReady`.