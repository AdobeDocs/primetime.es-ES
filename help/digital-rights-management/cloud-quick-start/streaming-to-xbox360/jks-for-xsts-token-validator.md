---
title: Creación de JKS para un validador XSTS
description: Creación de JKS para un validador XSTS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# Crear JKS para un validador XSTS{#create-jks-for-an-xsts-validator}

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
