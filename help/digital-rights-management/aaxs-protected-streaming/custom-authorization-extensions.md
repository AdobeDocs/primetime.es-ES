---
title: Extensiones de autorización personalizadas
description: Durante la adquisición de la licencia, se puede invocar la lógica de autorización personalizada para decidir si se debe conceder una licencia al cliente solicitante.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Extensiones de autorización personalizadas {#custom-authorization-extensions}

Durante la adquisición de la licencia, se puede invocar la lógica de autorización personalizada para decidir si se debe conceder una licencia al cliente solicitante.

Para implementar su propia extensión de autorización de cliente, en primer lugar consulte el código de muestra [!DNL SampleAuthorizer.java] ubicado en el directorio samples (la versión compilada de este ejemplo se encuentra en flashaccess-license-server-ext-sample.jar).

Para crear su propia extensión, implemente la interfaz `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` y asegúrese de que `flashaccess-license-server-exts.jar` y `commons-logging.jar` estén en la ruta de compilación `adobe-flashaccess-sdk.jar` también deben estar en la ruta de compilación si utiliza ciertos campos en `IMessageFacade`). Para implementar la extensión, copie los archivos jar o de clase en *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Si necesita actualizar los archivos jar o de clase , el servidor debe reiniciarse antes de utilizar la versión actualizada. También debe agregar el nombre de clase del autorizador al archivo de configuración del inquilino.
