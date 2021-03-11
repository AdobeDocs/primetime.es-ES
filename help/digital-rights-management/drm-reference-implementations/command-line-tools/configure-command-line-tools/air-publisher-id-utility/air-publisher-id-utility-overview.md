---
title: Información general
description: Información general
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Utilidad de ID de editor de AIR {#air-publisher-id-utility}

Al crear un archivo de AIR, la herramienta para desarrolladores de AIR (ADT) genera automáticamente un ID de editor. La utilidad AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) calcula el ID de editor de una aplicación de AIR.

El ID de editor es único para el certificado que se utiliza para crear un archivo de AIR. Si vuelve a utilizar el mismo certificado para varias aplicaciones de AIR, todas las aplicaciones de AIR tienen el mismo ID de editor. Una versión de AIR posterior a la versión 1.5.2 no agrega el ID de editor generado a un archivo. Por lo tanto, si planea utilizar una lista de permitidos de aplicación de AIR, utilice esta herramienta para determinar el ID del editor.

>[!NOTE]
>
>El ID de editor que se utiliza para la aplicación de listas de permitidos de AIR no es el mismo que el ID de editor que especifica el editor de la aplicación en el archivo [!DNL application.xml] de la aplicación.

## Uso de la línea de comandos de la utilidad AIR Publisher ID {#air-publisher-id-utility-command-line-usage}

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
   * `signaturefile`* especifica una ruta al  [!DNL signatures.xml] archivo de la aplicación de AIR, ubicado en el  [!DNL META-INF] directorio de aplicaciones

* `signingcert` especifica el certificado que se utiliza para firmar una aplicación de AIR

>[!NOTE]
>
>Para determinar el ID del editor para una aplicación de Android, debe utilizar la opción `-s` para especificar el certificado utilizado para firmar el paquete de la aplicación de Android (APK). Primetime DRM es necesario para crear aplicaciones Android que puedan reproducir contenido protegido por DRM de Primetime.