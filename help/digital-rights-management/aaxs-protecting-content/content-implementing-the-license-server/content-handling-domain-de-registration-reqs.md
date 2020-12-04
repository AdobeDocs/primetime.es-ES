---
seo-title: Gestión de solicitudes de anulación del registro de dominio
title: Gestión de solicitudes de anulación del registro de dominio
uuid: 6f056b2b-374d-4e4d-926a-68605b2c923b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Gestión de solicitudes de desregistro de dominio{#handling-domain-de-registration-requests}

Si la aplicación cliente necesita dejar un dominio, invoca la `DRMManager.removeFromDeviceGroup()`API de ActionScript o la `leaveLicenseDomain()` API de iOS para iniciar el proceso de anulación del registro del dominio. La anulación del registro de dominios es un proceso de dos fases. El cliente envía primero una solicitud de previsualización de anulación del registro. El servidor de dominio examina la solicitud y determina si el cliente puede abandonar el dominio (se puede devolver un error si el equipo no forma parte actualmente del dominio). Si la respuesta es correcta, el cliente elimina sus credenciales de dominio y todas las licencias emitidas a ese dominio y, a continuación, envía una solicitud de anulación del registro.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la dirección URL de la solicitud es &quot;URL del servidor de dominio en metadatos: + &quot;/flashaccess/dereg/v4&quot;. De lo contrario, la URL de la solicitud es la URL del servidor de dominio en los metadatos&quot; + &quot;/flashaccess/dereg/v3&quot;

Al procesar las solicitudes de anulación del registro de dominio, el servidor utiliza `getRequestPhase()` para determinar si el cliente se encuentra en la fase de previsualización o cancelación del registro. En la fase de previsualización, el servidor de dominio examina la solicitud y determina si el cliente puede abandonar el dominio (la solicitud puede ser denegada, por ejemplo, si el equipo no forma parte actualmente del dominio). En la fase de anulación del registro, el servidor registra el hecho de que la máquina ha abandonado el dominio. Se recomienda encarecidamente al servidor que evalúe la misma lógica en la solicitud de previsualización que en la solicitud de anulación del registro real para minimizar la posibilidad de que falle la segunda fase.
