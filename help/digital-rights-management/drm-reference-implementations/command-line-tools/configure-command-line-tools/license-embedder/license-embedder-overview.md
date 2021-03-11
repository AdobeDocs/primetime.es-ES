---
title: Información general
description: Información general
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Incrustador de licencias DRM {#license-embedder}

Utilice [!DNL AdobeLicenseEmbedder.jar] para incrustar licencias pregeneradas en el contenido que protege Media Packager.

## Uso de la línea de comandos del grabador de licencias {#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` representa un archivo cifrado.
* `destfile` especifica el nombre del archivo en el que se guarda el contenido cifrado con la licencia incrustada.

   Si especifica un directorio, el archivo se guarda en el directorio de destino. El nombre del archivo de origen también se convierte en el nombre del archivo que se guarda en el directorio de destino.

En la tabla siguiente se describen las opciones de la línea de comandos que puede especificar:

**Tabla 7: Opciones**

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
   <td colname="2" class="- topic/entry "> Nombre del archivo que incluye la licencia que desea incrustar. Puede especificar varias opciones <span class="codeph"> -l </span> para incrustar varias licencias. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filename  </span> </td> 
   <td colname="2" class="- topic/entry "> Especifica los metadatos de contenido para los que se puede generar una licencia. Esta opción es necesaria para generar una licencia. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> No pregunte si el archivo de destino debe sobrescribirse. Si el archivo de destino ya existe y <span class="codeph"> -o </span> no se ha aplicado, se produce un error. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, puede sobrescribirlo sin que se le solicite. </td> 
  </tr> 
 </tbody> 
</table>
