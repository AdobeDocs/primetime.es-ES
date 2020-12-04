---
seo-title: Previsualización de licencia
title: Previsualización de licencia
uuid: 3171647d-1437-48ab-9659-3eb363993618
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# Previsualización de licencia{#license-preview}

El cliente puede enviar una solicitud de previsualización de licencia, lo que significa que la aplicación puede realizar una operación de previsualización antes de solicitar al usuario que compre el contenido para determinar si el equipo del usuario cumple realmente todos los criterios necesarios para la reproducción. *La* vista previa de la licencia se refiere a la capacidad del cliente para realizar la previsualización de la licencia (para ver qué derechos permite la licencia) en lugar de la vista previa del contenido (ver una pequeña parte del contenido antes de decidir comprar). Algunos de los parámetros exclusivos de cada equipo son: las salidas disponibles y su estado de protección, la versión de tiempo de ejecución/DRM disponible y el nivel de seguridad del cliente DRM. El modo de previsualización de licencias permite al cliente de tiempo de ejecución/DRM probar la lógica empresarial del servidor de licencias y proporcionar información al usuario para que pueda tomar una decisión informada. Por lo tanto, el cliente puede ver el aspecto de una licencia válida, pero no recibirá la clave para descifrar el contenido. La compatibilidad con la previsualización de licencias es opcional y solo es necesaria si se implementa un cliente personalizado que utilice esta funcionalidad.

Para determinar si el cliente envió una solicitud de previsualización o de adquisición de licencia, llame a `LicenseRequestMessage.getRequestPhase()`y compárela con `LicenseRequestMessage.RequestPhase.Acquire`
