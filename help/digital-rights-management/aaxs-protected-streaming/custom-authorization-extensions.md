---
title: Extensiones de autorización personalizadas
description: Durante la adquisición de la licencia se puede invocar la lógica de autorización personalizada para decidir si se debe emitir una licencia al cliente solicitante.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Extensiones de autorización personalizadas {#custom-authorization-extensions}

Durante la adquisición de la licencia se puede invocar la lógica de autorización personalizada para decidir si se debe emitir una licencia al cliente solicitante.

Para implementar su propia extensión de autorización de cliente, consulte primero la [!DNL SampleAuthorizer.java] código de ejemplo ubicado en el directorio samples (la versión compilada de este ejemplo se encuentra en flashaccess-license-server-ext-sample.jar).

Para crear su propia extensión, implemente la `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` interfaz y asegúrese de que `flashaccess-license-server-exts.jar` y `commons-logging.jar` están en la ruta de compilación `adobe-flashaccess-sdk.jar` también debe estar en la ruta de compilación si utiliza ciertos campos en `IMessageFacade`). Para implementar la extensión, copie los archivos jar o de clase en *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Si necesita actualizar los archivos jar o de clase, debe reiniciar el servidor antes de utilizar la versión actualizada. También debe agregar el nombre de clase del autorizador al archivo de configuración del inquilino.
