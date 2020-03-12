---
seo-title: Uso de la línea de comandos
title: Uso de la línea de comandos
uuid: b3a995de-653e-491a-9262-86dc56b9ce31
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uso de la línea de comandos {#command-line-usage}

Para generar una licencia, utilice la sintaxis siguiente:

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` es un archivo .metadata que contiene los metadatos DRM de Adobe Access. Este archivo se puede obtener a partir de contenido protegido mediante la `-d -m` opción de Media Packager.

Para mostrar una licencia generada anteriormente, utilice la sintaxis siguiente:

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` es un archivo que contiene una licencia de Adobe Access generada por el Generador de licencias.

En la tabla siguiente se describen las opciones de la línea de comandos que se pueden especificar junto con la sintaxis anteriormente mencionada:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción de línea de comandos </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c archivo de configuración</span> </td> 
   <td colname="2" class="- topic/entry "> Especifique la ubicación del archivo de configuración. Si no se utiliza esta opción, el Generador de licencias buscará flashaccesstools.properties en el directorio de trabajo. Las opciones especificadas en la línea de comandos tienen prioridad sobre las presentes en el archivo de configuración. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> archivo de licencia</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Mostrar información sobre una licencia que ya se ha generado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf_filename</span> </td> 
   <td colname="2" class="- topic/entry "> Genere una licencia de hoja y escriba el resultado en un archivo especificado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Especifique los metadatos de contenido para los que desea generar una licencia. (Necesario para generar una licencia) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">No pregunte si se debe sobrescribir el archivo de destino. Si el archivo de destino ya existe y <span class="codeph"> -o</span> no está establecido, se mostrará un error. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> Si los metadatos contienen varias directivas, especifique el número de la directiva que se va a utilizar (a partir del 1) para generar la licencia. Si no se especifica, se utiliza la primera directiva. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r certificado de destinatario</span> </td> 
   <td colname="2" class="- topic/entry ">Genere una licencia para el destinatario especificado. Se puede utilizar un certificado de dispositivo o dominio. Se pueden especificar varias <span class="+ topic/ph pr-d/codeph codeph"></span>opciones -r para crear una licencia para varios destinatarios. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-root_filename</span> </td> 
   <td colname="2" class="- topic/entry "> Genere una licencia raíz y escriba el resultado en el archivo especificado. </td> 
  </tr> 
 </tbody> 
</table>

