---
title: Uso de Charles Proxy
description: Uso de Charles Proxy
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Uso de Charles Proxy {#using-charles-proxy}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


**Charles:** <http://charlesproxy.com>

 
## Descargar, instalar y comenzar con Charles Proxy {#download-install-and-get-stared-with-charles-proxy}

- **Descargar** - <http://www.charlesproxy.com/download/>
- **Instalar** - <http://www.charlesproxy.com/documentation/installation/>
- **Introducción** - <http://www.charlesproxy.com/documentation/getting-started/>

 
## Estructura vs. Pestañas de secuencia {#structure-vs-sequence-tabs}

Existen dos formas diferentes de ver el tráfico:

1. **Estructura** - Las solicitudes se agrupan por host
1. **Secuencia** - Las solicitudes se enumeran en el orden en que se llaman


## SSL y certificados {#ssl-and-certificates}

Habilitar el proxy SSL `\[ *Proxy -\> Proxy Settings... -\> SSL* \]`

Marque la casilla &quot;Habilitar el proxy SSL&quot; y añada todas las ubicaciones HTTPS.


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/ProxySettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/SSLSettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AddHttpsLocations.PNG)



- proxy SSL - <http://www.charlesproxy.com/documentation/proxying/ssl-proxying/>
- Certificados SSL - <http://www.charlesproxy.com/documentation/using-charles/ssl-certificates/>
- Proxying SSL desde dispositivos móviles: consulte a continuación.

 
## Ignorar/excluir hosts {#ignore-/-exclude-hosts}

Si la salida se vuelve demasiado saturada, puede elegir ignorar o excluir ubicaciones Puede ignorar o excluir ubicaciones haciendo cualquiera de las siguientes acciones:

- Haga clic con el botón derecho en las solicitudes que desee ignorar y, a continuación, seleccione &quot;Ignorar&quot;
- Agregar manualmente las ubicaciones de las que excluir `\[ *Proxy -\> Recording Settings... -\> Exclude* \]`

 
## Parpadeo de DNS {#dns-spoffing}

`\[ *Tools -\> DNS Spoofing...* \]`

 

La suplantación de DNS es muy útil cuando se intenta redirigir una solicitud a una IP diferente, especialmente cuando se trabaja con dispositivos móviles:

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/DNSSpoofing.PNG)

<http://www.charlesproxy.com/documentation/tools/dns-spoofing/>

 
## Mapa remoto {#map-remote}

`\[ *Tools -\> Map Remote...* \]`

 

Con map remote puede redirigir una solicitud &quot;entrante&quot; a un punto final diferente. El caso de uso más común para esta función es &quot;Mapa&quot; `AccessEnabler.swf` a `AccessEnablerDebug.swf:`

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemote.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemoteAdd.PNG)

<http://www.charlesproxy.com/documentation/tools/map-remote/>

 

## Proxy inverso {#reverse-proxy}

<http://www.charlesproxy.com/documentation/proxying/reverse-proxy/>

## Móvil {#mobile}

### Uso de Charles en un dispositivo iOS (iPhone/iPad) {#use-charles-on-an-ios-device-(iphone-/-ipad)}

#### Conexión SSL desde iPhone {#ssl-connection-from-iphone}

Vaya a <http://charlesproxy.com/charles.crt> desde su dispositivo iOS.  Esto iniciará el cuadro de diálogo de instalación del certificado:

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate1\(1\).PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate2\(1\).PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate3.PNG)

 </br>

Haga clic en `\[ *Install*... *Install*... *Done* \]` para completar la instalación del certificado.

<http://www.charlesproxy.com/documentation/faqs/ssl-connections-from-within-iphone-applications/>

 

#### Uso de Charles desde un dispositivo iOS {#using-charles-from-an-ios-device}

En el dispositivo iOS, seleccione `\[ *Settings* -\> *Wi-FI* -\> (*YOUR\_WIFI\_NETWORK)* \]`. Haga clic en la pequeña flecha azul junto a su red y, a continuación, vaya al proxy HTTP y seleccione &quot;Manual&quot;: 


 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy1.png)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy2.PNG)


 </br>
Aquí debe especificar la IP y el puerto del equipo donde está ejecutando Charles. <span style="line-height: 1.6em;">Ahora, si abre Safari en el dispositivo iOS e intenta abrir una página web, debería tener la siguiente ventana emergente en el equipo que ejecuta Charles:
 
 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy3.PNG)

</br>
Haga clic en "Permitir" para permitir que el dispositivo use Charles para representar todas sus solicitudes.

<http://www.charlesproxy.com/documentation/faqs/using-charles-from-an-iphone/>


#### iOS: confía en cualquier certificado {#ios-trust-any-certificates}

<http://stackoverflow.com/questions/933331/how-to-use-nsurlconnection-to-connect-with-ssl-for-an-untrusted-cert>

#### Error de autenticación de iOS: no se encuentra adobepass.ios.app

<https://tve.zendesk.com/entries/22135907-ios-authentication-error-adobepass-ios-app-cannot-be-found>


## Usar Charles para Android

<http://jaanus.com/post/17476995356/debugging-http-on-an-android-phone-or-tablet-with>

<http://www.charlesproxy.com/documentation/configuration/browser-and-system-configuration>


Vaya a [proxy Charles](http://charlesproxy.com/charles.crt) desde su dispositivo Android.
