---
title: Autenticación mediante el protocolo OAuth 2.0
description: Autenticación mediante el protocolo OAuth 2.0
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---


# Autenticación mediante el protocolo OAuth 2.0

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#overview}

Aunque SAML sigue siendo el protocolo principal utilizado para la autenticación por los MVPD de EE. UU. y las empresas en general, existe una clara tendencia a pasar a OAuth 2.0 como el protocolo de autenticación principal. El protocolo OAuth 2.0 (https://tools.ietf.org/html/rfc6749) se desarrolló principalmente para sitios de consumidores y fue rápidamente adoptado por gigantes de Internet como Facebook, Google y Twitter.

OAuth 2.0 tiene un gran éxito y esto ha llevado a las empresas a actualizar lentamente sus infraestructuras para apoyarlo.



## Ventajas de pasar a OAuth 2.0 {#adv-oauth2}

En un nivel superior, el protocolo OAuth 2.0 ofrece la misma funcionalidad que el protocolo SAML, pero hay algunas distinciones importantes.

Una de ellas es el hecho de que el flujo del token de actualización se puede utilizar como una forma de actualizar la autenticación entre bastidores. Esto permite que el IdP (los MVPD en este caso) mantenga el control y, a la vez, permita una buena experiencia de usuario, ya que ya no es necesario que el usuario inicie sesión con frecuencia debido a problemas de seguridad.

El protocolo también ofrece más flexibilidad en términos de los datos expuestos como proveedor de servicios, ahora puede utilizar los tokens para acceder a otras API para obtener información adicional. Esto a su vez resulta en un protocolo &quot;chattier&quot; para casos de uso de TVE, pero permite la flexibilidad necesaria para flujos de trabajo complejos.





## Requisitos para cambiar a OAuth 2.0 {#oauth-req}

Para admitir la autenticación con OAuth 2.0, un MVPD debe cumplir los siguientes requisitos previos:

En primer lugar, el MVPD debe asegurarse de que es compatible con el *[Concesión de código de autorización](https://oauthlib.readthedocs.io/en/latest/oauth2/grants/authcode.html) flujo.

Después de confirmar que soporta el flujo, el MVPD debe proporcionarnos la siguiente información:

* el punto final de autenticación
   * el punto final proporcionará el código de autorización que se utilizará más adelante a cambio del token de actualización y acceso
* el punto final /token
   * esto proporcionará el token de actualización y el token de acceso
   * el token de actualización debe ser estable (no debe cambiar cada vez que solicitamos un nuevo token de acceso)
   * el MVPD necesita permitir varios tokens de acceso activos para cada token de actualización
   * este punto final también intercambiará un token de actualización por un token de acceso
* necesitamos un **punto final para el perfil de usuario**
   * este punto final proporcionará el userID, que debe ser único para una cuenta y no debe contener información de identificación personal
* el **/logout** extremo (opcional)
   * La autenticación de Adobe Primetime redireccionará a este punto final, proporcionará al MVPD un URI de redirección hacia atrás; en este punto final, el MVPD puede borrar las cookies en el equipo cliente o aplicar cualquier lógica deseada para cerrar la sesión
* se recomienda especialmente tener compatibilidad con clientes autorizados (aplicaciones cliente que no déclencheur una página de autorización de usuario)
* también necesitamos:
   * **clientID** y **secreto de cliente** para las configuraciones de integración
   * **tiempo de vida** Valores (TTL) para el token de actualización y el token de acceso
   * Podemos proporcionar al MVPD un URI de devolución de llamada y cierre de sesión de Autorización. Además, si es necesario, podemos proporcionar a los MVPD una lista de IP que se incluirán en la lista de direcciones permitidas en la configuración del cortafuegos.


## Flujo de autenticación {#authn-flow}

En el flujo de autenticación, la autenticación de Adobe Primetime se comunica con el MVPD en el protocolo seleccionado en la configuración. El flujo de OAuth 2.0 se muestra en la siguiente imagen:



![Diagrama para mostrar el flujo de autenticación en la autenticación de Adobe que se comunica con el MVPD en el protocolo seleccionado en la configuración.](assets/authn-flow.png)

**Figura 1: Flujo de autenticación de OAuth 2.0**



## Solicitud y respuesta de autenticación {#authn-req-response}

En pocas palabras, el flujo de autenticación para los MVPD que admiten el protocolo OAuth 2.0 sigue estos pasos:

1. El usuario final navega al sitio del programador y selecciona iniciar sesión con sus credenciales de MVPD
1. AccessEnabler instalado en el lado del programador con envía una solicitud de autenticación en forma de solicitud HTTP al extremo de autenticación de Adobe Primetime, que el extremo de autenticación de Adobe Primetime redirige al extremo de autorización de MVPD.
1. El extremo de autorización de MVPD envía un código de autorización al extremo de autenticación de Adobe Primetime
1. La autenticación de Adobe Primetime utiliza el código de autorización recibido para solicitar un token de actualización y un token de acceso del extremo token de MVPD
1. Se puede enviar una llamada para recuperar información de usuario y metadatos al extremo del perfil del usuario en caso de que la información del usuario no se incluya en el token
1. El token de autenticación se pasa al usuario final que ahora puede examinar correctamente el sitio del programador

   >[!NOTE]
   >
   >El token de actualización se utiliza para obtener un nuevo token de acceso después de que el token de acceso actual no sea válido o caduque.


>[!IMPORTANT]
>
>El token de actualización no debe cambiar cuando se intercambia por un token de acceso.

Esta limitación se debe a los flujos de cliente que no permiten al servidor actualizar la autenticación AuthNToken que, para el protocolo OAuth 2.0, también contiene el token de actualización.

Un flujo de autorización típico realiza un intercambio del token de actualización guardado en AuthNToken para un token de acceso que posteriormente se utiliza para realizar la llamada de autorización en nombre del usuario que se autenticó en primer lugar. Si el Servidor de autorización (MVPD) cambiara el token de actualización e invalidara el antiguo, no podremos actualizar el AuthNToken válido. Por este motivo, los MVPD necesitan admitir tokens de actualización estables para poder configurar integraciones de OAuth 2.0 para ellos.


## Migración de SAML a OAuth 2.0 {#saml-auth2-migr}

La migración de integraciones de SAML a OAuth 2.0 la realizarán Adobe y el MVPD. No hay necesidad de ningún cambio técnico en el lado del programador, aunque el programador podría querer comprobar/probar la promoción conjunta de marca en la página de inicio de sesión de MVPD. Desde el punto de vista de la MVPD, se requieren los extremos y otra información solicitada en los requisitos de Oauth 2.0.

Para **conservar SSO**, los usuarios que ya tengan un token de autenticación obtenido mediante SAML se seguirán considerando autenticados y sus solicitudes se enrutarán a través de la antigua integración SAML.

Desde una perspectiva técnica:

1. Adobe permitirá una integración OAuth 2.0 entre el programador y el MVPD, SIN eliminar la integración SAML.
1. Después de la activación, todos los usuarios nuevos utilizarán los flujos de OAuth 2.0.
1. Los usuarios ya autenticados, que ya tienen un token AuthN local que contiene el subject-id de SAML, se enrutarán automáticamente mediante Adobe a través de la integración SAML.
1. Para los usuarios del paso 3, una vez que su token AuthN generado por SAML expira, el Adobe los tratará como nuevos usuarios y se comportará como los usuarios en el paso 2.
1. Adobe revisará los patrones de uso para determinar el momento en el que la integración SAML se puede desactivar de forma segura.

