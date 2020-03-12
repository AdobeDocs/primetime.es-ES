---
seo-title: Ajuste del rendimiento
title: Ajuste del rendimiento
uuid: db8889c7-ecf5-4551-a6fc-1d3ab992b9ff
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Ajuste del rendimiento{#performance-tuning}

Utilice las siguientes sugerencias para ayudar a aumentar el rendimiento:

* El uso de un HSM de red puede ser considerablemente más lento que el uso de un HSM conectado directamente.
* Para mejorar el rendimiento, si lo desea, puede activar la compatibilidad nativa con operaciones criptográficas mediante la implementación de las bibliotecas específicas de la plataforma situadas en la [!DNL thirdparty/cryptoj] carpeta del SDK. Para habilitar la compatibilidad nativa, agregue la biblioteca para su plataforma (jsafe.dll para Windows o libjsafe.so para Linux) a la ruta.

   >[!NOTE] {class=&quot;- topic/note &quot;}
   >
   >Si ejecuta varias aplicaciones web en la misma instancia de Tomcat y tiene `jsafe.dll` en la ruta, solo la primera aplicación web que se cargue podrá cargar la `jsafe.dll` biblioteca. Por lo tanto, solo la primera aplicación web obtiene el beneficio de la compatibilidad nativa. En esos casos, para mejorar el rendimiento de todas las aplicaciones web, coloque `cryptoj.jar`fuera del archivo de la GUERRA. Por ejemplo, en el `<tomcat_installation_folder>/lib` directorio.

* Un sistema operativo de 64 bits, como la versión de 64 bits de Red Hat® o Windows, ofrece un rendimiento mucho mejor que un sistema operativo de 32 bits.

## Generación de números aleatorios (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

Bajo ciertas condiciones, los entornos Linux pueden pausar al realizar operaciones relacionadas con DRM Primetime que requieren generación aleatoria de números, incluyendo:

* Inicio del servidor de licencias DRM de Adobe Primetime
* Generación de directivas mediante la [!DNL AdobePolicyManager] utilidad
* Empaquetado de contenido protegido con DRM con Adobe Media Server o Primetime OfflinePackager

Los retrasos durante estas operaciones son a menudo el resultado de un pool de baja entropía en su servidor Linux.

En Linux, se generan números aleatorios a partir del pool de entropías del entorno de servidor. El grupo de entropía normalmente se mantiene recibiendo interrupciones de hardware por parte del núcleo Linux. Si un servidor está aislado y no recibe entradas regulares de recursos de hardware (como un ratón o un teclado), se pueden ampliar las esperas para rellenar el grupo de entropía. En este escenario, las operaciones que esperan datos de [!DNL /dev/random] pueden detenerse.

Puede utilizar generadores de números aleatorios de hardware en servidores Linux para garantizar que se genera suficiente entropía. Sin embargo, si los generadores de números aleatorios de hardware no están disponibles en un escenario de implementación determinado, puede utilizar soluciones basadas en software para aumentar la frecuencia de actualización del grupo de entropía. Una de estas soluciones de software en Linux es [!DNL haveged] (daemon de recopilación y expansión de la entropía volátil HArdware).

## Determinación de la entropía disponible {#section_686B311FE6144566B6939E9F20915ADC}

Para verificar el número de bits disponibles en el grupo de entropía de un servidor determinado durante un retraso inesperado, ejecute el siguiente comando:

```
cat /proc/sys/kernel/random/entropy_avail 
```

Un sistema Linux saludable con mucha entropía disponible regresará cerca de los 4.096 bits completos de entropía. Si el valor devuelto es menor que 200, el sistema está funcionando muy bajo en entropía.
