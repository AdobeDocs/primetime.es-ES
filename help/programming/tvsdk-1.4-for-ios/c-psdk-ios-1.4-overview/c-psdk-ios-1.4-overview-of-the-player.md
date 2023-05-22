---
description: TVSDK para iOS incluye una variedad de funciones.
title: Funciones de TVSDK de Primetime
exl-id: 1968c072-2651-442d-9e4c-412f7959bcab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Funciones de TVSDK de Primetime {#primetime-tvsdk-features}

TVSDK para iOS incluye una variedad de funciones y proporciona las siguientes funciones principales:

* Reproducción de VOD y en directo/lineal

   * Gestión de la ventana de reproducción, incluidos los métodos de reproducción, detención, pausa, búsqueda y recuperación de la posición del cabezal de reproducción
   * Compatibilidad con la reproducción de eventos completos
   * Subtítulos (608, WebVTT) y formas alternativas de audio para una mayor accesibilidad
   * Capacidad DVR
   * Lógica de velocidad de bits adaptable (ABR) y configuración inicial de los controles ABR
   * Suscripción a etiquetas que no son HLS y HLS
   * Compatibilidad con failover de manifiesto activo

* Publicidad

   * VPAID 2.0
   * Vinculación de anuncios del lado del cliente

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
   * Integración con la compatibilidad con Adobe Analytics y Heartbeat

* Registro

   * Registro de Debug
