---
title: Monitorización
description: Monitorización
copied-description: true
exl-id: edf62298-4082-4ac1-b2b7-8d0e0959ed04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Monitorización{#monitoring}

El servidor de individualización y el servidor de generación de claves tienen una página de estado que puede utilizar para determinar el estado de los servidores.

* **Página de estado de individualización:** [!DNL https://SERVER:PORT/flashaccess/status]

   * Informa de &quot;Activo&quot; si el servidor de la aplicación se está ejecutando y la aplicación puede realizar una solicitud de GET al servidor de generación de claves
   * La página informa de &quot;Vivo&quot; o nada. No se muestra ninguna información sobre la aplicación, por lo que esta página podría utilizarse para la monitorización desde fuera del cortafuegos.

* **Página de estado de generación de claves:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * Informa de &quot;Activo&quot; si el servidor de la aplicación se está ejecutando
   * Todas las URL de generación de claves solo deben ser accesibles internamente

* **Página Estadísticas de Individualización:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * Incluye estadísticas sobre el servidor de individualización, como el número de solicitudes atendidas y el número de claves disponibles en la caché
   * Esta página solo debe ser accesible internamente

* **Página Estadísticas de Generación de Claves:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * Incluye estadísticas sobre el servidor de generación de claves, como el número de solicitudes servidas y el número de archivos de claves disponibles en el disco
   * Todas las URL de generación de claves solo deben ser accesibles internamente
