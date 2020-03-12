---
seo-title: Gestión de solicitudes de devolución de licencias
title: Gestión de solicitudes de devolución de licencias
uuid: d184faea-88cb-44f3-a253-e5314d577f17
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestión de solicitudes de devolución de licencias{#handling-license-return-requests}

Si la aplicación cliente necesita devolver una licencia, invoca la API de ActionScript de DRMManager.returnVoucher() para iniciar el proceso. Esta API puede funcionar en modo Commit inmediato o en modo confirmFirst. Si inmediatosCommit está establecido en true, el cliente eliminará las licencias locales inmediatamente, sin esperar a que el servidor de licencias confirme que ha recibido la solicitud de devolución de las licencias. El servidor de licencias de Adobe Access debe procesar la solicitud y enviar una respuesta al cliente. El servidor de licencias debe decidir si realmente hace algo con la solicitud (por ejemplo, decretar un recuento de licencias para un usuario determinado).

* La clase de controlador de solicitudes es com.adobe.flashaccess.sdk.protocol.licencisereturn.LicenseReturnHandler
* La clase de mensaje de solicitud es com.adobe.flashaccess.sdk.protocol.licencisereturn.LicenseReturnRequestMessage

La versión mínima requerida del SDK de Adobe Access es la versión 5; la dirección URL de la solicitud será &quot; `/flashaccess/lreturn/v5`&quot;. Al igual que con la anulación del registro de dominio, el servidor debe utilizar `getRequestPhase()` para determinar si el cliente está previsualizando una devolución de licencia.
