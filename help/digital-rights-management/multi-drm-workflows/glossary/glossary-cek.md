---
uuid: 2d927ae8-4c4b-4b64-88b8-9c86430e226c
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Glosario {#glossary}

Términos utilizados con frecuencia que requieren una definición especial.

## Clave de cifrado de contenido {#content-encryption-key}

La clave de cifrado de contenido (CEK), generada por una utilidad, es utilizada posteriormente por un empaquetador de contenido para preparar contenido que debe protegerse.
La utilidad genera la clave en hexadecimal con una longitud de 16 bytes.
Esta guía muestra, en notas y mensajes de error, archivos y ejemplos de comandos, las siguientes variantes de nombres de parámetro y nombres de valor para CEK:

* clave de contenido
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

Los nombres de archivo de un CEK se muestran como:

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

El propio CEK puede almacenarse en un sistema de gestión de claves, así como cifrarse. Esta guía hace referencia al índice de almacenamiento como CEK ID de Almacenamiento. El término Clave de cifrado de clave (KEK) hace referencia a la clave de cifrado de segundo nivel y el término `ek` hace referencia al valor de ese cifrado.
Algunas llamadas utilizan el CEK y el CEK ID de Almacenamiento CEK CEKSID, y el CEK recuperado de almacenamiento debe coincidir con el CEK proporcionado en la llamada.
Para HLS Offline con FairPlay, también hay un `persistentContentKey` que puede configurarse para que caduque.

## ID de Almacenamiento de clave de cifrado de contenido {#content-encryption-key-storage-id}

El ID de Almacenamiento de clave de cifrado de contenido (CEKSID) es un ID para recuperar una clave de cifrado de contenido de un sistema de administración de claves.

El CEKSID también se denomina
* ID de clave
* ID de contenido
* `&kid`

## Autenticación de cliente {#customer-authenticator}

Clave para la autenticación en solicitudes a la API de Express. Las solicitudes pueden incluir solicitudes de tokens.