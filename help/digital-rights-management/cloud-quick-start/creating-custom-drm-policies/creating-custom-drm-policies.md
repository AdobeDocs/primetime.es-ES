---
seo-title: Crear directivas de DRM personalizadas (opcional)
title: Crear directivas de DRM personalizadas (opcional)
uuid: 701b51d9-6dde-4c21-bc5b-09e612582968
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Crear directivas de DRM personalizadas (opcional){#create-custom-drm-policies-optional}

El kit de protección DRM de Primetime Cloud incluye algunas directivas preconfiguradas que se pueden usar durante el empaquetado. Si se desea una configuración de directiva adicional, por ejemplo, un derecho SWF de lista blanca específico, se puede usar el Administrador de directivas de DRM de Primetime incluido para generar políticas personalizadas.

>[!NOTE]
>
>Todas las directivas deben utilizar autenticación ANONYMOUS (no contraseña de nombre de usuario ni personalizada), independientemente de si se utiliza o no el flujo de trabajo de autorización/asignación de derechos personalizado.

El Administrador de directivas incluye el archivo de configuración, que se ha modificado para exponer únicamente las opciones de directiva configurables que admite el servicio DRM de Primetime Cloud. [!DNL flashaccesstools.properties] La configuración de las opciones de directiva que no sean compatibles con el servicio DRM de Primetime Cloud producirá errores de adquisición de licencias. Para obtener información sobre el uso del Administrador de directivas de DRM de Primetime, consulte: Implementaciones [de referencia de DRM de Primetime: Administrador](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager)de directivas.

Para crear una nueva directiva, actualice el [!DNL flashaccesstools.properties] archivo como desee y, a continuación, utilice el comando:

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Crear directivas de forma dinámica para la autenticación/asignación de derechos personalizada{#create-policies-dynamically-for-custom-auth-entitlement}

Si utiliza la autenticación/asignación de derechos personalizada de DRM de Primetime Cloud y desea crear dinámicamente una nueva directiva de DRM para cada solicitud de licencia (en lugar de extraer directivas de un grupo pregenerado), Adobe recomienda que utilice el SDK de Java de Primetime DRM directamente. El uso directo del SDK de Java es más rápido que la [!DNL AdobePolicyManager.jar] herramienta, que envía automáticamente el archivo de política al disco, lo que ocasiona sobrecarga de E/S de disco.

El código de muestra que utiliza el SDK de Java se encuentra en el [!DNL /Primetime DRM PolicyManager/sampleCode/] directorio, denominado [!DNL CreatePolicy.java] y [!DNL CreatePolicyWithOutputProtection.java]. Encontrará Javadocs y documentación para el SDK de Java en [Información general sobre el SDK de DRM de Adobe Primetime](../../../digital-rights-management/drm-sdk-overview/overview.md)

Para generar y ejecutar los ejemplos, copie los archivos .java en la carpeta ../libs/ y ejecute:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
