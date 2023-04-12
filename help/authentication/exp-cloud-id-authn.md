---
title: Uso del ID de Experience Cloud en la autenticación de Primetime
description: Uso del ID de Experience Cloud en la autenticación de Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# Uso del ID de Experience Cloud en la autenticación de Primetime

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## ¿Qué es el ID de Experience Cloud y cómo obtenerlo? {#what-exp-cloud-id-obtain}

El ID de Experience Cloud (ECID para abreviar) es un ID único que Adobe Experience Cloud genera para cada usuario individual de su aplicación/sitio web. ECID se utiliza principalmente en todos los informes de Experience Cloud que se utilizan para vincular información sobre un usuario específico en varias aplicaciones o sitios web.

Si ya dispone de un sistema que proporcione un ID de visitante, debe utilizar el mismo ID para el ámbito de este documento.

Una forma de obtener el ECID es utilizar el servicio de ID de Experience Cloud. Puede utilizar su tipo de implementación preferido, ya sea en función de TDM, biblioteca JS, servidor, integración directa o bibliotecas nativas para plataformas móviles. Para obtener una vista completa de los servicios, bibliotecas, SDK y guías de implementación disponibles, consulte: https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-implementation-guides.html





## ¿Cuál es la ventaja de utilizar el ID de Experience Cloud en la autenticación de Primetime? {#benefit-ex-cloud-id}

Si configura nuestros SDK y la API de REST sin cliente para que utilicen su ECID, más adelante podrá vincular los datos recopilados por la autenticación de Primetime a sus soluciones de Experience Cloud existentes. Esto le permitirá comprender mejor el recorrido y la experiencia de sus clientes en todas las soluciones que ofrece Adobe.

## ¿Cómo se utiliza el ID de Experience Cloud en la autenticación de Primetime? {#how-to-ex-cloud-id-authn}

Después de obtener el ECID (explicado anteriormente), debe pasar esta información a nuestros SDK y a nuestra API de REST sin clientes. Esta información se pasará posteriormente a nuestros servidores en cada llamada de red que realice el SDK. El proceso de configuración es diferente para cada SDK de la siguiente manera:

### SDK de JS {#js-sdk}

Para JavaScript, debe pasar el ECID en un mapa como tercer parámetro a la llamada setRequestor .

**Ejemplo de uso:**

```JavaScript
accessEnabler.setRequestor("REQUESTOR_ID", ["ENDPOINT_URL"],
    {
        "visitorID": "THE_ECID_VALUE"
    }
);
```

### SDK de iOS/tvOS {#ios-sdk}

Para el SDK de iOS/tvOS hay un método específico llamado setOptions.

**Ejemplo de uso:**

```JavaScript
accessEnabler.setOptions(
    [
        "visitorID": "THE_ECID_VALUE"
    ]
);
```

### SDK para Android/fireTV {#android-sdk}

Para el SDK de Android/fireTV, el mecanismo es similar a iOS. Solo el nombre del parámetro es diferente. La API está documentada aquí.

**Ejemplo de uso:**

```JavaScript
String visitor_id = "THE_ECID_VALUE";

HashMap<String, String> options = new HashMap();
options.put("ap_vi",visitor_id);

accessEnabler.setOptions(options);
```

### API sin cliente {#clientless-api}

Al usar Adobe Primetime mediante su API de REST, la variable **ECID** se debe enviar **en todas las API** como parámetro denominado **&#39;ap_vi&#39;**.

**Ejemplo de uso:**

`GET: https://api.auth.adobe.com/api/v1/authorize?...&ap_vi=THE_ECID_VALUE`