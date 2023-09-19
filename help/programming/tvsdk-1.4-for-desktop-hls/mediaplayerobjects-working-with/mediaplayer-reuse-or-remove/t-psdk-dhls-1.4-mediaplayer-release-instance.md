---
description: Debe liberar una instancia de MediaPlayer y recursos cuando ya no necesite MediaResource.
title: Lanzamiento de una instancia de MediaPlayer y recursos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Lanzamiento de una instancia de MediaPlayer y recursos{#release-a-mediaplayer-instance-and-resources}

Debe liberar una instancia de MediaPlayer y recursos cuando ya no necesite MediaResource.

Cuando libera un `MediaPlayer` , los recursos de hardware subyacentes asociados a este objeto `MediaPlayer` objeto están desasignados.

Estas son algunas razones para publicar un `MediaPlayer`:

* Mantener recursos innecesarios puede afectar al rendimiento.
* Si no se admiten varias instancias del mismo códec de vídeo en un dispositivo, puede producirse un error de reproducción en otras aplicaciones.

1. Suelte el `MediaPlayer`.

   ```
   function release():void;
   ```

Después del `MediaPlayer` Una vez liberada, ya no puede utilizarla. Si hay algún método del `MediaPlayer` se llama a la interfaz de después de su lanzamiento, y `IllegalStateException` se ha lanzado.
