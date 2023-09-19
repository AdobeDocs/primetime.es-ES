---
description: TVSDK para Android incluye una variedad de funciones y proporciona las siguientes funciones principales
title: Funciones de TVSDK de Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Funciones de TVSDK de Primetime{#primetime-tvsdk-features}

TVSDK para Android incluye una variedad de funciones y proporciona las siguientes funciones principales:

* Reproducción de VOD y en directo/lineal

   * Gestión de la ventana de reproducción, incluidos los métodos de reproducción, detención, pausa, búsqueda y recuperación de la posición del cabezal de reproducción
   * Compatibilidad con la reproducción de eventos completos
   * Subtítulos (608, 708, WebVTT) y formas alternativas de audio para una mayor accesibilidad
   * Control del estilo del texto en los subtítulos
   * Capacidad DVR, avance rápido/rebobinado rápido (modo truco-reproducción)
   * Lógica de velocidad de bits adaptable (ABR) y configuración inicial de los controles ABR
   * Compatibilidad con failover de manifiesto activo
   * Búferes de reproducción ajustables
   * Compatibilidad con seguimiento de duración, tamaño y tiempo para la descarga de fragmentos

* Publicidad

   * VPAID 2.0
   * Vinculación de anuncios del lado del cliente

      * Inserción parcial de desglose de anuncios, que permite una experiencia similar a la de una TV de poder unirse en medio de un anuncio.
      * Inserción de anuncios sin problemas, incluida la compatibilidad con VAST/VMAP
      * Compatibilidad con etiquetas de referencia personalizadas para anuncios
      * Compatibilidad para marcar, reemplazar y eliminar anuncios de C3
      * Flujo de trabajo personalizable de inserción de contenido/publicidad, incluida la señalización de interrupción

* Protección de contenido

   * Acceso a servicios relacionados con la gestión de derechos digitales (DRM)
   * Reproducción de flujos HLS sin cifrar o con flujo HTTP en directo protegido (PHLS)
   * Control de salida basado en resolución, basado en la política de DRM

* Seguimiento de vídeos y anuncios

   * Seguimiento de eventos de QoS
   * Notificaciones que ayudan a TVSDK y a su aplicación a comunicarse de forma asíncrona sobre el estado de los vídeos, los anuncios y otros elementos, y también sobre la actividad de registro

* Registro

   * Registro de Debug
   * Compatibilidad de seguimiento para la duración, el tamaño y el tiempo de descarga del fragmento
