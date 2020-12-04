---
seo-title: Revocando credenciales de equipo
title: Revocando credenciales de equipo
uuid: 3647c843-5f1a-457e-949d-10a6278b1c29
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Revocando credenciales de máquina {#revoking-machine-credentials}

Adobe mantiene una CRL para revocar las credenciales de máquina que se sabe que están en peligro. El SDK aplica automáticamente esta CRL. Si hay equipos adicionales a los que no desea que su servidor de licencias emita licencias, puede crear una lista de revocación de máquina y agregar el nombre del emisor y el número de serie de los tokens de máquina que desea excluir (utilice `MachineToken.getMachineTokenId()` para recuperar el nombre del emisor y el número de serie del certificado de máquina).

La revocación de las credenciales del equipo implica el uso de un objeto `RevocationListFactory`. Para crear una lista de revocación, cargue una lista de revocación existente y compruebe si se ha revocado un autentificador de equipo mediante la API de Java, lleve a cabo los siguientes pasos:

1. Configure el entorno de desarrollo e incluya todos los archivos JAR mencionados en [Configuración del entorno de desarrollo](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) dentro del proyecto.
1. Cree una instancia `ServerCredentialFactory` para cargar las credenciales necesarias para la firma. Las credenciales del servidor de licencias se utilizan para firmar la lista de revocación.
1. Cree una instancia `RevocationListFactory`.
1. Especifique el emisor y el número de serie del token de equipo que se va a revocar mediante un objeto `IssuerAndSerialNumber`. Todas las solicitudes DRM de Adobe Primetime contienen un token de equipo.
1. Cree un objeto `RevocationList` utilizando el objeto `IssuerAndSerialNumber` que acaba de crear y agréguelo a la lista de revocación pasándolo a `RevocationListFactory.addRevocationEntry()`. Genere la nueva lista de revocación llamando a `RevocationListFactory.generateRevocationList()`.

1. Para guardar la lista de revocación, puede serializarla llamando a `RevocationList.getBytes()`. Para cargar la lista, llame a `RevocationListFactory.loadRevocationList()` y pase la lista serializada.

1. Compruebe que la firma es válida y que el servidor de licencias correcto ha firmado la lista llamando a `RevocationList.verifySignature()`.
1. Para comprobar si se ha revocado una entrada, pase el objeto `IssuerAndSerialNumber` a `RevocationList.isRevoked()`. La lista de revocación también se puede pasar a `HandlerConfiguration` para que el SDK aplique la lista de revocación para todas las solicitudes de autenticación y licencia.

Para agregar entradas adicionales a una `RevocationList` existente, cargue una lista de revocación existente. Cree una nueva instancia `RevocationListFactory` y asegúrese de incrementar el número CRL. Llame a `RevocationListFactioryEntries.addRevocationEntries` para agregar todas las entradas de la lista antigua a la nueva lista. Llame a `RevocationListFactory.addRevocationEntry` para agregar cualquier entrada de revocación nueva a RevocationList.

Para obtener el código de muestra que muestra cómo crear una lista de revocación, cargar una lista de revocación existente y comprobar si se ha revocado un token de equipo, consulte `com.adobe.flashaccess.samples.revocation.CreateRevocationList` en el directorio Reference Implementation Command Line Tools [!DNL samples].
