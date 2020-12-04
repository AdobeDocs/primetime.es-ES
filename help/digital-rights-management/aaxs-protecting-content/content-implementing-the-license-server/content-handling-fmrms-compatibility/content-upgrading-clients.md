---
seo-title: Actualización de clientes
title: Actualización de clientes
uuid: 9c9bc7da-2a97-4659-945a-554d778d30a3
translation-type: tm+mt
source-git-commit: 5cf90a75d8805fb64d7d145722ad10a1ce77a14d
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Actualizando clientes{#upgrading-clients}

Si un cliente de FMRMS 1.x se pone en contacto con un servidor de Adobe Access, el servidor debe solicitar al cliente que actualice la aplicación.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* La dirección URL de solicitud es &quot;*URL base desde 1.x content*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   A diferencia de otros controladores de solicitudes de acceso a Adobe, este controlador no proporciona acceso a ninguna información de solicitud ni requiere que se establezca ningún dato de respuesta. Cree una instancia de `FMRMSv1RequestHandler` y luego llame a `close()`