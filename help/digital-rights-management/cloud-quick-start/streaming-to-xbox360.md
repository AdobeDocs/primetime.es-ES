---
title: Establezca el token XSTS en su reproductor
description: Establezca el token XSTS en su reproductor
copied-description: true
exl-id: 1b83baac-e6a6-4e84-8ea5-07bd7e4afd9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# Transmisión a Xbox360 (opcional) {#streaming-to-xboc360}

Primetime DRM está disponible en la plataforma Xbox360. Sin embargo, solo se admite el caso de uso Flujo protegido, no el conjunto completo de derechos de directiva DRM. No se admiten los derechos de directiva de DRM que no sean de flujo continuo, como Grupos de dominio de dispositivo. La Xbox360 ignora los derechos no admitidos al intentar reproducir contenido.

Los derechos de directiva DRM de Primetime admitidos para Xbox son:
* Protección de salida digital
* Fecha de finalización de almacenamiento en caché de licencia sin conexión
* Fecha de inicio de licencia
* Fecha de finalización de licencia
* Duración de la ventana de reproducción (segundos)

Es posible que el contenido no tenga que volver a empaquetarse para transmitirse a Xbox360 si ya estaba empaquetado para otra plataforma de Primetime, como iOS, Android o Desktop.

Una advertencia con Xbox360 es que siempre debe ponerse en contacto con un servidor de claves cada vez que se encuentre una etiqueta EXT-X-KEY en el M3U8. A diferencia de iOS, donde una configuración de directiva DRM (policy.requireKeyServer) hará que el reproductor de vídeo de iOS Primetime recupere la clave de descifrado AES de localhost, Xbox siempre intentará recuperar la clave de descifrado de un servidor de claves remoto No hay derecho de directiva DRM para indicar a la aplicación Xbox que recupere la clave de descifrado AES del host local. Debido a este requisito, las entradas de EXT-X-KEY deben estar en el M3U8 apuntando al punto final de DRM de Primetime Cloud. Esta URL se establece mediante &lt;key_url> en el archivo de configuración OfflinePackager.jar config_hls.xml.

Si desea empaquetar contenido una vez y transmitirlo a todos los destinos de Primetime, así como configurar dispositivos iOS para que no recupere una clave de un servidor de claves remoto, puede empaquetar el contenido mediante una directiva DRM que tenga la propiedad policy.requireKeyServer=false (como en policy_ios_localkeyserver.pol). Los dispositivos iOS recuperarán la clave AES localmente, mientras que los dispositivos Xbox ignorarán esta propiedad y se pondrán en contacto con el servidor de claves DRM de Primetime Cloud para obtener una clave de descifrado.

>!Nota
>
>Todas las solicitudes de Xbox360 deben utilizar autenticación personalizada/>derecho.Esto se debe a que en la plataforma Xbox360, Xbox Live >utiliza un token de Xbox Secure Token Server (XSTS) para >fines de autenticación.
>El servidor de licencias DRM de Primetime Cloud usa el token XSTS para >validar la integridad del dispositivo Xbox y del usuario que realiza >la solicitud de licencia. Sin embargo, para validar el token de XSTS se requiere una clave de proveedor privada de Xbox Live del >cliente, que Primetime Cloud DRM >no almacena. Debido a esto, cuando Primetime Cloud DRM recibe >una solicitud de licencia de un cliente Xbox 360, Primetime Cloud DRM >reenviará el token XSTS al servidor back-end >autenticación/derecho del cliente de Primetime. El servidor del cliente de Primetime
>analizará y validará el token XSTS para asegurarse de que se >firmó con la clave de editor de la aplicación del cliente.
>Para pasar un token XSTS del cliente Xbox360, establezca el token >sincrónicamente en respuesta al evento MediaPlayer.RequestKeyAttribute >descrito con más detalle aquí: **Configure el token XSTS en el reproductor.** Con la versión del software se incluye un ejemplo de servidor de autenticación/derecho back-end en el directorio de autenticación personalizada y derecho.La validación de tokens XSTS se analiza >con más detalle aquí: **Validación de token XSTS de Xbox Live.**


## Establezca el token XSTS en su reproductor {#set-the-xsts-token-in-your-player}

En Xbox360, el token se establece de forma asíncrona en respuesta a la `MediaPlayer.RequestKeyAttribute` evento.

Establezca el token XSTS.

La aplicación de ejemplo incluida con el software muestra cómo establecer el token XSTS en el reproductor. Este es el fragmento de código relevante del reproductor de muestra:

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

## Validación de token XSTS de Xbox Live {#xbox-live-xsts-token-validation}

Para solicitudes XSTS, la variable `customerSpecificAuthToken` contendrá el token XSTS codificado en Base64. La muestra `XSTSValidator` El código examina el token descodificado Base64 para detectar la existencia del `EncryptedAssertion` ; sin embargo, puede utilizar otros métodos para distinguir entre estas solicitudes y las solicitudes que no son de Xbox. Por ejemplo, puede utilizar una dirección URL diferente.

La política devuelta en el mensaje de respuesta anulará la política original en los metadatos DRM suministrados con la solicitud de clave Xbox. El cliente Xbox solo admite un subconjunto de características de directiva, y estos campos son los únicos que anularán la directiva original.

Se necesitan pasos de configuración adicionales para admitir el descifrado y la validación de tokens. Debe cargar el [!DNL xsts_partner_cert.pfx] y [!DNL x_secure_token_service.part.xboxlive.com.cer] credenciales en un repositorio de claves en formato JKS, que luego proporciona al servidor de derechos de back-end como propiedad del sistema `xsts-keystore`. De forma predeterminada, el socio [!DNL .pfx] tiene el alias `xsts`y el certificado de validación de token tiene el alias `xsts-verify-cert`. También puede anularlos mediante las propiedades del sistema. Finalmente, hay una propiedad del sistema `xsts-keystore-password` que no tiene valor predeterminado y que contiene la contraseña del almacén de claves. Las propiedades del sistema leídas por el `XSTSValidator` Los códigos se resumen a continuación:

| Propiedad del sistema | Valor predeterminado | Comentario |
|---|---|---|
| xsts-keystore | xsts.jks | Almacén de claves de formato JKS utilizado por el validador. |
| xsts-keystore-password |  | Contraseña del almacén de claves |
| xsts-alias | xsts | Alias utilizado para recuperar la clave de descifrado del almacén de claves |
| xsts-verify-cert-alias | xsts-verify-cert | Alias utilizado para recuperar el certificado de validación del almacén de claves |

## Crear JKS para un validador de XSTS{#create-jks-for-an-xsts-validator}

1. Averigüe el nombre de alias del certificado privado, ubicado en el socio [!DNL .pfx] archivo.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Convertir [!DNL .pfx] hasta [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (donde `<alias>` es el nombre de alias del certificado privado que descubrió en el paso 1).
1. Importar [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Put [!DNL xsts.jks] en el directorio de inicio de Tomcat y defina `-Dxsts-keystore-password=****` para Tomcat.

If [!DNL xsts_partner_cert.pfx] y [!DNL xsts.jks] están utilizando contraseñas diferentes, actualice el `xsts` contraseña en `jks` para que sean iguales.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
