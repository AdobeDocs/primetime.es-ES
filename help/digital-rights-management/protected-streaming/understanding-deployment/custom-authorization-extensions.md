---
description: Puede invocar la lógica de autorización personalizada durante la adquisición de licencia para decidir si se debe emitir una licencia al cliente solicitante.
seo-description: Puede invocar la lógica de autorización personalizada durante la adquisición de licencia para decidir si se debe emitir una licencia al cliente solicitante.
seo-title: Extensiones de autorización personalizadas
title: Extensiones de autorización personalizadas
uuid: 588b05e5-3402-4586-bbd4-58b7e9a58ee4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Extensiones de autorización personalizadas{#custom-authorization-extensions}

Puede invocar la lógica de autorización personalizada durante la adquisición de licencia para decidir si se debe emitir una licencia al cliente solicitante.

Si desea implementar su propia extensión de autorización de cliente, primero debe echar un vistazo al código de muestra que se encuentra en el directorio samples [!DNL SampleAuthorizer.java] . La versión compilada de este ejemplo se encuentra en [!DNL flashaccess-license-server-ext-sample.jar].

Si desea crear su propia extensión, debe implementar la `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` interfaz y asegurarse de que [!DNL flashaccess-license-server-exts.jar] y [!DNL commons-logging.jar] se encuentran en la ruta de compilación ( [!DNL adobe-flashaccess-sdk.jar] debe estar también en la ruta de compilación si utiliza determinados campos en `IMessageFacade`).

Si desea implementar la extensión, debe copiar los archivos jar o de clase en *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

Si desea actualizar los archivos jar o de clase, debe reiniciar el servidor antes de poder utilizar la versión actualizada. También debe agregar el nombre de clase de autorizador al archivo de configuración de inquilino.
