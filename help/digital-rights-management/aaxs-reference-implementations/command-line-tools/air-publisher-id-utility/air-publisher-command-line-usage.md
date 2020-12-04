---
seo-title: Uso de la línea de comandos
title: Uso de la línea de comandos
uuid: 54b1e867-c6cc-4355-b8e6-a7ec910bd33d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Uso de la línea de comandos {#command-line-usage}

Para ejecutar la herramienta, utilice la sintaxis siguiente:

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

* 
   * `signaturefile`* especifica la ruta al archivo signature.xml de la aplicación de AIR, ubicado en el  [!DNL META-INF] directorio de aplicaciones

* `signingcert` especifica el certificado utilizado para firmar la aplicación de AIR

>[!NOTE]
>
>Para determinar el ID de editor de una aplicación de iOS, utilice la opción `-s` y especifique el certificado utilizado para firmar la aplicación de iOS. ***Se requiere Adobe Primetime para crear aplicaciones de iOS que puedan reproducir contenido*** protegido con Access.

