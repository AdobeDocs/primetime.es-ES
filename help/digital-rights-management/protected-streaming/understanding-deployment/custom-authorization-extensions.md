---
description: Puede invocar la lógica de autorización personalizada durante la adquisición de la licencia para decidir si se debe emitir una licencia al cliente solicitante.
title: Extensiones de autorización personalizadas
exl-id: dbdda9c6-32bf-4904-981f-0029bf0a82f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# Extensiones de autorización personalizadas{#custom-authorization-extensions}

Puede invocar la lógica de autorización personalizada durante la adquisición de la licencia para decidir si se debe emitir una licencia al cliente solicitante.

Si desea implementar su propia extensión de autorización de cliente, primero debe consultar la [!DNL SampleAuthorizer.java] código de ejemplo ubicado en el directorio samples. La versión compilada de este ejemplo se encuentra en [!DNL flashaccess-license-server-ext-sample.jar].

Si desea crear su propia extensión, debe implementar el `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` interfaz y asegúrese de que [!DNL flashaccess-license-server-exts.jar] y [!DNL commons-logging.jar] se encuentran en la ruta de compilación ( [!DNL adobe-flashaccess-sdk.jar] también debe estar en la ruta de compilación si utiliza ciertos campos en `IMessageFacade`).

Si desea implementar la extensión, debe copiar los archivos jar o de clase en *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

Si desea actualizar los archivos jar o de clase, debe reiniciar el servidor antes de poder utilizar la versión actualizada. También debe agregar el nombre de clase del autorizador al archivo de configuración del inquilino.
