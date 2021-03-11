---
title: Resumen de reglas basadas en el tiempo
description: Resumen de reglas basadas en el tiempo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Reglas basadas en el tiempo {#time-based-rules}

Primetime DRM utiliza la &quot;aplicación suave&quot; de las restricciones de licencia basadas en el tiempo. Si un derecho de tiempo caduca durante la reproducción de un vídeo, el comportamiento predeterminado de Primetime DRM es no restringir la reproducción hasta la próxima vez que se vuelva a crear el flujo de vídeo (llamando a `Netstream.stop()` y `Netstream.play()`).

Aunque el comportamiento predeterminado es la aplicación de software, también puede habilitar el cumplimiento de normas mediante la realización de una de las siguientes tareas:

* Pida al reproductor de vídeo que sondee periódicamente la licencia para asegurarse de que ninguna de las restricciones de tiempo ha caducado. Esto se puede lograr llamando a `DRMManager.loadVoucher(LOCAL_ONLY).` Un código de error indica que la licencia almacenada localmente ya no es válida.
* Siempre que el usuario haga clic en **[!UICONTROL Pause]**, puede registrar la marca de tiempo del vídeo actual y luego llamar a `Netstream.stop()`. Cuando el usuario hace clic en el botón Reproducir, puede buscar la ubicación registrada y luego llamar a `Netstream.play()`.