---
description: TVSDK descarga los segmentos de anuncio y los procesa en la pantalla del dispositivo.
title: Fase de reproducción del anuncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Fase de reproducción de anuncio{#ad-playback-phase}

TVSDK descarga los segmentos de anuncio y los procesa en la pantalla del dispositivo.

En este punto, TVSDK ha resuelto anuncios, los ha colocado en la cronología e intenta renderizar el contenido en la pantalla.

En esta fase pueden producirse las siguientes clases principales de errores:

* Errores al conectarse al servidor host
* Errores al descargar el archivo de manifiesto
* Errores al descargar los segmentos de medios

Para las tres clases de error, TVSDK reenvía a su aplicación eventos activados, incluidos:

* Eventos de notificación activados cuando se produce una conmutación por error.
* Eventos de notificación cuando se cambia el perfil debido al algoritmo de conmutación por error.
* Los eventos de notificación se activan cuando se tienen en cuenta todas las opciones de conmutación por error y no se puede realizar ninguna acción adicional automáticamente.

   La aplicación debe realizar la acción adecuada.

Tanto si se producen errores como si no, TVSDK llama a onAdBreakComplete para cada `onAdBreakStart` y `onAdComplete` para cada `onAdStart`. Sin embargo, si no se pueden descargar los segmentos, es posible que haya espacios en la cronología. Cuando los espacios son lo suficientemente grandes, los valores en la posición del cabezal de reproducción y el progreso del anuncio registrado pueden mostrar interrupciones.
