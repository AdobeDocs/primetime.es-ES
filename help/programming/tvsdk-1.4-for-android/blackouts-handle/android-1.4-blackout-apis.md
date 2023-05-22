---
description: Puede gestionar interrupciones en emisiones de vídeo en directo y proporcionar contenido alternativo durante una interrupción.
title: Elementos de API de interrupción
exl-id: 8e4f1dc3-f2f6-4db9-b9d0-3e79d21032e9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Elementos de API de interrupción{#blackout-api-elements}

Puede gestionar interrupciones en emisiones de vídeo en directo y proporcionar contenido alternativo durante una interrupción.

Cuando se produce una interrupción en un flujo en directo, el reproductor utiliza controladores de eventos para detectar la interrupción y proporcionar contenido alternativo a los usuarios que no pueden ver el flujo principal. El reproductor detecta el inicio y el final del periodo de interrupción, cambia la reproducción del flujo principal a un flujo alternativo y vuelve al flujo principal cuando finaliza el periodo de interrupción.

Para gestionar interrupciones en emisiones en directo:

1. Configure la aplicación para que detecte etiquetas de interrupción mediante la suscripción a etiquetas de interrupción en un manifiesto de flujo en directo.

   TVSDK no detecta las etiquetas de interrupción por sí solo; debe suscribirse a las etiquetas de interrupción para recibir una notificación cuando se encuentren las etiquetas durante el análisis del archivo de manifiesto.
1. Cree oyentes de eventos para las etiquetas a las que está suscrito su reproductor (en este caso, etiquetas PLAYBACK y BLACKOUTS)

   Cuando se produce una etiqueta a la que el reproductor se ha suscrito (por ejemplo, una etiqueta de interrupción) en los manifiestos de flujo en primer plano (contenido principal) o en segundo plano (contenido alternativo), TVSDK envía un `TimedMetadataEvent` y crea un `TimedMetadataObject` para el `TimedMetadataEvent`.

1. Implemente controladores para los eventos de metadatos cronometrados para las secuencias de primer plano y de segundo plano.

   En estos controladores, obtenga las horas de inicio y finalización del periodo de interrupción desde los objetos de evento de metadatos cronometrados.
1. Cree métodos para cambiar el contenido al principio y al final del período de interrupción.

   Cuando comience el periodo de interrupción, cambie el contenido principal al fondo y cambie el contenido alternativo para que se convierta en el flujo principal. Continúe recuperando y analizando el manifiesto original en segundo plano y compruebe la etiqueta &quot;final de interrupción&quot; para que el reproductor pueda volver a unirse al flujo original cuando termine la interrupción.
1. Actualice los rangos no buscables si el rango de interrupción está en DVR en el flujo de reproducción.

   Rastree y gestione el `TimedMetadata` en el flujo en segundo plano, preparando y actualizando intervalos no buscables de interrupción.

TVSDK proporciona elementos de API que son útiles para implementar interrupciones, incluidos métodos, metadatos y notificaciones.

Puede utilizar lo siguiente al implementar una solución de interrupción en el reproductor.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Guarda el recurso cargado actualmente como recurso de fondo. If `replaceCurrentResource` se llama después de este método, TVSDK continúa descargando el manifiesto del elemento en segundo plano hasta que realice la llamada a `unregisterCurrentBackgroundItem`, `release`, o `reset`.

   * `unregisterCurrentBackgroundItem` Establece el elemento de fondo como nulo y detiene la recuperación y el análisis del manifiesto de fondo.

* **BlackoutMetadata** -

   Una clase de metadatos específica de las interrupciones.

   Esto le permite establecer intervalos no buscables (una matriz de `TimeRanges`) en TVSDK. TVSDK comprueba estos intervalos cada vez que el usuario realiza una búsqueda. Si está establecido y el usuario busca en un rango no buscable, TVSDK fuerza al visor al final del rango no buscable.

* **COMIENCE AQUÍ SIGUIENTE AdvertisingMetadata** Habilite o deshabilite el preroll en un flujo en vivo mediante la configuración `enableLivePreroll` a true o false. Si es false, TVSDK no realiza una llamada explícita al servidor de publicidad para los anuncios previos a la emisión antes de la reproducción del contenido y, por lo tanto, no reproduce el anuncio previo a la emisión. Esto no afecta a los mid-rolls. El valor predeterminado es True.

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem` - Se envía cuando detecta una etiqueta suscrita en el manifiesto de fondo y un nuevo `TimedMetadata` La instancia de se prepara a partir de ella. El `TimedMetadata` La instancia de se envía como parámetro.

   * `onBackgroundManifestFailed` : Se envía cuando el reproductor de contenido no puede cargar completamente el manifiesto de fondo, es decir, todas las direcciones URL de flujo devuelven un error o una respuesta no válida.

* **Notificaciones**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Advertencia
      * Error al descargar el manifiesto en segundo plano.
