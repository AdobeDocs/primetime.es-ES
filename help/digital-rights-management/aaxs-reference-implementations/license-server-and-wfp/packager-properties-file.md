---
seo-title: Archivo de propiedades de Packager
title: Archivo de propiedades de Packager
uuid: 156624ec-66f0-4718-8a66-ed04a47f234d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Archivo de propiedades de Packager {#packager-properties-file}

Utilice el [!DNL flashaccess-refimpl-packager.properties] archivo para configurar el componente Watched Folder Packager de la implementación de referencia. Como mínimo, asegúrese de establecer la URL del servidor de licencias, el certificado del servidor de licencias, las credenciales del empaquetador y las opciones de protección de claves. Este archivo también contiene la ubicación de cada carpeta vigilada (packager.watchfolder.source). `n`). Los cambios realizados en los valores de este archivo de propiedades tendrán efecto la próxima vez que se ejecute el empaquetador de carpetas observado (no es necesario reiniciar el servidor). Sin embargo, si hay un error de configuración en el empaquetador, se cerrará el subproceso del empaquetador de carpetas observado y el servidor deberá reiniciarse para reiniciar el subproceso del empaquetador.
