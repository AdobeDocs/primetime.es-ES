---
seo-title: Gestión de solicitudes de devolución de licencias
title: Gestión de solicitudes de devolución de licencias
uuid: 994df5af-476a-4ee8-b371-8900241be83d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestión de solicitudes de devolución de licencias{#handle-license-return-requests}

Si la aplicación cliente necesita devolver una licencia, invoca la API de `DRMManager.returnVoucher()` Actionscript para iniciar el proceso. Esta API puede funcionar en un `immediateCommit` modo o en un `confirmFirst` modo. Si `immediateCommit` se establece en `true`, el cliente elimina las licencias locales inmediatamente sin esperar a que el servidor de licencias confirme que ha recibido la solicitud de devolución de las licencias. El servidor de licencias DRM de Adobe Primetime debe procesar la solicitud y enviar una respuesta al cliente. El servidor de licencias decide si el servidor de licencias procesa o no la solicitud, como la disminución de un recuento de licencias para un usuario especificado.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

La versión mínima necesaria `Adobe Primetime DRM` del SDK es la versión 5; la dirección URL de la solicitud es &quot; [!DNL /flashaccess/lreturn/v5]&quot;. Al igual que en el caso de la anulación del registro de dominio, el servidor utiliza `getRequestPhase()` para determinar si el cliente puede obtener una vista previa de una devolución de licencia.
