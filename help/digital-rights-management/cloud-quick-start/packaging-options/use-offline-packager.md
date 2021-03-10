---
title: Usar el Primetime Offline Packager incluido
description: Usar el Primetime Offline Packager incluido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Utilice el Primetime Offline Packager incluido{#use-the-included-primetime-offline-packager}

Su Java Packager de Primetime viene preconfigurado con la mayoría de las opciones que necesita para empaquetar contenido. Solo hay algunas áreas que actualizar para empezar.

## Actualizar propiedades del empaquetador {#section_99904D35E99944A28FF43D924E516CC2}

Contexto de la tarea actual

* Actualice las siguientes propiedades del empaquetador antes de utilizar el archivo de configuración para empaquetar el contenido:

### Propiedades del archivo de configuración XML proporcionado por el usuario

| Nombre de propiedad | Descripción |
|---|---|
| `policy_file` | ruta del archivo de directiva. El Adobe proporcionará varias políticas preconfiguradas entre las que elegir. |
| `pkgr_pfx` | Ruta de acceso de las credenciales de Packager. Debe proporcionar su propia credencial de empaquetador emitido por Adobe ( [!DNL .pfx]) aquí. |
| `pkgr_pfx_pwd` | Contraseña de las credenciales de Packager. Debe proporcionar la contraseña a su credencial de empaquetador emitida por Adobe aquí. |

## Paquete utilizando la línea de comandos {#section_DFBE462679E34D62963BE201FD3321F9}

Antes de empaquetar contenido, asegúrese de que ha proporcionado toda la información necesaria en el archivo de configuración.

* Para empaquetar contenido con el archivo de configuración, utilice la siguiente sintaxis en la línea de comandos:

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

Se proporcionan archivos de configuración de muestra para empaquetar el contenido en formato HLS o HDS, llamados [!DNL config_hds.xml] y [!DNL config.hls.xml].

El contenido del HDS o HLS se enviará a la carpeta [!DNL /output] en el directorio del Kit de protección. Todos los artefactos escritos en este directorio deben alojarse en un servidor web HTTP para que se puedan reproducir.
