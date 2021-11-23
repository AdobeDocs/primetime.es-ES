---
title: Notas de la versión de PTAI 21.11.1
description: Las notas de la versión de PTAI describen las novedades o los cambios, los problemas resueltos y conocidos de Primetime Ad Insertion en el año 2021.
exl-id: 39a05f6d-431a-4416-81b1-21d82c0dbd69
source-git-commit: f4c6ef44c7f13bf8170a1f23a7ae8eba0171316a
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# Notas de la versión de Primetime Ad Insertion 21.11.1

Las notas de la versión de Primetime Ad Insertion 21.xx.x describen las novedades o los cambios, los problemas resueltos y los problemas conocidos en Primetime Ad Insertion en el año 2021.

## Novedades de PTAI 21.11.1

Cuando: Martes 9 de noviembre de 2021 de la 1:30 a las 04:30 a.m., hora del este

* [!UICONTROL EXT-X-IMAGE-STREAM-INF] ahora se puede configurar por zona.

* Roku Trick Play es totalmente compatible.

## Mejoras y correcciones en versiones anteriores

### Versión 21.10.1

Cuando: Martes 12 de octubre de 2021 de las 7:45 a la 13:45 (hora del Este)

* Servidores consolidados, servidores no productivos y no útiles eliminados.

### Versión de mantenimiento del Ad Insertion de Primetime

Cuando: Martes, 28 de septiembre de 2021 de las 5:00 a.m. a las 6:00 a.m., hora del Este

* Actualizaciones de la pila del equilibrador de carga elástica de AWS al equilibrador de carga de aplicaciones de AWS para mejorar la funcionalidad y la escalabilidad. Estos equilibradores de carga se utilizan para enrutar y solicitar el tráfico al back-end de Auditude desde la capa de Ad Insertion (SSAI/CSAI).

### Versión 21.9.1

Cuando: Martes, 7 de septiembre de 2021 de las 02:30 a las 05:30 (hora del Este)

* Actualizaciones de los componentes de infraestructura detrás de los componentes de mediación e informes de Primetime Ad Insertion (GUI de Primetime Ads).

### Versión 21.8.1

Cuando: Martes, 24 de agosto de 2021 de las 2 a las 5 horas, hora del este

* Se ha añadido compatibilidad con flujos en directo/lineales de DASH (VOD ya es compatible).

### Versión 21.5.1

Cuando: Miércoles, 26 de mayo de 2021 de las 3:30 a.m. a las 06:30 a.m. hora del Este

**Cambios**

* Se ha agregado compatibilidad con el tipo de segmentación obsoleta 0x01 (UPID) para formatos de referencia basados en SCTE.

* Se ha añadido una nueva telemetría para los próximos cambios en el tablero.

### Versión 21.4.1

**Cuando:** Jueves 22 de abril de 2021 de las 2 a las 5 a.m. hora del este

**Cambios**

* La limitación de solicitudes de sesión se habilitará para protegerse contra posibles ataques DDOS. Las sesiones se limitarán a 10 solicitudes por segundo, con un límite de 100 solicitudes en cola. No anticipamos ningún impacto para los jugadores que se comportan de acuerdo con las especificaciones HLS/DASH.

* Otras mejoras de mantenimiento y seguridad

### Versión 21.2.2

**Cuando:** Martes, 23 de febrero de 2021 de la 1 a las 04 horas, hora del este

**Cambios**

* Se ha agregado compatibilidad con la inserción/sincronización de flujo EXT-X-IMAGE-STREAM-INF en flujos HLS. La función se habilita mediante una configuración del lado del servidor. Póngase en contacto con el representante de cuentas técnicas para habilitar la función.

### Versión 21.2.1

**Cuando:** Miércoles, 3 de febrero de 2021 de la 1 a las 4 de la mañana, hora del este

**Cambios**

* Se ha agregado compatibilidad con la optimización de salida DASH: consolidación de nodos basada en el tiempo.

### Versión 21.1.2

**Cuando:** Martes 19 de enero de 2021 de las 12:30 a las 08:30 a.m., hora del este

**Cambios**

* Actualización de mantenimiento: Actualización de clústeres de memcache back-end del Ad Insertion de Primetime.

### Versión 21.1.1

**Cuando:** Miércoles, 13 de enero de 2021 de las 01:00 a las 04:00 a. m. hora del este

**Cambios**

* Se agregó compatibilidad con las ofertas de afiliados para los formatos de referencia basados en SCTE35.
