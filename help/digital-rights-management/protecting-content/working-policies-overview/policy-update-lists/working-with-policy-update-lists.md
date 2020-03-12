---
seo-title: Uso de listas de actualización de directivas DRM
title: Uso de listas de actualización de directivas DRM
uuid: 41f89671-81c6-4d3d-ac31-9c2a1980517a
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Listas de actualización de directivas DRM {#drm-policy-update-lists}

Si actualiza las reglas de uso en una directiva DRM después de empaquetar cualquier contenido, el servidor de licencias debe tener la última versión para poder emitir licencias que utilicen una directiva DRM actualizada. Una manera de lograrlo es a través de una lista de actualización de directivas DRM.

Una lista de actualización de directiva DRM se representa mediante un archivo que incluye una lista de directivas DRM actualizadas o revocadas. Siempre que actualice una directiva DRM, deberá generar una nueva lista de actualización de la directiva DRM e insertar periódicamente la lista en todos los servidores de licencias.

## Uso de listas de actualización de directivas DRM {#working-with-drm-policy-update-lists}

Para los servidores de licencias que no tienen acceso a una base de datos para almacenar información sobre las directivas DRM, es posible que desee utilizar una lista de actualización de directivas DRM para notificar al servidor de licencias cualquier directiva DRM actualizada. Las listas de actualización de directivas de DRM pueden incluir versiones actualizadas de directivas de DRM o una lista de ID de directivas de DRM que se han revocado. Si se incluye una lista de actualizaciones de directivas en `HandlerConfiguration`, el SDK aplica esta lista cuando emite una licencia.

También puede revocar cualquier directiva de DRM si los propietarios o distribuidores de contenido desean dejar de emitir licencias en una política de DRM en particular. Se puede usar una lista de actualización de directiva DRM para aplicar la revocación de directiva DRM en el SDK. También puede aplicar listas de actualización de directivas DRM para proporcionar una lista de directivas DRM actualizadas al SDK.

>[!NOTE]
>
>Cuando se revoca una directiva DRM, las licencias que ya se hayan emitido no se revocan automáticamente. Sólo evita que se emitan licencias adicionales en virtud de esa política de gestión de recursos digitales.

## Actualizar listas de actualización de directivas{#update-policy-update-lists}

Trabajar con listas de actualización de directivas DRM implica el uso de un `PolicyUpdateListFactory` objeto. Si desea crear una lista de actualización de directiva DRM, debe cargar una lista de actualización de directiva DRM existente y, a continuación, comprobar si una directiva DRM se ha actualizado o revocado mediante la API de Java.

Para trabajar con las listas de actualizaciones de directivas de DRM:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR que se incluyen al configurar el entorno de desarrollo en un proyecto.
1. Cree una `ServerCredentialFactory` instancia para cargar las credenciales necesarias para la firma.
1. Cree una `PolicyUpdateListFactory` instancia utilizando el `ServerCredential` que ha creado.
1. Especifique el ID de directiva de DRM que desea revocar.
1. Cree un `PolicyRevocationEntry` objeto con el ID de directiva de DRM `String` que acaba de crear y, a continuación, agréguelo a la lista de actualización de directivas de DRM pasando a `PolicyUpdateListFactory.addRevocationEntry()`.
1. Genere la nueva lista de actualización de directivas de DRM llamando `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   Del mismo modo, puede actualizar las directivas de DRM a la lista mediante `PolicyUpdateEntry`.
1. Si ya existe una lista de actualización de directiva DRM, puede serializarla para cargarla llamando a `PolicyUpdateList.getBytes()`.

   Para cargar la lista, realice una llamada `PolicyUpdateListFactory.loadPolicyUpdateList()` y pásela en la lista serializada.
1. Compruebe que la firma es válida y que la lista ha sido firmada por el certificado de servidor de licencias correcto llamando a `PolicyUpdateList.verifySignature()`.
1. Pase el ID de directiva DRM `String` a `PolicyUpdateList.isRevoked()` para comprobar que se ha revocado una entrada.

   También puede pasar la lista a `HandlerConfiguration` donde se aplica cada vez que se emitan licencias.
Si desea agregar más entradas a una existente `PolicyUpdateList`, debe cargar una lista de actualizaciones de directivas DRM existente. Por lo tanto, debe crear una nueva `PolicyUpdateListFactory` instancia de DRM. Llame `PolicyUpdateListFactory.addEntries` para agregar todas las entradas de la lista antigua a la nueva lista. Llame `PolicyUpdateListFactory.addRevocationEntry` o `addUpdatedEntry` para agregar cualquier entrada de revocación o actualización nueva a DRM PolicyUpdateList.

Para obtener un código de muestra que muestre cómo crear una lista de actualización de directivas DRM, consulte `com.adobe.flashaccess.samples.policyupdatelist` en el directorio Herramientas `.CreatePolicyUpdateList` de línea de comandos de implementación de *referencia* [!DNL samples] .
