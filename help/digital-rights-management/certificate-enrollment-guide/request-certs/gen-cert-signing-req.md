---
title: Generar una solicitud de firma de certificado (solicitante)
description: Generar una solicitud de firma de certificado (solicitante)
copied-description: true
exl-id: 4f8dae3d-da56-453d-b3c4-e67fe4f37064
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Generar una solicitud de firma de certificado (solicitante) {#generate-a-certificate-signing-request-requester}

1. Genere un par de claves. Para utilizar una utilidad como OpenSSL, abra una Ventana de comandos e introduzca lo siguiente:

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe recomienda incluir el tipo de certificado (lic, pkgr, trans, trial o eval) en el nombre de clave. Esta convención de nombres facilita su implementación en el servidor de licencias. Este ejemplo utiliza &quot;mycompany-license.key&quot;. Para las versiones de evaluación y prueba, utilice &quot;mycompany-eval.key&quot; y &quot;mycompany-trial.key&quot;.

1. Introduzca una contraseña para proteger la clave privada.

   Las contraseñas deben contener al menos 12 caracteres. Los caracteres deben incluir una mezcla de caracteres ASCII en mayúsculas y minúsculas y números. Para utilizar OpenSSL para generar una contraseña segura, abra una Ventana de comandos e introduzca lo siguiente:

   ```
   openssl rand -base64 8
   ```

1. Generar una solicitud de firma de certificado (CSR).

   Para utilizar OpenSSL para generar una CSR, abra una Ventana de comandos e introduzca lo siguiente:

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. Se le pedirá que introduzca la contraseña de la clave privada.
1. Cree una copia de seguridad de la clave privada y la contraseña.

   Si pierde la clave privada o si se ve comprometida, póngase en contacto con el administrador de certificados de Adobe para revocar el certificado y solicitar uno nuevo.

   >[!NOTE]
   >
   >Adobe recomienda utilizar un HSM para proteger la clave privada y la contraseña.
