---
description: Aunque el método de codificación AES-128 cifra todo el contenedor de flujo de transporte (TS), incluidos los encabezados, el cifrado SAMPLE-AES sólo cifra el audio y parte de los datos del vídeo.
seo-description: Aunque el método de codificación AES-128 cifra todo el contenedor de flujo de transporte (TS), incluidos los encabezados, el cifrado SAMPLE-AES sólo cifra el audio y parte de los datos del vídeo.
seo-title: Flujos HLS cifrados AES de muestra
title: Flujos HLS cifrados AES de muestra
uuid: 32c1f87b-eb81-4e1c-92ea-ec37260a7ecb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Flujos HLS cifrados AES de muestra{#sample-aes-encrypted-hls-streams}

Aunque el método de codificación AES-128 cifra todo el contenedor de flujo de transporte (TS), incluidos los encabezados, el cifrado SAMPLE-AES sólo cifra el audio y parte de los datos del vídeo.

En los flujos cifrados, se identifica un bloque protegido sobre el cual se completa el proceso de protección. Los bloques protegidos por vídeo H.264 son el cuerpo de los tipos 1 y 5 de unidades de capa de adaptación de red (NAL). Un bloque de audio protegido es un marco de audio y el audio debe estar en formato AAC.

>[!IMPORTANT]
>
>Debe tener la clave y el vector de inicialización (IV). El SDK del explorador utiliza la clave y la IV para descifrar el flujo antes de reproducirlo.

Cada bloque protegido contiene un entero de bloques de 16 bytes cifrados con el modo de encadenado de bloques de cifrado AES-128 (CBC) sin relleno. CBC se produce en cada bloque protegido y, en el inicio de cada nuevo bloque protegido, la IV debe restablecerse a su valor original.

Se admiten los siguientes códecs:

* Para vídeo, se admite H.264.
* Para audio, sample-AES solo se admite para AAC.

