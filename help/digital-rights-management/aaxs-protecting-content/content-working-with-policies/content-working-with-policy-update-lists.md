---
title: Uso de listas de actualización de directivas
description: Uso de listas de actualización de directivas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Uso de listas de actualización de directivas{#working-with-policy-update-lists}

Para los servidores de licencias que no tienen acceso a una base de datos para almacenar información sobre directivas, puede que desee utilizar una lista de actualización de directivas para notificar al servidor de licencias de directivas actualizadas. Las listas de actualización de directivas pueden contener versiones actualizadas de directivas o una lista de ID de directivas que se han revocado. Si se proporciona una lista de actualización de directivas en `HandlerConfiguration`, el SDK aplicará esta lista al emitir una licencia.

Las políticas también pueden ser revocadas si los propietarios o distribuidores de contenido quieren dejar de emitir licencias bajo una política en particular. Se puede utilizar una lista de actualización de directivas para aplicar la revocación de directivas en el SDK. Las listas de actualización de directivas también pueden utilizarse para proporcionar una lista de directivas actualizadas al SDK. Tenga en cuenta que la revocación de una directiva no revoca las licencias que ya se han emitido. Sólo impide que se expidan licencias adicionales en virtud de esa política.

El uso de listas de actualización de directivas implica el uso de un objeto `PolicyUpdateListFactory`. Para crear una lista de actualización de directivas, cargue una lista de actualización de directivas existente y compruebe si una directiva se ha actualizado o revocado usando la API de Java, siga los siguientes pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en Configuración del entorno de desarrollo dentro del proyecto.
1. Cree una instancia `ServerCredentialFactory` para cargar las credenciales necesarias para firmar.
1. Cree una instancia `PolicyUpdateListFactory` utilizando el `ServerCredential` que ha creado.
1. Especifique el ID de la directiva que se va a revocar.
1. Cree un objeto `PolicyRevocationEntry` utilizando el identificador de directiva `String` que acaba de crear y agréguelo a la lista de actualización de directivas pasándolo a `PolicyUpdateListFactory.addRevocationEntry()`. Genere la nueva lista de actualización de directivas llamando a `PolicyUpdateListFactory.generatePolicyUpdateList()`. Del mismo modo, se pueden agregar directivas actualizadas a la lista utilizando `PolicyUpdateEntry`.
1. Si ya existe una lista de actualización de directivas, puede serializarla para cargarla llamando a `PolicyUpdateList.getBytes()`. Para cargar la lista, llame a `PolicyUpdateListFactory.loadPolicyUpdateList()` y pase a la lista serializada.
1. Compruebe que la firma es válida y que la lista está firmada por el certificado correcto del servidor de licencias llamando a `PolicyUpdateList.verifySignature()`.
1. Para comprobar si una entrada se ha revocado, pase el ID de directiva `String` a `PolicyUpdateList.isRevoked()`. Alternativamente, la lista se puede pasar a `HandlerConfiguration` y se aplicará cuando se expidan licencias.

Para agregar entradas adicionales a una `PolicyUpdateList` existente, cargue una lista de actualización de directivas existente. Cree una nueva instancia `PolicyUpdateListFactory`. Llame a P `olicyUpdateListFactory.addEntries` para añadir todas las entradas de la lista antigua a la nueva lista. Llame a `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` para agregar cualquier entrada nueva de revocación o actualización a PolicyUpdateList.

Para obtener un código de ejemplo que muestre cómo crear una lista de actualización de directivas, cargar una lista de actualización de directivas existente y comprobar si se ha revocado una directiva, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` en el directorio &quot;muestras&quot; de las herramientas de la línea de comandos de implementación de referencia.
