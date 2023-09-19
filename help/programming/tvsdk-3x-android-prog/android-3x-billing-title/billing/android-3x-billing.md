---
description: Para dar cabida a los clientes que desean pagar únicamente por lo que utilizan, en lugar de una tasa fija independientemente del uso real, los Adobes recopilan las métricas de uso y las utilizan para determinar cuánto facturar a los clientes.
title: Métricas de facturación
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Métricas de facturación {#billing-metrics}

Para dar cabida a los clientes que desean pagar únicamente por lo que utilizan, en lugar de una tasa fija independientemente del uso real, los Adobes recopilan las métricas de uso y las utilizan para determinar cuánto facturar a los clientes.

Cada vez que el reproductor genera un evento de inicio de flujo, TVSDK comienza a enviar mensajes HTTP periódicamente al sistema de facturación de Adobe. El periodo, conocido como duración facturable, puede ser diferente para VOD estándar, PRO VOD (anuncios mid-roll habilitados) y contenido en directo. La duración predeterminada de cada tipo de contenido es de 30 minutos, pero el contrato con el Adobe determina los valores reales.

Los mensajes contienen la siguiente información:

* Tipo de contenido (activo, lineal o VOD)
* URL de contenido
* Si los anuncios están habilitados
* Si los anuncios mid-roll están habilitados (solo VOD)
* Si el flujo está protegido por DRM
* La versión y plataforma de TVSDK

Adobe preconfigura esta disposición, pero puede trabajar con su representante de habilitación de Adobe para cambiar la disposición y con su representante de habilitación de Adobe.

Para supervisar las estadísticas que TVSDK envía al Adobe, obtenga la URL de su representante de habilitación de Adobe y utilice una herramienta de captura de red, como Charles, para ver los datos.
