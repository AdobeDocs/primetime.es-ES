---
description: En este tema se describen las consideraciones relacionadas con el rendimiento. Cualquier configuración del archivo de configuración global llamada flashaccess-global.xml afecta al rendimiento.
title: Archivo de configuración global
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Ajuste del rendimiento {#performance-tuning}

En este tema se describen las consideraciones relacionadas con el rendimiento. Cualquier configuración del archivo de configuración global llamada flashaccess-global.xml afecta al rendimiento.

## Archivo de configuración global {#global-configuration-file}

El archivo de configuración incluye los siguientes elementos de configuración:

* `<Caching>` El `<Caching>` controla el almacenamiento en caché de los archivos de configuración en la memoria. El `<Caching>` admite la siguiente sintaxis:

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Controla la frecuencia con la que el servidor comprueba las actualizaciones de los archivos de configuración. Un valor bajo para `refreshDelaySeconds` afecta negativamente al rendimiento, mientras que un valor mayor puede mejorarlo.

  Consulte *Actualización de archivos de configuración* para obtener más información sobre `refreshDelaySeconds`.

* `numTenants` especifica el número de inquilinos. Un valor inferior al número de inquilinos afecta al rendimiento porque las solicitudes a los inquilinos restantes dan como resultado errores de caché. La falta de caché para cualquier dato de configuración afecta negativamente al rendimiento. Por lo tanto, se recomienda configurar este valor por encima del número de inquilinos configurados para el servidor a menos que haya limitaciones de memoria que tenga que tener en cuenta.

* `<Logging>` El `<Logging>` especifica el nivel de registro y la frecuencia con la que se acumulan los archivos de registro. El `<Logging>` admite la siguiente sintaxis:

  ```
  <Logging level="..." rollingFrequency="..."/>
  ```

* `<level>`  `level` especifica los mensajes a un registro. Un valor de `DEBUG` genera muchos mensajes de registro, lo que puede afectar negativamente al rendimiento. Se recomienda aplicar una configuración de `WARN` para un rendimiento óptimo. Sin embargo, este valor puede provocar la pérdida de información esencial en tiempo de ejecución, como las auditorías de licencias. Si desea guardar la información de registro con un impacto mínimo en el rendimiento, debe aplicar un valor de `INFO`.

* `<rollingFrequency>`  `rollingFrequency` especifica la frecuencia con la que los archivos de registro son *enrollado*. *`Rolling`* es un proceso que designa cualquier archivo de registro nuevo como registro activo. Por lo tanto, el archivo de registro activo anteriormente ya no se puede modificar y se considera *`rolled`*. Puede establecer el intervalo móvil en `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY`, o `NEVER`.

Consulte *Uso del SDK de DRM de Adobe Primetime para proteger el contenido* para obtener sugerencias sobre cómo optimizar el rendimiento.
