---
description: Para los medios en directo y vídeo bajo demanda (VOD), TVSDK inicia la reproducción descargando la lista de reproducción asociada con la velocidad de bits de resolución media y descarga los segmentos de medios definidos por esa lista de reproducción. Selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados y continúa el proceso de descarga.
title: Reproducción de medios y failover
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Reproducción de medios y failover{#media-playback-and-failover}

Para los medios en directo y vídeo bajo demanda (VOD), TVSDK inicia la reproducción descargando la lista de reproducción asociada con la velocidad de bits de resolución media y descarga los segmentos de medios definidos por esa lista de reproducción. Selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados y continúa el proceso de descarga.

## Falta conmutación por error de lista de reproducción {#section_E6B6A15930894F56A0A8501577B35E7F}

Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, TVSDK intenta recuperarse. Si no se puede recuperar, la aplicación determina el siguiente paso.

Si falta la lista de reproducción asociada con la velocidad de bits de resolución media, TVSDK busca una lista de reproducción de variante con la misma resolución. Si encuentra la misma resolución, comienza a descargar la lista de reproducción de variante y los segmentos desde la posición coincidente. Si TVSDK no encuentra la misma lista de reproducción de resolución, intentará navegar por otras listas de reproducción de velocidad de bits y sus variantes. Una velocidad de bits inmediatamente inferior es la primera opción, luego su variante, etc. Si todas las listas de reproducción de velocidad de bits más baja y sus variantes se agotan en el intento de encontrar una lista de reproducción válida, TVSDK irá a la velocidad de bits superior y contará desde allí. Si no se encuentra una lista de reproducción válida, el proceso falla y el reproductor pasa al estado ERROR.

Su aplicación puede determinar cómo manejar esta situación. Por ejemplo, es posible que desee cerrar la actividad del reproductor y dirigir al usuario a la actividad del catálogo. El evento de interés es el `STATUS_CHANGED` y la llamada de retorno correspondiente es el evento `onStatusChange` método. Este es un código que monitoriza si el reproductor cambia su estado interno a ERROR:

Para obtener más información, consulte la `PSDKDemo` archivo. Los detectores de eventos se adjuntan a la instancia de MediaPlayer.

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

Si la red del lado del cliente está caída, puede utilizar este código para verificarla.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

La API proporcionará la dirección URL que se utiliza para comprobar si la red del lado del cliente está caída. Debe ser una URL válida, que devuelva el código de respuesta http 200 en solicitudes http.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

Si setNetworkDownVerificationUrl no está establecido, TVSDK utiliza la dirección URL MainManifest de forma predeterminada para determinar si la red está inactiva.

## Falta conmutación por error de segmento {#section_ED8CF666289042D39E9914D42BDD9BA4}

Cuando falta un segmento, por ejemplo cuando un segmento en particular no se puede descargar, TVSDK intenta recuperarse mediante una serie de intentos de conmutación por error. Si no se puede recuperar, genera un error.

Si falta un segmento en el servidor porque, por ejemplo, el archivo de manifiesto no está presente, el segmento no se puede descargar, etc., TVSDK intenta conmutar por error al intentar las siguientes opciones:

1. Intentar una conmutación por error al mismo segmento, a la misma velocidad de bits, en un archivo de variante.
1. Cambie a una velocidad de bits alternativa (conmutador ABR) en el mismo archivo.
1. Pasa por cada velocidad de bits disponible en cada variante disponible.
1. Omita el segmento y emita una advertencia.

Cuando TVSDK no puede obtener un segmento alternativo, déclencheur un `CONTENT_ERROR` notificación de error. Esta notificación contiene una notificación interna con el código `DOWNLOAD_ERROR` código. Si el flujo con el problema es una pista de audio alternativa, TVSDK genera el `AUDIO_TRACK_ERROR` notificación de error.

Si el motor de vídeo no puede obtener segmentos de forma continua, limita las saltas de segmento continuas a 5, después de lo cual se detiene la reproducción y TVSDK emite una `NATIVE_ERROR` con el código 5.

>[!NOTE]
>
>Los parámetros de control de velocidad de bits adaptable (ABR) no se tienen en cuenta cuando se produce una conmutación por error. Esto se debe a que el mecanismo de conmutación por error está diseñado para utilizar cualquiera de las listas de reproducción disponibles actualmente, independientemente de su perfil de velocidad de bits, como flujos de copia de seguridad.
>
>Durante una operación de conmutación por error, puede haber un conmutador de perfil. Si se produce un error durante la descarga de uno de los segmentos de la lista de reproducción, se omiten los parámetros de control ABR como la velocidad de bits mínima/máxima permitida.
