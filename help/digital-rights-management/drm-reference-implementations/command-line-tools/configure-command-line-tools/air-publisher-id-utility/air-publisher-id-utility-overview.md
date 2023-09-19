---
title: Información general
description: Información general
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Utilidad AIR Publisher ID {#air-publisher-id-utility}

Al generar un archivo de AIR, la Herramienta de desarrollo de AIR (ADT) genera automáticamente un ID de publicador. La utilidad AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) calcula el ID de publicador de una aplicación de AIR.

El identificador de publicador es exclusivo del certificado que se utiliza para generar un archivo AIR. Si vuelve a utilizar el mismo certificado para varias aplicaciones de AIR, todas las aplicaciones de AIR tienen el mismo ID de publicador. Una versión de AIR posterior a la versión 1.5.2 no agrega el ID de publicador generado a un archivo. Por lo tanto, si planea utilizar una lista de permitidos de aplicación de AIR, utilice esta herramienta para determinar el ID del publicador.

>[!NOTE]
>
>El identificador de publicador que se utiliza para la aplicación de listas de permitidos de AIR no es el mismo que el identificador de publicador que el publicador de la aplicación especifica en el [!DNL application.xml] archivo.

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

* `signaturefile` especifica una ruta al de la aplicación AIR [!DNL signatures.xml] , ubicado en las aplicaciones [!DNL META-INF] directorio

* `signingcert` especifica el certificado que se utiliza para firmar una aplicación de AIR

>[!NOTE]
>
>Para determinar el ID del editor de una aplicación de Android, debe utilizar el `-s` para especificar el certificado utilizado para firmar el paquete de la aplicación de Android (APK). Se requiere DRM de Primetime para crear aplicaciones de Android que puedan reproducir contenido protegido por DRM de Primetime.
