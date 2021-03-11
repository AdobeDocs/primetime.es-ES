---
title: Configuración de la ruta y la ruta de clase
description: Configuración de la ruta y la ruta de clase
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---


# Configurar la ruta y la ruta de acceso de la clase{#configure-the-path-and-classpath}

El [!DNL flashaccess.war] contiene [!DNL jsafeWithNative.jar], que es la biblioteca Crypto-J. Este último requiere una biblioteca nativa adicional para realizar operaciones de cifrado.

1. Agregue la biblioteca [!DNL jsafe] nativa a la ruta.

   * **Linux /  [!DNL libjsafe.so] -** El directorio que contiene  [!DNL libjsafe.so] debe estar en la ruta (las bibliotecas nativas de Crypto-J también están disponibles para otras plataformas). Por ejemplo, establezca [!DNL libjsafe.so] en `LD_LIBRARY_PATH`.

   * **Windows /  [!DNL jsafe.dll] -** El homólogo de Windows a  [!DNL libjsafe.so] es el apropiado  [!DNL jsafe.dll].
   Estas bibliotecas están disponibles en la carpeta de biblioteca [!DNL thirdparty].
1. Coloque uno de los archivos jar [!DNL adobe-flashaccess-certs] en la ruta de la clase.

       Este archivo JAR no está incluido en el archivo WAR; debe agregarla explícitamente a la ruta de clase.
   
   * Servidores de desarrollo: solo debe utilizar [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Servidores de producción: solo debe utilizar [!DNL adobe-flashaccess- certs.jar]

La distribución incluye una carpeta [!DNL shared] que incluye tanto el archivo jar como un archivo [!DNL AdobeInitial.properties] preconfigurado. Adobe recomienda agregar estos elementos al `common.loader` mediante el archivo [!DNL catalina.properties]. Por ejemplo:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


