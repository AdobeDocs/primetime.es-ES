---
title: Establezca el token XSTS en el reproductor
description: Establezca el token XSTS en el reproductor
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---


# Transmisión a Xbox360 (opcional) {#streaming-to-xboc360}

Primetime DRM está disponible en la plataforma Xbox360. Sin embargo, solo se admite el caso de uso de transmisión protegida, no el conjunto completo de derechos de directivas de DRM. No se admiten derechos de directiva DRM que no sean de flujo, como los Grupos de dominios de dispositivos. La Xbox360 ignora los derechos no compatibles al intentar reproducir contenido.

Los derechos compatibles de la directiva DRM de Primetime para Xbox son:
* Protección de salida digital
* Fecha de finalización del almacenamiento en caché sin conexión de licencia
* Fecha de inicio de la licencia
* Fecha de finalización de la licencia
* Duración de la ventana de reproducción (segundos)

Es posible que el contenido no tenga que volver a empaquetarse para que se transmita a Xbox360 si ya estaba empaquetado para otra plataforma de Primetime, como iOS, Android o Escritorio.

Una advertencia con Xbox360 es que siempre debe llegar a un servidor de claves cada vez que se encuentra una etiqueta EXT-X-KEY en el M3U8. A diferencia de iOS, donde una configuración de directiva DRM (policy.requiredKeyServer) hará que el reproductor de vídeo iOS Primetime recupere la clave de descifrado AES de localhost, Xbox siempre intentará recuperar la clave de descifrado de un servidor de claves remoto . No hay ninguna directiva de DRM que indique a la aplicación Xbox que recupere el descifrado de AES
clave de localhost. Debido a este requisito, las entradas EXT-X-KEY deben estar en la M3U8 que apunten al extremo DRM de Primetime Cloud. Esta URL se establece mediante &lt;key_url> en el archivo de configuración OfflinePackager.jar config_hls.xml.

Si desea empaquetar contenido una vez y hacer que se transmita a todos los destinos de Primetime, así como configurar los dispositivos iOS para que no recuperen una clave de un servidor de claves remoto, puede empaquetar el contenido utilizando una directiva DRM que tenga la propiedad policy.requiredKeyServer=false (como en policy_ios_localkeyserver.pol). Los dispositivos iOS recuperarán la clave AES localmente, mientras que los dispositivos Xbox ignorarán esta propiedad y se pondrán en contacto con el servidor de claves DRM de Primetime Cloud
para una clave de descifrado.

>!Nota
>
>Todas las solicitudes de Xbox360 deben utilizar Autenticación personalizada/>Derecho. Esto se debe a que en la plataforma Xbox360, Xbox Live >utiliza un token de Xbox Secure Token Server (XSTS) para >fines de autenticación.
>El servidor de licencias DRM de Primetime Cloud utiliza el token XSTS para >validar la integridad tanto del dispositivo Xbox como del usuario que realiza >la solicitud de licencia. Sin embargo, la validación del token XSTS requiere una >clave privada del proveedor de Xbox Live del cliente, que Primetime Cloud DRM >no almacena. Debido a esto, cuando Primetime Cloud DRM recibe >una solicitud de licencia de un cliente Xbox 360, Primetime Cloud DRM >reenviará el token XSTS al servidor back-end del cliente Primetime >Autenticación/Derecho. El servidor del cliente de Primetime
>a continuación, analizará y validará el token XSTS para asegurarse de que se >firmó con la clave del editor de la aplicación del cliente.
>Para pasar un token XSTS desde el cliente Xbox360, establezca el token >sincrónicamente en respuesta al evento MediaPlayer.RequestKeyAttribute >que se describe más detalladamente aquí: **Establezca el token XSTS en su reproductor.** Un servidor back-end de autenticación/derechos de muestra >se incluye con la versión del software en el directorio Autenticación personalizada >y Derecho.La validación de los tokens XSTS se analiza >en más detalle aquí:  **Validación de tokens de Xbox Live XSTS.**


## Establezca el token XSTS en su reproductor {#set-the-xsts-token-in-your-player}

En Xbox360, establece el token asincrónicamente en respuesta al evento `MediaPlayer.RequestKeyAttribute`.

Establezca el token XSTS.

La aplicación de ejemplo incluida con el software muestra cómo configurar el token XSTS en el reproductor. Este es el fragmento de código relevante del reproductor de muestra:

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

## Validación de tokens de Xbox Live XSTS {#xbox-live-xsts-token-validation}

Para las solicitudes XSTS, el campo `customerSpecificAuthToken` contiene el token XSTS codificado Base64. El código `XSTSValidator` de muestra examina el token decodificado Base64 para comprobar la existencia del elemento `EncryptedAssertion`; sin embargo, puede usar otros métodos para distinguir entre estas solicitudes y las que no son de Xbox. Por ejemplo, puede usar una dirección URL diferente.

La directiva devuelta en el mensaje de respuesta anulará la directiva original en los metadatos DRM suministrados con la solicitud de clave Xbox. El cliente Xbox solo admite un subconjunto de características de directivas, y estos campos son los únicos que anularán la directiva original.

Se necesitan pasos de configuración adicionales para admitir el descifrado y la validación de tokens. Debe cargar las credenciales [!DNL xsts_partner_cert.pfx] y [!DNL x_secure_token_service.part.xboxlive.com.cer] en un almacén de claves en formato JKS, que luego proporcionará a su servidor de autorizaciones back-end como propiedad del sistema `xsts-keystore`. De forma predeterminada, el socio [!DNL .pfx] tiene el alias `xsts` y el certificado de validación del token tiene el alias `xsts-verify-cert`. También puede anularlos utilizando las propiedades del sistema. Finalmente, existe una propiedad del sistema `xsts-keystore-password` que no tiene valor predeterminado y que contiene la contraseña del almacén de claves. Las propiedades del sistema leídas por el código `XSTSValidator` se resumen a continuación:

| Propiedad System | Valor predeterminado | Comentario |
|---|---|---|
| xsts-keystore | xsts.jks | Almacén de claves en formato JKS utilizado por el validador. |
| xsts-keystore-password |  | Contraseña del almacén de claves |
| xsts-alias | xsts | Alias utilizado para recuperar la clave de descifrado del almacén de claves |
| xsts-verify-cert-alias | xsts-verify-cert | Alias utilizado para recuperar el certificado de validación del almacén de claves |

## Crear JKS para un validador XSTS{#create-jks-for-an-xsts-validator}

1. Descubra el nombre de alias del certificado privado, ubicado en el archivo del socio [!DNL .pfx].

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Convierta [!DNL .pfx] a [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (donde `<alias>` es el nombre de alias del certificado privado que ha descubierto en el paso 1).
1. Importar [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Coloque [!DNL xsts.jks] en el directorio raíz de Tomcat y defina `-Dxsts-keystore-password=****` para Tomcat.

Si [!DNL xsts_partner_cert.pfx] y [!DNL xsts.jks] están utilizando contraseñas diferentes, actualice la contraseña `xsts` en `jks` para que sean la misma.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
