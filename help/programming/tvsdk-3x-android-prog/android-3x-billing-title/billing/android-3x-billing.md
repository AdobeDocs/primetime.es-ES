---
description: Para dar cabida a los clientes que solo desean pagar por lo que utilizan, en lugar de una tasa fija independientemente del uso real, Adobe recopila métricas de uso y utiliza estas métricas para determinar cuánto facturar a los clientes.
seo-description: Para dar cabida a los clientes que solo desean pagar por lo que utilizan, en lugar de una tasa fija independientemente del uso real, Adobe recopila métricas de uso y utiliza estas métricas para determinar cuánto facturar a los clientes.
seo-title: Métricas de facturación
title: Métricas de facturación
uuid: 6ae9eb1e-4b03-467f-b80a-96313bd01543
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Métricas de facturación {#billing-metrics}

Para dar cabida a los clientes que solo desean pagar por lo que utilizan, en lugar de una tasa fija independientemente del uso real, Adobe recopila métricas de uso y utiliza estas métricas para determinar cuánto facturar a los clientes.

Cada vez que el reproductor genera un evento de inicio de flujo, TVSDK comienza a enviar mensajes HTTP periódicamente al sistema de facturación de Adobe. El período, conocido como duración facturable, puede ser diferente para VOD estándar, VOD pro (anuncios intermedios habilitados) y contenido activo. La duración predeterminada para cada tipo de contenido es de 30 minutos, pero el contrato con Adobe determina los valores reales.

Los mensajes contienen la siguiente información:

* Tipo de contenido (activo, lineal o VOD)
* Dirección URL del contenido
* Indica si las publicidades están habilitadas
* Indica si los anuncios medios están activados (solo VOD)
* Si el flujo está protegido por DRM
* La versión y la plataforma TVSDK

Adobe configura previamente esta disposición, pero puede trabajar con su representante de habilitación de Adobe para cambiar la disposición, en colaboración con su representante de habilitación de Adobe.

Para supervisar las estadísticas que TVSDK envía a Adobe, obtenga la URL de su representante de habilitación de Adobe y utilice una herramienta de captura de red, como Charles, para ver los datos.