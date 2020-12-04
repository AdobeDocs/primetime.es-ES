---
seo-title: Uso de Listas de actualización de directivas DRM
title: Uso de Listas de actualización de directivas DRM
uuid: 41f89671-81c6-4d3d-ac31-9c2a1980517a
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Listas de actualización de directivas de DRM {#drm-policy-update-lists}

Si actualiza las reglas de uso en una directiva DRM después de empaquetar cualquier contenido, el servidor de licencias debe tener la última versión para poder emitir licencias que utilicen una directiva DRM actualizada. Una manera de lograrlo es a través de una lista de actualización de políticas de DRM.

Una lista de actualización de directiva DRM se representa mediante un archivo que incluye una lista de directivas DRM actualizadas o revocadas. Siempre que actualice una directiva DRM, deberá generar una nueva Lista de actualización de directiva DRM e insertar periódicamente la lista en todos los servidores de licencias.

## Uso de Listas de actualización de directivas de DRM {#working-with-drm-policy-update-lists}

Para los servidores de licencias que no tienen acceso a una base de datos para almacenar información sobre las directivas DRM, es posible que desee utilizar una lista de actualización de directivas DRM para notificar al servidor de licencias cualquier directiva DRM actualizada. Las Listas de actualización de directivas de DRM pueden incluir versiones actualizadas de directivas de DRM o una lista de ID de directivas de DRM que se hayan revocado. Si se incluye una lista de actualización de directiva en `HandlerConfiguration`, el SDK aplica esta lista cuando emite una licencia.

También puede revocar cualquier directiva de DRM si los propietarios o distribuidores de contenido desean dejar de emitir licencias en una política de DRM en particular. Se puede utilizar una lista de actualización de directiva DRM para aplicar la revocación de directiva DRM en el SDK. También puede aplicar listas de actualización de directivas DRM para proporcionar una lista de las directivas DRM actualizadas al SDK.

>[!NOTE]
>
>Cuando se revoca una directiva DRM, las licencias que ya se hayan emitido no se revocan automáticamente. Sólo evita que se emitan licencias adicionales en virtud de esa política de gestión de recursos digitales.

## Actualizar Listas de actualización de directiva{#update-policy-update-lists}

Trabajar con listas de actualización de directivas DRM implica el uso de un objeto `PolicyUpdateListFactory`. Si desea crear una lista de actualización de directiva DRM, debe cargar una lista de actualización de directiva DRM existente y, a continuación, comprobar si una directiva DRM se ha actualizado o revocado mediante la API de Java.

Para trabajar con Listas de actualización de directivas de DRM:

1. Configure el entorno de desarrollo e incluya todos los archivos JAR que se incluyen al configurar el entorno de desarrollo en un proyecto.
1. Cree una instancia `ServerCredentialFactory` para cargar las credenciales necesarias para la firma.
1. Cree una instancia `PolicyUpdateListFactory` mediante el uso de `ServerCredential` que ha creado.
1. Especifique el ID de directiva de DRM que desea revocar.
1. Cree un objeto `PolicyRevocationEntry` utilizando el ID de directiva de DRM `String` que acaba de crear y, a continuación, agréguelo a la lista de actualización de directiva de DRM pasando a `PolicyUpdateListFactory.addRevocationEntry()`.
1. Genere la nueva lista de actualización de directivas DRM llamando a `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   Del mismo modo, puede actualizar las directivas de DRM a la lista mediante `PolicyUpdateEntry`.
1. Si ya existe una lista de actualización de directiva DRM, puede serializarla para la carga llamando a `PolicyUpdateList.getBytes()`.

   Para cargar la lista, llame a `PolicyUpdateListFactory.loadPolicyUpdateList()` y pásela en la lista serializada.
1. Compruebe que la firma es válida y que la lista ha sido firmada por el certificado de servidor de licencias correcto llamando a `PolicyUpdateList.verifySignature()`.
1. Pase el ID de directiva de DRM `String` a `PolicyUpdateList.isRevoked()` para verificar que se ha revocado una entrada.

   Como alternativa, puede pasar la lista a `HandlerConfiguration` donde se aplica cada vez que se emiten licencias.
Si desea agregar más entradas a una `PolicyUpdateList` existente, debe cargar una lista de actualización de directiva DRM existente. Por lo tanto, debe crear una nueva instancia de DRM `PolicyUpdateListFactory`. Llame a `PolicyUpdateListFactory.addEntries` para agregar todas las entradas de la lista antigua a la nueva lista. Llame a `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` para agregar cualquier entrada de revocación o actualización nueva a DRM PolicyUpdateList.

Para obtener el código de muestra que muestra cómo crear una lista de actualización de directiva DRM, consulte `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` en el directorio *Reference Implementation Command Line Tools* [!DNL samples].
