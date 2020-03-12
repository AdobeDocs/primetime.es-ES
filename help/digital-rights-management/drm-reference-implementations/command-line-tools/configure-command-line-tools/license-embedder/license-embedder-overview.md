---
seo-title: Información general
title: Información general
uuid: 5487d1d3-7eb8-410d-a4b1-cde3e94c00a1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Incrustación de licencias DRM {#license-embedder}

Se utiliza [!DNL AdobeLicenseEmbedder.jar] para incrustar licencias pregeneradas en el contenido que protege Media Packager.

## Uso de la línea de comandos de incrustación de licencias {#license-embedder-command-line-usage}

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
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename </span> </td> 
   <td colname="2" class="- topic/entry "> Nombre del archivo que incluye la licencia que desea incrustar. Puede especificar varias opciones <span class="codeph"> -l </span> para incrustar varias licencias. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filename </span> </td> 
   <td colname="2" class="- topic/entry "> Especifica los metadatos de contenido para los que puede generar una licencia. Esta opción es necesaria para generar una licencia. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> No pregunte si se debe sobrescribir el archivo de destino. Si el archivo de destino ya existe y no se ha aplicado <span class="codeph"> -o </span> , se producirá un error. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, puede sobrescribirlo sin que se le pregunte. </td> 
  </tr> 
 </tbody> 
</table>
