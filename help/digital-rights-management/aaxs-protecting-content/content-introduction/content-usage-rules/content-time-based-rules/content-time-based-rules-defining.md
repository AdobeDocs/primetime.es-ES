---
title: Definición de reglas basadas en el tiempo
description: Definición de reglas basadas en el tiempo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Definición de reglas basadas en el tiempo {#defining-time-based-rules}

Adobe Access utiliza la &quot;aplicación flexible&quot; de las restricciones de licencia basadas en el tiempo. Si caduca un derecho de tiempo durante la reproducción de un vídeo, el comportamiento predeterminado de Acceso desde Adobe es no restringir la reproducción hasta la próxima vez que se vuelva a crear el flujo de vídeo (llamando a `Netstream.stop()` y `Netstream.play()`).

Aunque la aplicación flexible es el comportamiento predeterminado, también puede habilitarla si realiza una de las siguientes tareas:

* Pida al reproductor de vídeo que sondee periódicamente la licencia para asegurarse de que ninguna de las restricciones temporales ha caducado. Esto se puede lograr llamando a `DRMManager.loadVoucher(LOCAL_ONLY).`Un código de error indica que la licencia almacenada localmente ya no es válida.
* Siempre que el usuario haga clic en el botón Pausa, puede grabar la marca de tiempo del vídeo actual y, a continuación, llamar a `Netstream.stop().`Cuando el usuario hace clic en el botón Reproducir, puede buscar en la ubicación grabada y, a continuación, llamar a `Netstream.play()`.

## Fecha de inicio {#start-date}

Especifica la fecha tras la cual una licencia es válida.

Ejemplo de caso de uso: utilice una fecha absoluta para emitir licencias de contenido antes de la fecha de disponibilidad de un recurso o para aplicar un período de &quot;embargo&quot;.

## Fecha de finalización {#end-date}

Especifica la fecha a partir de la cual caduca una licencia.

Ejemplo de caso de uso: utilice una fecha de caducidad absoluta para reflejar el final de los derechos de distribución.

## Fecha de finalización relativa {#relative-end-date}

Especifica la fecha de caducidad de la licencia, expresada en relación con la fecha de empaquetado.

Ejemplo de caso de uso: en un proceso de empaquetado automatizado, utilice una sola directiva con esta opción para una serie de vídeos a fin de establecer la fecha de caducidad en 30 días respecto a la fecha de empaquetado.

## Duración de almacenamiento en caché de licencias {#license-caching-duration}

Especifica la duración durante la cual se puede almacenar una licencia en caché en el disco del almacén de licencias local del cliente sin que sea necesario volver a obtenerla del servidor de licencias. También puede especificar una fecha/hora absoluta tras la cual una licencia ya no se puede almacenar en caché.

Una vez transcurrida la fecha de caducidad de la caché, la licencia deja de ser válida y el cliente debe solicitar una nueva licencia al servidor de licencias.

Ejemplo de caso de uso: utilice la duración del almacenamiento en caché de la licencia para especificar una cantidad fija de tiempo válido para una licencia determinada, como en un caso de uso de alquiler. Se puede especificar un alquiler de 30 días (con almacenamiento en caché de licencias) para indicar la duración total de la licencia dentro de la cual se consumirá el contenido.

## Ventana de reproducción {#playback-window}

Especifica la duración de la validez de una licencia después de la primera vez que se utiliza para reproducir contenido protegido.

Ejemplo de caso de uso: Algunos modelos comerciales permiten un periodo de alquiler de 30 días, pero, una vez iniciada la reproducción, debe completarse en 48 horas. Esta duración de 48 horas de la licencia se define como la ventana de reproducción.

## Requisitos para la sincronización {#requirements-for-synchronization}

Especifica la frecuencia con la que el cliente sincronizará su estado con el servidor. Si se ha emitido una licencia fuera de banda al cliente (sin que se haya establecido contacto con un servidor de licencias), las reglas de uso pueden especificar que el cliente debe enviar mensajes de sincronización al servidor para sincronizar la hora segura del cliente y notificar el estado del cliente al servidor.

El comportamiento de sincronización se define mediante los siguientes parámetros:

* Intervalo de inicio: especifica el tiempo de espera después de la última sincronización correcta para iniciar otra solicitud de sincronización.
* Intervalo de detención rígida (opcional). No permitir la reproducción si no se ha producido una sincronización correcta en el tiempo especificado.
* Forzar probabilidad de sincronización (opcional). Probabilidad con la que el cliente debe enviar un mensaje de sincronización antes del siguiente intervalo de inicio.

>[!NOTE]
>
>Esta regla de uso es compatible con la versión 3.0 y posteriores de los clientes de Adobe Access. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente que admita el servidor de licencias. Consulte. [Versión mínima del cliente](../../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).
