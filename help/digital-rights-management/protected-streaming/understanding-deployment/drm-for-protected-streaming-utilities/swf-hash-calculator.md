---
description: La utilidad Calculadora de hash de SWF calcula el resumen de una aplicación de SWF ubicada en un archivo.
title: calculadora de hash de SWF
exl-id: 245254fe-2fcb-41e8-94bd-0cbc8b39b2b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# calculadora de hash de SWF{#swf-hash-calculator}

La utilidad Calculadora de hash de SWF calcula el resumen de una aplicación de SWF ubicada en un archivo.

Para ejecutar el hash, escriba:

```
Hasher.bat 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

o

```
java -jar libs/flashaccess-hasher.jar 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

La utilidad muestra el siguiente mensaje:

```
SWF Hash: 
<i class="+ topic ph hi-d="" i "="">
  hash-of-swf
</i class="+ topic>
```

Puede utilizar este valor para especificar el compendio de SWF en [!DNL flashaccess-tenant.xml].
