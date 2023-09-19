---
title: Reglas de reescritura de manifiestos y recuperación de anuncios
description: Reglas de reescritura de manifiestos y recuperación de anuncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Reglas de reescritura de manifiestos y recuperación de anuncios {#manifest-rewriting}

El Ad Insertion de Primetime puede volver a escribir fragmentos y recuperar recursos mediante reglas sencillas de búsqueda y sustitución.  Esto se puede utilizar para convertir https en solicitudes http, lo que aumentaría el rendimiento al eliminar los protocolos de enlace TLS.  Esto también se puede utilizar para enviar recursos de publicidad y de red de distribución de contenido (cdn) desde la misma CDN.

Las reglas se definen como búsqueda/sustitución de expresiones regulares y se pueden utilizar para transformar las direcciones URL antes de enviarlas, así como después de insertarlas en un manifiesto.

Esta regla de ejemplo convertirá todas las solicitudes de publicidad a domain.com de https a http.

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

La siguiente regla utilizará la CDN de contenido para enviar anuncios que se encuentren en la CDN de almacenamiento de anuncios de Adobe.

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

Las reglas se pueden nombrar y habilitar/deshabilitar modificando la variable `ptprotoswitch` en la API de Bootstrap, que es una lista de reglas separadas por coma que se van a ejecutar.  Por ejemplo, estas dos reglas se pueden ejecutar al establecer `ptprotoswitch=adfetch_rule1,adfetch_rule2`:

```
<ruleSet>
    <rule name="rule1">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
    <rule name="rule2">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
</ruleSet>
```

Póngase en contacto con el servicio de asistencia técnica para crear o habilitar estas reglas para su cuenta.
