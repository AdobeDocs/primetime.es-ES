---
title: Ajuste del rendimiento
description: Ajuste del rendimiento
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Ajuste del rendimiento{#performance-tuning}

Utilice las siguientes sugerencias para aumentar el rendimiento:

* Usar un HSM de red puede ser significativamente más lento que usar un HSM conectado directamente.
* Para mejorar el rendimiento, puede habilitar opcionalmente la compatibilidad nativa con operaciones criptográficas implementando las bibliotecas específicas de la plataforma ubicadas en la carpeta &quot;third party/cryptoj&quot; del SDK. Para habilitar la compatibilidad nativa, agregue la biblioteca de su plataforma (jsafe.dll para Windows o libjsafe.so para Linux) a la ruta.

  >[!NOTE]
  >
  >Si ejecuta varias aplicaciones web en la misma instancia de Tomcat y tiene `jsafe.dll` en la ruta, solo la primera aplicación web que carga puede cargar el `jsafe.dll` biblioteca. Por lo tanto, solo la primera aplicación web obtiene el beneficio de la compatibilidad nativa. En estos casos, para mejorar el rendimiento de todas las aplicaciones web, coloque `cryptoj.jar`fuera del archivo WAR. Por ejemplo, en la variable `<tomcat_installation_folder>/lib` directorio.

* Un sistema operativo de 64 bits, como la versión de 64 bits de Red Hat® o Windows, proporciona un rendimiento mucho mejor que un sistema operativo de 32 bits.
