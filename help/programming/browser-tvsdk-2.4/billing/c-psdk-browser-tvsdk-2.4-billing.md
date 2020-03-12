---
description: Para dar cabida a los clientes que solo desean pagar por lo que utilizan, en lugar de una tasa fija independientemente del uso real, Adobe recopila métricas de uso y utiliza estas métricas para determinar cuánto facturar a los clientes.
seo-description: Para dar cabida a los clientes que solo desean pagar por lo que utilizan, en lugar de una tasa fija independientemente del uso real, Adobe recopila métricas de uso y utiliza estas métricas para determinar cuánto facturar a los clientes.
seo-title: Métricas de facturación
title: Métricas de facturación
uuid: e09b77b3-89d3-44d6-be4e-e1612fbf89fc
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Información general {#billing-metrics-overview}

Para dar cabida a los clientes que solo desean pagar por lo que utilizan, en lugar de una tasa fija independientemente del uso real, Adobe recopila métricas de uso y utiliza estas métricas para determinar cuánto facturar a los clientes.

Cada vez que el reproductor genera un evento de inicio de flujo, TVSDK del explorador comienza a enviar mensajes HTTP periódicamente al sistema de facturación de Adobe. El período, conocido como duración facturable, puede ser diferente para VOD estándar, VOD pro (anuncios intermedios habilitados) y contenido activo. La duración predeterminada para cada tipo de contenido es de 30 minutos, pero el contrato con Adobe determina los valores reales.

Los mensajes contienen la siguiente información:

* Tipo de contenido (activo, lineal o VOD)
* Dirección URL del contenido
* Indica si las publicidades están habilitadas
* Indica si los anuncios medios están activados (solo VOD)
* Si el flujo está protegido por DRM
* Versión y plataforma del TVSDK del explorador

Adobe configura previamente esta disposición, pero si desea cambiar la disposición, trabaje con su representante de habilitación de Adobe.

Para supervisar las estadísticas que TVSDK del explorador envía a Adobe, obtenga la URL de su representante de habilitación de Adobe y utilice una herramienta de captura de red, por ejemplo Charles, para ver los datos.
