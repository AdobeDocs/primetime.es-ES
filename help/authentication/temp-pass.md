---
title: Pase temporal
description: Pase temporal
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2210'
ht-degree: 0%

---


# Pase temporal {#temp-pass}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Resumen de características {#tempass-featur-summary}

Temp Pass permite a los programadores ofrecer acceso temporal a su contenido protegido, para los usuarios que no tengan credenciales de cuenta con un MVPD.  Temp Pass incluye las siguientes capacidades:

* Temp Pass se puede configurar para proporcionar acceso temporal para cubrir una variedad de escenarios, incluyendo los siguientes:
   * Un programador puede ofrecer una vista previa diaria y corta (por ejemplo, de 10 minutos) de uno de sus sitios.
   * Un programador puede ofrecer una sola y larga presentación (por ejemplo, cuatro horas) de un gran evento deportivo como los Juegos Olímpicos, o la locura de la Marcha de la NCAA.
   * Un programador puede proporcionar una combinación de los dos escenarios anteriores; por ejemplo, un período de visualización inicial más largo un día, seguido de una serie de períodos breves que se repiten diariamente durante algunos días posteriores.
* Los programadores especifican la duración (tiempo de vida o TTL) de su paso temporal.
* El paso temporal funciona por solicitante.  Por ejemplo, NBC podría configurar un Pase temporal de 4 horas para el solicitante &quot;NBCOlympics&quot;.
* Los programadores pueden restablecer todos los tokens otorgados a un solicitante en particular.  El &quot;MVPD temporal&quot; utilizado para implementar el Pase temporal debe configurarse con &quot;Autenticación por solicitante&quot; habilitado.
* **El acceso a Temp Pass se concede a usuarios individuales en dispositivos específicos**. Una vez que el acceso a Temp Pass expira para un usuario, este no podrá obtener acceso temporal en el mismo dispositivo hasta que el usuario caduque [token de autorización](/help/authentication/glossary.md#authz-token) se borra del servidor de autenticación de Adobe Primetime.


>[!NOTE]
>
>Temp Pass forma parte del paquete Premium Workflow . Póngase en contacto con su representante de ventas de Primetime si le interesa utilizar esta funcionalidad.

## Detalles de las funciones {#tempass-featur-details}

* **Cálculo del tiempo de visualización** - La cantidad de tiempo que un pase temporal sigue siendo válido no se correlaciona con la cantidad de tiempo que un usuario pasa viendo contenido en la aplicación del programador.  Tras la solicitud inicial de autorización del usuario mediante Temp Pass, se calcula el tiempo de caducidad añadiendo el tiempo de solicitud inicial actual al TTL especificado por el Programador. Esta hora de caducidad está asociada al ID de dispositivo del usuario y al ID de solicitante del programador, y se almacena en la base de datos de autenticación de Primetime. Cada vez que el usuario intenta acceder al contenido utilizando Temp Pass desde el mismo dispositivo, la autenticación de Primetime compara la hora de solicitud del servidor con la hora de caducidad asociada con el ID del dispositivo del usuario y el ID del solicitante del programador. Si el tiempo de solicitud del servidor es menor que el tiempo de caducidad, se concede la autorización. de lo contrario, se denegará la autorización.
* **Parámetros de configuración** - Un programador puede especificar los siguientes parámetros de paso temporal para crear una regla de paso temporal:
   * **TTL de token** - La cantidad de tiempo que un usuario puede ver sin iniciar sesión en un MVPD. Esta vez se basa en el reloj y caduca si el usuario está viendo el contenido o no.
   >[!NOTE]
   >Un ID de solicitante no puede tener más de una regla de pase temporal asociada.
* **Autenticación/autorización** - En el flujo de paso temporal, usted especifica el MVPD como &quot;Paso temporal&quot;.  La autenticación de Primetime no se comunica con un MVPD real en el flujo de paso temporal, por lo que el MVPD &quot;Temp Pass&quot; autoriza cualquier recurso. Los programadores pueden especificar un recurso al que se pueda acceder mediante Temp Pass igual que lo hacen para el resto de los recursos de su sitio. La biblioteca del verificador de medios se puede usar de la forma habitual para verificar el token de medios cortos de Temp Pass y hacer cumplir la comprobación de recursos antes de la reproducción.
* **Seguimiento de datos en el flujo de paso temporal** - Dos puntos con respecto al seguimiento de datos durante un flujo de derechos de paso temporal:
   * El ID de seguimiento que se pasa de la autenticación de Primetime a su **sendTrackingData()** callback es un hash del ID del dispositivo.
   * Dado que el ID de MVPD utilizado en el flujo de transferencia temporal es &quot;Temp Pass&quot;, ese mismo ID de MVPD se devuelve a **sendTrackingData()**. Es probable que la mayoría de los programadores deseen tratar las métricas de Temp Pass de forma diferente a las métricas reales de MVPD. Esto requiere un poco de trabajo adicional en la implementación de analytics.

La siguiente ilustración muestra el flujo de paso temporal:

![Flujo de paso temporal](assets/temp-pass-flow.png)

*Figura: Flujo de paso temporal*

## Implementación de pase temporal {#implement-tempass}

En el lado de la autenticación de Primetime, Temp Pass se implementa con la adición de un pseudo-MVPD llamado &quot;TempPass&quot; a la configuración del servidor del programador participante.  Este pseudo-MVPD actúa como un MVPD real que otorga temporalmente acceso al contenido protegido del programador.

Por el lado del programador, Temp Pass se implementa de la siguiente manera para los dos escenarios que utilizan los MVPD para la autenticación:

* **iFrame en la página del programador**. El paso temporal funciona independientemente del tipo de autenticación de un MVPD, pero para el escenario de iFrame se necesitan pasos adicionales para cancelar el flujo de autenticación actual y autenticarse con el paso temporal. Estos pasos se muestran en la sección [Inicio de sesión en iFrame](/help/authentication/temp-pass.md) más abajo.
* **Redirigir a la página de inicio de sesión de MVPD**. En el caso más tradicional, en el que la interfaz de usuario para activar el Pase temporal se presenta antes de iniciar la autenticación con un MVPD, no hay pasos especiales que realizar. El Pase Temp debe tratarse como un MVPD normal.

Los siguientes puntos se aplican a ambos escenarios de implementación:

* El &quot;Pase temporal&quot; debe mostrarse en el selector de MVPD solo para los usuarios que aún no hayan solicitado una autorización de Pase temporal. Para bloquear la visualización de solicitudes posteriores, se puede mantener un indicador en las cookies. Esto funcionará siempre que el usuario no borre la caché del explorador. Si los usuarios borran las cachés del explorador, aparecerá &quot;Paso temporal&quot; de nuevo en el selector y el usuario podrá solicitarlo de nuevo. El acceso solo se concederá si el tiempo &quot;Temp Pass&quot; aún no ha caducado.
* Cuando un usuario solicita acceso a través de Temp Pass, el servidor de autenticación de Primetime no realizará su solicitud habitual de Lenguaje de marcado de aserción de seguridad (SAML) durante el proceso de autenticación. En su lugar, el punto final de autenticación devolverá el éxito cada vez que se invoque mientras los tokens son válidos para el dispositivo.
* Cuando caduca un pase temporal, su usuario ya no se autenticará, ya que en el flujo de paso temporal el token de autenticación y el token de autorización tienen la misma fecha de caducidad. Para explicar a los usuarios que su paso temporal ha caducado, los programadores deben recuperar el MVPD seleccionado justo después de llamar a `setRequestor()`y, a continuación, llame a `checkAuthentication()` como de costumbre. En el `setAuthenticationStatus()` llamada de retorno se puede realizar una comprobación para determinar si el estado de autenticación es 0, de modo que si el MVPD seleccionado era &quot;TempPass&quot;, se pueda presentar a los usuarios un mensaje que indique que su sesión de Temp Pass ha caducado.
* Si un usuario elimina el token de pase temporal antes de la caducidad, las siguientes comprobaciones de derechos generarán un token que tendrá un TTL igual al tiempo restante.
* Si el usuario elimina el token de pase temporal después de la caducidad, las siguientes comprobaciones de derechos devolverán &quot;usuario no autorizado&quot;.

Consulte los ejemplos de [Código de muestra](/help/authentication/temp-pass.md#tempass-sample-code) a continuación para ver ejemplos de cómo codificar los detalles de implementación descritos en esta sección.

## Código de muestra {#tempass-sample-code}

Las secciones siguientes muestran cómo llamar a la API de autenticación de Primetime para implementar el flujo de paso temporal:

* [Ejemplo de inicio de sesión en iFrame](/help/authentication/temp-pass.md#iframe-login-sample)
* [Ejemplo de inicio de sesión automático](/help/authentication/temp-pass.md#auto-login-sample)

### Ejemplo de inicio de sesión en iFrame {#iframe-login-sample}

Este ejemplo muestra cómo implementar Temp Pass para aquellos casos en los que los MVPD admiten la integración iFrame:

```HTML
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
        "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript" src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var ae, ifrm, providersMenu, previousSelectedProvider;
        var tempassSelected = false;
 
        $(document).ready(function() {
            ifrm = $('#ifrm');
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {wmode: "transparent", allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded() {
            ae = $('#accessEnabler')[0];
            ae.setProviderDialogURL("none");
            ae.setRequestor("sample_requestor_Id");
            previousSelectedProvider = ae.getSelectedProvider(); 
            ae.checkAuthentication();
        }
 
        function createIFrame() {
            providersMenu.hide();
 
            // If the user already used TempPass once, hide the button
            if ($.cookie("TPSelected") == "1"){
                $('#tempassBtn').hide();
            }
            ifrm.show();
        }
 
        function displayProviderDialog(providers) {
            if (tempassSelected) {
                // Remember in a cookie that the user selected temp pass
                $.cookie("TPSelected", "1", {expires: 366, path: '/'});
 
                // Authenticate with temp pass
                ae.setSelectedProvider("TempPass");
            } else {
                $('#loginBtn').hide();
                providersMenu = $('<select></select>');
 
                providersMenu.change(function(event){
                    ae.setSelectedProvider(event.target.value);
                });
 
                $.each(providers, function(k, v) {
                    // Add the MVPDs to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if(v.ID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:v.ID}).text(v.displayName));                       
                    }
                });
                $('body').append(providersMenu);
            }
        }
 
        function setAuthenticationStatus(status, code) {
            loginBtn = $('#loginBtn');
            logoutBtn = $('#logoutBtn');
            console.log(previousSelectedProvider);
 
            if (status == 1) {
                $('#selectedProvider').text("Authenticated with " + ae.getSelectedProvider().MVPD + "   ");
                loginBtn.hide();
                logoutBtn.show();
 
                // Get authorization
                ae.getAuthorization("sample_requestor_Id");
            } else {
                // If selected provider is TempPass but the user is not authenticated,
                //   infer that the TempPass period has expired, so reset the MVPD selection
                if (previousSelectedProvider && previousSelectedProvider.MVPD == "TempPass") {
                    previousSelectedProvider = null;
                    ae.setSelectedProvider(null);
                    alert("Your Temp Pass has expired, please login with your regular cable provider!");
                }
                loginBtn.show();
                logoutBtn.hide();
            }
        }
 
        function selectTempPass() {
            ifrm.hide();
 
            // Signal the fact that the user selected temp pass
            tempassSelected = true;
 
            // Cancel the current authentication flow
            ae.setSelectedProvider(null);
 
            // Retry authentication
            ae.getAuthentication();
 
        }
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="ae.getAuthentication();">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
           style="display: none" onclick="ae.logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px; width: 400px; height: 400px; border: 2px solid red;">
        <button id="tempassBtn"
           onclick="selectTempPass();"
             style="float:left">Don't know your credentials? Click here to get a Temp Pass.
        </button>
        <button onclick="window.location.reload()" style="float:right">X</button>
        <br />
        <hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="90%" height="90%" frameborder="0"></iframe>
    </div>
    <br/>
    <div id="ae" style="display: none">
        <p>Loading Access Enabler...</p>
    </div>
</body>
</html>
```

#### Casos de uso de inicio de sesión en iFrame {#iframe-login-use-cases}

**Para solicitar un Pase temporal por primera vez:**

1. Un usuario accede a la página Programador y hace clic en el vínculo de inicio de sesión.
1. Se abre el selector de MVPD y el usuario elige un MVPD de la lista.
1. Se muestra el iFrame de autenticación. Este iFrame contiene un vínculo &quot;Temp Pass&quot;.
1. El usuario hace clic en &quot;Paso temporal&quot;, por lo que el programador agrega un indicador a una cookie para evitar que el usuario vea el vínculo &quot;Paso temporal&quot; en las visitas posteriores a la página.
1. La solicitud de autenticación de paso temporal llega a los servidores de autenticación de Primetime y genera un token de autenticación. El TTL es igual al periodo de tiempo establecido por el programador para el paso temporal.
1. La solicitud de autorización de Temp Pass llega a los servidores de autenticación de Primetime.
1. Los servidores de autenticación de Primetime extraen los ID de dispositivo y solicitante de la solicitud y los almacenan en la base de datos junto con la hora de caducidad. El tiempo de caducidad se calcula como: tiempo inicial de solicitud de paso temporal más el TTL (especificado por el programador).
1. Los servidores de autenticación de Primetime generan un token de autorización.
1. El usuario accede al contenido protegido.

**Para solicitar de nuevo un paso temporal después de que un usuario de Temp Pass que regresa haya eliminado las cookies del explorador:**

1. El usuario accede a la página Programador y hace clic en el vínculo de inicio de sesión.
1. Se abre el selector de MVPD y el usuario elige un MVPD de la lista.
1. Se muestra el iFrame de autenticación. Este iFrame contiene un vínculo &quot;Temp Pass&quot; (el usuario borró la cookie original, por lo que el programador no sabe si el usuario ha hecho clic anteriormente en el vínculo &quot;Temp Pass&quot;).
1. El usuario vuelve a hacer clic en &quot;Pase temporal&quot;, por lo que el programador agrega una marca a una cookie de nuevo para evitar que el usuario vea el vínculo &quot;Pase temporal&quot; en las visitas posteriores a la página.
1. La solicitud de autenticación de paso temporal llega a los servidores de autenticación de Primetime, que generan un token de autenticación. El TTL es ahora el tiempo restante para la Pase temporal (la diferencia entre la hora actual y la hora de caducidad asociada al ID del dispositivo).
1. La solicitud de autorización de Temp Pass llega a los servidores de autenticación de Primetime.
1. Los servidores de autenticación de Primetime extraen los ID de dispositivo y solicitante de la solicitud y los utilizan para recuperar la hora de caducidad de la base de datos de autenticación de Primetime. La hora actual se compara con la hora de caducidad.
1. Si el paso temporal del usuario no ha caducado, los servidores de autenticación de Primetime generarán un token de autorización.
1. Si el paso temporal del usuario no ha caducado, el usuario podrá acceder al contenido protegido.

### Ejemplo de inicio de sesión automático {#auto-login-sample}

El siguiente ejemplo ilustra un caso en el que un usuario ha iniciado sesión automáticamente con TempPass al visitar un sitio. El usuario puede elegir iniciar sesión con un MVPD normal en cualquier momento y se le advierte si TempPass ha caducado:

```HTML
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript"
             src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript"
             src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript"
             src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var REQUESTOR = "REF";
        var RESOURCE = "sample_requestor_Id";
        var selectedProvider = null;
        var mvpds;
        var hasTempPassMVPD = false;
 
        // Used to cache the mvpd picker
        var picker;
 
        $(document).ready(function() {
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded(){
            console.log("AccessEnabler loaded");
            ae = $('#accessEnabler')[0];
 
            // Make sure the default picker is disabled
            ae.setProviderDialogURL("none");
 
            ae.setRequestor(REQUESTOR);
            ae.checkAuthentication();
        }
 
        /**
         * Callback received as a result of setRequestor()
         *
         * @param xml object holding the configuration for the current REQUESTOR
         * including the MVPD list
         */
        function setConfig(config) {
            // Save the mvpd list
            var mvpdList = $.parseXML(config);
            mvpds = $(mvpdList).find('mvpd');
 
            // Create the picker only once and cache it
            if(!picker) {
                picker = $('<div id="mvpdPicker"/>');
 
                var providersMenu = $('<select id="mvpdList" multiple></select>');
 
                $.each(mvpds, function(k, v) {
                    var mvpdID = $(v).find("id").text();
                    var mvpdName = $(v).find("displayName").text();
 
                    // Add the mvpd's to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if (mvpdID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:mvpdID}).text(mvpdName));
                    } else {
                        hasTempPassMVPD = true;
                    }
                });
                picker.append(providersMenu);
                picker.append($('<br/>'));
                picker.append($('<input type="button" onclick="login()" value="login" />'));
                picker.append($('<input type="button" onclick="cancelPicker()" value="cancel" />'));                  
            }
 
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");             
            }
        }
 
        /**
         * Callback triggered for iFramed MVPD's
         */
        function createIFrame() {
            $('#mvpdPicker').remove();
            $('#ifrm').show();
        }
 
        /**
         * Hides the MVPD picker
         * when the user clicks "Cancel"
         */
        function cancelPicker() {
            $('#video').show();
            $('#mvpdPicker').remove();
            $('#loginBtn').show();
        }
 
        /**
         * Pops up the MVPD picker
         */
        function showPicker() {
            $('#video').hide();
            $('#loginBtn').hide();
            $('body').append(picker);
        }
 
        function logout() {
            $.removeCookie('tempPassUsed');
            ae.logout();
        }
 
        /**
         * Performs login with the selected MVPD
         */
        function login() {
            selectedProvider = $('#mvpdList').val()[0];
 
            // Make sure we clear out previously
            // selected. This is a must if we want to force
            // login with a real MVPD while still logged in with
            // TempPass, without doing an ae.logout()
            ae.setSelectedProvider(null);
            ae.getAuthentication();
        }

        /**
         * Callback triggered by AccessEnabler. This is usually
         * triggered in order to display the MVPD picker, but
         * since we already constructed, cached, and displayed the
         * picker, and the user already picked the MVPD, we don't need
         * to do anything here but state management
         */
        function displayProviderDialog() {
            // If the selected MVPD is TempPass
            // store this fact in a cookie,
            // otherwise clear it
            if (selectedProvider != 'TempPass') {
                $.removeCookie('tempPassUsed');
            } else {
                $.cookie("tempPassUsed", 1);
            }
 
            // Since the picker was already shown
            // and the user picked an MVPD,
            // just proceed to login
            ae.setSelectedProvider(selectedProvider);
        }
 
        function setAuthenticationStatus(status, code) {
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");
            } else if(status == 1) {
                selectedProvider = ae.getSelectedProvider().MVPD;
                $('#selectedProvider').text("Authenticated with " + selectedProvider + "   ");
 
                // If authenticated with TempPass
                // allow the user to login with
                // a real MVPD
                if (selectedProvider == "TempPass") {
                    $('#loginBtn').show();
                    $('#logoutBtn').hide();
                } else {
                    $('#loginBtn').hide();
                    $('#logoutBtn').show();
                }
 
                // Get authorization
                // Note: This is mandatory in order to "start" the temp pass countdown
                ae.checkAuthorization(RESOURCE);
            } else if(code != "Provider not Selected Error") {
                // Auto-authenticate with TempPass only if we infer
                // that TempPass has not expired, otherwise we
                // inform the user that TempPass has expired
                if ($.cookie('tempPassUsed') == 1) {
                   $('#selectedProvider').text("Your Temp Pass has expired, please log in with your cable provider!");
                   $('#logoutBtn').show();
                   showPicker();
                } else {
                    selectedProvider = 'TempPass';
                    ae.getAuthentication();
                }
            }
        }
 
        /**
         * Displays the picker as a result
         * of user action
         */
        function loginClicked() {
            $('#loginBtn').hide();
            showPicker();
        }
 
        /**
         * Callback triggered in case of authorization success
         */
        function setToken(token) {
            console.log(token);
            $('#video').html('<img src=">');
        }
 
        /**
         * Callback triggered in case of authz failure
         */
        function tokenRequestFailed(resource, status, message) {
            console.log(resource);
            $('#video').html('<p style="color: red">' + status + ': ' + message + '</p>');
        }
 
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="loginClicked()">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
        style="display: none" onclick="logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px;
         width: 400px; height: 400px; border: 2px solid red;">
        <button onclick="window.location.reload()" style="float:right">Close this window</button>
        <br /><hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="80%" height="80%" frameborder="0"></iframe>  
    </div>
    <br/>
 
    <div id="video"></div>
    <div id="ae" style="display: none"><p>Loading Access Enabler...</p></div>
</body>
</html>
```

## Usar varias pasadas temporales {#use-mult-tempass}

Algunos eventos requieren acceso libre por fases al contenido, como un intervalo inicial de acceso libre (por ejemplo, 4 horas), seguido de accesos gratuitos diarios (por ejemplo, 10 minutos cada día siguiente).  Para que un programador implemente este escenario, debe organizarlo con su contacto de Adobe para configurar dos MVPD temporales para el programador.

Para este escenario de ejemplo (una sesión gratuita inicial de 4 horas, seguida de sesiones gratuitas diarias de 10 minutos), el Adobe configura un MVPD llamado TempPass1 con un tiempo de vida (TTL) de 4 horas y un TempPass2 con un TTL de 10 minutos para el periodo siguiente.  Ambos están asociados con el ID de solicitante del programador.

### Implementación del programador {#mult-tempass-prog-impl}

Después de que el Adobe configure las dos instancias de TempPass, los dos MVPD adicionales (TempPass1 y TempPass2) aparecerán en la lista MVPD del programador.  El programador debe realizar los siguientes pasos para implementar los pases temporales múltiples:

1. En la visita inicial del usuario al sitio, inicie sesión automáticamente con TempPass1. Puede utilizar el ejemplo de autenticación anterior como punto de partida para esta tarea.
1. Cuando detecte que TempPass1 ha caducado, almacene el hecho (en una cookie/almacenamiento local) y presente al usuario su selector MVPD estándar. **Asegúrese de filtrar TempPass1 y TempPass2 de esa lista**.
1. En cada día siguiente, si TempPass1 ha caducado, inicie sesión en ese usuario con TempPass2.
1. Cuando TempPass2 haya caducado, almacene el hecho (en una cookie/almacenamiento local) durante el día y presente al usuario su selector MVPD estándar. De nuevo, asegúrese de filtrar TempPass1 y TempPass2 de esa lista.
1. En cada nuevo día, a las 00:00 horas, restablezca todos los pases temporales para TempPass2, utilizando la variable [Restablecer la API web de TempPass](/help/authentication/temp-pass.md#reset-all-tempass).

>[!NOTE]
>**Nota de programación:** La autenticación de Primetime no tiene un mecanismo integrado para detener la transmisión gratuita una vez transcurridos los 10 minutos.  Depende de los programadores restringir el acceso una vez que TempPass2 caduque. Para lograr esto, los programadores pueden implementar en sus sitios/aplicaciones una llamada &quot;checkAuthorization&quot; cada X minutos, donde X es el periodo de tiempo que el programador determina que tiene sentido para sus aplicaciones.

## Restablecer todas las pasadas temporales {#reset-all-tempass}

Algunas reglas comerciales requieren la depuración regular de la Pase temporal o un restablecimiento ad hoc de todas las Pases temporales emitidas para un ID de solicitante e ID de MVPD en particular. Esta función admite casos de uso como los siguientes:

* Un Pase temporal diario de 10 minutos (el Pase temporal debe restablecerse al comienzo del día)
* Pase temporal disponible para todos los usuarios durante las noticias de último minuto. (El paso temporal debe restablecerse para todos los dispositivos en cuanto se inicie la noticia de último minuto).
* El escenario de varias pasadas temporales que proporciona una combinación de un periodo de visualización inicial de cierta longitud, seguido de periodos diarios subsiguientes de otra longitud.

Para restablecer todas las pasadas temporales, la autenticación de Primetime proporciona a los programadores un *public* API web:

```url
DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset
```

>[!NOTE]
>La URL anterior sustituye a la API de restablecimiento anterior. Ya no se admite la API de restablecimiento anterior (v1).

* **Protocolo:** HTTPS
* **Host:**
   * Versión: mgmt.auth.adobe.com
   * Prequal: mgmt-prequal.auth.adobe.com
* **Ruta:** /reset-tempass/v2/reset
* **Parámetros de consulta:** `device_id=all&requestor_id=REQUESTOR_ID&mvpd_id=TEMPPASS_MVPD_ID`
* **Encabezados:** ApiKey - 1232293681726481
* **Respuesta:**
   * Correcto - HTTP 204
   * Error:
      * HTTP 400 para una solicitud incorrecta
      * HTTP 401 si ApiKey no se especificó
      * HTTP 403 si ApiKey no es válido

Por ejemplo:

```curl
$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=all&requestor_id=AdobeBEAST&mvpd_id=TempPass"
```

## Clientes admitidos {#supp-clients}

Compatibilidad con la herramienta Temp Pass y Reset por plataforma:

| Clientes de autenticación de Adobe Primetime | Pase temporal | Herramienta Restablecer |
|:--------------------------------------:|:---------:|:----------:|
| JS AccessEnabler | SÍ | SÍ |
| iOS de cliente nativo | SÍ | SÍ |
| Cliente nativo tvOS | SÍ | SÍ |
| Android de cliente nativo | SÍ | SÍ |
| FireTV de cliente nativo | SÍ | SÍ |
| API sin cliente | SÍ | SÍ |

## Limitaciones y problemas conocidos {#limitations}

Esta sección describe las limitaciones que se aplican a la implementación actual de Temp Pass.

**SDK de JavaScript**: admite restablecer la funcionalidad de pasar temporal desde la versión **3.X y posterior**.

<!--For Customers migrating from the 2.X JavaScript AccessEnabler to the 3.X JavaScript AccessEnabler, see [AccessEnabler JS 2.x to JS 3.x migration guide](https://tve.helpdocsonline.com/accessenabler-js-to-js-migration-guide).-->