---
title: Configurar y ejecutar las herramientas de la línea de comandos
description: Configurar y ejecutar las herramientas de la línea de comandos
copied-description: true
exl-id: ff0d4316-24e6-4a34-b332-abd737d6fcf9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Configurar y ejecutar las herramientas de la línea de comandos {#configure-and-run-the-command-line-tools}

Las herramientas de la línea de comandos tienen propiedades asociadas para las que se deben establecer valores en [!DNL flashaccesstools.properties] *antes* ejecuta las herramientas. Algunas de las herramientas de la línea de comandos también permiten especificar valores de propiedad desde la línea de comandos. Los valores especificados desde la línea de comandos tienen prioridad sobre los valores proporcionados desde [!DNL flashaccesstools.properties].

Debe modificar la configuración en las siguientes secciones de [!DNL flashaccesstools.properties] para habilitar las herramientas de línea de comandos correspondientes que desea utilizar:

* **Propiedades del empaquetador de medios** - (para [!DNL AdobePackager.jar])

* **Propiedades del Administrador de listas de actualización de directivas y del Administrador de listas de revocación** - (para [!DNL AdobePolicyUpdateListManager.jar] y [!DNL AdobeRevocationListManager.jar])

* **Propiedades del Administrador de directivas** - (para [!DNL AdobePolicyManager.jar])

* **Propiedades del generador de licencias** - (para [!DNL AdobeLicenseGenerator.jar])
