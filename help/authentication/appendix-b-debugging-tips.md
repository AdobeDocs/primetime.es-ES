---
title: Apéndice B "Sugerencias de depuración"
description: Apéndice B "Sugerencias de depuración"
exl-id: ea024797-315e-47c0-99ea-1ac49c8c9697
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Apéndice B: Sugerencias de depuración {#appendix-b-debugging-tips}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.


## Borrando datos temporales {#clearing-temporary-data}

La autenticación de Adobe Primetime almacena datos temporales, como la caché del explorador, la caché de LSO y las cookies. Borrar los datos temporales es importante para asegurarse de que obtiene una pizarra limpia al realizar pruebas.

- [Borrado de la caché y las cookies del explorador](#clearing-the-browser-cache-and-cookies)
- [Borrando caché de LSO](#clearing-lsos-cache)\
    

## Borrado de la caché y las cookies del explorador {#clearing-the-browser-cache-and-cookies}

Es fiable para el navegador, pero en Firefox: &quot;Herramientas&quot; -\> &quot;Borrar historial reciente...&quot; -\> En &quot;Intervalo de tiempo para borrar:&quot; seleccione &quot;Todo&quot;; y en &quot;Detalles&quot;: marque las &quot;Cookies&quot; y &quot;Caché&quot; -\> Haga clic en &quot;Borrar ahora&quot;.\
 

## Borrando caché de LSO {#clearing-lsos-cache}

Acceda a la [ayuda de Flash Player](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager07.html).

Seleccione el ```entitlement.\*``` (según lo que se pruebe) y haga clic en &quot;Eliminar sitio web&quot;.\
 

## Herramientas de depuración {#tools}

Los ingenieros de autenticación de Adobe Primetime utilizan las siguientes herramientas de depuración:

- Firebug - <http://www.getfirebug.com/>
- Flashbug (funciona con la versión de depuración del reproductor Flash) <https://addons.mozilla.org/en-US/firefox/addon/14465/>
- Encabezados http activos: <https://addons.mozilla.org/en-US/firefox/addon/3829/>
- Fiddler - <http://www.fiddler2.com/fiddler2/>
- Charles: <http://www.charlesproxy.com/>
- Wireshark: <http://www.wireshark.org/>


<!--
## Related Information

- [Programmer Integration Guide](/help/authentication/programmer-integration-guide-overview.md)

- [Using Charles Proxy (Tech Note)](https://tve.zendesk.com/hc/en-us/articles/204962849-Using-Charles-Proxy)
-->
