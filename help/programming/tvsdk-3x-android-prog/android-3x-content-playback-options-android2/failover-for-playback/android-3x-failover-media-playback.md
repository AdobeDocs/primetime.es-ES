---
description: Para los contenidos en directo y vídeo bajo demanda (VOD), TVSDK inicia la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y descarga los segmentos de contenidos definidos por dicha lista de reproducción. Selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados y continúa el proceso de descarga.
title: Reproducción de medios y failover
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Reproducción de medios y failover {#media-playback-and-failover}

Para los contenidos en directo y vídeo bajo demanda (VOD), TVSDK inicia la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y descarga los segmentos de contenidos definidos por dicha lista de reproducción. Selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados y continúa el proceso de descarga.

## Falta conmutación por error de lista de reproducción {#section_4EA0AEFA7FB84FCEA699DFB10B135368}

Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, TVSDK intenta recuperarse. Si no se puede recuperar, la aplicación determina el siguiente paso.

Si falta la lista de reproducción asociada con la velocidad de bits de resolución media, TVSDK busca una lista de reproducción de variante con la misma resolución. Si encuentra la misma resolución, TVSDK comienza a descargar la lista de reproducción de variante y los segmentos desde la posición coincidente. Si el reproductor no encuentra la misma lista de reproducción de resolución, intentará pasar por otras listas de reproducción de velocidad de bits y sus variantes. Una velocidad de bits inmediatamente inferior es la primera opción, luego su variante, etc. Si todas las listas de reproducción de velocidad de bits más baja y sus variantes se agotan en el intento de encontrar una lista de reproducción válida, TVSDK irá a la velocidad de bits superior y contará desde allí. Si no se encuentra una lista de reproducción válida, el proceso falla y el reproductor pasa al estado ERROR.

Su aplicación puede determinar cómo manejar esta situación. Por ejemplo, es posible que desee cerrar la actividad del reproductor y dirigir al usuario a la actividad del catálogo. El evento de interés es el `STATUS_CHANGED` y la llamada de retorno correspondiente es el evento `onStatusChanged` método. Este es un código que monitoriza si el reproductor cambia su estado interno a `ERROR`:

```java
... 
case ERROR: 
getActivity().finish(); // this is where we close the current activity (the Player activity) 
break; 
...
```

## Falta conmutación por error de segmento {#section_D8DF377CCB644D7FB936796DA0CC5A4B}

Cuando falta un segmento, por ejemplo cuando un segmento en particular no se puede descargar, TVSDK intenta recuperarse mediante una serie de intentos de conmutación por error. Si no se puede recuperar, genera un error.

Si falta un segmento en el servidor porque, por ejemplo, el archivo de manifiesto no está presente, el segmento no se puede descargar, etc., TVSDK intenta conmutar por error al intentar las siguientes opciones:

1. Intentar una conmutación por error al mismo segmento, a la misma velocidad de bits, en un archivo de variante.
1. Cambie a una velocidad de bits alternativa (conmutador ABR) en el mismo archivo.
1. Pasa por cada velocidad de bits disponible en cada variante disponible.
1. Omita el segmento y emita una advertencia.

Cuando TVSDK no puede obtener un segmento alternativo, déclencheur un `CONTENT_ERROR` notificación de error. Esta notificación contiene una notificación interna con el `DOWNLOAD_ERROR` código. Si el flujo con el problema es una pista de audio alternativa, TVSDK genera el `AUDIO_TRACK_ERROR` notificación de error.

Si el motor de vídeo no puede obtener segmentos de forma continua, limita las saltas de segmento continuas a 5, después de lo cual se detiene la reproducción y TVSDK emite una `NATIVE_ERROR` con el código 5.

>[!NOTE]
>
>**Restricciones**
>
>Estas son algunas restricciones que debe tener en cuenta:
>
>* Los parámetros de control de velocidad de bits adaptable (ABR) no se tienen en cuenta cuando se produce una conmutación por error.
>
>  Esto se debe a que el mecanismo de conmutación por error está diseñado para utilizar cualquiera de las listas de reproducción disponibles actualmente, independientemente de su perfil de velocidad de bits, como flujos de copia de seguridad.
>* Durante una operación de conmutación por error, puede haber un conmutador de perfil.
>
>  Si se produce un error durante la descarga de uno de los segmentos de la lista de reproducción, se omiten los parámetros de control ABR como la velocidad de bits mínima/máxima permitida.
