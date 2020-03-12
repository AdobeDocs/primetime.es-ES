---
seo-title: Monitoreo
title: Monitoreo
uuid: ee62c55f-0d44-40f4-a2c7-39456f4d3d99
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c

---


# Monitoreo{#monitoring}

Tanto el servidor de individualización como el servidor de generación de claves tienen una página de estado, que puede utilizar para determinar el estado de los servidores.

* **Página de estado de la individualización:** [!DNL https://SERVER:PORT/flashaccess/status]

   * Informa &quot;activo&quot; si el servidor de aplicaciones se está ejecutando y la aplicación puede realizar una solicitud GET al servidor de generación de claves
   * La página informa &quot;Vivo&quot; o nada. No se muestra información sobre la aplicación, por lo que esta página se puede utilizar para monitorear desde fuera del cortafuegos.

* **Página de estado de Generación de claves:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * Informa &quot;activo&quot; si se está ejecutando el servidor de aplicaciones
   * Todas las direcciones URL de generación de claves solo deben ser accesibles internamente

* **Página Estadísticas de individualización:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * Incluye estadísticas sobre el servidor de individualización, como el número de solicitudes servidas y el número de claves disponibles en la caché
   * Esta página solo debe ser accesible internamente

* **Página Estadísticas de Generación de Clave:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * Incluye estadísticas sobre el servidor de generación de claves, como el número de solicitudes servidas y el número de archivos clave disponibles en el disco
   * Todas las direcciones URL de generación de claves solo deben ser accesibles internamente

