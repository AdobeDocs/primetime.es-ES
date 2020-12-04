---
description: La utilidad calculadora hash SWF calcula el compendio de una aplicación SWF ubicada en un archivo.
seo-description: La utilidad calculadora hash SWF calcula el compendio de una aplicación SWF ubicada en un archivo.
seo-title: Calculadora hash SWF
title: Calculadora hash SWF
uuid: 0cf972c1-4717-4d78-a594-b27178ece512
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# Calculadora hash SWF{#swf-hash-calculator}

La utilidad calculadora hash SWF calcula el compendio de una aplicación SWF ubicada en un archivo.

Para ejecutar el lavafaros, escriba:

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

Puede utilizar este valor para especificar el compendio SWF en [!DNL flashaccess-tenant.xml].
