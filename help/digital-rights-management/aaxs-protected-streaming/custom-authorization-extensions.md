---
seo-title: Extensiones de autorización personalizadas
title: Extensiones de autorización personalizadas
description: Durante la adquisición de la licencia se puede invocar la lógica de autorización personalizada para decidir si se debe expedir una licencia al cliente solicitante.
seo-description: Durante la adquisición de la licencia se puede invocar la lógica de autorización personalizada para decidir si se debe expedir una licencia al cliente solicitante.
uuid: fb40db6f-30aa-46e3-9eeb-faff3cfedab1
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Extensiones de autorización personalizadas {#custom-authorization-extensions}

Durante la adquisición de la licencia se puede invocar la lógica de autorización personalizada para decidir si se debe expedir una licencia al cliente solicitante.

Para implementar su propia extensión de autorización de cliente, primero mire el código de muestra [!DNL SampleAuthorizer.java] ubicado en el directorio samples (la versión compilada de este ejemplo se encuentra en flashaccess-license-server-ext-sample.jar).

Para crear su propia extensión, implemente la interfaz `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` y asegúrese de que `flashaccess-license-server-exts.jar` y `commons-logging.jar` están en la ruta de compilación `adobe-flashaccess-sdk.jar` también deben estar en la ruta de compilación si utiliza ciertos campos en `IMessageFacade`). Para implementar la extensión, copie los archivos jar o de clase en *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Si necesita actualizar los archivos jar o de clase, debe reiniciar el servidor antes de utilizar la versión actualizada. También debe agregar el nombre de clase de autorizador al archivo de configuración de inquilino.
