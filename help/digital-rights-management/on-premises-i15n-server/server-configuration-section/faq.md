---
title: FAQ
description: FAQ
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
