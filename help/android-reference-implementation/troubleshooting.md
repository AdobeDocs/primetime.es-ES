---
seo-title: Resolución de problemas
title: Resolución de problemas
uuid: b7a41ea7-86c5-442c-b751-86a9055c5e35
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---


# Resolución de problemas{#troubleshooting}

* Para algunos dispositivos antiguos que ejecutan API de nivel 10 o superior, logcat no puede abrir el dispositivo de registro debido a un problema de permisos. Aparece la siguiente excepción: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Solución:**

   1. Abra [!DNL AndroidManifest.xml] en el proyecto [!DNL CatalogActivity] del área de trabajo.

   1. Añada el siguiente permiso al archivo [!DNL `AndroidManfest.xml`]:

      ```
      android.permission.READ_LOGS
      ```
