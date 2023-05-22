---
title: Actualización de clientes
description: Actualización de clientes
copied-description: true
exl-id: 0476c9ef-3622-4bc5-bb24-f8543470b7d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# Actualización de clientes{#upgrading-clients}

Si un cliente de FMRMS 1.x se pone en contacto con un servidor de acceso a Adobe, el servidor debe pedir al cliente que actualice.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* La URL de solicitud es &quot;*URL base del contenido 1.x*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   A diferencia de otros controladores de solicitudes de acceso de Adobe, este controlador no proporciona acceso a ninguna información de solicitud ni requiere que se establezcan datos de respuesta. Cree una instancia de `FMRMSv1RequestHandler`y, a continuación, invoque `close()`
