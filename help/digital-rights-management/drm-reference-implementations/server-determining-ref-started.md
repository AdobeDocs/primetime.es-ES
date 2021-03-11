---
title: Comprobar si el servidor de licencias se inició correctamente
description: Comprobar si el servidor de licencias se inició correctamente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Compruebe si el servidor de licencias se inició correctamente {#check-whether-the-license-server-started-properly}

Existen varias formas de determinar si el Servidor de licencias de implementación de referencia se ha iniciado correctamente. Una forma es comprobar los registros [!DNL catalina.log], pero esto puede no ser suficiente, ya que el servidor de licencias inicia sesión en sus propios archivos de registro.
1. Compruebe el archivo [!DNL AdobeFlashAccess.log].

   Aquí es donde el servidor de licencias de Implementación de referencia escribe la información de registro. La ubicación de este archivo de registro la indica su archivo [!DNL log4j.xml] y se puede modificar para que apunte a cualquier ubicación. De forma predeterminada, el archivo de registro se copia en el directorio de trabajo donde ejecuta el script `catalina` Tomcat.
1. Vaya a la siguiente URL y compruebe que se muestra el texto &quot;El servidor de licencias está configurado correctamente&quot;:
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
