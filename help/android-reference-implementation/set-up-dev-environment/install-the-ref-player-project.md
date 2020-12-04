---
description: La referencia TVSDK Primetime es una aplicación de Android creada en torno a los marcos TVSDK y AVE.
seo-description: La referencia TVSDK Primetime es una aplicación de Android creada en torno a los marcos TVSDK y AVE.
seo-title: Genere la implementación de referencia de Primetime
title: Genere la implementación de referencia de Primetime
uuid: ab12660a-1563-49a4-82d9-1ab13f8a92be
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 1%

---


# Genere la implementación de referencia de Primetime {#build-the-primetime-reference-implementation}

La referencia TVSDK Primetime es una aplicación de Android creada en torno a los marcos TVSDK y AVE.

Para configurar y crear el proyecto de referencia Primetime en Eclipse:

1. Descargue el archivo zip TVSDK para Android y descárguelo en un directorio en una ubicación que recordará.
1. Inicie Eclipse.
1. Seleccione **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Seleccione **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Haga clic **[!UICONTROL Next]**.
1. Utilice el botón **[!UICONTROL Browse]** para rellenar el campo **[!UICONTROL Root Directory]** con el directorio de [!DNL samples/PrimetimeReference/src] en el que descomprimió el archivo zip TVSDK para Android.
1. Seleccione los siguientes proyectos para importar: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. Haga clic **[!UICONTROL Finish]**.
1. Seleccione **[!UICONTROL Project]** > **[!UICONTROL Build Project]** para generar el proyecto.

   Este paso no es necesario si el proyecto está configurado para generarse automáticamente.
1. Si desea incluir el proyecto de pruebas en el espacio de trabajo, asocie el proyecto de pruebas con el proyecto PrimetimeReference:
   1. Repita los pasos 3. hasta 6.
   1. Seleccione el siguiente proyecto para importar: `PrimetimeReference\tests`.
   1. Haga clic **[!UICONTROL Finish]**.

      El proyecto de pruebas depende del proyecto CatalogActivity, por lo que debe asociar el proyecto de pruebas con el proyecto CatalogActivity.
   1. Haga clic con el botón derecho **[!UICONTROL tests]** y elija **[!UICONTROL Properties]**.
   1. Seleccione la ficha **[!UICONTROL Projects]** en Ruta de compilación de Java.
   1. Haga clic **[!UICONTROL Add...]**
   1. Seleccione CatalogActivity.
   1. Haga clic en **[!UICONTROL OK]** para agregar el proyecto.
   1. Haga clic en **[!UICONTROL OK]** para salir de la página Propiedades.
   1. Seleccione **[!UICONTROL Project]** > **[!UICONTROL Build Project]** para generar el proyecto.

      Este paso no es necesario si el proyecto está configurado para generarse automáticamente.
