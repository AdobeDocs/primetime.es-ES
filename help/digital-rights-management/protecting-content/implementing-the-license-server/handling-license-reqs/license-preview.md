---
title: Vista previa de licencia
description: Vista previa de licencia
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Vista previa de licencia{#license-preview}

El cliente puede enviar una solicitud de vista previa de licencia, lo que significa que la aplicación puede realizar una operación de vista previa antes de solicitar al usuario que compre el contenido para determinar si el equipo del usuario cumple realmente todos los criterios necesarios para la reproducción.

*`License preview`* hace referencia a la capacidad de un cliente para obtener una vista previa de la licencia (para ver qué derechos permite la licencia) en lugar de obtener una vista previa del contenido (ver una pequeña parte del contenido antes de decidir comprar). Algunos de los parámetros únicos de cada equipo son: las salidas disponibles y su estado de protección, la versión de tiempo de ejecución/DRM disponible y el nivel de seguridad del cliente DRM. El modo de vista previa de licencia permite al cliente de tiempo de ejecución/DRM probar la lógica empresarial del servidor de licencias y devolver la información al usuario para que pueda tomar una decisión informada. Por lo tanto, el cliente puede ver el aspecto de una licencia válida, pero no recibirá la clave para descifrar el contenido. La compatibilidad con la vista previa de licencias es opcional y solo es necesaria si implementa un cliente personalizado que utiliza esta funcionalidad.

Para determinar si el cliente envió una solicitud de vista previa o una solicitud de adquisición de licencia, llame a `LicenseRequestMessage.getRequestPhase()`y compárela a `LicenseRequestMessage.RequestPhase.Acquire`
