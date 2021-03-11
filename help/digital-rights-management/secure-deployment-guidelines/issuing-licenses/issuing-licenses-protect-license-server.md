---
description: 'Debe asegurarse de que está emitiendo licencias de forma segura. Tenga en cuenta estas prácticas recomendadas para proteger el servidor de licencias '
title: Protección del servidor de licencias
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---


# Protección del servidor de licencias {#protecting-the-license-server}

Debe asegurarse de que está emitiendo licencias de forma segura. Tenga en cuenta estas prácticas recomendadas para proteger el servidor de licencias:

## Consumo de listas CRL generadas localmente {#consuming-locally-generated-crls}

Para consumir listas de revocación de certificados (CRL) generadas localmente y listas de actualización de directivas, utilice las API de Adobe Primetime DRM para verificar la firma.

Las siguientes API verifican que las listas no se hayan manipulado y que las listas hayan sido firmadas por el servidor de licencias correcto:

* Llame a [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) para comprobar la firma antes de proporcionar [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a cualquier API.

   Para obtener más información, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Llame a [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) para comprobar la firma antes de proporcionar el `PolicyUpdateList` a cualquier API.

   Para obtener más información, consulte [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Consumo de listas CRL publicadas por Adobe{#consuming-crls-published-by-adobe}

El SDK descarga periódicamente las CRL publicadas por Adobe. Debe asegurarse de que el acceso a estos archivos no esté bloqueado o de que no se impida la aplicación de estas CRL.

El SDK tiene una opción de configuración para ignorar los errores al recuperar las CRL de Adobe y solo puede aplicar esta opción en entornos de desarrollo. En entornos de producción, el servidor de licencias debe recuperar las CRL desde el Adobe. Si el servidor de licencias no puede obtener una CRL válida, se ha producido un error.

## Generación de listas CRL para complementar las publicadas por Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Puede utilizar Adobe Primetime DRM para crear listas CRL que complementen la CRL del equipo que publica el Adobe.

El SDK de DRM de Primetime comprueba y aplica las CRL de Adobe. Sin embargo, puede no permitir equipos cliente adicionales creando una CRL que revoque credenciales de equipo adicionales pasando la CRL al SDK de DRM de Primetime. Cuando emite una licencia, el SDK comprueba la CRL de Adobe y la CRL.

Para generar listas CRL, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## Detección de reversión {#rollback-detection}

Si su implementación de Adobe Primetime DRM utiliza reglas comerciales que requieren que el cliente mantenga el estado (por ejemplo, el intervalo de la ventana de reproducción), Adobe recomienda que el servidor realice un seguimiento del contador de reversión y utilice la lista de permitidos de AIR o SWF.

El contador de reversión se envía al servidor en la mayoría de las solicitudes del cliente. Si la implementación de DRM de Primetime no requiere el contador de reversión, se puede ignorar. De lo contrario, Adobe recomienda que el servidor almacene el ID de equipo aleatorio, que se obtiene mediante [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), y el valor de contador actual en una base de datos.

Para obtener más información sobre cómo incrementar y rastrear el contador de reversión, consulte [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) y Detección de reversión.

## Recuento de máquinas al emitir licencias {#machine-count-when-issuing-licenses}

Si las reglas comerciales requieren que se realice un seguimiento del número de equipos de un usuario, el servidor de licencias o el servidor de dominio deben almacenar los ID de equipo asociados al usuario.

La forma más sólida de rastrear los ID de equipo es almacenar el valor devuelto por el método [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) en una base de datos. Cuando se recibe una nueva solicitud, compare el ID del equipo de la solicitud con los ID del equipo conocidos mediante el uso de [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) realiza una comparación de ID para determinar si los ID representan el mismo equipo. Esta comparación solo es práctica si hay un pequeño número de ID de equipo. Por ejemplo, si se permite a los usuarios cinco equipos en su dominio, puede buscar en la base de datos los ID de equipo asociados al nombre de usuario del usuario y obtener un pequeño conjunto de datos para compararlos.

Esta comparación no es práctica para implementaciones que permiten el acceso anónimo. En este caso, se puede utilizar [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()). Sin embargo, este ID no puede ser el mismo si el usuario accede al contenido desde los tiempos de ejecución de Flash y Adobe AIR®.

>[!NOTE]
>
>El ID no sobrevive si el usuario cambia el formato del disco duro.

## Protección contra repetición {#replay-protection}

La protección de reproducción evita que un atacante vuelva a reproducir un mensaje de solicitud de licencia y pueda causar un ataque de denegación de servicio (DoS) contra el cliente.

Un ataque DoS es un intento de los atacantes de evitar que los usuarios legítimos de un servicio usen ese servicio. Por ejemplo, un ataque de reproducción que utilice el contador de reversión podría utilizarse para &quot;engañar&quot; al servidor de licencias para que piense que el cliente de DRM ha vuelto a su estado, lo que provoca una suspensión de la cuenta.

Para obtener más información sobre la protección contra repetición, consulte [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## Mantener una lista de permitidos de paquetes de contenido de confianza {#maintain-a-allowlist-of-trusted-content-packagers}

Una lista de permitidos es una lista de entidades de confianza.

Para los paquetes de contenido, las entidades son organizaciones en las que el propietario del contenido confía para empaquetar (o encriptar) los archivos de vídeo y crear contenido protegido por DRM. Al implementar Adobe Primetime DRM, debe mantener una lista de permitidos de paquetes de contenido de confianza. También debe verificar la identidad del paquete de contenido en los metadatos DRM de un archivo protegido DRM antes de emitir una licencia.

Para obtener información sobre la entidad que empaquetó el contenido, consulte [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## Tiempo de espera para los tokens de autenticación{#timeout-for-authentication-tokens}

Todos los tokens de autenticación generados por el SDK de Adobe Primetime DRM tienen un intervalo de tiempo de espera para proteger la seguridad de la aplicación.

La caducidad del token de autenticación se especifica mediante el uso del SDK de DRM de Primetime al gestionar una solicitud de autenticación. Una vez caducado, el token ya no es válido y el usuario debe volver a autenticarse con el servidor de licencias.

Para obtener más información sobre las solicitudes de autenticación, consulte [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## Anulación de opciones de directiva {#overriding-policy-options}

Al emitir una licencia, el servidor de licencias puede anular las reglas de uso especificadas en la directiva.

Si la directiva especifica una fecha de inicio, no se genera una licencia antes de esa fecha de inicio. Sin embargo, puede establecer una fecha de inicio futura en la licencia después de generarla. Esta opción debe utilizarse con precaución, ya que el cliente no puede impedir que el usuario mueva el tiempo del sistema hacia adelante para evitar la fecha de inicio.