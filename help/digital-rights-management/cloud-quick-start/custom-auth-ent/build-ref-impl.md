---
title: Creación de la implementación de referencia de BEES
description: Creación de la implementación de referencia de BEES
copied-description: true
exl-id: 330c14de-fe4e-4cc8-b0a5-8f7c74417adf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Creación de la implementación de referencia de BEES {#build-the-bees-reference-implementation}

Asegúrese de utilizar Java 1.6.0_24 o posterior.
1. Rellene las rutas vacías necesarias, como `tomcatdir` y `fasterxmldir` in [!DNL build-bees.xml]

   Se incluye FasterXML/Jackson. También puede descargarlo desde [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Actualizar los nombres de archivo JAR reales en [!DNL build.common.xml] si desea utilizar una versión diferente de las bibliotecas de Jackson.
1. Ejecute el `all` destinatario de [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

El [!DNL bees.war] se crearán en el [!DNL bees-build/wars] carpeta.
