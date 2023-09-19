---
description: La referencia de Primetime de TVSDK es una aplicación de Android creada en torno a los marcos de TVSDK y AVE.
title: Genere la implementación de referencia de Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Genere la implementación de referencia de Primetime {#build-the-primetime-reference-implementation}

La referencia de Primetime de TVSDK es una aplicación de Android creada en torno a los marcos de TVSDK y AVE.

Para configurar y generar el proyecto de referencia de Primetime en Eclipse:

1. Descargue el archivo zip de Android de TVSDK y desempaquete en un directorio en una ubicación que recuerde.
1. Inicie Eclipse.
1. Seleccionar **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Seleccionar **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Clic **[!UICONTROL Next]**.
1. Utilice el **[!UICONTROL Browse]** para rellenar el **[!UICONTROL Root Directory]** con el directorio en [!DNL samples/PrimetimeReference/src] al que ha desempaquetado el archivo zip de TVSDK para Android.
1. Seleccione los siguientes proyectos para importar: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. Clic **[!UICONTROL Finish]**.
1. Seleccionar  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** para generar el proyecto.

   Este paso no es necesario si el proyecto se configura para que se genere automáticamente.
1. Si desea incluir el proyecto de pruebas en el espacio de trabajo, asócielo con el proyecto PrimetimeReference:
   1. Repita los pasos 3. hasta el 6.
   1. Seleccione el siguiente proyecto para importar: `PrimetimeReference\tests`.
   1. Clic **[!UICONTROL Finish]**.

      El proyecto de pruebas depende del proyecto CatalogActivity, por lo que debe asociar el proyecto de pruebas con el proyecto CatalogActivity.
   1. Clic con el botón derecho **[!UICONTROL tests]** y elija **[!UICONTROL Properties]**.
   1. Seleccione el **[!UICONTROL Projects]** en Ruta de la versión de Java.
   1. Clic **[!UICONTROL Add...]**
   1. Seleccione CatalogActivity.
   1. Clic **[!UICONTROL OK]** para agregar el proyecto.
   1. Clic **[!UICONTROL OK]** para salir de la página Propiedades.
   1. Seleccionar  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** para generar el proyecto.

      Este paso no es necesario si el proyecto se configura para que se genere automáticamente.
