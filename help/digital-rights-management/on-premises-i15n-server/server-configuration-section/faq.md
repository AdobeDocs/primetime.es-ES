---
title: FAQ
description: FAQ
copied-description: true
exl-id: 9058604e-dbab-4df5-89fd-1219c85c7643
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# FAQ {#faq}

* ¿Con qué frecuencia ocurren los cambios en la ECI?
   * Cada vez que se lanza un nuevo cliente DRM de Adobe, se añade un registro de dispositivo ECI.

* ¿Qué tamaño tienen los archivos ECI?
   * Suelen tener menos de 1 kilobyte por registro de dispositivo.

* ¿Qué sucede si al servidor le falta un registro de dispositivo ECI?
   * Esa clase particular de clientes no podrá individualizarse con el servidor de individualización local y se registrarán los errores en los archivos de registro.

* ¿Qué sucede si las CRL de un servidor caducan?
   * El servidor dejará de funcionar correctamente y se registrarán los errores en los archivos de registro.
