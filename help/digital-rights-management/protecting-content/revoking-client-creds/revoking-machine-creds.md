---
title: Revocación de credenciales de máquina
description: Revocación de credenciales de máquina
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Revocando las credenciales del equipo {#revoking-machine-credentials}

Adobe mantiene una CRL para revocar las credenciales de la máquina que se sabe que están en peligro. El SDK aplica automáticamente esta CRL. Si hay equipos adicionales a los que no desea que su servidor de licencias emita licencias, puede crear una lista de revocación de máquinas y agregar el nombre del emisor y el número de serie de los tokens de máquina que desea excluir (utilice `MachineToken.getMachineTokenId()` para recuperar el nombre del emisor y el número de serie del certificado de máquina).

La revocación de las credenciales del equipo implica el uso de un objeto `RevocationListFactory`. Para crear una lista de revocación, cargar una lista de revocación existente y comprobar si se ha revocado un token de equipo mediante la API de Java, realice los pasos siguientes:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en [Configuración del entorno de desarrollo](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) dentro del proyecto.
1. Cree una instancia `ServerCredentialFactory` para cargar las credenciales necesarias para firmar. La credencial del servidor de licencias se utiliza para firmar la lista de revocación.
1. Cree una instancia `RevocationListFactory`.
1. Especifique el emisor y el número de serie del token del equipo que se va a revocar utilizando un objeto `IssuerAndSerialNumber`. Todas las solicitudes de Adobe Primetime DRM contienen un token de equipo.
1. Cree un objeto `RevocationList` utilizando el objeto `IssuerAndSerialNumber` que acaba de crear y agréguelo a la lista de revocación pasándolo a `RevocationListFactory.addRevocationEntry()`. Genere la nueva lista de revocación llamando a `RevocationListFactory.generateRevocationList()`.

1. Para guardar la lista de revocación, puede serializarla llamando a `RevocationList.getBytes()`. Para cargar la lista, llame a `RevocationListFactory.loadRevocationList()` y pase a la lista serializada.

1. Compruebe que la firma es válida y que la lista ha sido firmada por el servidor de licencias correcto llamando a `RevocationList.verifySignature()`.
1. Para comprobar si una entrada se ha revocado, pase el objeto `IssuerAndSerialNumber` a `RevocationList.isRevoked()`. La lista de revocación también se puede pasar a `HandlerConfiguration` para que el SDK aplique la lista de revocación para todas las solicitudes de autenticación y licencia.

Para agregar entradas adicionales a una `RevocationList` existente, cargue una lista de revocación existente. Cree una nueva instancia `RevocationListFactory` y asegúrese de aumentar el número CRL. Llame a `RevocationListFactioryEntries.addRevocationEntries` para agregar todas las entradas de la lista antigua a la nueva lista. Llame a `RevocationListFactory.addRevocationEntry` para agregar cualquier entrada de revocación nueva a RevocationList.

Para obtener un código de ejemplo que muestre cómo crear una lista de revocación, cargar una lista de revocación existente y comprobar si se ha revocado un token de equipo, consulte `com.adobe.flashaccess.samples.revocation.CreateRevocationList` en el directorio Herramientas [!DNL samples] de la línea de comandos de implementación de referencia.
