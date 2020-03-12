---
description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-title: Usar el comportamiento de reproducción predeterminado
title: Usar el comportamiento de reproducción predeterminado
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Usar el comportamiento de reproducción predeterminado{#use-the-default-playback-behavior}

Puede elegir usar comportamientos de publicidad predeterminados.

Para utilizar comportamientos predeterminados:

    * Si implementa su propia clase &quot;ContentFactory&quot;, devuelva una nueva instancia de &quot;DefaultAdPolicySelector&quot; en la implementación de &quot;doRetrieveAdPolicySelector&quot;.
    
    &quot;CustomContentFactory de clase
    pública amplía ContentFactory {
    
    //...
    // su código personalizado para clases
    publicitarias//...
    
    /**
    * @inheritDoc
    */
    override protected
    functionRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector {
    return new DefaultAdPolicySelector(item);
    }
    }
    &quot;
    
    * Si no tiene una implementación personalizada para la clase `ContentFactory`, TVSDK utiliza el selector de &quot;AdPolicyAdPredeterminado&quot;&quot;.