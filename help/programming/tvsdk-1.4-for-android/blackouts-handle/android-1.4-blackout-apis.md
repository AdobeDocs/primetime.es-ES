---
description: Puede controlar los bloqueos en los flujos de vídeo en directo y proporcionar contenido alternativo durante un apagón.
title: Elementos de API de bloqueo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# Bloqueo de elementos de API{#blackout-api-elements}

Puede controlar los bloqueos en los flujos de vídeo en directo y proporcionar contenido alternativo durante un apagón.

Cuando se produce una interrupción en una emisión en directo, el reproductor utiliza controladores de eventos para detectar la interrupción y proporcionar contenido alternativo a los usuarios que no pueden ver la emisión principal. El reproductor detecta el inicio y el final del período de interrupción, cambia la reproducción del flujo principal a un flujo alternativo y vuelve al flujo principal cuando termina el período de interrupción.

Para controlar las interrupciones en las emisiones en directo:

1. Configure la aplicación para detectar etiquetas de bloqueo suscribiéndose a etiquetas de bloqueo en un manifiesto de flujo en directo.

   TVSDK no detecta etiquetas de bloqueo por sí solo; debe suscribirse a las etiquetas de interrupción para recibir notificaciones cuando se encuentren las etiquetas durante el análisis del archivo de manifiesto.
1. Cree oyentes de eventos para las etiquetas a las que está suscrito su reproductor (en este caso, etiquetas PLAYBACK y BLACKOUTS) .

   Cuando se produce una etiqueta que el reproductor se ha suscrito a (por ejemplo, una etiqueta de bloqueo) en los manifiestos de flujo en primer plano (contenido principal) o en segundo plano (contenido alternativo), TVSDK envía un `TimedMetadataEvent` y crea un `TimedMetadataObject` para el `TimedMetadataEvent`.

1. Implemente controladores para los eventos de metadatos temporizados tanto para los flujos en primer plano como de fondo.

   En estos controladores, obtenga las horas de inicio y finalización del período de interrupción de los objetos de evento de metadatos temporizados.
1. Cree métodos para cambiar contenido al principio y al final del periodo de interrupción.

   Cuando se inicie el periodo de interrupción, cambie el contenido principal al fondo y el contenido alternativo para que se convierta en la emisión principal. Continúe recuperando y analizando el manifiesto original en segundo plano y siga comprobando la etiqueta &quot;blackout end&quot; para que el reproductor pueda volver a unirse al flujo original cuando termine el bloqueo.
1. Actualice rangos no buscables si el rango de interrupción está en DVR en el flujo de reproducción.

   Rastree y gestione el `TimedMetadata` en el flujo de fondo, preparando y actualizando intervalos no buscables de bloqueo.

TVSDK proporciona elementos de API que son útiles para implementar bloqueos, incluidos métodos, metadatos y notificaciones.

Puede utilizar lo siguiente al implementar una solución de bloqueo en el reproductor.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Guarda el recurso cargado actualmente como el recurso en segundo plano. Si se llama a `replaceCurrentResource` después de este método, TVSDK continúa descargando el manifiesto del elemento de fondo hasta que realiza una llamada a `unregisterCurrentBackgroundItem`, `release` o `reset`.

   * `unregisterCurrentBackgroundItem` Establece el elemento de fondo en nulo y deja de recuperar y analizar el manifiesto de fondo.

* **BlackoutMetadata**  -

   Una clase de metadatos específica de las interrupciones del servicio.

   Esto le permite establecer rangos que no se pueden buscar (una matriz de `TimeRanges`) en TVSDK. TVSDK comprueba estos intervalos cada vez que el usuario busca. Si está establecido y el usuario busca en un rango que no se puede buscar, TVSDK fuerza al visor al final del rango que no se puede buscar.

* **INICIE AQUÍ SIGUIENTE** AdvertisingMetadataHabilite o deshabilite la preconfiguración en una emisión en directo estableciendo  `enableLivePreroll` en true o false. Si es false, TVSDK no realiza una llamada explícita al servidor de publicidad para los anuncios previos a la emisión antes de la reproducción del contenido y, por lo tanto, no reproduce el anuncio previo a la emisión. Esto no afecta a los grupos intermedios. El valor predeterminado es true.

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem` - Se envía cuando detecta una etiqueta suscrita en el manifiesto en segundo plano y se prepara una nueva  `TimedMetadata` instancia a partir de ella. La instancia `TimedMetadata` se envía como parámetro.

   * `onBackgroundManifestFailed` : Se envía cuando el reproductor de contenidos no puede cargar completamente el manifiesto de fondo, es decir, todas las direcciones URL de flujo devuelven un error o una respuesta no válida.

* **Notificaciones**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Advertencia
      * Error en la descarga del manifiesto en segundo plano.