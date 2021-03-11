---
title: Gestión de solicitudes de sincronización
description: Gestión de solicitudes de sincronización
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Gestión de solicitudes de sincronización{#handling-synchronization-requests}

. Si una licencia especifica requisitos de sincronización ([Requisitos para la sincronización](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)), el cliente enviará periódicamente solicitudes de sincronización al servidor, según la frecuencia especificada en la licencia. Para activar los mensajes de sincronización, establezca SyncFrequencyRequirements en un PlayRight.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la URL de la solicitud es &quot;URL del servidor de licencias en los metadatos: + &quot;/flashaccess/sync/v4&quot;. De lo contrario, la URL de solicitud es &quot;URL del servidor de licencias en metadatos&quot; + &quot;/flashaccess/sync/v3&quot;

Los mensajes de sincronización se utilizan para sincronizar la hora del cliente con la hora del servidor. Si las licencias están incrustadas en el contenido y no es necesario recuperarlas de un servidor de licencias, la sincronización del tiempo del cliente es importante para evitar que el cliente modifique su reloj para evitar que caduque la licencia.

Los mensajes de sincronización también se pueden utilizar para comunicar la información del estado del cliente al servidor ( `getClientState()`) para la detección de reversión. Consulte [Protección de reversión](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).