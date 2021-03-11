---
title: Convertir archivos
description: Convertir archivos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Convertir archivos{#convert-files}

Utilizando una utilidad como OpenSSL y la clave privada, el solicitante genera los archivos PKCS#12 (pfx) y PEM/DER introduciendo los siguientes comandos desde una ventana de comandos:

1. Convierta el archivo PKCS#7 en un archivo PEM temporal.

   Para utilizar OpenSSL, abra una ventana de comandos e introduzca lo siguiente:

   ```
   openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem \ 
   -outform PEM -print_certs 
   ```

   >[!NOTE]
   >
   >Este PEM temporal contiene su certificado y los certificados para las CA intermedias. Utilice estos certificados para generar el archivo PFX.

1. Convierta el archivo PEM temporal en un archivo PFX.

   Para utilizar OpenSSL, abra una ventana de comandos e introduzca lo siguiente:

   ```
   openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem \ 
   -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password 
   ```

1. Convierta el archivo PEM temporal en un archivo PEM final.

   Para utilizar OpenSSL, abra una ventana de comandos e introduzca lo siguiente:

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >Aunque no es obligatorio, Adobe recomienda utilizar contraseñas diferentes para la clave privada (private_key_password) y el PFX (pfx_password).

   Este archivo PEM final contiene solamente su certificado.

1. Convierta el archivo PEM en un archivo DER.

   Para utilizar OpenSSL, abra una ventana de comandos e introduzca lo siguiente:

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >Los archivos DER solo son necesarios para el empaquetador de HTTP Dynamic Streaming.

