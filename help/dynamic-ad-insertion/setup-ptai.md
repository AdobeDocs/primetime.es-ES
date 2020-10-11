---
title: Configurar Adobe Primetime Ad Insertion
description: Configuración de Adobe Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# Configurar Adobe Primetime Ad Insertion {#ptai-setup}

El proceso para configurar Primetime Ad Insertion es el siguiente:

1. Integre el servidor de publicidad en el Ad Insertion Primetime iniciando sesión en la consola del Ad Insertion Primetime y configurando las reglas de redirección. Para obtener más información, consulte [Integración del servidor](integrate-ad-server.md)de publicidad.

1. Configure canales o plataformas en la consola Ad Insertion Primetime para garantizar unas dimensiones de sistema de informes adecuadas.

1. Configure e integre su CDN en Primetime Ad Insertion. Para obtener más información, consulte [Integración de su CDN](integrate-cdn.md).

1. Determinar si el reempaquetado de anuncios justo a tiempo es necesario para el flujo de trabajo de la publicidad. Póngase en contacto con el representante de asistencia técnica de Primetime para habilitar el servicio.

1. Actualice la aplicación para que utilice la API [de](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md) Bootstrap para realizar y recibir solicitudes para Primetime Ad Insertion, y configure la aplicación para que sea compatible. Para obtener más información, consulte Seguimiento [de publicidad](set-up-ad-tracking.md).

1. Pruebe la aplicación para garantizar una reproducción correcta de la publicidad. <!-- using the [Debugging tools](troubleshoot-and-debug.md).-->

1. Pruebe las aplicaciones para garantizar la activación correcta del seguimiento de publicidad y las señalizaciones de impresión.<!-- using the [Reporting](reporting-and-billing.md).-->
