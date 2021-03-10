---
description: Adobe Primetime DRM es una solución avanzada de Digital Rights Management (DRM) y protección de contenido para contenido audiovisual de alto valor. En las aplicaciones que admiten la creación de API de Java, puede utilizar el SDK de DRM de Primetime para especificar políticas de DRM, aplicar dichas políticas al contenido y cifrar ese contenido.
title: Novedades de Adobe Primetime DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Novedades de Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM es una solución avanzada de Digital Rights Management (DRM) y protección de contenido para contenido audiovisual de alto valor. En las aplicaciones que admiten la creación de API de Java, puede utilizar el SDK de DRM de Primetime para especificar políticas de DRM, aplicar dichas políticas al contenido y cifrar ese contenido.

>[!NOTE]
>
>Primetime DRM antes se llamaba Acceso al Adobe, y antes de eso, Flash Access.

A continuación se muestra una explicación general del proceso de protección de contenido:

1. Utilice las API de Java de DRM para establecer las propiedades de la directiva de DRM y los parámetros de codificación.
1. Cree una directiva DRM que describa las funciones de uso de cualquier contenido.

   Puede crear cualquier número de directivas de DRM. La mayoría de los usuarios crean un pequeño número de directivas y luego las aplican a muchos archivos.
1. Empaquete un archivo multimedia.

   *`Packaging a file`* significa que se cifra el archivo y, a continuación, se aplica una directiva DRM al archivo.
1. Implemente el servidor de licencias para emitir una licencia al usuario.

Con la finalización de estos pasos, el contenido cifrado está listo para la implementación. Después de la implementación, un cliente puede solicitar una licencia al servidor de licencias y, tras la recepción, puede reproducir el contenido.

El SDK de DRM de Primetime proporciona una API de Java para completar estas tareas. El SDK incluye implementaciones de referencia del servidor de licencias y de las herramientas de línea de comandos, ambas basadas en las API Java del SDK de DRM.

Las funciones que se describen a continuación son nuevas en esta versión.

## Nuevas funciones {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **Parada dura:** puede especificar si la reproducción se detiene o continúa al final de una ventana de reproducción.
* **Controles de salida dependientes de la resolución:** puede especificar restricciones de salida basadas en resoluciones de píxeles.
* **Anonimización de las respuestas del servidor de licencias:** para mejorar la privacidad con los protocolos del servidor de licencias DRM de Primetime, el número de serie del certificado de transporte se pondrá a cero para las respuestas del servidor de licencias a los clientes de asistencia.

