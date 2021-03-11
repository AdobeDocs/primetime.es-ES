---
title: Gestión de solicitudes de devolución de licencias
description: Gestión de solicitudes de devolución de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Gestión de solicitudes de devolución de licencias{#handling-license-return-requests}

Si la aplicación cliente necesita devolver una licencia, invoca la API Actionscript DRMManager.returnVoucher() para iniciar el proceso. Esta API puede funcionar en modo de confirmación inmediata o en modo de confirmación. Si inmediatosCommit se establece en true, el cliente eliminará las licencias locales inmediatamente, sin esperar a que el servidor de licencias confirme que ha recibido la solicitud de devolución de las licencias. El servidor de licencias de acceso a Adobe debe procesar la solicitud y enviar una respuesta al cliente. Depende del servidor de licencias decidir si realmente hace algo con la solicitud (como reducir un recuento de licencias para el usuario dado).

* La clase del controlador de solicitud es com.adobe.flashaccess.sdk.protocol.licencisereturn.LicenseReturnHandler
* La clase de mensaje de solicitud es com.adobe.flashaccess.sdk.protocol.licencisereturn.LicenseReturnRequestMessage

La versión mínima necesaria del SDK de acceso al Adobe es la versión 5; la dirección URL de solicitud será &quot; `/flashaccess/lreturn/v5`&quot;. Al igual que con la anulación de registro del dominio, el servidor debe utilizar `getRequestPhase()` para determinar si el cliente está previsualizando una devolución de licencia.
