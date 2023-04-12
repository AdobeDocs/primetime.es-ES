---
title: Información general del SDK de JavaScript
description: Información general del SDK de JavaScript
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# Información general del SDK de JavaScript {#javascript-sdk-overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción

Adobe recomienda encarecidamente migrar al último JS v4.x de la biblioteca AccessEnabler.

La integración de JavaScript de autenticación de Adobe Primetime ofrece a los programadores una solución de TV en todas partes en el entorno familiar de desarrollo de aplicaciones web JS. Los componentes principales de la integración son su aplicación de &quot;alto nivel&quot; (interacción del usuario, presentación de vídeo) y la biblioteca AccessEnabler de &quot;bajo nivel&quot; proporcionada por el Adobe que proporciona su entrada a los flujos de derechos y gestiona la comunicación con los servidores de autenticación de Adobe Primetime.

El flujo general de derechos de autenticación de Adobe Primetime se cubre en [Flujo de derechos del programador](/help/authentication/entitlement-flow.md)y la Guía de integración de JavaScript lo acompaña durante la implementación. Las secciones siguientes proporcionan descripciones y muestras específicas de la integración de AccessEnabler de JavaScript.

>[!IMPORTANT]
>
>Este documento describe la implementación para una solución web de escritorio. La biblioteca JavaScript no es compatible con plataformas móviles (por ejemplo, Safari en iOS, Chrome en Android). Utilice nuestros SDK nativos si desea segmentar una plataforma móvil (iOS, Android, Windows).

## Creación del cuadro de diálogo Selección de MVPD {#creating-the-mvpd-selection-dialog}

Para que un usuario inicie sesión en su MVPD y se autentique, su página o reproductor debe proporcionar una forma para que el usuario identifique su MVPD. Se proporciona una versión predeterminada de un cuadro de diálogo de selección de MVPD para el desarrollo. Para su uso en producción, debe implementar su propio selector de MVPD. 

Si ya sabe quién es el proveedor del cliente, puede [configurar el MVPD mediante programación](/help/authentication/home.md), sin interacción del usuario. La técnica es la misma, pero evita el paso de invocar el cuadro de diálogo Selector de proveedor y pedir al cliente que seleccione su MVPD.

## Visualización del proveedor de servicios {#displaying-the-service-provider}

El siguiente ejemplo de código muestra cómo descubrir y mostrar el proveedor de servicios para el cliente actual:

 **HTML** - Esta página agrega una sección a la página que muestra el proveedor elegido por el cliente, si ya ha iniciado sesión:

```HTML
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
            "http://www.w3.org/TR/html4/loose.dtd"> 
    <html>
    <head>
        <title>Get the distributor that is used for the authentication</title>
        <script type="text/javascript" src="libs/jquery-1.4.4.min.js"></script>
        <script type="text/javascript" src="libs/swfobject.js"></script>
        <script type="text/javascript" src="scripts/sample6.js"></script>
    </head>
    <body>
        <div id="alternative">
        <a href="http://www.adobe.com/go/getflashplayer"> 
            <img src="http://www.adobe.com/images/shared/download_buttons/get_flash_player.gif" 
                 alt="Get Adobe Flash player"/> </a>
        </div> 
        <div id="user_authenticated">Please wait while we verify your authentication status</div> 
        <div id="control">
        <button id="sign_in" style="display:none;">Sign in</button>
        <button id="sign_out" style="display:none;">Sign out</button>
        </div> 
        <div id="distributor"></div> 
        <div id="provider_selector" style="display:none;">
        <select id="provider_list"></select>
        <button id="login">Login</button>
        <button id="cancel">Cancel</button>
        </div> 
        <div id="video_player">This is a video player showing an image as a preview.  You are not yet authorized to see this content.  Make sure that you first sign in.
        </div> 
        <div id="get_authorization">
        <button id="request_access" style="display:none;">Request access</button>
        </div> 
    </body>
    </html>
```
 

**JavaScript** Este archivo JavaScript consulta Access Enabler para el proveedor actual si el usuario ya ha iniciado sesión y muestra el resultado en la sección de página reservada para él. También implementa un cuadro de diálogo de selector de MVPD:

```JS
    $(function() {
        embedAE();
    }); 
    function embedAE() {
        var flashvars = {};
        var params = {
            bgcolor: "#869ca7",
            quality: "high",
            allowscriptaccess: "always"
        };
        var attributes = {
            id: "ae_swf",
            align: "middle",
            name: "ae_swf"
        };
        swfobject.embedSWF(
                "https://entitlement.auth-staging.adobe.com/entitlement/AccessEnabler.swf",      
                "alternative", "1", "1", "10.1.53", "", flashvars, params, attributes);
    } 
    function getAE() {
        return document.getElementById("ae_swf");
    } 
    function swfLoaded() {
        var swf = getAE();
        initBindings();
        // don't load the default provider-selection dialog 
        swf.setProviderDialogURL("none");
        // identify yourself 
        swf.setRequestor("sample_requestor_Id");
        swf.checkAuthentication();
    } 
    // Define the button actions for the provider dialog
    function initBindings() {
        var provider_selector = $('#provider_selector');
        var sign_in = $('#sign_in');
        var sign_out = $('#sign_out');
        var login = $('#login');
        var cancel = $('#cancel');
        var request_access = $('#request_access'); 
        sign_out.click(function() {
            getAE().logout();
        });
        sign_in.click(function() {
            getAE().getAuthentication();
        }); 
        login.click(function() {
            var selected_mvpd_id = $("#provider_list option:selected").val();
            getAE().setSelectedProvider(selected_mvpd_id);
        }); 
        cancel.click(function() {
            getAE().setSelectedProvider(null);
            provider_selector.hide();
        }); 
        request_access.click(function(){
            getAE().getAuthorization("sample_requestor_Id");
        });
    }
    // Called if user is already authenticated; queries AE to find the current user's MVPD, 
    // Adds the result to the UI 
    function setDistributor() {
        var distributor = $("#distributor");
        var selectedProvider = getAE().getSelectedProvider();
        distributor.replaceWith('<div id="distributor">' +
                                'Courtesy of ' +
                                selectedProvider.MVPD +
                                '</div>');
    } 
    // Adjust the contents of the provider dialog, based on authentication status 
    // Adds the call to check and display the current distributor, if the user is already
    // logged in. 
    function setAuthenticationStatus(isAuthenticated, errorCode) {
        var user_authenticated = $("#user_authenticated");
        var video_player = $("#video_player");
        var sign_in = $('#sign_in');
        var sign_out = $('#sign_out');
        var request_access = $('#request_access'); 
        if (isAuthenticated == 1) {
            setDistributor();
            user_authenticated.replaceWith('<div id="user_authenticated">
                                           You are authenticated - if you wish you can sign out
                                           </div>');
            sign_out.show();
            sign_in.hide();
            video_player.replaceWith('<div id="video_player">Now you can ask for access.</div>');
            request_access.show();
        } else {
            user_authenticated.replaceWith('<div id="user_authenticated">
                                           You are not authenticated please sign in
                                           </div>');
            sign_in.show();
            sign_out.hide();
        }
    } 
    // Allow user to choose a provider 
    function displayProviderDialog(providers) {
        var provider_list = $("#provider_list");
        var options = provider_list.attr('options');
        for (var index in providers) {
            options[index] = new Option(providers[index].displayName,
                                        providers[index].ID);
        }
        //select the first one by default 
        if (!$("#provider_list option:selected").length)
            $("#provider_list option[0]").attr('selected', 'selected'); 
        $('#provider_selector').show();
    } 
    // Handle the authorization response by sending token to video player 
    function setToken(requested_resource_id, token) {
        var video_player = $("#video_player");
        var request_access = $("#request_access");
        video_player.replaceWith('<div id="video_player">Now you are authorized to ' +
                                 requested_resource_id +
                                 ' content with ' + token + ' . </div>');
    }
```

## Cerrar sesión {#logout}

La llamada `logout()` para iniciar el proceso de cierre de sesión. Este método no tiene argumentos. cierra la sesión del usuario actual, borra toda la información de autenticación y autorización de ese usuario y elimina todos los tokens de AuthN y AuthZ del sistema local.

Hay algunos casos en los que el reproductor no es responsable de administrar los inicios de sesión de los usuarios:

 

- **Cuando se inicia el cierre de sesión desde un sitio que no está integrado con la autenticación de Adobe Primetime.** En este caso, el MVPD puede invocar el servicio de autenticación de Adobe Primetime Single Logout a través de un redireccionamiento del explorador. (Actualmente no se admite la invocación de SLO mediante una llamada en segundo plano).

>[!NOTE]
>
>Si el usuario deja el equipo inactivo el tiempo suficiente para que sus tokens caduquen, puede volver a su sesión e iniciar sesión correctamente. La autenticación de Adobe Primetime garantiza que todos los tokens se eliminen y notifica al MVPD que también debe eliminar su sesión.

El siguiente código JavaScript muestra el cierre de sesión (desautenticación) de un usuario autenticado actualmente:

```JS
    [...]
    /*
     * @param isAuthenticated authentication status: 1 - Authenticated, 0 - not authenticated 
     * @param errorCode Any error that occurred when determining the authentication status.
     * An empty string if no error occurred.
     */
    function setAuthenticationStatus(isAuthenticated, errorCode) {
        if (isAuthenticated == 1 ) {
            /* User is authenticated – we can logout / deauthenticate */
            accessEnablerObject.logout();
            /* Logs out the current user, clearing all authentication
             * and authorization information for that user. Deletes
             * all authN and authZ tokens from the user's system.
             */
        } else {
            /*
             * User is NOT authenticated – we do not need to logout;
             * Show the log-in image/button/message
             */
        }
    }
```

<!--
**Related Information**

- [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
- [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
- [JavaScript Code Samples](#javascript-code-samples)
- [Understanding Tokens](#understanding_tokens)
-->