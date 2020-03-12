---
description: 'Debe asegurarse de que está emitiendo licencias de forma segura. Considere estas prácticas recomendadas para proteger el servidor de licencias '
seo-description: 'Debe asegurarse de que está emitiendo licencias de forma segura. Considere estas prácticas recomendadas para proteger el servidor de licencias '
seo-title: Protección del servidor de licencias
title: Protección del servidor de licencias
uuid: 7b5de17d-d0a7-41df-9651-4ff51c9965c6
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Protección del servidor de licencias {#protecting-the-license-server}

Debe asegurarse de que está emitiendo licencias de forma segura. Tenga en cuenta estas optimizaciones para proteger el servidor de licencias:

## Consumo de CRL generadas localmente {#consuming-locally-generated-crls}

Para consumir listas de revocación de certificados (CRL) generadas localmente y listas de actualización de políticas, utilice las API de DRM de Adobe Primetime para verificar la firma.

Las siguientes API comprueban que las listas no se han manipulado y que las listas están firmadas por el servidor de licencias correcto:

* Llame a [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) para comprobar la firma antes de proporcionar [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a cualquier API.

   Para obtener más información, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Llame a [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) para comprobar la firma antes de proporcionar el `PolicyUpdateList` a cualquier API.

   Para obtener más información, consulte [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Consumo de CRL publicadas por Adobe{#consuming-crls-published-by-adobe}

El SDK descarga periódicamente las CRL publicadas por Adobe. Debe asegurarse de que no se bloquee el acceso a estos archivos o de que no se impida la aplicación de estas CRL.

El SDK tiene una opción de configuración para ignorar los errores al recuperar las CRL de Adobe y solo puede aplicar esta opción en entornos de desarrollo. En los entornos de producción, el servidor de licencias debe recuperar las CRL de Adobe. Si el servidor de licencias no puede obtener una CRL válida, se ha producido un error.

## Generación de CRL para complementar las publicadas por Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Puede utilizar DRM de Adobe Primetime para crear CRL que complementen la CRL de equipos publicada por Adobe.

El SDK de DRM de Primetime comprueba y aplica las CRL de Adobe. Sin embargo, puede no permitir equipos cliente adicionales creando una CRL que revoque las credenciales de equipo adicionales pasando la CRL al SDK de DRM de Primetime. Cuando se emite una licencia, el SDK comprueba la CRL de Adobe y la CRL.

Para generar CRL, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## Detección de retroceso {#rollback-detection}

Si la implementación de Adobe Primetime DRM utiliza reglas comerciales que requieren que el cliente mantenga el estado (por ejemplo, el intervalo de la ventana de reproducción), Adobe recomienda que el servidor rastree el contador de rollback y utilice la lista blanca de AIR o SWF.

El contador de reversión se envía al servidor en la mayoría de las solicitudes del cliente. Si la implementación de DRM de Primetime no requiere el contador de reversión, se puede ignorar. De lo contrario, Adobe recomienda que el servidor almacene el ID de equipo aleatorio, que se obtiene mediante [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), y el valor de contador actual en una base de datos.

Para obtener más información sobre cómo incrementar y realizar el seguimiento del contador de rollback, consulte Detección de [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) y Rollback.

## Recuento de equipos al emitir licencias {#machine-count-when-issuing-licenses}

Si las reglas comerciales requieren que se realice un seguimiento del número de equipos de un usuario, el servidor de licencias o el servidor de dominio deben almacenar los ID de equipo asociados al usuario.

La forma más sólida de rastrear los ID de equipo es almacenar el valor devuelto por el método [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) en una base de datos. Cuando se recibe una nueva solicitud, compare el ID de equipo de la solicitud con los ID de equipo conocidos mediante [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) realiza una comparación de ID para determinar si los ID representan el mismo equipo. Esta comparación solo es práctica si hay un pequeño número de ID de máquina. Por ejemplo, si se permite a los usuarios cinco equipos en su dominio, puede buscar en la base de datos los ID de equipo asociados al nombre de usuario del usuario y obtener un pequeño conjunto de datos para la comparación.

Esta comparación no es práctica para implementaciones que permiten el acceso anónimo. En este caso, se puede usar [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) . Sin embargo, este ID no puede ser el mismo si el usuario accede al contenido desde los tiempos de ejecución de Flash y Adobe AIR®.

>[!NOTE]
>
>El ID no sobrevive si el usuario cambia el formato del disco duro.

## Protección contra repetición {#replay-protection}

La protección de reproducción evita que un atacante vuelva a reproducir un mensaje de solicitud de licencia y pueda causar un ataque de denegación de servicio (DoS) contra el cliente.

Un ataque DoS es un intento de los atacantes de evitar que los usuarios legítimos de un servicio usen ese servicio. Por ejemplo, un ataque de reproducción que utilice el contador de reversión podría utilizarse para &quot;engañar&quot; al servidor de licencias para que piense que el cliente de DRM ha revertido su estado, lo que provoca una suspensión de la cuenta.

Para obtener más información sobre la protección contra la reproducción, consulte [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## Mantener una lista blanca de empaquetadores de contenido de confianza{#maintain-a-whitelist-of-trusted-content-packagers}

Una lista blanca es una lista de entidades de confianza.

Para los empaquetadores de contenido, las entidades son organizaciones en las que el propietario del contenido confía para empaquetar (o cifrar) los archivos de vídeo y crear contenido protegido con DRM. Al implementar Adobe Primetime DRM, debe mantener una lista blanca de empaquetadores de contenido de confianza. También debe comprobar la identidad del empaquetador de contenido en los metadatos DRM de un archivo protegido con DRM antes de emitir una licencia.

Para obtener información sobre la entidad que empaquetó el contenido, consulte [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## Tiempo de espera para los tokens de autenticación{#timeout-for-authentication-tokens}

Todos los tokens de autenticación generados por el SDK de DRM de Adobe Primetime tienen un intervalo de tiempo de espera para proteger la seguridad de la aplicación.

La caducidad del autentificador se especifica mediante el uso del SDK de Primetime DRM al gestionar una solicitud de autenticación. Una vez caducado, el token ya no es válido y el usuario debe volver a autenticarse con el servidor de licencias.

Para obtener más información sobre las solicitudes de autenticación, consulte [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## Anular opciones de directiva {#overriding-policy-options}

Al emitir una licencia, el servidor de licencias puede anular las reglas de uso especificadas en la directiva.

Si la política especifica una fecha de inicio, no se genera una licencia antes de esa fecha de inicio. Sin embargo, puede establecer una fecha de inicio futura en la licencia una vez generada la licencia. Esta opción debe utilizarse con precaución, ya que el cliente no puede evitar que el usuario mueva el tiempo del sistema hacia adelante para evitar la fecha de inicio.