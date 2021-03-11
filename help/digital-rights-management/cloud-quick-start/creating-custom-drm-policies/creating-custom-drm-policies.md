---
title: Crear directivas de DRM personalizadas (opcional)
description: Crear directivas de DRM personalizadas (opcional)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Crear directivas de DRM personalizadas (opcional){#create-custom-drm-policies-optional}

El kit de protección de DRM de Primetime Cloud incluye algunas políticas preconfiguradas que se pueden utilizar durante el empaquetado. Si desea realizar configuraciones de directiva adicionales, por ejemplo, un derecho de lista de permitidos SWF específico, el administrador de políticas de DRM de Primetime incluido se puede usar para generar políticas personalizadas.

>[!NOTE]
>
>Todas las directivas deben utilizar autenticación ANONYMOUS (no contraseña de nombre de usuario ni personalizada), independientemente de si se utiliza o no el flujo de trabajo de autenticación/derechos personalizados .

Con el Administrador de directivas se incluye el archivo de configuración [!DNL flashaccesstools.properties], que se ha modificado para exponer únicamente las opciones de directiva configurables que admite el servicio de DRM de Primetime Cloud. Si se establecen opciones de directiva que no sean compatibles con el servicio Primetime Cloud DRM, se generarán errores de adquisición de licencias. Para obtener información sobre el uso del Administrador de políticas de DRM de Primetime, consulte: [Implementaciones de referencia de DRM de Primetime: Administrador de directivas](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

Para crear una política nueva, actualice el archivo [!DNL flashaccesstools.properties] como desee y, a continuación, utilice el comando :

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Crear directivas de forma dinámica para Auth/Entitlement{#create-policies-dynamically-for-custom-auth-entitlement} personalizado

Si utiliza la autenticación/derechos personalizados de DRM de Primetime Cloud y desea crear dinámicamente una nueva directiva de DRM para cada solicitud de licencia (en lugar de extraer directivas de un grupo pregenerado), Adobe recomienda que utilice directamente el SDK de Java de DRM de Primetime. El uso directo del SDK de Java es más rápido que la herramienta [!DNL AdobePolicyManager.jar], que envía automáticamente el archivo de directiva al disco, lo que incurre en sobrecarga de E/S de disco.

El código de muestra que utiliza el SDK de Java se encuentra en el directorio [!DNL /Primetime DRM PolicyManager/sampleCode/], denominado [!DNL CreatePolicy.java] y [!DNL CreatePolicyWithOutputProtection.java]. Puede encontrar Javadocs y la documentación del SDK de Java en [Información general del SDK de Adobe Primetime DRM](../../../digital-rights-management/drm-sdk-overview/overview.md)

Para crear y ejecutar los ejemplos, copie los archivos .java en la carpeta ../libs/ y ejecute:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
