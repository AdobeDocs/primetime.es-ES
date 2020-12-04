---
seo-title: Gestión de solicitudes de sincronización
title: Gestión de solicitudes de sincronización
uuid: 37b2db09-4c09-4216-874b-b570a84569b6
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Gestión de solicitudes de sincronización{#handling-synchronization-requests}

. Si una licencia especifica requisitos de sincronización ([Requisitos para la sincronización](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)), el cliente enviará periódicamente solicitudes de sincronización al servidor, según la frecuencia especificada en la licencia. Para activar los mensajes de sincronización, establezca SyncFrequencyRequirements en un PlayRight.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la dirección URL de la solicitud es &quot;URL del servidor de licencias en metadatos: + &quot;/flashaccess/sync/v4&quot;. De lo contrario, la dirección URL de la solicitud es &quot;URL del servidor de licencias en metadatos&quot; + &quot;/flashaccess/sync/v3&quot;

Los mensajes de sincronización se utilizan para sincronizar la hora del cliente con la hora del servidor. Si las licencias están incrustadas en el contenido y no es necesario recuperarlas de un servidor de licencias, es importante sincronizar el tiempo del cliente para evitar que este modifique su reloj a fin de evitar la caducidad de la licencia.

Los mensajes de sincronización también se pueden utilizar para comunicar la información del estado del cliente al servidor ( `getClientState()`) para la detección de rollback. Consulte [Protección contra retroceso](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).