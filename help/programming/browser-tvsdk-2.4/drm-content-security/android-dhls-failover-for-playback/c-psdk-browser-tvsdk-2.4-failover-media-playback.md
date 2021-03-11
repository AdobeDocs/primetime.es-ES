---
description: Para los contenidos en directo y VOD, el SDK de explorador inicia la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y, a continuación, descargando segmentos del medio de velocidad de bits de resolución media definido por la lista de reproducción.
title: Reproducción de medios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Reproducción de medios {#media-playback}

Para los contenidos en directo y VOD, el SDK de explorador inicia la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y, a continuación, descargando segmentos del medio de velocidad de bits de resolución media definido por la lista de reproducción.

El SDK de explorador selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados y continúa el proceso de descarga.

## Falta la conmutación por error de la lista de reproducción {#section_81A5822C108449E1A0E94A6E25DE9E8E}

Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, el Explorador TVSDK intenta recuperarse. Si no se puede recuperar, la aplicación determina el siguiente paso.

Si falta la lista de reproducción asociada a la velocidad de bits de resolución media, el SDK del explorador busca una lista de reproducción de variante con la misma resolución. Si encuentra la misma resolución, comienza a descargar la lista de reproducción de variante y los segmentos desde la posición coincidente. Si el TVSDK del explorador no encuentra la misma lista de reproducción de resolución, tratará de pasar por otras listas de reproducción de velocidad de bits y sus variantes. Una velocidad de bits inmediatamente inferior es la primera opción, luego su variante, etc. Si todas las listas de reproducción de velocidad de bits inferior y sus variantes se agotan al intentar encontrar una lista de reproducción válida, el SDK de TVSDK del explorador pasará a la velocidad de bits superior y se contará desde allí. Si no se encuentra una lista de reproducción válida, el proceso falla y el reproductor pasa al estado ERROR.

La aplicación puede determinar cómo manejar esta situación. Por ejemplo, es posible que desee cerrar la actividad del reproductor y dirigir al usuario a la actividad del catálogo. El evento de interés es el evento de cambio de estado o estado, y la llamada de retorno correspondiente es el método de cambio de estado on . Este es un código que controla si el reproductor cambia su estado interno a ERROR:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
