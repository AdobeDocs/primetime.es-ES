---
seo-title: Obtención de certificados de CA de dominio
title: Obtención de certificados de CA de dominio
uuid: 41bbe02b-363a-47f4-9cc0-350730b6c787
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Obtener certificados CA de dominio{#obtain-domain-ca-certificates}

A diferencia del certificado de servidor de licencias, Packager o Transport, el certificado de CA de dominio no se emite por Adobe. Puede obtener este certificado de una entidad emisora de certificados o puede generar un certificado autofirmado para utilizarlo con este fin.

El certificado de CA de dominio debe utilizar una clave de 1024 bits y contener los atributos estándar requeridos en un certificado de CA:

* Extensión Restricciones básicas con el indicador de CA establecido en true
* Se permite la extensión Uso de claves que especifica la firma de certificados

Por ejemplo, con OpenSSL, se puede generar un certificado de CA con firma automática de la siguiente manera:

1. Cree un archivo llamado [!DNL ca-extensions.txt] que contenga:

   ```
   keyUsage=critical,keyCertSign  
   basicConstraints=critical,CA:TRUE  
   subjectKeyIdentifier=hash 
   ```

1. Generar clave:

   ```
   openssl genrsa -des3 -out domain-ca.key 1024 
   ```

1. Generar CSR:

   ```
   openssl req -new -key domain-ca.key -out domain-ca.csr 
   ```

1. Generar certificado:

   ```
   openssl x509 -req -days 365 -in domain-ca.csr -signkey domain-ca.key \ 
     -out domain-ca.cer -extfile ca-extensions.txt 
   ```

1. Generar contraseña:

   ```
   openssl rand -base64 8 
   ```

1. Generar PFX:

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```

