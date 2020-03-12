---
seo-title: Administrador de listas de revocación de DRM
title: Administrador de listas de revocación de DRM
uuid: 30ab5f54-4aac-4535-b30c-b4e5dbfbc475
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Administrador de listas de revocación de DRM {#policy-revocation-list-manager}

Utilice la herramienta de línea de comandos del Administrador de listas de revocación de DRM de Primetime ( [!DNL AdobeRevocationListManager.jar]) para crear y administrar listas de revocación y para comprobar si las políticas se han revocado.

Antes de ejecutar [!DNL AdobeRevocationListManager.jar], debe establecer las propiedades en la sección Propiedades *del Administrador de listas de actualizaciones de* directivas y del Administrador de listas de revocación del archivo de configuración.

>[!NOTE]
>
>También puede especificar todas las propiedades del Administrador de listas de revocación desde la línea de comandos.

## Uso de la línea de comandos del Administrador de listas de revocación {#revocation-list-manager-command-line-usage}

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

* `destfile` especifica el nombre del archivo en el que se guardan las propiedades de la lista de revocación.
* `crlNumber` representa un número de versión no negativo de la Lista de revocación de certificados (CRL). Debe aumentar este número cada vez que se actualice la CRL.

**Tabla 5: Opciones de línea de comandos**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opción de línea de comandos </th> 
   <th colname="2" class="- topic/entry entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c archivo de configuración</span> </td> 
   <td colname="2" class="- topic/entry "><p class="- topic/p ">Especifica el nombre y la ubicación del archivo de configuración. </p><p class="- topic/p ">Si no especifica un nombre ni una ubicación, el Administrador de listas de revocación de DRM busca <span class="filepath"> flashaccesstools.properties</span> en el directorio de trabajo actual. </p><p>Nota:  Las opciones que especifique en la línea de comandos tendrán prioridad sobre las opciones que especifique en el archivo de configuración. </p>Especifica la ubicación del archivo de configuración. Si no aplica esta opción, el Administrador de listas de revocación busca <span class="filepath"> flashaccesstools.properties</span> en el directorio de trabajo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d nombre de archivo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Muestra información sobre la lista de revocación. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e fecha</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) La fecha de caducidad de la lista de revocación. Utilice uno de los siguientes formatos: 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:seg</span> </li> 
     </ul>Por ejemplo, 2009-01-31-14:30:00 representa el 31 de enero a las 2:30 p.m. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f filename[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Agrega todas las entradas de la lista de revocación existente. Sólo puede especificar un archivo existente. </p> <p class="- topic/p ">Si la lista existente se firmó con una credencial distinta a la que utilizó para firmar la nueva lista, debe especificar su archivo de certificado junto a para verificar su firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si se debe sobrescribir el archivo de destino. Si el archivo de destino ya existe y <span class="codeph"> -o</span> no está establecido, se producirá un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, puede sobrescribirlo sin que se le pregunte. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revela el certificado identificado por <span class="codeph"> issuerName</span> y <span class="codeph"> serialNumber</span> en la fecha especificada. El <span class="codeph"> issuerName</span> debe utilizar el formato de nombre 509. Por ejemplo, <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>. </p> <p>Debe especificar los números de serie en formato hexadecimal. También debe especificar la fecha de revocación en uno de los siguientes formatos: 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-dd-h24:min:seg</span> </li> 
     </ul>Por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 para la medianoche del 1 de diciembre de 2008. Si no especifica la fecha de revocación, la fecha actual se aplica automáticamente. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Propiedades de configuración {#configuration-properties}

Debe aplicar las credenciales para firmar listas de revocación. Las siguientes propiedades del Administrador de listas de revocación especifican un archivo PKCS12 que incluye credenciales para firmar listas de revocación (certificado del servidor de licencias), junto con la contraseña del certificado:

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`