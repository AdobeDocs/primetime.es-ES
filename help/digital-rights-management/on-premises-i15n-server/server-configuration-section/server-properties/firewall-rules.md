---
title: Reglas del cortafuegos
description: Reglas del cortafuegos
copied-description: true
exl-id: 1a40822a-893d-43ec-9c3e-8e0b4ebe6d01
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Reglas del cortafuegos{#firewall-rules}

Para proteger el acceso al servidor de individualización, solo es necesario exponer determinadas rutas de aplicación. El servidor de individualización debe aceptar solicitudes de clientes a estas rutas:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Rutas de servicio, como [!DNL /flashaccess/admin/*] (es decir, las páginas de estado y administración) solo deben ser accesibles desde el cortafuegos. No se debe acceder a ninguna parte del servidor de generación de claves desde fuera del cortafuegos.
