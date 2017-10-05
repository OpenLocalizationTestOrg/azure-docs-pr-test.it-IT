---
title: Come distribuire in un contenitore i microservizi di Azure Service Fabric (anteprima)
description: "Azure Service Fabric ha aggiunto nuove funzionalità per distribuire in un contenitore i microservizi di Service Fabric. Questa funzionalità è attualmente in anteprima."
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
ms.openlocfilehash: 6f8ad0bad8d1ae861e6b72f7e1a32ab0675813c2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-containerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="72d5d-104">Come distribuire in un contenitore Reliable Services e Reliable Actors di Service Fabric (anteprima)</span><span class="sxs-lookup"><span data-stu-id="72d5d-104">How to containerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="72d5d-105">Service Fabric supporta la distribuzione in un contenitore di microservizi di Service Fabric (servizi di base di Reliable Services e Reliable Actors).</span><span class="sxs-lookup"><span data-stu-id="72d5d-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="72d5d-106">Per altre informazioni, vedere [Service Fabric e contenitori](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72d5d-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="72d5d-107">Questa funzionalità è in anteprima e questo articolo fornisce i diversi passaggi per eseguire il servizio all'interno di un contenitore.</span><span class="sxs-lookup"><span data-stu-id="72d5d-107">This feature is in preview and this article provides the various steps to get your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="72d5d-108">Questa funzionalità è in versione di anteprima e non è supportata in produzione.</span><span class="sxs-lookup"><span data-stu-id="72d5d-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="72d5d-109">Attualmente questa funzionalità funziona solo per Windows.</span><span class="sxs-lookup"><span data-stu-id="72d5d-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-to-containerize-your-service-fabric-application"></a><span data-ttu-id="72d5d-110">Procedura per distribuire in un contenitore l'applicazione Service Fabric</span><span class="sxs-lookup"><span data-stu-id="72d5d-110">Steps to containerize your Service Fabric Application</span></span>

1. <span data-ttu-id="72d5d-111">Aprire l'applicazione di Service Fabric in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="72d5d-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="72d5d-112">Aggiungere la classe [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) al progetto.</span><span class="sxs-lookup"><span data-stu-id="72d5d-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) to your project.</span></span> <span data-ttu-id="72d5d-113">Il codice in questa classe è un metodo di supporto per caricare correttamente i file binari di runtime di Service Fabric all'interno dell'applicazione quando è in esecuzione all'interno di un contenitore.</span><span class="sxs-lookup"><span data-stu-id="72d5d-113">The code in this class is a helper to correctly load the Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="72d5d-114">Per ogni pacchetto di codice che si desidera distribuire in un contenitore, inizializzare il caricatore nel punto di ingresso del programma.</span><span class="sxs-lookup"><span data-stu-id="72d5d-114">For each code package you would like to containerize, initialize the loader at the program entry point.</span></span> <span data-ttu-id="72d5d-115">Aggiungere il costruttore statico illustrato nel frammento di codice seguente al file del punto di ingresso del programma.</span><span class="sxs-lookup"><span data-stu-id="72d5d-115">Add the static constructor shown in the following code snippet to your program entry point file.</span></span>

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
          /// This is the entry point of the service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. <span data-ttu-id="72d5d-116">Compilare e inserire in un [pacchetto](service-fabric-package-apps.md#Package-App) il progetto.</span><span class="sxs-lookup"><span data-stu-id="72d5d-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="72d5d-117">Per costruire e creare un pacchetto, fare clic con il pulsante destro sul progetto dell'applicazione in Esplora soluzioni e scegliere il comando **Pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="72d5d-117">To build and create a package, right-click the application project in Solution Explorer and choose the **Package** command.</span></span>

5. <span data-ttu-id="72d5d-118">Per ogni pacchetto di codice che è necessario distribuire in un contenitore, eseguire lo script di PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="72d5d-118">For every code package you need to containerize, run the PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="72d5d-119">L'utilizzo è il seguente:</span><span class="sxs-lookup"><span data-stu-id="72d5d-119">The usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path to the code package to containerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for the generated docker folder.'
    $applicationExeName = 'Name of the ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="72d5d-120">Lo script crea una cartella con gli elementi di Docker in $dockerPackageOutputDirectoryPath.</span><span class="sxs-lookup"><span data-stu-id="72d5d-120">The script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="72d5d-121">Modificare il Dockerfile generato per esporre le porte, eseguire gli script di configurazione e così via in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="72d5d-121">Modify the generated Dockerfile to expose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="72d5d-122">È quindi necessario [compilare](service-fabric-get-started-containers.md#Build-Containers) ed [eseguire il push](service-fabric-get-started-containers.md#Push-Containers) del pacchetto del contenitore Docker nel repository.</span><span class="sxs-lookup"><span data-stu-id="72d5d-122">Next you need to [build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package to your repository.</span></span>

7. <span data-ttu-id="72d5d-123">Modificare ApplicationManifest.xml e ServiceManifest.xml per aggiungere l'immagine del contenitore, le informazioni sul repository, l'autenticazione del registro di sistema e il mapping tra porta e host.</span><span class="sxs-lookup"><span data-stu-id="72d5d-123">Modify the ApplicationManifest.xml and ServiceManifest.xml to add your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="72d5d-124">Per modificare i manifesti, vedere [Creare la prima applicazione contenitore di Service Fabric in Windows](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="72d5d-124">For modifying the manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="72d5d-125">La definizione del pacchetto di codice nel manifesto del servizio deve essere sostituita con l'immagine del contenitore corrispondente.</span><span class="sxs-lookup"><span data-stu-id="72d5d-125">The code package definition in the service manifest needs to be replaced with corresponding container image.</span></span> <span data-ttu-id="72d5d-126">Verificare di modificare il punto di ingresso in un tipo ContainerHost.</span><span class="sxs-lookup"><span data-stu-id="72d5d-126">Make sure to change the EntryPoint to a ContainerHost type.</span></span>

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers to Service Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables to your container: -->    
</CodePackage>
  ```

8. <span data-ttu-id="72d5d-127">Aggiungere il mapping da porta a host per la replica e un endpoint di servizio.</span><span class="sxs-lookup"><span data-stu-id="72d5d-127">Add the port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="72d5d-128">Poiché entrambe queste porte vengono assegnate in fase di esecuzione di Service Fabric, il ContainerPort è impostato su zero per usare la porta assegnata per il mapping.</span><span class="sxs-lookup"><span data-stu-id="72d5d-128">Since both these ports are assigned at runtime by Service Fabric, the ContainerPort is set to zero to use the assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="72d5d-129">Per testare questa applicazione, è necessario distribuirla in un cluster che esegue la versione 5.7 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="72d5d-129">To test this application, you need to deploy it to a cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="72d5d-130">È anche necessario modificare e aggiornare le impostazioni del cluster per abilitare questa funzionalità di anteprima.</span><span class="sxs-lookup"><span data-stu-id="72d5d-130">In addition, you need to edit and update the cluster settings to enable this preview feature.</span></span> <span data-ttu-id="72d5d-131">Seguire la procedura in questo [articolo](service-fabric-cluster-fabric-settings.md) per aggiungere l'impostazione illustrata di seguito.</span><span class="sxs-lookup"><span data-stu-id="72d5d-131">Follow the steps in this [article](service-fabric-cluster-fabric-settings.md) to add the setting shown next.</span></span>
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
10. <span data-ttu-id="72d5d-132">Successivamente, [distribuire](service-fabric-deploy-remove-applications.md) il pacchetto di applicazioni modificato in questo cluster.</span><span class="sxs-lookup"><span data-stu-id="72d5d-132">Next [deploy](service-fabric-deploy-remove-applications.md) the edited application package to this cluster.</span></span>

<span data-ttu-id="72d5d-133">Ora si dovrebbe avere un'applicazione di Service Fabric distribuita nei contenitori che esegue il cluster.</span><span class="sxs-lookup"><span data-stu-id="72d5d-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72d5d-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="72d5d-134">Next steps</span></span>
* <span data-ttu-id="72d5d-135">Altre informazioni sull'esecuzione di [contenitori in Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="72d5d-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="72d5d-136">Altre informazioni sul [ciclo di vita dell'applicazione](service-fabric-application-lifecycle.md) di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="72d5d-136">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
