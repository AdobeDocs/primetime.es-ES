---
title: Uso de listas de actualización de directivas
description: Uso de listas de actualización de directivas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Uso de listas de actualización de directivas{#working-with-policy-update-lists}

En el caso de los servidores de licencias que no tienen acceso a una base de datos para almacenar información sobre directivas, puede utilizar una lista de actualización de directivas para notificar al servidor de licencias las directivas actualizadas. Las Listas de actualización de directivas pueden contener versiones actualizadas de directivas o una lista de ID de directivas que se han revocado. Si se proporciona una lista de actualización de directivas en `HandlerConfiguration`, el SDK aplicará esta lista al emitir una licencia.

Las directivas también se pueden revocar si los propietarios o distribuidores de contenido desean dejar de emitir licencias según una directiva en particular. Se puede utilizar una lista de actualización de directivas para aplicar la revocación de directivas en el SDK. Las listas de actualización de directivas también se pueden utilizar para proporcionar una lista de directivas actualizadas al SDK. Tenga en cuenta que revocar una directiva no anula las licencias que ya se han emitido. Sólo evita que se expidan licencias adicionales en virtud de esa política.

El trabajo con listas de actualización de directivas implica el uso de un `PolicyUpdateListFactory` objeto. Para crear una lista de actualización de directivas, cargar una lista de actualización de directivas existente y comprobar si una directiva se ha actualizado o revocado mediante la API de Java, realice los siguientes pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en Configuración del entorno de desarrollo dentro del proyecto.
1. Crear un `ServerCredentialFactory` para cargar las credenciales necesarias para la firma.
1. Crear un `PolicyUpdateListFactory` instancia con el `ServerCredential` que ha creado.
1. Especifique el ID de política que desea revocar.
1. Crear un `PolicyRevocationEntry` objeto que utiliza el ID de directiva `String` acaba de crear y agréguelo a la lista de actualización de directivas pasándolo a `PolicyUpdateListFactory.addRevocationEntry()`. Generar la nueva lista de actualización de directivas llamando a `PolicyUpdateListFactory.generatePolicyUpdateList()`. Del mismo modo, las directivas actualizadas se pueden añadir a la lista mediante `PolicyUpdateEntry`.
1. Si ya existe una lista de actualización de directivas, puede serializarla para cargarla llamando a `PolicyUpdateList.getBytes()`. Para cargar la lista, llame a `PolicyUpdateListFactory.loadPolicyUpdateList()` y pasar en la lista serializada.
1. Compruebe que la firma es válida y que la lista está firmada por el certificado de servidor de licencias correcto llamando a `PolicyUpdateList.verifySignature()`.
1. Para comprobar si una entrada se ha revocado, pase el ID de política `String` en `PolicyUpdateList.isRevoked()`. Alternativamente, la lista se puede pasar a `HandlerConfiguration` y se aplicará cuando se emitan licencias.

Para agregar entradas adicionales a una existente `PolicyUpdateList`, cargue una lista de actualización de directivas existente. Crear un nuevo `PolicyUpdateListFactory` ejemplo. Llamar a P `olicyUpdateListFactory.addEntries` para agregar todas las entradas de la lista antigua a la nueva. Llamada `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` para agregar entradas de revocación o actualización nuevas a PolicyUpdateList.

Para ver un código de ejemplo que muestra cómo crear una lista de actualización de directivas, cargar una lista de actualización de directivas existente y comprobar si una directiva se ha revocado, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` en el directorio &quot;samples&quot; de Herramientas de línea de comandos de implementación de referencia.
