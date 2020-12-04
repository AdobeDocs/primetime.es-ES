---
seo-title: Configurar y ejecutar las herramientas de la línea de comandos
title: Configurar y ejecutar las herramientas de la línea de comandos
uuid: b65f8621-54fa-4927-b2f4-d2fd60350fc1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Configurar y ejecutar las herramientas de la línea de comandos {#configure-and-run-the-command-line-tools}

Las herramientas de la línea de comandos tienen propiedades asociadas para las que debe establecer valores en [!DNL flashaccesstools.properties] *antes de* ejecutar las herramientas. Algunas de las herramientas de la línea de comandos también permiten especificar valores de propiedad desde la línea de comandos. Los valores que especifique desde la línea de comandos tienen prioridad sobre los valores que proporcione desde [!DNL flashaccesstools.properties].

Debe modificar la configuración en las siguientes secciones de [!DNL flashaccesstools.properties] para habilitar las herramientas de línea de comandos correspondientes que desee utilizar:

* **Propiedades**  de Media Packager: (para  [!DNL AdobePackager.jar])

* **Propiedades**  del Administrador de Listas de actualización de directivas y del Administrador de Listas de revocación: (para  [!DNL AdobePolicyUpdateListManager.jar] y  [!DNL AdobeRevocationListManager.jar])

* **Propiedades**  del Administrador de directivas: (para  [!DNL AdobePolicyManager.jar])

* **Propiedades**  del generador de licencias: (para  [!DNL AdobeLicenseGenerator.jar])