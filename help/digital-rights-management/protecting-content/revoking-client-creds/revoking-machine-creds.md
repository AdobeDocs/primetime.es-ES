---
title: Revocar credenciales de equipo
description: Revocar credenciales de equipo
copied-description: true
exl-id: 4f49a94c-1bd9-4a7a-ac92-4da0b7fe4ae4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# Revocar credenciales de equipo {#revoking-machine-credentials}

La Adobe mantiene una CRL para revocar las credenciales de la máquina que se sabe que están en peligro. El SDK aplica automáticamente esta CRL. Si hay máquinas adicionales en las que no desea que el servidor de licencias emita licencias, puede crear una lista de revocación de equipos y agregar el nombre del emisor y el número de serie de los tokens de equipo que desea excluir (use `MachineToken.getMachineTokenId()` para recuperar el nombre del emisor y el número de serie del certificado de máquina).

Revocar credenciales de equipo implica el uso de un `RevocationListFactory` objeto. Para crear una lista de revocación, cargar una lista de revocación existente y comprobar si un token de equipo se ha revocado mediante la API de Java, realice los siguientes pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en [Configuración del entorno de desarrollo](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) dentro del proyecto.
1. Crear un `ServerCredentialFactory` para cargar las credenciales necesarias para la firma. La credencial del servidor de licencias se usa para firmar la lista de revocación.
1. Crear un `RevocationListFactory` ejemplo.
1. Especifique el emisor y el número de serie del token de equipo que se va a revocar mediante una `IssuerAndSerialNumber` objeto. Todas las solicitudes de DRM de Adobe Primetime contienen un token de equipo.
1. Crear un `RevocationList` objeto que utiliza el `IssuerAndSerialNumber` objeto que acaba de crear y agréguelo a la lista de revocación pasándolo a `RevocationListFactory.addRevocationEntry()`. Generar la nueva lista de revocación llamando a `RevocationListFactory.generateRevocationList()`.

1. Para guardar la lista de revocación, puede serializarla llamando a `RevocationList.getBytes()`. Para cargar la lista, llame a `RevocationListFactory.loadRevocationList()` y pasar en la lista serializada.

1. Compruebe que la firma es válida y que el servidor de licencias correcto ha firmado la lista llamando a `RevocationList.verifySignature()`.
1. Para comprobar si una entrada se ha revocado, pase el `IssuerAndSerialNumber` objeto en `RevocationList.isRevoked()`. La lista de revocación también se puede pasar a `HandlerConfiguration` para que el SDK aplique la lista de revocación para todas las solicitudes de autenticación y licencia.

Para agregar entradas adicionales a una existente `RevocationList`, cargue una lista de revocación existente. Crear un nuevo `RevocationListFactory` y asegúrese de incrementar el número de CRL. Llamada `RevocationListFactioryEntries.addRevocationEntries` para agregar todas las entradas de la lista antigua a la nueva. Llamada `RevocationListFactory.addRevocationEntry` para agregar nuevas entradas de revocación a RevocationList.

Para ver un código de ejemplo que muestra cómo crear una lista de revocación, cargar una lista de revocación existente y comprobar si se ha revocado un token de equipo, consulte `com.adobe.flashaccess.samples.revocation.CreateRevocationList` en las herramientas de línea de comandos de implementación de referencia [!DNL samples] directorio.
