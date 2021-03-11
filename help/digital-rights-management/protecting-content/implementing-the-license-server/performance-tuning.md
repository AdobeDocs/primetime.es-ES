---
title: Ajuste del rendimiento
description: Ajuste del rendimiento
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Ajuste de rendimiento{#performance-tuning}

Utilice los siguientes consejos para aumentar el rendimiento:

* El uso de un HSM de red puede ser significativamente más lento que el uso de un HSM conectado directamente.
* Para mejorar el rendimiento, si lo desea, puede habilitar la compatibilidad nativa con las operaciones criptográficas mediante la implementación de las bibliotecas específicas de la plataforma que se encuentran en la carpeta [!DNL thirdparty/cryptoj] del SDK. Para habilitar el soporte nativo, agregue la biblioteca para su plataforma (jsafe.dll para Windows o libjsafe.so para Linux) a la ruta.

   >[!NOTE]
   >
   >Si ejecuta varias aplicaciones web en la misma instancia de Tomcat y tiene `jsafe.dll` en la ruta, solo la primera aplicación web que carga puede cargar la biblioteca `jsafe.dll`. Por lo tanto, solo la primera aplicación web obtiene el beneficio del soporte nativo. En estos casos, para mejorar el rendimiento de todas las aplicaciones web, coloque `cryptoj.jar`fuera del archivo WAR. Por ejemplo, en el directorio `<tomcat_installation_folder>/lib`.

* Un sistema operativo de 64 bits, como la versión de 64 bits de Red Hat® o Windows, proporciona un rendimiento mucho mejor que un sistema operativo de 32 bits.

## Generación de números aleatorios (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

Bajo ciertas condiciones, los entornos Linux pueden pausarse al realizar operaciones relacionadas con DRM de Primetime que requieren generación aleatoria de números, incluyendo:

* Inicio del servidor de licencias DRM de Adobe Primetime
* Generación de directivas mediante la utilidad [!DNL AdobePolicyManager]
* Empaquetado de contenido protegido con DRM con Adobe Medium Server o Primetime OfflinePackager

Los retrasos durante estas operaciones son a menudo el resultado de un pool de baja entropía en su servidor Linux.

En Linux, se generan números aleatorios a partir del grupo de entropía del entorno del servidor. El grupo de entropía se mantiene normalmente recibiendo interrupciones de hardware por parte del núcleo Linux. Si un servidor está aislado y no recibe entradas regulares de los recursos de hardware (como un ratón o un teclado), las esperas para rellenar el grupo de entropía pueden ampliarse. En este escenario, es posible que se detengan las operaciones que esperan datos de [!DNL /dev/random].

Puede usar generadores de números aleatorios de hardware en servidores Linux para garantizar que se genere suficiente entropía. Sin embargo, si los generadores de números aleatorios de hardware no están disponibles en un escenario de implementación determinado, puede utilizar soluciones basadas en software para aumentar la tasa de actualización del grupo de entropía. Una de estas soluciones de software en Linux es [!DNL haveged] (daemon de recolección y expansión de entropía volátil de HArdware).

## Determinación de la Entropía Disponible {#section_686B311FE6144566B6939E9F20915ADC}

Para verificar el número de bits disponibles en el grupo de entropía de un servidor determinado durante un retraso inesperado, ejecute el siguiente comando:

```
cat /proc/sys/kernel/random/entropy_avail 
```

Un sistema Linux sano con mucha entropía disponible volverá casi a los 4.096 bits completos de entropía. Si el valor devuelto es menor que 200, el sistema se ejecuta muy poco en entropía.
