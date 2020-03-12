---
description: TVSDK para Android 3.4 incluye una serie de funciones que puede implementar en sus reproductores.
seo-description: TVSDK para Android 3.4 incluye una serie de funciones que puede implementar en sus reproductores.
seo-title: Funciones de Primetime TVSDK
title: Funciones de Primetime TVSDK
uuid: 6e26c09c-2858-47d1-80e8-1d7c6a468b86
translation-type: tm+mt
source-git-commit: ad58732842eb651514a47dd565e31e3d98a84c46

---


# Funciones de Primetime TVSDK {#primetime-tvsdk-features}

TVSDK para Android 3.9 incluye una serie de funciones que puede implementar en sus reproductores.

Funciones de TVSDK:

* **VOD y reproducción en directo/lineal**

   * Administración de la ventana de reproducción, incluidos los métodos que reproducen, detienen, pausan, buscan y recuperan la posición del cursor de reproducción
   * Compatibilidad con la reproducción de eventos completos
   * Subtítulos opcionales (608, 708, WebVTT) y formas alternativas de audio para aumentar la accesibilidad
   * Controles para el estilo de texto en rótulos
   * Capacidad DVR, avance rápido y rebobinado rápido (estos dos últimos se conocen como modo *de* juego truco)
   * Lógica de velocidad de bits adaptable (ABR) y configuración inicial de los controles ABR
   * Compatibilidad con failover de manifiesto en directo
   * Búferes de reproducción ajustables
   * Compatibilidad con el seguimiento de duración, tamaño y tiempo de descarga del fragmento

* **Publicidad**

   * VPAID 2.0
   * Vinculación de anuncios del lado del cliente

      * Inserción de anuncios perfecta, incluida la compatibilidad con VAST/VMAP
      * Compatibilidad con etiquetas de referencia personalizadas para anuncios
      * Compatibilidad para marcar, reemplazar y eliminar publicidades C3
      * Flujo de trabajo personalizable de inserción de publicidad o contenido, incluida la señalización de bloqueo

* **Protección del contenido**

   * Acceso a servicios relacionados con la administración de derechos digitales (DRM)
   * Reproducción de flujos HLS sin cifrar o con flujo en directo HTTP protegido (PHLS)
   * Control de salida basado en la resolución, basado en la directiva DRM

* **Seguimiento de anuncios y videos**

   * Seguimiento de eventos de QoS
   * Notificaciones que ayudan a TVSDK y a su aplicación a comunicarse asincrónicamente sobre el estado de los vídeos, los anuncios y otros elementos. Las notificaciones también registran la actividad.

* **Registro**

   * Registro de depuración
   * Compatibilidad con el seguimiento de la duración, el tamaño y el tiempo de descarga del fragmento.

* **Entrega segura**

   * Compatibilidad de entrega segura (HTTPS) para todas las llamadas procedentes de TVSDK.