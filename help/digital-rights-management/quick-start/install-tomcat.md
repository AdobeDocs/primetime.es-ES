---
title: Instalar Tomcat
description: Instalar Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Instalar Tomcat {#install-tomcat}

Debe instalar Tomcat en ambos servidores.
1. Instale Tomcat desde el directorio [!DNL \Third Party\Tomcat\6.0.18\] en el DVD de instalación.

   >[!NOTE]
   >
   >Asegúrese de que Tomcat esté instalado en una ubicación donde no haya espacios en la ruta. Puede introducir `C:\Program Files\Tomcat`, pero no `C:\Tomcat\`.

1. Para iniciar Tomcat, escriba `TomcatInstallDir>\bin\catalina.bat run`.
1. Para verificar la instalación, vaya a la página de aterrizaje de Tomcat introduciendo `https://<Hostname>:8080/`.
1. Cree un archivo `crossdomain.xml` y colóquelo en el directorio `<TomcatInstallDir>\webapps\ROOT\`.

   También puede copiar un archivo desde el directorio `https://drmtest2.adobe.com/crossdomain.xml`.
