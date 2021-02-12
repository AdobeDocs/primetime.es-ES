---
title: Solución de problemas y depuración
description: null
translation-type: tm+mt
source-git-commit: 242b5a2875ebc0e0020296ce9489dd54438b5ad0
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Solucionar problemas y depurar {#troubleshooting-debugging}

Primetime Ad Insertion oferta herramientas para identificar y diagnosticar problemas que pueden producirse en todas las fases del envío de vídeo, como errores de envío CDN, errores creativos de publicidad o errores de conectividad de cliente.

Primetime Ad Insertion admite el registro detallado mediante el [parámetro API de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` o `ptdebug=AdCall` en la dirección URL de arranque. Los registros se envían a los encabezados de respuesta HTTP y a la consola de Ad Insertion Primetime. Este parámetro está diseñado solo para pruebas localizadas, no para flujos de producción. Para obtener más información sobre los tipos de mensajes cuando el registro detallado está habilitado, consulte [eventos de registro ptdebug en el registro detallado](verbose-logging.md#ptdebug-logging-events).

El Ad Insertion Primetime también ofrece depuración de rendimiento en todas las solicitudes con el encabezado X-ADBE-AI-X1, que se puede utilizar para medir el rendimiento y las inserciones de anuncios en cualquier solicitud dada. Este encabezado de solicitud está disponible independientemente de si el registro detallado está habilitado. Para obtener más información, consulte [Encabezados versbose: X-ADBE-PTAI-X1](debugging-headers.md).
