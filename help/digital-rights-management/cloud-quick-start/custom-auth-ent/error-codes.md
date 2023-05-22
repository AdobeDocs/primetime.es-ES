---
title: Códigos de error BEES
description: Códigos de error BEES
copied-description: true
exl-id: 36c83ee9-7e28-442e-8076-691a1bd43a01
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Códigos de error BEES {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

Si se produce un error durante una comprobación BEES, se debe `DRMErrorEvent` se devolverá al cliente. Puede analizar las propiedades de este evento para encontrar detalles sobre la naturaleza del error. A continuación se enumera un subconjunto de posibles códigos de error.

| Error | Descripción |
|---|---|
| `3304:305` | Error de autorización genérica del DRM de Primetime Cloud al intentar gestionar una solicitud de autenticación/autorización. Normalmente no está asociado a una emisión de BEES. Si este error se encuentra de forma consistente, debe enviar un ticket de problema al equipo de DRM de Primetime Cloud junto con información de diagnóstico. |
| `3329:0` | Error específico de la aplicación (del autorizador BEES). Si no se devolvió ningún código de suberror, el texto del error mostrará detalles del problema. Por ejemplo, se ha producido un problema al analizar la respuesta o el servidor BEES no estaba disponible. |
| `3329:<HTTP error code>` | El servidor BEES emitió una respuesta HTTP distinta de 200. El código de error HTTP se devuelve al cliente en el campo suberror code. Esto podría indicar un problema de configuración o una interrupción del servidor BEES. |
| `3329:<x>` | El servidor BEES NO PERMITIÓ la solicitud de licencia. El servidor BEES especifica el código de suberror y el texto de error dentro de la respuesta JSON de `error` y `errorText` propiedades. Este tipo de respuesta no debe considerarse un error, sino una respuesta de denegación regular de su servidor BEES. |
