---
title: Gestionar solicitudes de devolución de licencias
description: Gestionar solicitudes de devolución de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Gestionar solicitudes de devolución de licencias{#handle-license-return-requests}

Si la aplicación cliente necesita devolver una licencia, invoca la API de Actionscript `DRMManager.returnVoucher()` para iniciar el proceso. Esta API puede funcionar en modo `immediateCommit` o `confirmFirst`. Si `immediateCommit` está establecido en `true`, el cliente elimina las licencias locales inmediatamente sin esperar a que el servidor de licencias confirme que ha recibido la solicitud de devolución de las licencias. El servidor de licencias DRM de Adobe Primetime debe procesar la solicitud y enviar una respuesta al cliente. El servidor de licencias decide si el servidor de licencias procesa o no la solicitud, como la reducción de un recuento de licencias para un usuario especificado.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

La versión mínima del SDK `Adobe Primetime DRM` necesaria es la versión 5; la dirección URL de la solicitud es &quot; [!DNL /flashaccess/lreturn/v5]&quot;. Al igual que con la anulación de registro de dominio, el servidor utiliza `getRequestPhase()` para determinar si el cliente puede obtener una vista previa de una devolución de licencia.
