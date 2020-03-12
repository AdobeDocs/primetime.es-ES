---
seo-title: Reglas basadas en el tiempo
title: Reglas basadas en el tiempo
uuid: 19a6ee7e-9580-48bb-a3a6-ff2cedcc796a
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Reglas basadas en el tiempo {#time-based-rules}

Primetime DRM utiliza &quot;cumplimiento suave&quot; de las restricciones de licencia basadas en el tiempo. Si un derecho de tiempo caduca durante la reproducción de un vídeo, el comportamiento predeterminado de Primetime DRM es no restringir la reproducción hasta la próxima vez que se vuelva a crear el flujo de vídeo (llamando `Netstream.stop()` y `Netstream.play()`).

Aunque la aplicación en pantalla es el comportamiento predeterminado, también puede activar la aplicación en estado estricto realizando una de las siguientes tareas:

* Pida al reproductor de vídeo que sondee periódicamente la licencia para asegurarse de que ninguna de las restricciones de tiempo ha caducado. Esto se puede lograr llamando a `DRMManager.loadVoucher(LOCAL_ONLY).` Un código de error indica que la licencia almacenada localmente ya no es válida.
* Siempre que el usuario haga clic **[!UICONTROL Pause]**, podrá grabar la marca de tiempo del vídeo actual y, a continuación, llamar `Netstream.stop()`. Cuando el usuario hace clic en el botón Reproducir, puede buscar la ubicación grabada y, a continuación, llamar `Netstream.play()`.

## Fecha de inicio {#start-date}

La fecha de inicio especifica la fecha después de la cual una licencia es válida.

Ejemplo de caso de uso: Utilice una fecha absoluta para emitir licencias de contenido antes de la fecha de disponibilidad de un recurso o para aplicar un período de &quot;embargo&quot;.

## Fecha final {#end-date}

La fecha de finalización especifica la fecha después de la cual caduca una licencia.

Ejemplo de caso de uso: Utilice una fecha de caducidad absoluta para reflejar el final de los derechos de distribución.

## Fecha final relativa {#relative-end-date}

La fecha de finalización relativa especifica la fecha de caducidad de la licencia, que se expresa en relación con la fecha de embalaje, no en relación con la fecha en que se emitió la licencia.

Ejemplo de caso de uso: En un proceso de empaquetado automatizado, utilice una única directiva DRM de Primetime con esta opción para una serie de vídeos, para establecer la fecha de caducidad en 30 días en relación con la fecha de empaquetado.

## Duración del almacenamiento en caché de licencias{#license-caching-duration}

La duración de la caché de licencia especifica cuánto tiempo se puede almacenar una licencia en caché en disco en el almacén de licencias local del cliente sin necesidad de volver a adquirirla en el servidor de licencias. También puede especificar una fecha y hora absolutas después de las cuales una licencia ya no se puede almacenar en caché.

Una vez pasada la fecha de caducidad de la caché, la licencia ya no es válida y el cliente debe solicitar una nueva licencia al servidor de licencias.

Ejemplo de caso de uso: Utilice la duración de la caché de licencia para especificar una cantidad fija de tiempo válida para una licencia determinada, como en un caso de uso de alquiler. Puede especificar un alquiler de 30 días (con caché de licencia) para indicar la duración total de la licencia dentro de la cual se consumirá el contenido.

## Ventana de reproducción {#playback-window}

La ventana de reproducción especifica la duración durante la que una licencia es válida la primera vez que se utiliza para reproducir contenido protegido.

Ejemplo de caso de uso: Algunos modelos empresariales permiten un período de alquiler de 30 días, pero, una vez que comienza la reproducción, la reproducción debe completarse en 48 horas. En este caso, la duración de 48 horas de la licencia es la ventana de reproducción.

**A partir de la versión 5.3 hacia adelante** : la ventana de reproducción también admite la opción de activar o desactivar la opción Parada dura, que indica si el contexto de descifrado para la reproducción debe detenerse al finalizar la ventana de reproducción (activado) o continuar a pesar de la caducidad (deshabilitado).

>[!NOTE]
>
>La opción de parada dura no funciona correctamente con la ventana de reproducción si se utiliza junto con ella (no se respetará la ventana de reproducción). La reproducción de contenido con la ventana de reproducción sin parada segura respeta la restricción de la ventana de reproducción.