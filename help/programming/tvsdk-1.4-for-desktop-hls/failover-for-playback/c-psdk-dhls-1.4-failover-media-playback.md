---
description: Para los medios en directo y vídeo bajo demanda (VOD), TVSDK inicia la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y descarga los segmentos de medios definidos por esa lista de reproducción. Selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados, y continúa con el proceso de descarga.
title: Reproducción y failover de medios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Reproducción de medios y conmutación por error{#media-playback-and-failover}

Para los medios en directo y vídeo bajo demanda (VOD), TVSDK inicia la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y descarga los segmentos de medios definidos por esa lista de reproducción. Selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados, y continúa con el proceso de descarga.

## Falta la conmutación por error de la lista de reproducción {#section_E6B6A15930894F56A0A8501577B35E7F}

Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, TVSDK intenta recuperarse. Si no se puede recuperar, la aplicación determina el siguiente paso.

Si falta la lista de reproducción asociada a la velocidad de bits de resolución media, TVSDK busca una lista de reproducción de variante con la misma resolución. Si encuentra la misma resolución, comienza a descargar la lista de reproducción de variante y los segmentos desde la posición coincidente. Si TVSDK no encuentra la misma lista de reproducción de resolución, tratará de pasar por otras listas de reproducción de velocidad de bits y sus variantes. Una velocidad de bits inmediatamente inferior es la primera opción, luego su variante, etc. Si todas las listas de reproducción de velocidad de bits inferior y sus variantes se agotan al intentar encontrar una lista de reproducción válida, TVSDK pasará a la velocidad de bits superior y contará hacia abajo desde allí. Si no se encuentra una lista de reproducción válida, el proceso falla y el reproductor pasa al estado ERROR.

La aplicación puede determinar cómo manejar esta situación. Por ejemplo, es posible que desee cerrar la actividad del reproductor y dirigir al usuario a la actividad del catálogo. El evento de interés es el evento `STATUS_CHANGED` y la llamada de retorno correspondiente es el método `onStatusChange`. Este es un código que controla si el reproductor cambia su estado interno a ERROR:

Para obtener más información, consulte el archivo `PSDKDemo` . Los oyentes de eventos se adjuntan a la instancia de MediaPlayer.

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

Si la red del lado del cliente está inactiva, puede utilizar este código para verificarlo.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

La API proporcionará la url que se utiliza para verificar si la red del lado del cliente está inactiva. Debe ser una dirección url válida, que devuelve el código de respuesta http 200 en las solicitudes http.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

Si setNetworkDownVerifyUrl no está establecido, TVSDK utiliza la URL MainManifest de forma predeterminada para determinar si la red está inactiva.

## Falta la conmutación por error de segmento {#section_ED8CF666289042D39E9914D42BDD9BA4}

Cuando falta un segmento, por ejemplo, cuando un segmento en particular no se descarga, TVSDK intenta recuperarse mediante una variedad de intentos de conmutación por error. Si no puede recuperarse, genera un error.

Si falta un segmento en el servidor porque, por ejemplo, el archivo de manifiesto no está presente, el segmento no se puede descargar, etc., TVSDK intenta conmutarlo probando las siguientes opciones:

1. Intente realizar una conmutación por error en el mismo segmento, a la misma velocidad de bits, en un archivo de variante.
1. Cambie a una velocidad de bits alternativa (conmutador ABR) en el mismo archivo.
1. Recorra todas las tasas de bits disponibles en cada variante disponible.
1. Omita el segmento y emita una advertencia.

Cuando TVSDK no puede obtener un segmento alternativo, déclencheur una notificación de error `CONTENT_ERROR`. Esta notificación contiene una notificación interna con el código `DOWNLOAD_ERROR` . Si el flujo con el problema es una pista de audio alternativa, TVSDK genera la notificación de error `AUDIO_TRACK_ERROR`.

Si el motor de vídeo no puede obtener segmentos de forma continua, limita los saltos de segmento continuos a 5, después de los cuales se detiene la reproducción y TVSDK emite un `NATIVE_ERROR` con el código 5.

>[!NOTE]
>
>Los parámetros de control de velocidad de bits adaptable (ABR) no se tienen en cuenta cuando se produce una conmutación por error. Esto se debe a que el mecanismo de conmutación por error está diseñado para usar cualquiera de las listas de reproducción disponibles actualmente, independientemente de su perfil de velocidad de bits, como flujos de backup.
>
>Durante una operación de conmutación por error, puede haber un conmutador de perfil. Si se produce un error durante la descarga de uno de los segmentos de la lista de reproducción, se omiten parámetros de control de ABR como tasa de bits mínima/máxima permitida.

