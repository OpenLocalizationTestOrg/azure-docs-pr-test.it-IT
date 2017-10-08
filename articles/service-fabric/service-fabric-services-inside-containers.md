---
title: aaaHow toocontainerize il microservizi Azure Service Fabric (anteprima)
description: "Azure Service Fabric ha aggiunto nuove funzionalità toocontainerize microservizi l'infrastruttura del servizio. Questa funzionalità è attualmente in anteprima."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a>Come toocontainerize affidabile di infrastruttura del servizio dei servizi e Reliable Actors (anteprima)

Service Fabric supporta la distribuzione in un contenitore di microservizi di Service Fabric (servizi di base di Reliable Services e Reliable Actors). Per altre informazioni, vedere [Service Fabric e contenitori](service-fabric-containers-overview.md).


 Questa funzionalità è disponibile in anteprima e questo articolo fornisce hello vari passaggi tooget il servizio in esecuzione all'interno di un contenitore.  

> [!NOTE]
> Questa funzionalità è in versione di anteprima e non è supportata in produzione. Attualmente questa funzionalità funziona solo per Windows.

## <a name="steps-toocontainerize-your-service-fabric-application"></a>I passaggi toocontainerize l'applicazione di Service Fabric

1. Aprire l'applicazione di Service Fabric in Visual Studio.

2. Aggiungi classe [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour progetto. codice Hello in questa classe è un helper toocorrectly carico hello Service Fabric file binari di runtime all'interno dell'applicazione quando viene eseguito in un contenitore.

3. Per ogni pacchetto di codice sarebbe toocontainerize, inizializzare hello caricatore al punto di ingresso del programma hello. Aggiungere costruttore statico di hello mostrato nel seguente file del punto di codice frammento tooyour programma voce hello.

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. Compilare e inserire in un [pacchetto](service-fabric-package-apps.md#Package-App) il progetto. toobuild e creare un pacchetto, fare clic sul progetto dell'applicazione hello in Esplora soluzioni e scegliere hello **pacchetto** comando.

5. Per ogni pacchetto di codice è necessario toocontainerize, hello esecuzione script di PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1). utilizzo di Hello è come segue:
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  script Hello crea una cartella con gli elementi di Docker in $dockerPackageOutputDirectoryPath. Modificare tooexpose Dockerfile hello generato le porte, eseguire gli script di installazione e così via in base alle proprie esigenze.

6. È quindi necessario troppo[compilare](service-fabric-get-started-containers.md#Build-Containers) e [push](service-fabric-get-started-containers.md#Push-Containers) il repository di tooyour pacchetto contenitore Docker.

7. L'immagine contenitore, informazioni dell'archivio, l'autenticazione del Registro di sistema e mapping di porta a host, modificare hello ApplicationManifest.xml e tooadd ServiceManifest.xml. Per la modifica di manifesti hello, vedere [creare un'applicazione contenitore di Azure Service Fabric](service-fabric-get-started-containers.md). definizione del pacchetto di codice Hello in hello servizio esigenze manifesto toobe sostituito con l'immagine contenitore corrispondente. Verificare che toochange hello EntryPoint tooa ContainerHost tipo.

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. Aggiungere mapping di porta per ospitare hello per la replica e un endpoint di servizio. Poiché entrambe queste porte vengono assegnate in fase di esecuzione dall'infrastruttura di servizio, hello ContainerPort è impostato toozero toouse hello assegnata una porta per il mapping.

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. tootest questa applicazione, è necessario toodeploy è tooa cluster che esegue versione 5.7 o versioni successive. È inoltre necessario tooedit e aggiornare hello cluster impostazioni tooenable questa funzionalità di anteprima. Seguire i passaggi di hello in questo [articolo](service-fabric-cluster-fabric-settings.md) impostazione hello tooadd illustrato nella figura seguente.
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. Avanti [distribuire](service-fabric-deploy-remove-applications.md) hello modificato cluster toothis pacchetto di applicazione.

Ora si dovrebbe avere un'applicazione di Service Fabric distribuita nei contenitori che esegue il cluster.

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sull'esecuzione di [contenitori in Service Fabric](service-fabric-get-started-containers.md).
* Informazioni su Service Fabric hello [del ciclo di vita dell'applicazione](service-fabric-application-lifecycle.md).
