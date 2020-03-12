---
seo-title: Administrar solicitudes de registro de dominio
title: Administrar solicitudes de registro de dominio
uuid: d92db6c2-5a16-41ea-a1aa-541c59780678
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Administrar solicitudes de registro de dominio {#handle-domain-registration-requests}

Si los metadatos DRM indican que es necesario registrar el dominio para reproducir el contenido, la aplicación cliente debe invocar la API de `DRMManager.addToDeviceGroup()` ActionScript o la API de `joinLicenseDomain()` iOS. Si el cliente aún no se ha registrado en el servidor de dominio especificado (o si la aplicación está obligando a volver a unirse), se envía una solicitud de registro de dominio. El servidor de dominio determina si el cliente puede unirse a un dominio y emite una o varias credenciales de dominio al cliente.

* La clase de controlador de solicitudes es `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la dirección URL de la solicitud es &quot;URL del servidor de dominio en metadatos: + &quot; [!DNL /flashaccess/domain/v4]&quot;. De lo contrario, la dirección URL de la solicitud es la URL del servidor de dominio en los metadatos&quot; + &quot; [!DNL /flashaccess/domain/v3]&quot;

Al inicializar el `DomainRegistrationHandler`, debe especificar la dirección URL del servidor de dominio. Esta dirección URL se incluye en los tokens de dominio emitidos por el controlador para indicar al servidor de dominio que se ha emitido el token. La dirección URL debe coincidir con la dirección URL del servidor de dominio especificada en cualquier directiva DRM que requiera el registro de dominio con el servidor.

Para determinar si el cliente está autorizado a unirse al dominio, el servidor puede examinar la información del equipo y del usuario en la solicitud. El servidor también puede determinar el dominio al que se permite unirse el cliente.

>[!NOTE]
>
>Un cliente solo puede ser miembro de un dominio por dirección URL de servidor de dominio. Si el equipo ya tiene un token de dominio para esta URL de servidor de dominio, la solicitud de registro de dominio incluye el nombre de dominio actual ( `getRequestDomainName()`).

Para una solicitud de reunión, el servidor de dominio debe devolver el conjunto actual de credenciales de dominio para este dominio o devolver un error. El servidor de dominio no puede devolver las credenciales de dominio para un dominio diferente.

Consulte [Uso de identificadores](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#use-machine-identifiers) de equipo para obtener información sobre cómo identificar y contar los equipos que se unen al dominio.

Si el servidor de dominio requiere autenticación para unirse a un dominio, la solicitud debe contener un token de autenticación. Al igual que con una solicitud de licencia, el registro del dominio puede requerir un nombre de usuario/contraseña o autenticación personalizada.

Consulte Autenticación [de usuarios](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#user-authentication) para obtener más información sobre cómo administrar los tokens de autenticación.

El servidor de dominio es responsable de almacenar y administrar las claves de dominio asociadas con cada dominio. Cuando se necesita generar un nuevo par de claves para un dominio (el primer registro de dominio para el dominio), se debe invocar `generateDomainCredential(String, int, Principal, Date)`. Este método genera un nuevo par de claves de dominio y un certificado de dominio. El servidor de dominio debe almacenar la clave privada y el certificado y proporcionar dichos objetos al procesar solicitudes posteriores para este dominio. También es posible generar un nuevo par de claves para un dominio a fin de pasar las claves. Cuando pase el cursor sobre las claves de un dominio en particular, asegúrese de incrementar la versión clave en `generateDomainCredential`.

Cada vez que un equipo se registra con el mismo dominio, se debe utilizar la misma clave privada de dominio y el mismo certificado. Invocar `addDomainCredential(DomainToken, PrivateKey)` para devolver una credencial de dominio existente al cliente. Si hay varias credenciales de dominio para el dominio porque se cambiaron las claves de dominio, el servidor debe proporcionar credenciales de dominio para la clave de dominio actual y todas las claves de dominio anteriores para que el cliente pueda consumir licencias vinculadas a claves de dominio antiguas. Esto permite que una licencia enlazada a un token de dominio antiguo se mueva a un equipo recién registrado y se pueda reproducir.
