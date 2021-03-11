---
title: Validación de tokens de Xbox Live XSTS
description: Validación de tokens de Xbox Live XSTS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Validación de tokens de Xbox Live XSTS{#xbox-live-xsts-token-validation}

Para las solicitudes XSTS, el campo `customerSpecificAuthToken` contiene el token XSTS codificado Base64. El código `XSTSValidator` de muestra examina el token decodificado Base64 para comprobar la existencia del elemento `EncryptedAssertion`; sin embargo, puede usar otros métodos para distinguir entre estas solicitudes y las que no son de Xbox. Por ejemplo, puede usar una dirección URL diferente.

La directiva devuelta en el mensaje de respuesta anulará la directiva original en los metadatos DRM suministrados con la solicitud de clave Xbox. El cliente Xbox solo admite un subconjunto de características de directivas, y estos campos son los únicos que anularán la directiva original.

Se necesitan pasos de configuración adicionales para admitir el descifrado y la validación de tokens. Debe cargar las credenciales [!DNL xsts_partner_cert.pfx] y [!DNL x_secure_token_service.part.xboxlive.com.cer] en un almacén de claves en formato JKS, que luego proporcionará a su servidor de autorizaciones back-end como propiedad del sistema `xsts-keystore`. De forma predeterminada, el socio [!DNL .pfx] tiene el alias `xsts` y el certificado de validación del token tiene el alias `xsts-verify-cert`. También puede anularlos utilizando las propiedades del sistema. Finalmente, existe una propiedad del sistema `xsts-keystore-password` que no tiene valor predeterminado y que contiene la contraseña del almacén de claves. Las propiedades del sistema leídas por el código `XSTSValidator` se resumen a continuación:

| Propiedad System | Valor predeterminado | Comentario |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | Almacén de claves en formato JKS utilizado por el validador. |
| `xsts-keystore-password` |  | Contraseña del almacén de claves |
| `xsts-alias` | `xsts` | Alias utilizado para recuperar la clave de descifrado del almacén de claves |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias utilizado para recuperar el certificado de validación del almacén de claves |

