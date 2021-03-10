---
title: Archivo de configuración global
description: Archivo de configuración global
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Archivo de configuración global{#global-configuration-file}

El mayor impacto en el rendimiento que puede lograr es mediante el uso de la configuración en el archivo de configuración global, flashaccess-global.xml. Esta configuración incluye los elementos `<Caching>` y `<Logging>` .

* `<Caching>` El  `<Caching>` elemento controla el almacenamiento en caché de los archivos de configuración en la memoria. El elemento `<Caching>` tiene la siguiente sintaxis:

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` controla la frecuencia con la que el servidor comprueba si hay actualizaciones en los archivos de configuración. Un valor bajo para `refreshDelaySeconds` afecta negativamente al rendimiento, mientras que un valor más alto puede mejorar el rendimiento. Para obtener más información sobre `refreshDelaySeconds`, consulte &quot;[Actualización de archivos de configuración](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)&quot;.

   * `numTenants` especifica el número de inquilinos. Un valor inferior al número de inquilinos probablemente afecte al rendimiento porque las solicitudes a los inquilinos restantes resultan en errores de caché. La falta de caché para los datos de configuración afecta negativamente al rendimiento. Por lo tanto, Adobe recomienda que establezca este valor más que el número de inquilinos configurados para el servidor, a menos que haya limitaciones de memoria que considerar.

* `<Logging>` El  `<Logging>` elemento especifica el nivel de registro y la frecuencia con la que se rompen los archivos de registro. El elemento `<Logging>` tiene la siguiente sintaxis:

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` especifica los mensajes que se van a registrar. Un valor de &quot;DEBUG&quot; produce muchos mensajes de registro y puede afectar negativamente al rendimiento. Adobe recomienda una configuración de &quot;WARN&quot; para un rendimiento óptimo. Sin embargo, este valor sí corre el riesgo de perder información esencial del tiempo de ejecución, como las auditorías de licencias. Para conservar información de registro valiosa con un impacto mínimo en el rendimiento, utilice el valor &quot;INFO&quot;.
   * `rollingFrequency` especifica la frecuencia con la que se  *rompen* los archivos de registro. Móvil es el proceso en el que un nuevo archivo de registro se convierte en el registro activo, mientras que el archivo de registro activo anterior ya no se escribe en y se considera resumido. El intervalo móvil se puede configurar en &quot;MINUTELY&quot;, &quot;HOURLY&quot;, &quot;TWICE-DAILY&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; o &quot;NEVER&quot;.

Consulte *Uso del SDK de acceso a Adobe para la protección de contenido* para obtener sugerencias adicionales sobre la optimización del rendimiento.
