---
title: Archivo de propiedades del paquete
description: Archivo de propiedades del paquete
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Archivo de propiedades del paquete {#packager-properties-file}

Utilice el archivo [!DNL flashaccess-refimpl-packager.properties] para configurar el componente del empaquetador de carpetas vigiladas de la implementación de referencia. Como mínimo, asegúrese de establecer la URL del servidor de licencias, el certificado del servidor de licencias, las credenciales del empaquetador y las opciones de protección de claves. Este archivo también contiene la ubicación de cada carpeta vigilada (packager.watchfolder.source). `n`). Cualquier cambio realizado en los valores de este archivo de propiedad surtirá efecto la próxima vez que se ejecute el paquete de carpetas visto (no es necesario reiniciar el servidor). Sin embargo, si hay un error de configuración en el empaquetador, se cerrará el subproceso del empaquetador de carpetas visto y el servidor deberá reiniciarse para reiniciar el subproceso del empaquetador.
