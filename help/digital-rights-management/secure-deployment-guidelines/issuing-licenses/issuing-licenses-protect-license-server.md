---
description: Debe asegurarse de que está emitiendo licencias de forma segura. Tenga en cuenta estas prácticas recomendadas para proteger el servidor de licencias
title: Protección del servidor de licencias
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# Protección del servidor de licencias {#protecting-the-license-server}

Debe asegurarse de que está emitiendo licencias de forma segura. Tenga en cuenta estas prácticas recomendadas para proteger el servidor de licencias:

## Consumo de CRL generadas localmente {#consuming-locally-generated-crls}

Para consumir listas de revocación de certificados (CRL) generadas localmente y listas de actualización de directivas, utilice las API de DRM de Adobe Primetime para comprobar la firma.

Las siguientes API comprueban que las listas no se han manipulado y que el servidor de licencias correcto ha firmado las listas:

* Llamada [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) para comprobar la firma antes de proporcionar el [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a cualquier API.

  Para obtener más información, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Llamada [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) para comprobar la firma antes de proporcionar el `PolicyUpdateList` a cualquier API.

  Para obtener más información, consulte [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Consumo de CRL publicadas por Adobe{#consuming-crls-published-by-adobe}

El SDK descarga periódicamente CRL publicadas por Adobe. Debe asegurarse de que no se bloquee el acceso a estos archivos o de que no se impida la aplicación de estas CRL.

El SDK tiene una opción de configuración para ignorar los errores al recuperar CRL de Adobe, y solo puede aplicar esta opción en entornos de desarrollo. En entornos de producción, el servidor de licencias debe recuperar las CRL de la Adobe. Si el servidor de licencias no puede obtener una CRL válida, se ha producido un error.

## Generación de listas CRL para complementar las publicadas por Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Puede utilizar Adobe Primetime DRM para crear listas CRL que complementen la lista CRL de la máquina publicada por Adobe.

El SDK de DRM de Primetime comprueba y aplica las CRL de Adobe. Sin embargo, puede no permitir equipos cliente adicionales creando una CRL que revoque las credenciales de equipo adicionales pasando la CRL al SDK de DRM de Primetime. Al emitir una licencia, el SDK comprueba la CRL de Adobe y su CRL.

Para generar CRL, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## Detección de reversión {#rollback-detection}

Si la implementación de Adobe Primetime DRM utiliza reglas empresariales que requieran que el cliente mantenga el estado (por ejemplo, el intervalo de ventana de reproducción), Adobe recomienda que el servidor realice un seguimiento del contador de reversiones y utilice la lista de permitidos de AIR o de SWF.

El contador de reversión se envía al servidor en la mayoría de las solicitudes del cliente. Si la implementación de DRM de Primetime no requiere el contador de reversiones, se puede ignorar. De lo contrario, Adobe recomienda que el servidor almacene el ID de equipo aleatorio, que se obtiene mediante [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())y el valor del contador actual en una base de datos.

Para obtener más información sobre cómo incrementar y realizar un seguimiento del contador de reversiones, consulte [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) y Detección de reversión.

## Recuento de máquinas al emitir licencias {#machine-count-when-issuing-licenses}

Si las reglas empresariales requieren que se realice un seguimiento del número de equipos de un usuario, el servidor de licencias o el servidor de dominio deben almacenar los identificadores de equipo asociados al usuario.

La forma más sólida de realizar un seguimiento de los ID de equipo es almacenar el valor que arroja el [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) en una base de datos. Cuando reciba una nueva solicitud, compare el ID de equipo de la solicitud con los ID de equipo conocidos mediante [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) realiza una comparación de los ID para determinar si los ID representan el mismo equipo. Esta comparación solo es práctica si hay un pequeño número de ID de equipo. Por ejemplo, si a los usuarios se les permiten cinco equipos en su dominio, puede buscar en la base de datos los ID de equipo asociados al nombre de usuario del usuario y obtener un pequeño conjunto de datos para comparar.

Esta comparación no es práctica para implementaciones que permiten el acceso anónimo. En este caso, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) se puede utilizar. Sin embargo, este ID no puede ser el mismo si el usuario accede al contenido desde los tiempos de ejecución de Flash y Adobe AIR®.

>[!NOTE]
>
>El ID no se conservará si el usuario vuelve a dar formato al disco duro.

## Protección de repetición {#replay-protection}

La protección de reproducción evita que un atacante reproduzca un mensaje de solicitud de licencia y que pueda provocar un ataque de denegación de servicio (DoS) contra el cliente.

Un ataque DoS es un intento de los atacantes de impedir que los usuarios legítimos de un servicio utilicen ese servicio. Por ejemplo, un ataque de reproducción que utilice el contador de reversión podría utilizarse para &quot;engañar&quot; al servidor de licencias y hacer pensar que el cliente DRM ha revertido su estado, lo que provoca una suspensión de la cuenta.

Para obtener más información acerca de la protección de reproducción, consulte [AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## Mantener una lista de permitidos de paquetes de contenido de confianza {#maintain-a-allowlist-of-trusted-content-packagers}

Una lista de permitidos es una lista de entidades de confianza.

En el caso de los empaquetadores de contenido, las entidades son organizaciones en las que el propietario de contenido confía para empaquetar (o cifrar) los archivos de vídeo y crear contenido protegido por DRM. Al implementar Adobe Primetime DRM, debe mantener una lista de permitidos de paquetes de contenido de confianza. También debe verificar la identidad del empaquetador de contenido en los metadatos DRM de un archivo protegido por DRM antes de emitir una licencia.

Para obtener información sobre la entidad que empaquetó el contenido, consulte [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## Tiempo de espera para tokens de autenticación{#timeout-for-authentication-tokens}

Todos los tokens de autenticación generados por el SDK de DRM de Adobe Primetime tienen un intervalo de tiempo de espera para proteger la seguridad de la aplicación.

La caducidad del token de autenticación se especifica al utilizar el SDK de DRM de Primetime al gestionar una solicitud de autenticación. Una vez caducado, el token deja de ser válido y el usuario debe volver a autenticarse con el servidor de licencias.

Para obtener más información sobre las solicitudes de autenticación, consulte [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## Anular opciones de directiva {#overriding-policy-options}

Al emitir una licencia, el servidor de licencias puede anular las reglas de uso especificadas en la directiva.

Si la directiva especifica una fecha de inicio, no se genera una licencia antes de esa fecha de inicio. Sin embargo, puede establecer una fecha de inicio futura en la licencia una vez generada la licencia. Esta opción debe utilizarse con precaución porque el cliente no puede impedir que el usuario avance el tiempo del sistema para evitar la fecha de inicio.
