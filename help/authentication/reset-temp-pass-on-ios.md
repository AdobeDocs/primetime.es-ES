---
title: Restaurar paso temporal en iOS
description: Restaurar paso temporal en iOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# Restaurar paso temporal en iOS {#reset-temp-pass-on-ios}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

La aplicación de demostración de iOS incluye una pantalla dedicada para restablecer el TTL de paso temporal. Se requiere la siguiente información para la operación de restablecimiento:

- **Entorno:** especifica el punto final del servidor de pase de TV de pago de Adobe que recibirá la llamada de red restablecer Temp Pass. Valores posibles: **Prequal** (*mgmt-prequal.auth-staging.adobe.com*), **Versión** (*mgmt.auth.adobe.com*) o **Personalizado** (reservado para pruebas internas de Adobe).
- **Token del portador de OAuth2:** el token OAuth2 es necesario para autorizar al programador para la autenticación Adobe Pay-TV. Este token se puede obtener del extremo OAuth2 de autenticación de Pay-TV dedicado (por ejemplo, *curl -u &quot;\&lt;consumer _key=&quot;&quot;>:\&lt;consumer _secret=&quot;&quot; _key=&quot;&quot;>*&quot; *&quot;https://mgmt.auth.adobe.com/oauth2/permanent\_accesstoken?grant\_type=client\_credentials&quot;*).
- **ID del solicitante:** el ID exclusivo del programador actual. Este valor se lee desde la pantalla principal de la aplicación de demostración (el campo solicitante).
- **Id. de paso temporal:** ID exclusivo para el MVPD de Temp Pass.
- **ID del dispositivo:** ID de dispositivo con hash calculado por la aplicación de demostración.
- **Clave genérica:** algunos MVPD de Temp Pass (es decir, la siguiente funcionalidad extensible de Temp Pass) admiten una clave genérica para restablecer Temp Pass (junto con el ID del dispositivo).

Todos los parámetros anteriores (excepto el *Clave genérica*) son obligatorios. A continuación, se muestra un ejemplo de parámetros y la llamada de red asociada que realizará la aplicación de demostración (el ejemplo tiene la forma de un *comando * curl):

- **Entorno:** Versión (*mgmt.auth.adobe.com*)
- **Token del portador de OAuth2:** H4j7cF3GtJX81BrsgDa10GwSizVz
- **ID del programador:** REF
- **Id. de paso temporal:** TempPassREF
- **ID del dispositivo:** f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa6399 91 
- **Clave genérica:** null (no se ha proporcionado ningún valor)

```curl
curl -X DELETE -H "Authorization:Bearer* *H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991&requestor_id=REF&mvpd_id=TempPassREF"
```

se realizará una solicitud HTTP DELETE a la variable **/reset** , pasando el *Token del portador de OAuth2* en el encabezado Autorización y en el *ID del dispositivo*, *ID del solicitante* y *ID de paso temporal (ID de MVPD)* como parámetros.

Si el programador proporciona un valor para la variable *Clave genérica*, se realizará otra llamada HTTP (esta vez a la función **/reset/generic** punto final), pasando el *Clave genérica* dentro del *key* parámetro de solicitud.

Por ejemplo, si se configura la variable *Clave genérica* a un hash de dirección de correo electrónico (para MVPD de Temp Pass que admitan este tipo de funcionalidad) dará como resultado la siguiente llamada HTTP (el correo electrónico es `user@domain.com` su hash SHA-256 es `f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7`):

```curl
curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz"
"https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=TempPassREF"
```

Es importante destacar que el restablecimiento de Temp Pass en la aplicación de demostración puede no tener el mismo efecto para una aplicación de programación en el mismo dispositivo. Esto se debe a que el ID del dispositivo (calculado por la aplicación de demostración y AccessEnabler) puede no ser el mismo para todas las aplicaciones del dispositivo:

- iOS 6 y versiones posteriores: el ID del dispositivo se calcula mediante la dirección de MAC (que es única para todas las aplicaciones), por lo que al restablecer Temp Pass en la aplicación de demostración, se restablecerá en todas las demás aplicaciones de programador del dispositivo.

- iOS 7 y superior: el ID del dispositivo se calcula en función del valor IDFV (ID del proveedor), que es único para todas las aplicaciones que tienen el mismo prefijo de ID de paquete (es decir, todos los componentes excepto el último). Dado que la aplicación de demostración y una aplicación de programador tienen ID de paquete diferentes, al restablecer el paso temporal en la aplicación de demostración no se aplicará ningún efecto en una aplicación de programador.

El último caso de uso (iOS 7 y superior) es el más común, así que veamos cómo los programadores pueden restablecer Temp Pass para sus aplicaciones en esta situación. Hay varias opciones:

1. Puerto el código desde la aplicación de demostración a la aplicación de programador. La variable *TempPassResetViewController* y *DeviceIdDemoApp* contienen la lógica principal para restablecer Temp Pass, y pueden modificarse e incluirse fácilmente en la aplicación Programmer.

1. Ejecute la solicitud HTTP para restablecer el paso temporal con *curl*. El parámetro device\_Id se puede obtener calculando el IDFV de la aplicación de programación y aplicando un hash SHA-256 sobre ella (código de muestra en la variable *DeviceIdDemoApp* clase ).

1. Simplemente realice el restablecimiento desde la aplicación de demostración especificando el IDFV con hash de la aplicación del programador como *Clave genérica*. Esto resultará en dos llamadas de red: una para restablecer el pase temporal para la aplicación de demostración (irrelevante para el programador) y otra para restablecer el pase temporal para la aplicación del programador.

Todas las opciones anteriores son similares, es responsabilidad del programador elegir una según la facilidad de implementación. 

