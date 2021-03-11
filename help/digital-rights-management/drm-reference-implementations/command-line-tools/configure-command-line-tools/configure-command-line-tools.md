---
title: Configuración y ejecución de las herramientas de la línea de comandos
description: Configuración y ejecución de las herramientas de la línea de comandos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Configurar y ejecutar las herramientas de línea de comandos {#configure-and-run-the-command-line-tools}

Las herramientas de línea de comandos tienen propiedades asociadas para las que debe establecer valores en [!DNL flashaccesstools.properties] *antes de* que ejecute las herramientas. Algunas de las herramientas de la línea de comandos también permiten especificar valores de propiedad de la línea de comandos. Los valores que especifique desde la línea de comandos tienen prioridad sobre los valores que proporcione desde [!DNL flashaccesstools.properties].

Debe modificar la configuración en las siguientes secciones de [!DNL flashaccesstools.properties] para habilitar las herramientas de línea de comandos correspondientes que desea utilizar:

* **Propiedades de Media Packager** : (para  [!DNL AdobePackager.jar])

* **Administrador de listas de actualizaciones de directivas y Propiedades**  del Administrador de listas de revocaciones: (para  [!DNL AdobePolicyUpdateListManager.jar] y  [!DNL AdobeRevocationListManager.jar])

* **Propiedades**  del Administrador de políticas: (para  [!DNL AdobePolicyManager.jar])

* **Propiedades**  del generador de licencias: (para  [!DNL AdobeLicenseGenerator.jar])