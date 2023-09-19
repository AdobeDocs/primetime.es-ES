---
title: Gestión de errores de solicitud de licencia
description: Gestión de errores de solicitud de licencia
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Gestión de errores de solicitud de licencia {#license-request-error-handling}

Si se produce un error durante el análisis de la solicitud, `HandlerParsingException` ocurre. Esta excepción incluye información de error que se devuelve al cliente. Si necesita recuperar la información del error, debe llamar a `HandlerParsingException.getErrorData()`. Si se produce un error durante la generación de una licencia debido a que no se han cumplido los requisitos de la directiva DRM, una `PolicyEvaluationException` ocurre. Esta excepción también incluye `ErrorData` para que se devuelva al cliente.

Consulte la documentación de la API para `LicenseRequestMessage.generateLicense()` para obtener más información sobre cómo se evalúan las políticas de DRM durante la generación de licencias.
