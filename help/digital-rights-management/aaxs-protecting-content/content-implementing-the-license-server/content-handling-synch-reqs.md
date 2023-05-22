---
title: Administrar solicitudes de sincronización
description: Administrar solicitudes de sincronización
copied-description: true
exl-id: bbfc6096-72df-4597-96b3-8f67a640ea8f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Administrar solicitudes de sincronización{#handling-synchronization-requests}

. Si una licencia especifica los requisitos de sincronización ([Requisitos para la sincronización](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)), el cliente enviará periódicamente solicitudes de sincronización al servidor, según la frecuencia especificada en la licencia. Para habilitar los mensajes de sincronización, establezca SyncFrequencyRequirements en un PlayRight.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la URL de solicitud es &quot;URL del servidor de licencias en los metadatos: + &quot;/flashaccess/sync/v4&quot;. De lo contrario, la URL de solicitud es &quot;URL del servidor de licencias en los metadatos&quot; + &quot;/flashaccess/sync/v3&quot;

Los mensajes de sincronización se utilizan para sincronizar la hora del cliente con la hora del servidor. Si las licencias están incrustadas en el contenido y no es necesario recuperarlas de un servidor de licencias, sincronizar la hora del cliente es importante para evitar que el cliente modifique su reloj para evitar la caducidad de la licencia.

Los mensajes de sincronización también se pueden utilizar para comunicar la información de estado del cliente al servidor ( `getClientState()`) para la detección de reversiones. Consulte [Protección contra reversiones](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).
