---
description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios reproducidos localmente.
seo-description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios reproducidos localmente.
seo-title: Reproducción y conmutación por error
title: Reproducción y conmutación por error
uuid: 5d75e55d-9c01-4a36-9bdf-891289821c6b
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# Reproducción y failover {#playback-and-failover}

La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios reproducidos localmente.

Primetime no puede protegerse de errores como una interrupción de ISP o una desconexión de cable. Sin embargo, el flujo de Primetime proporciona protección de conmutación por error para proteger la reproducción de determinados fallos de servidor remoto o fallos operativos, lo que ofrece una mejor experiencia a los visores. TVSDK del explorador implementa la protección de conmutación por error para minimizar las interrupciones de reproducción y lograr una reproducción sin problemas a pesar de los problemas de transmisión. El reproductor de vídeo cambia automáticamente a un conjunto de medios de copia de seguridad cuando no están disponibles representaciones o fragmentos completos.

## Reproducción de medios {#media-playback}

Para los medios en directo y VOD, el SDK de TVSDK del explorador inicio la reproducción descargando la lista de reproducción asociada a la velocidad de bits de resolución media y, a continuación, descargando segmentos del medio de velocidad de bits de resolución media definido por la lista de reproducción.

El SDK TVSDK del explorador selecciona rápidamente la lista de reproducción de velocidad de bits de alta resolución y sus medios asociados y continúa el proceso de descarga.

## Falta la conmutación por error de la lista de reproducción {#section_81A5822C108449E1A0E94A6E25DE9E8E}

Cuando falta una lista de reproducción completa, por ejemplo, cuando no se descarga el archivo M3U8 especificado en un archivo de manifiesto de nivel superior, el SDK TVSDK del explorador intenta recuperarse. Si no se puede recuperar, la aplicación determina el paso siguiente.

Si falta la lista de reproducción asociada con la velocidad de bits de resolución media, el SDK de TVSDK del explorador buscará una lista de reproducción variante con la misma resolución. Si encuentra la misma resolución, inicio descargar la lista de reproducción variante y los segmentos desde la posición coincidente. Si TVSDK del explorador no encuentra la misma lista de reproducción de resolución, intentará desplazarse por otras listas de reproducción de velocidad de bits y sus variantes. Una velocidad de bits inmediatamente inferior es la primera opción, luego su variante, etc. Si todas las listas de reproducción de velocidad de bits inferior y sus variantes se agotan en el intento de encontrar una lista de reproducción válida, el SDK de TVSDK del explorador irá a la velocidad de bits superior y contará desde allí. Si no se encuentra una lista de reproducción válida, el proceso falla y el reproductor pasa al estado ERROR.

La aplicación puede determinar cómo manejar esta situación. Por ejemplo, puede que desee cerrar la actividad del reproductor y dirigir al usuario a la actividad del catálogo. El evento de interés es el evento de cambio de estado o estado y la llamada de retorno correspondiente es el método de cambio de estado on. Este es un código que controla si el reproductor cambia su estado interno a ERROR:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
