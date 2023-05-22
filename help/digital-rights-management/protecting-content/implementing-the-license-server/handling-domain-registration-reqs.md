---
title: Administrar solicitudes de registro de dominio
description: Administrar solicitudes de registro de dominio
copied-description: true
exl-id: 6f4ed908-32ee-4c8b-8965-53381b737989
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# Administrar solicitudes de registro de dominio {#handle-domain-registration-requests}

Si los metadatos DRM indican que es necesario registrar el dominio para reproducir el contenido, la aplicación cliente debe invocar el `DRMManager.addToDeviceGroup()` API de ActionScript o `joinLicenseDomain()` API de iOS. Si el cliente aún no se ha registrado con el servidor de dominio especificado (o si la aplicación está forzando una nueva unión), se envía una solicitud de registro de dominio. El servidor de dominios determina si se permite al cliente unirse a un dominio y emite una o más credenciales de dominio al cliente.

* La clase del controlador de solicitud es `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* La clase de mensaje de solicitud es `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Si tanto el cliente como el servidor admiten el protocolo versión 5, la dirección URL de solicitud es &quot;URL del servidor de dominio en los metadatos: +&quot; [!DNL /flashaccess/domain/v4]&quot;. De lo contrario, la URL de solicitud es la URL del servidor de dominio en los metadatos &quot; + &quot; [!DNL /flashaccess/domain/v3]&quot;

Al inicializar el `DomainRegistrationHandler`, debe especificar la URL del servidor de dominio. A continuación, esta dirección URL se incluye en los tokens de dominio emitidos por el controlador para indicar al servidor de dominio que se ha emitido el token. La URL debe coincidir con la URL del servidor de dominio especificada en cualquier directiva DRM que requiera el registro de dominio con el servidor.

Para determinar si se permite al cliente unirse al dominio, el servidor puede examinar la información del equipo y del usuario en la solicitud. El servidor también puede determinar a qué dominio puede unirse el cliente.

>[!NOTE]
>
>Un cliente solo puede ser miembro de un dominio por URL de servidor de dominio. Si el equipo ya tiene un token de dominio para esta URL de servidor de dominio, la solicitud de registro de dominio incluye el nombre de dominio actual ( `getRequestDomainName()`).

Para una solicitud de reunión, el servidor de dominio debe devolver el conjunto actual de credenciales de dominio para este dominio o devolver un error. Es posible que el servidor de dominios no devuelva las credenciales de dominio de un dominio diferente.

Consulte [Uso de identificadores de equipo](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#use-machine-identifiers) para obtener información sobre cómo identificar y contar los equipos que se unen al dominio.

Si el servidor de dominio requiere autenticación para unirse a un dominio, la solicitud debe contener un token de autenticación. Al igual que con una solicitud de licencia, el registro de dominio puede requerir un nombre de usuario/contraseña o autenticación personalizada.

Consulte [Autenticación de usuario](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#user-authentication) para obtener más información sobre cómo administrar los tokens de autenticación.

El servidor de dominios es responsable de almacenar y administrar las claves de dominio asociadas a cada dominio. Cuando sea necesario generar un nuevo par de claves para un dominio (el primer registro de dominios para el dominio), se debe invocar `generateDomainCredential(String, int, Principal, Date)`. Este método genera un nuevo par de claves de dominio y un certificado de dominio. El servidor de dominio debe almacenar la clave privada y el certificado y proporcionar esos objetos al procesar las solicitudes posteriores para este dominio. También es posible generar un nuevo par de claves para un dominio a fin de renovar las claves. Cuando transfiera las claves de un dominio concreto, asegúrese de incrementar la versión de la clave en `generateDomainCredential`.

Cada vez que un equipo se registra con el mismo dominio, se debe utilizar la misma clave privada y el mismo certificado de dominio. Invocar `addDomainCredential(DomainToken, PrivateKey)` para devolver una credencial de dominio existente al cliente. Si hay varias credenciales de dominio para el dominio porque se cambiaron las claves de dominio, el servidor debe proporcionar credenciales de dominio para la clave de dominio actual y todas las claves de dominio anteriores para que el cliente pueda consumir licencias enlazadas a claves de dominio antiguas. Esto permite mover una licencia enlazada a un token de dominio antiguo a un equipo recién registrado y seguir reproduciéndose.
