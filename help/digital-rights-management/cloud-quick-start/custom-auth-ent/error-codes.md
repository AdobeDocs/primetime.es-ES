---
seo-title: Códigos de error BEES
title: Códigos de error BEES
uuid: 7b2d0dd1-9a43-47e3-b932-a4eaf784ae7a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Códigos de error BEES {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

Si se produce un error durante una comprobación de BEES, se `DRMErrorEvent` devolverá un mensaje al cliente. Puede analizar las propiedades de este evento para encontrar detalles sobre la naturaleza del error. A continuación se muestra un subconjunto de posibles códigos de error.

| Error | Descripción |
|---|---|
| `3304:305` | Error de autorización genérica de Primetime Cloud DRM al intentar gestionar una solicitud de autenticación/autorización. Normalmente no se asocia con un problema de BEES. Si este error se detecta de forma constante, debe enviar un ticket de problema al equipo de DRM de Primetime Cloud junto con información de diagnóstico. |
| `3329:0` | Error específico de la aplicación (del autorizador de BEES). Si no se devuelve ningún código de suberror, el texto de error mostrará los detalles del problema. Por ejemplo, se produjo un problema al analizar la respuesta o no se pudo acceder al servidor BEES. |
| `3329:<HTTP error code>` | El servidor BEES emitió una respuesta HTTP distinta de 200. El código de error HTTP se devuelve al cliente en el campo de código de suberror. Esto podría indicar un problema de configuración o una interrupción del servidor BEES. |
| `3329:<x>` | EL servidor BEES DESHABILITÓ la solicitud de licencia. El servidor BEES especifica el código de suberror y el texto de error dentro de las propiedades `error` y `errorText` de la respuesta JSON. Este tipo de respuesta no debe considerarse un error, sino una respuesta de denegación regular del servidor BEES. |