---
title: Instalación de Tomcat
description: Instalación de Tomcat
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Instalación de Tomcat {#install-tomcat}

Debe instalar Tomcat en ambos servidores.
1. Instale Tomcat desde el [!DNL \Third Party\Tomcat\6.0.18\] en el DVD de instalación.

   >[!NOTE]
   >
   >Asegúrese de que Tomcat está instalado en una ubicación en la que no haya espacios en la ruta. Puede introducir `C:\Program Files\Tomcat`, pero no `C:\Tomcat\`.

1. Para iniciar Tomcat, introduzca `TomcatInstallDir>\bin\catalina.bat run`.
1. Para verificar la instalación, vaya a la página de aterrizaje de Tomcat introduciendo `https://<Hostname>:8080/`.
1. Crear un `crossdomain.xml` y coloque el archivo en la carpeta `<TomcatInstallDir>\webapps\ROOT\` directorio.

   También puede copiar un archivo desde el `https://drmtest2.adobe.com/crossdomain.xml` directorio.
