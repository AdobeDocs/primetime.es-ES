---
title: Implementación de los archivos WAR
description: Implementación de los archivos WAR
copied-description: true
exl-id: 9f491596-2a02-4a55-9baa-86407e389d20
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---

# Implementación de los archivos WAR{#deploy-the-war-files}

1. Copie el archivo WAR en el de Tomcat. [!DNL webapps] directorio.

   * Servidor de individualización: [!DNL flashaccess.war]
   * Servidor de generación de claves: [!DNL flashaccess-kgs.war]

1. Copie el [!DNL ROOT] carpeta del paquete proporcionado por el Adobe a [!DNL webapps] directorio.

   El servidor de individualización también debe alojar el [!DNL crossdomain.xml] archivo. (La [!DNL ROOT] La carpeta contiene el [!DNL crossdomain.xml] file; [!DNL ROOT] debe estar en mayúsculas). El servidor de generación de claves no requiere este archivo.
