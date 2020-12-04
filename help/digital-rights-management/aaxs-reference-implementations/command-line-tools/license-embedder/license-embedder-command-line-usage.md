---
seo-title: Uso de la línea de comandos
title: Uso de la línea de comandos
uuid: 72117619-a723-49d3-9aa9-5eefcf5b0916
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Uso de la línea de comandos {#command-line-usage}

Para incrustar una licencia, utilice la sintaxis siguiente:

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` es un archivo FLV o F4V cifrado.
* `destfile` especifica dónde se escribirá el contenido cifrado con la licencia incrustada. Si se especifica un directorio, el archivo se guardará en este directorio utilizando el mismo nombre de archivo que el archivo de origen, pero el directorio no debe ser el directorio que contiene el archivo de origen.

En la tabla siguiente se describen las opciones de la línea de comandos que se pueden especificar junto con la sintaxis anteriormente mencionada:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción de línea de comandos </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename  </span> </td> 
   <td colname="2" class="- topic/entry "> Nombre del archivo que contiene la licencia para incrustar. Se pueden especificar varias opciones <span class="codeph"> -l </span> para incrustar varias licencias. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filename  </span> </td> 
   <td colname="2" class="- topic/entry "> Especifique los metadatos de contenido para los que desea generar una licencia. (Necesario para generar una licencia) </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> No pregunte si se debe sobrescribir el archivo de destino. Si el archivo de destino ya existe y <span class="codeph"> -o </span> no está establecido, se mostrará un error. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </td> 
  </tr> 
 </tbody> 
</table>

