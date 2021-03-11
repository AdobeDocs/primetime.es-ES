---
title: Archivos de propiedades del servidor
description: Archivos de propiedades del servidor
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Archivos de propiedades del servidor {#server-properties-files}

El servidor requiere dos archivos de configuración, uno para el servidor de licencias y otro para el empaquetador. Ambos archivos deben colocarse en la ruta de clase. Los archivos de propiedades contienen la ubicación de las credenciales emitidas por el Adobe. Estas credenciales se pueden especificar como archivo .pfx y contraseña, o bien proporcionando un alias y una contraseña para una credencial almacenada en un HSM.

Consulte los archivos de propiedad para obtener detalles sobre los valores específicos y el uso de cada parámetro. Puede encontrar archivos de propiedades de ejemplo en el directorio &quot;resources&quot; de la implementación de referencia (consulte Implementation\Server\resources).

Para garantizar la seguridad de la contraseña de su credencial, se proporciona una herramienta (ScrambleUtil.class) para cifrar la contraseña antes de que se introduzca en el archivo flashaccess-refimpl.properties o flashaccess-refimpl-packager.properties .

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

La utilidad envía la contraseña cifrada, que debe copiarse en el archivo [!DNL .properties].
