---
title: Inicio de sesión y cierre de sesión sin actualizar
description: Inicio de sesión y cierre de sesión sin actualizar
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 0%

---


# Inicio de sesión y cierre de sesión sin actualizar {#tefresh-less-login-and-logout}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#overview}

Para las aplicaciones web, debe tener en cuenta diferentes escenarios posibles para autenticar y cerrar sesión de usuarios.  Los MVPD requieren que los usuarios inicien sesión en la página web del MVPD para autenticarse, con los siguientes factores adicionales en juego:

- Algunos MVPD requieren un redireccionamiento completo desde el sitio a su página de inicio de sesión
- Algunos MVPD requieren que abra un iFrame en su sitio para mostrar la página de inicio de sesión de MVPD
- Algunos navegadores no gestionan bien el escenario de iFrame, por lo que para esos navegadores una mejor alternativa es usar una ventana emergente en lugar del iFrame

Antes de la autenticación de Adobe Primetime 2.7, todos estos escenarios para autenticar a un usuario implicaban una actualización de página completa de la página del programador. Para la versión 2.7 y versiones posteriores, el equipo de autenticación de Adobe Primetime mejoró estos flujos para que el usuario no tenga que actualizar la página en la aplicación durante el inicio de sesión y el cierre de sesión.  


## Descripción detallada {#detailed_description}

Comencemos con un resumen de los flujos de autenticación y cierre de sesión originales, y sigamos con los flujos mejorados de autenticación y cierre de sesión. Tenga en cuenta que las primeras cuatro secciones tratan de los MVPD normales (que no sean TempPass), mientras que la última sección describe la implementación especial que debe aplicarse para TempPass:

- [Flujo de autenticación original](#orig_authn)
- [Flujo de cierre de sesión original](#orig_logout)
- [Flujo de autenticación mejorado](#improved_authn)
- [Flujo de cierre de sesión mejorado](#improved_logout)
- [Flujo TempPass](#improved_temppass)

</br>

## Flujos de autenticación/cierre de sesión originales {#orig_authn}

**Autenticación**

Los clientes web de autenticación de Adobe Primetime tienen dos formas de autenticarse, según los requisitos de los MVPD:

1. **Redireccionamiento de página completa -** Una vez que el usuario selecciona un proveedor (configurado con redireccionamiento de página completa) desde el selector de MVPD en el sitio web del programador, `setSelectedProvider(<mvpd>)` se invoca en AccessEnabler y se redirige al usuario a la página de inicio de sesión de MVPD. Una vez que el usuario proporciona credenciales válidas, se le redirige de nuevo al sitio web del programador. AccessEnabler se inicializa y el token de autenticación se recupera de la autenticación de Adobe Primetime durante `setRequestor`.
1. **iFrame / Ventana emergente -** Una vez que el usuario selecciona un proveedor (configurado con iFrame), `setSelectedProvider(<mvpd>)` se invoca en AccessEnabler. Esta acción déclencheur el `createIFrame(width, height)` llamada de retorno, notificando al programador que cree un iFrame (o ventana emergente, según el navegador o las preferencias) con el nombre `"mvpdframe"` y las dimensiones proporcionadas. Una vez creado el iFrame/popup, AccessEnabler carga la página de inicio de sesión del MVPD en el iFrame/popup. El usuario proporciona credenciales válidas y el iFrame/elemento emergente se redirige a la autenticación de Adobe Primetime, que devuelve un fragmento de JS que cierra el iFrame/elemento emergente y vuelve a cargar la página principal (sitio web del programador). Al igual que el flujo 1, el token de autenticación se recupera durante `setRequestor`. 

La variable `displayProviderDialog` llamada de retorno (activada por `getAuthentication`/`getAuthorization`) devuelve una lista de MVPD y su configuración adecuada. La variable `iFrameRequired` La propiedad de un MVPD permite al programador saber si debe activar el flujo 1 o el flujo 2. Tenga en cuenta que el programador debe realizar una acción adicional (crear un iFrame/popup) solo para el flujo 2.

**Cancelar autenticación**

También está la situación en la que el usuario cancela explícitamente el flujo de autenticación cerrando la página de inicio de sesión. Aquí están los escenarios y la solución propuesta para los programadores:

1. **Redireccionamiento de página completa -** Cuando se cierre la página de inicio de sesión, el usuario deberá volver a navegar al sitio web del programador e iniciar todo el flujo desde el principio. No se requiere ninguna acción explícita por parte del programador en este escenario.
1. **iFrame -** Se recomienda que el programador aloje el iFrame dentro de un `div` (o componente de IU similar) que tiene un botón Cerrar adjunto. Cuando el usuario presiona el botón Cerrar, el programador destruye el iFrame junto con la IU asociada y realiza la acción `setSelectedProvider(null)`. Esta llamada permite que AccessEnabler borre su estado interno y permite al usuario iniciar un flujo de autenticación posterior. `setAuthenticationStatus` y `sendTrackingData(AUTHENTICATION_DETECTION...)` se activará para indicar que se ha producido un error en el flujo de autenticación (ambos activados) `getAuthentication` y `getAuthorization`).
1. **Elemento emergente -** Algunos exploradores no pueden detectar con precisión el evento de cierre de ventana, por lo que es necesario adoptar un enfoque diferente aquí (a diferencia del flujo de iFrame anterior). Adobe recomienda que el programador inicialice un temporizador que verifique periódicamente la existencia de la ventana emergente de inicio de sesión. Si la ventana no existe, el programador puede estar seguro de que el usuario ha cancelado manualmente el flujo de inicio de sesión y el programador puede continuar llamando a `setSelectedProvider(null)`. Las llamadas de retorno activadas son las mismas que en el flujo 2 anterior.

</br>

## Flujo de cierre de sesión original {#orig_logout}

La API de cierre de sesión de AccessEnabler borra el estado local de la biblioteca y carga la URL de cierre de sesión de MVPD en la pestaña o ventana actual. El navegador navega al punto final de cierre de sesión de MVPD y, una vez completado el proceso, se redirige al usuario de nuevo al sitio web del programador. La única acción necesaria en nombre del usuario es pulsar el botón/vínculo Cerrar sesión e iniciar el flujo; no se requiere interacción del usuario en el punto final de cierre de sesión de MVPD.

**Flujo de autenticación/cierre de sesión original con actualización de página**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_refresh_web.png)

</br>

## Autenticación mejorada (sin actualizar) {#improved_authn}

>[!NOTE]
>
>Los flujos mejorados de inicio de sesión y cierre de sesión sin actualizar requieren que el explorador admita las tecnologías modernas de HTML5, incluida la mensajería web.

Tanto los flujos de autenticación (inicio de sesión) como los de cierre de sesión mencionados anteriormente proporcionan una experiencia de usuario similar al volver a cargar la página principal después de completar cada flujo.  La función actual pretende mejorar la experiencia del usuario proporcionando inicio de sesión sin actualizar (en segundo plano) y cierre de sesión. El programador puede habilitar/deshabilitar el inicio de sesión en segundo plano y el cierre de sesión pasando dos indicadores booleanos (`backgroundLogin` y `backgroundLogout`) a la variable `configInfo` del parámetro `setRequestor` API. De forma predeterminada, el inicio de sesión o cierre de sesión en segundo plano están desactivados (esto proporciona compatibilidad con la implementación anterior).

**Ejemplo:**

```JSON
    var configInfo = {
        callSetConfig: true,
        backgroundLogin: true,
        backgroundLogout: true
    };
    accessEnabler.setRequestor(REQUESTOR_ID, null, configInfo);
```

**Autenticación**

Los siguientes puntos describen la transición entre los flujos de autenticación originales y los flujos mejorados:

1. El redireccionamiento de página completa se reemplaza con una nueva pestaña del explorador en la que se realiza el inicio de sesión de MVPD. El programador es necesario para crear una nueva pestaña (a través de `window.open`) con nombre `mvpdwindow` cuando el usuario selecciona un MVPD (con `iFrameRequired = false`). A continuación, se ejecuta el programador `setSelectedProvider(<mvpd>)`, permitiendo que AccessEnabler cargue la URL de inicio de sesión de MVPD en la nueva pestaña. Una vez que el usuario proporcione credenciales válidas, la autenticación de Adobe Primetime cerrará la pestaña y enviará un window.postMessage al sitio web del programador para indicar al AccessEnabler que el flujo de autenticación ha finalizado. Se activan las siguientes llamadas de retorno:

   - Si el flujo lo inició `getAuthentication`: `setAuthenticationStatus` y `sendTrackingData(AUTHENTICATION_DETECTION...)` se activará para indicar que la autenticación se ha realizado correctamente o no.

   - Si el flujo lo inició `getAuthorization`: `setToken/tokenRequestFailed` y `sendTrackingData(AUTHORIZATION_DETECTION...)` se activará para indicar que la autorización se ha realizado correctamente o no.

1. El flujo de la ventana emergente/iFrame permanece prácticamente sin cambios, con la diferencia de que después de que el usuario proporcione credenciales válidas, la página principal no se volverá a cargar. El iFrame/popup se cerrará automáticamente después del inicio de sesión y de un `window.postMessage` se envía a la página principal notificando a AccessEnabler que el flujo ha finalizado. Las mismas llamadas de retorno se activan como en el flujo anterior, **además de la siguiente llamada de retorno nueva: `destroyIFrame`**. La variable `destroyIFrame` la rellamada permite al programador eliminar cualquier componente iFrame asociado/auxiliar, como las decoraciones de la interfaz de usuario. La existencia de esta llamada de retorno no era necesaria en el flujo de autenticación antiguo porque una vez finalizado el inicio de sesión, la autenticación de Adobe Primetime volvía a cargar la página del programador, destruyendo así todos los componentes de la interfaz de usuario que contiene.

</br>     

>[!IMPORTANT]
> 
>Debe cargar el iFrame de inicio de sesión de MVPD o la ventana emergente como elemento secundario directo de la página que contiene la instancia de AccessEnabler. Si el iFrame de inicio de sesión de MVPD o la ventana emergente están anidados dos o más niveles debajo de la página que contiene la instancia de AccessEnabler, el flujo podría bloquearse. Por ejemplo, si tiene un iFrame situado entre la página principal y el iFrame de MVPD (Página =\> iFrame =\> MVPD iFrame), el flujo de inicio de sesión podría fallar.

</br>

 **Cancelar autenticación**

Estos son los flujos para cancelar la autenticación:

1. **Ficha Explorador -** Como la pestaña es básicamente una nueva ventana, la captura de su evento close tiene las mismas limitaciones que se describen en el escenario 3 de los flujos de autenticación antiguos. Además, el método del temporizador no es posible aquí, ya que no hay forma de distinguir entre una pestaña que el usuario cerró manualmente y una pestaña que se cerró automáticamente al final del flujo de inicio de sesión. La solución aquí es que AccessEnabler permanezca &#39;silencioso&#39; (no se activan llamadas de retorno) cuando el usuario cancela el flujo. Además, el Programador no está obligado a tomar ninguna medida específica. El usuario podrá iniciar otro flujo de autenticación sin recibir el error &quot;Error de varias solicitudes de autenticación&quot; (este error se ha deshabilitado en AccessEnabler para el inicio de sesión en segundo plano).

1. **iFrame -** El programador puede utilizar el método descrito en el escenario 2 a partir de los flujos de autenticación antiguos (cree una interfaz de usuario de envoltura a partir del iFrame y el botón Cerrar asociado a los déclencheur) `setSelectedProvider(null)`. Aunque este método ya no es un requisito importante (se permiten varios flujos de autenticación para el inicio de sesión en segundo plano, como se explica en el escenario 1 anterior), el Adobe sigue recomendando este método.

1. **Elemento emergente -** Esto es idéntico al flujo de pestañas Explorador anterior.

</br>

## Flujo de cierre de sesión mejorado {#improved_logout}

El nuevo flujo de cierre de sesión se realizará en un iFrame oculto, con lo que se eliminará el redireccionamiento de página completa.  Esto es posible porque el usuario no necesita realizar una acción específica en la página de cierre de sesión de MVPD.

Una vez completado el flujo de cierre de sesión, redireccionará el iFrame a un extremo de autenticación Adobe Primetime personalizado. Esto servirá un fragmento de JS que realiza un `window.postMessage` al elemento principal, notificando a AccessEnabler que el cierre de sesión ha finalizado. Se activan las siguientes llamadas de retorno: `setAuthenticationStatus()` y `sendTrackingData(AUTHENTICATION_DETECTION ...)`, indicando que el usuario ya no está autenticado. 

La siguiente ilustración muestra el flujo sin actualizar que permite al usuario iniciar sesión en su MVPD sin actualizar la página principal de la aplicación:

**Flujo de autenticación/cierre de sesión mejorado (sin actualizar)**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_no_refresh_web.png)

</br>

## Flujo TempPass {#improved_temppas}

El inicio de sesión sin actualización sigue un enfoque diferente para los MVPD de tipo TempPass.

Dado que el flujo TempPass requiere que una ventana se cree automáticamente y se cierre sin interacción explícita del usuario, puede plantear un problema en algunos exploradores (bloqueadores de ventanas emergentes). Por lo tanto, AccessEnabler implementa la fase de inicio de sesión entre bastidores, sin requerir un contenedor web creado por el programador.

Estos son los aspectos que el programador debe tener en cuenta al implementar TempPass para el inicio de sesión y cierre de sesión sin actualizar:

- Antes de iniciar la autenticación, el iFrame o la ventana emergente solo deben crearse para los MVPD que no sean de TempPass. El programador puede detectar si un MVPD es TempPass o no leyendo el `tempPass` propiedad del objeto MVPD (devuelto por `setConfig()` / `displayProviderDialog()`).

- La variable `createIFrame()` la llamada de retorno debe contener una comprobación para TempPass y ejecutar su lógica solo cuando el MVPD NO sea TempPass.

- La variable `destroyIFrame()` la llamada de retorno debe contener una comprobación para TempPass y ejecutar su lógica solo cuando el MVPD NO sea TempPass.

- La variable `setAuthenticationStatus()` y `sendTrackingData()` las llamadas de retorno se invocan después de completarse la autenticación (exactamente como en el flujo sin actualización para los MVPD normales).

>[!NOTE]
>
>Este flujo solo está disponible para Refresh-less TempPass. Para el flujo de actualización, TempPass debe gestionarse explícitamente (cuando TempPass requiere iFrame / popup)

</br>

El siguiente ejemplo de código muestra cómo gestionar una ventana MVPD en el sitio web de un programador (tanto para MVPD normales como para TempPass):

```javascript
    var aeHostname = "https://entitlement.auth.adobe.com";
    var mvpdWindow = null;
    var mvpd = <mvpd_object_from_displayProviderDialog>;
    var useIframeLogin = <boolean_depending_on_browser_or_Programmer_preferences>;
    var backgroundLogin = <boolean_depending_on_Programmer_preferences>;
     
    // Do not create any windows for refreshless and temp pass
    if (!(backgroundLogin && mvpd.tempPass)) {
        if (backgroundLogin && !mvpd.popup) {
            mvpdWindow = window.open(aeHostname, "mvpdwindow");
        } else if (mvpd.popup && !useIframeLogin) {
            var width = mvpd.width;
            var height = mvpd.height;
            // Center on screen
            var top = (document.all) ? window.screenTop : window.screenY + 100;
            var left = (document.all) ? window.screenLeft : window.screenX + window.innerWidth / 2 - width / 2;
        
            mvpdWindow = window.open(aeHostname, "mvpdframe",
                           "width=" + width + ",height=" + height + ",top=" + top + ",left=" + left);
            // Monitor the mvpd popup for close
            if (!backgroundLogin) {
                clearInterval(cancelTimer);
                cancelTimer = setInterval(function () {
                    if (mvpdWindow && mvpdWindow.closed) {
                        clearInterval(cancelTimer);
                        $('#mvpddiv').hide();
                        accessEnablerAPI.setSelectedProvider(null);
                    }
                }, 200);
            }
        }
    }
```

