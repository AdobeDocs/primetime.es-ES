---
description: Adobe Primetime DRM es una solución de protección de contenidos y Digitales Rights Management avanzados (DRM) para contenido audiovisual de alto valor. En las aplicaciones que admiten la creación de API de Java, puede utilizar el SDK de DRM de Primetime para especificar directivas de DRM, aplicarlas al contenido y cifrar dicho contenido.
title: Novedades de Adobe Primetime DRM
exl-id: 998dae80-b3d3-419e-8fd3-d925a83d8b53
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Novedades de Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM es una solución de protección de contenidos y Digitales Rights Management avanzados (DRM) para contenido audiovisual de alto valor. En las aplicaciones que admiten la creación de API de Java, puede utilizar el SDK de DRM de Primetime para especificar directivas de DRM, aplicarlas al contenido y cifrar dicho contenido.

>[!NOTE]
>
>Primetime DRM se llamaba anteriormente Acceso de Adobe, y antes de eso, Flash Access.

A continuación se muestra una explicación detallada de alto nivel del proceso de protección de contenido:

1. Utilice las API de Java de DRM para establecer las propiedades de directivas de DRM y los parámetros de cifrado.
1. Cree una directiva DRM que describa las funciones de uso de cualquier contenido.

   Puede crear cualquier número de políticas de DRM. La mayoría de los usuarios crea un pequeño número de directivas y, a continuación, las aplica a muchos archivos.
1. Empaquete un archivo multimedia.

   *`Packaging a file`* significa que se cifra el archivo y, a continuación, se aplica una directiva DRM al archivo.
1. Implemente el servidor de licencias para emitir una licencia al usuario.

Al completar estos pasos, el contenido cifrado está listo para su implementación. Después de la implementación, un cliente puede solicitar una licencia al servidor de licencias y, al recibirla, puede reproducir el contenido.

El SDK de DRM de Primetime proporciona una API de Java para completar estas tareas. El SDK incluye implementaciones de referencia del servidor de licencias y herramientas de línea de comandos, ambas basadas en las API de Java del SDK de DRM.

Las funciones que se describen a continuación son nuevas en esta versión.

## Nuevas funciones {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **Parada rígida -** Puede especificar si la reproducción se detiene o continúa al final de una ventana de reproducción.
* **Controles de salida dependientes de la resolución -** Puede especificar restricciones de salida en función de las resoluciones de píxel.
* **Anonimización de las respuestas del servidor de licencias:** Para mejorar la privacidad con los protocolos del servidor de licencias DRM de Primetime, el número de serie del certificado de transporte se pondrá a cero para las respuestas del servidor de licencias a los clientes de soporte.
