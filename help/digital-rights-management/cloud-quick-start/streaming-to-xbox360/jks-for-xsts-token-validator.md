---
seo-title: Creación de JKS para un validador XSTS
title: Creación de JKS para un validador XSTS
uuid: e02b517d-0b72-4e95-92b2-09b8f785cce6
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Creación de JKS para un validador XSTS{#create-jks-for-an-xsts-validator}

1. Averiguar el nombre de alias del certificado privado, ubicado en el [!DNL .pfx] archivo del socio.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Convertir [!DNL .pfx] a [!DNL .jks].

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

1. Ponga [!DNL xsts.jks] en su directorio de inicio de Tomcat y defina `-Dxsts-keystore-password=****` para Tomcat.

Si [!DNL xsts_partner_cert.pfx] y [!DNL xsts.jks] utilizan contraseñas diferentes, actualice la `xsts` contraseña en `jks` para que sean iguales.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
