---
seo-title: Gestión de errores de solicitud de licencia
title: Gestión de errores de solicitud de licencia
uuid: 4563f546-77fe-4fb9-9ad8-a0689fe6fb4d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Gestión de errores de solicitud de licencia {#license-request-error-handling}

Si se produce un error durante el análisis de la solicitud, se produce un `HandlerParsingException`. Esta excepción incluye la información de error que se devuelve al cliente. Si necesita recuperar la información del error, debe llamar a `HandlerParsingException.getErrorData()`. Si se produce un error durante la generación de una licencia debido a los requisitos de directiva DRM que no se han cumplido, se produce un `PolicyEvaluationException`. Esta excepción también incluye `ErrorData` que se devolverá al cliente.

Consulte la documentación de API para `LicenseRequestMessage.generateLicense()` para obtener más información sobre cómo se evalúan las políticas de DRM durante la generación de licencias.
