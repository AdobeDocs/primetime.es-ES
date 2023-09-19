---
title: Archivo de propiedades del empaquetador
description: Archivo de propiedades del empaquetador
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Archivo de propiedades del empaquetador {#packager-properties-file}

Utilice el [!DNL flashaccess-refimpl-packager.properties] para configurar el componente Empaquetador de carpetas inspeccionadas de la implementación de referencia. Como mínimo, asegúrese de establecer la URL del servidor de licencias, el certificado del servidor de licencias, las credenciales del empaquetador y las opciones de protección de claves. Este archivo también contiene la ubicación de cada carpeta vigilada (packager.watchfolder.source). `n`). Cualquier cambio realizado en los valores de este archivo de propiedades surtirá efecto la próxima vez que se ejecute el empaquetador de carpetas vigiladas (no es necesario reiniciar el servidor). Sin embargo, si hay un error de configuración en el empaquetador, el subproceso del empaquetador de carpetas inspeccionado se cerrará y será necesario reiniciar el servidor para reiniciar el subproceso del empaquetador.
