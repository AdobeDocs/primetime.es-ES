---
title: Extensiones de autorización personalizadas
description: Durante la adquisición de la licencia se puede invocar la lógica de autorización personalizada para decidir si se debe emitir una licencia al cliente solicitante.
exl-id: bf7870f5-11bf-4392-a422-506b47d684f9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Extensiones de autorización personalizadas {#custom-authorization-extensions}

Durante la adquisición de la licencia se puede invocar la lógica de autorización personalizada para decidir si se debe emitir una licencia al cliente solicitante.

Para implementar su propia extensión de autorización de cliente, consulte primero la [!DNL SampleAuthorizer.java] código de ejemplo ubicado en el directorio samples (la versión compilada de este ejemplo se encuentra en flashaccess-license-server-ext-sample.jar).

Para crear su propia extensión, implemente la `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` interfaz y asegúrese de que `flashaccess-license-server-exts.jar` y `commons-logging.jar` están en la ruta de compilación `adobe-flashaccess-sdk.jar` también debe estar en la ruta de compilación si utiliza ciertos campos en `IMessageFacade`). Para implementar la extensión, copie los archivos jar o de clase en *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Si necesita actualizar los archivos jar o de clase, debe reiniciar el servidor antes de utilizar la versión actualizada. También debe agregar el nombre de clase del autorizador al archivo de configuración del inquilino.
