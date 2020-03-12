---
description: Adobe Primetime DRM es una solución avanzada de gestión de derechos digitales (DRM) y protección de contenido para contenido audiovisual de gran valor. En las aplicaciones que admiten la creación de API de Java, puede utilizar el SDK de DRM de Primetime para especificar políticas de DRM, aplicar dichas políticas al contenido y cifrar dicho contenido.
seo-description: Adobe Primetime DRM es una solución avanzada de gestión de derechos digitales (DRM) y protección de contenido para contenido audiovisual de gran valor. En las aplicaciones que admiten la creación de API de Java, puede utilizar el SDK de DRM de Primetime para especificar políticas de DRM, aplicar dichas políticas al contenido y cifrar dicho contenido.
seo-title: Novedades de Adobe Primetime DRM
title: Novedades de Adobe Primetime DRM
uuid: 3c8da594-a231-4496-bffc-130775ecae50
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Novedades de Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM es una solución avanzada de gestión de derechos digitales (DRM) y protección de contenido para contenido audiovisual de gran valor. En las aplicaciones que admiten la creación de API de Java, puede utilizar el SDK de DRM de Primetime para especificar políticas de DRM, aplicar dichas políticas al contenido y cifrar dicho contenido.

>[!NOTE]
>
>Primetime DRM se llamaba anteriormente Adobe Access y antes de eso, Flash Access.

A continuación se muestra una descripción detallada del proceso de protección de contenido:

1. Utilice las API de Java de DRM para establecer las propiedades de directiva de DRM y los parámetros de codificación.
1. Cree una directiva DRM que describa las funciones de uso de cualquier contenido.

   Puede crear cualquier número de directivas DRM. La mayoría de los usuarios crea un pequeño número de directivas y, a continuación, las aplica a muchos archivos.
1. Empaquete un archivo multimedia.

   *`Packaging a file`* significa que se cifra el archivo y, a continuación, se aplica una política de DRM al archivo.
1. Implemente el servidor de licencias para emitir una licencia al usuario.

Al completar estos pasos, el contenido cifrado está listo para la implementación. Después de la implementación, un cliente puede solicitar una licencia del servidor de licencias y, una vez recibida, puede reproducir el contenido.

El SDK de DRM de Primetime proporciona una API de Java para completar estas tareas. El SDK incluye implementaciones de referencia del servidor de licencias y de las herramientas de la línea de comandos, ambas basadas en las API de Java del SDK de DRM.

Las funciones que se describen a continuación son nuevas en esta versión.

## Nuevas funciones {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **Parada dura:** puede especificar si la reproducción se detiene o continúa al final de una ventana de reproducción.
* **Controles de salida dependientes de la resolución:** puede especificar restricciones de salida basadas en resoluciones de píxeles.
* **Anonimización de las respuestas del servidor de licencias:** para mejorar la privacidad con los protocolos del servidor de licencias DRM de Primetime, el número de serie del certificado de transporte se centra en las respuestas del servidor de licencias a los clientes de soporte.

