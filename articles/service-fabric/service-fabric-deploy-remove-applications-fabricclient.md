---
title: distribuzione di applicazioni di Service Fabric aaaAzure | Documenti Microsoft
description: Utilizzare hello FabricClient APIs toodeploy e rimuovere le applicazioni nell'infrastruttura del servizio.
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
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="f13e0-103">Distribuire e rimuovere applicazioni con il client Fabric</span><span class="sxs-lookup"><span data-stu-id="f13e0-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f13e0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f13e0-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="f13e0-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f13e0-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="f13e0-106">API client Fabric</span><span class="sxs-lookup"><span data-stu-id="f13e0-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="f13e0-107">Dopo aver creato il [pacchetto di un tipo di applicazione][10], è possibile distribuirlo in un cluster di Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f13e0-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="f13e0-108">Distribuzione coinvolge hello tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="f13e0-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="f13e0-109">Caricare l'archivio di immagini toohello pacchetto applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f13e0-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="f13e0-110">Registrare il tipo di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f13e0-110">Register hello application type</span></span>
3. <span data-ttu-id="f13e0-111">Creare l'istanza dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f13e0-111">Create hello application instance</span></span>

<span data-ttu-id="f13e0-112">Dopo che un'applicazione viene distribuita e cluster hello è in esecuzione un'istanza, è possibile eliminare l'istanza dell'applicazione hello e il relativo tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="f13e0-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="f13e0-113">Rimuovi toocompletely un'applicazione dal cluster hello prevede hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f13e0-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="f13e0-114">Rimuovere hello esegue l'istanza dell'applicazione (o eliminare)</span><span class="sxs-lookup"><span data-stu-id="f13e0-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="f13e0-115">Annullare la registrazione del tipo di applicazione hello se non è più necessario</span><span class="sxs-lookup"><span data-stu-id="f13e0-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="f13e0-116">Rimuovere il pacchetto di applicazione hello dall'archivio immagini hello</span><span class="sxs-lookup"><span data-stu-id="f13e0-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="f13e0-117">Se si utilizza [Visual Studio per la distribuzione e debug di applicazioni](service-fabric-publish-app-remote-cluster.md) nel cluster di sviluppo locale, tutti i passaggi precedenti di hello vengono gestite automaticamente tramite uno script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f13e0-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="f13e0-118">Questo script è presente in hello *script* nella cartella del progetto di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f13e0-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="f13e0-119">In questo articolo vengono fornite informazioni su cosa fa lo script in modo che sia possibile eseguire hello stesse operazioni all'esterno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f13e0-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="f13e0-120">Connettere il cluster toohello</span><span class="sxs-lookup"><span data-stu-id="f13e0-120">Connect toohello cluster</span></span>
<span data-ttu-id="f13e0-121">Connettere il cluster di toohello creando un [FabricClient](/dotnet/api/system.fabric.fabricclient) istanza prima di eseguire una delle hello esempi di codice in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f13e0-121">Connect toohello cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of hello code examples in this article.</span></span> <span data-ttu-id="f13e0-122">Per esempi di cluster di sviluppo locale tooa connessione o un cluster remoto o un cluster protetto tramite Azure Active Directory, X509 certificati o Active Directory di Windows vedere [Connetti tooa sicura cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="f13e0-122">For examples of connecting tooa local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="f13e0-123">cluster di sviluppo locale di toohello di tooconnect, eseguire hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f13e0-123">tooconnect toohello local development cluster, run hello following:</span></span>

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a><span data-ttu-id="f13e0-124">Caricare il pacchetto di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f13e0-124">Upload hello application package</span></span>
<span data-ttu-id="f13e0-125">Si supponga di compilare e assemblare un'applicazione denominata *MyApplication* in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f13e0-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="f13e0-126">Per impostazione predefinita, nome del tipo applicazione hello elencati in ApplicationManifest.xml hello è "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="f13e0-126">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="f13e0-127">Hello pacchetto di applicazione, che contiene un manifesto dell'applicazione hello, i manifesti del servizio e i pacchetti di configurazione/codice/dati, si trova *C:\Users\&lt; nome utente&gt;\Documents\Visual 2017\Projects\ Studio MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="f13e0-127">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="f13e0-128">Caricamento del pacchetto dell'applicazione hello lo inserisce in una posizione accessibile da componenti interni di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="f13e0-128">Uploading hello application package puts it in a location that's accessible by hello internal Service Fabric components.</span></span> <span data-ttu-id="f13e0-129">Service Fabric verifica il pacchetto di applicazione hello durante la registrazione di hello hello del pacchetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="f13e0-129">Service Fabric verifies hello application package during hello registration of hello application package.</span></span> <span data-ttu-id="f13e0-130">Tuttavia, se si desidera localmente pacchetto dell'applicazione hello tooverify (ad esempio, prima del caricamento), utilizzare hello [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f13e0-130">However, if you want tooverify hello application package locally (i.e., before uploading), use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="f13e0-131">Hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API Carica archivio di immagini cluster toohello pacchetto applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f13e0-131">hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads hello application package toohello cluster image store.</span></span> 

<span data-ttu-id="f13e0-132">Se il pacchetto di applicazione hello è di grandi dimensioni e/o dispone di molti file, è possibile [comprimerli](service-fabric-package-apps.md#compress-a-package) e copiarlo toohello archivio di immagini tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f13e0-132">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it toohello image store using PowerShell.</span></span> <span data-ttu-id="f13e0-133">la compressione di Hello riduce hello dimensioni e il numero di hello dei file.</span><span class="sxs-lookup"><span data-stu-id="f13e0-133">hello compression reduces hello size and hello number of files.</span></span>

<span data-ttu-id="f13e0-134">Vedere [comprendere una stringa di connessione di archivio immagine hello](service-fabric-image-store-connection-string.md) informazioni supplementari sull'archivio di immagini hello e immagine archiviare una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="f13e0-134">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="f13e0-135">Registrare il pacchetto di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f13e0-135">Register hello application package</span></span>
<span data-ttu-id="f13e0-136">tipo di applicazione Hello e versione dichiarati nel manifesto dell'applicazione hello diventano disponibile per l'utilizzo quando il pacchetto di applicazione hello viene registrato.</span><span class="sxs-lookup"><span data-stu-id="f13e0-136">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="f13e0-137">sistema Hello legge pacchetto hello caricato nel passaggio precedente hello, verifica i pacchetti hello, elabora i contenuti del pacchetto hello e Copia percorso di sistema interno tooan pacchetto hello elaborato.</span><span class="sxs-lookup"><span data-stu-id="f13e0-137">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="f13e0-138">Hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registri hello tipo di applicazione in cluster hello e renderlo disponibile per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f13e0-138">hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers hello application type in hello cluster and make it available for deployment.</span></span>

<span data-ttu-id="f13e0-139">Hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API fornisce informazioni su tutti i tipi di applicazione registrato correttamente.</span><span class="sxs-lookup"><span data-stu-id="f13e0-139">hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="f13e0-140">È possibile utilizzare questo toodetermine API quando viene eseguita la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="f13e0-140">You can use this API toodetermine when hello registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="f13e0-141">Creare un'istanza dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f13e0-141">Create an application instance</span></span>
<span data-ttu-id="f13e0-142">È possibile creare un'istanza di un'applicazione da qualsiasi tipo di applicazione che è stato registrato correttamente tramite hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="f13e0-142">You can instantiate an application from any application type that has been registered successfully by using hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="f13e0-143">nome Hello di ogni applicazione deve iniziare con hello *"fabric:"* dello schema e deve essere univoco per ogni istanza dell'applicazione (all'interno di un cluster).</span><span class="sxs-lookup"><span data-stu-id="f13e0-143">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="f13e0-144">Vengono creati anche i servizi predefiniti definiti nel manifesto dell'applicazione hello del tipo di applicazione di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="f13e0-144">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

<span data-ttu-id="f13e0-145">Per qualsiasi versione di un tipo di applicazione registrato, è possibile creare più istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f13e0-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="f13e0-146">Ogni istanza dell'applicazione viene eseguita in isolamento, con una propria directory di lavoro e un proprio set di processi.</span><span class="sxs-lookup"><span data-stu-id="f13e0-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="f13e0-147">toosee denominato applicazioni e servizi sono in esecuzione in cluster hello, eseguire hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) e [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API.</span><span class="sxs-lookup"><span data-stu-id="f13e0-147">toosee which named applications and services are running in hello cluster, run hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="f13e0-148">Creare un'istanza del servizio</span><span class="sxs-lookup"><span data-stu-id="f13e0-148">Create a service instance</span></span>
<span data-ttu-id="f13e0-149">È possibile creare un'istanza di un servizio da un tipo di servizio utilizzando hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="f13e0-149">You can instantiate a service from a service type using hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="f13e0-150">Se il servizio di hello è dichiarato come un servizio predefinito nel manifesto dell'applicazione hello, viene creata un'istanza servizio hello quando viene creata un'istanza di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f13e0-150">If hello service is declared as a default service in hello application manifest, hello service is instantiated when hello application is instantiated.</span></span>  <span data-ttu-id="f13e0-151">Chiamare il metodo hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API per un servizio che viene creata un'istanza già restituirà un'eccezione di tipo FabricException contenente un codice di errore con un valore di FabricErrorCode.ServiceAlreadyExists.</span><span class="sxs-lookup"><span data-stu-id="f13e0-151">Calling hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="f13e0-152">Rimuovere un'istanza del servizio</span><span class="sxs-lookup"><span data-stu-id="f13e0-152">Remove a service instance</span></span>
<span data-ttu-id="f13e0-153">Quando un'istanza del servizio non è più necessario, è possibile rimuoverlo dal hello eseguendo l'istanza dell'applicazione chiamante hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="f13e0-153">When a service instance is no longer needed, you can remove it from hello running application instance by calling hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="f13e0-154">Tale operazione non può essere annullata e lo stato del servizio non può essere recuperato.</span><span class="sxs-lookup"><span data-stu-id="f13e0-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="f13e0-155">Rimuovere un'istanza dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f13e0-155">Remove an application instance</span></span>
<span data-ttu-id="f13e0-156">Quando un'istanza di applicazione non è più necessario, è possibile rimuoverlo in modo permanente in base al nome utilizzando hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="f13e0-156">When an application instance is no longer needed, you can permanently remove it by name using hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="f13e0-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) rimuove automaticamente tutti i servizi che appartengono toohello applicazione nonché, in modo permanente la rimozione di tutti gli stati di servizio.</span><span class="sxs-lookup"><span data-stu-id="f13e0-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="f13e0-158">Tale operazione non può essere annullata e lo stato dell'applicazione non può essere recuperato.</span><span class="sxs-lookup"><span data-stu-id="f13e0-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="f13e0-159">Annullare la registrazione di un tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="f13e0-159">Unregister an application type</span></span>
<span data-ttu-id="f13e0-160">Quando una particolare versione di un tipo di applicazione non è più necessario, si deve annullare la registrazione di quella versione specifica del tipo di applicazione hello utilizzando hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="f13e0-160">When a particular version of an application type is no longer needed, you should unregister that particular version of hello application type using hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="f13e0-161">Annullamento della registrazione le versioni di spazio di archiviazione delle versioni di applicazione tipi utilizzato dall'archivio immagini hello.</span><span class="sxs-lookup"><span data-stu-id="f13e0-161">Unregistering unused versions of application types releases storage space used by hello image store.</span></span> <span data-ttu-id="f13e0-162">Una versione di un tipo di applicazione è possibile annullare la registrazione fino a quando non esistono applicazioni vengono creata un'istanza con tale versione del tipo di applicazione hello e non gli aggiornamenti in sospeso dell'applicazione fa riferimento a tale versione del tipo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f13e0-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of hello application type and no pending application upgrades are referencing that version of hello application type.</span></span>

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="f13e0-163">Rimuovere un pacchetto di applicazioni dall'archivio immagini hello</span><span class="sxs-lookup"><span data-stu-id="f13e0-163">Remove an application package from hello image store</span></span>
<span data-ttu-id="f13e0-164">Quando un pacchetto di applicazione non è più necessario, è possibile eliminarlo dal hello immagine archivio toofree le risorse di sistema utilizzando hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span><span class="sxs-lookup"><span data-stu-id="f13e0-164">When an application package is no longer needed, you can delete it from hello image store toofree up system resources using hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f13e0-165">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="f13e0-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="f13e0-166">Copy-ServiceFabricApplicationPackage chiede un parametro ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="f13e0-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="f13e0-167">ambiente di Service Fabric SDK Hello dovrebbe già disporre hello corretto impostare valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="f13e0-167">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="f13e0-168">Ma se necessario, hello ImageStoreConnectionString per tutti i comandi debba corrispondere valore hello tale hello dell'infrastruttura del servizio cluster utilizza.</span><span class="sxs-lookup"><span data-stu-id="f13e0-168">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="f13e0-169">È possibile trovare hello ImageStoreConnectionString nel manifesto del cluster hello, recuperati tramite hello [Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) e i comandi Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="f13e0-169">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="f13e0-170">Hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet, che fa parte del modulo PowerShell di Service Fabric SDK hello, è immagine hello tooget utilizzati archiviare la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="f13e0-170">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="f13e0-171">modulo SDK di hello di tooimport, eseguire:</span><span class="sxs-lookup"><span data-stu-id="f13e0-171">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="f13e0-172">Hello ImageStoreConnectionString viene trovato nel manifesto del cluster hello:</span><span class="sxs-lookup"><span data-stu-id="f13e0-172">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="f13e0-173">Vedere [comprendere una stringa di connessione di archivio immagine hello](service-fabric-image-store-connection-string.md) informazioni supplementari sull'archivio di immagini hello e immagine archiviare una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="f13e0-173">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="f13e0-174">Distribuire un pacchetto dell'applicazione di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="f13e0-174">Deploy large application package</span></span>
<span data-ttu-id="f13e0-175">Problema: l'API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) raggiunge il timeout per un pacchetto dell'applicazione di grandi dimensioni (nell'ordine di GB).</span><span class="sxs-lookup"><span data-stu-id="f13e0-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="f13e0-176">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="f13e0-176">Try:</span></span>
- <span data-ttu-id="f13e0-177">Specificare un timeout maggiore per il metodo [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) con il parametro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="f13e0-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="f13e0-178">Per impostazione predefinita, il timeout di hello è 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="f13e0-178">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="f13e0-179">Controllare la connessione di rete hello tra il computer di origine e il cluster.</span><span class="sxs-lookup"><span data-stu-id="f13e0-179">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="f13e0-180">Se hello connessione è lenta, considerare l'utilizzo di un computer con una connessione di rete migliorata.</span><span class="sxs-lookup"><span data-stu-id="f13e0-180">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="f13e0-181">Se hello client macchina si trova in un'altra area di cluster hello, considerare l'uso di un computer client in un'area più vicino o stesso come cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f13e0-181">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="f13e0-182">Controllare se si stiano raggiungendo le limitazioni esterne.</span><span class="sxs-lookup"><span data-stu-id="f13e0-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="f13e0-183">Ad esempio, quando l'archivio immagini hello è configurato toouse azure storage, caricamento può essere limitato.</span><span class="sxs-lookup"><span data-stu-id="f13e0-183">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="f13e0-184">Problema: il pacchetto è stato caricato completamente, ma si è verificato il timeout dell'API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync). Soluzione:</span><span class="sxs-lookup"><span data-stu-id="f13e0-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out. Try:</span></span>
- <span data-ttu-id="f13e0-185">[Comprimere il pacchetto di hello](service-fabric-package-apps.md#compress-a-package) prima della copia toohello archivio di immagini.</span><span class="sxs-lookup"><span data-stu-id="f13e0-185">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="f13e0-186">la compressione di Hello riduce le dimensioni di hello e hello diversi file, che a sua volta riduce hello quantità di traffico e di lavoro di Service Fabric devono eseguire.</span><span class="sxs-lookup"><span data-stu-id="f13e0-186">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="f13e0-187">operazione di caricamento Hello potrebbe risultare più lenta (in particolare se si include il tempo di compressione hello), ma il tipo di applicazione hello registrare e annullare la registrazione sono più veloci.</span><span class="sxs-lookup"><span data-stu-id="f13e0-187">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="f13e0-188">Specificare un timeout maggiore per l'API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con il parametro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="f13e0-188">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="f13e0-189">Distribuire un pacchetto di applicazione con numerosi file</span><span class="sxs-lookup"><span data-stu-id="f13e0-189">Deploy application package with many files</span></span>
<span data-ttu-id="f13e0-190">Problema: si verifica un timeout di [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) per un pacchetto di applicazione con molti file (nell'ordine di migliaia).</span><span class="sxs-lookup"><span data-stu-id="f13e0-190">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="f13e0-191">Soluzione:</span><span class="sxs-lookup"><span data-stu-id="f13e0-191">Try:</span></span>
- <span data-ttu-id="f13e0-192">[Comprimere il pacchetto di hello](service-fabric-package-apps.md#compress-a-package) prima della copia toohello archivio di immagini.</span><span class="sxs-lookup"><span data-stu-id="f13e0-192">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="f13e0-193">la compressione di Hello riduce il numero di hello di file.</span><span class="sxs-lookup"><span data-stu-id="f13e0-193">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="f13e0-194">Specificare un timeout maggiore per il metodo [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con il parametro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="f13e0-194">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="f13e0-195">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="f13e0-195">Code example</span></span>
<span data-ttu-id="f13e0-196">Hello esempio copia di un archivio di immagini toohello pacchetto di applicazione, il tipo di applicazione hello viene eseguito il provisioning, crea un'istanza di applicazione, crea un'istanza del servizio, istanza dell'applicazione hello rimuove, disposizioni di un tipo di applicazione hello, e Elimina il pacchetto di applicazione hello dall'archivio immagini hello.</span><span class="sxs-lookup"><span data-stu-id="f13e0-196">hello following example copies an application package toohello image store, provisions hello application type, creates an application instance, creates a service instance, removes hello application instance, un-provisions hello application type, and deletes hello application package from hello image store.</span></span>

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

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
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

    //  Create hello application instance.
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

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
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

    // Delete an application instance from hello application type.
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

    // Un-provision hello application type.
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

    // Delete hello application package from a location in hello image store.
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

## <a name="next-steps"></a><span data-ttu-id="f13e0-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f13e0-197">Next steps</span></span>
[<span data-ttu-id="f13e0-198">Aggiornamento di un'applicazione di infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="f13e0-198">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="f13e0-199">Introduzione all'integrità di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f13e0-199">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="f13e0-200">Eseguire la diagnosi e la risoluzione dei problemi di un servizio di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f13e0-200">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="f13e0-201">Modellare un'applicazione in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f13e0-201">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
