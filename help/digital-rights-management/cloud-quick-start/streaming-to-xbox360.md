---
description: 'null'
seo-description: 'null'
seo-title: Configure el token XSTS en el reproductor
title: Configure el token XSTS en el reproductor
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: c37061c116b8a6bc8ce085dc89dc8aadd0a2e490
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---


# Flujo a Xbox360 (opcional) {#streaming-to-xboc360}

Primetime DRM está disponible en la plataforma Xbox360. Sin embargo, solo se admite el caso de uso de flujo protegido, no el grupo completo de derechos de directiva DRM. No se admiten los derechos de directiva DRM que no sean de flujo, como los grupos de dominios de dispositivo. La Xbox360 ignora los derechos no admitidos al intentar reproducir contenido.

Los derechos de directiva DRM de Primetime admitidos para Xbox son:
* Protección de salida digital
* Fecha de finalización del almacenamiento en caché sin conexión de licencia
* Fecha de Inicio de licencia
* Fecha de finalización de licencia
* Duración de la ventana de reproducción (segundos)

Es posible que el contenido no tenga que volver a empaquetarse para que se transmita a Xbox360, si ya se ha empaquetado para otra plataforma Primetime, como iOS, Android o Desktop.

Una advertencia con Xbox360 es que siempre debe llegar a un servidor de claves cada vez que se encuentra una etiqueta EXT-X-KEY en el M3U8. A diferencia de iOS, donde una configuración de directiva DRM (policy.requiredKeyServer) hará que el reproductor de vídeo Primetime de iOS recupere la clave de descifrado de AES desde localhost, Xbox siempre intentará recuperar la clave de descifrado desde un servidor de claves remoto. No hay ninguna directiva de DRM que indique a la aplicación de Xbox que recupere el descifrado de AES
de localhost. Debido a este requisito, las entradas EXT-X-KEY deben estar en la M3U8 que apuntan al extremo DRM de Primetime Cloud. Esta dirección URL se establece mediante &lt;key_url> en el archivo de configuración OfflinePackager.jar config_hls.xml.

Si desea empaquetar contenido una vez y hacer que se transmita a todos los destinatarios Primetime, así como configurar dispositivos iOS para que no recuperen una clave de un servidor de claves remoto, puede empaquetar el contenido mediante una directiva DRM que tenga la propiedad policy.requireKeyServer=false (como en policy_ios_localkeyserver.pol). Los dispositivos iOS recuperarán la clave AES localmente, mientras que los dispositivos Xbox omitirán esta propiedad y se conectarán al servidor de claves DRM de Primetime Cloud
para una clave de descifrado.

>!Nota
>
>Todas las solicitudes de Xbox360 deben utilizar Autenticación personalizada/>Asignación de derechos. Esto se debe a que en la plataforma Xbox360, Xbox Live >utiliza un token de Xbox Secure Token Server (XSTS) para >propósitos de autenticación.
>El servidor de licencias DRM de Primetime Cloud utiliza el token XSTS para >validar la integridad tanto del dispositivo Xbox como del usuario que realiza >la solicitud de licencia. Sin embargo, la validación del token XSTS requiere una clave de proveedor de Xbox Live privada de >cliente, que Primetime Cloud DRM >no almacena. Debido a esto, cuando Primetime Cloud DRM recibe >una solicitud de licencia de un cliente Xbox 360, Primetime Cloud DRM >reenviará el token XSTS al servidor Back-End >Authentication/Entitlement del cliente Primetime. El servidor del cliente Primetime
>luego analizará y validará el token XSTS para asegurarse de que se >firmó usando la clave del editor de la aplicación del cliente.
>Para pasar un token XSTS desde el cliente Xbox360, establezca el token >sincrónicamente en respuesta a MediaPlayer.RequestKeyAttribute >evento - descrito en detalle aquí: **Configure el token XSTS en el reproductor.** Se incluye un ejemplo de servidor de autenticación/asignación de derechos del back-end >con la versión de software en el directorio Autenticación personalizada >y asignación de derechos.La validación de los tokens XSTS se analiza >en detalle aquí:  **Validación del token XSTS de Xbox Live.**


## Configure el token XSTS en el reproductor {#set-the-xsts-token-in-your-player}

En Xbox360, configuras el token asincrónicamente en respuesta al evento `MediaPlayer.RequestKeyAttribute`.

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

## Validación del token XSTS de Xbox Live {#xbox-live-xsts-token-validation}

Para las solicitudes XSTS, el campo `customerSpecificAuthToken` contendrá el token XSTS codificado Base64. El código de muestra `XSTSValidator` examina el token descodificado Base64 para la existencia del elemento `EncryptedAssertion`; sin embargo, puede usar otros métodos para distinguir entre estas solicitudes y las que no son de Xbox. Por ejemplo, puede usar una dirección URL diferente.

La directiva devuelta en el mensaje de respuesta anulará la directiva original en los metadatos de DRM suministrados con la solicitud de clave de Xbox. Solo el cliente Xbox admite un subconjunto de funciones de política, y estos campos son los únicos que anularán la directiva original.

Se necesitan pasos de configuración adicionales para admitir la descodificación y validación de tokens. Debe cargar las credenciales [!DNL xsts_partner_cert.pfx] y [!DNL x_secure_token_service.part.xboxlive.com.cer] en un almacén de claves de formato JKS, que luego proporciona al servidor de asignación de derechos back-end como propiedad del sistema `xsts-keystore`. De forma predeterminada, el socio [!DNL .pfx] tiene el alias `xsts` y el certificado de validación del token tiene el alias `xsts-verify-cert`. También puede omitirlas mediante las propiedades del sistema. Finalmente, existe una propiedad del sistema `xsts-keystore-password` que no tiene valor predeterminado y que contiene la contraseña del almacén de claves. Las propiedades del sistema leídas por el código `XSTSValidator` se resumen a continuación:

| Propiedad System | Valor predeterminado | Comentario |
|---|---|---|
| xsts-keystore | xsts.jks | Almacén de claves de formato JKS utilizado por el validador. |
| xsts-keystore-password |  | Contraseña para el almacén de claves |
| xsts-alias | xsts | Alias utilizado para recuperar la clave de descifrado del almacén de claves |
| xsts-verify-cert-alias | xsts-verify-cert | Alias utilizado para recuperar el certificado de validación del almacén de claves |

## Crear JKS para un validador XSTS{#create-jks-for-an-xsts-validator}

1. Descubra el nombre de alias del certificado privado, ubicado en el archivo [!DNL .pfx] del socio.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Convierta [!DNL .pfx] a [!DNL .jks].

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

1. Coloque [!DNL xsts.jks] en el directorio principal de Tomcat y defina `-Dxsts-keystore-password=****` para Tomcat.

Si [!DNL xsts_partner_cert.pfx] y [!DNL xsts.jks] están utilizando contraseñas diferentes, actualice la contraseña `xsts` en `jks` para que sean iguales.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
