---
title: Lista de actualización de directivas
description: Lista de actualización de directivas
copied-description: true
exl-id: 78078e95-775e-4c64-ab0f-d8bf644f3aee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Lista de actualización de directivas {#policy-update-list}

Puede utilizar Listas de actualización de directivas para comunicar los cambios de directivas a un servidor de licencias. Si se modifica una directiva una vez que se utiliza para empaquetar contenido, es deseable que el servidor de licencias tenga en cuenta la versión más reciente de la directiva, de modo que esa versión se pueda utilizar para emitir una licencia.

Para crear una Lista de actualización de directivas por primera vez, haga clic en **[!UICONTROL Add policies]** para ver todas las directivas disponibles en el servidor. Para cualquier política que se haya actualizado desde que se utilizó para empaquetar contenido, seleccione la **[!UICONTROL update]** botón de opción.

Si ya no desea utilizar una directiva para emitir licencias y la directiva ya se utilizó para empaquetar contenido, es posible que desee revocar la directiva. Para ello, seleccione la opción **[!UICONTROL revoke]** botón de opción. Una vez seleccionadas las políticas deseadas, elija **[!UICONTROL Create Policy Update List]**. Un archivo llamado [!DNL PolicyUpdateList.dat] se guardarán en el [!DNL Resources] Directorio.

Para modificar una Lista de actualización de directivas existente, haga clic en **[!UICONTROL Add policies]** para ver todas las directivas disponibles en el servidor. Elija las políticas adicionales que desee añadir o revocar. Las entradas existentes en la Lista de actualización de directivas se pueden cambiar en la sección superior de la pantalla. Políticas que están marcadas **[!UICONTROL updated]** se puede cambiar a **[!UICONTROL revoked]**, pero una vez que se define una directiva **[!UICONTROL revoked]**, no se puede volver a cambiar a **[!UICONTROL updated]**.

Cuando se hayan realizado los cambios deseados, elija **[!UICONTROL Create Policy Update List]**, y el [!DNL PolicyUpdateList.dat] se regenera el archivo. Si una directiva ya está en la lista de actualización de directivas y se actualizó desde la última vez que se generó la lista, se utilizará la versión más reciente cuando se vuelva a generar la lista de actualización de directivas.
