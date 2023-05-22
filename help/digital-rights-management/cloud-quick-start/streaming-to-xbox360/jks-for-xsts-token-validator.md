---
title: Crear JKS para un validador de XSTS
description: Crear JKS para un validador de XSTS
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# Crear JKS para un validador de XSTS{#create-jks-for-an-xsts-validator}

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
