---
seo-title: Crear CRL de CA de individualización
title: Crear CRL de CA de individualización
uuid: f722f3d1-517f-43e3-b892-f9287527fbe6
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Crear CRL de CA de individualización{#create-individualization-ca-crl}

Este punto de distribución de la Lista de revocación de certificados (CRL) se incluye en cada certificado de equipo emitido por el servidor de individualización. Durante la validación de certificados de equipo en el servidor de licencias, esta CRL se descargará desde el punto de distribución enumerado en el certificado (o se leerá desde la caché si ya se ha descargado) y se comprobará para asegurarse de que el certificado no se ha revocado.

>[!NOTE]
>
>Para establecer la URL del punto de distribución CRL, deberá establecer el [!DNL AdobeInitial.properties] campo `cert.machine.crldp` . Primetime DRM *no comprueba* la validez de este punto de distribución. Debe comprobar que esta dirección URL es válida. Los errores que resulten de una dirección URL no válida no aparecerán hasta que aparezcan los errores de validación del servidor de licencias.

Las instrucciones de ejemplo para utilizar OpenSSL para crear listas CRL que el servidor de licencias puede consumir se describen a continuación. Adobe recomienda que realice estos pasos de forma segura y en un entorno, una vez que se haya obtenido una credencial CA de personalización de producción.

1. Cambie el directorio de trabajo al directorio [!DNL create_crl] incluido en esta distribución.
1. Copie la CA de individualización [!DNL pfx] en el mismo [!DNL create_crl] directorio.

   Los pasos siguientes suponen que el pfx de CA de individualización se denomina [!DNL i15n.pfx]. Ajuste según corresponda para la configuración.
1. Extraiga la clave privada del [!DNL pfx] archivo CA de individualización.

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Convierta la clave privada a [!DNL pksc8] formato.

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Genere la CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   En este ejemplo se crea una CRL con un período de validez de 1 mes predeterminado. Utilice las opciones `-crldays` y `-crlhours` para anular los valores predeterminados.

   La generación de una CRL utiliza el archivo [!DNL index] y [!DNL crlnumber] señalado en su [!DNL openssl.conf]. De forma predeterminada, se utiliza la ubicación [!DNL demoCA] en el directorio de trabajo. Los archivos de ejemplo [!DNL index] y [!DNL crlnumber] archivos se incluyen en el [!DNL demoCA] directorio proporcionado.

1. Implemente el archivo CRL generado en el paso anterior en una ubicación adecuada a la que pueda acceder el servidor de licencias (por ejemplo: servidor de individualización [!DNL ROOT]).
1. Reinicie el servidor de licencias una vez que la CRL esté implementada.
