---
seo-title: Implementar los archivos WAR
title: Implementar los archivos WAR
uuid: 435a6a6e-c981-46fb-bca9-7f5f34eecd6a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Implementar los archivos WAR{#deploy-the-war-files}

1. Copie el archivo WAR al directorio de Tomcat [!DNL webapps] .

   * Servidor de individualización: [!DNL flashaccess.war]
   * Servidor de generación de claves: [!DNL flashaccess-kgs.war]

1. Copie la [!DNL ROOT] carpeta del paquete proporcionado por Adobe en el [!DNL webapps] directorio.

   El servidor de individualización también necesita alojar el [!DNL crossdomain.xml] archivo. (La [!DNL ROOT] carpeta contiene el [!DNL crossdomain.xml] archivo; [!DNL ROOT] debe estar en mayúsculas). El servidor de generación de claves no requiere este archivo.

