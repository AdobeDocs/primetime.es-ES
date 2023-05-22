---
title: Calculadora de hash de SWF
description: Calculadora de hash de SWF
copied-description: true
exl-id: 651b31bc-47b5-4388-aa00-27d3bd59da30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# Calculadora de hash de SWF{#swf-hash-calculator}

La utilidad Calculadora de hash de SWF calculó el resumen de una aplicación de SWF ubicada en un archivo. Para ejecutar el hash, ejecute el comando:

```
Hasher.bat filename.swf
```

o el comando:

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

La utilidad genera el siguiente mensaje:

```
SWF Hash: hash-of-swf
```

Este valor se puede utilizar para especificar el compendio de SWF en [!DNL flashaccess-tenant.xml].
