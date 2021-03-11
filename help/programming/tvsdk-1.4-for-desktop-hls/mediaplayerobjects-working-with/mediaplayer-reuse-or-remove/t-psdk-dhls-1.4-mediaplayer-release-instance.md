---
description: Debe liberar una instancia y recursos de MediaPlayer cuando ya no necesite MediaResource.
title: Liberar una instancia y recursos de MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Liberar una instancia y recursos de MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Debe liberar una instancia y recursos de MediaPlayer cuando ya no necesite MediaResource.

Cuando libera un objeto `MediaPlayer`, se desasignan los recursos de hardware subyacentes asociados a este objeto `MediaPlayer`.

Estas son algunas razones para publicar un `MediaPlayer`:

* Mantener recursos innecesarios puede afectar al rendimiento.
* Si en un dispositivo no se admiten varias instancias del mismo códec de vídeo, puede ocurrir un error de reproducción en otras aplicaciones.

1. Suelte el `MediaPlayer`.

   ```
   function release():void;
   ```

Una vez lanzada la instancia `MediaPlayer`, ya no puede usarla. Si se llama a algún método de la interfaz `MediaPlayer` después de su lanzamiento, se genera un `IllegalStateException`.