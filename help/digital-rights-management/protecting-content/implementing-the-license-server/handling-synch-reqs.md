---
title: Administrar solicitudes de sincronización
description: Administrar solicitudes de sincronización
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# Administrar solicitudes de sincronización {#handle-synchronization-requests}

Si una licencia especifica los requisitos de sincronización  [Requisitos para la sincronización,](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) el cliente envía periódicamente solicitudes de sincronización al servidor, en función de la frecuencia especificada en la licencia. Para habilitar los mensajes de sincronización, establezca `SyncFrequencyRequirements` en una PlayRight.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la URL de solicitud es &quot;URL del servidor de licencias en los metadatos: +&quot; [!DNL /flashaccess/sync/v4]&quot;. De lo contrario, la URL de solicitud es &quot;URL del servidor de licencias en los metadatos&quot; + &quot; [!DNL /flashaccess/sync/v3]&quot;

Los mensajes de sincronización se utilizan para sincronizar la hora del cliente con la hora del servidor. Si las licencias están incrustadas en el contenido y no es necesario recuperarlas de un servidor de licencias, sincronizar la hora del cliente es importante para evitar que el cliente modifique su reloj para evitar la caducidad de la licencia.

Los mensajes de sincronización también se pueden utilizar para comunicar la información de estado del cliente al servidor ( `getClientState()`) para la detección de reversiones.

Consulte [Protección contra reversiones](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection).
