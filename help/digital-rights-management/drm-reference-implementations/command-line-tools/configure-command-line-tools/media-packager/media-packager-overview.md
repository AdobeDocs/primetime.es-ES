---
title: Información general
description: Información general
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# Empaquetador de medios DRM {#media-packager}

Usar el empaquetador de medios ( [!DNL AdobePackager.jar]) para especificar una directiva DRM que se aplicará al contenido y para especificar qué parte del contenido se va a cifrar. Por ejemplo, puede especificar que el empaquetador debe cifrar los datos de vídeo, pero no los datos de audio.

Antes de ejecutar [!DNL AdobePackager.jar], debe establecer las propiedades en la sección Propiedades del empaquetador de medios del archivo de configuración.

>[!NOTE]
>
>También puede especificar todas las propiedades del empaquetador de medios desde la línea de comandos.

## Uso de la línea de comandos de Media Packager {#media-packager-command-line-usage}

**Empaquetar un archivo:**

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
* `dest` : nombre del archivo cifrado resultante.

  Si especifica un directorio, el archivo cifrado se guarda automáticamente en el directorio especificado con el mismo nombre de archivo especificado como archivo de origen. Sin embargo, no puede especificar un directorio de destino que incluya el archivo de origen.

**Empaquetar varios archivos con la misma clave** (para compatibilidad con varias velocidades de bits):

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
* `dest-directory` : directorio de destino en el que desea escribir contenido cifrado. Los archivos cifrados se guardan automáticamente en este directorio utilizando los mismos nombres de archivo que los archivos de origen. Sin embargo, el directorio de destino no puede incluir ningún archivo de origen.

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

* `metadatafile` es un [!DNL .metadata] que incluye metadatos DRM.

>[!NOTE]
>
>Durante el empaquetado, Media Packager ya no puede generar un [!DNL .header] de forma predeterminada. Para generar un [!DNL .header] , utilice el `-h` opción durante el empaquetado.

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
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> configfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nombre y la ubicación del archivo de configuración. </p> <p class="- topic/p ">Si no especifica un nombre o una ubicación, el empaquetador de medios DRM busca <span class="filepath"> flashaccesstools.properties </span> en el directorio de trabajo actual. </p> <p>Nota: Las opciones que especifique en la línea de comandos tienen prioridad sobre las opciones especificadas en el fichero de configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> archivo cifrado </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permite ver información acerca de un archivo que ya se ha empaquetado. </p> <p class="- topic/p ">Los archivos de origen y destino no son obligatorios. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> archivo de metadatos </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Permite ver información sobre metadatos existentes. </p> <p class="- topic/p ">Los archivos de origen y destino no son obligatorios. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extrae directivas DRM de un archivo empaquetado cuando se aplica esta opción junto con el <span class="codeph"> -d </span> opción. </p> <p class="- topic/p ">Se crea automáticamente un fichero en el mismo directorio en el que se encuentra el fichero cifrado con un nombre de fichero y un identificador de política DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extrae el encabezado DRM de un archivo empaquetado al aplicar esta opción junto con el <span class="codeph"> -d </span> opción. </p> <p class="- topic/p ">Se crea automáticamente un archivo en el mismo directorio en el que se encuentra el archivo cifrado, con el nombre y la extensión del archivo <span class="filepath"> .header </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica un identificador único para este segmento de contenido. </p> <p class="- topic/p ">Si no especifica un identificador, se aplica automáticamente el nombre del archivo de destino. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> key </span>= <span class="+ topic/ph pr-d/codeph codeph"> valor </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica una clave o un valor personalizados para agregarlos a los metadatos del contenido. </p> <p class="- topic/p ">Puede especificar varias <span class="codeph"> -k </span> opciones. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Extraer metadatos de un archivo empaquetado al aplicar esta opción junto con la variable <span class="codeph"> -d </span> opción. </p> <p class="- topic/p ">Se crea automáticamente un archivo en el mismo directorio que el archivo cifrado con un nombre de archivo y un <span class="codeph"> .metadata </span> extensión. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si el archivo de destino debe sobrescribirse. </p> <p class="- topic/p ">Si el archivo de destino ya existe y <span class="codeph"> -o </span> no está configurado y se produce un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sobrescribe el archivo de destino sin que se le pregunte a menos que ya exista. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> nombre de archivo [domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nombre del archivo que incluye la directiva DRM. </p> <p class="- topic/p ">Si la directiva DRM requiere el registro de dominio con un servidor que utilice un certificado de transporte distinto del especificado en el archivo de propiedades, deberá proporcionar el certificado de transporte de dominio. </p> <p class="- topic/p ">Puede especificar varias <span class="codeph"> -p </span> opciones. El cliente siempre aplica la primera opción de forma predeterminada. Los valores especificados en la línea de comandos tienen prioridad sobre los especificados en el archivo de configuración. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Propiedades de configuración {#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>Para nombres de propiedades que incluyen* n*, *n* representa un entero que comienza con 1 y aumenta para cada instancia de la propiedad.

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
   <td colname="2" class="- topic/entry "> Indica si se debe cifrar el contenido de vídeo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.audio</span> </td> 
   <td colname="2" class="- topic/entry "> Indica si se debe cifrar el audio. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.script</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Indica si se deben cifrar los datos de script en mp4s. </p> <p><i class="+ topic/ph hi-d/i ">onMetaData</i> y <i class="+ topic/ph hi-d/i ">onXMP</i> las etiquetas de datos de script nunca se cifran, aunque active esta opción. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica el nivel de cifrado de vídeo. </p> <p class="- topic/p ">Un valor de <span class="codeph"> alto</span> se utiliza para cifrar todo el contenido de vídeo, mientras que los valores de <span class="codeph"> mediano</span> y <span class="codeph"> baja</span> se utilizan para cifrar partes del contenido de vídeo para archivos mp4 que incluyen contenido H.264. </p> <p class="- topic/p ">value = <span class="codeph"> alto | medio | bajo</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.content.secondsUnencryption</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si un valor es mayor que 0, el número especificado de segundos de contenido al principio del archivo no se cifrará. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Archivo de certificado del servidor de licencias utilizado para cifrar la clave. </p> <p class="- topic/p ">El <span class="codeph"> encrypt.keys.asymmetric.certfile</span> especifica un archivo que incluye solo el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esta propiedad se utiliza repetidamente para crear una lista de directivas DRM que se aplican al contenido. <span class="codeph"> n</span> representa un entero cuyo valor es 1 o mayor. El cliente utiliza la primera instancia de forma predeterminada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del servidor de licencias </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Certificado de transporte para el servidor de licencias. </p> <p class="- topic/p ">Esta propiedad especifica un <span class="filepath"> .cer</span> que solo incluye el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">El archivo PKCS12 que incluye credenciales de empaquetador para firmar contenido. </p> <p class="- topic/p ">El <span class="codeph"> encrypt.sign.certfile</span> necesita hacer referencia a un <span class="filepath"> .pfx</span> que incluye un certificado y una clave privada. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La contraseña que puede aplicar para proteger el archivo especificado por <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Establece la versión mínima del servidor necesaria para emitir licencias para el contenido que se empaqueta. </p> <p class="- topic/p ">Especifique x (para Primetime DRM x.0), donde x representa un número de versión superior. Las versiones de los servidores anteriores a la versión 3.0 de Adobe Primetime no admiten esta configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si una directiva DRM <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> requiere el registro de dominio con un servidor que admita un certificado de transporte distinto del especificado en <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>, debe proporcionar el certificado de transporte de dominio que necesita. </p> <p class="- topic/p ">Esta propiedad especifica un archivo que incluye solo el certificado (se acepta el formato PEM o DER). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica una clave de licencia. </p> <p class="- topic/p ">Si no especifica una clave, esta se genera de forma aleatoria. Si no habilita la rotación de claves, puede utilizar esta clave para cifrar el contenido. </p> <p class="- topic/p ">Al habilitar la rotación de claves, puede utilizar esta clave para proteger las claves de rotación. La clave debe tener 16 bytes de longitud y especificarse como valores hexadecimales. El espacio en blanco entre los valores hexadecimales es opcional. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica si la rotación de claves está habilitada. </p> <p class="- topic/p ">Si se establece en false, que es la configuración predeterminada, se deshabilita la rotación de claves y se utiliza la CEK maestra para cifrar todas las muestras del contenido. </p> <p class="- topic/p ">Si se establece en true, la rotación de claves está habilitada y se pueden utilizar claves diferentes para cifrar segmentos de cualquier contenido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Secuencia de claves giradas que puede especificar para cifrar el contenido cuando la rotación de claves está habilitada. </p> <p class="- topic/p ">Si no especifica ninguna clave, las claves se generan de forma aleatoria. Las claves deben tener 16 bytes de longitud y especificarse como valores hexadecimales. </p> <p class="- topic/p ">El espacio en blanco entre los valores hexadecimales es opcional. <i class="+ topic/ph hi-d/i ">n</i> debe aumentar monotónicamente, a partir de 1. Cuando se especifican varias claves, las claves se recorren en el orden indicado. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el intervalo de tiempo en segundos durante el cual se puede aplicar una clave de rotación para cifrar muestras de contenido. </p> <p class="- topic/p ">Una vez transcurrido el intervalo de tiempo en el que se ha cifrado el contenido, se aplica la siguiente clave de rotación. Si ha habilitado la rotación de claves pero no ha especificado ningún intervalo de tiempo, las teclas girarán automáticamente cada 15 minutos. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si esta opción se establece en true, no estará disponible ningún servidor de licencias del que se puedan obtener licencias. </p> <p class="- topic/p ">Las licencias deben estar incrustadas u obtenerse fuera de banda. El valor predeterminado se establece en false a menos que especifique un valor diferente. Esta opción solo es compatible con Primetime DRM Professional. </p> </td> 
  </tr> 
 </tbody> 
</table>
