---
title: Utilizar el empaquetador sin conexión de Primetime incluido
description: Utilizar el empaquetador sin conexión de Primetime incluido
copied-description: true
exl-id: 6a1d0dc3-8906-4de5-8351-890c1cf31efd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Utilizar el empaquetador sin conexión de Primetime incluido{#use-the-included-primetime-offline-packager}

El empaquetador Java de Primetime viene preconfigurado con la mayoría de las opciones que necesita para empaquetar contenido. Solo hay unas pocas áreas que actualizar para comenzar.

## Actualizar propiedades del empaquetador {#section_99904D35E99944A28FF43D924E516CC2}

Contexto de la tarea actual

* Actualice las siguientes propiedades del empaquetador antes de utilizar el archivo de configuración para empaquetar el contenido:

### Propiedades del archivo de configuración XML proporcionado por el usuario

| Nombre de propiedad | Descripción |
|---|---|
| `policy_file` | ruta del archivo de directivas. El Adobe debe proporcionar varias políticas preconfiguradas entre las que elegir. |
| `pkgr_pfx` | Ruta de credenciales del empaquetador. Debe proporcionar sus propias credenciales de empaquetador emitidas por el Adobe ( [!DNL .pfx]) aquí. |
| `pkgr_pfx_pwd` | Contraseña de credenciales del empaquetador. Debe proporcionar la contraseña a la credencial de empaquetador emitida por el Adobe aquí. |

## Empaquetar mediante la línea de comandos {#section_DFBE462679E34D62963BE201FD3321F9}

Antes de empaquetar el contenido, asegúrese de que ha proporcionado toda la información necesaria en el archivo de configuración.

* Para empaquetar contenido con el archivo de configuración, utilice la siguiente sintaxis en la línea de comandos:

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

Se proporcionan archivos de configuración de muestra para empaquetar el contenido en formato HLS o HDS, denominados [!DNL config_hds.xml] y [!DNL config.hls.xml].

El contenido del HDS o del HLS se envía al [!DNL /output] en el directorio de Kit de protección. Todos los artefactos escritos en este directorio deben alojarse en un servidor web HTTP para poder reproducirse.
