---
seo-title: Gestión de solicitudes de registro de dominio
title: Gestión de solicitudes de registro de dominio
uuid: e0cef9c4-b2d1-4bec-8dce-50452bc826fb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestión de solicitudes de registro de dominio{#handling-domain-registration-requests}

Si los metadatos DRM indican que se necesita el registro de dominio para reproducir el contenido, la aplicación cliente debe invocar la API de ActionScript DRMManager.addToDeviceGroup() o la API de iOS joinLicenseDomain(). Si el cliente aún no se ha registrado en el servidor de dominio especificado (o si la aplicación está obligando a volver a unirse), se envía una solicitud de registro de dominio. El servidor de dominio determina si el cliente puede unirse a un dominio y emite una o varias credenciales de dominio al cliente.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la dirección URL de la solicitud es &quot;URL del servidor de dominio en metadatos: + &quot;/flashaccess/domain/v4&quot;. De lo contrario, la URL de la solicitud es la URL del servidor de dominio en los metadatos&quot; + &quot;/flashaccess/domain/v3&quot;

Al inicializar el `DomainRegistrationHandler`, se debe especificar la dirección URL del servidor de dominio. Esta dirección URL se incluirá en los tokens de dominio emitidos por el controlador para indicar el servidor de dominio que emitió el token. La dirección URL debe coincidir con la dirección URL del servidor de dominio especificada en cualquier directiva que requiera el registro de dominio con el servidor.

Para determinar si el cliente está autorizado a unirse al dominio, el servidor puede examinar la información del equipo y del usuario en la solicitud. Consulte [Uso de identificadores](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) de equipo para obtener información sobre cómo identificar y contar los equipos que se unen al dominio. El servidor también puede determinar el dominio al que se permite unirse el cliente. Tenga en cuenta que un cliente solo puede ser miembro de una dirección URL de dominio por servidor de dominio. Si el equipo ya tiene un token de dominio para esta URL de servidor de dominio, la solicitud de registro de dominio incluirá el nombre de dominio actual ( `getRequestDomainName()`). Para una solicitud de reunión, el servidor de dominio debe devolver el conjunto actual de credenciales de dominio para este dominio o devolver un error (es posible que el servidor de dominio no devuelva las credenciales de dominio para otro dominio).

Si el servidor de dominio requiere autenticación para unirse a un dominio, la solicitud debe contener un token de autenticación. Al igual que con una solicitud de licencia, el registro del dominio puede requerir un nombre de usuario/contraseña o autenticación personalizada. Consulte Autenticación [de usuarios](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) para obtener más información sobre la administración de tokens de autenticación.

El servidor de dominio es responsable de almacenar y administrar las claves de dominio asociadas con cada dominio. Cuando sea necesario generar un nuevo par de claves para un dominio (el primer registro de dominio para el dominio), invoque `generateDomainCredential``(String, int, Principal, Date)`. Este método generará un nuevo par de claves de dominio y un certificado de dominio. El servidor de dominio debe almacenar la clave privada y el certificado y proporcionar dichos objetos al procesar solicitudes posteriores para este dominio. También es posible generar un nuevo par de claves para un dominio a fin de pasar las claves. Al pasar el ratón por encima de las claves de un dominio en particular, asegúrese de incrementar `generateDomainCredential` también la versión clave.

Cada vez que un equipo se registra con el mismo dominio, se debe utilizar la misma clave privada de dominio y el mismo certificado. Invocar `addDomainCredential(DomainToken, PrivateKey)` para devolver una credencial de dominio existente al cliente. Si hay varias credenciales de dominio para el dominio porque se cambiaron las claves de dominio, el servidor debe proporcionar credenciales de dominio para la clave de dominio actual y todas las claves de dominio anteriores para que el cliente pueda consumir licencias vinculadas a claves de dominio antiguas. Esto permite que una licencia enlazada a un token de dominio antiguo se mueva a un equipo recién registrado y se pueda reproducir.
