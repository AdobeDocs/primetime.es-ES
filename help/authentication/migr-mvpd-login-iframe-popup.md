---
title: Cómo migrar la página de inicio de sesión de MVPD de iFrame a Elemento emergente
description: Cómo migrar la página de inicio de sesión de MVPD de iFrame a Elemento emergente
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# Cómo migrar la página de inicio de sesión de MVPD de iFrame a Elemento emergente {#migr-mvpd-login-iframe-popup}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Elemento emergente frente a iFrame {#popup-vs-iframe}

Algunos usuarios han encontrado problemas con cookies de terceros con la implementación de iFrame de una página de inicio de sesión de MVPD.
<!--These issues are described in the tech notes linked below:

* [Adobe Primetime authentication and Safari login issues](https://tve.helpdocsonline.com/adobe-pass)
* [MVPD iFrame login and 3rd party cookies](https://tve.helpdocsonline.com/mvpd)-->

El equipo de autenticación de Adobe Primetime **recomienda implementar la página de inicio de sesión emergente / nueva ventana** en lugar de la versión de iFrame en Firefox y Safari.  Sin embargo, si va a implementar una página de inicio de sesión para Internet Explorer, puede encontrar problemas con la implementación emergente. Los problemas de IE se deben al hecho de que, después de que el usuario se autentica con su MVPD en la ventana emergente, la autenticación de Adobe Primetime fuerza un redireccionamiento de página principal, que Internet Explorer ve como un bloqueador emergente. El equipo de autenticación de Adobe Primetime **recomienda implementar el inicio de sesión en iFrame para Internet Explorer**.

El código de ejemplo presentado en esta nota técnica utiliza una implementación híbrida tanto de iFrame como de la ventana emergente: se abre un iFrame en Internet Explorer y se muestra una ventana emergente en los demás navegadores.

Teniendo en cuenta que ya existe una implementación de iFrame, la primera parte de la nota técnica presenta el código para la implementación de iFrame y la segunda parte presenta los cambios para dar cabida a la implementación emergente como predeterminada.


## Selector de MVPD con página de inicio de sesión en un iFrame {#mvpd-pickr-iframe}

Los ejemplos de código anterior mostraban una página de HTML que contenía la variable &lt;div> etiqueta donde se creará el iFrame junto con el botón cerrar iFrame:

```HTML
<body> 
    <div id="mvpddiv">
        <div style="background: red">
            <input type="button" id="btnCloseIframe" value="X" onclick="closeIframeAction();">
        </div>
        <br/>
        <!-- We use the "about:blank" value so that when the iFrame loads
             we do not see the the parent page. -->
        <iframe id="mvpdframe" name="mvpdframe" src="about:blank"></iframe>
    </div> 
</body>
```

Aquí está el asociado **JavaScript** código:

```JavaScript
/*
 * Callback indicating that the AccessEnabler swf has initialized
 */
function swfLoaded() {
    // AccessEnabler is loaded so we can use the API function it provides
    accessEnablerObject.setRequestor(requestorID); 
    accessEnablerObject.checkAuthentication();
} 
/*
* The code the correctly closes the opened IFrame and does not leave the
* AccessEnabler in an undefined state.
*/
function closeIframeAction () {
    accessEnablerObject.setSelectedProvider(null);
    /* We use the "about:blank" value so that when the iFrame loads
     * we do not see the the previous MVPD.
     */
    document.getElementById('mvpdframe').src="about:blank";
    document.getElementById('mvpddiv').style.visibility="hidden";
    document.getElementById('mvpddiv').style.display="none";
}
/*
* Some of the supported MVPDs require their login pages to be displayed within an iFrame.
* In your HTML page, you must include the following <div> tag: "<div id="mvpddiv"></div>".
* Called when the selected MVPD requires an iFrame in which to display its authentication UI.
*/
function createIFrame(inWidth, inHeight) {
     // Create the iFrame to the specified width and height for the auth page
    ifrm = document.createElement("IFRAME");
    ifrm.name = "mvpdframe";
    ...
    document.getElementById('mvpddiv').appendChild(ifrm);
    ...
    // Force the name into the DOM since it is still not refreshed, for IE
    window.frames["mvpdframe"].name = "mvpdframe";
}
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
    /* This is an example how previously the MVPD picker was build and will be replaced. */
}
/* 
* Sending the user selected MVPD of the custom dialog is achieved
* by calling the API function setSelectedProvider(providerID:String).
*/
function setSelectedProvider(providerID) {
    accessEnablerObject.setSelectedProvider(providerID);
}
```


## Selector de MVPD con página de inicio de sesión en una ventana emergente {#mvpd-pickr-popup}

Ya que no vamos a usar un **iFrame** el código de HTML ya no contendrá el iFrame ni el botón para cerrar el iFrame. El div que anteriormente contenía el iFrame - **mvpddiv** - se conservarán y utilizarán para:

* para notificar al usuario que la página de inicio de sesión de MVPD ya está abierta si se pierde el foco emergente
* proporcionar un vínculo para recuperar el foco en la ventana emergente

```HTML
<body onload="javascript:loadAccessEnabler();"> 
   <div id="aeHolder">
       <div name="contentAccessEnabler" id="contentAccessEnabler"></div>
   </div>
   <div id="mvpddiv">
      <p>
      <strong>No login window?</strong>
      <br/>
      <a href="javascript:mvpdWindow.focus();">Click here to open it.</a>
      <br/>
      Still not working? Check popup blockers!
      </p>
   </div> 
 
   <div id="picker" style="display:none">
      Choose MVPD: <br/>
      <select id="mvpdList" multiple></select>
      <br/>
         <a id="authenticateButton" onclick="javascript:authenticate();">Authenticate</a>
   </div>
</body>
```

La lista de MVPD se mostrará en el div llamado **picker** como selección **-mvpdList**.

Se utilizará una nueva llamada de retorno de API: **setConfig(configXML)**. La rellamada se activa después de llamar a la función setRequestor(requestorID) . Esta llamada de retorno devuelve la lista de MVPD que están integrados con requestorID establecido anteriormente. En el método de rellamada, se analizará el XML entrante y la lista de MVPD se almacenará en caché. El selector de MVPD también se crea pero no se muestra.

```JavaScript
var mvpdList;  // The list of cached MVPDs
var mvpdWindow;  // The reference to the popup with the MVPD login page
var cancelTimer = 0;
/* Callback indicating that the AccessEnabler swf has initialized */
function swfLoaded() {
   accessEnablerObject = $('#AccessEnabler').get(0);
   // Using a custom implementation of the MVPD picker
   accessEnablerObject.setProviderDialogURL('none');
   accessEnablerObject.setRequestor(requestorID); 
}

function setConfig(configXML) {
   mvpdList = [];
   $.each($($.parseXML(configXML)).find('mvpd'), function (idx, item) {
      var mvpdId = $(item).find('id').text();
      mvpdList[mvpdId] = {
         displayName: $(item).find('displayName').text(),
         logo: $(item).find('logoUrl').text(),
         popup: $(item).find('iFrameRequired').text() == "true",
         width: $(item).find('iFrameWidth').text(),
         height: $(item).find('iFrameHeight').text()
      };

      $('#mvpdList').append($('<option value="' + mvpdId + '" title="' + mvpdId + '">' + mvpdList[mvpdId].displayName + '</option>'));
   });
   accessEnablerObject.getAuthentication();
}
```

Después de llamar a la función getAuthentication() o getAuthorization() , se activa la llamada de retorno displayProviderDialog() . Normalmente, dentro de esta llamada de retorno, la lista MVPD se habría creado y mostrado. Dado que el selector de MVPD ya está creado, lo único que queda por hacer es mostrarlo al usuario.

```JavaScript
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
   $('#picker').show();
}
```

Una vez que el usuario ha seleccionado un MVPD desde el selector, se debe crear la ventana emergente. Algunos exploradores pueden bloquear la ventana emergente si se crea con about:blank o con una página que se encuentra en otro dominio, por lo que se recomienda abrirla con el nombre de host desde el que se carga AccessEnabler.

En la implementación de iFrame, el restablecimiento del flujo de autenticación se realizaba mediante el botón btnCloseIframe y la función de JavaScript closeIframeAction(), pero ahora ya no es posible decorar el iFrame. Por lo tanto, se logra el mismo comportamiento mirando cuándo se cierra la ventana emergente (ya sea por el usuario o finalizando el flujo de autenticación). Se ha añadido un fragmento de código que también ayuda en caso de que el usuario pierda el foco de la ventana emergente:

```HTML
"<a href="javascript:mvpdWindow.focus();">Click here to open it.</a>".
```

En la llamada de retorno createIFrame() , la variable **mvpddiv** se mostrará div.

```JavaScript
function createIFrame(width, height) {
   $('#mvpddiv').show();
   if (useIframeLoginStyle) {
      ...
   }
}

/* Function called when user has selected the MVPD from the picker */
function authenticate() {
   var selectedMvpd = $('#mvpdList').val()[0];
   if (mvpdList[selectedMvpd].popup) {
      mvpdWindow = window.open("http://entitlement.auth-staging.adobe.com", "mvpdframe", "width=" + mvpdList[selectedMvpd].width + ",height=" + mvpdList[selectedMvpd].height, true);
      if (!mvpdWindow) {
         // Message to user that popup blocker is not allowing the authentication process to start
      }
      //watch the mvpd popup for close
      clearInterval(cancelTimer);
      cancelTimer = setInterval(checkClosed, 200);
   }
   accessEnablerObject.setSelectedProvider(selectedMvpd);
}

function checkClosed() {
   try {
      if (mvpdWindow && mvpdWindow["closed"]) {
         clearInterval(cancelTimer);
         accessEnablerObject.setSelectedProvider(null);
         accessEnablerObject.getAuthentication();
         $('#mvpddiv').hide();
      }
   } catch (error) {
      console.log(error);
   }
}
```

>[!IMPORTANT]
>
>* El código de ejemplo contiene una variable codificada para el requestorID - &quot;REF&quot; utilizado que debe reemplazarse por un ID de solicitante de programador real.
>* El código de ejemplo solo se ejecutará correctamente desde un dominio en la lista blanca asociado al id de solicitante utilizado.
>* Dado que todo el código está disponible para descarga, el código presentado en esta nota técnica se ha truncado. Para obtener una muestra completa, consulte **Ejemplo de iFrame de JS frente a muestra emergente**.
>* Las bibliotecas JavaScript externas se vincularon desde [Servicios alojados en Google](https://developers.google.com/speed/libraries/).

