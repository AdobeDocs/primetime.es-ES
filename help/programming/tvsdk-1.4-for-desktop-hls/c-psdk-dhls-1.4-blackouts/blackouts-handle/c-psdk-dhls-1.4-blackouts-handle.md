---
description: Puede gestionar interrupciones en emisiones de vídeo en directo y proporcionar contenido alternativo durante una interrupción.
title: Gestión de interrupciones en emisiones en directo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Gestión de interrupciones en emisiones en directo{#handle-blackouts-in-live-streams}

Puede gestionar interrupciones en emisiones de vídeo en directo y proporcionar contenido alternativo durante una interrupción.

Cuando se produce una interrupción en un flujo en directo, el reproductor utiliza controladores de eventos para detectar la interrupción y proporcionar contenido alternativo a los usuarios que no pueden ver el flujo principal. El reproductor detecta el inicio y el final del periodo de interrupción, cambia la reproducción del flujo principal a un flujo alternativo y vuelve al flujo principal cuando finaliza el periodo de interrupción.

En la aplicación cliente, se suscribe a las etiquetas de interrupción en TVSDK. Al recibir la notificación de nuevos *metadatos cronometrados* objetos, se analizan los datos del objeto de metadatos cronometrados para identificar si el objeto indica una entrada o salida de interrupción. En el caso de las interrupciones identificadas, se llama a los elementos de TVSDK relevantes para cambiar al contenido alternativo al principio de la interrupción y, de nuevo, para volver al contenido principal cuando haya finalizado la interrupción.

>[!TIP]
>
>Las claves se descargan del manifiesto antes de reproducir el contenido.

Cuando un usuario se conecta a un flujo en directo después de que termine el periodo de interrupción y se desplaza hacia atrás en el tiempo hasta el periodo de interrupción, se reproduce el contenido.

>[!IMPORTANT]
>
>Si todas las solicitudes de clave fallan, se genera un error al analizar el manifiesto. Si algunas solicitudes fallan y otras tienen éxito, TVSDK intenta reproducir el contenido. Si TVSDK intenta reproducir una sección del contenido, pero no hay una clave válida para descifrar este contenido, devuelve un error.

Para gestionar interrupciones en emisiones en directo:

1. Configure la aplicación para que detecte etiquetas de interrupción mediante la suscripción a etiquetas de interrupción en un manifiesto de flujo en directo.

   TVSDK no detecta las etiquetas de interrupción por sí solo; debe suscribirse a las etiquetas de interrupción para recibir una notificación cuando se encuentren las etiquetas durante el análisis del archivo de manifiesto.
1. Cree oyentes de eventos para las etiquetas a las que está suscrito el reproductor.

   Cuando se produce una etiqueta a la que el reproductor se ha suscrito (por ejemplo, una etiqueta de interrupción) en los manifiestos de flujo en primer plano (contenido principal) o en segundo plano (contenido alternativo), TVSDK envía un `TimedMetadataEvent` y crea un `TimedMetadataObject` para el `TimedMetadataEvent`.
1. Implemente controladores para los eventos de metadatos cronometrados para las secuencias de primer plano y de segundo plano.

   En estos controladores, obtenga las horas de inicio y finalización del periodo de interrupción desde los objetos de evento de metadatos cronometrados.
1. Prepare el `MediaPlayer` para apagones.

   Si la variable `MediaPlayer` entra en el estado PREPARADO, se calculan y preparan los rangos de interrupción y se establecen en el `MediaPlayer` objeto.

1. Para cada actualización de la posición del cabezal de reproducción, compruebe la lista de `TimedMetadataObjects`.

   Aquí es donde el reproductor detecta el inicio y el final de la interrupción y rastrea el tiempo de la interrupción a medida que se produce.

1. Cree métodos para cambiar el contenido al principio y al final del período de interrupción.

   Cuando comience el periodo de interrupción, cambie el contenido principal al fondo y cambie el contenido alternativo para que se convierta en el flujo principal. Continúe recuperando y analizando el manifiesto original en segundo plano y compruebe la etiqueta &quot;final de interrupción&quot; para que el reproductor pueda volver a unirse al flujo original cuando termine la interrupción.
