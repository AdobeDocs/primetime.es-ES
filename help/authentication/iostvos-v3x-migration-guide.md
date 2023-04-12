---
title: Guía de migración de iOS/tvOS v3.x
description: Guía de migración de iOS/tvOS v3.x
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Guía de migración de iOS/tvOS v3.x {#iostvos-v3x-migration-guide}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

>[!TIP]
> 
> **Notas:**
>
> - A partir de la versión 3.1 del sdk de iOS, los implementadores ahora pueden utilizar WKWebView o UIWebView de forma intercambiable. Dado que UIWebView está en desuso, las aplicaciones deben migrar a WKWebView para evitar problemas con futuras versiones de iOS.
> - Tenga en cuenta que la migración implicaría simplemente cambiar la clase UIWebView por WKWebView, no hay trabajo específico por hacer con AccessEnabler de Adobe.


</br>

## Actualizar configuración de compilación {#update}

Esta versión contiene funciones escritas en lenguaje SWIFT. Si la aplicación es completamente Objective-C, debe establecer la casilla de verificación &quot;Incorporar siempre bibliotecas estándar de Swift&quot; en la configuración de compilación de su destino en &quot;Sí&quot;. Cuando se establece esta opción, Xcode explora los marcos agrupados en la aplicación y, si alguno de ellos contiene código Swift, copia las bibliotecas pertinentes en el paquete de la aplicación. Si no actualiza la configuración de la compilación, es posible que la aplicación se bloquee con errores que indiquen que no puede cargar AccessEnabler.framework o varios `ibswift*` bibliotecas.

</br>

## Adición de la declaración de software {#add}

> Para obtener información sobre cómo obtener su declaración de software, vaya a esta
> página:
> [Registro de solicitudes](/help/authentication/iostvos-application-registration.md)

Una vez que tenga su declaración de software, le recomendamos que la aloje en un servidor remoto para que pueda revocarla o cambiarla fácilmente sin implementar una nueva versión de la aplicación en App Store. Cuando se inicie la aplicación, obtenga la declaración del software desde la ubicación remota y páselo en el constructor AccessEnabler:

```swift
    accessEnabler = AccessEnabler("YOUR_SOFTWARE_STATEMENT_HERE");
```

> Información de API aquí: [Referencia de la API de iOS/tvOS](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## Añadir el esquema de URL personalizado {#add-custom}

> Para obtener información sobre cómo obtener un esquema de URL personalizado, vaya a esta página: [Obtener un esquema de URL de cliente](/help/authentication/iostvos-application-registration.md)

Después de obtener el esquema de URL personalizado, debe agregarlo al archivo info.plist de la aplicación. El esquema personalizado tiene este formato: `adbe.u-XFXJeTSDuJiIQs0HVRAg://`. Debe omitir los dos puntos y las barras diagonales al añadirlos al archivo. El ejemplo anterior pasará a ser `adbe.u-XFXJeTSDuJiIQs0HVRAg`.

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>CUSTOM_URL_SCHEME_HERE</string>
            </array>
        </dict>
    </array>
```

</br>

## Interceptación de llamadas en el esquema de URL personalizado {#intercept}

Esto solo se aplica en caso de que la aplicación haya habilitado anteriormente la administración manual del controlador de vista Safari (SVC) a través del [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](/help/authentication/iostvos-sdk-api-reference.md) y para MVPD específicos que requieren el controlador de vista Safari (SVC), por lo que requieren cargar las direcciones URL de los extremos de autenticación y cierre de sesión por un controlador SFSafariViewController en lugar de un controlador UIWebView/WKWebView.

Durante los flujos de autenticación y cierre de sesión, la aplicación debe monitorizar la actividad de `SFSafariViewController `a medida que pasa por varias redirecciones. La aplicación debe detectar el momento en que carga una URL personalizada específica definida por el `application's custom URL scheme` (p. ej.`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com)`. Cuando el controlador carga esta dirección URL personalizada específica, la aplicación debe cerrar la `SFSafariViewController` y llame a AccessEnabler `handleExternalURL:url `método de API.

En `AppDelegate` añada el siguiente método:

```swift
    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey: Any]) -> Bool {
            if (url.absoluteString.hasPrefix("adbe.")) {
                accessEnabler.handleExternalURL(url.description)
                return true;
            } 
        }
```

> Información de API aquí: [Gestión de URL externa](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## Actualizar la firma del método setRequestor {#update-setreq}

Dado que el nuevo SDK utiliza un nuevo mecanismo de autenticación, no es necesario el parámetro signedRequestId o la clave pública y el secreto (para tvOS). La variable `setRequestor` se simplifica y solo necesita requestorID.

### iOS

Este código:

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId)
```

se convierte en:

```swift
    accessEnabler.setRequestor(requestorId)
```

</br>

### tvOS

Este código:

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId,
                    secret: "secret", publicKey: "public_key")
```

se convierte en:

```swift
    accessEnabler.setRequestor(requestorId)
```

> Información de API aquí: [Definir solicitante](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## Sustituya el método getAuthenticationToken por el método handleExternalURL {#replace}

`getAuthentication` se ha utilizado anteriormente para completar el flujo de autenticación. Como su nombre era engañoso, se le cambió el nombre a `handleExternalURL` y toma la url como parámetro.

Cambie todas las ocurrencias de esto:

```swift
    accessEnabler.getAuthenticationToken()
```

en esto:

```swift
    accessEnabler.handleExternalURL(request.url?.description);
```

> Información de API aquí: [Gestión de URL externa](/help/authentication/iostvos-sdk-api-reference.md)
