---
title: Uso de línea de comandos
description: Uso de línea de comandos
copied-description: true
exl-id: b9e51bab-7bef-459f-bb4d-13ccc4add37a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Uso de línea de comandos {#command-line-usage}

El Administrador de listas de revocación se encuentra en el directorio \Implementación de referencia\Herramientas de línea de comandos del DVD. Para ejecutar la herramienta, utilice una de las siguientes sintaxis:

```
    java -jar AdobeRevocationListManager.jar 
<i class="+ topic ph hi-d="" i "="">
 destfile 
 <i class="+ topic ph hi-d="" i "="">
  crlNumber [
  <i class="+ topic ph hi-d="" i "="">
   options] 
       java -jar AdobeRevocationListManager.jar -d 
   <i class="+ topic ph hi-d="" i "="">
     filename
   </i class="+ topic>
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `destfile` indica dónde se escribirá la lista de revocación.
* `crlNumber` es un número de versión no negativo de la Lista de revocación de certificados (CRL). Este número debe incrementarse cada vez que se actualiza la CRL.

La siguiente tabla contiene descripciones de las opciones de la línea de comandos mostradas en la sintaxis anterior:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opción de línea de comandos </th> 
   <th colname="2" class="- topic/entry entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c archivoDeConfiguración</span> </td> 
   <td colname="2" class="- topic/entry ">Especifica la ubicación del archivo de configuración. Si no se utiliza esta opción, el Administrador de listas de revocación buscará <span class="filepath"> flashaccesstools.properties</span> en el directorio de trabajo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d nombre de archivo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Muestra información acerca de la lista de revocación. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e fecha</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) Fecha de caducidad de la lista de revocación. Usar el formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span> (por ejemplo, 2009-01-31-14:30:00 representa el 31 de enero a las 2:30 p.m.). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f nombreDeArchivo[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">Agrega todas las entradas de la lista de revocación existente. Solo se puede especificar un archivo existente. <p class="- topic/p ">Si esta lista existente se firmó con una credencial diferente a la que se usa para firmar la nueva lista, especifique su archivo de certificado a continuación, de modo que se pueda comprobar su firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si el archivo de destino debe sobrescribirse. Si el archivo de destino ya existe y no se ha establecido -o, se devolverá un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r nombreDeEmisor númeroDeSerie revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revoca el certificado identificado por <span class="codeph"> IssuerName</span> y <span class="codeph"> serialNumber</span> en la fecha determinada. El <span class="codeph"> IssuerName</span> debe seguir el formato de nombre 509 (por ejemplo, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>). Especifique los números de serie en formato hexadecimal. Especificar la fecha de revocación como <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:s</span>, por ejemplo 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008. Si no se especifica la fecha de revocación, se utiliza la fecha actual. </p> </td> 
  </tr> 
 </tbody> 
</table>
