---
description: Si desea configurar Primetime DRM, copie los archivos del DVD. Estos archivos incluyen archivos JAR que incluyen código, certificados y clases de terceros. Además, debe solicitar un certificado de Adobe Systems Incorporated. A continuación, Adobe emite varias credenciales que se utilizan para proteger la integridad del contenido empaquetado, las licencias y la comunicación entre el cliente y el servidor.
title: Configurar el entorno de desarrollo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Configurar el entorno de desarrollo {#set-up-your-development-environment}

Si desea configurar Primetime DRM, copie los archivos del DVD. Estos archivos incluyen archivos JAR que incluyen código, certificados y clases de terceros. Además, debe solicitar un certificado de Adobe Systems Incorporated. A continuación, Adobe emite varias credenciales que se utilizan para proteger la integridad del contenido empaquetado, las licencias y la comunicación entre el cliente y el servidor.

Adobe proporciona el SDK de DRM de Primetime en DVD:

1. Copie los siguientes archivos de [!DNL [DVD DRM]/SDK/] a su sistema de desarrollo (en su ruta de clase Java):

   * [!DNL adobe-flashaccess-certs.jar] - Incluye certificados raíz de Adobe
   * [!DNL adobe-flashaccess-sdk.jar] : incluye clases de SDK principal de DRM de Primetime
   * [!DNL adobe-flashaccess-sdk-pro.jar] - Incluye clases de SDK de Primetime DRM Professional, necesarias solo para las funciones profesionales

1. Copie los siguientes archivos de [!DNL [DVD DRM]/SDK/thirdParty] a su sistema de desarrollo:

   * [!DNL bcmail-jdk15-141.jar]
   * [!DNL bcprov-jdk15-141.jar]
   * [!DNL commons-discovery-0.4.jar]
   * [!DNL commons-logging-1.1.1.jar]
   * [!DNL cryptoj.jar]
   * [!DNL jaxb-api.jar]
   * [!DNL jaxb-impl.jar]
   * [!DNL jaxb-libs.jar]
   * [!DNL relaxngDatatype.jar]
   * [!DNL rm-pdrl.jar]
   * [!DNL xsdlib.jar]
   * [!DNL jackson-annotations-2.4.0-rc4-20140522.175222-3.jar]
   * [!DNL jackson-core--2.4.0-rc4-20140529.184520-13.jar]
   * [!DNL jackson-databind-2.4.0-rc4-20140603.005043-38.jar]

1. (Opcional) Para mejorar el rendimiento, puede habilitar la compatibilidad nativa con las operaciones criptográficas copiando la biblioteca específica de la plataforma adecuada de [!DNL [DVD DRM]/SDK/thirdParty/cryptoj/] a su sistema de desarrollo (recuerde colocar la ubicación en la ruta):

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

     >[!NOTE]
     >
     >Hay disponibles versiones de 32 y 64 bits de estas bibliotecas. Solo debe utilizar la versión de 64 bits si tiene un sistema operativo de 64 bits y ejecuta la versión de 64 bits de Java.

1. (Opcional) Para obtener funcionalidad relacionada con la compatibilidad con Adobe Flash Media Rights Management Server (FMRMS) 1.x, copie `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` a su sistema de desarrollo:

   Implemente esto solo si anteriormente implementó FMRMS 1.x y no desea volver a empaquetar el contenido protegido por FMRMS. En este caso, debe añadir esta compatibilidad al servidor de licencias para que pueda administrar el contenido y los clientes antiguos.
