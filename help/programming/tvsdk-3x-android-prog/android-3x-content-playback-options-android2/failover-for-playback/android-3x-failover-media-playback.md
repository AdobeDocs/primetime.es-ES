---
description: Para medios en directo y vídeo a petición (VOD), TVSDK inicia la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y descarga los segmentos de medios definidos por esa lista de reproducción. Selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados y continúa el proceso de descarga.
seo-description: Para medios en directo y vídeo a petición (VOD), TVSDK inicia la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y descarga los segmentos de medios definidos por esa lista de reproducción. Selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados y continúa el proceso de descarga.
seo-title: Reproducción de medios y conmutación por error
title: Reproducción de medios y conmutación por error
uuid: e0072eeb-8ad1-436f-bf4a-fee6885a25bd
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Reproducción de medios y conmutación por error {#media-playback-and-failover}

Para medios en directo y vídeo a petición (VOD), TVSDK inicia la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y descarga los segmentos de medios definidos por esa lista de reproducción. Selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados y continúa el proceso de descarga.

## Falta la conmutación por error de la lista de reproducción {#section_4EA0AEFA7FB84FCEA699DFB10B135368}

Cuando falta una lista de reproducción completa, por ejemplo, cuando no se descarga el archivo M3U8 especificado en un archivo de manifiesto de nivel superior, TVSDK intenta recuperarse. Si no se puede recuperar, la aplicación determina el paso siguiente.

Si falta la lista de reproducción asociada con la velocidad de bits de resolución media, TVSDK busca una lista de reproducción variante con la misma resolución. Si encuentra la misma resolución, TVSDK empezará a descargar la lista de reproducción de variante y los segmentos desde la posición coincidente. Si el reproductor no encuentra la misma lista de reproducción de resolución, intentará desplazarse por otras listas de reproducción de velocidad de bits y sus variantes. Una velocidad de bits inmediatamente inferior es la primera opción, luego su variante, etc. Si todas las listas de reproducción de velocidad de bits inferior y sus variantes se agotan al intentar encontrar una lista de reproducción válida, TVSDK irá a la velocidad de bits superior y contará desde allí. Si no se encuentra una lista de reproducción válida, el proceso falla y el reproductor pasa al estado ERROR.

La aplicación puede determinar cómo manejar esta situación. Por ejemplo, es posible que desee cerrar la actividad del reproductor y dirigir al usuario a la actividad del catálogo. El evento de interés es el `STATUS_CHANGED` evento y la llamada de retorno correspondiente es el `onStatusChanged` método. Este es un código que controla si el reproductor cambia su estado interno a `ERROR`:

```java
... 
case ERROR: 
getActivity().finish(); // this is where we close the current activity (the Player activity) 
break; 
...
```

## Falta la conmutación por error de segmentos {#section_D8DF377CCB644D7FB936796DA0CC5A4B}

Cuando falta un segmento, por ejemplo cuando un segmento en particular no se puede descargar, TVSDK intenta recuperarse mediante una serie de intentos de conmutación por error. Si no puede recuperarse, emite un error.

Si falta un segmento en el servidor porque, por ejemplo, el archivo de manifiesto no está presente, no se puede descargar el segmento, etc., TVSDK intenta conmutarlo al intentar las siguientes opciones:

1. Intente realizar una conmutación por error en el mismo segmento, a la misma velocidad de bits, en un archivo de variante.
1. Cambie a una velocidad de bits alternativa (conmutador ABR) en el mismo archivo.
1. Recorra cada velocidad de bits disponible en cada variante disponible.
1. Omita el segmento y emite una advertencia.

Cuando TVSDK no puede obtener un segmento alternativo, activa una notificación de `CONTENT_ERROR` error. Esta notificación contiene una notificación interna con el `DOWNLOAD_ERROR` código. Si el flujo con el problema es una pista de audio alternativa, TVSDK genera la notificación de `AUDIO_TRACK_ERROR` error.

Si el motor de vídeo no puede obtener segmentos de forma continua, limita los saltos de segmento continuos a 5, tras los cuales se detiene la reproducción y TVSDK emite un error `NATIVE_ERROR` con el código 5.

>[!Rrestricciones]
>
>Estas son algunas de las restricciones que debe tener en cuenta:
>* Los parámetros de control de velocidad de bits adaptable (ABR) no se tienen en cuenta cuando se produce una conmutación por error.
>
>  
Esto se debe a que el mecanismo de conmutación por error está diseñado para utilizar como flujos de backup cualquiera de las listas de reproducción disponibles actualmente, independientemente de su perfil de velocidad de bits.
>* Durante una operación de conmutación por error, puede haber un conmutador de perfil.
>
>  
Si se produce un error durante la descarga de uno de los segmentos de la lista de reproducción, se omiten los parámetros de control de ABR, como la velocidad de bits mínima/máxima permitida.