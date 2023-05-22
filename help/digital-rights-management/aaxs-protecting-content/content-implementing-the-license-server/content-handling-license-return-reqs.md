---
title: Administrar solicitudes de devolución de licencia
description: Administrar solicitudes de devolución de licencia
copied-description: true
exl-id: c8813f7a-9a12-4c71-a945-cee73b6784fd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Administrar solicitudes de devolución de licencia{#handling-license-return-requests}

Si la aplicación cliente necesita devolver una licencia, invoca la API Actionscript de DRManager.returnVoucher() para iniciar el proceso. Esta API puede funcionar en modo inmediatoCommit o en modo confirmFirst. Si el valor de promptCommit se establece en true, el cliente eliminará las licencias locales inmediatamente, sin esperar la confirmación por parte del servidor de licencias de que ha recibido la solicitud para devolver las licencias. El servidor de licencias de acceso a Adobe debe procesar la solicitud y enviar una respuesta al cliente. Depende del servidor de licencias decidir si realmente hace algo con la solicitud (como disminuir el recuento de licencias para el usuario determinado).

* La clase del controlador de solicitudes es com.adobe.flashaccess.sdk.protocol.licenseReturnHandler
* La clase de mensaje de solicitud es com.adobe.flashaccess.sdk.protocol.licenseReturnRequestMessage

La versión mínima del SDK de acceso a Adobe requerida es la versión 5; la dirección URL de la solicitud será &quot; `/flashaccess/lreturn/v5`&quot;. Al igual que con la anulación del registro de dominios, el servidor debe utilizar `getRequestPhase()` para determinar si el cliente está previsualizando una devolución de licencia.
