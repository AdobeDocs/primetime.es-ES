---
title: Limitaciones y problemas conocidos
description: Problemas conocidos en el producto.
exl-id: 08d65716-8b6a-4300-acda-fec63e1e6815
source-git-commit: dcd89849937f4893705423465be4003948739eeb
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Problemas y limitaciones conocidos {#known-issues}

Adobe se esfuerza por ofrecer una funcionalidad sólida y experiencias de usuario sin problemas a través de sus ofertas. La versión actual (versión 1.1) de Account IQ proporciona análisis de uso compartido y suscripción a proveedores de flujo continuo con un alto grado de confianza. Sin embargo, las siguientes limitaciones se solucionarán en las próximas versiones.

* Al definir cohortes en el tablero o en las páginas de informes, actualmente no hay opción de agregar métricas como **número de dispositivos** para restringir el segmento. Esta capacidad estará disponible próximamente.

* Al estimar las puntuaciones de uso compartido de cuentas individuales, Account IQ adopta un enfoque conservador que permite a las empresas actuar en el uso compartido con bueno grado de confianza. Sin embargo, este enfoque tiende a subestimar la cantidad total de uso compartido cuando se agrega entre muchas cuentas.

* La variable [Puntuación de uso compartido general](/help/AccountIQ/dashboard.md#overall-sharing-score) actualmente solo factores en [Nivel de uso compartido](/help/AccountIQ/dashboard.md#sharing-level) y [Uso de cuentas compartidas](/help/AccountIQ/dashboard.md#usage-from-shared-accounts). Las versiones futuras incorporarán métricas adicionales.

* Al definir cohortes en las páginas de informes o tableros, los selectores para MVPD y canales carecen del mecanismo de búsqueda, a partir de ahora.

* Al definir cohortes en las páginas de informes o tableros, existe una limitación para seleccionar solo hasta 10 MVPD y programadores (o canales individuales).

* La opción de exportar estadísticas de cuenta está limitada a exportar 1000 cuentas hasta ahora.

* La opción para seleccionar [Tipo de segmento](#segment-type) cuando se define Operaciones se limita a **Número fijo de cuentas**. La variable **Número variable de cuentas** estará disponible en una versión próxima.

* Las secciones Prueba comparativa, Modelos de detección, Segmentos, Instantáneas y Reglas del panel de navegación izquierdo están deshabilitadas actualmente y estarán disponibles en una versión próxima.

* Al crear [operaciones](/help/AccountIQ/operation-affecting-user-segment.md), solo puede identificar dos tipos de [Acciones](/help/AccountIQ/operation-affecting-user-segment.md) a partir de ahora: reglas de monitorización de concurrencia y acciones externas.

* Actualmente, las Operaciones solo se pueden crear y [programado](/help/AccountIQ/operation-affecting-user-segment.md#action). Las versiones futuras le permitirán pausar, reanudar y administrar por completo.

* Debido al conjunto de datos más limitado utilizado, el modo de aislamiento no refleja realmente la cantidad de uso compartido. Por lo tanto, MVPD en modo de aislamiento no puede compararse con ningún otro MVPD. <!--do we need to separate out this limitation, which is from a different persona i.e. only for Programmer persona?-->

* Al definir un [segmento](/help/AccountIQ/segments-timeframe.md) para una operación puede agregar métricas. Pero si selecciona un segmento guardado, no podrá agregar más métricas para refinar el segmento.

* La granularidad y el selector de intervalo de tiempo están limitados a una semana o un mes, lo que significa que los datos se pueden evaluar en una sola semana o en un solo mes.

* Actualmente, los intervalos predefinidos están desactivados en el selector de granularidad y marcos de tiempo, y estarán disponibles en una versión futura.
