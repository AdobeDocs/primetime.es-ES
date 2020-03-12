---
seo-title: Uso de la línea de comandos
title: Uso de la línea de comandos
uuid: 1c3a450d-5d9c-4437-89dd-1bd8719268b7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uso de la línea de comandos {#command-line-usage}

El Administrador de listas de actualizaciones de directivas se encuentra en el directorio \Reference Implementation\Command Line Tools del DVD. Para crear una lista de actualizaciones de directivas, utilice la sintaxis siguiente:

```
    java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` indica dónde se escribirá la lista de actualización de directivas.

Para ver una lista de actualización de directiva existente, utilice la sintaxis siguiente:

```
    java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

La siguiente tabla contiene descripciones de las opciones de la línea de comandos que se muestran en la sintaxis anterior:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción de línea de comandos </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c archivo de configuración </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica la ubicación del archivo de configuración. Si no se utiliza esta opción, el Administrador de lista de actualización de directivas buscará <span class="filepath"> flashaccesstools.properties </span> en el directorio de trabajo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d nombre de archivo </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Muestra información sobre la lista de actualizaciones de directivas. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e fecha </span> </td> 
   <td colname="2" class="- topic/entry "> (Opcional) La fecha de caducidad de la lista de actualizaciones de directivas. Utilice el formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span> (por ejemplo, 2009-01-31-14:30:00 representa el 31 de enero a las 2:30 p.m.). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f nombre de archivo [certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Agrega todas las entradas de la lista de actualizaciones de directivas existentes. Sólo se puede especificar un archivo existente. </p> <p class="- topic/p ">Si esta lista existente se firmó con una credencial diferente a la que se está utilizando para firmar la nueva lista, especifique su archivo de certificado para que se pueda comprobar su firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si se debe sobrescribir el archivo de destino. Si el archivo de destino ya existe y <span class="codeph"> -o </span> no está establecido, se mostrará un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> fecha <span class="+ topic/ph pr-d/codeph codeph"> " </span> reasonCode <span class="+ topic/ph pr-d/codeph codeph"> " " </span>reasonText <span class="+ topic/ph pr-d/codeph codeph"> " " </span>reasonURL <span class="+ topic/ph pr-d/codeph codeph"> </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) Anula el ID de la política en la fecha especificada. También se puede proporcionar un código de razón opcional, texto de motivo y una dirección URL de motivo. Especifique una cadena vacía "" para indicar que no se proporciona ningún valor para los parámetros opcionales. Especifique la fecha como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span> (por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008). Si no se especifica una fecha, se utiliza la fecha actual. El código de motivo debe ser bueno o igual a 0. Se pueden especificar varias opciones -r. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyNombre de archivo </span> fecha <span class="+ topic/ph pr-d/codeph codeph"> </span> " <span class="+ topic/ph pr-d/codeph codeph"> razonamientoCódigo </span>" " <span class="+ topic/ph pr-d/codeph codeph"> motivoTexto </span>" " <span class="+ topic/ph pr-d/codeph codeph"> motivoURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Realiza la misma acción que el indicador -r, pero extrae el identificador de política del archivo dado. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Reemplaza cualquier directiva coincidente en una solicitud de licencia con esta directiva mediante el código de motivo dado (opcional), el texto del motivo (opcional) y la URL del motivo (opcional). </p> <p>Especifique una cadena vacía "" para indicar que no se proporciona ningún valor para los parámetros opcionales. </p> <p>El código de motivo debe ser bueno o igual a <span class="codeph"> 0 </span>. Se pueden especificar varias opciones <span class="codeph"> -u </span> . </p> </td> 
  </tr> 
 </tbody> 
</table>

