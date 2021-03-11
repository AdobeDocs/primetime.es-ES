---
title: Códigos de error BEES
description: Códigos de error BEES
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Códigos de error BEES {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

Si hay un error durante una comprobación BEES, se devolverá un `DRMErrorEvent` al cliente. Puede analizar las propiedades de este evento para encontrar detalles sobre la naturaleza del error. A continuación se enumera un subconjunto de posibles códigos de error.

| Error | Descripción |
|---|---|
| `3304:305` | Error de autorización genérica del DRM de Primetime Cloud que intenta gestionar una solicitud de autenticación/autorización. Normalmente no se asocia con un problema de BEES. Si este error se encuentra de forma coherente, debe enviar un ticket de problema al equipo de DRM de Primetime Cloud junto con información de diagnóstico. |
| `3329:0` | Error específico de la aplicación (del Autorizador de BEES). Si no se devuelve ningún código de suberror, el texto del error mostrará los detalles del problema. Por ejemplo, hubo un problema al analizar la respuesta, o el servidor BEES no estaba disponible. |
| `3329:<HTTP error code>` | El servidor BEES emitió una respuesta HTTP distinta de 200. El código de error HTTP se devuelve al cliente en el campo de código de suberror. Esto podría indicar un problema de configuración o una interrupción en el servidor BEES. |
| `3329:<x>` | EL servidor BEES DESACTIVÓ la solicitud de licencia. El servidor BEES especifica el código de suberror y el texto de error dentro de las propiedades `error` y `errorText` de la respuesta JSON. Este tipo de respuesta no debe considerarse un error, sino una respuesta de denegación regular de su servidor BEES. |