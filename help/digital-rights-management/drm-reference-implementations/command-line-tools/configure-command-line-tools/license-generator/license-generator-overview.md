---
title: Información general
description: Información general
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Generador de licencias DRM {#license-generator}

Uso [!DNL AdobeLicenseGenerator.jar] para generar licencias sin que sea necesario que el cliente envíe una solicitud de licencia a un servidor. A continuación, puede incrustar una licencia generada previamente en el contenido o entregar la licencia al cliente a través de otros mecanismos, como un simple servidor web HTTP.

## Uso de la línea de comandos del Generador de licencias {#license-generator-command-line-usage}

**Generar una licencia:**

```
java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

* `metadata` : incluye los metadatos DRM de Adobe Primetime.

  Puede recuperar este archivo del contenido protegido con la variable `-d -m` opciones en el empaquetador de medios.

**Mostrar una licencia generada anteriormente:**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license` : contiene una licencia DRM de Adobe Primetime generada por el Generador de licencias.

**Tabla 6: Opciones**

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Especifica el nombre y la ubicación del archivo de configuración. </p> <p class="- topic/p ">Si no especifica un nombre o una ubicación, el Generador de licencias DRM busca <span class="filepath"> flashaccesstools.properties</span> en el directorio de trabajo actual. </p> <p>Nota: Las opciones que especifique en la línea de comandos tienen prioridad sobre las opciones especificadas en el fichero de configuración. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> archivo de licencias</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> Muestra información acerca de una licencia que ya se ha generado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> Genera una licencia de hoja y guarda la salida en un archivo especificado. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m nombre_archivo_metadatos</span> </td> 
   <td colname="2" class="- topic/entry "> Especifica los metadatos de contenido para los que se debe generar una licencia. Esta opción es necesaria para generar una licencia. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">No pregunte si el archivo de destino debe sobrescribirse. Si el archivo de destino ya existe y la variable <span class="codeph"> -o</span> no se ha establecido, se produce un error. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Si el archivo de destino ya existe, puede sobrescribirlo sin que se le solicite. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy núm-directiva</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Si los metadatos incluyen varias políticas de DRM, puede especificar el número de políticas de DRM que puede utilizar para generar una licencia. </p> <p>Si no especifica el número de directivas DRM, se aplica automáticamente la primera directiva DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r certificado de destinatario</span> </td> 
   <td colname="2" class="- topic/entry ">Genera una licencia para un destinatario especificado. Puede utilizar un dispositivo o un certificado de dominio y especificar varios <span class="+ topic/ph pr-d/codeph codeph"> -r </span>opciones para crear una licencia para varios destinatarios. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root nombre_archivo_raíz</span> </td> 
   <td colname="2" class="- topic/entry "> Genera una licencia raíz y guarda la salida en el archivo que especifique. </td> 
  </tr> 
 </tbody> 
</table>

## Propiedades del archivo de configuración {#configuration-file-properties}

Antes de ejecutar el Generador de licencias, debe especificar valores para las propiedades del Generador de licencias en el archivo de configuración.

>[!NOTE]
>
>Para nombres de propiedades que incluyen *n*, *n* representa un entero que comienza con 1 y aumenta para cada instancia de la propiedad.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Propiedad </th> 
   <th colname="2" class="- topic/entry entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Establece la versión de cliente mínima admitida actualmente. Si no establece esta propiedad, todas las versiones se admiten automáticamente de forma predeterminada. </p> <p>Puede establecer este valor para controlar cómo responden los clientes más antiguos a los requisitos de licencia que no admiten. Especificar <span class="codeph"> x</span> (para Adobe Primetime DRM x.0) donde <span class="codeph"> x</span> representa un número de versión principal. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licenses.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Certificado de servidor de claves, que es un certificado de servidor de licencias emitido por Adobe que utiliza el servidor de claves. Este certificado se aplica solo si la directiva de metadatos/DRM indica que se requiere un servidor de claves para la entrega de claves a dispositivos iOS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> El archivo PKCS12 que incluye las credenciales del servidor de licencias para firmar licencias. Esta propiedad necesita hacer referencia a un archivo .pfx que incluye un certificado y una clave privada. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">La contraseña que protege el archivo que ha especificado con el <span class="+ topic/ph pr-d/codeph codeph"> licencisegen.sign.certfile</span> opción. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licencisegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Si genera licencias enlazadas al dominio, debe especificar uno o varios certificados de CA de dominio para indicar las autoridades de dominio en las que puede confiar el emisor de la licencia. </p> <p>Si el destinatario de la licencia es un certificado de dominio, que no fue emitido por una de las CA de dominio especificadas, entonces no se puede generar una licencia. Esta propiedad especifica un <span class="filepath"> .cer</span> que incluye el certificado en formato PEM o DER. <span class="codeph">n</span> debe aumentar monotónicamente, a partir de 1. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Archivo PKCS12 opcional que incluye credenciales adicionales del servidor de licencias para descifrar el CEK en la directiva de metadatos y DRM. Puede configurar credenciales adicionales si el contenido se ha empaquetado anteriormente con un certificado del servidor de licencias distinto de las credenciales especificadas con <span class="codeph"> licencisegen.sign.certfile</span>. Esta propiedad debe hacer referencia a un <span class="filepath"> .pfx</span> que incluye un certificado y una clave privada. <span class="codeph">n</span> debe aumentar monotónicamente, a partir de 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>La contraseña se aplica para proteger el archivo que ha especificado con el<span class="+ topic/ph pr-d/codeph codeph"> licencisegen.keys.asymmetric.licenseServerCredential.n</span> propiedad. </p> </td> 
  </tr> 
 </tbody> 
</table>
