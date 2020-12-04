---
description: Puede controlar los bloqueos de los flujos de vídeo en directo y proporcionar contenido alternativo durante un bloqueo.
seo-description: Puede controlar los bloqueos de los flujos de vídeo en directo y proporcionar contenido alternativo durante un bloqueo.
seo-title: Gestión de interrupciones en flujos activos
title: Gestión de interrupciones en flujos activos
uuid: df933087-c8a8-49eb-a016-6dfd971c219c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# Controlar los bloqueos en flujos activos{#handle-blackouts-in-live-streams}

Puede controlar los bloqueos de los flujos de vídeo en directo y proporcionar contenido alternativo durante un bloqueo.

Cuando se produce una interrupción en un flujo en directo, el reproductor utiliza controladores de evento para detectar la interrupción y proporcionar contenido alternativo a los usuarios que no pueden ver el flujo principal. El reproductor detecta el inicio y el final del período de interrupción, cambia la reproducción del flujo principal a un flujo alternativo y vuelve al flujo principal cuando termina el período de interrupción.

En la aplicación de cliente, se suscribe a las etiquetas de bloqueo de TVSDK. Tras recibir una notificación de nuevos objetos *metadatos temporizados*, se analizan los datos del objeto de metadatos temporizados para identificar si el objeto indica una entrada o salida de bloqueo. En el caso de los bloqueos identificados, se llama a los elementos relevantes de TVSDK para cambiar al contenido alternativo al principio de la interrupción y, de nuevo, para volver al contenido principal cuando la interrupción haya terminado.

>[!TIP]
>
>Las claves se siguen descargando del manifiesto antes de que se reproduzca el contenido.

Cuando un usuario se conecta a un flujo en directo después de que haya finalizado el período de interrupción y se desplaza hacia atrás en el tiempo hasta el período de bloqueo, se reproducirá el contenido.

>[!IMPORTANT]
>
>Si todas las solicitudes de clave fallan, se genera un error al analizar el manifiesto. Si algunas solicitudes fallan y otras tienen éxito, TVSDK intenta reproducir el contenido. Si TVSDK intenta reproducir una sección del contenido, pero no hay ninguna clave válida para descifrar este contenido, devuelve un error.

Para controlar las interrupciones en flujos en directo:

1. Configure la aplicación para detectar etiquetas de bloqueo mediante la suscripción a etiquetas de bloqueo en un manifiesto de flujo en directo.

   TVSDK no detecta etiquetas de bloqueo por sí solo; debe suscribirse a las etiquetas de bloqueo para recibir notificaciones cuando se encuentren durante el análisis de archivos de manifiesto.
1. Cree oyentes de evento para las etiquetas a las que está suscrito el reproductor.

   Cuando se produce una etiqueta a la que el reproductor se ha suscrito (por ejemplo, una etiqueta de interrupción) en los manifiestos de flujo de primer plano (contenido principal) o de fondo (contenido alternativo), TVSDK distribuye un `TimedMetadataEvent` y crea un `TimedMetadataObject` para el `TimedMetadataEvent`.
1. Implementar controladores para los eventos de metadatos temporizados tanto para los flujos de primer plano como de fondo.

   En estos controladores, obtenga las horas de inicio y finalización del período de interrupción de los objetos de evento de metadatos temporizados.
1. Prepare el `MediaPlayer` para los apagones.

   Cuando `MediaPlayer` entra en el estado PREPARADO, se calculan y preparan los rangos de interrupción y se establecen en el objeto `MediaPlayer`.

1. Para cada actualización a la posición del cursor de reproducción, compruebe la lista de `TimedMetadataObjects`.

   Aquí es donde el reproductor detecta el inicio y el final de la interrupción, y rastrea el tiempo de la interrupción a medida que se produce.

1. Cree métodos para cambiar el contenido al inicio y al final del período de interrupción.

   Cuando se inicio el período de interrupción, cambie el contenido principal al fondo y el contenido alternativo para que se convierta en el flujo principal. Continúe buscando y analizando el manifiesto original en segundo plano y siga buscando la etiqueta &quot;blackout end&quot; para que el reproductor pueda volver a unirse al flujo original cuando termine el bloqueo.

