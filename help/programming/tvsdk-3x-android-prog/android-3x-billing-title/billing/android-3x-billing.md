---
description: Para dar cabida a los clientes que solo desean pagar por lo que utilizan, en lugar de una tasa fija independientemente del uso real, los Adobes recopilan métricas de uso y utilizan estas métricas para determinar cuánto facturar a los clientes.
title: Métricas de facturación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Métricas de facturación {#billing-metrics}

Para dar cabida a los clientes que solo desean pagar por lo que utilizan, en lugar de una tasa fija independientemente del uso real, los Adobes recopilan métricas de uso y utilizan estas métricas para determinar cuánto facturar a los clientes.

Cada vez que el reproductor genera un evento de inicio de flujo, TVSDK comienza a enviar mensajes HTTP periódicamente al sistema de facturación del Adobe. El periodo, conocido como duración facturable, puede ser diferente para VOD estándar, VOD pro (anuncios mid-roll habilitados) y contenido activo. La duración predeterminada de cada tipo de contenido es de 30 minutos, pero el contrato con Adobe determina los valores reales.

Los mensajes contienen la siguiente información:

* Tipo de contenido (activo, lineal o VOD)
* URL de contenido
* Si los anuncios están habilitados
* Indica si los anuncios mid-roll están habilitados (solo VOD)
* Si el flujo está protegido por DRM
* La versión y la plataforma del TVSDK

Adobe configura previamente este arreglo, pero puede trabajar con su representante de habilitación de Adobe para cambiar el arreglo, y con su representante de habilitación de Adobe.

Para supervisar las estadísticas que TVSDK envía a Adobe, obtenga la URL de su representante de habilitación de Adobe y utilice una herramienta de captura de red, como Charles, para ver los datos.