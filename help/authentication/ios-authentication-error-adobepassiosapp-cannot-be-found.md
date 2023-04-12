---
title: 'Error de autenticación de iOS: no se puede encontrar adobepass.ios.app'
description: 'Error de autenticación de iOS: no se puede encontrar adobepass.ios.app'
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Error de autenticación de iOS: no se puede encontrar adobepass.ios.app {#ios-authentication-error-adobepass.ios.app-cannot-be-found}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Problema {#issue}

El usuario va a través del flujo de autenticación y, después de que haya introducido correctamente sus credenciales con su proveedor, se les redirige a una página de error, una página de búsqueda o a otra página personalizada que le informe de que `adobepass.ios.app` no se pudo encontrar/resolver.

## Explicación {#explanation}

En iOS, `adobepass.ios.app` se utiliza como dirección URL de redirección final para indicar que el flujo AuthN ha finalizado. En este punto, la aplicación necesita realizar una solicitud a AccessEnabler para obtener el autenticador de autenticación y finalizar el flujo de autenticación.

El problema es que `adobepass.ios.app` no existe realmente y genera un déclencheur de un mensaje de error en la variable `webView`. Las versiones anteriores de iOS DemoApp supusieron que este error siempre se activaría al final del flujo AuthN y se configuró para manejarlo en consecuencia (`indidFailLoadWithError`).

**Nota:** Este problema se ha corregido en versiones posteriores de DemoApp (incluida con la descarga del SDK de iOS).

Desafortunadamente, esta suposición NO es correcta. Existen algunos servidores DNS o proxy &quot;inteligentes&quot; que no solo transmiten el error generado, sino que, en su lugar, realizan una de las siguientes acciones: 

- Crear una página de error personalizada
- Reenviar a una página de búsqueda o a otro tipo de página o portal del cliente.

En estos casos, la respuesta que regresa a iOS webView será una respuesta perfectamente válida en lo que respecta a webView, y NO déclencheur el error en el que dependía la antigua DemoApp.

## Solución {#solution}

NO realice la misma suposición que la DemoApp. En su lugar, intercepte la solicitud antes de ejecutarla (en `shouldStartLoadWithRequest`) y manejarlo adecuadamente.

Ejemplo de cómo interceptar la solicitud antes de ejecutarla:

```obj-c
- (BOOL)webView:(UIWebView*)localWebView shouldStartLoadWithRequest:(NSURLRequest*)request navigationType:(UIWebViewNavigationType)navigationType {

NSString *absolutePath = [[request URL] absoluteString]; 
if ([absolutePath isEqualToString:ADOBEPASS_REDIRECT_URL] && ![APP_DELEGATE getAuthenticationWasCalled]) {

// user was logged ok => call getAuthenticationToken() 
[APP_DELEGATE setGetAuthenticationWasCalled:YES]; 
[[APP_DELEGATE accessEnabler] getAuthenticationToken];
return NO;

}

return YES;

}
```

Algunas cosas a tener en cuenta:

- NUNCA usar `adobepass.ios.app` directamente en cualquier parte del código. En su lugar, utilice la constante `ADOBEPASS_REDIRECT_URL`
- La variable `return NO;` impide que la página se cargue
- Asegúrese de que la variable `getAuthenticationToken` se llama una vez y solo una vez en el código. Varias llamadas a `getAuthenticationToken` dará como resultado resultados no definidos.

