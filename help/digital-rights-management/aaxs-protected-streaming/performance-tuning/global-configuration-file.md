---
seo-title: Archivo de configuración global
title: Archivo de configuración global
uuid: 48c45f56-55c2-4526-b854-5552caf21541
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Archivo de configuración global{#global-configuration-file}

El mayor impacto que puede tener en el rendimiento es usar la configuración del archivo de configuración global, flashaccess-global.xml. Estos ajustes incluyen los `<Caching>` elementos y `<Logging>` .

* `<Caching>` El `<Caching>` elemento controla el almacenamiento en caché de los archivos de configuración en la memoria. El `<Caching>` elemento tiene la siguiente sintaxis:

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` controla la frecuencia con la que el servidor comprueba la existencia de actualizaciones en los archivos de configuración. Un valor bajo para `refreshDelaySeconds` impacta negativamente en el rendimiento, mientras que un valor más alto puede mejorar el rendimiento. Para obtener más información sobre `refreshDelaySeconds`, consulte &quot;[Actualización de archivos](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)de configuración&quot;.

   * `numTenants` especifica el número de inquilinos. Un valor inferior al número de inquilinos probablemente repercuta en el rendimiento porque las solicitudes a los inquilinos restantes resultan en errores de caché. Un fallo en la caché de los datos de configuración afecta negativamente al rendimiento. Por lo tanto, Adobe recomienda que establezca este valor por encima del número de inquilinos configurados para el servidor, a menos que existan limitaciones de memoria que considerar.

* `<Logging>` El `<Logging>` elemento especifica el nivel de registro y la frecuencia con la que se desplazan los archivos de registro. El `<Logging>` elemento tiene la siguiente sintaxis:

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` especifica los mensajes que se van a registrar. Un valor de &quot;DEBUG&quot; produce muchos mensajes de registro y puede afectar negativamente al rendimiento. Adobe recomienda una configuración de &quot;WARN&quot; para un rendimiento óptimo. Sin embargo, ese valor corre el riesgo de perder información esencial del tiempo de ejecución, como las auditorías de licencias. Para conservar información de registro valiosa con un impacto mínimo en el rendimiento, utilice el valor &quot;INFO&quot;.
   * `rollingFrequency` especifica la frecuencia con la que se *desplazan* los archivos de registro. Rolling es el proceso en el que un nuevo archivo de registro se convierte en el registro activo, mientras que el archivo de registro activo anterior ya no se escribe y se considera rodado. El intervalo móvil se puede establecer en &quot;MINUTELY&quot;, &quot;HOURLY&quot;, &quot;TWICE-DAILY&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; o &quot;NUNCA&quot;.

Consulte *Uso del SDK de Adobe Access para la protección de contenido* para obtener más sugerencias sobre la optimización del rendimiento.
