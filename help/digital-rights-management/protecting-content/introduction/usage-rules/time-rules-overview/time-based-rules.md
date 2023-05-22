---
title: Resumen de reglas basadas en el tiempo
description: Resumen de reglas basadas en el tiempo
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Reglas basadas en el tiempo {#time-based-rules}

Primetime DRM utiliza la &quot;aplicación suave&quot; de las restricciones de licencia basadas en el tiempo. Si caduca un derecho de tiempo durante la reproducción de un vídeo, el comportamiento predeterminado de Primetime DRM es no restringir la reproducción hasta la próxima vez que se vuelva a crear el flujo de vídeo (llamando a `Netstream.stop()` y `Netstream.play()`).

Aunque la aplicación flexible es el comportamiento predeterminado, también puede habilitarla si realiza una de las siguientes tareas:

* Pida al reproductor de vídeo que sondee periódicamente la licencia para asegurarse de que ninguna de las restricciones temporales ha caducado. Esto se puede lograr llamando a `DRMManager.loadVoucher(LOCAL_ONLY).` Un código de error indica que la licencia almacenada localmente ya no es válida.
* Cada vez que el usuario haga clic **[!UICONTROL Pause]**, puede grabar la marca de tiempo del vídeo actual y, a continuación, llamar a `Netstream.stop()`. Cuando el usuario hace clic en el botón Reproducir, puede buscar en la ubicación grabada y, a continuación, llamar a `Netstream.play()`.