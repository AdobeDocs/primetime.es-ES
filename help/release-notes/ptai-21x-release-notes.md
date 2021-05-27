---
title: Notas de la versión de PTAI 21.5.1
description: Las notas de la versión de PTAI describen las novedades o los cambios, los problemas resueltos y conocidos de Primetime Ad Insertion en el año 2021.
exl-id: 39a05f6d-431a-4416-81b1-21d82c0dbd69
source-git-commit: 02e43df4d9b58b4b1ed8fdbc086771bbf3380c0f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Notas de la versión de Primetime Ad Insertion 21.5.1

Las notas de la versión de Primetime Ad Insertion 21.x.x describen las novedades o los cambios, los problemas resueltos y los problemas conocidos en Primetime Ad Insertion en el año 2021.

## Novedades de PTAI 21.5.1

Cuando:  Miércoles, 26 de mayo de 2021 de las 3:30 a.m. a las 06:30 AM ESTE

* Se ha agregado compatibilidad con el tipo de segmentación obsoleta 0x01 (UPID) para formatos de referencia basados en SCTE.
* Se ha añadido una nueva telemetría para los próximos cambios en el tablero.

## Mejoras y correcciones en versiones anteriores

### Versión 21.4.1

**Cuándo:** Jueves, 22 de abril de 2021 de las 2:00 a las 5:00 AM ORIENTE

**Cambios**

* La limitación de solicitudes de sesión se habilitará para protegerse contra posibles ataques DDOS. Las sesiones se limitarán a 10 solicitudes por segundo, con un límite de 100 solicitudes en cola. No anticipamos ningún impacto para los jugadores que se comportan de acuerdo con las especificaciones HLS/DASH.
* Otras mejoras de mantenimiento y seguridad

### Versión 21.2.2

**Cuándo:** martes, 23 de febrero de 2021, de la 1:00 a.m. a las 4:00 a.m., hora del este

**Cambios**

* Se ha agregado compatibilidad con la inserción/sincronización de flujo EXT-X-IMAGE-STREAM-INF en flujos HLS. La función se habilita mediante una configuración del lado del servidor. Póngase en contacto con el representante de cuentas técnicas para habilitar la función.

### Versión 21.2.1

**Cuándo:** miércoles, 3 de febrero de 2021, de la 1:00 a.m. a las 04:00 a.m., hora del este

**Cambios**

* Se ha agregado compatibilidad con la optimización de salida DASH: consolidación de nodos basada en el tiempo.

### Versión 21.1.2

**Cuándo:** martes, 19 de enero de 2021 de las 12:30 a las 08:30 a.m., hora del este

**Cambios**

* Actualización de mantenimiento: Actualización de clústeres de memcache back-end del Ad Insertion de Primetime.

### Versión 21.1.1

**Cuándo:** miércoles, 13 de enero de 2021, de las 01:00 a las 04:00 a.m., hora del este

**Cambios**

* Se agregó compatibilidad con las ofertas de afiliados para los formatos de referencia basados en SCTE35.
