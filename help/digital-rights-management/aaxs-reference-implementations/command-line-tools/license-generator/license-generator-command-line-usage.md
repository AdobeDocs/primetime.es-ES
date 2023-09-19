---
title: Uso de línea de comandos
description: Uso de línea de comandos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Uso de línea de comandos {#command-line-usage}

Para generar una licencia, utilice la siguiente sintaxis:

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` es un archivo .metadata que contiene los metadatos de DRM de acceso de Adobe. Este archivo se puede obtener del contenido protegido mediante el `-d -m` de Media Packager.

Para mostrar una licencia generada anteriormente, utilice la siguiente sintaxis:

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` es un archivo que contiene una licencia de acceso a Adobe generada por el Generador de licencias.

En la tabla siguiente se describen las opciones de línea de comandos que se pueden especificar junto con la sintaxis mencionada anteriormente:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción de línea de comandos </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c archivoDeConfiguración</span> </td> 
   <td colname="2" class="- topic/entry "> Especifique la ubicación del archivo de configuración. Si no se utiliza esta opción, el Generador de licencias buscará flashaccesstools.properties en el directorio de trabajo. Las opciones especificadas en la línea de comandos tienen prioridad sobre las presentes en el archivo de configuración. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> archivo de licencias</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Mostrar información sobre una licencia que ya se ha generado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Genere una licencia hoja y escriba el resultado en un archivo especificado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m nombre_archivo_metadatos</span> </td> 
   <td colname="2" class="- topic/entry "> Especifique los metadatos de contenido para los que desea generar una licencia. (Necesario para generar la licencia) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">No pregunte si el archivo de destino debe sobrescribirse. Si el archivo de destino ya existe y <span class="codeph"> -o</span> no se ha configurado, se devolverá un error. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy núm-directiva</span> </td> 
   <td colname="2" class="- topic/entry "> Si los metadatos contienen varias directivas, especifique el número de la directiva que desea utilizar (a partir del 1) para generar la licencia. Si no se especifica, se utiliza la primera directiva. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r certificado de destinatario</span> </td> 
   <td colname="2" class="- topic/entry ">Genere una licencia para el destinatario especificado. Se puede utilizar un dispositivo o un certificado de dominio. Múltiple <span class="+ topic/ph pr-d/codeph codeph"> -r </span>se pueden especificar opciones para crear una licencia para varios destinatarios. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root nombre_archivo_raíz</span> </td> 
   <td colname="2" class="- topic/entry "> Genere una licencia raíz y escriba la salida en el archivo especificado. </td> 
  </tr> 
 </tbody> 
</table>
