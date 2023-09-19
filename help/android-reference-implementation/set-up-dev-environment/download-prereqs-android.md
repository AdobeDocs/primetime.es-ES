---
title: Descargar y configurar software necesario
description: El proceso de instalación es sencillo. Si ya tiene el JDK instalado en el sistema, puede omitir este paso, pero tenga en cuenta que el JDK, Eclipse IDE y el sistema operativo deben ser compatibles.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Descargar y configurar software necesario {#download-and-configure-prerequisite-software}

1. Descargue el JDK de [https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/).

   El proceso de instalación es sencillo. Si ya tiene el JDK instalado en el sistema, puede omitir este paso, pero tenga en cuenta que el JDK, Eclipse IDE y el sistema operativo deben ser compatibles.
1. Descargue Eclipse IDE para desarrolladores de Java de [https://www.eclipse.org/downloads](https://www.eclipse.org/downloads).

   Después de descomprimir el paquete, puede ejecutar Eclipse directamente. No hay ningún instalador.
1. Descargue el paquete ADT del SDK para Android desde [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html).

   Este paquete incluye Eclipse. Si ya tiene Eclipse instalado en el sistema, puede descargar las herramientas de SDK para su plataforma desde el [!UICONTROL Use An Existing IDE] sección.

   Desempaquete e instale en una ubicación que recuerde. Deberá hacer referencia a esto en un paso posterior.
1. Configure el SDK para Android.
   1. Abra un terminal (en Mac OS X) o un símbolo del sistema (en Windows).
   1. Vaya al directorio en el que ha descargado/desempaquetado el SDK para Android.
   1. Vaya a la carpeta de herramientas, que contiene un archivo llamado [!DNL android].
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

      En Windows, si Eclipse no se inicia y el problema del que se ha informado es que Eclipse no puede encontrar un archivo Java requerido, intente lo siguiente:

      * añadir `-vm C:\[path to your JDK bin]\javaw.exe` a su [!DNL eclipse.ini] archivo.
   1. Seleccionar  **[!UICONTROL Help]** > **[!UICONTROL Install New Software]** .
   1. Clic **[!UICONTROL Add...]**.
   1. Entrar `Android` para el nombre.
   1. Entrar `https://dl-ssl.google.com/android/eclipse/` para el **[!UICONTROL Work with]** vínculo.
   1. Clic **[!UICONTROL OK]**.

      Debería ver un cuadro de diálogo similar al siguiente:

      ![](assets/available_software.jpg)

   1. Seleccione los paquetes resultantes (los de Herramientas para desarrolladores y Complementos NDK) y haga clic en **[!UICONTROL Next]**.

      Se descargarán las herramientas de desarrollo de Android (ADT).
   1. Una vez finalizada la descarga, reinicie Eclipse.

   El SDK para Android ya está instalado. 1. Configure Eclipse para que pueda encontrar el SDK de Android y utilizarlo como recurso.
   1. Abra Eclipse.
   1. Seleccionar  **[!UICONTROL Window]** > **[!UICONTROL Preferences]** en Windows;  **[!UICONTROL ADT]** > **[!UICONTROL Preferences]** en Mac OS X.
   1. Seleccione el **[!UICONTROL Android]** pestaña.
   1. Vaya a la ubicación del SDK para Android.
   1. Clic **[!UICONTROL Apply]**.

      ![Resultado del paso](assets/ss2.jpg)
