---
description: Para medios en directo y VOD, el SDK de TVSDK del explorador comienza la reproducción descargando la lista de reproducción asociada con la velocidad de bits de resolución media y, a continuación, descargando segmentos del medio de velocidad de bits de resolución media definido por la lista de reproducción.
seo-description: Para medios en directo y VOD, el SDK de TVSDK del explorador comienza la reproducción descargando la lista de reproducción asociada con la velocidad de bits de resolución media y, a continuación, descargando segmentos del medio de velocidad de bits de resolución media definido por la lista de reproducción.
seo-title: Reproducción de medios
title: Reproducción de medios
uuid: 454f84fe-8077-4f37-8e62-1d6ba0fcde27
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Reproducción de medios {#media-playback}

Para medios en directo y VOD, el SDK de TVSDK del explorador comienza la reproducción descargando la lista de reproducción asociada con la velocidad de bits de resolución media y, a continuación, descargando segmentos del medio de velocidad de bits de resolución media definido por la lista de reproducción.

El SDK TVSDK del explorador selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados y continúa el proceso de descarga.

## Falta la conmutación por error de la lista de reproducción {#section_81A5822C108449E1A0E94A6E25DE9E8E}

Cuando falta una lista de reproducción completa, por ejemplo, cuando no se descarga el archivo M3U8 especificado en un archivo de manifiesto de nivel superior, el SDK TVSDK del explorador intenta recuperarse. Si no se puede recuperar, la aplicación determina el paso siguiente.

Si falta la lista de reproducción asociada con la velocidad de bits de resolución media, el SDK de TVSDK del explorador buscará una lista de reproducción variante con la misma resolución. Si encuentra la misma resolución, comienza a descargar la lista de reproducción variante y los segmentos desde la posición coincidente. Si TVSDK del explorador no encuentra la misma lista de reproducción de resolución, intentará desplazarse por otras listas de reproducción de velocidad de bits y sus variantes. Una velocidad de bits inmediatamente inferior es la primera opción, luego su variante, etc. Si todas las listas de reproducción de velocidad de bits inferior y sus variantes se agotan en el intento de encontrar una lista de reproducción válida, el SDK de TVSDK del explorador irá a la velocidad de bits superior y contará desde allí. Si no se encuentra una lista de reproducción válida, el proceso falla y el reproductor pasa al estado ERROR.

La aplicación puede determinar cómo manejar esta situación. Por ejemplo, es posible que desee cerrar la actividad del reproductor y dirigir al usuario a la actividad del catálogo. El evento de interés es el evento de cambio de estado o estado, y la llamada de retorno correspondiente es el método de cambio de estado on. Este es un código que controla si el reproductor cambia su estado interno a ERROR:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
