---
title: Actualización de clientes
description: Actualización de clientes
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Actualización de clientes{#upgrading-clients}

Si un cliente de FMRMS 1.x se pone en contacto con un servidor de acceso a Adobe, el servidor debe pedir al cliente que actualice el servidor.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* La URL de solicitud es &quot;*URL base desde 1.x content*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   A diferencia de otros controladores de solicitudes de acceso a Adobe, este controlador no proporciona acceso a ninguna información de solicitud ni requiere que se establezca ningún dato de respuesta. Cree una instancia de `FMRMSv1RequestHandler` y luego llame a `close()`