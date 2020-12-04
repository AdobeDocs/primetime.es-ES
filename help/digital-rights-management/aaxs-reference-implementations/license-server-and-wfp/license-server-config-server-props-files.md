---
seo-title: Archivos de propiedades del servidor
title: Archivos de propiedades del servidor
uuid: 3d3a0ee3-009f-4d62-9587-7e487ecdcafd
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Archivos de propiedades del servidor {#server-properties-files}

El servidor requiere dos archivos de configuración, uno para el servidor de licencias y otro para el empaquetador. Ambos archivos deben colocarse en la ruta de clases. Los archivos de propiedades contienen la ubicación de las credenciales emitidas por Adobe. Estas credenciales se pueden especificar como archivo .pfx y contraseña o proporcionando un alias y una contraseña para una credencial almacenada en un HSM.

Consulte los archivos de propiedades para obtener detalles sobre los valores específicos y el uso de cada parámetro. Puede encontrar archivos de propiedades de ejemplo en el directorio &quot;resources&quot; de la implementación de referencia (Referencia Implementation\Server\resources).

Para garantizar la seguridad de la contraseña de la credencial, se proporciona una herramienta (ScrambleUtil.class) para cifrar la contraseña antes de que se introduzca en el archivo flashaccess-refimpl.properties o flashaccess-refimpl-packager.properties.

Para preparar correctamente la contraseña de la credencial:

1. Vaya a [!DNL Reference Implementation\Server\refimpl\scrambler].
1. En el símbolo del sistema, introduzca el comando:

   ```
   java -classpath  
   <i class="+ topic ph hi-d="" i "="">
   path_to_adobe-flashaccess-sdk.jar.; 
        com.adobe.flashaccess.refimpl.util.ScrambleUtil " 
   <i class="+ topic ph hi-d="" i "="">
   your_pfx_password" 
   </i class="+ topic> 
   </i class="+ topic>
   ```

>[!NOTE]
>
>El ejemplo anterior utiliza un punto y coma (;) como delimitador. Para plataformas que no sean Microsoft Windows, utilice dos puntos (:) como delimitador.

La utilidad genera la contraseña cifrada, que debe copiar en el archivo [!DNL .properties].
