---
title: Distribuzione dell'applicazione Azure Service Fabric | Microsoft Docs
description: Usare le API del client Fabric per distribuire e rimuovere le applicazioni in Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: 2e4ca1069b4e8e473b26b790e81770b41e25ff50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="fd95f-103">Distribuire e rimuovere applicazioni con il client Fabric</span><span class="sxs-lookup"><span data-stu-id="fd95f-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd95f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd95f-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="fd95f-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fd95f-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="fd95f-106">API client Fabric</span><span class="sxs-lookup"><span data-stu-id="fd95f-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="fd95f-107">Dopo aver creato il [pacchetto di un tipo di applicazione][10], è possibile distribuirlo in un cluster di Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fd95f-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="fd95f-108">La distribuzione prevede i tre passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd95f-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="fd95f-109">Caricamento del pacchetto dell'applicazione nell'archivio di immagini</span><span class="sxs-lookup"><span data-stu-id="fd95f-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="fd95f-110">Registrare il tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="fd95f-110">Register the application type</span></span>
3. <span data-ttu-id="fd95f-111">Creare l'istanza dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="fd95f-111">Create the application instance</span></span>

<span data-ttu-id="fd95f-112">Dopo che un'applicazione è stata distribuita e un'istanza è in esecuzione nel cluster, è possibile eliminare l'istanza dell'applicazione e il tipo di applicazione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="fd95f-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="fd95f-113">Per rimuovere completamente un'applicazione dal cluster, sono necessari i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd95f-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="fd95f-114">Rimuovere (o eliminare) l'istanza dell'applicazione in esecuzione</span><span class="sxs-lookup"><span data-stu-id="fd95f-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="fd95f-115">Annullare la registrazione del tipo di applicazione se non è più necessario</span><span class="sxs-lookup"><span data-stu-id="fd95f-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="fd95f-116">Rimuovere il pacchetto applicazione da Image Store.</span><span class="sxs-lookup"><span data-stu-id="fd95f-116">Remove the application package from the image store</span></span>

<span data-ttu-id="fd95f-117">Se si usa [Visual Studio per eseguire la distribuzione e il debug delle applicazioni](service-fabric-publish-app-remote-cluster.md) nel cluster di sviluppo locale, tutti i passaggi precedenti vengono gestiti automaticamente tramite uno script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd95f-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="fd95f-118">Questo script è disponibile nella cartella *Scripts* del progetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fd95f-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="fd95f-119">Questo articolo illustra le operazioni eseguite da tali script per consentirne l'esecuzione anche all'esterno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd95f-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="fd95f-120">Connettersi al cluster</span><span class="sxs-lookup"><span data-stu-id="fd95f-120">Connect to the cluster</span></span>
<span data-ttu-id="fd95f-121">Connettersi al cluster tramite la creazione di un'istanza [client Fabric](/dotnet/api/system.fabric.fabricclient) prima di eseguire uno degli esempi di codice forniti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="fd95f-121">Connect to the cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of the code examples in this article.</span></span> <span data-ttu-id="fd95f-122">Per esempi di connessione a un cluster di sviluppo locale, un cluster remoto o un cluster protetto usando Azure Active Directory, certificati X509 o Windows Active Directory, vedere [Connettersi a un cluster sicuro](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="fd95f-122">For examples of connecting to a local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="fd95f-123">Per connettersi al cluster di sviluppo locale eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd95f-123">To connect to the local development cluster, run the following:</span></span>

```csharp
// Connect to the local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-the-application-package"></a><span data-ttu-id="fd95f-124">Caricare il pacchetto applicazione</span><span class="sxs-lookup"><span data-stu-id="fd95f-124">Upload the application package</span></span>
<span data-ttu-id="fd95f-125">Si supponga di compilare e assemblare un'applicazione denominata *MyApplication* in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd95f-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="fd95f-126">Per impostazione predefinita, il nome del tipo di applicazione elencato nel file ApplicationManifest.xml è "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="fd95f-126">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="fd95f-127">Il pacchetto dell'applicazione, che contiene il manifesto dell'applicazione necessario, i manifesti dei servizi e i pacchetti di codice, configurazione e dati, si trova in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="fd95f-127">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="fd95f-128">Quando si carica il pacchetto dell'applicazione, lo si inserisce in un percorso accessibile ai componenti interni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fd95f-128">Uploading the application package puts it in a location that's accessible by the internal Service Fabric components.</span></span> <span data-ttu-id="fd95f-129">Service Fabric verifica il pacchetto dell'applicazione durante la registrazione.</span><span class="sxs-lookup"><span data-stu-id="fd95f-129">Service Fabric verifies the application package during the registration of the application package.</span></span> <span data-ttu-id="fd95f-130">Tuttavia, se si desidera verificare il pacchetto dell'applicazione in locale, ad esempio prima di caricarlo, usare il cmdlet [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="fd95f-130">However, if you want to verify the application package locally (i.e., before uploading), use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="fd95f-131">L'API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) carica il pacchetto dell'applicazione nell'archivio immagini del cluster.</span><span class="sxs-lookup"><span data-stu-id="fd95f-131">The [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads the application package to the cluster image store.</span></span> 

<span data-ttu-id="fd95f-132">Se il pacchetto dell'applicazione è di grandi dimensioni e/o è costituito da numerosi file, è possibile [comprimerlo](service-fabric-package-apps.md#compress-a-package) e copiarlo nell'archivio immagini con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd95f-132">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it to the image store using PowerShell.</span></span> <span data-ttu-id="fd95f-133">La compressione riduce le dimensioni e il numero di file.</span><span class="sxs-lookup"><span data-stu-id="fd95f-133">The compression reduces the size and the number of files.</span></span>

<span data-ttu-id="fd95f-134">Per informazioni agguntive sull'archivio di immagini e ImageStoreConnectionString, vedere [Understand the image store connection string](service-fabric-image-store-connection-string.md) (Comprendere la stringa di connessione dell'archivio di immagini).</span><span class="sxs-lookup"><span data-stu-id="fd95f-134">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="fd95f-135">Registrare il pacchetto applicazione</span><span class="sxs-lookup"><span data-stu-id="fd95f-135">Register the application package</span></span>
<span data-ttu-id="fd95f-136">Quando si registra il pacchetto dell'applicazione, il tipo e la versione dell'applicazione dichiarati nel manifesto di quest'ultima diventano disponibili per l'uso.</span><span class="sxs-lookup"><span data-stu-id="fd95f-136">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="fd95f-137">Il sistema leggerà il pacchetto caricato al passaggio precedente, lo verificherà, ne elaborerà il contenuto e infine copierà il pacchetto elaborato in un percorso di sistema interno.</span><span class="sxs-lookup"><span data-stu-id="fd95f-137">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="fd95f-138">L'API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) registra il tipo di applicazione nel cluster e la rende disponibile per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fd95f-138">The [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers the application type in the cluster and make it available for deployment.</span></span>

<span data-ttu-id="fd95f-139">L'API [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) fornisce informazioni su tutti i tipi di applicazioni registrati correttamente.</span><span class="sxs-lookup"><span data-stu-id="fd95f-139">The [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="fd95f-140">È possibile usare questa API per determinare quando viene eseguita la registrazione.</span><span class="sxs-lookup"><span data-stu-id="fd95f-140">You can use this API to determine when the registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="fd95f-141">Creare un'istanza dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="fd95f-141">Create an application instance</span></span>
<span data-ttu-id="fd95f-142">È possibile creare un'istanza di un'applicazione da qualsiasi tipo di applicazione registrato correttamente usando l'API [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync).</span><span class="sxs-lookup"><span data-stu-id="fd95f-142">You can instantiate an application from any application type that has been registered successfully by using the [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="fd95f-143">Il nome di ogni applicazione deve iniziare con lo schema *"fabric:"* e deve essere univoco per ogni istanza dell'applicazione (all'interno di un cluster).</span><span class="sxs-lookup"><span data-stu-id="fd95f-143">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="fd95f-144">Vengono creati anche i servizi predefiniti specificati nel manifesto dell'applicazione del tipo di applicazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="fd95f-144">Any default services defined in the application manifest of the target application type are also created.</span></span>

<span data-ttu-id="fd95f-145">Per qualsiasi versione di un tipo di applicazione registrato, è possibile creare più istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fd95f-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="fd95f-146">Ogni istanza dell'applicazione viene eseguita in isolamento, con una propria directory di lavoro e un proprio set di processi.</span><span class="sxs-lookup"><span data-stu-id="fd95f-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="fd95f-147">Per vedere quali applicazioni e servizi denominati sono in esecuzione nel cluster, eseguire le API [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) e [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync).</span><span class="sxs-lookup"><span data-stu-id="fd95f-147">To see which named applications and services are running in the cluster, run the [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="fd95f-148">Creare un'istanza del servizio</span><span class="sxs-lookup"><span data-stu-id="fd95f-148">Create a service instance</span></span>
<span data-ttu-id="fd95f-149">È possibile creare un'istanza di un servizio da un tipo di servizio usando l'API [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync).</span><span class="sxs-lookup"><span data-stu-id="fd95f-149">You can instantiate a service from a service type using the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="fd95f-150">Se il servizio è dichiarato come servizio predefinito nel manifesto dell'applicazione, viene creata un'istanza del servizio durante la creazione dell'istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fd95f-150">If the service is declared as a default service in the application manifest, the service is instantiated when the application is instantiated.</span></span>  <span data-ttu-id="fd95f-151">La chiamata all'API [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) per un servizio di cui è già stata creata un'istanza restituirà un'eccezione di tipo FabricException contenente un codice di errore con un valore di FabricErrorCode.ServiceAlreadyExists.</span><span class="sxs-lookup"><span data-stu-id="fd95f-151">Calling the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="fd95f-152">Rimuovere un'istanza del servizio</span><span class="sxs-lookup"><span data-stu-id="fd95f-152">Remove a service instance</span></span>
<span data-ttu-id="fd95f-153">Quando un'istanza del servizio non è più necessaria, è possibile rimuoverla dall'istanza dell'applicazione in esecuzione tramite la chiamata all'API [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="fd95f-153">When a service instance is no longer needed, you can remove it from the running application instance by calling the [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="fd95f-154">Tale operazione non può essere annullata e lo stato del servizio non può essere recuperato.</span><span class="sxs-lookup"><span data-stu-id="fd95f-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="fd95f-155">Rimuovere un'istanza dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="fd95f-155">Remove an application instance</span></span>
<span data-ttu-id="fd95f-156">Quando un'istanza dell'applicazione non è più necessaria, è possibile rimuoverla definitivamente in base al nome tramite la chiamata all'API [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync).</span><span class="sxs-lookup"><span data-stu-id="fd95f-156">When an application instance is no longer needed, you can permanently remove it by name using the [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="fd95f-157">Il metodo [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) rimuove automaticamente anche tutti i servizi che appartengono all'applicazione, rimuovendo così in modo permanente lo stato di tutti i servizi.</span><span class="sxs-lookup"><span data-stu-id="fd95f-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="fd95f-158">Tale operazione non può essere annullata e lo stato dell'applicazione non può essere recuperato.</span><span class="sxs-lookup"><span data-stu-id="fd95f-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="fd95f-159">Annullare la registrazione di un tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="fd95f-159">Unregister an application type</span></span>
<span data-ttu-id="fd95f-160">Quando una determinata versione di un tipo di applicazione non è più necessaria, è consigliabile annullare la registrazione di quella specifica versione del tipo di applicazione usando l'API [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync).</span><span class="sxs-lookup"><span data-stu-id="fd95f-160">When a particular version of an application type is no longer needed, you should unregister that particular version of the application type using the [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="fd95f-161">L'annullamento della registrazione delle versioni inutilizzate dei tipi di applicazioni rilascia lo spazio di archiviazione usato dall'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="fd95f-161">Unregistering unused versions of application types releases storage space used by the image store.</span></span> <span data-ttu-id="fd95f-162">È possibile annullare la registrazione di una versione di un tipo di applicazione solo se non sono state create istanze di applicazioni basate su quella versione del tipo di applicazione e non vi sono aggiornamenti di applicazioni in sospeso che fanno riferimento a quella versione del tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="fd95f-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of the application type and no pending application upgrades are referencing that version of the application type.</span></span>

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="fd95f-163">Rimuovere il pacchetto di un'applicazione dall'archivio di immagini</span><span class="sxs-lookup"><span data-stu-id="fd95f-163">Remove an application package from the image store</span></span>
<span data-ttu-id="fd95f-164">Quando il pacchetto di un'applicazione non è più necessario, è possibile eliminarlo dall'archivio immagini tramite l'API [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage), liberando così risorse di sistema.</span><span class="sxs-lookup"><span data-stu-id="fd95f-164">When an application package is no longer needed, you can delete it from the image store to free up system resources using the [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fd95f-165">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="fd95f-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="fd95f-166">Copy-ServiceFabricApplicationPackage chiede un parametro ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="fd95f-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="fd95f-167">Nell'ambiente Service Fabric SDK dovrebbero già essere configurate le impostazioni predefinite corrette.</span><span class="sxs-lookup"><span data-stu-id="fd95f-167">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="fd95f-168">Tuttavia, se necessario, ImageStoreConnectionString per tutti i comandi deve corrispondere al valore che viene usato dal cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fd95f-168">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="fd95f-169">È possibile trovare ImageStoreConnectionString nel manifesto del cluster, recuperato tramite i comandi [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) e Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="fd95f-169">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="fd95f-170">Il cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , che fa parte del modulo PowerShell Service Fabric SDK, viene usato per ottenere la stringa di connessione dell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="fd95f-170">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="fd95f-171">Per importare il modulo SDK, eseguire:</span><span class="sxs-lookup"><span data-stu-id="fd95f-171">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="fd95f-172">ImageStoreConnectionString è disponibile nel manifesto del cluster:</span><span class="sxs-lookup"><span data-stu-id="fd95f-172">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="fd95f-173">Per informazioni agguntive sull'archivio di immagini e ImageStoreConnectionString, vedere [Understand the image store connection string](service-fabric-image-store-connection-string.md) (Comprendere la stringa di connessione dell'archivio di immagini).</span><span class="sxs-lookup"><span data-stu-id="fd95f-173">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="fd95f-174">Distribuire un pacchetto dell'applicazione di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="fd95f-174">Deploy large application package</span></span>
<span data-ttu-id="fd95f-175">Problema: l'API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) raggiunge il timeout per un pacchetto dell'applicazione di grandi dimensioni (nell'ordine di GB).</span><span class="sxs-lookup"><span data-stu-id="fd95f-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="fd95f-176">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="fd95f-176">Try:</span></span>
- <span data-ttu-id="fd95f-177">Specificare un timeout maggiore per il metodo [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) con il parametro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="fd95f-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="fd95f-178">Il timeout è di 30 minuti per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fd95f-178">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="fd95f-179">Controllare la connessione di rete tra il computer di origine e il cluster.</span><span class="sxs-lookup"><span data-stu-id="fd95f-179">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="fd95f-180">Se la connessione è lenta, provare a usare una macchina con una connessione di rete più veloce.</span><span class="sxs-lookup"><span data-stu-id="fd95f-180">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="fd95f-181">Se il computer client si trova in un'area diversa dal cluster, si consiglia di usare un computer cliente in un'area più vicina o nella stessa area del cluster.</span><span class="sxs-lookup"><span data-stu-id="fd95f-181">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="fd95f-182">Controllare se si stiano raggiungendo le limitazioni esterne.</span><span class="sxs-lookup"><span data-stu-id="fd95f-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="fd95f-183">Ad esempio, quando l'archivio immagini è configurato per usare l'archiviazione di Azure, il caricamento potrebbe essere limitato.</span><span class="sxs-lookup"><span data-stu-id="fd95f-183">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="fd95f-184">Problema: il pacchetto è stato caricato completamente, ma si è verificato il timeout dell'API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync).</span><span class="sxs-lookup"><span data-stu-id="fd95f-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out.</span></span>
<span data-ttu-id="fd95f-185">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="fd95f-185">Try:</span></span>
- <span data-ttu-id="fd95f-186">[Comprimere il pacchetto](service-fabric-package-apps.md#compress-a-package) prima di copiarlo nell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="fd95f-186">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="fd95f-187">La compressione riduce le dimensioni e il numero di file, cosa che a sua volta riduce il traffico e le operazioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fd95f-187">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="fd95f-188">L'operazione di caricamento potrebbe risultare più lenta (specialmente se si include il tempo di compressione), ma registrazione e relativo annullamento del tipo dell'applicazione saranno più veloci.</span><span class="sxs-lookup"><span data-stu-id="fd95f-188">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="fd95f-189">Specificare un timeout maggiore per l'API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con il parametro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="fd95f-189">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="fd95f-190">Distribuire un pacchetto di applicazione con numerosi file</span><span class="sxs-lookup"><span data-stu-id="fd95f-190">Deploy application package with many files</span></span>
<span data-ttu-id="fd95f-191">Problema: si verifica un timeout di [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) per un pacchetto di applicazione con molti file (nell'ordine di migliaia).</span><span class="sxs-lookup"><span data-stu-id="fd95f-191">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="fd95f-192">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="fd95f-192">Try:</span></span>
- <span data-ttu-id="fd95f-193">[Comprimere il pacchetto](service-fabric-package-apps.md#compress-a-package) prima di copiarlo nell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="fd95f-193">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="fd95f-194">La compressione riduce il numero dei file.</span><span class="sxs-lookup"><span data-stu-id="fd95f-194">The compression reduces the number of files.</span></span>
- <span data-ttu-id="fd95f-195">Specificare un timeout maggiore per il metodo [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con il parametro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="fd95f-195">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="fd95f-196">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="fd95f-196">Code example</span></span>
<span data-ttu-id="fd95f-197">L'esempio seguente copia un pacchetto dell'applicazione nell'archivio immagini, effettua il provisioning del tipo di applicazione, crea un'istanza dell'applicazione, crea un'istanza del servizio, rimuove l'istanza dell'applicazione, annulla il provisioning del tipo di applicazione ed elimina il pacchetto dell'applicazione dall'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="fd95f-197">The following example copies an application package to the image store, provisions the application type, creates an application instance, creates a service instance, removes the application instance, un-provisions the application type, and deletes the application package from the image store.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect to the cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy the application package to a location in the image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied to {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy to Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision the application.  "MyApplicationV1" is the folder in the image store where the application package is located. 
    // The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) 
    // is now registered in the cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create the application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create the stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create the service instance.  If the service is declared as a default service in the ApplicationManifest.xml,
    // the service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from the application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision the application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete the application package from a location in the image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a><span data-ttu-id="fd95f-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd95f-198">Next steps</span></span>
[<span data-ttu-id="fd95f-199">Aggiornamento di un'applicazione di infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="fd95f-199">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="fd95f-200">Introduzione all'integrità di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fd95f-200">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="fd95f-201">Eseguire la diagnosi e la risoluzione dei problemi di un servizio di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fd95f-201">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="fd95f-202">Modellare un'applicazione in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fd95f-202">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
