---
seo-title: Ajuste del rendimiento
title: Ajuste del rendimiento
uuid: bb5321a0-48ef-49cb-aaf0-00d7ab9562fe
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Ajuste del rendimiento{#performance-tuning}

Utilice las siguientes sugerencias para ayudar a aumentar el rendimiento:

* El uso de un HSM de red puede ser considerablemente más lento que el uso de un HSM conectado directamente.
* Para mejorar el rendimiento, si lo desea, puede activar la compatibilidad nativa con operaciones criptográficas mediante la implementación de las bibliotecas específicas de la plataforma situadas en la carpeta &quot;thirdparty/cryptoj&quot; del SDK. Para habilitar la compatibilidad nativa, agregue la biblioteca para su plataforma (jsafe.dll para Windows o libjsafe.so para Linux) a la ruta.

   >[!NOTE]
   >
   >Si ejecuta varias aplicaciones web en la misma instancia de Tomcat y tiene `jsafe.dll` en la ruta, sólo la primera aplicación web que se cargue podrá cargar la biblioteca `jsafe.dll`. Por lo tanto, solo la primera aplicación web obtiene el beneficio de la compatibilidad nativa. En esos casos, para mejorar el rendimiento de todas las aplicaciones Web, coloque `cryptoj.jar`fuera del archivo WAR. Por ejemplo, en el directorio `<tomcat_installation_folder>/lib`.

* Un sistema operativo de 64 bits, como la versión de 64 bits de Red Hat® o Windows, ofrece un rendimiento mucho mejor que un sistema operativo de 32 bits.

