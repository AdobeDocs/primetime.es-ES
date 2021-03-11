---
description: Mientras que el método de cifrado AES-128 cifra todo el contenedor de flujo de transporte (TS), incluidos los encabezados, el cifrado SAMPLE-AES solo cifra el audio y parte de los datos de vídeo.
title: Muestra de flujos HLS cifrados AES
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# Muestra de flujos HLS cifrados AES{#sample-aes-encrypted-hls-streams}

Mientras que el método de cifrado AES-128 cifra todo el contenedor de flujo de transporte (TS), incluidos los encabezados, el cifrado SAMPLE-AES solo cifra el audio y parte de los datos de vídeo.

En los flujos cifrados, se identifica un bloque protegido sobre el que se completa el proceso de protección. Los bloques protegidos por vídeo H.264 son el cuerpo de los tipos 1 y 5 de las unidades de capa de adaptación de red (NAL). Un bloque protegido de audio es un marco de audio, y el audio debe estar en formato AAC.

>[!IMPORTANT]
>
>Debe tener la clave y el vector de inicialización (IV). El SDK del explorador utiliza la clave y IV para descifrar el flujo antes de reproducirlo.

Cada bloque protegido contiene un entero de bloques de 16 bytes cifrados con el modo de encadenado de bloques cifrado (CBC) AES-128 sin relleno. La CBC se produce en cada bloque protegido y al principio de cada nuevo bloque protegido, la IV debe restablecerse a su valor original.

Se admiten los siguientes códecs:

* Para vídeo, se admite H.264.
* Para audio, el AES de muestra solo es compatible con AAC.

