---
title: Ejecución del servidor DRM para la transmisión protegida
description: Ejecución del servidor DRM para la transmisión protegida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---


# Ejecución del servidor DRM para la transmisión protegida {#running-the-drm-server-for-protected-streaming}

Antes de iniciar Adobe Primetime DRM Server para la transmisión protegida, se recomienda comprobar la validez de los ajustes en los archivos de configuración.

Puede verificar la validez de la configuración utilizando las utilidades proporcionadas con el servidor de licencias. (Consulte *Validador de configuración* en esta guía.

Si desea iniciar Tomcat y el servidor de licencias, debe ejecutar [!DNL catalina.bat start] o [!DNL catalina.sh start] desde el directorio [!DNL bin] de Tomcat.

Una vez iniciado el servidor, debe comprobar que se ha configurado correctamente abriendo `https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1` en una ventana del explorador. Si la configuración del inquilino se ha cargado correctamente, aparece un mensaje de confirmación.

## Archivos de registro {#log-files}

Los archivos de registro generados por la aplicación Adobe Primetime DRM Server para la transmisión protegida se encuentran en el directorio especificado por LicenseServer.LogRoot.

>[!NOTE]
>
>Si los archivos de registro actuales se eliminan o mueven mientras el servidor se ejecuta, es posible que el archivo de registro no se vuelva a crear. Por lo tanto, se puede eliminar parte de la información de registro.

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

El archivo de registro global, [!DNL flashaccess-global.log], se encuentra en *LicenseServer.LogRoot*. El registro puede incluir mensajes de registro que el SDK de Java de Adobe Primetime DRM o los mensajes de registro pueden haber generado durante el tiempo en que se ha inicializado el servidor.

### Archivo de registro de partición {#section_5660137CD6AA40519E72A4315534846B}

El archivo de registro de partición, [!DNL flashaccess-partition.log], se encuentra en el directorio `<LicenseServer.LogRoot>/flashaccesserver`. Incluye mensajes de registro que se han generado durante el procesamiento de una solicitud de licencia.

### Archivo de registro del inquilino {#section_F0257CC0831647F18A746B4F02E3E910}

El archivo de registro de inquilino de cada inquilino, [!DNL flashaccess-tenant.log], se encuentra en `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. El registro de inquilino incluye información de auditoría que describe cada licencia generada para este inquilino.

## Actualización de archivos de configuración {#updating-configuration-files}

Tan pronto como el servidor de licencias lee uno de los archivos de configuración del servidor de licencias (configuración global o de inquilino), la información de configuración se almacena en caché en la memoria. Por lo tanto, los archivos no tienen que ser leídos desde el disco para cada solicitud de licencia. Sin embargo, el servidor también permite modificar la mayoría de los valores de los archivos de configuración sin necesidad de reiniciar el servidor para que los cambios surtan efecto.

Cada vez que modifica el archivo de configuración, el servidor de licencias almacena la hora en que se modificó el archivo por última vez. Con un intervalo configurable, el servidor comprueba si el tiempo de modificación del archivo ha cambiado. Si ha cambiado, el servidor vuelve a cargar automáticamente el contenido del archivo de configuración.

Si desea controlar la frecuencia con la que el servidor comprueba si hay actualizaciones, debe establecer el atributo `refreshDelaySeconds` en el elemento `Caching` del archivo de configuración global. Por ejemplo, si `refreshDelaySeconds` está establecido en 3600 segundos, el servidor actualizará la configuración en un plazo máximo de una hora desde el momento de modificación del archivo de configuración. Si `refreshDelaySeconds` está establecido en 0, el servidor comprueba si hay actualizaciones de configuración en cada solicitud. No se recomienda establecer `refreshDelaySeconds` en un valor bajo en cualquier entorno de producción porque esto puede afectar al rendimiento.

El elemento `Caching` también controla la cantidad de configuraciones de inquilinos almacenadas en caché a la vez. Puede establecer este valor en un número menor que el número total de inquilinos para limitar la cantidad de memoria que se utiliza para almacenar en caché la información de configuración. Si se recibe una solicitud para un inquilino que no está en la caché, la configuración se carga antes de que se pueda procesar la solicitud. Si la caché está llena, el inquilino utilizado menos recientemente se elimina de la caché.

La versión en caché de la configuración se sigue utilizando en las siguientes situaciones (hasta la próxima vez que el servidor compruebe si hay actualizaciones):

* Si se guarda un cambio en un archivo de configuración o en cualquiera de los archivos de certificado a los que se hace referencia en el archivo [!DNL flashaccess-tenant.xml] mientras el servidor intenta leer el archivo
* Si se encuentra que la marca de tiempo del archivo es inferior a un segundo antes de la hora actual
* Si la marca de tiempo del archivo es futura

Si no hay ninguna versión en caché, la carga de la configuración falla y se devuelve un error al cliente. A continuación, el servidor intenta cargar el archivo de nuevo la próxima vez que reciba una solicitud para ese inquilino.

### Actualización del archivo de configuración global {#section_AA546C72442646CFB8906AEEBDF50587}

Puede modificar la contraseña de HSM en [!DNL flashaccess-global.xml] en cualquier momento. Los cambios surtirán efecto la próxima vez que el servidor vuelva a cargar el archivo de configuración. Sin embargo, los cambios en los elementos Registro y Almacenamiento en caché no se vuelven a cargar. Debe reiniciar el servidor antes de que los cambios para estos elementos entren en vigor.

### Actualización del archivo de configuración del inquilino {#section_71624DB8DF28480F84F34F0FF7FD4365}

Puede modificar todos los valores especificados en el archivo [!DNL flashaccess-tenant.xml] en cualquier momento. Los cambios surtirán efecto la próxima vez que el servidor vuelva a cargar el archivo de configuración. Además, el servidor comprueba si hay modificaciones en todos los archivos de credenciales ( [!DNL .pfx]) y archivos de certificado de lista de permitidos del empaquetador a los que se hace referencia en el archivo de configuración del inquilino.