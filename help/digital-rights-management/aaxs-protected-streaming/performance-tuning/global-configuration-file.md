---
title: Archivo de configuración global
description: Archivo de configuración global
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Archivo de configuración global{#global-configuration-file}

El mayor impacto en el rendimiento que puede tener es el uso de la configuración en el archivo de configuración global, flashaccess-global.xml. Esta configuración incluye `<Caching>` y `<Logging>` elementos.

* `<Caching>` El `<Caching>` controla el almacenamiento en caché de los archivos de configuración en la memoria. El `<Caching>` tiene la sintaxis siguiente:

  ```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
  ```

   * `refreshDelaySeconds` controla la frecuencia con la que el servidor comprueba las actualizaciones de los archivos de configuración. Un valor bajo para `refreshDelaySeconds` afecta negativamente al rendimiento, mientras que un valor mayor puede mejorarlo. Para obtener más información sobre `refreshDelaySeconds`, consulte &quot;[Actualización de archivos de configuración](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)&quot;.

   * `numTenants` especifica el número de inquilinos. Un valor inferior al número de inquilinos probablemente afecte al rendimiento porque las solicitudes a los inquilinos restantes resultan en errores de caché. La falta de caché para los datos de configuración afecta negativamente al rendimiento. Por lo tanto, Adobe recomienda configurar este valor más alto que el número de inquilinos configurados para el servidor, a menos que haya limitaciones de memoria que considerar.

* `<Logging>` El `<Logging>` especifica el nivel de registro y la frecuencia con la que se acumulan los archivos de registro. El `<Logging>` tiene la sintaxis siguiente:

  ```
  <Logging level="..." rollingFrequency=""/>
  ```

   * `level` especifica los mensajes para registrar. El valor &quot;DEBUG&quot; genera muchos mensajes de registro y puede afectar negativamente al rendimiento. El Adobe recomienda configurar &quot;WARN&quot; para obtener un rendimiento óptimo. Sin embargo, ese valor sí corre el riesgo de perder información esencial en tiempo de ejecución, como las auditorías de licencias. Para conservar la información de registro valiosa con un impacto mínimo en el rendimiento, utilice el valor &quot;INFO&quot;.
   * `rollingFrequency` especifica la frecuencia con la que los archivos de registro son *enrollado*. Móvil es el proceso en el que un nuevo archivo de registro se convierte en el registro activo, mientras que el archivo de registro activo anteriormente ya no se escribe en él y se considera acumulado. El intervalo móvil puede establecerse en &quot;MINUTELY&quot;, &quot;HOURLY&quot;, &quot;TWICE-DAILY&quot;, &quot;DAILY&quot;, &quot;WEEKLY&quot;, &quot;MONTHLY&quot; o &quot;NEVER&quot;.

Consulte *Uso del SDK de acceso a Adobe para proteger el contenido* para obtener sugerencias adicionales sobre cómo optimizar el rendimiento.
