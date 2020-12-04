---
description: Tan pronto como el servidor de licencias lee uno de los archivos de configuración del servidor de licencias (configuración global o del inquilino), la información de configuración se almacena en caché en la memoria. Por lo tanto, no es necesario leer los archivos del disco para cada solicitud de licencia. Sin embargo, el servidor también permite modificar la mayoría de los valores de los archivos de configuración sin necesidad de reiniciar el servidor para que los cambios surtan efecto.
seo-description: Tan pronto como el servidor de licencias lee uno de los archivos de configuración del servidor de licencias (configuración global o del inquilino), la información de configuración se almacena en caché en la memoria. Por lo tanto, no es necesario leer los archivos del disco para cada solicitud de licencia. Sin embargo, el servidor también permite modificar la mayoría de los valores de los archivos de configuración sin necesidad de reiniciar el servidor para que los cambios surtan efecto.
seo-title: Actualización de archivos de configuración
title: Actualización de archivos de configuración
uuid: 34b3247c-3458-49de-b1b0-dc0ebbf61c88
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Actualizando archivos de configuración{#updating-configuration-files}

Tan pronto como el servidor de licencias lee uno de los archivos de configuración del servidor de licencias (configuración global o del inquilino), la información de configuración se almacena en caché en la memoria. Por lo tanto, no es necesario leer los archivos del disco para cada solicitud de licencia. Sin embargo, el servidor también permite modificar la mayoría de los valores de los archivos de configuración sin necesidad de reiniciar el servidor para que los cambios surtan efecto.

Siempre que modifique el archivo de configuración, el servidor de licencias almacenará la hora de la última modificación del archivo. A un intervalo configurable, el servidor comprueba si el tiempo de modificación del archivo ha cambiado. Si ha cambiado, el servidor vuelve a cargar automáticamente el contenido del archivo de configuración.

Si desea controlar la frecuencia con la que el servidor comprueba si hay actualizaciones, debe establecer el atributo `refreshDelaySeconds` en el elemento `Caching` del archivo de configuración global. Por ejemplo: si `refreshDelaySeconds` se establece en 3600 segundos, el servidor actualizará la configuración en un plazo máximo de una hora desde el momento de modificación del archivo de configuración. Si `refreshDelaySeconds` se establece en 0, el servidor comprueba si hay actualizaciones de configuración en cada solicitud. No se recomienda establecer `refreshDelaySeconds` en un valor bajo en cualquier entorno de producción porque esto puede afectar al rendimiento.

El elemento `Caching` también controla cuántas configuraciones de inquilinos se almacenan en caché a la vez. Puede establecer este valor en un número que sea menor que el número total de inquilinos para limitar la cantidad de memoria que se utiliza para almacenar la información de configuración en caché. Si se recibe una solicitud para un inquilino que no está en la caché, la configuración se carga antes de que se pueda procesar la solicitud. Si la caché está llena, el inquilino utilizado menos recientemente se elimina de la caché.

La versión en caché de la configuración sigue utilizándose en las situaciones siguientes (hasta la próxima vez que el servidor compruebe si hay actualizaciones):

* Si se guarda un cambio en un archivo de configuración o en cualquiera de los archivos de certificado a los que se hace referencia en el archivo [!DNL flashaccess-tenant.xml] mientras el servidor intenta leer el archivo
* Si la marca de tiempo del archivo es inferior a un segundo antes de la hora actual
* Si la marca de tiempo del archivo está en el futuro

Si no hay ninguna versión en caché, la carga de la configuración falla y se devuelve un error al cliente. A continuación, el servidor intenta cargar el archivo de nuevo la próxima vez que reciba una solicitud para ese inquilino.

## Actualizando el archivo de configuración global {#section_AA546C72442646CFB8906AEEBDF50587}

Puede modificar la contraseña de HSM en [!DNL flashaccess-global.xml] en cualquier momento. Los cambios tendrán efecto la próxima vez que el servidor vuelva a cargar el archivo de configuración. Sin embargo, los cambios en los elementos Registro y Almacenamiento en caché no se recargan. Debe reiniciar el servidor antes de que los cambios de estos elementos se hagan efectivos.

## Actualizando el archivo de configuración del inquilino {#section_71624DB8DF28480F84F34F0FF7FD4365}

Puede modificar todos los valores especificados en el archivo [!DNL flashaccess-tenant.xml] en cualquier momento. Los cambios tendrán efecto la próxima vez que el servidor vuelva a cargar el archivo de configuración. Además, el servidor comprueba si hay modificaciones en todos los archivos de credenciales ( [!DNL .pfx]) y en los archivos de certificados de lista de permitidos del empaquetador a los que se hace referencia en el archivo de configuración del inquilino.
