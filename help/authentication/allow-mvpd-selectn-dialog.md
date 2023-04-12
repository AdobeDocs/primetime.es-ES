---
title: Permitir MVPD en el cuadro de diálogo de selección
description: Permitir MVPD en el cuadro de diálogo de selección
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Permitir MVPD en el cuadro de diálogo de selección {#allow-mvpds-selection-dialog}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Problema {#issue}

Es posible que el programador desee probar o comprobar la experiencia del usuario con las nuevas integraciones de MVPD antes de publicarla entre los usuarios finales.

## Solución {#solution}

En el `displayProviderDialog()` llamada de retorno, la autenticación de Adobe Primetime devuelve todos los MVPD integrados con el programador seleccionado (ID del solicitante). Sin embargo, el Programador puede aplicar un filtro a la matriz de MVPD que se devuelve y mostrar solamente aquellos que están en ambas listas.

## Ejemplo {#example}

En este ejemplo se muestra cómo mostrar solo CableCompany_1 y CableCompany_2 dentro del cuadro de diálogo de selección de MVPD y no mostrar CableCompany_NewIntegration.

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if ( isAllowListed(currentMvpd.ID) ) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isAllowListed(mvpdID) {
    // Implement allowlisting on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
}
```

<!--
**Related Information**
* [Prevent MVPDs from appearing in the Selection Dialog](/help/authentication/prevent-mvpd-selectn-dialog.md)
* **Code Samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->