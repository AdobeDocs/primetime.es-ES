---
description: Mientras que el método de cifrado AES-128 cifra todo el contenedor de flujo de transporte (TS), incluidos los encabezados, el cifrado SAMPLE-AES solo cifra el audio y parte de los datos de vídeo.
title: Flujo HLS cifrado AES de muestra
exl-id: 04bda50f-5ca4-4a00-bb5a-97259a2cb005
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Flujo HLS cifrado AES de muestra{#sample-aes-encrypted-hls-streams}

Mientras que el método de cifrado AES-128 cifra todo el contenedor de flujo de transporte (TS), incluidos los encabezados, el cifrado SAMPLE-AES solo cifra el audio y parte de los datos de vídeo.

En los flujos cifrados, se identifica un bloque protegido sobre el que se completa el proceso de protección. Los bloques protegidos por vídeo H.264 son el cuerpo de los tipos 1 y 5 de las unidades de capa de adaptación a la red (NAL). Un bloque de audio protegido es un cuadro de audio, y el audio debe estar en formato AAC.

>[!IMPORTANT]
>
>Debe tener la clave y el vector de inicialización (IV). El TVSDK del explorador utiliza la clave y la IV para descifrar el flujo antes de reproducirlo.

Cada bloque protegido contiene un entero de bloques de 16 bytes que se cifran con el modo de encadenamiento de bloques de cifrado (CBC) AES-128 sin relleno. El hemograma completo se produce en cada bloque protegido y, al comienzo de cada nuevo bloque protegido, el IV debe restablecerse a su valor original.

Se admiten los siguientes códecs:

* Para vídeo, se admite H.264.
* Para el audio, sample-AES solo es compatible con AAC.
