---
title: Uso de la línea de comandos
description: Uso de la línea de comandos
copied-description: true
exl-id: 67056085-beb5-4f54-8962-369bc32d7907
source-git-commit: 79cab347d0daa01549fbf8a9b37bf0a91c14648e
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

* `signaturefile` especifica la ruta al archivo signature.xml de la aplicación AIR, ubicado en las aplicaciones [!DNL META-INF] directory

* `signingcert` especifica el certificado utilizado para firmar la aplicación AIR

>[!NOTE]
>
>Para determinar el ID del editor de una aplicación de iOS, utilice la variable `-s` y especifique el certificado utilizado para firmar la aplicación iOS. ***Adobe Primetime es necesario para crear aplicaciones de iOS que puedan reproducir contenido protegido por Access***.
