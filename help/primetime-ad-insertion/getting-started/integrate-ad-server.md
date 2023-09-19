---
title: Integración del servidor de publicidad
description: Integración del servidor de publicidad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Integración del servidor de publicidad {#integrate-ad-server}

Para empezar, se le proporcionará un inicio de sesión para acceder a la consola del Ad Insertion de Primetime, donde configurará las reglas que utiliza el Ad Insertion de Primetime para reenviar solicitudes de publicidad al servidor de publicidad de su elección. El Ad Insertion de Primetime admite la mayoría de los servidores de publicidad compatibles con VAST o VMAP.

>[!NOTE]
>
>[Página VAST de IAB](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast)

## Compatibilidad con macros {#macro-support}

El Ad Insertion de Primetime habilita las siguientes macros de servidor de publicidad para todas las secuencias:

* Destrucción de caché
* Contexto de aplicación o URL de página
* Duración disponible
* Recurso de vídeo actual

Si se necesitan macros adicionales, póngase en contacto con el representante de soporte técnico de Adobe Primetime.

## Funciones avanzadas {#advanced-features}

Primetime Ad Insertion también incluye la toma de decisiones basada en reglas que habilita las funciones avanzadas. Esto puede ser importante si desea enrutar anuncios a diferentes servidores de publicidad en función de los derechos de inventario o habilitar límites de frecuencia para anuncios individuales. Para obtener más información, consulte [Funciones avanzadas](/help/primetime-ad-insertion/advanced-features/route-ads-based-on-rules.md).
