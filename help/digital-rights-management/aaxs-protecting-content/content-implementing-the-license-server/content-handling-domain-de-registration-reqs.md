---
title: Administrar solicitudes de anulación de registro de dominios
description: Administrar solicitudes de anulación de registro de dominios
copied-description: true
exl-id: f29507b5-d32a-4b22-a02e-6701b86db133
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Administrar solicitudes de anulación de registro de dominios{#handling-domain-de-registration-requests}

Si la aplicación cliente necesita salir de un dominio, invoca el `DRMManager.removeFromDeviceGroup()`API de ActionScript para `leaveLicenseDomain()` API de iOS para iniciar el proceso de anulación de registro del dominio. La anulación del registro de dominios es un proceso de dos fases. El cliente envía primero una solicitud de previsualización de anulación de registro. El servidor de dominio examina la solicitud y determina si se permite al cliente abandonar el dominio (puede devolverse un error si el equipo no forma parte actualmente del dominio). Una vez respondida correctamente, el cliente elimina sus credenciales de dominio y las licencias emitidas para ese dominio y, a continuación, envía una solicitud de anulación de registro.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la URL de solicitud es &quot;URL del servidor de dominio en los metadatos: + &quot;/flashaccess/dereg/v4&quot;. De lo contrario, la URL de solicitud es &quot;URL del servidor de dominio en los metadatos&quot; + &quot;/flashaccess/dereg/v3&quot;

Al procesar solicitudes de anulación del registro de dominios, el servidor utiliza `getRequestPhase()` para determinar si el cliente se encuentra en la fase de previsualización o de anulación de registro. En la fase de vista previa, el servidor de dominios examina la solicitud y determina si se permite al cliente abandonar el dominio (la solicitud puede denegarse, por ejemplo, si el equipo no forma parte actualmente del dominio). En la fase de anulación de registro, el servidor registra el hecho de que el equipo ha abandonado el dominio. Se recomienda encarecidamente que el servidor evalúe la misma lógica en la solicitud de previsualización que en la solicitud de anulación de registro real para minimizar las posibilidades de que falle la segunda fase.
