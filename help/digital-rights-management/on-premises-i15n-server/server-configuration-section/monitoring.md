---
title: Monitorización
description: Monitorización
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Monitorización{#monitoring}

El servidor de Individualización y el servidor de generación de claves tienen cada uno una página de estado que puede utilizar para determinar el estado de los servidores.

* **Página de estado de individualización:** [!DNL https://SERVER:PORT/flashaccess/status]

   * Informa de &quot;activo&quot; si el servidor de aplicaciones se está ejecutando y la aplicación puede realizar una solicitud de GET al servidor de generación de claves
   * La página indica &quot;Vivo&quot; o nada. No se muestra información sobre la aplicación, por lo que esta página puede utilizarse para monitorizar desde fuera del cortafuegos.

* **Página de estado de generación de claves:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * Informa de &quot;activo&quot; si el servidor de aplicaciones se está ejecutando
   * Todas las direcciones URL de generación de claves solo deben ser accesibles internamente

* **Página Estadísticas de Individualización:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * Incluye estadísticas sobre el servidor de Individualización, como el número de solicitudes servidas y el número de claves disponibles en la caché
   * Esta página solo debe ser accesible internamente

* **Página Estadísticas de Generación de Claves:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * Incluye estadísticas sobre el servidor de generación de claves, como el número de solicitudes servidas y el número de archivos clave disponibles en el disco
   * Todas las direcciones URL de generación de claves solo deben ser accesibles internamente

