---
title: Calculadora de hash SWF
description: Calculadora de hash SWF
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# Calculadora de hash SWF{#swf-hash-calculator}

La utilidad Calculadora de hash SWF calculó el compendio de una aplicación SWF ubicada en un archivo. Para ejecutar el hasher, ejecute el comando:

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

Este valor se puede utilizar para especificar el compendio SWF en [!DNL flashaccess-tenant.xml].
