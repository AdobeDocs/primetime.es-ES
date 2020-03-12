---
description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-title: Usar el comportamiento de reproducción predeterminado
title: Usar el comportamiento de reproducción predeterminado
uuid: 36f76c42-4c6c-4620-9b47-ec97519a642a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Usar el comportamiento de reproducción predeterminado {#use-the-default-playback-behavior}

Puede elegir usar comportamientos de publicidad predeterminados.

1. Para utilizar comportamientos predeterminados, realice una de las siguientes tareas:

   * Si implementa su propia `AdvertisingFactory` clase, devuelva null para `createAdPolicySelector`.

   * Si no tiene una implementación personalizada para la `AdvertisingFactory` clase, TVSDK utiliza un selector de directivas de publicidad predeterminado.

## Configurar la reproducción personalizada {#set-up-customized-playback}

Puede personalizar o anular los comportamientos de publicidad.

Antes de poder personalizar o anular los comportamientos de publicidad, registre la instancia de directiva de publicidad con .
Para personalizar los comportamientos de las publicidades, realice una de las siguientes acciones:

* Implementar la `AdPolicySelector` interfaz y todos sus métodos.

   Esta opción se recomienda si necesita anular **todos** los comportamientos de publicidad predeterminados.

* Amplíe la `DefaultAdPolicySelector` clase y proporcione implementaciones solo para aquellos comportamientos que requieran personalización.

   Esta opción se recomienda si necesita anular solo **algunos** de los comportamientos predeterminados.

Para personalizar los comportamientos de publicidad:

1. Implementar la `AdPolicySelector` interfaz y todos sus métodos.
1. Asigne la instancia de directiva que usará TVSDK a través de la fábrica de publicidad.

>[!NOTE]
>class CustomContentFactory extiende ContentFactory {
>...
>@Override
>public AdPolicySelector recuperarAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) {
>return new CustomAdPolicySelector(mediaPlayerItem);
>}
>...
>}
>// registrar la fábrica de contenido personalizado con el reproductor de medios
>Configuración de MediaPlayerItemConfig = new MediaPlayerItemConfig();
>config.setAdvertisingFactory(new CustomContentFactory());
>// esta configuración debe pasarse más tarde mientras se carga >el recurso
>mediaPlayer.replaceCurrentResource(resource, config);

1. Implemente sus personalizaciones.