---
title: Calculadora de hash de SWF
description: Calculadora de hash de SWF
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
