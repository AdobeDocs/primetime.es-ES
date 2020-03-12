---
seo-title: Revocando credenciales de equipo
title: Revocando credenciales de equipo
uuid: 16119ff9-8147-4fe0-9744-a705d94a9400
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Revocando credenciales de equipo{#revoking-machine-credentials}

Adobe mantiene una CRL para revocar las credenciales del equipo que se sabe que están en peligro. El SDK aplica automáticamente esta CRL. Si hay equipos adicionales a los que no desea que el servidor de licencias emita licencias, puede crear una lista de revocación de máquinas y agregar el nombre del emisor y el número de serie de los tokens de máquina que desea excluir (utilice `MachineToken.getMachineTokenId()` para recuperar el nombre del emisor y el número de serie del certificado de máquina).

La revocación de las credenciales del equipo implica el uso de un `RevocationListFactory` objeto. Para crear una lista de revocación, cargue una lista de revocación existente y compruebe si se ha revocado un autentificador de equipo mediante la API de Java, lleve a cabo los siguientes pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en [Configuración del entorno](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) de desarrollo dentro del proyecto.
1. Cree una `ServerCredentialFactory` instancia para cargar las credenciales necesarias para firmar. Las credenciales del servidor de licencias se utilizan para firmar la lista de revocación.
1. Cree una `RevocationListFactory` instancia.
1. Especifique el emisor y el número de serie del token de equipo que se va a revocar mediante un `IssuerAndSerialNumber` objeto. Todas las solicitudes de Adobe Access contienen un token de equipo.
1. Cree un `RevocationList` objeto con el `IssuerAndSerialNumber` objeto que acaba de crear y agréguelo a la lista de revocación pasando a `RevocationListFactory.addRevocationEntry()`. Genere la nueva lista de revocación llamando a `RevocationListFactory.generateRevocationList()`.
1. Para guardar la lista de revocación, puede serializarla llamando a `RevocationList.getBytes()`. Para cargar la lista, llame `RevocationListFactory.loadRevocationList()` y pase la lista serializada.
1. Compruebe que la firma es válida y que el servidor de licencias correcto ha firmado la lista llamando `RevocationList.verifySignature()`.
1. Para comprobar si se ha revocado una entrada, pase el `IssuerAndSerialNumber` objeto a `RevocationList.isRevoked()`. La lista de revocación también se puede pasar `HandlerConfiguration` para que el SDK aplique la lista de revocación para todas las solicitudes de autenticación y licencia.

Para agregar entradas adicionales a una existente `RevocationList`, cargue una lista de revocación existente. Cree una nueva `RevocationListFactory` instancia y asegúrese de aumentar el número CRL. Llame `RevocationListFactioryEntries.addRevocationEntries` para agregar todas las entradas de la lista antigua a la nueva lista. Llame `RevocationListFactory.addRevocationEntry` para agregar cualquier entrada de revocación nueva a RevocationList.

Para obtener el código de muestra que muestra cómo crear una lista de revocación, cargar una lista de revocación existente y comprobar si se ha revocado un token de equipo, consulte `com.adobe.flashaccess.samples.revocation.CreateRevocationList` en el directorio &quot;samples&quot; de Herramientas de la línea de comandos de implementación de referencia.
