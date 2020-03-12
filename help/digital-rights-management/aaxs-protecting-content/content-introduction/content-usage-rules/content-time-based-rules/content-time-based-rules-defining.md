---
seo-title: Definición de reglas basadas en el tiempo
title: Definición de reglas basadas en el tiempo
uuid: 17c69869-ac81-4561-9fb6-b1c5c9c4006d
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Definición de reglas basadas en el tiempo {#defining-time-based-rules}

Adobe Access utiliza la &quot;aplicación suave&quot; de las restricciones de licencia basadas en el tiempo. Si un derecho de tiempo caduca durante la reproducción de un vídeo, el comportamiento predeterminado de Adobe Access es no restringir la reproducción hasta la próxima vez que se vuelva a crear el flujo de vídeo (llamando `Netstream.stop()` y `Netstream.play()`).

Aunque la aplicación en pantalla es el comportamiento predeterminado, también puede activar la aplicación en estado estricto realizando una de las siguientes tareas:

* Pida al reproductor de vídeo que sondee periódicamente la licencia para asegurarse de que ninguna de las restricciones de tiempo ha caducado. Esto se puede lograr llamando a `DRMManager.loadVoucher(LOCAL_ONLY).`un código de error que indica que la licencia almacenada localmente ya no es válida.
* Siempre que el usuario haga clic en el botón Pausa, podrá grabar la marca de tiempo del vídeo actual y, a continuación, llamar `Netstream.stop().`Cuando el usuario haga clic en el botón Reproducir, podrá buscar la ubicación grabada y, a continuación, llamar `Netstream.play()`.

## Fecha de inicio {#start-date}

Especifica la fecha después de la cual una licencia es válida.

Ejemplo de caso de uso: Utilice una fecha absoluta para emitir licencias de contenido antes de la fecha de disponibilidad de un recurso o para aplicar un período de &quot;embargo&quot;.

## Fecha final {#end-date}

Especifica la fecha después de la cual caduca una licencia.

Ejemplo de caso de uso: Utilice una fecha de caducidad absoluta para reflejar el final de los derechos de distribución.

## Fecha final relativa {#relative-end-date}

Especifica la fecha de caducidad de la licencia, expresada en relación con la fecha de empaquetado.

Ejemplo de caso de uso: En un proceso de empaquetado automatizado, utilice una única política con esta opción para una serie de vídeos a fin de establecer la fecha de caducidad en 30 días en relación con la fecha de empaquetado.

## Duración del almacenamiento en caché de licencias {#license-caching-duration}

Especifica la duración durante la que una licencia se puede almacenar en caché en disco en el almacén de licencias local del cliente sin necesidad de volver a adquirirla en el servidor de licencias. También puede especificar una fecha y hora absolutas después de la cual una licencia ya no se puede almacenar en caché.

Una vez pasada la fecha de caducidad de la caché, la licencia ya no es válida y el cliente debe solicitar una nueva licencia al servidor de licencias.

Ejemplo de caso de uso: Utilice la duración de la caché de licencia para especificar una cantidad fija de tiempo válida para una licencia determinada, como en un caso de uso de alquiler. Se puede especificar un alquiler de 30 días (con caché de licencia) para indicar la duración total de la licencia dentro de la cual se consumirá el contenido.

## Ventana de reproducción {#playback-window}

Especifica la duración durante la que una licencia es válida la primera vez que se utiliza para reproducir contenido protegido.

Ejemplo de caso de uso: Algunos modelos de negocio permiten un período de alquiler de 30 días, pero una vez que comienza la reproducción, debe completarse en 48 horas. Esta longevidad de 48 horas de la licencia se define como la ventana de reproducción.

## Requisitos para la sincronización {#requirements-for-synchronization}

Especifica la frecuencia con la que el cliente sincronizará su estado con el servidor. Si se ha emitido una licencia fuera de banda al cliente (sin que se haya establecido contacto con un servidor de licencias), las reglas de uso pueden especificar que el cliente debe enviar mensajes de sincronización al servidor para sincronizar el tiempo seguro del cliente y notificar el estado del cliente al servidor.

El comportamiento de sincronización se define con los siguientes parámetros:

* Intervalo de inicio — Especifica cuánto tiempo se espera después de la última sincronización correcta para iniciar otra solicitud de sincronización.
* Intervalo de parada dura — (Opcional). No permitir la reproducción si no se ha producido una sincronización correcta en el tiempo especificado.
* Forzar la probabilidad de sincronización — (Opcional). Probabilidad con la que el cliente debe enviar un mensaje de sincronización antes del siguiente intervalo de inicio.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Esta regla de uso es compatible con los clientes de Adobe Access versión 3.0 y posterior. El comportamiento de los clientes más antiguos depende de la versión mínima del cliente admitida por el servidor de licencias. Consulte Versión [mínima del cliente](../../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).