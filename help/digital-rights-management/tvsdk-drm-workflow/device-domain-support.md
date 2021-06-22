---
description: Normalmente, todas las licencias de DRM de Primetime, en el momento de la creación, están vinculadas a un dispositivo único. Este enlace impide que los usuarios compartan licencias entre distintos dispositivos sin autorización. Además del enlace por dispositivo, Primetime DRM proporciona la capacidad de enlazar licencias a un dominio de dispositivo o a un grupo de dispositivos.
title: Reproducción de contenido cifrado mediante compatibilidad con dominios
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Compatibilidad con el dominio del dispositivo {#device-domain-support}

Normalmente, todas las licencias de DRM de Primetime, en el momento de la creación, están vinculadas a un dispositivo único. Este enlace impide que los usuarios compartan licencias entre distintos dispositivos sin autorización. Además del enlace por dispositivo, Primetime DRM proporciona la capacidad de enlazar licencias a un dominio de dispositivo o a un grupo de dispositivos.

Si los metadatos de contenido especifican que el registro del dominio del dispositivo es obligatorio, la aplicación puede invocar una API para unirse a un grupo de dispositivos. Esta acción déclencheur que se envíe una solicitud de registro de dominio al servidor de dominio. Una vez que se emite una licencia para un grupo de dispositivos, la licencia se puede exportar y compartir con otros dispositivos que se hayan unido al grupo de dispositivos.

A continuación, la información del grupo de dispositivos se utiliza en el objeto `DRMContentData` `VoucherAccessInfo` , que se utilizará para presentar la información necesaria para recuperar y consumir correctamente una licencia.

## Reproducir el contenido cifrado mediante la compatibilidad con el dominio {#play-encrypted-content-using-domain-support}

Para reproducir contenido cifrado mediante Primetime DRM , realice los siguientes pasos:

1. Con `VoucherAccessInfo.deviceGroup`, compruebe si se requiere el registro de grupo de dispositivos.
1. Si se requiere autenticación:
   1. Utilice la propiedad `DeviceGroupInfo.authenticationMethod` para averiguar si se requiere autenticación.
   1. Si se requiere autenticación, autentique al usuario realizando UNO de los siguientes pasos:

      * Obtenga el nombre de usuario y la contraseña del usuario e invoque `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * Obtenga un token de autenticación en caché/pregenerado e invoque `DRMManager.setAuthenticationToken()`.
   1. Invocar `DRMManager.addToDeviceGroup()`
1. Obtenga la licencia para el contenido realizando una de las siguientes tareas:
   1. Utilice el método `DRMManager.loadVoucher()`.
   1. Obtenga la licencia de un dispositivo diferente registrado en el mismo grupo de dispositivos y proporcione la licencia a `DRMManager` mediante el método `DRMManager.storeVoucher()`.
1. Reproducir el contenido cifrado con el método `Primetime.play()`.
Para exportar la licencia del contenido, cualquiera de los dispositivos puede proporcionar los bytes sin procesar de la licencia mediante el método `DRMVoucher.toByteArray()` después de obtener la licencia del servidor de licencias DRM de Primetime. Los proveedores de contenido suelen limitar el número de dispositivos de un grupo de dispositivos. Si se alcanza el límite, es posible que tenga que llamar al método `DRMManager.removeFromDeviceGroup()` en un dispositivo no utilizado antes de registrar el dispositivo actual.
