---
title: Información general sobre actualización de archivos de configuración
description: Información general sobre actualización de archivos de configuración
copied-description: true
exl-id: 51c8a0af-9445-4c9e-93bc-af0af0096705
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Información general sobre actualización de archivos de configuración {#updating-configuration-files-overview}

Una vez que el servidor de licencias lee uno de los archivos de configuración del servidor de licencias (configuración global o de inquilino), la información de configuración se almacena en caché. Por lo tanto, no es necesario leer los archivos del disco para cada solicitud de licencia. Sin embargo, el servidor también permite modificar la mayoría de los valores de los archivos de configuración sin necesidad de reiniciar el servidor para que los cambios surtan efecto. (Consulte a continuación para obtener detalles sobre los valores de configuración que se comprueban en busca de actualizaciones).

Para volver a cargar la configuración cuando se realizan cambios, el servidor de licencias almacena la hora en que se modificó el archivo por última vez. A intervalos configurables, el servidor comprueba si el tiempo de modificación del archivo ha cambiado y, si es así, vuelve a cargar el contenido del archivo.

Para controlar la frecuencia con la que el servidor comprueba las actualizaciones, configure el `refreshDelaySeconds` en el elemento Caching del archivo de configuración global. Por ejemplo, si `refreshDelaySeconds` se establece en 3600 segundos y tarda como máximo una hora desde el momento en que se actualiza el archivo para que el servidor detecte las actualizaciones de configuración. If `refreshDelaySeconds` se establece en 0, el servidor comprueba las actualizaciones de configuración en cada solicitud. Configuración `refreshDelaySeconds` no se recomienda usar en un valor bajo para entornos de producción, ya que podría afectar al rendimiento.

El elemento Almacenamiento en caché también controla cuántas configuraciones de inquilinos se almacenan en caché a la vez. Puede establecer este valor en un número menor que el número total de inquilinos para limitar la cantidad de memoria utilizada para almacenar en caché la información de configuración. Si se recibe una solicitud para un inquilino que no está en la caché, la configuración se carga antes de que se pueda procesar la solicitud. Si la caché está llena, el inquilino utilizado menos recientemente se elimina de la caché.

Si un cambio se guarda en un archivo de configuración o en cualquiera de los archivos de certificado a los que se hace referencia en [!DNL flashaccess-tenant.xml] mientras el servidor intenta leer el archivo, o si la marca de tiempo del archivo se encuentra menos de un segundo antes de la hora actual o es futura, la versión en caché de la configuración se utiliza hasta la próxima vez que el servidor comprueba las actualizaciones. Si no hay ninguna versión en caché, falla la carga de la configuración y se devuelve un error al cliente. El servidor intenta volver a cargar el archivo la próxima vez que recibe una solicitud para ese inquilino.
