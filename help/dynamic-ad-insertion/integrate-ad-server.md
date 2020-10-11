---
title: Integrar el servidor de publicidad
description: Integración del servidor de publicidad
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Integrar el servidor de publicidad {#integrate-ad-server}

Para inicio, se le proporcionará un inicio de sesión para acceder a la consola de Ad Insertion Primetime, donde configurará las reglas que utiliza Primetime Ad Insertion para reenviar solicitudes de publicidad al servidor de publicidad de su elección. Primetime Ad Insertion admite la mayoría de servidores de publicidad compatibles con VAST o VMAP.

>[!NOTE]
>
>[Página IAB VAST](https://www.iab.com/guidelines/digital-video-ad-serving-template-vast)

## Compatibilidad con macros {#macro-support}

Primetime Ad Insertion habilita las siguientes macros del servidor de publicidad para todos los flujos:

* Descarga de caché
* Contexto de la aplicación o dirección URL de la página
* Duración promedio
* Recurso de vídeo actual

<!--For technical information regarding specific ad servers or ad macros, see [Supported ad servers and macros](supported-ad-servers-and-macros.md).-->

Si necesita macros adicionales, póngase en contacto con el representante de asistencia técnica de Adobe Primetime.

## Funciones avanzadas {#advanced-features}

Primetime Ad Insertion también ofrece decisiones basadas en reglas que permiten funciones avanzadas. Esto puede ser importante si desea enrutar las publicidades a diferentes servidores de publicidad en función de los derechos de inventario o habilitar el límite de frecuencia para las publicidades individuales. <!--For more information, see [Advanced Features](route-ads-based-on-rules.md).-->
