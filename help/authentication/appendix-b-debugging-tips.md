---
title: Apéndice B "Consejos de depuración"
description: Apéndice B "Consejos de depuración"
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Apéndice B: Sugerencias de depuración {#appendix-b-debugging-tips}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


## Borrado de datos temporales {#clearing-temporary-data}

La autenticación de Adobe Primetime almacena datos temporales, como la caché del explorador, la caché de LSO y las cookies. Es importante borrar los datos temporales para asegurarse de obtener una pizarra limpia durante las pruebas.

- [Borrado de la caché del explorador y las cookies](#clearing-the-browser-cache-and-cookies)
- [Borrado de la caché de LSO](#clearing-lsos-cache)\
    

## Borrado de la caché del explorador y las cookies {#clearing-the-browser-cache-and-cookies}

Es fiable para el explorador, pero en Firefox: &quot;Herramientas&quot; -\> &quot;Borrar historial reciente...&quot; -\> En &quot;Intervalo de tiempo para borrar:&quot; seleccione &quot;Todo&quot;; y en &quot;Detalles&quot;: marque &quot;Cookies&quot; y &quot;Caché&quot; -\> Haga clic en &quot;Borrar ahora&quot;.\
 

## Borrado de la caché de LSO {#clearing-lsos-cache}

Acceda a la [Ayuda de Flash Player](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager07.html).

Seleccione el ```entitlement.\*``` (dependiendo de lo que se pruebe) y haga clic en &quot;Eliminar sitio web&quot;.\
 

## Herramientas de depuración {#tools}

Los ingenieros de autenticación de Adobe Primetime utilizan las siguientes herramientas de depuración:

- Firebug - <http://www.getfirebug.com/>
- Flashbug (funciona con la versión de depuración del reproductor Flash) <https://addons.mozilla.org/en-US/firefox/addon/14465/>
- Encabezados http en directo - <https://addons.mozilla.org/en-US/firefox/addon/3829/>
- Fiddler <http://www.fiddler2.com/fiddler2/>
- Charles - <http://www.charlesproxy.com/>
- Wireshark - <http://www.wireshark.org/>


<!--
## Related Information

- [Programmer Integration Guide](/help/authentication/programmer-integration-guide-overview.md)

- [Using Charles Proxy (Tech Note)](https://tve.zendesk.com/hc/en-us/articles/204962849-Using-Charles-Proxy)
-->