---
title: Actualización de una directiva mediante la API de Java
description: Actualización de una directiva mediante la API de Java
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Actualización de una directiva mediante la API de Java {#updating-a-policy-using-the-java-api}

Para actualizar una directiva mediante la API de Java, realice los pasos siguientes:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en [Configuración del entorno de desarrollo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) dentro del proyecto.
1. Cree una instancia `Policy` y lea la política desde un archivo o base de datos.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Actualice el objeto `Policy` estableciendo sus propiedades, como su nombre y reglas de uso.

   ```java
     // Change the policy name.  
     policy.setName("UpdatedDemoPolicy");  
   
     // Add DRM module restrictions to the play right  
     for (Right r: policy.getRights()) {  
      if (r instanceof PlayRight) {  
       PlayRight pr = (PlayRight) r;  
       // Disallow Linux versions up to and including 1.9.  Allow  
       // all other OSes and Linux versions above 1.9  
       VersionInfo toExclude = new VersionInfo();  
       toExclude.setOS("Linux");  
       toExclude.setReleaseVersion("1.9");  
       Collection<VersionInfo> exclusions = new ArrayList<VersionInfo>();  
       exclusions.add(toExclude);  
       ModuleRequirements drmRestrictions = new ModuleRequirements();  
       drmRestrictions.setExcludedVersions(exclusions);  
       pr.setDRMModuleRequirements(drmRestrictions);  
       break;  
      }  
     }
   ```

1. Serialice el objeto `Policy` actualizado y guárdelo en un archivo o base de datos.

   ```java
      // Serialize the policy.  
      byte[] policyBytes = policy.getBytes();  
      System.out.println("New policy revision number: "  
       +  policy.getRevision());      
      // Write the policy to a file.   
      // Alternatively, the policy may be stored in a database.  
      FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
      out.write(policyBytes);  
      out.close(); 
   ```

Para obtener la fuente completa de este código de ejemplo, consulte `com.adobe.flashaccess.samples.policy.UpdatePolicy` en el directorio Ejemplos de las herramientas de la línea de comandos de implementación de referencia.
