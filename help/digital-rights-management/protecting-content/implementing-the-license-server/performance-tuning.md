---
title: Ajuste del rendimiento
description: Ajuste del rendimiento
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Ajuste del rendimiento{#performance-tuning}

Utilice las siguientes sugerencias para aumentar el rendimiento:

* Usar un HSM de red puede ser significativamente más lento que usar un HSM conectado directamente.
* Para mejorar el rendimiento, puede habilitar opcionalmente la compatibilidad nativa con las operaciones criptográficas implementando las bibliotecas específicas de la plataforma ubicadas en el [!DNL thirdparty/cryptoj] del SDK. Para habilitar la compatibilidad nativa, agregue la biblioteca de su plataforma (jsafe.dll para Windows o libjsafe.so para Linux) a la ruta.

  >[!NOTE]
  >
  >Si ejecuta varias aplicaciones web en la misma instancia de Tomcat y tiene `jsafe.dll` en la ruta, solo la primera aplicación web que carga puede cargar el `jsafe.dll` biblioteca. Por lo tanto, solo la primera aplicación web obtiene el beneficio de la compatibilidad nativa. En estos casos, para mejorar el rendimiento de todas las aplicaciones web, coloque `cryptoj.jar`fuera del archivo WAR. Por ejemplo, en la variable `<tomcat_installation_folder>/lib` directorio.

* Un sistema operativo de 64 bits, como la versión de 64 bits de Red Hat® o Windows, proporciona un rendimiento mucho mejor que un sistema operativo de 32 bits.

## Generación de números aleatorios (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

En ciertas condiciones, los entornos Linux pueden pausarse al realizar operaciones relacionadas con DRM de Primetime que requieran generación de números aleatorios, como las siguientes:

* Inicio del servidor de licencias DRM de Adobe Primetime
* Generación de directivas con [!DNL AdobePolicyManager] utilidad
* Empaquetado de contenido protegido por DRM con Adobe Media Server o el Primetime OfflinePackager

Los retrasos durante estas operaciones suelen deberse a un grupo de baja entropía en el servidor Linux.

En Linux, los números aleatorios se generan a partir del grupo de entropía del entorno del servidor. El grupo de entropía normalmente se mantiene recibiendo interrupciones de hardware del núcleo de Linux. Si un servidor está aislado y no recibe entradas regulares de los recursos de hardware (como un ratón o un teclado), es posible que se amplíe la espera para rellenar el grupo de entropía. En esta situación, operaciones que esperan datos de [!DNL /dev/random] puede pausarse.

Puede utilizar generadores de números aleatorios de hardware en servidores Linux para asegurarse de que se genera la entropía suficiente. Sin embargo, si los generadores de números aleatorios de hardware no están disponibles en un escenario de implementación determinado, puede utilizar soluciones basadas en software para aumentar la frecuencia de actualización del grupo de entropía. Una de estas soluciones de software en Linux es [!DNL haveged] (daemon de expansión y recopilación de entropía volátil de hardware).

## Determinación de la entropía disponible {#section_686B311FE6144566B6939E9F20915ADC}

Para verificar el número de bits disponibles en el grupo de entropía de un servidor determinado durante un retraso inesperado, ejecute el siguiente comando:

```
cat /proc/sys/kernel/random/entropy_avail 
```

Un sistema Linux saludable con mucha entropía disponible volverá a tener cerca de los 4.096 bits completos de entropía. Si el valor devuelto es menor de 200, el sistema está ejecutando una entropía muy baja.
