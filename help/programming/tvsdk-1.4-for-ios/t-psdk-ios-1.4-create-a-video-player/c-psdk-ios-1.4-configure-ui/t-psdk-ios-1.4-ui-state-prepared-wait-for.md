---
description: Para poder usar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.
title: Espere un estado válido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Espere un estado válido{#wait-for-a-valid-state}

Para poder usar la mayoría de los métodos del reproductor TVSDK, el reproductor debe tener un estado válido.

El reproductor pasa por varios estados. Esperar que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está en al menos el estado requerido, muchos métodos del reproductor arrojan `IllegalStateException`.

El estado requerido suele ser `PTMediaPlayerStatusReady`.
