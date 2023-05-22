---
title: Administrar solicitudes de devolución de licencia
description: Administrar solicitudes de devolución de licencia
copied-description: true
exl-id: de577cb9-4ede-440e-8b71-1b39c6cc3c5b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Administrar solicitudes de devolución de licencia{#handle-license-return-requests}

Si la aplicación cliente necesita devolver una licencia, invoca el método `DRMManager.returnVoucher()` La API de Actionscript para iniciar el proceso. Esta API puede funcionar en un `immediateCommit` o un `confirmFirst` modo. If `immediateCommit` se establece en `true`, el cliente elimina las licencias locales inmediatamente sin esperar la confirmación del servidor de licencias de que ha recibido la solicitud para devolver las licencias. El servidor de licencias DRM de Adobe Primetime debe procesar la solicitud y enviar una respuesta al cliente. El servidor de licencias decide si procesa o no la solicitud, como reducir el recuento de licencias de un usuario especificado.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

El mínimo `Adobe Primetime DRM` La versión necesaria del SDK es la 5; la dirección URL de la solicitud es &quot; [!DNL /flashaccess/lreturn/v5]&quot;. Al igual que con la anulación del registro de dominios, el servidor utiliza `getRequestPhase()` para determinar si el cliente puede obtener una vista previa de una devolución de licencia.
