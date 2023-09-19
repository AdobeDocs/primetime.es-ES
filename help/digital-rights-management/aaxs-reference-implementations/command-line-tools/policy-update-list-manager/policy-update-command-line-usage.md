---
title: Uso de línea de comandos
description: Uso de línea de comandos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Uso de línea de comandos {#command-line-usage}

El Administrador de listas de actualización de directivas se encuentra en el directorio \Implementación de referencia\Herramientas de línea de comandos del DVD. Para crear una lista de actualización de directivas, utilice la siguiente sintaxis:

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

Para ver una lista de actualización de directivas existente, utilice la siguiente sintaxis:

```
    java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

La siguiente tabla contiene descripciones de las opciones de la línea de comandos mostradas en la sintaxis anterior:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opción de línea de comandos </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descripción </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c archivoDeConfiguración </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica la ubicación del archivo de configuración. Si no se utiliza esta opción, el Administrador de listas de actualización de directivas buscará <span class="filepath"> flashaccesstools.properties </span> en el directorio de trabajo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d nombre de archivo </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Muestra información sobre la lista de actualización de directivas. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e fecha </span> </td> 
   <td colname="2" class="- topic/entry "> (Opcional) Fecha de caducidad de la lista de actualización de directivas. Usar el formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> (por ejemplo, 2009-01-31-14:30:00 representa el 31 de enero a las 2:30 p.m.). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f nombreDeArchivo [certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Agrega todas las entradas de la lista de actualización de directivas existente. Solo se puede especificar un archivo existente. </p> <p class="- topic/p ">Si esta lista existente se firmó con una credencial diferente a la utilizada para firmar la nueva lista, especifique su archivo de certificado, de modo que se pueda comprobar su firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si el archivo de destino debe sobrescribirse. Si el archivo de destino ya existe y <span class="codeph"> -o </span> no se ha configurado, se devolverá un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r idDeDirectiva </span> <span class="+ topic/ph pr-d/codeph codeph"> fecha </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) Revoca el ID de la directiva en la fecha especificada. También se puede proporcionar un código de motivo, un texto de motivo y una URL de motivo opcionales. Especifique una cadena vacía "" para indicar que no se proporciona ningún valor para los parámetros opcionales. Especifique la fecha como <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:s </span> (por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008). Si no se especifica una fecha, se utiliza la fecha actual. El código de razón debe ser mayor o igual que 0. Se pueden especificar varias opciones -r. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> fecha </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Realiza la misma acción que el indicador -r, pero extrae el identificador de directiva del archivo dado. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u nombreDeArchivo " códigoDeRazón " " textoDeRazón " " URLDeRazón" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Reemplaza cualquier política que coincida en una solicitud de licencia por esta política utilizando el código de motivo dado (opcional), el texto de motivo (opcional) y la URL de motivo (opcional). </p> <p>Especifique una cadena vacía "" para indicar que no se proporciona ningún valor para los parámetros opcionales. </p> <p>El código de motivo debe ser mayor o igual que <span class="codeph"> 0 </span>. Múltiple <span class="codeph"> -u </span> se pueden especificar opciones. </p> </td> 
  </tr> 
 </tbody> 
</table>
