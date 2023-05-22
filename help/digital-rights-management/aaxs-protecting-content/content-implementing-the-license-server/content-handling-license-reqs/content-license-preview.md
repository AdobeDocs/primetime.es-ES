---
title: Previsualización de licencia
description: Previsualización de licencia
copied-description: true
exl-id: 283ee661-b1ee-46b9-9337-0497c97bd785
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Previsualización de licencia{#license-preview}

El cliente puede enviar una solicitud de previsualización de licencia, lo que significa que la aplicación puede realizar una operación de previsualización antes de pedir al usuario que compre el contenido para determinar si el equipo del usuario cumple realmente todos los criterios necesarios para la reproducción. *Previsualización de licencia* se refiere a la capacidad del cliente para obtener una vista previa de la licencia (para ver qué derechos permite la licencia), en lugar de obtener una vista previa del contenido (viendo una pequeña parte del contenido antes de decidir comprar). Algunos de los parámetros que son únicos para cada equipo son: salidas disponibles y su estado de protección, la versión de tiempo de ejecución/DRM disponible y el nivel de seguridad del cliente DRM. El modo de vista previa de licencia permite al cliente de tiempo de ejecución/DRM probar la lógica empresarial del servidor de licencias y proporcionar información al usuario para que pueda tomar una decisión informada. Por lo tanto, el cliente puede ver el aspecto de una licencia válida, pero en realidad no recibiría la clave para descifrar el contenido. La compatibilidad con la vista previa de licencias es opcional y solo es necesaria si implementa un cliente personalizado que utilice esta funcionalidad.

Para determinar si el cliente envió una solicitud de previsualización o de adquisición de licencia, llame a `LicenseRequestMessage.getRequestPhase()`y compararlo con `LicenseRequestMessage.RequestPhase.Acquire`
