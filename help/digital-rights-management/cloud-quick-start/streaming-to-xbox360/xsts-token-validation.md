---
title: Validación de token XSTS de Xbox Live
description: Validación de token XSTS de Xbox Live
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Validación de token XSTS de Xbox Live{#xbox-live-xsts-token-validation}

Para solicitudes XSTS, la variable `customerSpecificAuthToken` contendrá el token XSTS codificado en Base64. La muestra `XSTSValidator` El código examina el token descodificado Base64 para detectar la existencia del `EncryptedAssertion` ; sin embargo, puede utilizar otros métodos para distinguir entre estas solicitudes y las solicitudes que no son de Xbox. Por ejemplo, puede utilizar una dirección URL diferente.

La política devuelta en el mensaje de respuesta anulará la política original en los metadatos DRM suministrados con la solicitud de clave Xbox. El cliente Xbox solo admite un subconjunto de características de directiva, y estos campos son los únicos que anularán la directiva original.

Se necesitan pasos de configuración adicionales para admitir el descifrado y la validación de tokens. Debe cargar el [!DNL xsts_partner_cert.pfx] y [!DNL x_secure_token_service.part.xboxlive.com.cer] credenciales en un repositorio de claves en formato JKS, que luego proporciona al servidor de derechos de back-end como propiedad del sistema `xsts-keystore`. De forma predeterminada, el socio [!DNL .pfx] tiene el alias `xsts`y el certificado de validación de token tiene el alias `xsts-verify-cert`. También puede anularlos mediante las propiedades del sistema. Finalmente, hay una propiedad del sistema `xsts-keystore-password` que no tiene valor predeterminado y que contiene la contraseña del almacén de claves. Las propiedades del sistema leídas por el `XSTSValidator` Los códigos se resumen a continuación:

| Propiedad del sistema | Valor predeterminado | Comentario |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | Almacén de claves de formato JKS utilizado por el validador. |
| `xsts-keystore-password` |  | Contraseña del almacén de claves |
| `xsts-alias` | `xsts` | Alias utilizado para recuperar la clave de descifrado del almacén de claves |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias utilizado para recuperar el certificado de validación del almacén de claves |

