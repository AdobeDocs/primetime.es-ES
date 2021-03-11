---
title: Uso de listas de actualización de directivas de DRM
description: Uso de listas de actualización de directivas de DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Listas de actualización de directivas de DRM {#drm-policy-update-lists}

Si actualiza las reglas de uso en una directiva DRM después de empaquetar cualquier contenido, el servidor de licencias debe tener la última versión para poder emitir licencias que utilicen una directiva DRM actualizada. Una forma de lograrlo es a través de una lista de actualización de directivas de DRM.

Una lista de actualización de directivas DRM se representa mediante un archivo que incluye una lista de directivas DRM actualizadas o revocadas. Siempre que actualice una directiva de DRM, debe generar una nueva lista de actualización de directivas de DRM e insertar periódicamente la lista en todos los servidores de licencias.

## Uso de listas de actualización de directivas de DRM {#working-with-drm-policy-update-lists}

Para los servidores de licencias que no tienen acceso a una base de datos para almacenar información sobre directivas DRM, es posible que desee utilizar una lista de actualización de directivas DRM para notificar al servidor de licencias cualquier directiva DRM actualizada. Las listas de actualización de directivas de DRM pueden incluir versiones actualizadas de directivas de DRM o una lista de ID de directivas de DRM que se han revocado. Si se incluye una lista de actualización de directivas en `HandlerConfiguration`, el SDK aplicará esta lista cuando emita una licencia.

También puede revocar cualquier política de DRM si los propietarios o distribuidores de contenido desean dejar de emitir licencias bajo una política de DRM en particular. Se puede utilizar una lista de actualización de directivas de DRM para aplicar la revocación de directivas de DRM en el SDK. También puede aplicar listas de actualización de directivas de DRM para proporcionar una lista de directivas de DRM actualizadas al SDK.

>[!NOTE]
>
>Siempre que revoque una directiva de DRM, las licencias que ya se hayan emitido no se revocan automáticamente. Sólo evita que se expidan licencias adicionales en virtud de esa política de gestión de los recursos propios.

## Actualizar listas de actualización de directivas{#update-policy-update-lists}

El uso de listas de actualización de directivas de DRM implica el uso de un objeto `PolicyUpdateListFactory`. Si desea crear una lista de actualización de directivas de DRM, debe cargar una lista de actualización de directivas de DRM existente y, a continuación, comprobar si una directiva de DRM se ha actualizado o revocado utilizando la API de Java.

Para trabajar con las listas de actualización de directivas de DRM:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR que se incluyen al configurar el entorno de desarrollo en un proyecto .
1. Cree una instancia `ServerCredentialFactory` para cargar las credenciales necesarias para firmar.
1. Cree una instancia `PolicyUpdateListFactory` utilizando el `ServerCredential` que ha creado.
1. Especifique el ID de directiva de DRM que desea revocar.
1. Cree un objeto `PolicyRevocationEntry` utilizando el ID de directiva de DRM `String` que acaba de crear y, a continuación, agréguelo a la lista de actualización de directivas de DRM pasando a `PolicyUpdateListFactory.addRevocationEntry()`.
1. Genere la nueva lista de actualización de directivas de DRM llamando a `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   Del mismo modo, puede actualizar las políticas de DRM a la lista utilizando `PolicyUpdateEntry`.
1. Si ya existe una lista de actualización de directivas de DRM, puede serializarla para cargarla llamando a `PolicyUpdateList.getBytes()`.

   Para cargar la lista, llame a `PolicyUpdateListFactory.loadPolicyUpdateList()` y pásela en la lista serializada.
1. Compruebe que la firma es válida y que la lista ha sido firmada por el certificado correcto del servidor de licencias llamando a `PolicyUpdateList.verifySignature()`.
1. Pase el ID de directiva de DRM `String` a `PolicyUpdateList.isRevoked()` para verificar que una entrada se haya revocado.

   Como alternativa, puede pasar la lista a `HandlerConfiguration`, donde se aplicará cada vez que se expidan licencias.
Si desea agregar más entradas a una `PolicyUpdateList` existente, debe cargar una lista de actualización de directivas DRM existente. Por lo tanto, debe crear una nueva instancia de DRM `PolicyUpdateListFactory`. Llame a `PolicyUpdateListFactory.addEntries` para agregar todas las entradas de la lista antigua a la nueva lista. Llame a `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` para agregar cualquier entrada nueva de revocación o actualización a la lista de actualización de directivas de DRM.

Para obtener un código de ejemplo que muestre cómo crear una lista de actualización de directivas de DRM, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` en el directorio *Reference Implementation Line Tools* [!DNL samples] .
