---
title: Descargar y configurar software de requisitos previos
description: El proceso de instalación es sencillo. Si ya tiene el JDK instalado en su sistema, puede omitir este paso, pero tenga en cuenta que su JDK, Eclipse IDE y OS deben ser compatibles.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Descargue y configure el software de requisitos previos {#download-and-configure-prerequisite-software}

1. Descargue el JDK desde [https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/).

   El proceso de instalación es sencillo. Si ya tiene el JDK instalado en su sistema, puede omitir este paso, pero tenga en cuenta que su JDK, Eclipse IDE y OS deben ser compatibles.
1. Descargue el IDE de Eclipse para desarrolladores de Java desde [https://www.eclipse.org/downloads](https://www.eclipse.org/downloads).

   Después de descomprimir el paquete, puede ejecutar Eclipse directamente. No hay instalador.
1. Descargue el paquete ADT del SDK para Android desde [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html).

   Este paquete incluye Eclipse. Si ya tiene Eclipse instalado en su sistema, puede descargar las herramientas de SDK para su plataforma desde la sección [!UICONTROL Use An Existing IDE] .

   Desempaquete e instale en una ubicación que recuerde. Deberá hacer referencia a esto en un paso posterior.
1. Configure el SDK para Android.
   1. Abra un terminal (en Mac OS X) o un símbolo del sistema (en Windows).
   1. Vaya al directorio en el que descargó/desempaquetó el SDK para Android.
   1. Vaya a la carpeta herramientas, que contiene un archivo llamado [!DNL android].
   1. Ejecute los siguientes comandos:

      * Para Mac OS X/Unix:

         ```
         chmod +x android 
         android update sdk --no-ui
         ```

      * Para Windows:

         ```
         android update sdk --no-ui
         ```

         Este proceso lleva un tiempo.

1. Configure Eclipse.
   1. Inicie Eclipse.

      En Windows, si Eclipse no se inicia y el problema que se informa es que Eclipse no puede encontrar un archivo Java requerido, pruebe lo siguiente:

      * añada `-vm C:\[path to your JDK bin]\javaw.exe` al archivo [!DNL eclipse.ini].
   1. Seleccione **[!UICONTROL Help]** > **[!UICONTROL Install New Software]** .
   1. Haga clic **[!UICONTROL Add...]**.
   1. Escriba `Android` para el nombre.
   1. Introduzca `https://dl-ssl.google.com/android/eclipse/` en el enlace **[!UICONTROL Work with]**.
   1. Haga clic **[!UICONTROL OK]**.

      Debería ver un cuadro de diálogo similar a este:

      ![](assets/available_software.jpg)

   1. Seleccione los paquetes resultantes (los de las herramientas para desarrolladores y los complementos NDK) y haga clic en **[!UICONTROL Next]**.

      Esto descarga las herramientas de desarrollo de Android (ADT).
   1. Una vez finalizada la descarga, reinicie Eclipse.

   El SDK para Android ya está instalado. 1. Configure Eclipse para que pueda encontrar el SDK para Android y utilizarlo como recurso.
   1. Abra Eclipse.
   1. Seleccione **[!UICONTROL Window]** > **[!UICONTROL Preferences]** en Windows;  **[!UICONTROL ADT]** > **[!UICONTROL Preferences]** en Mac OS X.
   1. Seleccione la pestaña **[!UICONTROL Android]**.
   1. Vaya a la ubicación del SDK para Android.
   1. Haga clic **[!UICONTROL Apply]**.

      ![Resultado de los pasos](assets/ss2.jpg)


