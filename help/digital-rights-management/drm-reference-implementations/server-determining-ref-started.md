---
description: 'null'
seo-description: 'null'
seo-title: Compruebe si el servidor de licencias se ha iniciado correctamente
title: Compruebe si el servidor de licencias se ha iniciado correctamente
uuid: a6a034c9-b3c4-4e26-b901-d2c132c00c52
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Compruebe si el servidor de licencias se ha iniciado correctamente {#check-whether-the-license-server-started-properly}

Existen varias formas de determinar si el servidor de licencias de implementación de referencia se ha iniciado correctamente. Una forma es comprobar los [!DNL catalina.log] registros, pero esto puede no ser suficiente, ya que el servidor de licencias registra sus propios archivos de registro.
1. Compruebe su [!DNL AdobeFlashAccess.log] archivo.

   Aquí es donde el servidor de licencias de Implementación de referencia escribe la información del registro. El archivo indica la ubicación de este archivo de registro y se puede modificar para que señale a cualquier ubicación. [!DNL log4j.xml] De forma predeterminada, el archivo de registro se copia en el directorio de trabajo en el que se ejecuta la secuencia de comandos de `catalina` Tomcat.
1. Vaya a la siguiente URL y compruebe que se muestra el texto &quot;El servidor de licencias está configurado correctamente&quot;:
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
