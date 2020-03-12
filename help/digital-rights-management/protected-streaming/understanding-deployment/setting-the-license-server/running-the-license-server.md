---
seo-title: Ejecución del servidor DRM para flujo continuo protegido
title: Ejecución del servidor DRM para flujo continuo protegido
uuid: 9bbe211d-268b-43c2-9e55-7ce62de40d30
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Ejecución del servidor DRM para flujo continuo protegido {#running-the-drm-server-for-protected-streaming}

Antes de iniciar Adobe Primetime DRM Server para flujo protegido, se recomienda comprobar la validez de la configuración en los archivos de configuración.

Puede comprobar la validez de la configuración utilizando las utilidades proporcionadas con el servidor de licencias. (Consulte Validador *de configuración* en esta guía.

Si desea iniciar Tomcat y el servidor de licencias, debe ejecutar [!DNL catalina.bat start] o [!DNL catalina.sh start] desde el [!DNL bin] directorio de Tomcat.

Una vez iniciado el servidor, debe comprobar que se ha configurado correctamente abriendo [!DNL https://<lic<span></span>ense-server-host:port>/flashaccesserver/<tenant-name>/flashaccess/license/v1] en una ventana del explorador. Si la configuración del inquilino se ha cargado correctamente, aparece un mensaje de confirmación.

## Archivos de registro {#log-files}

Los archivos de registro generados por la aplicación Adobe Primetime DRM Server for Protected Streaming se encuentran en el directorio especificado por LicenseServer.LogRoot.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Si los archivos de registro actuales se eliminan o mueven mientras se ejecuta el servidor, es posible que no se vuelva a crear el archivo de registro. Por lo tanto, se puede eliminar parte de la información de registro.

### Estructura del directorio de registro {#section_F490A483D60145ADBC21038914C39203}

Los directorios de registro están estructurados para facilitar su uso. El directorio de registro tiene la siguiente estructura:

```
<i class="+ topic ph hi-d="" i "="">
 LicenseServer.LogRoot/ 
 flashaccess-global.log 
     flashaccessserver/ 
         flashaccess-partition.log 
         tenants/ 
             
 <i class="+ topic ph hi-d="" i "="">
  tenantname/ 
                  flashaccess-tenant.log
 </i class="+ topic>
</i class="+ topic>
```

### Archivo de registro global {#section_1CFA90748142439C9F3BE380969539DA}

El archivo de registro global, [!DNL flashaccess-global.log], se encuentra en *LicenseServer.LogRoot*. El registro puede incluir mensajes de registro que el SDK de Java de Adobe Primetime DRM o los mensajes de registro pueden haber generado durante el tiempo en que se inicializó el servidor.

### Archivo de registro de partición {#section_5660137CD6AA40519E72A4315534846B}

El archivo de registro de partición, [!DNL flashaccess-partition.log], se encuentra en el [!DNL <LicenseServer.LogRoot>/flashaccesserver] directorio. Incluye los mensajes de registro que se han generado durante el procesamiento de una solicitud de licencia.

### Archivo de registro del inquilino {#section_F0257CC0831647F18A746B4F02E3E910}

El archivo de registro de inquilinos de cada inquilino, [!DNL flashaccess-tenant.log], se encuentra en [!DNL &lt;LicenseServer.LogRoot>/flashaccesserver/inants/<tenantname>]. El registro de inquilinos incluye información de auditoría que describe cada licencia que se genera para este inquilino.

## Actualización de archivos de configuración {#updating-configuration-files}

Tan pronto como el servidor de licencias lee uno de los archivos de configuración del servidor de licencias (configuración global o del inquilino), la información de configuración se almacena en caché en la memoria. Por lo tanto, no es necesario leer los archivos del disco para cada solicitud de licencia. Sin embargo, el servidor también permite modificar la mayoría de los valores de los archivos de configuración sin necesidad de reiniciar el servidor para que los cambios surtan efecto.

Siempre que modifique el archivo de configuración, el servidor de licencias almacenará la hora de la última modificación del archivo. A un intervalo configurable, el servidor comprueba si el tiempo de modificación del archivo ha cambiado. Si ha cambiado, el servidor vuelve a cargar automáticamente el contenido del archivo de configuración.

Si desea controlar la frecuencia con la que el servidor comprueba si hay actualizaciones, debe establecer el `refreshDelaySeconds` atributo en el `Caching` elemento del archivo de configuración global. Por ejemplo, si `refreshDelaySeconds` se establece en 3600 segundos, el servidor actualizará la configuración en un plazo máximo de una hora desde el momento de modificación del archivo de configuración. Si `refreshDelaySeconds` se establece en 0, el servidor comprueba si hay actualizaciones de configuración en cada solicitud. No se recomienda establecer `refreshDelaySeconds` un valor bajo en ningún entorno de producción porque esto puede afectar al rendimiento.

El `Caching` elemento también controla cuántas configuraciones de inquilinos se almacenan en caché a la vez. Puede establecer este valor en un número que sea menor que el número total de inquilinos para limitar la cantidad de memoria que se utiliza para almacenar la información de configuración en caché. Si se recibe una solicitud para un inquilino que no está en la caché, la configuración se carga antes de que se pueda procesar la solicitud. Si la caché está llena, el inquilino utilizado menos recientemente se elimina de la caché.

La versión en caché de la configuración sigue utilizándose en las situaciones siguientes (hasta la próxima vez que el servidor compruebe si hay actualizaciones):

* Si se guarda un cambio en un archivo de configuración o en cualquiera de los archivos de certificado a los que se hace referencia en el [!DNL flashaccess-tenant.xml] archivo mientras el servidor intenta leer el archivo
* Si la marca de tiempo del archivo es inferior a un segundo antes de la hora actual
* Si la marca de tiempo del archivo está en el futuro

Si no hay ninguna versión en caché, la carga de la configuración falla y se devuelve un error al cliente. A continuación, el servidor intenta cargar el archivo de nuevo la próxima vez que reciba una solicitud para ese inquilino.

### Actualización del archivo de configuración global {#section_AA546C72442646CFB8906AEEBDF50587}

Puede modificar la contraseña de HSM en [!DNL flashaccess-global.xml] cualquier momento. Los cambios tendrán efecto la próxima vez que el servidor vuelva a cargar el archivo de configuración. Sin embargo, los cambios en los elementos Registro y Almacenamiento en caché no se recargan. Debe reiniciar el servidor antes de que los cambios de estos elementos se hagan efectivos.

### Actualización del archivo de configuración del inquilino {#section_71624DB8DF28480F84F34F0FF7FD4365}

Puede modificar todos los valores especificados en el [!DNL flashaccess-tenant.xml] archivo en cualquier momento. Los cambios tendrán efecto la próxima vez que el servidor vuelva a cargar el archivo de configuración. Además, el servidor comprueba si hay modificaciones en todos los archivos de credenciales ( [!DNL .pfx]) y en los archivos de certificados de la lista blanca del empaquetador a los que se hace referencia en el archivo de configuración del inquilino.