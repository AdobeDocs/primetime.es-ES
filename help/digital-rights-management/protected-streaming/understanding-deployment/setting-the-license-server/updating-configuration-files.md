---
description: En cuanto el servidor de licencias lee uno de los archivos de configuración del servidor de licencias (configuración global o de inquilino), la información de configuración se almacena en caché. Por lo tanto, no es necesario leer los archivos del disco para cada solicitud de licencia. Sin embargo, el servidor también permite modificar la mayoría de los valores de los archivos de configuración sin necesidad de reiniciar el servidor para que los cambios surtan efecto.
title: Actualización de archivos de configuración
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Actualización de archivos de configuración{#updating-configuration-files}

En cuanto el servidor de licencias lee uno de los archivos de configuración del servidor de licencias (configuración global o de inquilino), la información de configuración se almacena en caché. Por lo tanto, no es necesario leer los archivos del disco para cada solicitud de licencia. Sin embargo, el servidor también permite modificar la mayoría de los valores de los archivos de configuración sin necesidad de reiniciar el servidor para que los cambios surtan efecto.

Cada vez que modifica el archivo de configuración, el servidor de licencias almacena la hora en que se modificó por última vez el archivo. A intervalos configurables, el servidor comprueba si ha cambiado la hora de modificación del archivo. Si ha cambiado, el servidor vuelve a cargar automáticamente el contenido del archivo de configuración.

Si desea controlar la frecuencia con la que el servidor comprueba las actualizaciones, debe configurar la variable `refreshDelaySeconds` en el `Caching` del archivo de configuración global. Por ejemplo, si `refreshDelaySeconds` se establece en 3600 segundos, el servidor actualizará la configuración en el plazo máximo de una hora desde la hora de modificación del archivo de configuración. If `refreshDelaySeconds` se establece en 0, el servidor comprueba las actualizaciones de configuración en cada solicitud. No se recomienda que configure `refreshDelaySeconds` a un valor bajo en cualquier entorno de producción, ya que esto puede afectar al rendimiento.

El `Caching` también controla cuántas configuraciones de inquilinos se almacenan en caché a la vez. Puede establecer este valor en un número que sea menor que el número total de inquilinos para limitar la cantidad de memoria que se utiliza para almacenar en caché la información de configuración. Si se recibe una solicitud para un inquilino que no está en la caché, la configuración se carga antes de que se pueda procesar la solicitud. Si la caché está llena, el inquilino utilizado menos recientemente se elimina de la caché.

La versión en caché de la configuración se sigue utilizando en las siguientes situaciones (hasta la próxima vez que el servidor compruebe las actualizaciones):

* Si un cambio se guarda en un archivo de configuración o en cualquiera de los archivos de certificado a los que se hace referencia en la [!DNL flashaccess-tenant.xml] mientras el servidor intenta leer el archivo
* Si la marca de tiempo del archivo es inferior a un segundo antes de la hora actual
* Si la marca de tiempo del archivo es futura

Si no hay ninguna versión en caché, la carga de la configuración falla y se devuelve un error al cliente. A continuación, el servidor intenta volver a cargar el archivo la próxima vez que recibe una solicitud para ese inquilino.

## Actualización del archivo de configuración global {#section_AA546C72442646CFB8906AEEBDF50587}

Puede modificar la contraseña de HSM en [!DNL flashaccess-global.xml] en cualquier momento. Los cambios surtirán efecto la próxima vez que el servidor vuelva a cargar el archivo de configuración. Sin embargo, los cambios realizados en los elementos Logging y Caching no se vuelven a cargar. Debe reiniciar el servidor antes de que los cambios de estos elementos entren en vigor.

## Actualizando el archivo de configuración del inquilino {#section_71624DB8DF28480F84F34F0FF7FD4365}

Puede modificar todos los valores especificados en la variable [!DNL flashaccess-tenant.xml] archivo en cualquier momento. Los cambios surtirán efecto la próxima vez que el servidor vuelva a cargar el archivo de configuración. Además, el servidor comprueba si hay modificaciones en todas las credenciales ( [!DNL .pfx]) archivos y archivos de certificado de lista de permitidos del empaquetador a los que se hace referencia en el archivo de configuración del inquilino.
