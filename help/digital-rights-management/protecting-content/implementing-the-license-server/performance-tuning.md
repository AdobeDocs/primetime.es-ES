---
seo-title: Ajuste del rendimiento
title: Ajuste del rendimiento
uuid: db8889c7-ecf5-4551-a6fc-1d3ab992b9ff
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Ajuste del rendimiento{#performance-tuning}

Utilice las siguientes sugerencias para ayudar a aumentar el rendimiento:

* El uso de un HSM de red puede ser considerablemente más lento que el uso de un HSM conectado directamente.
* Para mejorar el rendimiento, opcionalmente puede habilitar la compatibilidad nativa con operaciones criptográficas mediante la implementación de las bibliotecas específicas de la plataforma ubicadas en la carpeta [!DNL thirdparty/cryptoj] del SDK. Para habilitar la compatibilidad nativa, agregue la biblioteca para su plataforma (jsafe.dll para Windows o libjsafe.so para Linux) a la ruta.

   >[!NOTE]
   >
   >Si ejecuta varias aplicaciones web en la misma instancia de Tomcat y tiene `jsafe.dll` en la ruta, sólo la primera aplicación web que se cargue podrá cargar la biblioteca `jsafe.dll`. Por lo tanto, solo la primera aplicación web obtiene el beneficio de la compatibilidad nativa. En esos casos, para mejorar el rendimiento de todas las aplicaciones Web, coloque `cryptoj.jar`fuera del archivo WAR. Por ejemplo, en el directorio `<tomcat_installation_folder>/lib`.

* Un sistema operativo de 64 bits, como la versión de 64 bits de Red Hat® o Windows, ofrece un rendimiento mucho mejor que un sistema operativo de 32 bits.

## Generación de números aleatorios (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

Bajo ciertas condiciones, los entornos Linux pueden detenerse al realizar operaciones relacionadas con DRM de Primetime que requieren generación aleatoria de números, incluyendo:

* Inicio del servidor de licencias DRM de Adobe Primetime
* Generación de políticas mediante la utilidad [!DNL AdobePolicyManager]
* Empaquetado de contenido protegido con DRM con Adobe Media Server o Primetime OfflinePackager

Los retrasos durante estas operaciones son a menudo el resultado de un pool de baja entropía en su servidor Linux.

En Linux, los números aleatorios se generan a partir del grupo de entropía del entorno del servidor. El grupo de entropía normalmente se mantiene recibiendo interrupciones de hardware por parte del núcleo Linux. Si un servidor está aislado y no recibe entradas regulares de recursos de hardware (como un ratón o un teclado), se pueden ampliar las esperas para rellenar el grupo de entropía. En este escenario, es posible que las operaciones que esperan datos de [!DNL /dev/random] se detengan.

Puede utilizar generadores de números aleatorios de hardware en servidores Linux para garantizar que se genera suficiente entropía. Sin embargo, si los generadores de números aleatorios de hardware no están disponibles en un escenario de implementación determinado, puede utilizar soluciones basadas en software para aumentar la frecuencia de actualización del grupo de entropía. Una de estas soluciones de software en Linux es [!DNL haveged] (daemon de recopilación y expansión de entropía volátil HArdware).

## Determinación de la Entropía Disponible {#section_686B311FE6144566B6939E9F20915ADC}

Para verificar el número de bits disponibles en el grupo de entropía de un servidor determinado durante un retraso inesperado, ejecute el siguiente comando:

```
cat /proc/sys/kernel/random/entropy_avail 
```

Un sistema Linux saludable con mucha entropía disponible regresará cerca de los 4.096 bits completos de entropía. Si el valor devuelto es menor que 200, el sistema está funcionando muy bajo en entropía.
