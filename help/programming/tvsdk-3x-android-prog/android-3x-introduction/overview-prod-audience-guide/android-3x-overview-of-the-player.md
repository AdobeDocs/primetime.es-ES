---
description: TVSDK para Android 3.4 incluye una variedad de funciones que puede implementar en los reproductores.
title: Funciones de TVSDK de Primetime
exl-id: 85c41c57-f7a7-49aa-9118-a418f27838e4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# Funciones de TVSDK de Primetime {#primetime-tvsdk-features}

TVSDK para Android 3.9 incluye una variedad de funciones que puede implementar en los reproductores.

Funciones de TVSDK:

* **Reproducción de VOD y en directo/lineal**

   * Gestión de la ventana de reproducción, incluidos los métodos de reproducción, detención, pausa, búsqueda y recuperación de la posición del cabezal de reproducción
   * Compatibilidad con la reproducción de eventos completos
   * Subtítulos (608, 708, WebVTT) y formas alternativas de audio para una mayor accesibilidad
   * Controles para aplicar estilo al texto de los subtítulos
   * Capacidad de DVR, avance rápido y rebobinado rápido (los dos últimos se conocen como *modo de truco*)
   * Lógica de velocidad de bits adaptable (ABR) y configuración inicial de los controles ABR
   * Compatibilidad con failover de manifiesto activo
   * Búferes de reproducción ajustables
   * Compatibilidad con seguimiento de duración, tamaño y tiempo para la descarga de fragmentos

* **Publicidad**

   * VPAID 2.0
   * Vinculación de anuncios del lado del cliente

      * Inserción de anuncios sin problemas, incluida la compatibilidad con VAST/VMAP
      * Compatibilidad con etiquetas de referencia personalizadas para anuncios
      * Compatibilidad para marcar, reemplazar y eliminar anuncios de C3
      * Flujo de trabajo personalizable de inserción de contenido/publicidad, incluida la señalización de interrupción

* **Protección de contenido**

   * Acceso a servicios relacionados con la gestión de derechos digitales (DRM)
   * Reproducción de flujos HLS sin cifrar o con flujo HTTP en directo protegido (PHLS)
   * Control de salida basado en resolución, basado en la política de DRM

* **Seguimiento de vídeos y anuncios**

   * Seguimiento de eventos de QoS
   * Notificaciones que ayudan a TVSDK y a su aplicación a comunicarse de forma asíncrona acerca del estado de vídeos, anuncios y otros elementos. Las notificaciones también registran la actividad.

* **Registro**

   * Registro de Debug
   * Compatibilidad de seguimiento para la duración, el tamaño y el tiempo de descarga del fragmento.

* **Envío seguro**

   * Compatibilidad con entrega segura (HTTPS) para todas las llamadas que se originan desde TVSDK.
