---
title: Cómo probar los flujos de autenticación y autorización mediante el sitio de prueba de la API de Adobe
description: Cómo probar los flujos de autenticación y autorización mediante el sitio de prueba de la API de Adobe
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# Cómo probar los flujos de autenticación y autorización mediante el sitio de prueba de la API de Adobe {#How-to-test-auth-flows}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

Para probar los flujos AuthN y AuthZ, hemos preparado un **Sitio de prueba de API** que está a su disposición. Nuestro equipo de asistencia estará encantado de proporcionarle credenciales. Puede ponerse en contacto con nosotros en **support@tve.zendesk.com**.


## Parte I {#part-I}

Para realizar pruebas con el entorno RELEASE, vaya directamente a la parte II.  Para realizar pruebas en el entorno de precalificación, consulte [Configuración del entorno y pruebas en Pre-Qual](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

## Parte II

Después de completar la parte I, siga los siguientes pasos:


1. Abra la página web: [Prueba de API de ensayo](https://sp.auth-staging.adobe.com/apitest/api.html).
1. Cargue el activador de acceso desde la siguiente URL:
   * [Javascript del activador de acceso para ensayo](https://entitlement.auth-staging.adobe.com/entitlement/js/AccessEnabler.js).
   * O
   * [Javascript del activador de acceso para producción](https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js).
   * A CONTINUACIÓN, haga clic en el &quot;**Activador de acceso de carga**&quot;.
1. Ahora establezca el valor de id del solicitante en &quot;**requestorID**&quot; y haga clic en el botón &quot;setRequestor&quot;.
1. Después, pulse el botón &quot;getAuthentication&quot; y espere a que aparezca el selector de pantalla.
1. Seleccione el **MVPD**&quot; del selector.
1. Escriba sus credenciales en el &quot;**MVPD**&quot; página de inicio de sesión.
1. Después de redirigirse hacia atrás, rehaga los pasos del 1 al 3
1. Después de rehacer el paso 3 en &quot;setAuthenticationStatus&quot;, debería ver el valor &quot;1&quot;. Si la autenticación no funciona, se mostrará el cuadro de diálogo MVPD.
1. Para probar la autorización, en el campo de entrada de recursos introduzca &quot;**requestorID**&quot; y haga clic en el botón &quot;getAuthorization&quot;.
1. Como resultado, en el cuadro de texto &quot;setToken&quot;-\>&quot;id de recurso&quot; se mostrará el recurso y en el cuadro de texto &quot;setToken&quot;-\>&quot;token&quot; se mostrará shortAuthorizationToken, lo que significa que authZ se ha realizado correctamente.
1. Ahora puede hacer clic en el botón &quot;cerrar sesión&quot; para eliminar los tokens.

