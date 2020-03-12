---
seo-title: Uso de listas de actualización de directivas
title: Uso de listas de actualización de directivas
uuid: 583abb31-5c80-43f2-bc3d-a2300f61c4ea
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uso de listas de actualización de directivas{#working-with-policy-update-lists}

Para los servidores de licencias que no tienen acceso a una base de datos para almacenar información sobre directivas, puede que desee utilizar una lista de actualizaciones de directivas para notificar al servidor de licencias las directivas actualizadas. Las listas de actualización de directivas pueden contener versiones actualizadas de directivas o una lista de ID de directivas que se han revocado. Si se proporciona una lista de actualizaciones de directivas en `HandlerConfiguration`, el SDK aplicará esta lista al emitir una licencia.

Las políticas también se pueden revocar si los propietarios o distribuidores de contenido desean dejar de emitir licencias según una política determinada. Se puede usar una lista de actualización de directiva para aplicar la revocación de directiva en el SDK. Las listas de actualización de directivas también pueden utilizarse para proporcionar una lista de directivas actualizadas al SDK. Tenga en cuenta que la revocación de una política no anula las licencias que ya se han emitido. Sólo impide que se expidan licencias adicionales en virtud de esa política.

Trabajar con listas de actualización de directivas implica el uso de un `PolicyUpdateListFactory` objeto. Para crear una lista de actualizaciones de directivas, cargue una lista de actualizaciones de directivas existente y compruebe si una directiva se ha actualizado o revocado mediante la API de Java. Siga estos pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en Configuración del entorno de desarrollo dentro del proyecto.
1. Cree una `ServerCredentialFactory` instancia para cargar las credenciales necesarias para firmar.
1. Cree una `PolicyUpdateListFactory` instancia con el `ServerCredential` nombre creado.
1. Especifique el ID de directiva que se va a revocar.
1. Cree un `PolicyRevocationEntry` objeto con el ID de política `String` que acaba de crear y agréguelo a la lista de actualizaciones de políticas pasando a `PolicyUpdateListFactory.addRevocationEntry()`. Genere la nueva lista de actualizaciones de directivas llamando a `PolicyUpdateListFactory.generatePolicyUpdateList()`. Del mismo modo, se pueden agregar directivas actualizadas a la lista mediante `PolicyUpdateEntry`.
1. Si ya existe una lista de actualizaciones de directivas, puede serializarla para cargarla llamando a `PolicyUpdateList.getBytes()`. Para cargar la lista, llame `PolicyUpdateListFactory.loadPolicyUpdateList()` y pase la lista serializada.
1. Verifique que la firma sea válida y que la lista esté firmada por el certificado de servidor de licencias correcto llamando `PolicyUpdateList.verifySignature()`.
1. Para comprobar si se ha revocado una entrada, pase el ID de directiva `String` a `PolicyUpdateList.isRevoked()`. De forma alternativa, la lista se puede pasar a `HandlerConfiguration` y se aplicará cuando se emitan licencias.

Para agregar entradas adicionales a una existente `PolicyUpdateList`, cargue una lista de actualizaciones de directivas existente. Cree una nueva `PolicyUpdateListFactory` instancia. Llame `olicyUpdateListFactory.addEntries` a P para agregar todas las entradas de la lista antigua a la nueva lista. Llame `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` para agregar cualquier nueva entrada de revocación o actualización a PolicyUpdateList.

Para obtener un código de muestra que muestre cómo crear una lista de actualización de directivas, cargar una lista de actualización de directivas existente y comprobar si se ha revocado una directiva, consulte `com.adobe.flashaccess.samples.policyupdatelist` en el directorio &quot;samples&quot; de Herramientas de la línea de comandos de implementación de referencia `.CreatePolicyUpdateList` .
