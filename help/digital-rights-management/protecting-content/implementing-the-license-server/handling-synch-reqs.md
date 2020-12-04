---
seo-title: Administrar solicitudes de sincronización
title: Administrar solicitudes de sincronización
uuid: e2623afb-7a57-402d-a8a1-07bcf6324d41
translation-type: tm+mt
source-git-commit: eed2ed2512c2c462cd43637d83d80bf9a5c0d490
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# Administrar solicitudes de sincronización {#handle-synchronization-requests}

Si una licencia especifica requisitos de sincronización [Requisitos para la sincronización,](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) el cliente envía periódicamente solicitudes de sincronización al servidor, según la frecuencia especificada en la licencia. Para habilitar los mensajes de sincronización, establezca `SyncFrequencyRequirements` en una PlayRight.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la dirección URL de la solicitud es &quot;URL del servidor de licencias en metadatos: + &quot; [!DNL /flashaccess/sync/v4]&quot;. De lo contrario, la dirección URL de la solicitud es &quot;URL del servidor de licencias en metadatos&quot; + &quot; [!DNL /flashaccess/sync/v3]&quot;

Los mensajes de sincronización se utilizan para sincronizar la hora del cliente con la hora del servidor. Si las licencias están incrustadas en el contenido y no es necesario recuperarlas de un servidor de licencias, es importante sincronizar el tiempo del cliente para evitar que este modifique su reloj a fin de evitar la caducidad de la licencia.

Los mensajes de sincronización también se pueden utilizar para comunicar la información del estado del cliente al servidor ( `getClientState()`) para la detección de rollback.

Consulte [Protección contra retroceso](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection).
