---
title: Reglas de reescritura y búsqueda de anuncios de manifiesto
description: 'Reglas de reescritura y búsqueda de anuncios de manifiesto '
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Reglas de reescritura y captura de anuncios de manifiesto {#manifest-rewriting}

Primetime Ad Insertion puede reescribir fragmentos y recuperar recursos con reglas de búsqueda y reemplazo sencillas.  Esto se puede usar para convertir https en solicitudes http, lo que aumentaría el rendimiento eliminando los apretones de manos TLS.  Esto también se puede usar para enviar recursos de publicidad y recursos de cdn desde la misma CDN.

Las reglas se definen como búsqueda/reemplazo de expresión normal y se pueden utilizar para transformar las direcciones URL antes de enviarlas, así como después de insertarlas en un manifiesto.

Esta regla de ejemplo convertirá todas las solicitudes de publicidad en domain.com de https a http.

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

La regla siguiente utilizará la CDN de contenido para enviar publicidades que se encuentran en la CDN de Adobe y almacenamiento.

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

Las reglas pueden nombrarse y habilitarse o deshabilitarse modificando el parámetro `ptprotoswitch` en la API de Bootstrap, que es una lista de reglas separadas por coma que se van a ejecutar.  Por ejemplo: estas dos reglas se pueden ejecutar configurando `ptprotoswitch=adfetch_rule1,adfetch_rule2`:

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