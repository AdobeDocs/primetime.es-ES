---
title: Depuración de encabezados
description: Depuración de encabezados
copied-description: true
exl-id: 42c19089-2c61-4622-b53a-c28b8d495ef8
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---

# Depuración de encabezados (X-ADBE-AI-X1) {#debugging-headers}

SSAI envía encabezados HTTP que se pueden utilizar para recopilar información y determinar el rendimiento de las sesiones de producción, ubicadas en el encabezado X-ADBE-AI-X1.

Ejemplo de encabezado:
`X-ADBE-AI-X1: 0 1 1594181097704 15126333-5ba9-49b8-a219-4f37e60d259c v 0 1 30 2 1 199 2 185 497 204 104 0 1 0 4`

La descripción de los campos es la siguiente:

| Nombre | Descripción | Ejemplo |
|--- |--- |--- |
| isActivePreroll | Si se ha enviado una llamada de anuncio para anuncio previo a la emisión | 0 |
| isActiveMidroll | Si se ha enviado una llamada de anuncio para midroll-roll | 1 |
| ID de solicitud | SSAI interno | 1594181097704 |
| ID de sesión | ID de sesión de la solicitud | 15126333-5ba9-49b8-a219-4f37e60d259c |
| Tipo de emisión | u=variant, l=live, v=vod | v |
| isBootstrap | Si esta solicitud es una llamada de arranque | 0 |
| Recuento de pausas publicitarias | Número total de pausas publicitarias en este manifiesto | 1 |
| Duración total de la pausa publicitaria | Duración total de la pausa publicitaria, en segundos | 30 |
| Recuento de llamadas de anuncio | Número de llamadas de anuncio enviadas en esta solicitud | 2 |
| Recuento de llamadas de anuncio de redireccionamiento | Número de llamadas de anuncio de redireccionamiento enviadas en esta solicitud | 1 |
| Duración total de la llamada de anuncio | Tiempo total de procesamiento de llamadas de anuncio | 199 |
| Recuento de anuncios insertados | Número de anuncios insertados en el manifiesto | 2 |
| Hora de solicitud de manifiesto de origen | Tiempo empleado para recuperar contenido | 185 |
| Tiempo total de la solicitud | Tiempo total empleado en recuperar contenido y anuncios | 497 |
| Tiempo de recuperación del manifiesto de anuncio (total) | Cantidad total de tiempo de recuperación de manifiestos de publicidad | 204 |
| Tiempo de recuperación del manifiesto de anuncio (real) | Cantidad real de tiempo de recuperación de manifiestos de publicidad en paralelo | 104 |
| Visitas de caché de contenido | Número de visitas de caché de contenido | 0 |
| Miss de caché de contenido | Número de errores de caché de contenido | 3 |
| Visita de caché del manifiesto de anuncio | Número de visitas de caché de manifiesto de publicidad | 0 |
| Error de caché de manifiesto de publicidad | Número de errores de caché de manifiesto de anuncio | 4 |
