---
description: Puede invocar la lógica de autorización personalizada durante la adquisición de licencia para decidir si se debe emitir una licencia al cliente solicitante.
title: Extensiones de autorización personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Extensiones de autorización personalizadas{#custom-authorization-extensions}

Puede invocar la lógica de autorización personalizada durante la adquisición de licencia para decidir si se debe emitir una licencia al cliente solicitante.

Si desea implementar su propia extensión de autorización de cliente, primero debe echar un vistazo al código de muestra [!DNL SampleAuthorizer.java] que se encuentra en el directorio samples. La versión compilada de este ejemplo se encuentra en [!DNL flashaccess-license-server-ext-sample.jar].

Si desea crear su propia extensión, debe implementar la interfaz `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` y asegurarse de que [!DNL flashaccess-license-server-exts.jar] y [!DNL commons-logging.jar] estén en la ruta de compilación ( [!DNL adobe-flashaccess-sdk.jar] también debe estar en la ruta de compilación si utiliza ciertos campos en `IMessageFacade`).

Si desea implementar la extensión, debe copiar los archivos jar o de clase en *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

Si desea actualizar los archivos jar o de clase , debe reiniciar el servidor antes de poder utilizar la versión actualizada. También debe agregar el nombre de clase del autorizador al archivo de configuración del inquilino.
