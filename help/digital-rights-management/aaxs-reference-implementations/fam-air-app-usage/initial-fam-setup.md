---
title: Configuración inicial del Administrador de Flashes Access
description: Configuración inicial del Administrador de Flashes Access
copied-description: true
exl-id: 880822f3-0d21-42fc-889e-7375a2aab11a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Configuración inicial del Administrador de Flashes Access {#initial-flash-access-manager-setup}

Utilice el siguiente procedimiento para configurar el Administrador de Flash Access:

1. Implemente Packager Server. Este servidor sólo debe estar disponible para los usuarios del cortafuegos (no implemente este software en un equipo público). Para obtener más información sobre la implementación del servidor, consulte [Implementación del servidor de licencias y del empaquetador de carpetas vigiladas](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

   * Copiar [!DNL flashaccess-packager.war] a la carpeta de aplicaciones web de Tomcat.
   * Copiar [!DNL flashaccess-refimpl-packager.properties] de recursos a una ubicación en la ruta de clase.
   * Inicie el servidor. Verá algunos errores debido a problemas en el archivo de propiedades; esto es lo que se espera ya que las propiedades aún no se han rellenado.

1. Instale la aplicación AIR de Flash Access Manager iniciando el [!DNL .air] (requiere AIR 1.5 o superior).
1. Inicie la aplicación AIR de Flash Access Manager.

   Si el servidor se ejecuta en algún lugar distinto de `https://localhost:8080*`, verá errores que indican que la aplicación no se puede conectar al servidor. Descarte el cuadro de diálogo de error y rellene la dirección URL correcta para la dirección URL del servidor de Packager en la pestaña Preferencias. Si el servidor se está ejecutando en la dirección URL especificada y el archivo de propiedades se encuentra en la ruta de clase, la pantalla Preferencias se rellenará con los valores del archivo de propiedades. Después de establecer la URL del servidor del empaquetador, la aplicación de AIR recuerda esta configuración y no tendrá que introducirla la próxima vez que inicie la aplicación.
1. Rellene los valores de la pestaña Preferencias y haga clic en **[!UICONTROL Save]**.
1. Si desea utilizar las carpetas inspeccionadas, deberá reiniciar el servidor para recuperarse de los errores que vio en el paso 3. Si las preferencias están configuradas correctamente, no debería aparecer ningún error durante el inicio.
