---
description: Normalmente, todas las licencias de DRM de Primetime, en tiempo de creación, están enlazadas a un dispositivo único. Este enlace impide que los usuarios compartan licencias en distintos dispositivos sin autorización. Además del enlace por dispositivo, Primetime DRM permite enlazar licencias a un dominio de dispositivo o a un grupo de dispositivos.
seo-description: Normalmente, todas las licencias de DRM de Primetime, en tiempo de creación, están enlazadas a un dispositivo único. Este enlace impide que los usuarios compartan licencias en distintos dispositivos sin autorización. Además del enlace por dispositivo, Primetime DRM permite enlazar licencias a un dominio de dispositivo o a un grupo de dispositivos.
seo-title: Reproducción de contenido cifrado mediante compatibilidad con dominios
title: Reproducción de contenido cifrado mediante compatibilidad con dominios
uuid: 8854cc0f-9bfc-4833-82d7-a3f46ac88e06
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---


# Compatibilidad con dominios de dispositivo {#device-domain-support}

Normalmente, todas las licencias de DRM de Primetime, en tiempo de creación, están enlazadas a un dispositivo único. Este enlace impide que los usuarios compartan licencias en distintos dispositivos sin autorización. Además del enlace por dispositivo, Primetime DRM permite enlazar licencias a un dominio de dispositivo o a un grupo de dispositivos.

Si los metadatos de contenido especifican que se requiere el registro del dominio del dispositivo, la aplicación puede invocar una API para unirse a un grupo de dispositivos. Esta acción activa una solicitud de registro de dominio para enviarla al servidor de dominio. Una vez emitida una licencia a un grupo de dispositivos, la licencia se puede exportar y compartir con otros dispositivos que se hayan unido al grupo de dispositivos.

La información del grupo de dispositivos se utiliza en el objeto `DRMContentData` `VoucherAccessInfo`, que luego se utilizará para presentar la información necesaria para recuperar y consumir correctamente una licencia.

## Reproducir contenido cifrado mediante compatibilidad con dominios {#play-encrypted-content-using-domain-support}

Para reproducir contenido cifrado con Primetime DRM, realice los siguientes pasos:

1. Utilizando `VoucherAccessInfo.deviceGroup`, compruebe si se requiere el registro del grupo de dispositivos.
1. Si se requiere autenticación:
   1. Utilice la propiedad `DeviceGroupInfo.authenticationMethod` para averiguar si se requiere autenticación.
   1. Si se requiere autenticación, autentique al usuario realizando UNO de los siguientes pasos:

      * Obtenga el nombre de usuario y la contraseña del usuario e invoque `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * Obtenga un token de autenticación en caché/pregenerado e invoque `DRMManager.setAuthenticationToken()`.
   1. Invocar `DRMManager.addToDeviceGroup()`
1. Obtenga la licencia para el contenido realizando una de las siguientes tareas:
   1. Utilice el método `DRMManager.loadVoucher()`.
   1. Obtenga la licencia de un dispositivo diferente registrado en el mismo grupo de dispositivos y proporcione la licencia al ` DRMManager` mediante el método `DRMManager.storeVoucher()`.
1. Reproducir el contenido cifrado mediante el método `Primetime.play()`.
Para exportar la licencia del contenido, cualquiera de los dispositivos puede proporcionar los bytes sin procesar de la licencia mediante el método `DRMVoucher.toByteArray()` después de obtener la licencia del servidor de licencias DRM de Primetime. Los proveedores de contenido suelen limitar el número de dispositivos de un grupo de dispositivos. Si se alcanza el límite, es posible que tenga que llamar al método `DRMManager.removeFromDeviceGroup()` en un dispositivo sin usar antes de registrar el dispositivo actual.