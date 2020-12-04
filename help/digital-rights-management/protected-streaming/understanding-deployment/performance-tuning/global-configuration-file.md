---
description: En este tema se describen las consideraciones relacionadas con el rendimiento. Cualquier configuración del archivo de configuración global denominada flashaccess-global.xml afecta al rendimiento.
seo-description: En este tema se describen las consideraciones relacionadas con el rendimiento. Cualquier configuración del archivo de configuración global denominada flashaccess-global.xml afecta al rendimiento.
seo-title: Archivo de configuración global
title: Archivo de configuración global
uuid: 254925b5-d441-4a35-ad6f-f99db5de7591
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Ajuste del rendimiento {#performance-tuning}

En este tema se describen las consideraciones relacionadas con el rendimiento. Cualquier configuración del archivo de configuración global denominada flashaccess-global.xml afecta al rendimiento.

## Archivo de configuración global {#global-configuration-file}

El archivo de configuración incluye los siguientes elementos de configuración:

* `<Caching>` El  `<Caching>` elemento controla el almacenamiento en caché de los archivos de configuración en la memoria. El elemento `<Caching>` admite la siguiente sintaxis:

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Controla la frecuencia con la que el servidor comprueba si hay actualizaciones en los archivos de configuración. Un valor bajo para `refreshDelaySeconds` afecta negativamente al rendimiento, mientras que un valor más alto puede mejorar el rendimiento.

   Consulte *Actualización de archivos de configuración* para obtener más información sobre `refreshDelaySeconds`.

* `numTenants` especifica el número de inquilinos. Un valor inferior al número de inquilinos afecta al rendimiento porque las solicitudes a los inquilinos restantes resultan en errores de caché. Un fallo en la caché de cualquier dato de configuración afecta negativamente al rendimiento. Por lo tanto, se recomienda que establezca este valor por encima del número de inquilinos configurados para el servidor, a menos que haya limitaciones de memoria que necesite tener en cuenta.

* `<Logging>` El  `<Logging>` elemento especifica el nivel de registro y la frecuencia con la que se desplazan los archivos de registro. El elemento `<Logging>` admite la siguiente sintaxis:

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` especifica mensajes en un registro. Un valor de `DEBUG` genera muchos mensajes de registro, lo que puede afectar negativamente al rendimiento. Se recomienda aplicar una configuración de `WARN` para obtener un rendimiento óptimo. Sin embargo, este valor puede resultar en la pérdida de información esencial del tiempo de ejecución, como las auditorías de licencias. Si desea guardar la información del registro con un impacto mínimo en el rendimiento, debe aplicar un valor de `INFO`.

* `<rollingFrequency>`  `rollingFrequency` especifica la frecuencia con la que se  *desplazan* los archivos de registro. *`Rolling`* es un proceso que designa cualquier archivo de registro nuevo como registro activo. Por lo tanto, el archivo de registro activo anteriormente ya no se puede modificar y se considera *`rolled`*. Puede establecer el intervalo móvil en `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY` o `NEVER`.

Consulte *Uso del SDK de Adobe Primetime DRM para la protección de contenido* para obtener sugerencias sobre cómo optimizar el rendimiento.