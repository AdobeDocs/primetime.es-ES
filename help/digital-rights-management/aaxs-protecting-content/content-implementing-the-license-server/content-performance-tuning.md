---
title: Ajuste del rendimiento
description: Ajuste del rendimiento
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Ajuste de rendimiento{#performance-tuning}

Utilice los siguientes consejos para aumentar el rendimiento:

* El uso de un HSM de red puede ser significativamente más lento que el uso de un HSM conectado directamente.
* Para mejorar el rendimiento, opcionalmente, puede habilitar la compatibilidad nativa con las operaciones criptográficas mediante la implementación de las bibliotecas específicas de la plataforma ubicadas en la carpeta &quot;thirdparty/cryptoj&quot; del SDK. Para habilitar el soporte nativo, agregue la biblioteca para su plataforma (jsafe.dll para Windows o libjsafe.so para Linux) a la ruta.

   >[!NOTE]
   >
   >Si ejecuta varias aplicaciones web en la misma instancia de Tomcat y tiene `jsafe.dll` en la ruta, solo la primera aplicación web que carga puede cargar la biblioteca `jsafe.dll`. Por lo tanto, solo la primera aplicación web obtiene el beneficio del soporte nativo. En estos casos, para mejorar el rendimiento de todas las aplicaciones web, coloque `cryptoj.jar`fuera del archivo WAR. Por ejemplo, en el directorio `<tomcat_installation_folder>/lib`.

* Un sistema operativo de 64 bits, como la versión de 64 bits de Red Hat® o Windows, proporciona un rendimiento mucho mejor que un sistema operativo de 32 bits.

