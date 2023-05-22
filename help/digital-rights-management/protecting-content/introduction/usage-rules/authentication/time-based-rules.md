---
title: Reglas basadas en el tiempo
description: Reglas basadas en el tiempo
copied-description: true
exl-id: 02a5c10d-13f5-4482-b525-bf6a1ec9dcf0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Reglas basadas en el tiempo {#time-based-rules}

Primetime DRM utiliza la &quot;aplicación suave&quot; de las restricciones de licencia basadas en el tiempo. Si caduca un derecho de tiempo durante la reproducción de un vídeo, el comportamiento predeterminado de Primetime DRM es no restringir la reproducción hasta la próxima vez que se vuelva a crear el flujo de vídeo (llamando a `Netstream.stop()` y `Netstream.play()`).

Aunque la aplicación flexible es el comportamiento predeterminado, también puede habilitarla si realiza una de las siguientes tareas:

* Pida al reproductor de vídeo que sondee periódicamente la licencia para asegurarse de que ninguna de las restricciones temporales ha caducado. Esto se puede lograr llamando a `DRMManager.loadVoucher(LOCAL_ONLY).` Un código de error indica que la licencia almacenada localmente ya no es válida.
* Cada vez que el usuario haga clic **[!UICONTROL Pause]**, puede grabar la marca de tiempo del vídeo actual y, a continuación, llamar a `Netstream.stop()`. Cuando el usuario hace clic en el botón Reproducir, puede buscar en la ubicación grabada y, a continuación, llamar a `Netstream.play()`.

## Fecha de inicio {#start-date}

La fecha de inicio especifica la fecha después de la cual una licencia es válida.

Ejemplo de caso de uso: utilice una fecha absoluta para emitir licencias de contenido antes de la fecha de disponibilidad de un recurso o para aplicar un período de &quot;embargo&quot;.

## Fecha de finalización {#end-date}

La fecha de finalización especifica la fecha después de la cual caduca una licencia.

Ejemplo de caso de uso: utilice una fecha de caducidad absoluta para reflejar el final de los derechos de distribución.

## Fecha de finalización relativa {#relative-end-date}

La fecha final relativa especifica la fecha de caducidad de la licencia, que se expresa en relación con la fecha de empaquetado, no en relación con la fecha en que se emitió la licencia.

Ejemplo de caso de uso: en un proceso de empaquetado automatizado, utilice una única directiva DRM de Primetime con esta opción para una serie de vídeos, a fin de establecer la fecha de caducidad en 30 días en relación con la fecha de empaquetado.

## Duración de almacenamiento en caché de licencias{#license-caching-duration}

La duración del almacenamiento en caché de licencias especifica cuánto tiempo se puede almacenar una licencia en caché en el disco en el almacén de licencias local del cliente sin que sea necesario volver a obtenerla del servidor de licencias. También puede especificar una fecha y hora absolutas después de las cuales una licencia ya no se puede almacenar en caché.

Una vez transcurrida la fecha de caducidad de la caché, la licencia deja de ser válida y el cliente debe solicitar una nueva licencia al servidor de licencias.

Ejemplo de caso de uso: utilice la duración del almacenamiento en caché de la licencia para especificar una cantidad fija de tiempo válido para una licencia determinada, como en un caso de uso de alquiler. Puede especificar un alquiler de 30 días (con almacenamiento en caché de licencias) para indicar la duración total de la licencia dentro de la cual se consumirá el contenido.

## Ventana de reproducción {#playback-window}

La ventana de reproducción especifica la duración de la validez de una licencia tras la primera vez que se utiliza para reproducir contenido protegido.

Ejemplo de caso de uso: Algunos modelos comerciales permiten un periodo de alquiler de 30 días, pero, una vez iniciada la reproducción, esta debe completarse en 48 horas. En este caso, la duración de la licencia de 48 horas es la ventana de reproducción.

**A partir de la versión 5.3** : La ventana de reproducción también admite la opción de habilitar o deshabilitar la detención completa, lo que indica si el contexto de descifrado para la reproducción debe detenerse al expirar la ventana de reproducción (habilitada) o continuar a pesar de la caducidad (deshabilitada).

>[!NOTE]
>
>La opción de parada forzada no funciona correctamente con la ventana de reproducción si se utiliza junto con ella (la ventana de reproducción no se respetará). La reproducción de contenido con la ventana de reproducción sin parada segura respeta la restricción de la ventana de reproducción.
