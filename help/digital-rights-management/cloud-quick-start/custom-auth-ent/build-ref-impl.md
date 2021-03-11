---
title: Generar la implementación de referencia de BEES
description: Generar la implementación de referencia de BEES
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Generar la implementación de referencia de BEES {#build-the-bees-reference-implementation}

Asegúrese de que está utilizando Java 1.6.0_24 o posterior.
1. Complete las rutas vacías necesarias, como `tomcatdir` y `fasterxmldir` en [!DNL build-bees.xml]

   Se incluye FasterXML/Jackson. También puede descargarlo desde [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Actualice los nombres de archivo jar reales en [!DNL build.common.xml] si desea utilizar una versión diferente de las bibliotecas de Jackson.
1. Ejecute el destino `all` de [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

El [!DNL bees.war] se creará en la carpeta [!DNL bees-build/wars].