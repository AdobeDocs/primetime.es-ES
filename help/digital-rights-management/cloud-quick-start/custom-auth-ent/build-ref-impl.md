---
seo-title: Genere la implementación de referencia de BEES
title: Genere la implementación de referencia de BEES
uuid: c9358188-e626-4f99-a02c-4928b06d6ae2
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Genere la implementación de referencia de BEES {#build-the-bees-reference-implementation}

Asegúrese de utilizar Java 1.6.0_24 o posterior.
1. Rellene las rutas vacías necesarias, como `tomcatdir` y `fasterxmldir` en [!DNL build-bees.xml]

   Se incluye FasterXML/Jackson. También puede descargarlo desde [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Actualice los nombres de archivo de jar en [!DNL build.common.xml] si desea utilizar una versión diferente de las bibliotecas de Jackson.
1. Ejecutar el `all` objetivo de [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

El [!DNL bees.war] se creará en la [!DNL bees-build/wars] carpeta.