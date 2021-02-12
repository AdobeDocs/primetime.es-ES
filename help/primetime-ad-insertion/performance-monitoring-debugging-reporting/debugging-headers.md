---
title: Encabezados de depuración
description: null
translation-type: tm+mt
source-git-commit: 45e5c8e6144adf4a405bde7d8d19505b7ad549e0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 7%

---


# Depuración de encabezados (X-ADBE-AI-X1) {#debugging-headers}

SSAI envía encabezados HTTP que pueden utilizarse para recopilar información y determinar el rendimiento de las sesiones de producción, ubicadas en el encabezado X-ADBE-AI-X1.

Ejemplo de encabezado:
`X-ADBE-AI-X1: 0 1 1594181097704 15126333-5ba9-49b8-a219-4f37e60d259c v 0 1 30 2 1 199 2 185 497 204 104 0 1 0 4`

La descripción de los campos es la siguiente:

| Nombre | Descripción | Ejemplo |
|--- |--- |--- |
| isActivePreroll | Indica si se ha enviado una llamada de anuncio para la versión preliminar | 0 |
| isActiveMidroll | Si se envió una llamada de publicidad para el registro de midroll | 3 |
| Id. de solicitud | SSAI interno | 1594181097704 |
| ID de sesión | ID de sesión de la solicitud | 15126333-5ba9-49b8-a219-4f37e60d259c |
| Tipo de flujo | u=variante, l=activo, v=vod | v |
| isBootstrap | Si esta solicitud es una llamada de arranque | 0 |
| Recuento de saltos de publicidad | Número total de saltos de publicidad en este manifiesto | 3 |
| Duración total de la pausa publicitaria | Duración total de la pausa publicitaria, en segundos | 30 |
| Recuento de llamadas de publicidad | Número de llamadas de publicidad enviadas en esta solicitud | 2 |
| Recuento de llamadas de publicidad de redireccionamiento | Número de llamadas de publicidad de redireccionamiento enviadas en esta solicitud | 1 |
| Duración total de la llamada de publicidad | Tiempo total de procesamiento de llamadas de publicidad | 199 |
| Recuento de anuncios insertados | Número de publicidades insertadas en el manifiesto | 2 |
| Hora de solicitud de manifiesto de origen | Tiempo empleado en recuperar contenido solamente | 185 |
| Tiempo total de solicitud | Tiempo total empleado en la búsqueda de contenido y anuncios | 497 |
| Tiempo de captura del manifiesto de publicidad (total) | Cantidad total de tiempo de recuperación de manifiestos publicitarios | 204 |
| Tiempo de captura del manifiesto de publicidad (real) | Cantidad real de tiempo que se recuperan los manifiestos de publicidad en paralelo | 104 |
| Visitas a la caché de contenido | Número de visitas a la caché de contenido | 0 |
| Error de caché de contenido | Número de errores de caché de contenido | 3 |
| Visita a la caché de manifiestos de publicidad | Número de visitas de caché de manifiesto de publicidad | 0 |
| Error de caché de manifiesto de publicidad | Número de errores de caché de manifiesto de publicidad | 4 |