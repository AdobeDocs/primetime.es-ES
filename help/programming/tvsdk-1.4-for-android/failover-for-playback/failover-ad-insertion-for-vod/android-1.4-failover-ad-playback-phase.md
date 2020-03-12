---
description: TVSDK descarga los segmentos de publicidad y los procesa en la pantalla del dispositivo.
seo-description: TVSDK descarga los segmentos de publicidad y los procesa en la pantalla del dispositivo.
seo-title: Fase de reproducción de publicidad
title: Fase de reproducción de publicidad
uuid: 1bbcea08-3475-4a64-9f89-c455d5dd828e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Fase de reproducción de publicidad{#ad-playback-phase}

TVSDK descarga los segmentos de publicidad y los procesa en la pantalla del dispositivo.

En este punto, TVSDK ha resuelto las publicidades, las ha colocado en la línea de tiempo e intenta procesar el contenido en la pantalla.

En esta fase pueden producirse las siguientes clases principales de errores:

* Errores al conectarse al servidor host
* Errores al descargar el archivo de manifiesto
* Errores al descargar los segmentos de medios

Para las tres clases de error, TVSDK reenvía eventos activados a la aplicación, incluidos:

* Eventos de notificación activados cuando se produce una conmutación por error.
* Eventos de notificación cuando se cambia el perfil debido al algoritmo de conmutación por error.
* Los eventos de notificación se activan cuando se consideran todas las opciones de conmutación por error y no se puede realizar ninguna acción adicional automáticamente.

   La aplicación debe realizar la acción adecuada.

Independientemente de si se producen errores o no, TVSDK llama a onAdBreakComplete para cada `onAdBreakStart` y `onAdComplete` para cada `onAdStart`. Sin embargo, si no se pudieron descargar los segmentos, es posible que haya espacios en la línea de tiempo. Cuando los huecos son lo suficientemente grandes, los valores en la posición del cursor de reproducción y el progreso del anuncio informado pueden mostrar discontinuidades.
