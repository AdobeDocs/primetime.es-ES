---
title: Actualización de la información general de los archivos de configuración
description: Actualización de la información general de los archivos de configuración
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Actualización de la información general de los archivos de configuración {#updating-configuration-files-overview}

Una vez que el servidor de licencias lee uno de los archivos de configuración del servidor de licencias (configuración global o de inquilino), la información de configuración se almacena en caché en la memoria. Por lo tanto, los archivos no tienen que ser leídos desde el disco para cada solicitud de licencia. Sin embargo, el servidor también permite modificar la mayoría de los valores de los archivos de configuración sin necesidad de reiniciar el servidor para que los cambios surtan efecto. (Consulte a continuación para obtener más información sobre los valores de configuración que se comprueban para buscar actualizaciones).

Para volver a cargar la configuración cuando se realizan cambios, el servidor de licencias almacena la hora de la última modificación del archivo. Con un intervalo configurable, el servidor comprueba si el tiempo de modificación del archivo ha cambiado y, si es así, vuelve a cargar el contenido del archivo.

Para controlar la frecuencia con la que el servidor comprueba si hay actualizaciones, configure el atributo `refreshDelaySeconds` en el elemento Almacenamiento en caché del archivo de configuración global. Por ejemplo, si `refreshDelaySeconds` está establecido en 3600 segundos, el servidor debe detectar cualquier actualización de configuración a lo sumo una hora después de actualizar el archivo. Si `refreshDelaySeconds` está establecido en 0, el servidor comprueba si hay actualizaciones de configuración en cada solicitud. No se recomienda establecer `refreshDelaySeconds` en un valor bajo en los entornos de producción, ya que podría afectar al rendimiento.

El elemento Almacenamiento en caché también controla la cantidad de configuraciones de inquilinos almacenadas en caché a la vez. Puede establecer este valor en un número menor que el número total de inquilinos para limitar la cantidad de memoria utilizada para almacenar en caché la información de configuración. Si se recibe una solicitud para un inquilino que no está en la caché, la configuración se carga antes de que se pueda procesar la solicitud. Si la caché está llena, el inquilino utilizado menos recientemente se elimina de la caché.

Si se guarda un cambio en un archivo de configuración o en cualquiera de los archivos de certificado a los que se hace referencia en [!DNL flashaccess-tenant.xml] mientras el servidor intenta leer el archivo, o si se encuentra que la marca de tiempo del archivo es inferior a un segundo antes de la hora actual o está en el futuro, se utilizará la versión en caché de la configuración hasta la próxima vez que el servidor compruebe si hay actualizaciones. Si no hay ninguna versión en caché, la carga de la configuración falla y se devuelve un error al cliente. El servidor intenta cargar el archivo de nuevo la próxima vez que reciba una solicitud para ese inquilino.
