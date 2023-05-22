---
title: Preparación de contraseñas para los archivos de propiedades del servidor
description: Preparación de contraseñas para los archivos de propiedades del servidor
copied-description: true
exl-id: 70f75640-7075-450a-8191-dc348bd269b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Preparación de contraseñas para los archivos de propiedades del servidor {#preparing-passwords-for-the-server-properties-files}

Para garantizar la seguridad de la contraseña de su credencial, se proporciona una herramienta para cifrar la contraseña antes de introducirla en el [!DNL flashaccess-refimpl.properties] o [!DNL flashaccess-refimpl-packager.properties] archivo.

Para ejecutar la herramienta utilizando la secuencia de comandos ANT proporcionada:

* Ir a *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* Asegúrese de que `sdkdir` propiedad en [!DNL build-refimpl.xml] apunta al directorio que contiene el SDK de acceso a Adobe
* Ejecute el siguiente comando mediante ANT:

   ```
       ant -f build-refimpl.xml
   ```

* Cuando se le pida, escriba la contraseña de su credencial

Para ejecutar la herramienta mediante Java:

* Ir a *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* En el símbolo del sistema, introduzca el comando:

* En Windows:

   ```
   java -classpath path_to_adobe-flashaccess-sdk.jar;.  
   com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

* En Linux:

   ```
       java -classpath path_to_adobe-flashaccess-sdk.jar;.  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

La utilidad genera la contraseña cifrada, que debe copiar en el archivo de propiedades.

>[!NOTE]
>
>Las contraseñas codificadas con la utilidad de codificación de contraseñas proporcionada con la implementación de referencia no funcionarán con Adobe Access Server para flujo protegido.
