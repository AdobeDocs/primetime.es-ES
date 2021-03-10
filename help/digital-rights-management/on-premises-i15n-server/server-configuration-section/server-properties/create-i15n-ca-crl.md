---
title: Crear CRL de CA de individualización
description: Crear CRL de CA de individualización
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Crear CRL de CA de individualización{#create-individualization-ca-crl}

Este punto de distribución Lista de revocación de certificados (CRL) se incluye en cada certificado de equipo emitido por el servidor de individualización. Durante la validación del certificado del equipo en el servidor de licencias, esta CRL se descargará desde el punto de distribución indicado en el certificado (o se leerá desde la caché si ya se ha descargado) y se comprobará para asegurarse de que el certificado no se haya revocado.

>[!NOTE]
>
>Para establecer la URL del punto de distribución CRL, deberá establecer el campo [!DNL AdobeInitial.properties] `cert.machine.crldp` . Este punto de distribución es *not* verificado por Primetime DRM para su validez. Debe verificar que esta dirección URL sea válida. Los errores resultantes de una dirección URL no válida no aparecerán hasta que aparezcan errores de validación del servidor de licencias.

A continuación se describen las instrucciones simplificadas de ejemplo para usar OpenSSL para crear listas CRL que su servidor de licencias puede consumir. Adobe recomienda que realice estos pasos de forma segura y en un entorno seguro, una vez que se haya obtenido una credencial de CA de Individualización de producción.

1. Cambie el directorio de trabajo al directorio [!DNL create_crl] incluido en esta distribución.
1. Copie su CA de Individualización [!DNL pfx] en el mismo directorio [!DNL create_crl].

   Los pasos siguientes suponen que el pfx de CA de Individualización se llama [!DNL i15n.pfx]. Ajuste según su configuración.
1. Extraiga la clave privada del archivo Individualization CA [!DNL pfx].

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Convierta la clave privada al formato [!DNL pksc8] .

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Genere la CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   En este ejemplo se crea una CRL con un periodo de validez de 1 mes predeterminado. Utilice las opciones `-crldays` y `-crlhours` para anular los valores predeterminados.

   La generación de una CRL utiliza el archivo [!DNL index] y [!DNL crlnumber] indicado en su [!DNL openssl.conf]. De forma predeterminada, se utiliza la ubicación [!DNL demoCA] en el directorio de trabajo. Los archivos de muestra [!DNL index] y [!DNL crlnumber] se incluyen en el directorio proporcionado [!DNL demoCA].

1. Implemente el archivo CRL generado en el paso anterior en una ubicación adecuada a la que pueda acceder el servidor de licencias (por ejemplo: servidor de individualización [!DNL ROOT]).
1. Reinicie el servidor de licencias una vez que la CRL esté implementada.
