---
title: Información general
description: Información general
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---


# Paquete de medios DRM {#media-packager}

Utilice el Media Packager ( [!DNL AdobePackager.jar]) para especificar una política de DRM que se aplicará al contenido y para especificar qué parte del contenido se va a cifrar. Por ejemplo, puede especificar que el empaquetador debe cifrar los datos de vídeo, pero no los datos de audio.

Antes de ejecutar [!DNL AdobePackager.jar], debe establecer las propiedades en la sección Propiedades de Media Packager del archivo de configuración.

>[!NOTE]
>
>También puede especificar todas las propiedades de Media Packager desde la línea de comandos.

## Uso de la línea de comandos de Media Packager {#media-packager-command-line-usage}

**Paquete uno:**

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source` - El nombre del archivo que desea cifrar.
* `dest` - El nombre del archivo cifrado resultante.

   Si especifica un directorio, el archivo cifrado se guarda automáticamente en el directorio especificado con el mismo nombre de archivo especificado como archivo de origen. Sin embargo, no puede especificar un directorio de destino que incluya el archivo de origen.

**Empaquete varios archivos con la misma clave**  (para compatibilidad con velocidad de bits múltiples):

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles` - Una serie de entradas de origen delimitadas por espacios en blanco para los archivos que desea cifrar.
* `dest-directory` - El directorio de destino donde desea escribir contenido cifrado. Los archivos cifrados se guardan automáticamente en este directorio utilizando los mismos nombres de archivo que los archivos de origen. Sin embargo, el directorio de destino no puede incluir ningún archivo de origen.

**Ver información sobre un archivo cifrado:**

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

**Ver información sobre un archivo de metadatos:**

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` es un  [!DNL .metadata] archivo que incluye metadatos de DRM.

>[!NOTE]
>
>Durante el empaquetado, Media Packager ya no puede generar un archivo [!DNL .header] de forma predeterminada. Para generar un archivo [!DNL .header], utilice la opción `-h` durante el empaquetado.

**Tabla 3: Opciones**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción de línea de comandos </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> archivo de configuración </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nombre y la ubicación del archivo de configuración. </p> <p class="- topic/p ">Si no especifica un nombre o una ubicación, el Media Packager de DRM busca <span class="filepath"> flashaccesstools.properties </span> en el directorio de trabajo actual. </p> <p>Nota:  Las opciones que especifique en la línea de comandos tienen prioridad sobre las opciones que especifique en el archivo de configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> archivo cifrado </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permite ver información sobre un archivo que ya se ha empaquetado. </p> <p class="- topic/p ">Los archivos de origen y destino no son obligatorios. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> archivo de metadatos </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permite ver información sobre metadatos existentes. </p> <p class="- topic/p ">Los archivos de origen y destino no son obligatorios. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extrae las directivas DRM de un archivo empaquetado cuando se aplica esta opción junto con la opción <span class="codeph"> -d </span>. </p> <p class="- topic/p ">Un archivo se crea automáticamente en el mismo directorio en el que el archivo cifrado se encuentra con un nombre de archivo e identificador de directiva DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extrae el encabezado DRM de un archivo empaquetado cuando se aplica esta opción junto con la opción <span class="codeph"> -d </span>. </p> <p class="- topic/p ">Un archivo se crea automáticamente en el mismo directorio en el que se encuentra el archivo cifrado, con el nombre del archivo y la extensión <span class="filepath"> .header </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica un identificador único para este segmento de contenido. </p> <p class="- topic/p ">Si no especifica un identificador, se aplica automáticamente el nombre del archivo de destino. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> clave </span>= <span class="+ topic/ph pr-d/codeph codeph"> valor </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica una clave o valor personalizado para agregarlo a los metadatos de contenido. </p> <p class="- topic/p ">Puede especificar varias opciones <span class="codeph"> -k </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extraiga metadatos de un archivo empaquetado al aplicar esta opción junto con la opción <span class="codeph"> -d </span>. </p> <p class="- topic/p ">Un archivo se crea automáticamente en el mismo directorio que el archivo cifrado con un nombre de archivo y una extensión <span class="codeph"> .metadata </span> . </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si el archivo de destino debe sobrescribirse. </p> <p class="- topic/p ">Si el archivo de destino ya existe y <span class="codeph"> -o </span> no está configurado, se produce un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sobrescribe el archivo de destino sin que se le pregunte a menos que ya exista. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> nombre de archivo [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nombre del archivo que incluye la directiva DRM. </p> <p class="- topic/p ">Si la directiva DRM requiere el registro de dominio con un servidor que utiliza un certificado de transporte distinto del especificado en el archivo de propiedades, debe proporcionar el certificado de transporte de dominio. </p> <p class="- topic/p ">Puede especificar varias opciones <span class="codeph"> -p </span>. El cliente siempre aplica la primera opción de forma predeterminada. Los valores especificados en la línea de comandos tienen prioridad sobre los especificados en el archivo de configuración. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Propiedades de configuración {#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>Para los nombres de propiedad que incluyen* n*, *n* representa un número entero que comienza por 1 y aumenta para cada instancia de la propiedad.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Propiedad </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video</span> </td> 
   <td colname="2" class="- topic/entry "> Indica si se codificará el contenido de vídeo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Indica si codificar audio. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.script</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Indica si se cifrarán los datos de secuencia de comandos en mp4s. </p> <p><i class="+ topic/ph hi-d/i ">Las etiquetas de datos </i> onMetaDataand  <i class="+ topic/ph hi-d/i "></i> onXMPscript nunca se cifran aunque habilite esta opción. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica el nivel de codificación de vídeo. </p> <p class="- topic/p ">Se utiliza un valor <span class="codeph"> high</span> para cifrar todo el contenido de vídeo, mientras que los valores <span class="codeph"> medium</span> y <span class="codeph"> low</span> se utilizan para cifrar partes del contenido de vídeo para archivos mp4 que incluyen contenido H.264. </p> <p class="- topic/p ">value = <span class="codeph"> high | media | low</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.secondsUnencryption</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si un valor es bueno a 0, el número especificado de segundos de contenido al principio del archivo no se cifra. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Archivo de certificado del servidor de licencias utilizado para cifrar la clave. </p> <p class="- topic/p ">La propiedad <span class="codeph"> encrypt.keys.asymmetric.certfile</span> especifica un archivo que solo incluye el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esta propiedad se utiliza repetidamente para crear una lista de directivas de DRM que se aplican al contenido. <span class="codeph"> </span> representa un entero cuyo valor es 1 o bueno. El cliente utiliza la primera instancia de forma predeterminada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La URL del servidor de licencias </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El certificado de transporte para el servidor de licencias. </p> <p class="- topic/p ">Esta propiedad especifica un archivo <span class="filepath"> .cer</span> que incluye únicamente el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El archivo PKCS12 que incluye credenciales del empaquetador para firmar contenido. </p> <p class="- topic/p ">El <span class="codeph"> encrypt.sign.certfile</span> necesita hacer referencia a un archivo <span class="filepath"> .pfx</span> que incluye un certificado y una clave privada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La contraseña que puede aplicar para proteger el archivo especificado por <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Establece la versión mínima del servidor necesaria para emitir licencias para el contenido que se empaqueta. </p> <p class="- topic/p ">Especifique x (para Primetime DRM x.0) donde x representa un número de versión principal. Las versiones de servidores anteriores a la versión 3.0 de Adobe Primetime no admiten esta configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si una directiva DRM <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> requiere registro de dominio con un servidor que admita un certificado de transporte que no sea el especificado en <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, entonces debe proporcionar el certificado de transporte de dominio que necesite. </p> <p class="- topic/p ">Esta propiedad especifica un archivo que incluye únicamente el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica una clave de licencia. </p> <p class="- topic/p ">Si no especifica ninguna clave, la clave se genera aleatoriamente. Cuando no habilite la rotación de claves, puede utilizar esta clave para cifrar el contenido. </p> <p class="- topic/p ">Al habilitar la rotación de claves, puede utilizar esta clave para proteger las claves de rotación. La clave debe tener 16 bytes de longitud y especificarse como valores hexadecimales. El espacio en blanco entre los valores hexadecimales es opcional. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rot.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica si la rotación de claves está activada. </p> <p class="- topic/p ">Si se establece en false, que es la configuración predeterminada, la rotación de claves se desactiva y se utiliza el CEK maestro para cifrar todas las muestras del contenido. </p> <p class="- topic/p ">Si se establece en true, la rotación de claves está habilitada y se pueden usar claves diferentes para cifrar segmentos de cualquier contenido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rot.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Secuencia de claves giradas que puede especificar para cifrar contenido cuando la rotación de claves está habilitada. </p> <p class="- topic/p ">Si no especifica ninguna clave, las claves se generan aleatoriamente. Las claves deben tener una longitud de 16 bytes y especificarse como valores hexadecimales. </p> <p class="- topic/p ">El espacio en blanco entre los valores hexadecimales es opcional. <i class="+ topic/ph hi-d/i "></i> debe aumentar monotónicamente, a partir de 1. Cuando se especifican varias claves, las claves se pasan a ciclos en el orden indicado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rot.range</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el intervalo de tiempo en segundos durante el cual se puede aplicar una clave de rotación para cifrar muestras de contenido. </p> <p class="- topic/p ">Una vez transcurrido el intervalo de tiempo en el que se ha cifrado el contenido, se aplica la siguiente clave de rotación. Si ha habilitado la rotación de claves pero no ha especificado ningún intervalo de tiempo, las teclas giran automáticamente cada 15 minutos. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.server.less</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si esta opción se establece en true, no está disponible un servidor de licencias desde el que se puedan obtener licencias. </p> <p class="- topic/p ">Las licencias deben integrarse o obtenerse fuera de banda. El valor predeterminado se establece en false a menos que especifique un valor diferente. Esta opción solo es compatible con Primetime DRM Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>