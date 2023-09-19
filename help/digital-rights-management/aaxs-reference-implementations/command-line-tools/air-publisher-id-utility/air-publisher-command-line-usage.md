---
title: Uso de línea de comandos
description: Uso de línea de comandos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# Uso de línea de comandos {#command-line-usage}

Para ejecutar la herramienta, utilice la siguiente sintaxis:

```
java -jar AdobePublisherIDUtility.jar 
<i class="+ topic ph hi-d="" i "="">
 <i class="+ topic ph hi-d="" i "="">
  signaturefile 
  java -jar AdobePublisherIDUtility.jar -s 
  <i class="+ topic ph hi-d="" i "="">
    signingcert
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `signaturefile` especifica la ruta al archivo signatures.xml de la aplicación AIR, ubicado en las aplicaciones [!DNL META-INF] directorio

* `signingcert` especifica el certificado utilizado para firmar la aplicación de AIR

>[!NOTE]
>
>Para determinar el ID de editor de una aplicación de iOS, utilice el `-s` y especifique el certificado utilizado para firmar la aplicación de iOS. ***Adobe Primetime es necesario para crear aplicaciones de iOS que puedan reproducir contenido protegido por acceso***.
