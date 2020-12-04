---
description: 'null'
seo-description: 'null'
seo-title: Configuración inicial del Administrador de Flashes Access
title: Configuración inicial del Administrador de Flashes Access
uuid: e9041f7c-b098-4121-88bf-ff3e6369e01b
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---


# Configuración inicial del Administrador de Flashes Access {#initial-flash-access-manager-setup}

Siga el procedimiento siguiente para configurar el Administrador de Flashes Access:

1. Implemente Packager Server. Este servidor solo debe estar disponible para los usuarios dentro del servidor de seguridad (no implemente este software en un equipo público). Para obtener más información sobre la implementación del servidor, consulte [Implementación del servidor de licencias y el empaquetador de carpetas observado](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

   * Copie [!DNL flashaccess-packager.war] en la carpeta de aplicaciones web de Tomcat.
   * Copie [!DNL flashaccess-refimpl-packager.properties] de los recursos a una ubicación en la ruta de clases.
   * Inicio el servidor. Verá algunos errores debido a problemas en el archivo de propiedades; esto se espera ya que las propiedades no se han rellenado aún.

1. Instale la aplicación AIR de Flash Access Manager iniciando el archivo [!DNL .air] (requiere AIR 1.5 o superior).
1. Inicie la aplicación de AIR de Flash Access Manager.

   Si el servidor se está ejecutando en algún lugar que no sea `https://localhost:8080*`, verá errores que indican que la aplicación no se puede conectar al servidor. Deseche el cuadro de diálogo de error y rellene la dirección URL correcta para la URL del servidor de Packager en la ficha Preferencias. Si el servidor se ejecuta en la dirección URL especificada y el archivo de propiedades se encuentra en la ruta de clases, la pantalla Preferencias se rellenará con los valores del archivo de propiedades. Una vez configurada la URL del servidor del empaquetador, la aplicación de AIR recuerda esta configuración y no tendrá que introducirla la próxima vez que inicie la aplicación.
1. Rellene los valores de la ficha Preferencias y haga clic en **[!UICONTROL Save]**.
1. Si desea utilizar las carpetas vigiladas, deberá reiniciar el servidor para recuperarse de los errores que vio en el paso 3. Si las preferencias están configuradas correctamente, no deben aparecer errores durante el inicio.

