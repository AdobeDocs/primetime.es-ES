---
title: Uso de la línea de comandos
description: Uso de la línea de comandos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Uso de la línea de comandos {#command-line-usage}

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

* `signaturefile` especifica la ruta al archivo signatures.xml de la aplicación de AIR, ubicado en el  [!DNL META-INF] directorio de aplicaciones

* `signingcert` especifica el certificado utilizado para firmar la aplicación de AIR

>[!NOTE]
>
>Para determinar el ID del editor de una aplicación de iOS, utilice la opción `-s` y especifique el certificado utilizado para firmar la aplicación de iOS. ***Adobe Primetime es necesario para crear aplicaciones de iOS que puedan reproducir contenido*** protegido por Access.

