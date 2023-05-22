---
title: Solución de problemas
description: Solución de problemas
copied-description: true
exl-id: 618b1e19-d25d-435d-b118-b43455bde974
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# Solución de problemas{#troubleshooting}

* En el caso de algunos dispositivos más antiguos que ejecutan el nivel de API 10 o anterior, logcat no puede abrir el dispositivo de registro debido a un problema de permisos. Aparece la siguiente excepción: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Solución alternativa:**

   1. Abrir [!DNL AndroidManifest.xml] en el [!DNL CatalogActivity] proyecto en el espacio de trabajo.

   1. Añada el siguiente permiso a [!DNL `AndroidManfest.xml`] archivo:

      ```
      android.permission.READ_LOGS
      ```
