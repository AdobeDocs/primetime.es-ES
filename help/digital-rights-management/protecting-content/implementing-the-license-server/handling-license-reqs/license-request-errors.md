---
title: Gestión de errores de solicitud de licencia
description: Gestión de errores de solicitud de licencia
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Tratamiento de errores de solicitud de licencia {#license-request-error-handling}

Si se produce un error durante el análisis de la solicitud, se produce un `HandlerParsingException`. Esta excepción incluye información de error que se devuelve al cliente. Si necesita recuperar la información del error, debe llamar a `HandlerParsingException.getErrorData()`. Si se produce un error durante la generación de una licencia debido a los requisitos de directiva de DRM que no se han cumplido, se produce un `PolicyEvaluationException`. Esta excepción también incluye `ErrorData` que se devolverá al cliente.

Consulte la documentación de API para `LicenseRequestMessage.generateLicense()` para obtener más información sobre cómo se evalúan las políticas de DRM durante la generación de licencias.
