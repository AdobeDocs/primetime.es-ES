---
title: Resolución de problemas y depuración
description: Resolución de problemas y depuración
copied-description: true
exl-id: 1fcacd29-627d-4536-a746-16ddcfc8bc34
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Solucionar problemas y depurar {#troubleshooting-debugging}

Primetime Ad Insertion ofrece herramientas para identificar y diagnosticar los problemas que pueden producirse en todas las fases de la entrega de vídeo, como errores de entrega de CDN, errores creativos de publicidad o errores de conectividad de cliente.

El Ad Insertion de Primetime admite el registro detallado mediante el [parámetro de API del Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` o `ptdebug=AdCall` a la dirección URL del arranque. Los registros se envían a los encabezados de respuesta HTTP y a la consola del Ad Insertion Primetime. Este parámetro está diseñado para pruebas localizadas únicamente, no para flujos de producción. Para obtener más información sobre los tipos de mensajes cuando el registro detallado está habilitado, consulte [ptdebug logging events in verbose logging](verbose-logging.md#ptdebug-logging-events).

El Ad Insertion de Primetime también proporciona depuración de rendimiento en todas las solicitudes con el encabezado X-ADBE-AI-X1, que puede utilizarse para medir el rendimiento y las inserciones de anuncios en cualquier solicitud determinada. Este encabezado de solicitud está disponible independientemente de si el registro detallado está habilitado. Para obtener más información, consulte [Encabezados versátiles: X-ADBE-PTAI-X1](debugging-headers.md).
