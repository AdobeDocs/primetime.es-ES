---
title: Impedir que los MVPD aparezcan en el cuadro de diálogo Selección
description: Impedir que los MVPD aparezcan en el cuadro de diálogo Selección
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Impedir que los MVPD aparezcan en el cuadro de diálogo Selección

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Problema {#issue-prevent-mvpd-sel-dialog}

Debe evitar que los MVPD específicos (&quot;lista de bloqueados&quot;) aparezcan en el selector de MVPD.


## Solución {#solution-prevent-mvpd-sel-dialog}

La solución es hacer una lista de bloqueados cuando `displayProviderDialog()` se llama.

Por ejemplo, si desea que CableCompany_1 y CableCompany_2 no se muestren dentro del selector de MVPD, haría algo así como se muestra en el siguiente ejemplo.

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if (!isBlocklisted(currentMvpd.ID)) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isBlocklisted(mvpdID) {
    // Implement block-listing on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
} 
```

<!--
**Related Information**

* [Allow MVPDs in the Selection Dialog](/help/authentication/allow-mvpd-selectn-dialog.md)
* **Code samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->