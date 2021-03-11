---
description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un espectador significa que la reproducción remota puede no tener la calidad del contenido reproducido localmente.
title: Reproducción y failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Reproducción y failover {#playback-and-failover}

La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un espectador significa que la reproducción remota puede no tener la calidad del contenido reproducido localmente.

Primetime no puede protegerse de errores como una interrupción del ISP o una desconexión de cable. Sin embargo, la transmisión de Primetime proporciona protección contra fallos de conmutación por error para proteger la reproducción de ciertos fallos de funcionamiento o fallos de servidor remotos, lo que ofrece una mejor experiencia a los espectadores. El TVSDK del explorador implementa la protección de conmutación por error para minimizar las interrupciones de reproducción y lograr una reproducción sin problemas a pesar de los problemas de transmisión. El reproductor de vídeo cambia automáticamente a un conjunto de medios de copia de seguridad cuando no hay disponibles representaciones o fragmentos completos.

## Reproducción de medios {#media-playback}

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
