---
seo-title: Crear directivas de DRM personalizadas (opcional)
title: Crear directivas de DRM personalizadas (opcional)
uuid: 701b51d9-6dde-4c21-bc5b-09e612582968
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Crear directivas de DRM personalizadas (opcional){#create-custom-drm-policies-optional}

El kit de protección DRM de Primetime Cloud incluye algunas directivas preconfiguradas que se pueden usar durante el empaquetado. Si se desean configuraciones de directiva adicionales, por ejemplo, un derecho de listado permitido por SWF específico, se puede utilizar el Administrador de directivas de DRM de Primetime incluido para generar políticas personalizadas.

>[!NOTE]
>
>Todas las directivas deben utilizar autenticación ANONYMOUS (no contraseña de nombre de usuario ni personalizada), independientemente de si se utiliza o no el flujo de trabajo de autorización/asignación de derechos personalizado.

El Administrador de políticas incluye el archivo de configuración [!DNL flashaccesstools.properties], que se ha modificado para exponer únicamente las opciones de directiva configurables que admite el servicio DRM de Primetime Cloud. La configuración de las opciones de directiva que no sean compatibles con el servicio DRM de Primetime Cloud producirá errores de adquisición de licencias. Para obtener información sobre el uso del Administrador de directivas de DRM de Primetime, consulte: [Implementaciones de referencia de DRM de Primetime: Administrador de directivas](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

Para crear una nueva directiva, actualice el archivo [!DNL flashaccesstools.properties] como desee y, a continuación, utilice el comando:

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Crear directivas de forma dinámica para la autenticación/asignación de derechos personalizada{#create-policies-dynamically-for-custom-auth-entitlement}

Si utiliza la autenticación/asignación de derechos personalizada de DRM de Primetime Cloud y desea crear dinámicamente una nueva directiva de DRM para cada solicitud de licencia (en lugar de extraer directivas de un grupo pregenerado), Adobe recomienda que utilice directamente el SDK de Java de DRM de Primetime. El uso directo del SDK de Java es más rápido que la herramienta [!DNL AdobePolicyManager.jar], que envía automáticamente el archivo de política al disco, lo que ocasiona sobrecarga de E/S de disco.

El código de muestra que utiliza el SDK de Java se encuentra en el directorio [!DNL /Primetime DRM PolicyManager/sampleCode/], denominado [!DNL CreatePolicy.java] y [!DNL CreatePolicyWithOutputProtection.java]. Los javadocs y la documentación del SDK de Java se encuentran en [Información general del SDK de Adobe Primetime DRM](../../../digital-rights-management/drm-sdk-overview/overview.md)

Para generar y ejecutar los ejemplos, copie los archivos .java en la carpeta ../libs/ y ejecute:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
