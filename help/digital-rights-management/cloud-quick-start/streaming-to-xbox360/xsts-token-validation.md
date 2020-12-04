---
seo-title: Validación del token XSTS de Xbox Live
title: Validación del token XSTS de Xbox Live
uuid: 9647f8ee-32d6-4bed-bae2-8b36a72d04ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Validación del token XSTS de Xbox Live{#xbox-live-xsts-token-validation}

Para las solicitudes XSTS, el campo `customerSpecificAuthToken` contendrá el token XSTS codificado Base64. El código de muestra `XSTSValidator` examina el token descodificado Base64 para la existencia del elemento `EncryptedAssertion`; sin embargo, puede usar otros métodos para distinguir entre estas solicitudes y las que no son de Xbox. Por ejemplo, puede usar una dirección URL diferente.

La directiva devuelta en el mensaje de respuesta anulará la directiva original en los metadatos de DRM suministrados con la solicitud de clave de Xbox. Solo el cliente Xbox admite un subconjunto de funciones de política, y estos campos son los únicos que anularán la directiva original.

Se necesitan pasos de configuración adicionales para admitir la descodificación y validación de tokens. Debe cargar las credenciales [!DNL xsts_partner_cert.pfx] y [!DNL x_secure_token_service.part.xboxlive.com.cer] en un almacén de claves de formato JKS, que luego proporciona al servidor de asignación de derechos back-end como propiedad del sistema `xsts-keystore`. De forma predeterminada, el socio [!DNL .pfx] tiene el alias `xsts` y el certificado de validación del token tiene el alias `xsts-verify-cert`. También puede omitirlas mediante las propiedades del sistema. Finalmente, existe una propiedad del sistema `xsts-keystore-password` que no tiene valor predeterminado y que contiene la contraseña del almacén de claves. Las propiedades del sistema leídas por el código `XSTSValidator` se resumen a continuación:

| Propiedad System | Valor predeterminado | Comentario |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | Almacén de claves de formato JKS utilizado por el validador. |
| `xsts-keystore-password` |  | Contraseña para el almacén de claves |
| `xsts-alias` | `xsts` | Alias utilizado para recuperar la clave de descifrado del almacén de claves |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias utilizado para recuperar el certificado de validación del almacén de claves |

