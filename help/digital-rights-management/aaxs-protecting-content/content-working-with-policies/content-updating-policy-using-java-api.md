---
title: Actualización de una directiva mediante la API de Java
description: Actualización de una directiva mediante la API de Java
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Actualización de una directiva mediante la API de Java {#updating-a-policy-using-the-java-api}

Para actualizar una directiva mediante la API de Java, realice los siguientes pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en [Configuración del entorno de desarrollo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) dentro del proyecto.
1. Crear un `Policy` y leer en la directiva desde un archivo o base de datos.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Actualice el `Policy` estableciendo sus propiedades, como el nombre y las reglas de uso.

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

1. Serialice el actualizado `Policy` y almacenarlo en un archivo o base de datos.

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

Para ver el origen completo de este código de ejemplo, consulte `com.adobe.flashaccess.samples.policy.UpdatePolicy` en el directorio &quot;samples&quot; de Herramientas de línea de comandos de implementación de referencia.
