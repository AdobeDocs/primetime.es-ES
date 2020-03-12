---
seo-title: Información general
title: Información general
uuid: 19d05867-c210-4cd0-bc2f-5dd75f5774e5
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d

---


# Administrador de lista de actualización de directivas de DRM {#policy-update-list-manager}

Utilice la herramienta de línea de comandos del Administrador de actualizaciones de directivas de DRM de Primetime ( [!DNL AdobePolicyUpdateListManager.jar]) para crear y administrar listas de actualizaciones de directivas de DRM y para comprobar si las directivas se han actualizado o revocado.

Antes de ejecutar la herramienta de línea de comandos del Administrador de listas de actualizaciones de directivas, debe establecer las propiedades en la sección Propiedades *del Administrador de listas de actualizaciones de* directivas y del Administrador de listas de revocación del archivo de configuración.

>[!NOTE]
>
>También puede especificar todas las propiedades del Administrador de listas de actualizaciones de directivas desde la línea de comandos.

## Uso de la línea de comandos del Administrador de listas de actualizaciones de directivas {#policy-update-list-manager-command-line-usage}

**Crear una lista de actualización de directiva:**

```
java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` indica el nombre del archivo en el que se ha escrito la lista de actualización de directivas DRM.

**Ver una lista de actualización de directiva existente:**

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` Nombre del archivo de lista de actualizaciones de directivas.

**Tabla 4: Opciones de línea de comandos**

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nombre y la ubicación del archivo de configuración. </p> <p class="- topic/p ">Si no especifica un nombre ni una ubicación, el Administrador de listas de actualizaciones de directivas de DRM busca <span class="filepath"> flashaccesstools.properties </span> en el directorio de trabajo actual. </p> <p>Nota:  Las opciones que especifique en la línea de comandos tendrán prioridad sobre las opciones que especifique en el archivo de configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d nombre de archivo </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Muestra información sobre la lista de actualización de directivas DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e fecha </span> </td> 
   <td colname="2" class="- topic/entry "> <p>(Opcional) La fecha de caducidad de la lista de actualización de directivas de DRM. </p> <p>Utilice el formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span> (por ejemplo, 2009-01-31-14:30:00 representa el 31 de enero a las 2:30 p.m.). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f nombre de archivo [certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Agrega todas las entradas de la lista de actualización de directivas DRM existente. Sólo puede especificar un archivo existente. </p> <p class="- topic/p ">Si la lista existente se ha firmado con una credencial distinta a la que se está utilizando para firmar la nueva lista, deberá especificar su archivo de certificado para verificar su firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">No pregunte si se debe sobrescribir el archivo de destino. Si el archivo de destino ya existe y <span class="codeph"> -o </span> no está establecido, se producirá un error. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Si el archivo de destino ya existe, sobrescribirlo sin preguntar. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> fecha <span class="+ topic/ph pr-d/codeph codeph"> " </span> reasonCode <span class="+ topic/ph pr-d/codeph codeph"> " " </span>reasonText <span class="+ topic/ph pr-d/codeph codeph"> " " </span>reasonURL <span class="+ topic/ph pr-d/codeph codeph"> </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Opcional) Cambia el ID de la directiva DRM en la fecha especificada. Puede proporcionar un código de motivo, texto de motivo y URL de motivo opcional. Debe especificar una cadena vacía "" para indicar que no se proporciona ningún valor para los parámetros opcionales. Puede especificar la fecha en <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-dd-h24:min:sec </span> en estos formatos. Por ejemplo, 2008-12-1 o 2008-12-1-00:00:00 representa la medianoche del 1 de diciembre de 2008). Si no especifica una fecha, la fecha actual se aplica automáticamente. Por lo tanto, el código de razón debe ser bueno o igual a 0. También puede especificar varias opciones -r. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyNombre de archivo </span> fecha <span class="+ topic/ph pr-d/codeph codeph"> </span> " <span class="+ topic/ph pr-d/codeph codeph"> razonamientoCódigo </span>" " <span class="+ topic/ph pr-d/codeph codeph"> motivoTexto </span>" " <span class="+ topic/ph pr-d/codeph codeph"> motivoURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Realiza la misma acción que la opción <span class="codeph"> -r </span> . Sin embargo, extrae el identificador de directiva DRM de un archivo especificado. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Reemplaza cualquier directiva de DRM que coincida en una solicitud de licencia con esta directiva de DRM mediante el uso del código de motivo dado (opcional), el texto del motivo (opcional) y la URL del motivo (opcional). </p> <p>Una cadena vacía "" indica que no ha proporcionado ningún valor para los parámetros opcionales. </p> <p>El código de motivo debe ser bueno o igual a <span class="codeph"> 0 </span>. Puede especificar varias opciones <span class="codeph"> -u </span> . </p> </td> 
  </tr> 
 </tbody> 
</table>

## Propiedades de configuración {#configuration-properties}

Las siguientes propiedades del Administrador de lista de actualización de directivas de DRM de Primetime especifican un archivo PKCS12 que incluye credenciales para firmar listas de revocación (certificado del servidor de licencias), junto con una contraseña.

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`