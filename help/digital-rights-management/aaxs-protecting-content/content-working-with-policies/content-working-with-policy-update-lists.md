---
seo-title: Uso de Listas de actualización de directivas
title: Uso de Listas de actualización de directivas
uuid: 583abb31-5c80-43f2-bc3d-a2300f61c4ea
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Uso de Listas de actualización de directivas{#working-with-policy-update-lists}

Para los servidores de licencias que no tienen acceso a una base de datos para almacenar información sobre directivas, puede que desee utilizar una lista de actualización de directivas para notificar al servidor de licencias las directivas actualizadas. Las Listas de actualización de directivas pueden contener versiones actualizadas de directivas o una lista de ID de directivas que se han revocado. Si se proporciona una lista de actualización de directiva en `HandlerConfiguration`, el SDK aplicará esta lista al emitir una licencia.

Las políticas también se pueden revocar si los propietarios o distribuidores de contenido desean dejar de emitir licencias según una política determinada. Se puede utilizar una lista de actualización de directiva para aplicar la revocación de directiva en el SDK. Las listas de actualización de directivas también pueden utilizarse para proporcionar una lista de las directivas actualizadas al SDK. Tenga en cuenta que la revocación de una política no anula las licencias que ya se han emitido. Sólo impide que se expidan licencias adicionales en virtud de esa política.

Trabajar con listas de actualización de directivas implica el uso de un objeto `PolicyUpdateListFactory`. Para crear una lista de actualización de directiva, cargue una lista de actualización de directiva existente y compruebe si una directiva se ha actualizado o revocado mediante la API de Java, lleve a cabo los siguientes pasos:

1. Configure el entorno de desarrollo e incluya todos los archivos JAR mencionados en Configuración del entorno de desarrollo dentro del proyecto.
1. Cree una instancia `ServerCredentialFactory` para cargar las credenciales necesarias para la firma.
1. Cree una instancia `PolicyUpdateListFactory` mediante el `ServerCredential` que ha creado.
1. Especifique el ID de directiva que se va a revocar.
1. Cree un objeto `PolicyRevocationEntry` utilizando el identificador de directiva `String` que acaba de crear y agréguelo a la lista de actualización de directiva pasándolo a `PolicyUpdateListFactory.addRevocationEntry()`. Genere la nueva lista de actualización de directivas llamando a `PolicyUpdateListFactory.generatePolicyUpdateList()`. Del mismo modo, se pueden agregar políticas actualizadas a la lista mediante `PolicyUpdateEntry`.
1. Si ya existe una lista de actualización de directiva, puede serializarla para la carga llamando a `PolicyUpdateList.getBytes()`. Para cargar la lista, llame a `PolicyUpdateListFactory.loadPolicyUpdateList()` y pase la lista serializada.
1. Verifique que la firma sea válida y que la lista esté firmada por el certificado de servidor de licencias correcto llamando a `PolicyUpdateList.verifySignature()`.
1. Para comprobar si se ha revocado una entrada, pase el identificador de directiva `String` a `PolicyUpdateList.isRevoked()`. Otra posibilidad es que la lista se pase a `HandlerConfiguration` y se aplique cuando se expidan licencias.

Para agregar entradas adicionales a una `PolicyUpdateList` existente, cargue una lista de actualización de directiva existente. Cree una nueva instancia `PolicyUpdateListFactory`. Llame a P `olicyUpdateListFactory.addEntries` para agregar todas las entradas de la antigua lista a la nueva lista. Llame a `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` para agregar cualquier nueva entrada de revocación o actualización a PolicyUpdateList.

Para obtener el código de muestra que muestra cómo crear una lista de actualización de directiva, cargar una lista de actualización de directiva existente y comprobar si se ha revocado una directiva, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` en el directorio &quot;samples&quot; de las Herramientas de la línea de comandos de implementación de referencia.
