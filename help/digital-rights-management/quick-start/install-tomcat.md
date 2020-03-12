---
seo-title: Instalar Tomcat
title: Instalar Tomcat
uuid: f7663eda-ad18-4a6e-bb9f-01c74721b047
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Instalar Tomcat {#install-tomcat}

Debe instalar Tomcat en ambos servidores.
1. Instale Tomcat desde el directorio [!DNL \Third Party\Tomcat\6.0.18\] del DVD de instalación.

   >[!NOTE]
   >
   >Asegúrese de que Tomcat está instalado en una ubicación en la que no hay espacios en la ruta. Puede introducir `C:\Program Files\Tomcat`, pero no `C:\Tomcat\`.

1. Para iniciar Tomcat, entre `TomcatInstallDir>\bin\catalina.bat run`.
1. Para verificar la instalación, vaya a la página de aterrizaje de Tomcat ingresando `https://<Hostname>:8080/`.
1. Cree un `crossdomain.xml` archivo y colóquelo en el `<TomcatInstallDir>\webapps\ROOT\` directorio.

   También puede copiar un archivo del `https://drmtest2.adobe.com/crossdomain.xml` directorio.
