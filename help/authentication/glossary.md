---
title: Glosario
description: Glosario
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Glosario {#glossary}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## AccessEnabler {#accessEnabler}

Componente cliente de la autenticación de Adobe Primetime. La autenticación de Adobe Primetime proporciona una biblioteca de AccessEnabler para cada plataforma admitida.

## AuthN {#authn}

Se utiliza como método abreviado para la &quot;autenticación&quot;, como en &quot;Token AuthN&quot; o &quot;Flujo AuthN&quot;.


## Token AuthN{#authn-token}

Token de autenticación, generado por la autenticación de Adobe Primetime después de que un usuario se autentique correctamente con un MVPD. Según la plataforma de integración del programador, el token se almacena en el dispositivo del usuario o en los servidores de autenticación de Adobe Primetime.

## AuthZ {#authz}

Se utiliza como abreviatura para &quot;autorización&quot;, como en &quot;Token AuthZ&quot; o &quot;Flujo AuthZ&quot;.

## Token de AuthZ {#authz-token}

Token de autorización, generado por la autenticación de Adobe Primetime después de autorizar a un usuario a ver contenido protegido. El token AuthZ se almacena en los servidores de autenticación de Adobe Primetime y se utiliza para generar un [Token de medio de corta duración](#short-lived-token).

## ID de canal (obsoleto) {#channel_id}

Término anterior para el ID de recurso.

## API sin cliente {#clientless-api}

Una solución de integración de autenticación de Adobe Primetime que emplea servicios web en lugar del componente cliente AccessEnabler.

## ID del dispositivo {#device-id}

Identifica de forma exclusiva un dispositivo (como un teléfono, una tableta, etc.) en la autenticación de Adobe Primetime. Este ID lo obtiene o proporciona la aplicación del programador.


## Flujo de derechos{#entitlement_flow}

Término utilizado en la documentación de autenticación de Adobe Primetime para hacer referencia a todo el proceso de registro de un dispositivo o usuario con autenticación de Adobe Primetime, autenticación de un usuario con un MVPD, autorización de un recurso para un usuario y cierre de sesión de un usuario.


## GUID {#guid}

Consulte [ID de usuario](#user-id).

## IdP {#idp}

Identificar al proveedor; es sinónimo de MVPD en el contexto de la función de un MVPD en una integración de autenticación de Adobe Primetime. (Los clientes deben verificar su identidad a través de la página de inicio de sesión de su proveedor de televisión de pago).

## Verificador de tokens de medios {#media-token-verifier}

Una biblioteca proporcionada por el Adobe que usan los programadores para comprobar el token de medios de corta duración generado por la autenticación de Adobe Primetime después de completar correctamente un flujo de derechos.

## MVPD {#mvpd}

Distribuidor de programación de vídeo multicanal; sinónimo de &quot;proveedor de televisión de pago&quot;.

## ID de MVPD {#mvpd-id}

Consulte [ID de usuario](#user-id).

## ID de socio {#partner-id}

Identificador que el Adobe pasa a los MVPD, que lo utilizan para identificarse en cuyo nombre la autenticación de Adobe Primetime solicita la autenticación. A veces se utiliza para configurar sus UI para programadores particulares, a veces es lo mismo en todos los programadores, depende de las necesidades de MVPD.

## Proveedor de televisión de pago {#pay-tv-provider}

Sinónimo de [MVPD](#mvpd).

## Programador {#programmer}

Es sinónimo de &quot;proveedor de contenido&quot;, &quot;cuenta&quot;, &quot;canal&quot;, &quot;proveedor de servicios&quot;, &quot;marca&quot;, etc.

## MVPD de proxy {#proxy-mvpd}

Un MVPD que proporcione servicios de identidad para otros MVPD; directamente integrado con la autenticación de Adobe Primetime.

## MVPD Proxix {#proxied-mvpd}

Un MVPD que no tiene una integración directa con el SP de Adobe, pero que está integrado a través de un MVPD de Proxy.

## ID del solicitante {#requestor-id}

Identifica de forma exclusiva un [Programador](#programmer) (una cuenta, marca, canal o propiedad) dentro de la autenticación de Adobe Primetime. Este ID se determina entre el programador y el Adobe durante la configuración inicial de la cuenta. En la web, el ID del solicitante está asociado a un conjunto de dominios en la lista blanca; cualquier llamada que utilice un ID de un dominio externo se rechazará. Los programadores también utilizan el ID del solicitante para el análisis. Normalmente solo hay un ID de solicitante por programador. Una característica adicional relacionada con el ID del solicitante es que el programador debe proporcionar un certificado público al Adobe, ya que la llamada a la API setRequestor espera que se envíen datos cifrados, y se utiliza para autenticar al programador en el sistema de autenticación de Adobe Primetime.

## ID de recurso {#resource-id}

Una cadena o recurso mRSS que identifica un [Programador](#programmer) a MVPD. Se acuerda entre el Programador y los MVPD; La autenticación de Adobe Primetime pasa el ID de recurso a través de sin tocar, por lo que debe ser el mismo para todos los MVPD. Un programador puede utilizar varios ID de recursos siempre que los MVPD sepan lo que representa cada ID.

## SessionGUID {#sessionGUID}

Consulte [ID de usuario](#user-id).

## Token de medio de corta duración {#short-lived-token}

Este token lo genera la autenticación de Adobe Primetime cuando el proceso de asignación de derechos de un usuario concreto se completa correctamente. El token se pasa al programador, que utiliza el verificador de autenticadores de autenticación de Adobe Primetime en el token de medios de corta duración para verificar la seguridad del proceso de asignación de derechos.

## Dispositivo inteligente {#smart-device}

Término que se utiliza en toda la documentación de autenticación de Adobe Primetime para hacer referencia a cuadros de inicio, consolas de juegos y televisores inteligentes. Se trata de dispositivos que tienen funciones de red, pero que no pueden procesar páginas web.

## SP{#sp}

Proveedor de servicios; esto generalmente hace referencia a la variable *función* de SP, reproducido por la autenticación de Adobe Primetime, actuando en nombre de un programador en una integración con un [MVPD](#mvpd).

## Pase temporal {#temp-pass}

Característica que permite a los programadores proporcionar acceso gratuito temporal al contenido de pago. El acceso es por solicitante, para un período de tiempo especificado por el programador.

## TTL {#ttl}

Tiempo De Vida. Este es el período de tiempo especificado para que un token sea válido.

## TVE {#tve}

Televisión en todas partes.

## ID de usuario {#user-id}

Identifica de forma exclusiva al usuario de la aplicación de un programador, pero se origina desde el MVPD. Disponible en diferentes formularios para diferentes casos de uso. Consulte [Información sobre los ID de usuario en la información general del programador](/help/authentication/programmer-overview.md#user-ids).

## Lista de permitidos {#whitelist}

Una lista de dominios designados como legítimos para la comunicación con la autenticación de Adobe Primetime.

## Token XSTS {#xsts-token}

Token de seguridad emitido por Microsoft para el desarrollo de aplicaciones de la consola Xbox, usado en la integración de autenticación de Xbox/Adobe Primetime.
