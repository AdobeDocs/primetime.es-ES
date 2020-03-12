---
seo-title: Configurar la ruta y la ruta de clases
title: Configurar la ruta y la ruta de clases
uuid: cf10fafa-125e-450c-83ae-60b990dab6b5
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4

---


# Configurar la ruta y la ruta de clases{#configure-the-path-and-classpath}

El [!DNL flashaccess.war] contiene [!DNL jsafeWithNative.jar], que es la biblioteca Crypto-J. Este último requiere una biblioteca nativa adicional para realizar operaciones de cifrado.

1. Agregue la [!DNL jsafe] biblioteca nativa a la ruta.

   * **Linux /[!DNL libjsafe.so]-** El directorio que contiene [!DNL libjsafe.so] debe estar en la Ruta (las bibliotecas nativas de Crypto-J también están disponibles para otras plataformas). Por ejemplo, configure [!DNL libjsafe.so] on `LD_LIBRARY_PATH`.

   * **Windows /[!DNL jsafe.dll]-** La contraparte en Windows a [!DNL libjsafe.so] es la adecuada [!DNL jsafe.dll].
   Estas bibliotecas están disponibles en la carpeta de la [!DNL thirdparty] biblioteca.
1. Coloque uno de los archivos [!DNL adobe-flashaccess-certs] jar en la ruta de clases.

       Este archivo JAR no se incluye en el archivo WAR; debe agregarlo explícitamente a la ruta de clases.
   
   * Servidores de desarrollo: solo debe usarse [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Servidores de producción: solo debe usar [!DNL adobe-flashaccess- certs.jar]

La distribución incluye una [!DNL shared] carpeta que incluye tanto el archivo jar como un [!DNL AdobeInitial.properties] archivo preconfigurado. Adobe recomienda agregar estos elementos al `common.loader` a través del [!DNL catalina.properties] archivo. Por ejemplo:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


