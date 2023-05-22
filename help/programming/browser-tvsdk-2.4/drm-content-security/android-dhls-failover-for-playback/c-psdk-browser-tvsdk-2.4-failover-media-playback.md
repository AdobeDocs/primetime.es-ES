---
description: Para los medios en directo y VOD, el TVSDK del explorador inicia la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y, a continuación, descargando segmentos de los medios de velocidad de bits de resolución media definidos por la lista de reproducción.
title: Reproducción de contenidos
exl-id: 56033ca2-8a63-4a0d-ac7d-bf208273a238
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Reproducción de contenidos {#media-playback}

Para los medios en directo y VOD, el TVSDK del explorador inicia la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y, a continuación, descargando segmentos de los medios de velocidad de bits de resolución media definidos por la lista de reproducción.

TVSDK del explorador selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados y continúa el proceso de descarga.

## Falta conmutación por error de lista de reproducción {#section_81A5822C108449E1A0E94A6E25DE9E8E}

Cuando falta una lista de reproducción completa, por ejemplo, cuando el archivo M3U8 especificado en un archivo de manifiesto de nivel superior no se descarga, el TVSDK del explorador intenta recuperarse. Si no se puede recuperar, la aplicación determina el siguiente paso.

Si falta la lista de reproducción asociada con la velocidad de bits de resolución media, el TVSDK del explorador busca una lista de reproducción de variante con la misma resolución. Si encuentra la misma resolución, comienza a descargar la lista de reproducción de variante y los segmentos desde la posición coincidente. Si TVSDK del explorador no encuentra la misma lista de reproducción de resolución, intentará navegar por otras listas de reproducción de velocidad de bits y sus variantes. Una velocidad de bits inmediatamente inferior es la primera opción, luego su variante, etc. Si todas las listas de reproducción de velocidad de bits más baja y sus variantes se agotan en el intento de encontrar una lista de reproducción válida, TVSDK del explorador irá a la velocidad de bits superior y contará desde allí. Si no se encuentra una lista de reproducción válida, el proceso falla y el reproductor pasa al estado ERROR.

Su aplicación puede determinar cómo manejar esta situación. Por ejemplo, es posible que desee cerrar la actividad del reproductor y dirigir al usuario a la actividad del catálogo. El evento de interés es el evento de estado o estado cambiado, y la llamada de retorno correspondiente es el método on status changed. Este es un código que monitoriza si el reproductor cambia su estado interno a ERROR:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
