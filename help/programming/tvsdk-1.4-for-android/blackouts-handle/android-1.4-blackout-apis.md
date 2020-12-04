---
description: Puede controlar los bloqueos de los flujos de vídeo en directo y proporcionar contenido alternativo durante un bloqueo.
seo-description: Puede controlar los bloqueos de los flujos de vídeo en directo y proporcionar contenido alternativo durante un bloqueo.
seo-title: Elementos de la API de bloqueo
title: Elementos de la API de bloqueo
uuid: 263a8987-0c85-493a-9352-9605c877ba65
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Elementos de API de bloqueo{#blackout-api-elements}

Puede controlar los bloqueos de los flujos de vídeo en directo y proporcionar contenido alternativo durante un bloqueo.

Cuando se produce una interrupción en un flujo en directo, el reproductor utiliza controladores de evento para detectar la interrupción y proporcionar contenido alternativo a los usuarios que no pueden ver el flujo principal. El reproductor detecta el inicio y el final del período de interrupción, cambia la reproducción del flujo principal a un flujo alternativo y vuelve al flujo principal cuando termina el período de interrupción.

Para controlar las interrupciones en flujos en directo:

1. Configure la aplicación para detectar etiquetas de bloqueo mediante la suscripción a etiquetas de bloqueo en un manifiesto de flujo en directo.

   TVSDK no detecta etiquetas de bloqueo por sí solo; debe suscribirse a las etiquetas de bloqueo para recibir notificaciones cuando se encuentren durante el análisis de archivos de manifiesto.
1. Cree oyentes de evento para las etiquetas a las que está suscrito su reproductor (en este caso, las etiquetas PLAYBACK y BLACKOUTS).

   Cuando se produce una etiqueta a la que el reproductor se ha suscrito (por ejemplo, una etiqueta de interrupción) en los manifiestos de flujo de primer plano (contenido principal) o de fondo (contenido alternativo), TVSDK distribuye un `TimedMetadataEvent` y crea un `TimedMetadataObject` para el `TimedMetadataEvent`.

1. Implementar controladores para los eventos de metadatos temporizados tanto para los flujos de primer plano como de fondo.

   En estos controladores, obtenga las horas de inicio y finalización del período de interrupción de los objetos de evento de metadatos temporizados.
1. Cree métodos para cambiar el contenido al inicio y al final del período de interrupción.

   Cuando se inicio el período de interrupción, cambie el contenido principal al fondo y el contenido alternativo para que se convierta en el flujo principal. Continúe buscando y analizando el manifiesto original en segundo plano y siga buscando la etiqueta &quot;blackout end&quot; para que el reproductor pueda volver a unirse al flujo original cuando termine el bloqueo.
1. Actualice rangos no buscables si el rango de interrupción está en DVR en el flujo de reproducción.

   Rastree y gestione el `TimedMetadata` en el flujo de fondo, preparando y actualizando rangos no buscables de bloqueo.

TVSDK proporciona elementos de API que son útiles a la hora de implementar interrupciones, incluidos métodos, metadatos y notificaciones.

Puede utilizar lo siguiente al implementar una solución de bloqueo en el reproductor.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Guarda el recurso cargado actualmente como recurso de fondo. Si se llama a `replaceCurrentResource` después de este método, TVSDK continúa descargando el manifiesto del elemento de fondo hasta que llama a `unregisterCurrentBackgroundItem`, `release` o `reset`.

   * `unregisterCurrentBackgroundItem` Establece el elemento de fondo en nulo y deja de buscar y analizar el manifiesto de fondo.

* **BlackoutMetadata** -

   Una clase de metadatos específica para las interrupciones.

   Esto le permite establecer rangos no buscables (una matriz de `TimeRanges`) en TVSDK. TVSDK comprueba estos intervalos cada vez que el usuario busca. Si se establece y el usuario busca en un rango no buscable, TVSDK fuerza al visor al final del rango no buscable.

* **INICIO AQUÍ SIGUIENTE** Publicidad MetadatosHabilite o deshabilite la preconfiguración en un flujo en directo  `enableLivePreroll` en true o false. Si el valor es false, TVSDK no realiza una llamada explícita al servidor de publicidad para anuncios previos a la reproducción del contenido, por lo que no reproduce el anuncio previo. Esto no tiene ningún impacto en los rollos medios. El valor predeterminado es true.

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem` - Se distribuye cuando detecta una etiqueta suscrita en el manifiesto de fondo y se prepara una nueva  `TimedMetadata` instancia. La instancia `TimedMetadata` se distribuye como parámetro.

   * `onBackgroundManifestFailed` - Se distribuye cuando el reproductor de medios no puede cargar completamente el manifiesto en segundo plano, es decir, todas las URL de flujo devuelven un error o una respuesta no válida.

* **Notificaciones**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Advertencia
      * Error en la descarga del manifiesto en segundo plano.