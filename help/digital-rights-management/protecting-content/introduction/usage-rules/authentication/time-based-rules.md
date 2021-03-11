---
title: Reglas basadas en el tiempo
description: Reglas basadas en el tiempo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# Reglas basadas en el tiempo {#time-based-rules}

Primetime DRM utiliza la &quot;aplicación suave&quot; de las restricciones de licencia basadas en el tiempo. Si un derecho de tiempo caduca durante la reproducción de un vídeo, el comportamiento predeterminado de Primetime DRM es no restringir la reproducción hasta la próxima vez que se vuelva a crear el flujo de vídeo (llamando a `Netstream.stop()` y `Netstream.play()`).

Aunque el comportamiento predeterminado es la aplicación de software, también puede habilitar el cumplimiento de normas mediante la realización de una de las siguientes tareas:

* Pida al reproductor de vídeo que sondee periódicamente la licencia para asegurarse de que ninguna de las restricciones de tiempo ha caducado. Esto se puede lograr llamando a `DRMManager.loadVoucher(LOCAL_ONLY).` Un código de error indica que la licencia almacenada localmente ya no es válida.
* Siempre que el usuario haga clic en **[!UICONTROL Pause]**, puede registrar la marca de tiempo del vídeo actual y luego llamar a `Netstream.stop()`. Cuando el usuario hace clic en el botón Reproducir, puede buscar la ubicación registrada y luego llamar a `Netstream.play()`.

## Fecha de inicio {#start-date}

La fecha de inicio especifica la fecha después de la cual es válida una licencia.

Ejemplo de caso de uso: Utilice una fecha absoluta para emitir licencias de contenido antes de la fecha de disponibilidad de un recurso o para aplicar un período de &quot;embargo&quot;.

## Fecha de finalización {#end-date}

La fecha de finalización especifica la fecha después de la cual caduca una licencia.

Ejemplo de caso de uso: Utilice una fecha de caducidad absoluta para reflejar el final de los derechos de distribución.

## Fecha de finalización relativa {#relative-end-date}

La fecha de finalización relativa especifica la fecha de caducidad de la licencia, que se expresa en relación con la fecha de embalaje, no en relación con la fecha en que se emitió la licencia.

Ejemplo de caso de uso: En un proceso de empaquetado automatizado, utilice una sola directiva de Primetime DRM con esta opción para una serie de vídeos, para establecer la fecha de caducidad en 30 días en relación con la fecha de empaquetado.

## Duración del almacenamiento en caché de licencias{#license-caching-duration}

La duración del almacenamiento en caché de licencias especifica cuánto tiempo se puede almacenar una licencia en caché en disco en el almacén de licencias local del cliente sin necesidad de volver a adquirirla desde el servidor de licencias. Como alternativa, puede especificar una fecha y hora absolutas después de las cuales una licencia ya no se puede almacenar en caché.

Una vez que ha pasado la fecha de caducidad de la caché, la licencia ya no es válida y el cliente debe solicitar una nueva licencia al servidor de licencias.

Ejemplo de caso de uso: Utilice la duración de la caché de licencias para especificar una cantidad fija de tiempo válido para una licencia en particular, como en un caso de uso de alquiler. Puede especificar un alquiler de 30 días (con caché de licencia) para indicar la duración total de la licencia dentro de la cual consumir el contenido.

## Ventana de reproducción {#playback-window}

La ventana de reproducción especifica la duración de una licencia válida después de la primera vez que se utiliza para reproducir contenido protegido.

Ejemplo de caso de uso: Algunos modelos de negocio permiten un periodo de alquiler de 30 días, pero una vez que comienza la reproducción, la reproducción debe completarse en 48 horas. En este caso, la duración de 48 horas de la licencia es la ventana de reproducción.

**A partir de la versión 5.3 adelante** : la ventana de reproducción también admite la opción de habilitar o deshabilitar la Parada dura, que indica si el contexto de descifrado para la reproducción debe detenerse al expirar la ventana de reproducción (habilitada) o continuar a pesar de la caducidad (deshabilitada).

>[!NOTE]
>
>La opción de parada dura no funciona correctamente con la ventana de reproducción si se utiliza junto con ella (no se respetará la ventana de reproducción). Al reproducir contenido con la ventana de reproducción sin parada segura, se respeta la restricción de la ventana de reproducción.