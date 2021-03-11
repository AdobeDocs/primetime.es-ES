---
title: Implementar los archivos WAR
description: Implementar los archivos WAR
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# Implementar los archivos WAR{#deploy-the-war-files}

1. Copie el archivo WAR en el directorio [!DNL webapps] de Tomcat.

   * Servidor de individualización: [!DNL flashaccess.war]
   * Servidor de generación de claves: [!DNL flashaccess-kgs.war]

1. Copie la carpeta [!DNL ROOT] del paquete proporcionado por el Adobe en el directorio [!DNL webapps].

   El servidor de Individualización también necesita alojar el archivo [!DNL crossdomain.xml]. (La carpeta [!DNL ROOT] contiene el archivo [!DNL crossdomain.xml]; [!DNL ROOT] debe estar en mayúsculas). El servidor de generación de claves no requiere este archivo.

