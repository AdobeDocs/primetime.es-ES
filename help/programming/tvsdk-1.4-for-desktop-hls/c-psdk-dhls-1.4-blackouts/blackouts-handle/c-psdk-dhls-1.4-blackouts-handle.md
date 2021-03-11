---
description: Puede controlar los bloqueos en los flujos de vídeo en directo y proporcionar contenido alternativo durante un apagón.
title: Gestión de interrupciones en flujos en directo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Gestión de bloqueos en flujos en directo{#handle-blackouts-in-live-streams}

Puede controlar los bloqueos en los flujos de vídeo en directo y proporcionar contenido alternativo durante un apagón.

Cuando se produce una interrupción en una emisión en directo, el reproductor utiliza controladores de eventos para detectar la interrupción y proporcionar contenido alternativo a los usuarios que no pueden ver la emisión principal. El reproductor detecta el inicio y el final del período de interrupción, cambia la reproducción del flujo principal a un flujo alternativo y vuelve al flujo principal cuando termina el período de interrupción.

En la aplicación de cliente, se suscribe para las etiquetas de interrupción en TVSDK. Cuando se le notifica de nuevos objetos *timed metadata*, se analizan los datos del objeto de metadatos temporizados para identificar si el objeto indica una entrada o salida de interrupción. Para los bloqueos identificados, llame a los elementos relevantes del SDK de TVSDK para que cambien a contenido alternativo al principio de la interrupción y, de nuevo, para volver al contenido principal cuando termine la interrupción.

>[!TIP]
>
>Las claves se siguen descargando del manifiesto antes de que se reproduzca el contenido.

Cuando un usuario se conecta a una emisión en directo después de que haya terminado el período de interrupción y se desplaza hacia atrás en el tiempo hasta el período de exclusión, se reproduce el contenido.

>[!IMPORTANT]
>
>Si todas las solicitudes clave fallan, se produce un error al analizar el manifiesto. Si algunas solicitudes fallan y otras se realizan correctamente, TVSDK intenta reproducir el contenido. Si TVSDK intenta reproducir una sección del contenido, pero no hay una clave válida para descifrar este contenido, devuelve un error.

Para controlar las interrupciones en las emisiones en directo:

1. Configure la aplicación para detectar etiquetas de bloqueo suscribiéndose a etiquetas de bloqueo en un manifiesto de flujo en directo.

   TVSDK no detecta etiquetas de bloqueo por sí solo; debe suscribirse a las etiquetas de interrupción para recibir notificaciones cuando se encuentren las etiquetas durante el análisis del archivo de manifiesto.
1. Cree oyentes de eventos para las etiquetas a las que está suscrito su reproductor.

   Cuando se produce una etiqueta que el reproductor se ha suscrito a (por ejemplo, una etiqueta de bloqueo) en los manifiestos de flujo en primer plano (contenido principal) o en segundo plano (contenido alternativo), TVSDK envía un `TimedMetadataEvent` y crea un `TimedMetadataObject` para el `TimedMetadataEvent`.
1. Implemente controladores para los eventos de metadatos temporizados tanto para los flujos en primer plano como de fondo.

   En estos controladores, obtenga las horas de inicio y finalización del período de interrupción de los objetos de evento de metadatos temporizados.
1. Prepare el `MediaPlayer` para los apagones.

   Cuando el `MediaPlayer` entra en el estado PREPARADO, se calculan y se preparan los intervalos de bloqueo y se establecen en el objeto `MediaPlayer`.

1. Para cada actualización a la posición del cabezal de reproducción, compruebe la lista de `TimedMetadataObjects`.

   Aquí es donde el reproductor detecta el inicio y el final de la interrupción y rastrea el tiempo de la interrupción a medida que se produce.

1. Cree métodos para cambiar contenido al principio y al final del periodo de interrupción.

   Cuando se inicie el periodo de interrupción, cambie el contenido principal al fondo y el contenido alternativo para que se convierta en la emisión principal. Continúe recuperando y analizando el manifiesto original en segundo plano y siga comprobando la etiqueta &quot;blackout end&quot; para que el reproductor pueda volver a unirse al flujo original cuando termine el bloqueo.

