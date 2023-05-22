---
description: Para poder utilizar la mayoría de los métodos de reproductor de TVSDK, el reproductor debe estar en un estado válido.
title: Esperar a un estado válido
exl-id: 150b37b8-c36d-4143-bead-ddc601bba6fe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Esperar a un estado válido{#wait-for-a-valid-state}

Para poder utilizar la mayoría de los métodos de reproductor de TVSDK, el reproductor debe estar en un estado válido.

El reproductor se mueve a través de varios estados. Esperar a que el reproductor esté en el estado correcto garantiza que el recurso de medios se haya cargado correctamente. Si el reproductor no está en al menos el estado requerido, se lanzarán muchos métodos de reproductor `IllegalStateException`.

El estado requerido suele ser `PTMediaPlayerStatusReady`.
