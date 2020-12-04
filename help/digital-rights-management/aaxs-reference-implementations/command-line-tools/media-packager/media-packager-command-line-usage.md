---
seo-title: Uso de la línea de comandos
title: Uso de la línea de comandos
uuid: 5f24f18d-09ef-400a-9404-50a9fcf4316d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Uso de la línea de comandos {#command-line-usage}

Antes de usar Media Packager, asegúrese de cumplir los requisitos enumerados en Requisitos y de que el archivo de configuración contenga la información necesaria (consulte el archivo de configuración en *Uso de las implementaciones de referencia de acceso a Adobe*.

Media Packager está en el directorio [!DNL \Reference Implementation\Command Line tools] del DVD. Para cifrar un solo archivo, utilice la sintaxis siguiente:

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

* `source` es el archivo que se va a cifrar.
* `dest` especifica dónde se escribirá el contenido cifrado. Si se especifica un directorio, el archivo cifrado se guardará en esta carpeta utilizando el mismo nombre de archivo que el archivo de origen, pero el directorio no debe ser el directorio que contiene el archivo de origen.

Para cifrar varios archivos con la misma clave (para compatibilidad con varias velocidades de bits), utilice la siguiente sintaxis:

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

* `sourcefiles` es una serie de entradas de origen delimitadas por espacios en blanco que representan los archivos que se van a codificar.
* `dest-directory` especifica dónde se escribirá el contenido cifrado. Los archivos cifrados se guardarán en esta carpeta utilizando los mismos nombres de archivo que los archivos de origen, pero el directorio no debe ser el directorio que contiene los archivos de origen.

Para vista de información sobre un archivo cifrado, utilice la sintaxis siguiente:

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

* `encryptedfile` es el archivo cifrado.

Para vista de información sobre un archivo de metadatos, utilice la sintaxis siguiente:

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` es un  [!DNL .metadata] archivo que contiene los metadatos DRM.

>[!NOTE]
>
>Durante el empaquetado, Media Packager ya no generará un archivo .header de forma predeterminada. Para generar este archivo, utilice la opción `-h` durante el empaquetado.

La siguiente tabla contiene descripciones de las opciones de la línea de comandos que se muestran en la sintaxis anterior:

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica la ubicación del archivo de configuración. Si no se utiliza esta opción, Media Packager buscará <span class="filepath"> flashaccesstools.properties </span> en el directorio de trabajo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> archivo cifrado </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Muestra información sobre un archivo que ya estaba empaquetado. Los archivos de origen y destino no son obligatorios. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> archivo de metadatos </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Muestra información sobre metadatos existentes. Los archivos de origen y destino no son obligatorios. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilice esta opción con <span class="codeph"> -d </span> para extraer políticas de un archivo empaquetado. Se creará un archivo en el mismo directorio que el archivo cifrado mediante el nombre de archivo y el identificador de política. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilice con <span class="codeph"> -d </span> para extraer el encabezado DRM de un archivo empaquetado. Se crea un archivo en el mismo directorio que el archivo cifrado, utilizando el nombre de archivo y la extensión <span class="filepath"> .header </span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica un identificador único para este fragmento de contenido. Si no se especifica ningún identificador, se utilizará el nombre del archivo de destino. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> clave </span>= <span class="+ topic/ph pr-d/codeph codeph"> valor </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica una clave o valor personalizado para agregar a los metadatos de contenido. Se pueden especificar varias opciones <span class="codeph"> -k </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilice esta opción con <span class="codeph"> -d </span> para extraer metadatos de un archivo empaquetado. Se creará un archivo en el mismo directorio que el archivo cifrado con el nombre de archivo y la extensión <span class="codeph"> .metadata </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si se debe sobrescribir el archivo de destino. Si el archivo de destino ya existe y <span class="codeph"> -o </span> no está establecido, se mostrará un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sobrescribe el archivo de destino sin preguntar, si ya existe. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> nombre de archivo [domain-Transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nombre del archivo que contiene la política. Si la directiva requiere el registro de dominio con un servidor que utiliza un certificado de transporte diferente al especificado en el archivo de propiedades, también se debe proporcionar el certificado de transporte de dominio. </p> <p class="- topic/p ">Se pueden especificar varias opciones <span class="codeph"> -p </span> y el cliente utilizará la primera de forma predeterminada. Los valores especificados en la línea de comandos tienen prioridad sobre los especificados en el archivo de configuración. </p> </td> 
  </tr> 
 </tbody> 
</table>

