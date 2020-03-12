---
seo-title: Preparación de contraseñas para los archivos de propiedades del servidor
title: Preparación de contraseñas para los archivos de propiedades del servidor
uuid: 2d876eb0-b1a5-4c30-ae96-0a22f6a03910
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Preparación de contraseñas para los archivos de propiedades del servidor {#preparing-passwords-for-the-server-properties-files}

Para garantizar la seguridad de la contraseña de la credencial, se proporciona una herramienta para cifrar la contraseña antes de que se introduzca en el [!DNL flashaccess-refimpl.properties] archivo o [!DNL flashaccess-refimpl-packager.properties] .

Para ejecutar la herramienta con la secuencia de comandos ANT proporcionada:

* Ir a *`<Reference Implementation Server Path>`*[!DNL \refimpl]

* Asegúrese de que la `sdkdir` propiedad en [!DNL build-refimpl.xml] apunta al directorio que contiene el SDK de Adobe Access
* Ejecute el siguiente comando con ANT:

   ```
       ant -f build-refimpl.xml
   ```

* Cuando se le solicite, escriba la contraseña de la credencial

Para ejecutar la herramienta con Java:

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

La utilidad genera la contraseña cifrada, que debe copiar en el archivo .properties.

>[!NOTE]
>
>Las contraseñas codificadas con la utilidad de codificación de contraseñas proporcionada con la implementación de referencia no funcionarán con Adobe Access Server para flujo protegido.
