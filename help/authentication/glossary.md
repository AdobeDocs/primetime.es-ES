---
title: Glosario
description: Glosario
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# Glosario {#glossary}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

## AccessEnabler {#accessEnabler}

Componente de cliente de la autenticación de Adobe Primetime. La autenticación de Adobe Primetime proporciona una biblioteca AccessEnabler para cada plataforma compatible.

## AuthN {#authn}

Se utiliza como abreviatura para &quot;autenticación&quot;, como en &quot;Token AuthN&quot; o &quot;Flujo AuthN&quot;.


## Token de AuthN{#authn-token}

Token de autenticación, generado por la autenticación de Adobe Primetime después de que un usuario se autentique correctamente con una MVPD. Según la plataforma de integración del programador, el token se almacena en el dispositivo del usuario o en los servidores de autenticación de Adobe Primetime.

## AuthZ {#authz}

Se utiliza como abreviatura de &quot;autorización&quot;, como en &quot;AuthZ Token&quot; o &quot;AuthZ Flow&quot;.

## Token de AuthZ {#authz-token}

Token de autorización, generado por la autenticación de Adobe Primetime después de que un usuario haya sido autorizado para ver contenido protegido. El token de AuthZ se almacena en servidores de autenticación de Adobe Primetime y se utiliza para generar una [Token de medios de corta duración](#short-lived-token).

## ID de canal (obsoleto) {#channel_id}

Término anterior del ID de recurso.

## API sin cliente {#clientless-api}

Una solución de integración de autenticación de Adobe Primetime que emplea servicios web en lugar del componente de cliente AccessEnabler.

## ID de dispositivo {#device-id}

Identifica de forma exclusiva un dispositivo (como un teléfono, una tableta, etc.) en la autenticación de Adobe Primetime. La aplicación del programador obtiene/proporciona este ID.


## Flujo de derecho{#entitlement_flow}

Término que se utiliza en la documentación de autenticación de Adobe Primetime para referirse a todo el proceso de registro de un dispositivo o usuario con autenticación de Adobe Primetime, autenticación de un usuario con una MVPD, autorización de un recurso para un usuario y cierre de sesión de un usuario.


## GUID {#guid}

Consulte [ID de usuario](#user-id).

## IdP {#idp}

Identificar proveedor; sinónimo de MVPD en el contexto de la función de una MVPD en una integración de autenticación de Adobe Primetime. (Los clientes deben verificar su identidad a través de la página de inicio de sesión de su proveedor de TV de pago).

## Media Token Verifier {#media-token-verifier}

Biblioteca proporcionada por Adobe que utilizan los programadores para comprobar el token de medios de corta duración generado por la autenticación de Adobe Primetime después de completar correctamente un flujo de derechos.

## MVPD {#mvpd}

Distribuidor de programación de vídeo multicanal; sinónimo de &quot;Proveedor de TV de pago&quot;.

## ID de MVPD {#mvpd-id}

Consulte [ID de usuario](#user-id).

## ID de socio {#partner-id}

Identificador que el Adobe pasa a las MVPD, que lo utilizan para identificar en nombre de quién la autenticación de Adobe Primetime solicita autenticación. A veces se utiliza para configurar sus IU para programadores particulares, a veces es el mismo en todos los programadores, depende de las necesidades de la MVPD.

## Proveedor de TV de pago {#pay-tv-provider}

Sinónimo de [MVPD](#mvpd).

## Programador {#programmer}

Sinónimo de &quot;proveedor de contenido&quot;, &quot;cuenta&quot;, &quot;canal&quot;, &quot;proveedor de servicios&quot;, &quot;marca&quot;, etc.

## MVPD proxy {#proxy-mvpd}

Una MVPD que proporciona servicios de identidad para otras MVPD; directamente integrada con la autenticación de Adobe Primetime.

## MVPD por proxy {#proxied-mvpd}

Una MVPD que no tiene una integración directa con el SP de Adobe, pero que está integrada a través de un MVPD proxy.

## ID de solicitante {#requestor-id}

Identifica de forma exclusiva a [Programador](#programmer) (una cuenta, marca, canal o propiedad) dentro de la autenticación de Adobe Primetime. Este ID se determina entre el Programador y el Adobe durante la configuración inicial de la cuenta. En la web, el ID de solicitante está asociado a un conjunto de dominios en la lista blanca; se rechazará cualquier llamada que utilice un ID de un dominio externo. Los programadores también utilizan el ID de solicitante para Analytics. Normalmente, solo hay un ID de solicitante por programador. Una función adicional relacionada con el ID de solicitante es que el programador debe proporcionar Adobe con un certificado público, ya que la llamada de API setRequestor espera que se envíen datos cifrados, utilizados para autenticar al programador en el sistema de autenticación de Adobe Primetime.

## ID de recurso {#resource-id}

Una cadena o recurso mRSS que identifica un [Programador](#programmer) a MVPD. Se acuerda entre el programador y las MVPD; la autenticación de Adobe Primetime pasa el ID de recurso intacto, por lo que debe ser el mismo para todas las MVPD. Un programador puede utilizar varios ID de recurso siempre que las MVPD sepan lo que representa cada ID.

## SessionGUID {#sessionGUID}

Consulte [ID de usuario](#user-id).

## Token de medios de corta duración {#short-lived-token}

La autenticación de Adobe Primetime genera este token al completarse correctamente el proceso de asignación de derechos para un usuario determinado. El token se pasa al programador, que utiliza el verificador de tokens de autenticación de Adobe Primetime en el token de medios de corta duración para verificar la seguridad del proceso de asignación de derechos.

## Smart Device {#smart-device}

Término utilizado en toda la documentación de autenticación de Adobe Primetime para referirse a los decodificadores, las consolas de juegos y los televisores inteligentes. Son dispositivos que tienen capacidades de red, pero no son capaces de procesar páginas web.

## SP{#sp}

Proveedor de servicios; esto suele referirse a la variable *función* de SP, reproducido por la autenticación de Adobe Primetime, que actúa en nombre de un programador en una integración con un [MVPD](#mvpd).

## Pase temporal {#temp-pass}

Característica que permite a los programadores proporcionar acceso gratuito temporal al contenido de pago. El acceso es por solicitante, durante un período de tiempo especificado por el programador.

## TTL {#ttl}

Tiempo de vida. Período de tiempo especificado en el que un token es válido.

## TVE {#tve}

Televisión Por Todas Partes.

## ID de usuario {#user-id}

Identifica de forma exclusiva al usuario de la aplicación de un programador, pero se origina a partir de la MVPD. Disponible en diferentes formularios para diferentes casos de uso. Consulte [Explicación de los ID de usuario en la Información general del programador](/help/authentication/programmer-overview.md#user-ids).

## Lista de permitidos {#whitelist}

Una lista de dominios designados como legítimos para comunicarse con la autenticación de Adobe Primetime.

## Token XSTS {#xsts-token}

Token de seguridad emitido por Microsoft para el desarrollo de aplicaciones de la consola Xbox, utilizado en la integración de autenticación de Xbox/Adobe Primetime.
