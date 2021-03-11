---
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Glosario {#glossary}

Términos usados con frecuencia que requieren una definición especial.

## Clave de cifrado de contenido {#content-encryption-key}

La clave de cifrado de contenido (CEK), generada por una utilidad, la utiliza posteriormente un empaquetador de contenido para preparar contenido que debe protegerse.
La utilidad genera la clave en hexadecimal con una longitud de 16 bytes.
Esta guía muestra, en notas y mensajes de error, archivos y ejemplos de comandos, las siguientes variantes de nombres de parámetros y nombres de valores para CEK:

* clave de contenido
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

Los nombres de archivo de un CEK se muestran como:

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

El propio CEK puede almacenarse en un sistema de administración de claves, así como cifrarse. Esta guía hace referencia al índice de almacenamiento como CEK Storage ID CEKSID. El término clave de cifrado (KEK) hace referencia a la clave de cifrado de segundo nivel y el término `ek` hace referencia al valor de dicho cifrado.
Algunas llamadas utilizan el CEK y el CEK Storage ID CEKSID, y el CEK recuperado del almacenamiento debe coincidir con el CEK proporcionado en la llamada.
Para HLS Offline con FairPlay, también existe un `persistentContentKey` que puede configurarse para que caduque.

## ID de almacenamiento de clave de cifrado de contenido {#content-encryption-key-storage-id}

El ID de almacenamiento de clave de cifrado de contenido (CEKSID) es un ID para recuperar una clave de cifrado de contenido de un sistema de administración de claves.

El CEKSID también se conoce como
* ID de clave
* ID de contenido
* `&kid`

## Autenticación de cliente {#customer-authenticator}

Clave para la autenticación en solicitudes a la API de Expression. Las solicitudes pueden incluir solicitudes para tokens.