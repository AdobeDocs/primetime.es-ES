---
title: Configurar la ruta y la ruta de clase
description: Configurar la ruta y la ruta de clase
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Configurar la ruta y la ruta de clase{#configure-the-path-and-classpath}

El [!DNL flashaccess.war] contains [!DNL jsafeWithNative.jar], que es la biblioteca Crypto-J. Esto último requiere una biblioteca nativa adicional para realizar operaciones criptográficas.

1. Añadir el nativo [!DNL jsafe] a su ruta.

   * **Linux / [!DNL libjsafe.so] -** El directorio que contiene [!DNL libjsafe.so] debe estar en la ruta (las bibliotecas nativas Crypto-J también están disponibles para otras plataformas). Por ejemplo, set [!DNL libjsafe.so] el `LD_LIBRARY_PATH`.

   * **Windows / [!DNL jsafe.dll] -** El homólogo de Windows en [!DNL libjsafe.so] es el adecuado [!DNL jsafe.dll].

   Estas bibliotecas están disponibles en el [!DNL thirdparty] carpeta de la biblioteca.
1. Ponga uno de los [!DNL adobe-flashaccess-certs] archivos jar en la ruta de clase.

       Este archivo JAR no se incluye en el archivo WAR; debe agregarlo explícitamente a la ruta de clase.
   
   * Servidores de desarrollo: solo debe utilizar [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Servidores de producción: solo debe utilizar [!DNL adobe-flashaccess- certs.jar]

La distribución incluye un [!DNL shared] que incluye tanto el archivo jar como una carpeta preconfigurada [!DNL AdobeInitial.properties] archivo. El Adobe recomienda añadir estos elementos al `common.loader` a través de [!DNL catalina.properties] archivo. Por ejemplo:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```
