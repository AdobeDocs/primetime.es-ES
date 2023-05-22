---
title: Comprobar si el servidor de licencias se inició correctamente
description: Comprobar si el servidor de licencias se inició correctamente
copied-description: true
exl-id: 05995a75-9468-4237-9091-a07606297772
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Comprobar si el servidor de licencias se inició correctamente {#check-whether-the-license-server-started-properly}

Existen varias formas de determinar si el servidor de licencias de implementación de referencia se ha iniciado correctamente. Una forma es comprobar el [!DNL catalina.log] registra, pero esto puede no ser suficiente, ya que el servidor de licencias registra sus propios archivos de registro.
1. Compruebe su [!DNL AdobeFlashAccess.log] archivo.

   Aquí es donde el servidor de licencias de implementación de referencia escribe la información de registro. La ubicación de este archivo de registro se indica mediante su [!DNL log4j.xml] y se pueden modificar para que apunten a cualquier ubicación. De forma predeterminada, el fichero de registro se copia en el directorio de trabajo en el que se ejecuta la `catalina` Script Tomcat.
1. Vaya a la siguiente URL y compruebe que aparece el texto &quot;Servidor de licencias está configurado correctamente&quot;:
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
