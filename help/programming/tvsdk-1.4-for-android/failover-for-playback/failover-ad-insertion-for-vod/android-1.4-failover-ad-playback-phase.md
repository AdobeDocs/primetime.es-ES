---
description: TVSDK descarga los segmentos de publicidad y los procesa en la pantalla del dispositivo.
title: Fase de reproducción del anuncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Fase de reproducción del anuncio{#ad-playback-phase}

TVSDK descarga los segmentos de publicidad y los procesa en la pantalla del dispositivo.

En este punto, TVSDK ha resuelto anuncios, los ha colocado en la cronología e intenta reproducir el contenido en la pantalla.

En esta fase pueden producirse las siguientes clases principales de errores:

* Errores al conectar con el servidor host
* Errores al descargar el archivo de manifiesto
* Errores al descargar los segmentos de medios

Para las tres clases de error, TVSDK reenvía eventos activados a la aplicación, incluidos los siguientes:

* Eventos de notificación activados cuando se produce una conmutación por error.
* Eventos de notificación cuando se cambia el perfil debido al algoritmo de failover.
* Los eventos de notificación se activan cuando se han tenido en cuenta todas las opciones de conmutación por error y no se puede realizar ninguna acción adicional de forma automática.

  La aplicación debe realizar la acción adecuada.

Independientemente de si se producen errores o no, TVSDK llama a onAdBreakComplete para cada uno `onAdBreakStart` y `onAdComplete` para cada `onAdStart`. Sin embargo, si no se pueden descargar los segmentos, puede haber espacios en la cronología. Cuando los huecos son lo suficientemente grandes, los valores de la posición del cabezal de reproducción y el progreso del anuncio notificado pueden mostrar discontinuidades.
