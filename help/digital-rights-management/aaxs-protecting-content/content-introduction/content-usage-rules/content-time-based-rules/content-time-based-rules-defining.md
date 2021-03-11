---
title: Definición de reglas basadas en tiempo
description: Definición de reglas basadas en tiempo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Definición de reglas basadas en tiempo {#defining-time-based-rules}

Adobe Access utiliza la &quot;aplicación suave&quot; de las restricciones de licencia basadas en el tiempo. Si un derecho de tiempo caduca durante la reproducción de un vídeo, el comportamiento predeterminado de Acceso a Adobe es no restringir la reproducción hasta la próxima vez que se vuelva a crear el flujo de vídeo (llamando a `Netstream.stop()` y `Netstream.play()`).

Aunque el comportamiento predeterminado es la aplicación de software, también puede habilitar el cumplimiento de normas mediante la realización de una de las siguientes tareas:

* Pida al reproductor de vídeo que sondee periódicamente la licencia para asegurarse de que ninguna de las restricciones de tiempo ha caducado. Esto se puede lograr llamando a `DRMManager.loadVoucher(LOCAL_ONLY).`Un código de error indica que la licencia almacenada localmente ya no es válida.
* Cada vez que el usuario hace clic en el botón Pausa, puede registrar la marca de tiempo del vídeo actual y luego llamar a `Netstream.stop().`Cuando el usuario hace clic en el botón Reproducir, puede buscar la ubicación grabada y luego llamar a `Netstream.play()`.

## Fecha de inicio {#start-date}

Especifica la fecha después de la cual es válida una licencia.

Ejemplo de caso de uso: Utilice una fecha absoluta para emitir licencias de contenido antes de la fecha de disponibilidad de un recurso o para aplicar un período de &quot;embargo&quot;.

## Fecha de finalización {#end-date}

Especifica la fecha tras la cual caduca una licencia.

Ejemplo de caso de uso: Utilice una fecha de caducidad absoluta para reflejar el final de los derechos de distribución.

## Fecha de finalización relativa {#relative-end-date}

Especifica la fecha de caducidad de la licencia, expresada en relación con la fecha de empaquetado.

Ejemplo de caso de uso: En un proceso de empaquetado automatizado, utilice una sola directiva con esta opción para una serie de vídeos para establecer la fecha de caducidad en 30 días en relación con la fecha de empaquetado.

## Duración del almacenamiento en caché de licencias {#license-caching-duration}

Especifica la duración durante la que una licencia se puede almacenar en caché en disco en el almacén de licencias local del cliente sin necesidad de volver a adquirirse desde el servidor de licencias. También puede especificar una fecha y hora absolutas después de la cual una licencia ya no se puede almacenar en caché.

Una vez que ha pasado la fecha de caducidad de la caché, la licencia ya no es válida y el cliente debe solicitar una nueva licencia al servidor de licencias.

Ejemplo de caso de uso: Utilice la duración de la caché de licencias para especificar una cantidad fija de tiempo válido para una licencia en particular, como en un caso de uso de alquiler. Se puede especificar un alquiler de 30 días (con caché de licencia) para indicar la duración total de la licencia dentro de la cual se consumirá el contenido.

## Ventana de reproducción {#playback-window}

Especifica la duración de una licencia válida después de la primera vez que se utiliza para reproducir contenido protegido.

Ejemplo de caso de uso: Algunos modelos de negocio permiten un periodo de alquiler de 30 días, pero una vez que comienza la reproducción, debe completarse en 48 horas. Esta longevidad de 48 horas de la licencia se define como la ventana de reproducción.

## Requisitos para la sincronización {#requirements-for-synchronization}

Especifica la frecuencia con la que el cliente sincronizará su estado con el servidor. Si se ha emitido una licencia fuera de banda al cliente (sin ponerse en contacto con un servidor de licencias), las reglas de uso pueden especificar que el cliente debe enviar mensajes de sincronización al servidor para sincronizar la hora segura del cliente y el estado del cliente de informes con el servidor.

El comportamiento de sincronización se define mediante los siguientes parámetros:

* Intervalo de inicio: especifica cuánto tiempo se debe esperar después de la última sincronización correcta para iniciar otra solicitud de sincronización.
* Intervalo de detención de disco duro (opcional). No permitir la reproducción si no se ha producido una sincronización correcta en el tiempo especificado.
* Forzar Probabilidad De Sincronización — (Opcional). Probabilidad con la que el cliente debe enviar un mensaje de sincronización antes del siguiente intervalo de inicio.

>[!NOTE]
>
>Esta regla de uso es compatible con los clientes de acceso a Adobe versión 3.0 y posteriores. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente admitida por el servidor de licencias. Consulte [Versión mínima del cliente](../../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).