---
seo-title: Información general sobre las reglas basadas en el tiempo
title: Información general sobre las reglas basadas en el tiempo
uuid: 10b7766e-3b1a-4d8a-ba15-46976aa0847d
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Reglas basadas en el tiempo {#time-based-rules}

Primetime DRM utiliza &quot;cumplimiento suave&quot; de las restricciones de licencia basadas en el tiempo. Si un derecho de tiempo caduca durante la reproducción de un vídeo, el comportamiento predeterminado de Primetime DRM es no restringir la reproducción hasta la próxima vez que se vuelva a crear el flujo de vídeo (llamando `Netstream.stop()` y `Netstream.play()`).

Aunque la aplicación en pantalla es el comportamiento predeterminado, también puede activar la aplicación en estado estricto realizando una de las siguientes tareas:

* Pida al reproductor de vídeo que sondee periódicamente la licencia para asegurarse de que ninguna de las restricciones de tiempo ha caducado. Esto se puede lograr llamando a `DRMManager.loadVoucher(LOCAL_ONLY).` Un código de error indica que la licencia almacenada localmente ya no es válida.
* Siempre que el usuario haga clic **[!UICONTROL Pause]**, podrá grabar la marca de tiempo del vídeo actual y, a continuación, llamar `Netstream.stop()`. Cuando el usuario hace clic en el botón Reproducir, puede buscar la ubicación grabada y, a continuación, llamar `Netstream.play()`.