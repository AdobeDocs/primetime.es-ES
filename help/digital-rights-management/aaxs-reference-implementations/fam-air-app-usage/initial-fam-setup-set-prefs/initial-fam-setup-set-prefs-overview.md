---
seo-title: Descripción general de la configuración de preferencias
title: Descripción general de la configuración de preferencias
uuid: d1c067b1-6c2b-460e-8d00-5a5bfee0789c
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Configuración de la información general de preferencias {#setting-preferences-overview}

Con la excepción de la URL de Packager Server, todas las preferencias especificadas a continuación se almacenan en el archivo [!DNL flashaccess-refimpl-packager.properties] del servidor. Todos los ajustes se pueden modificar directamente en el archivo de propiedades o a través de la aplicación de AIR. Las contraseñas se cifran cuando se almacenan en el archivo de propiedades del servidor. Escriba la contraseña no cifrada en la interfaz de usuario y se cifrará antes de que se almacene en el archivo.

>[!NOTE]
>
>Todos los directorios y rutas hacen referencia a directorios en el servidor del empaquetador, no en el cliente que ejecuta la aplicación de AIR.

Los cambios realizados aquí surtirán efecto inmediatamente después de guardar las preferencias. No es necesario reiniciar el servidor a menos que el subproceso de Packager haya finalizado debido a problemas de configuración.

Las descripciones de preferencias utilizan los términos siguientes:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_tj5_hcz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Preferencia </th> 
   <th colname="2" class="- topic/entry entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL de Packager Server </td> 
   <td colname="2" class="- topic/entry "> Ubicación del servidor que ejecuta <span class="filepath"> flashaccess-packager.war </span>; por ejemplo, <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Directorio de recursos </td> 
   <td colname="2" class="- topic/entry "> Directorio que contiene directivas, certificados, credenciales y cualquier otro recurso necesario para el servidor de empaquetador </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL del servidor de licencias </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del servidor desde el que el cliente debe solicitar una licencia; por ejemplo, <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>

