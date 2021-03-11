---
title: Gestión de solicitudes de anulación de registro de dominios
description: Gestión de solicitudes de anulación de registro de dominios
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Gestión de solicitudes de anulación de registro de dominio {#handle-domain-de-registration-requests}

Si la aplicación cliente debe dejar un dominio, invoca la API de ActionScript `DRMManager.removeFromDeviceGroup()`o la API de iOS `leaveLicenseDomain()` para iniciar el proceso de anulación del registro del dominio. La anulación del registro de dominios es un proceso de dos fases. El cliente envía primero una solicitud de vista previa de anulación del registro. El servidor de dominio examina la solicitud y determina si el cliente puede abandonar el dominio. Puede devolverse un error si el equipo no forma parte actualmente del dominio. Cuando la respuesta es correcta, el cliente elimina sus credenciales de dominio y las licencias que se hayan emitido para ese dominio. A continuación, envía una solicitud de anulación del registro.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la URL de solicitud es &quot;URL del servidor de dominio en metadatos: + &quot; [!DNL /flashaccess/dereg/v4]&quot;. De lo contrario, la URL de solicitud es la URL del servidor de dominio en los metadatos&quot; + &quot; [!DNL /flashaccess/dereg/v3]&quot;

Al procesar las solicitudes de anulación de registro de dominios, el servidor utiliza `getRequestPhase()` para determinar si el cliente se encuentra en la fase de vista previa o de anulación de registro. En la fase de vista previa, el servidor de dominio examina la solicitud y determina si el cliente puede abandonar el dominio porque se puede denegar la solicitud; por ejemplo, la solicitud se puede denegar si el equipo no forma parte actualmente del dominio. En la fase de anulación del registro, el servidor registra el hecho de que el equipo ha abandonado el dominio. Se recomienda encarecidamente al servidor evaluar la misma lógica en la solicitud de vista previa que en la solicitud de anulación del registro real para minimizar la probabilidad de que falle la segunda fase.
