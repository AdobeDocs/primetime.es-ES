---
title: Preparación de contraseñas para los archivos de propiedades del servidor
description: Preparación de contraseñas para los archivos de propiedades del servidor
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Preparación de contraseñas para los archivos de propiedades del servidor {#preparing-passwords-for-the-server-properties-files}

Para garantizar la seguridad de la contraseña de la credencial, se proporciona una herramienta para cifrar la contraseña antes de introducirla en el archivo [!DNL flashaccess-refimpl.properties] o [!DNL flashaccess-refimpl-packager.properties].

Para ejecutar la herramienta utilizando la secuencia de comandos ANT proporcionada:

* Vaya a *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* Asegúrese de que la propiedad `sdkdir` de [!DNL build-refimpl.xml] apunta al directorio que contiene el SDK de acceso al Adobe
* Ejecute el siguiente comando utilizando ANT:

   ```
       ant -f build-refimpl.xml
   ```

* Cuando se le pida, escriba la contraseña de la credencial

Para ejecutar la herramienta mediante Java:

* Vaya a *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

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

La utilidad envía la contraseña cifrada, que debe copiarse en el archivo .properties .

>[!NOTE]
>
>Las contraseñas codificadas con la utilidad de reasignación de contraseñas proporcionada con la implementación de referencia no funcionarán con Adobe Access Server para la transmisión protegida.
