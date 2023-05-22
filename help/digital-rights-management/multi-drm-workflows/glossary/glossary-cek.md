---
title: Glosario
description: Términos utilizados con frecuencia que requieren una definición especial.
exl-id: 4e7874f7-c5c0-4f2c-ada2-a0da3ed4d4bf
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Glosario {#glossary}

Términos utilizados con frecuencia que requieren una definición especial.

## Clave de cifrado de contenido {#content-encryption-key}

La clave de cifrado de contenido (CEK), generada por una utilidad, la utiliza posteriormente un empaquetador de contenido para preparar contenido que debe protegerse.
La utilidad genera la clave en hexadecimal con una longitud de 16 bytes.
Esta guía muestra, en notas y mensajes de error, archivos y ejemplos de comandos, las siguientes variantes de nombres de parámetros y nombres de valores para la CEK:

* clave de contenido
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

Los nombres de archivo de una CEK se muestran como:

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

El CEK en sí puede almacenarse en un sistema de administración de claves y cifrarse. Esta guía hace referencia al índice de almacenamiento como CEK Storage ID CEKSID. El término clave de cifrado de clave (KEK) hace referencia a la clave de cifrado de segundo nivel y al término `ek` hace referencia al valor de ese cifrado.
Algunas llamadas utilizan tanto el CEK como el CEK Storage ID CEKSID, y el CEK recuperado del almacenamiento debe coincidir con el CEK proporcionado en la llamada.
Para HLS Offline con FairPlay, también hay un `persistentContentKey` que se puede configurar para que caduque.

## ID de almacenamiento de clave de cifrado de contenido {#content-encryption-key-storage-id}

El ID de almacenamiento de clave de cifrado de contenido (CEKSID) es un ID para recuperar una clave de cifrado de contenido de un sistema de administración de claves.

El CEKSID también se conoce como
* ID de clave
* ID de contenido
* `&kid`

## Autenticador de cliente {#customer-authenticator}

Una clave para la autenticación en solicitudes a la API de Expressplay. Las solicitudes pueden incluir solicitudes de tokens.
