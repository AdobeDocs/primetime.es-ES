---
title: Creación de la implementación de referencia de BEES
description: Creación de la implementación de referencia de BEES
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
