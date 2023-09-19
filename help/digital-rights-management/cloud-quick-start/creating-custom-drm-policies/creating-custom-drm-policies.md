---
title: Creación de políticas de DRM personalizadas (opcional)
description: Creación de políticas de DRM personalizadas (opcional)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Creación de políticas de DRM personalizadas (opcional){#create-custom-drm-policies-optional}

El kit de protección DRM de Primetime Cloud incluye algunas directivas preconfiguradas que se pueden utilizar durante el empaquetado. Si se desean configuraciones de directivas adicionales, por ejemplo, un derecho de inclusión en una lista de permitidos por el SWF específico, se puede utilizar el Administrador de directivas DRM de Primetime incluido para generar directivas personalizadas.

>[!NOTE]
>
>Todas las políticas deben utilizar la autenticación ANÓNIMA (no la contraseña del nombre de usuario o personalizada), independientemente de si se utiliza o no el flujo de trabajo de autenticación/derecho personalizado.

Junto con el Administrador de directivas se incluye la variable [!DNL flashaccesstools.properties] archivo de configuración, que se ha modificado para exponer únicamente las opciones de directiva configurables que admite el servicio DRM de Primetime Cloud. La configuración de opciones de directiva no admitidas por el servicio DRM de Primetime Cloud dará como resultado errores de adquisición de licencia. Para obtener información sobre el uso del Gestor de políticas de DRM de Primetime, consulte: [Implementaciones de referencia de DRM de Primetime: Administrador de directivas](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

Para crear una nueva directiva, actualice el [!DNL flashaccesstools.properties] como desee y, a continuación, utilice el comando:

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Crear directivas de forma dinámica para Autorización/Autorización personalizada{#create-policies-dynamically-for-custom-auth-entitlement}

Si utiliza la autenticación/derecho personalizado de DRM de Primetime Cloud y desea crear dinámicamente una nueva política de DRM para cada solicitud de licencia (en lugar de extraer políticas de un grupo generado previamente), Adobe recomienda utilizar directamente el SDK de Java de DRM de Primetime. El uso directo del SDK de Java es más rápido que el [!DNL AdobePolicyManager.jar] , que envía automáticamente el archivo de directiva al disco, incurriendo en una sobrecarga de E/S del disco.

Puede encontrar código de muestra con el SDK de Java en la [!DNL /Primetime DRM PolicyManager/sampleCode/] directorio, con nombre [!DNL CreatePolicy.java] y [!DNL CreatePolicyWithOutputProtection.java]. Puede encontrar documentación y JavaScript para el SDK de Java en [Información general sobre el SDK de DRM de Adobe Primetime](../../../digital-rights-management/drm-sdk-overview/overview.md)

Para generar y ejecutar los ejemplos, copie los archivos .java en la carpeta ../libs/ y ejecute:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
