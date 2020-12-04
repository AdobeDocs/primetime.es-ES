---
seo-title: Gestión de solicitudes de anulación del registro de dominio
title: Gestión de solicitudes de anulación del registro de dominio
uuid: 80dbbb60-9005-4a3d-86bf-26cdbed86452
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Administrar solicitudes de desregistro de dominio {#handle-domain-de-registration-requests}

Si la aplicación cliente necesita dejar un dominio, invoca la `DRMManager.removeFromDeviceGroup()`API de ActionScript o la `leaveLicenseDomain()` API de iOS para iniciar el proceso de anulación del registro del dominio. La anulación del registro de dominios es un proceso de dos fases. El cliente envía primero una solicitud de previsualización de anulación del registro. El servidor de dominio examina la solicitud y determina si el cliente puede abandonar el dominio. Se puede mostrar un error si el equipo no forma parte del dominio en este momento. Cuando la respuesta es correcta, el cliente elimina sus credenciales de dominio y todas las licencias que se hayan emitido a ese dominio. Luego envía una solicitud de anulación del registro.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la dirección URL de la solicitud es &quot;URL del servidor de dominio en metadatos: + &quot; [!DNL /flashaccess/dereg/v4]&quot;. De lo contrario, la dirección URL de la solicitud es la dirección URL del servidor de dominio en los metadatos&quot; + &quot; [!DNL /flashaccess/dereg/v3]&quot;

Al procesar las solicitudes de anulación del registro de dominio, el servidor utiliza `getRequestPhase()` para determinar si el cliente se encuentra en la fase de previsualización o cancelación del registro. En la fase de previsualización, el servidor de dominio examina la solicitud y determina si el cliente puede abandonar el dominio porque se puede denegar la solicitud; por ejemplo, la solicitud se puede denegar si el equipo no forma parte actualmente del dominio. En la fase de anulación del registro, el servidor registra el hecho de que la máquina ha abandonado el dominio. Se recomienda encarecidamente al servidor que evalúe la misma lógica en la solicitud de previsualización que en la solicitud de anulación del registro real para minimizar la posibilidad de que falle la segunda fase.
