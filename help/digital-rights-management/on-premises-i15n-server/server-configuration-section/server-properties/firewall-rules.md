---
seo-title: Reglas de cortafuegos
title: Reglas de cortafuegos
uuid: f1629ceb-22de-4bb5-b73f-9b874d97ea8b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Reglas de cortafuegos{#firewall-rules}

Para asegurar el acceso al servidor de individualización, solo es necesario exponer determinadas rutas de aplicación. El servidor de individualización debe aceptar solicitudes de los clientes a estas rutas:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Las rutas de servicio, como [!DNL /flashaccess/admin/*] (es decir, las páginas de estado y administración) sólo deben ser accesibles desde el servidor de seguridad. No se debe acceder a ninguna parte del servidor de generación de claves desde fuera del servidor de seguridad.
