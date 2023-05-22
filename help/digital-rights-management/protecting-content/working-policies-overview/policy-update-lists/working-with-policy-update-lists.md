---
title: Uso de listas de actualización de directivas DRM
description: Uso de listas de actualización de directivas DRM
copied-description: true
exl-id: 140f1fff-2078-427b-ade2-8ec18a14216f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Listas de actualización de directivas DRM {#drm-policy-update-lists}

Si actualiza las reglas de uso en una directiva DRM después de empaquetar cualquier contenido, el servidor de licencias debe tener la versión más reciente para poder emitir licencias que utilicen una directiva DRM actualizada. Una forma de conseguirlo es a través de una lista de actualización de directivas DRM.

Una lista de actualización de directivas DRM se representa mediante un fichero que incluye una lista de directivas DRM actualizadas o revocadas. Siempre que actualice una directiva DRM, deberá generar una nueva lista de actualización de directivas DRM y enviar periódicamente la lista a todos los servidores de licencias.

## Uso de listas de actualización de directivas DRM {#working-with-drm-policy-update-lists}

En el caso de los servidores de licencias que no tienen acceso a una base de datos para almacenar información sobre directivas DRM, puede que desee utilizar una lista de actualización de directivas DRM para notificar al servidor de licencias cualquier directiva DRM actualizada. Las listas de actualización de directivas DRM pueden incluir versiones actualizadas de directivas DRM o una lista de ID de directivas DRM que se han revocado. Si se incluye una lista de actualización de directivas en `HandlerConfiguration`Sin embargo, el SDK exige esta lista cuando emite una licencia.

También puede revocar cualquier política de DRM si los propietarios o distribuidores de contenido desean dejar de emitir licencias en virtud de una política de DRM concreta. Se puede utilizar una lista de actualización de directivas DRM para aplicar la revocación de directivas DRM en el SDK. También puede aplicar listas de actualización de directivas DRM para proporcionar una lista de directivas DRM actualizadas al SDK.

>[!NOTE]
>
>Cada vez que se revoca una directiva DRM, las licencias que ya se hayan emitido no se revocan automáticamente. Solo evita que se emitan licencias adicionales en virtud de esa política de DRM.

## Actualizar listas de actualización de directivas{#update-policy-update-lists}

El trabajo con listas de actualización de directivas DRM implica el uso de un `PolicyUpdateListFactory` objeto. Si desea crear una lista de actualización de directivas DRM, debe cargar una lista de actualización de directivas DRM existente y, a continuación, comprobar si una directiva DRM se ha actualizado o revocado mediante la API de Java.

Para trabajar con listas de actualización de directivas DRM:

1. Configure el entorno de desarrollo e incluya todos los archivos JAR que se incluyen al configurar el entorno de desarrollo en un proyecto
1. Crear un `ServerCredentialFactory` para cargar las credenciales necesarias para la firma.
1. Crear un `PolicyUpdateListFactory` mediante el uso de `ServerCredential` que ha creado.
1. Especifique el ID de la política de DRM que desea revocar.
1. Crear un `PolicyRevocationEntry` mediante el ID de directiva DRM. `String` que acaba de crear y, a continuación, agréguela a la lista de actualización de directivas de DRM pasándola a `PolicyUpdateListFactory.addRevocationEntry()`.
1. Generar la nueva lista de actualización de directivas DRM llamando a `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   Del mismo modo, se pueden actualizar las directivas de DRM a la lista mediante `PolicyUpdateEntry`.
1. Si ya existe una lista de actualización de directivas DRM, puede serializarla para cargarla llamando a `PolicyUpdateList.getBytes()`.

   Para cargar la lista, llame a `PolicyUpdateListFactory.loadPolicyUpdateList()` y pasarlo en la lista serializada.
1. Compruebe que la firma es válida y que el certificado del servidor de licencias correcto ha firmado la lista llamando a `PolicyUpdateList.verifySignature()`.
1. Pasar el ID de la política DRM `String` en `PolicyUpdateList.isRevoked()` para verificar que se ha revocado una entrada.

   También puede pasar la lista a `HandlerConfiguration` donde se aplica cada vez que se emiten licencias.
Si desea agregar más entradas a una existente `PolicyUpdateList`, debe cargar una lista de actualización de directivas DRM existente. Por lo tanto, se debe crear una nueva DRM `PolicyUpdateListFactory` ejemplo. Llamada `PolicyUpdateListFactory.addEntries` para agregar todas las entradas de la lista antigua a la nueva. Llamada `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` para añadir nuevas entradas de revocación o actualización a PolicyUpdateList de DRM.

Para ver un código de ejemplo que muestra cómo crear una lista de actualización de directivas DRM, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` en el *Herramientas de línea de comandos de implementación de referencia* [!DNL samples] directorio.
