---
title: Solucionar problemas y depurar
description: Solucionar problemas y depurar
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Solucionar problemas y depurar {#troubleshooting-debugging}

El Ad Insertion de Primetime ofrece herramientas para identificar y diagnosticar problemas que pueden producirse en todas las fases de la entrega de vídeo, como errores de entrega de CDN, errores creativos y errores de conectividad de cliente.

El Ad Insertion de Primetime admite el registro detallado mediante [Parámetro de API de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` o `ptdebug=AdCall` a la URL de bootstrap. Los registros se envían tanto a los encabezados de respuesta HTTP como a la consola del Ad Insertion de Primetime. Este parámetro solo está diseñado para pruebas localizadas, no para flujos de producción. Para obtener más información sobre los tipos de mensajes cuando se habilita el registro detallado, consulte [eventos de registro de ptdebug en registro detallado](verbose-logging.md#ptdebug-logging-events).

El Ad Insertion de Primetime también proporciona depuración del rendimiento en todas las solicitudes con el encabezado X-ADBE-AI-X1, que se puede utilizar para medir el rendimiento y las inserciones de publicidad en cualquier solicitud determinada. Este encabezado de solicitud está disponible independientemente de si el registro detallado está habilitado o no. Para obtener más información, consulte [Encabezados detallados: X-ADBE-PTAI-X1](debugging-headers.md).
