---
title: Crear CRL de CA de individualización
description: Crear CRL de CA de individualización
copied-description: true
exl-id: 72147209-1337-4aed-9e4e-210c905c55a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Crear CRL de CA de individualización{#create-individualization-ca-crl}

Este punto de distribución de lista de revocación de certificados (CRL) se incluye dentro de cada certificado de equipo emitido por el servidor de individualización. Durante la validación del certificado del equipo en el servidor de licencias, esta CRL se descargará desde el punto de distribución indicado en el certificado (o se leerá desde la caché si ya se ha descargado) y se comprobará que el certificado no se haya revocado.

>[!NOTE]
>
>Para establecer la dirección URL del punto de distribución CRL, deberá establecer la dirección URL [!DNL AdobeInitial.properties] `cert.machine.crldp` field. Este punto de distribución es *no* comprobado por DRM de Primetime para la validez. Debe comprobar que esta dirección URL es válida. Los errores que se deriven de una dirección URL no válida no se verán hasta que aparezcan errores de validación en el servidor de licencias.

A continuación se describen instrucciones de ejemplo simplificadas para utilizar OpenSSL para crear CRL que el servidor de licencias pueda consumir. El Adobe recomienda que realice estos pasos de forma y en un entorno seguros, una vez que se haya obtenido una credencial de CA de Production Individualization.

1. Cambie el directorio de trabajo a [!DNL create_crl] directorio incluido en esta distribución.
1. Copie su CA de individualización [!DNL pfx] a lo mismo [!DNL create_crl] directorio.

   Los pasos siguientes suponen que el pfx de la CA de individualización tiene el nombre [!DNL i15n.pfx]. Ajuste según corresponda para su configuración.
1. Extraer la CA de individualización [!DNL pfx] clave privada del archivo.

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Convierta la clave privada en [!DNL pksc8] formato.

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Genere la CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   En este ejemplo se crea una CRL con un período de validez predeterminado de un mes. Utilice el `-crldays` y `-crlhours` opciones para anular los valores predeterminados.

   La generación de una CRL utiliza el [!DNL index] y [!DNL crlnumber] archivo señalado en su [!DNL openssl.conf]. De forma predeterminada, la variable [!DNL demoCA] ubicación en el directorio de trabajo. Muestra [!DNL index] y [!DNL crlnumber] Los archivos de se incluyen en el [!DNL demoCA] directorio.

1. Implemente el archivo CRL generado en el paso anterior en una ubicación adecuada a la que pueda acceder el servidor de licencias (por ejemplo: servidor de individualización [!DNL ROOT]).
1. Reinicie el servidor de licencias una vez que se haya establecido la CRL.
