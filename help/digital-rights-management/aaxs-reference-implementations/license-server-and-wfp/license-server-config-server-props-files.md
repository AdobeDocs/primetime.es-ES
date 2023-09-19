---
title: Archivos de propiedades del servidor
description: Archivos de propiedades del servidor
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Archivos de propiedades del servidor {#server-properties-files}

El servidor requiere dos archivos de configuración, uno para el servidor de licencias y otro para el empaquetador. Ambos archivos deben colocarse en la ruta de clase. Los archivos de propiedades contienen la ubicación de las credenciales emitidas por la Adobe. Estas credenciales se pueden especificar como archivo .pfx y contraseña o proporcionando un alias y contraseña para una credencial almacenada en un HSM.

Consulte los archivos de propiedad para obtener más información sobre los valores específicos y el uso de cada parámetro. Se pueden encontrar archivos de propiedades de muestra en el directorio &quot;resources&quot; de la implementación de referencia (Reference Implementation\Server\resources).

Para garantizar la seguridad de la contraseña de la credencial, se proporciona una herramienta (ScrambleUtil.class) para cifrar la contraseña antes de introducirla en el archivo flashaccess-refimpl.properties o flashaccess-refimpl-packager.properties.

Para preparar correctamente la contraseña de su credencial:

1. Ir a [!DNL Reference Implementation\Server\refimpl\scrambler].
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
>El ejemplo anterior utiliza un punto y coma (;) como delimitador. Para plataformas distintas de Microsoft Windows, utilice dos puntos (:) como delimitador.

La utilidad genera la contraseña cifrada, que debe copiar en el [!DNL .properties] archivo.
