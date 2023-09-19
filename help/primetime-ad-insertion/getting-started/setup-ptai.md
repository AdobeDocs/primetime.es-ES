---
title: Configuración del Ad Insertion de Adobe Primetime
description: Configuración del Ad Insertion de Adobe Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Configuración del Ad Insertion de Adobe Primetime {#ptai-setup}

El proceso para configurar el Ad Insertion de Primetime es el siguiente:

1. Integre el servidor de publicidad en el Ad Insertion de Primetime iniciando sesión en la consola del Ad Insertion de Primetime y configurando reglas de redirección. Para obtener más información, consulte [Integración del servidor de publicidad](/help/primetime-ad-insertion/getting-started/integrate-ad-server.md).

1. Configure canales o plataformas en la consola de Ad Insertion de Primetime para garantizar dimensiones de informes adecuadas.

1. Configure e integre su CDN en el Ad Insertion de Primetime. Para obtener más información, consulte [Integración de su CDN](integrate-cdn.md).

1. Determine si el reempaquetado de anuncios justo a tiempo es necesario para el flujo de trabajo de publicidad. Póngase en contacto con el representante de soporte técnico de Primetime para habilitar el servicio.

1. Actualice la aplicación para que utilice [API de Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) para realizar y recibir solicitudes de Ad Insertion de Primetime y configurar la aplicación para que admita. Para obtener más información, consulte [Seguimiento de anuncios](set-up-ad-tracking.md).

1. Pruebe la aplicación para garantizar la reproducción correcta del anuncio utilizando [Herramientas de depuración](/help/primetime-ad-insertion/performance-monitoring-debugging-reporting/troubleshoot-and-debug.md).

1. Pruebe las aplicaciones para garantizar la activación correcta de las señalizaciones de seguimiento e impresión de anuncios mediante [Informes](/help/primetime-ad-insertion/performance-monitoring-debugging-reporting/reporting-and-billing.md).
