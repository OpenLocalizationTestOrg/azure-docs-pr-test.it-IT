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
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="52f08-104">Come toocontainerize affidabile di infrastruttura del servizio dei servizi e Reliable Actors (anteprima)</span><span class="sxs-lookup"><span data-stu-id="52f08-104">How toocontainerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="52f08-105">Service Fabric supporta la distribuzione in un contenitore di microservizi di Service Fabric (servizi di base di Reliable Services e Reliable Actors).</span><span class="sxs-lookup"><span data-stu-id="52f08-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="52f08-106">Per altre informazioni, vedere [Service Fabric e contenitori](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="52f08-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="52f08-107">Questa funzionalità è disponibile in anteprima e questo articolo fornisce hello vari passaggi tooget il servizio in esecuzione all'interno di un contenitore.</span><span class="sxs-lookup"><span data-stu-id="52f08-107">This feature is in preview and this article provides hello various steps tooget your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="52f08-108">Questa funzionalità è in versione di anteprima e non è supportata in produzione.</span><span class="sxs-lookup"><span data-stu-id="52f08-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="52f08-109">Attualmente questa funzionalità funziona solo per Windows.</span><span class="sxs-lookup"><span data-stu-id="52f08-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-toocontainerize-your-service-fabric-application"></a><span data-ttu-id="52f08-110">I passaggi toocontainerize l'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="52f08-110">Steps toocontainerize your Service Fabric Application</span></span>

1. <span data-ttu-id="52f08-111">Aprire l'applicazione di Service Fabric in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52f08-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="52f08-112">Aggiungi classe [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="52f08-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project.</span></span> <span data-ttu-id="52f08-113">codice Hello in questa classe è un helper toocorrectly carico hello Service Fabric file binari di runtime all'interno dell'applicazione quando viene eseguito in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="52f08-113">hello code in this class is a helper toocorrectly load hello Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="52f08-114">Per ogni pacchetto di codice sarebbe toocontainerize, inizializzare hello caricatore al punto di ingresso del programma hello.</span><span class="sxs-lookup"><span data-stu-id="52f08-114">For each code package you would like toocontainerize, initialize hello loader at hello program entry point.</span></span> <span data-ttu-id="52f08-115">Aggiungere costruttore statico di hello mostrato nel seguente file del punto di codice frammento tooyour programma voce hello.</span><span class="sxs-lookup"><span data-stu-id="52f08-115">Add hello static constructor shown in hello following code snippet tooyour program entry point file.</span></span>

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

4. <span data-ttu-id="52f08-116">Compilare e inserire in un [pacchetto](service-fabric-package-apps.md#Package-App) il progetto.</span><span class="sxs-lookup"><span data-stu-id="52f08-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="52f08-117">toobuild e creare un pacchetto, fare clic sul progetto dell'applicazione hello in Esplora soluzioni e scegliere hello **pacchetto** comando.</span><span class="sxs-lookup"><span data-stu-id="52f08-117">toobuild and create a package, right-click hello application project in Solution Explorer and choose hello **Package** command.</span></span>

5. <span data-ttu-id="52f08-118">Per ogni pacchetto di codice è necessario toocontainerize, hello esecuzione script di PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="52f08-118">For every code package you need toocontainerize, run hello PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="52f08-119">utilizzo di Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="52f08-119">hello usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="52f08-120">script Hello crea una cartella con gli elementi di Docker in $dockerPackageOutputDirectoryPath.</span><span class="sxs-lookup"><span data-stu-id="52f08-120">hello script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="52f08-121">Modificare tooexpose Dockerfile hello generato le porte, eseguire gli script di installazione e così via in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="52f08-121">Modify hello generated Dockerfile tooexpose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="52f08-122">È quindi necessario troppo[compilare](service-fabric-get-started-containers.md#Build-Containers) e [push](service-fabric-get-started-containers.md#Push-Containers) il repository di tooyour pacchetto contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="52f08-122">Next you need too[build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package tooyour repository.</span></span>

7. <span data-ttu-id="52f08-123">L'immagine contenitore, informazioni dell'archivio, l'autenticazione del Registro di sistema e mapping di porta a host, modificare hello ApplicationManifest.xml e tooadd ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="52f08-123">Modify hello ApplicationManifest.xml and ServiceManifest.xml tooadd your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="52f08-124">Per la modifica di manifesti hello, vedere [creare un'applicazione contenitore di Azure Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="52f08-124">For modifying hello manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="52f08-125">definizione del pacchetto di codice Hello in hello servizio esigenze manifesto toobe sostituito con l'immagine contenitore corrispondente.</span><span class="sxs-lookup"><span data-stu-id="52f08-125">hello code package definition in hello service manifest needs toobe replaced with corresponding container image.</span></span> <span data-ttu-id="52f08-126">Verificare che toochange hello EntryPoint tooa ContainerHost tipo.</span><span class="sxs-lookup"><span data-stu-id="52f08-126">Make sure toochange hello EntryPoint tooa ContainerHost type.</span></span>

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

8. <span data-ttu-id="52f08-127">Aggiungere mapping di porta per ospitare hello per la replica e un endpoint di servizio.</span><span class="sxs-lookup"><span data-stu-id="52f08-127">Add hello port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="52f08-128">Poiché entrambe queste porte vengono assegnate in fase di esecuzione dall'infrastruttura di servizio, hello ContainerPort è impostato toozero toouse hello assegnata una porta per il mapping.</span><span class="sxs-lookup"><span data-stu-id="52f08-128">Since both these ports are assigned at runtime by Service Fabric, hello ContainerPort is set toozero toouse hello assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="52f08-129">tootest questa applicazione, è necessario toodeploy è tooa cluster che esegue versione 5.7 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="52f08-129">tootest this application, you need toodeploy it tooa cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="52f08-130">È inoltre necessario tooedit e aggiornare hello cluster impostazioni tooenable questa funzionalità di anteprima.</span><span class="sxs-lookup"><span data-stu-id="52f08-130">In addition, you need tooedit and update hello cluster settings tooenable this preview feature.</span></span> <span data-ttu-id="52f08-131">Seguire i passaggi di hello in questo [articolo](service-fabric-cluster-fabric-settings.md) impostazione hello tooadd illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="52f08-131">Follow hello steps in this [article](service-fabric-cluster-fabric-settings.md) tooadd hello setting shown next.</span></span>
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
10. <span data-ttu-id="52f08-132">Avanti [distribuire](service-fabric-deploy-remove-applications.md) hello modificato cluster toothis pacchetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="52f08-132">Next [deploy](service-fabric-deploy-remove-applications.md) hello edited application package toothis cluster.</span></span>

<span data-ttu-id="52f08-133">Ora si dovrebbe avere un'applicazione di Service Fabric distribuita nei contenitori che esegue il cluster.</span><span class="sxs-lookup"><span data-stu-id="52f08-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52f08-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52f08-134">Next steps</span></span>
* <span data-ttu-id="52f08-135">Altre informazioni sull'esecuzione di [contenitori in Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="52f08-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="52f08-136">Informazioni su Service Fabric hello [del ciclo di vita dell'applicazione](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="52f08-136">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
