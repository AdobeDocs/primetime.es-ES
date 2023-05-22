---
title: Obtener certificados de CA de dominio
description: Obtener certificados de CA de dominio
copied-description: true
exl-id: cad233e0-41f7-4897-ab5f-d5a098c37306
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Obtener certificados de CA de dominio{#obtain-domain-ca-certificates}

A diferencia del servidor de licencias, el empaquetador o el certificado de transporte, el certificado de CA de dominio no se emite por Adobe. Puede obtener este certificado de una entidad emisora de certificados o generar un certificado autofirmado para utilizarlo con este fin.

El certificado de CA de dominio debe utilizar una clave de 1024 bits y contener los atributos estándar requeridos en un certificado de CA:

* Extensión de restricciones básicas con el indicador de CA establecido en true
* Extensión de uso de claves que especifica que se permite la firma de certificado

Por ejemplo, con OpenSSL, se puede generar un certificado de CA autofirmado de la siguiente manera:

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
