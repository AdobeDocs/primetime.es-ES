---
description: Debe liberar una instancia y recursos de MediaPlayer cuando ya no necesite MediaResource.
seo-description: Debe liberar una instancia y recursos de MediaPlayer cuando ya no necesite MediaResource.
seo-title: Liberar una instancia y recursos de MediaPlayer
title: Liberar una instancia y recursos de MediaPlayer
uuid: e7b2112e-8add-4789-9345-5f829d39d639
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Liberar una instancia y recursos de MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Debe liberar una instancia y recursos de MediaPlayer cuando ya no necesite MediaResource.

Cuando libera un objeto `MediaPlayer`, se desasignan los recursos de hardware subyacentes asociados a este objeto `MediaPlayer`.

A continuación se indican algunas razones para lanzar un `MediaPlayer`:

* La retención de recursos innecesarios puede afectar al rendimiento.
* Si no se admiten varias instancias del mismo códec de vídeo en un dispositivo, es posible que se produzca un error de reproducción en otras aplicaciones.

1. Libere el `MediaPlayer`.

   ```
   function release():void;
   ```

Una vez liberada la instancia `MediaPlayer`, ya no podrá usarla. Si se llama a algún método de la interfaz `MediaPlayer` después de liberarlo, se genera un `IllegalStateException`.