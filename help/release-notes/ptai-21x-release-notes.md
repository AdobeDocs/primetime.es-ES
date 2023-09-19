---
title: Notas de la versión de PTAI 21.11.1
description: Las notas de la versión de PTAI describen las novedades o los cambios, los problemas resueltos y conocidos en Primetime Ad Insertion en el año 2021.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# Notas de la versión de Primetime Ad Insertion 21.11.1

Las notas de la versión de Primetime Ad Insertion 21.xx.x describen las novedades o los cambios, los problemas resueltos y los problemas conocidos de Primetime Ad Insertion en el año 2021.

## Novedades de PTAI 21.11.1

Cuándo: martes, 9 de noviembre de 2021, de 1:30 a.m. a 04:30 a.m., hora del este

* [!UICONTROL EXT-X-IMAGE-STREAM-INF] ahora se puede configurar por zona.

* Roku Trick Play es totalmente compatible.

## Mejoras y correcciones en versiones anteriores de

### Versión 21.10.1

Cuándo: martes, 12 de octubre de 2021, de 7:45 a.m. a 1:45 p.m., hora del este

* Servidores consolidados, servidores no útiles y de producción eliminados.

### Versión de mantenimiento de Primetime Ad Insertion

Cuándo: martes, 28 de septiembre de 2021, de 5:00 a.m. a 6:00 a.m., hora del este

* Actualizaciones de la pila del equilibrador de carga de Elastic Load de AWS a Application Load Balancer de AWS para mejorar la funcionalidad y la escalabilidad. Estos equilibradores de carga se utilizan para enrutar y solicitar tráfico al backend del Auditude desde la capa del Ad Insertion (SSAI/CSAI).

### Versión 21.9.1

Cuándo: martes, 7 de septiembre de 2021 de 02:30 a.m. a 05:30 a.m., hora del este

* Actualizaciones de los componentes de infraestructura subyacentes a los componentes de mediación e informes del Ad Insertion de Primetime (GUI de Primetime Ads).

### Versión 21.8.1

Cuándo: martes, 24 de agosto de 2021 de 2:00 a.m. a 05:00 a.m., hora del este

* Se ha agregado compatibilidad con emisiones en directo/lineales DASH (VOD ya es compatible).

### Versión 21.5.1

Cuándo: Miércoles, 26 de mayo de 2021 de 3:30 a.m. a 06:30 a.m., hora del este

**Cambios**

* Se ha agregado compatibilidad con el tipo de segmentación 0x01 (UPID) obsoleto para formatos de referencia basados en SCTE.

* Se ha añadido nueva telemetría para próximos cambios en el tablero.

### Versión 21.4.1

**Cuándo:** Jueves, 22 de abril de 2021 de 2:00 a.m. a 5:00 a.m., hora del este

**Cambios**

* La limitación de solicitudes de sesión se habilitará para protegerse de posibles ataques de DDOS. Las sesiones se limitarán a 10 solicitudes por segundo, con un límite de 100 solicitudes en cola. No anticipamos ningún impacto a los jugadores que se comportan según las especificaciones de HLS/DASH.

* Otras mejoras de mantenimiento y seguridad

### Versión 21.2.2

**Cuándo:** Martes, 23 de febrero de 2021 de 1:00 a.m. a 04:00 a.m. hora del este

**Cambios**

* Se ha agregado compatibilidad con la inserción/sincronización de secuencias EXT-X-IMAGE-STREAM-INF en secuencias HLS. La función se habilita mediante una configuración del lado del servidor. Póngase en contacto con el representante de cuentas técnico para habilitar la función.

### Versión 21.2.1

**Cuándo:** Miércoles, 3 de febrero de 2021 de 1:00 a.m. a 04:00 a.m. hora del este

**Cambios**

* Se ha agregado compatibilidad con la optimización de la salida DASH: consolidación de nodos basada en el tiempo.

### Versión 21.1.2

**Cuándo:** Martes, 19 de enero de 2021 de 12:30 a.m. a 08:30 a.m., hora del este

**Cambios**

* Actualización de mantenimiento: Actualización de los clústeres de memcache del servidor del Ad Insertion Primetime.

### Versión 21.1.1

**Cuándo:** Miércoles, 13 de enero de 2021 de 01:00 a.m. a 04:00 a.m. hora del este

**Cambios**

* Se ha agregado compatibilidad con afiliadas disponibles para formatos de señal basados en SCTE35.
