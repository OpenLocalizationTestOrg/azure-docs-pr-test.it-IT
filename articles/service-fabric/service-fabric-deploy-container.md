---
title: aaaService dell'infrastruttura e la distribuzione di contenitori | Documenti Microsoft
description: "Service Fabric e hello utilizzare contenitori toodeploy microservizio applicazioni. Questo articolo descrive le funzionalità di hello forniti per i contenitori e come toodeploy immagine di un contenitore di Windows in un cluster di Service Fabric."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a><span data-ttu-id="7bce0-104">Distribuire un tooService di contenitore di Windows Fabric</span><span class="sxs-lookup"><span data-stu-id="7bce0-104">Deploy a Windows container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7bce0-105">Distribuire un contenitore Windows</span><span class="sxs-lookup"><span data-stu-id="7bce0-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="7bce0-106">Distribuire un contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="7bce0-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="7bce0-107">In questo articolo illustra hello processo di compilazione di servizi nei contenitori in contenitori di Windows.</span><span class="sxs-lookup"><span data-stu-id="7bce0-107">This article walks you through hello process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="7bce0-108">Service Fabric offre diverse funzionalità che consentono di creare applicazioni costituite da microservizi eseguiti in contenitori.</span><span class="sxs-lookup"><span data-stu-id="7bce0-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="7bce0-109">funzionalità di Hello includono:</span><span class="sxs-lookup"><span data-stu-id="7bce0-109">hello capabilities include:</span></span>

* <span data-ttu-id="7bce0-110">Distribuzione e attivazione di immagini contenitore</span><span class="sxs-lookup"><span data-stu-id="7bce0-110">Container image deployment and activation</span></span>
* <span data-ttu-id="7bce0-111">Governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="7bce0-111">Resource governance</span></span>
* <span data-ttu-id="7bce0-112">Autenticazione nel repository</span><span class="sxs-lookup"><span data-stu-id="7bce0-112">Repository authentication</span></span>
* <span data-ttu-id="7bce0-113">Mapping tra porta del contenitore e porta dell'host</span><span class="sxs-lookup"><span data-stu-id="7bce0-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="7bce0-114">Individuazione e comunicazione da contenitore a contenitore</span><span class="sxs-lookup"><span data-stu-id="7bce0-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="7bce0-115">Tooconfigure possibilità e impostare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="7bce0-115">Ability tooconfigure and set environment variables</span></span>

<span data-ttu-id="7bce0-116">Ecco come funziona ciascuna di funzionalità quando si crea un pacchetto toobe un servizio nei contenitori inclusi nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7bce0-116">Let's look at how each of capabilities works when you're packaging a containerized service toobe included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="7bce0-117">Creare il pacchetto di un contenitore Windows</span><span class="sxs-lookup"><span data-stu-id="7bce0-117">Package a Windows container</span></span>
<span data-ttu-id="7bce0-118">Quando si comprime un contenitore, è possibile scegliere toouse un modello di progetto Visual Studio o [creare manualmente il pacchetto di applicazione hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="7bce0-118">When you package a container, you can choose toouse either a Visual Studio project template or [create hello application package manually](#manually).</span></span>  <span data-ttu-id="7bce0-119">Quando si usa Visual Studio, struttura del pacchetto dell'applicazione hello e i file manifesto vengono creati dal modello di progetto nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-119">When you use Visual Studio, hello application package structure and manifest files are created by hello New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="7bce0-120">toopackage modo più semplice di Hello un'immagine contenitore esistente in un servizio è toouse Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7bce0-120">hello easiest way toopackage an existing container image into a service is toouse Visual Studio.</span></span>

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a><span data-ttu-id="7bce0-121">Utilizzare Visual Studio toopackage un'immagine contenitore esistente</span><span class="sxs-lookup"><span data-stu-id="7bce0-121">Use Visual Studio toopackage an existing container image</span></span>
<span data-ttu-id="7bce0-122">Visual Studio fornisce un'infrastruttura a servizio toohelp modello di servizio si distribuisce un cluster di Service Fabric tooa contenitore.</span><span class="sxs-lookup"><span data-stu-id="7bce0-122">Visual Studio provides a Service Fabric service template toohelp you deploy a container tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="7bce0-123">Scegliere **File** > **Nuovo progetto** e creare un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7bce0-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="7bce0-124">Scegliere **contenitore Guest** come modello di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-124">Choose **Guest Container** as hello service template.</span></span>
3. <span data-ttu-id="7bce0-125">Scegliere **nome immagine** e fornire hello percorso toohello immagine nel repository del contenitore.</span><span class="sxs-lookup"><span data-stu-id="7bce0-125">Choose **Image Name** and provide hello path toohello image in your container repository.</span></span> <span data-ttu-id="7bce0-126">Ad esempio `myrepo/myimage:v1` in https://hub.docker.com</span><span class="sxs-lookup"><span data-stu-id="7bce0-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="7bce0-127">Assegnare un nome al servizio e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7bce0-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="7bce0-128">Se il servizio nei contenitori necessita di un endpoint per la comunicazione, è ora possibile aggiungere hello protocollo, porta e il file ServiceManifest.xml toohello del tipo.</span><span class="sxs-lookup"><span data-stu-id="7bce0-128">If your containerized service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="7bce0-129">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7bce0-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="7bce0-130">Fornendo hello `UriScheme`, Service Fabric registra automaticamente l'endpoint del contenitore hello con il servizio di denominazione per il rilevamento di hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-130">By providing hello `UriScheme`, Service Fabric automatically registers hello container endpoint with hello Naming service for discoverability.</span></span> <span data-ttu-id="7bce0-131">porta Hello può essere risolto (come illustrato nell'esempio sopra riportato hello) o allocata dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="7bce0-131">hello port can either be fixed (as shown in hello preceding example) or dynamically allocated.</span></span> <span data-ttu-id="7bce0-132">Se non si specifica una porta, viene dinamicamente allocato dall'intervallo di porte applicazione hello (come accade con qualsiasi servizio).</span><span class="sxs-lookup"><span data-stu-id="7bce0-132">If you don't specify a port, it is dynamically allocated from hello application port range (as would happen with any service).</span></span>
    <span data-ttu-id="7bce0-133">È inoltre necessario mapping delle porte toohost tooconfigure hello contenitore specificando un `PortBinding` criteri nel manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-133">You also need tooconfigure hello container toohost port mapping by specifying a `PortBinding` policy in hello application manifest.</span></span> <span data-ttu-id="7bce0-134">Per ulteriori informazioni, vedere [configurare il mapping di porta del contenitore toohost](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="7bce0-134">For more information, see [Configure container toohost port mapping](#Portsection).</span></span>
6. <span data-ttu-id="7bce0-135">Se per il contenitore è necessaria una governance delle risorse, aggiungere un elemento `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="7bce0-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="7bce0-136">Se il contenitore deve tooauthenticate con un repository privato, quindi aggiungere `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="7bce0-136">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="7bce0-137">Se si esegue in un computer Windows Server 2016 con supporto contenitore abilitato, è possibile utilizzare i pacchetti hello e pubblicare cluster locale tooyour toodeploy di azione.</span><span class="sxs-lookup"><span data-stu-id="7bce0-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use hello package and publish action toodeploy tooyour local cluster.</span></span> 
8. <span data-ttu-id="7bce0-138">Quando si è pronti, è possibile pubblicare hello applicazione tooa remota del cluster o archiviare hello soluzione toosource controllo del codice.</span><span class="sxs-lookup"><span data-stu-id="7bce0-138">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span> 

<span data-ttu-id="7bce0-139">Per un esempio, hello estrazione [esempi di codice di contenitori di Service Fabric su GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="7bce0-139">For an example, checkout hello [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="7bce0-140">Creazione di un cluster di Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7bce0-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="7bce0-141">toodeploy l'applicazione nei contenitori, è necessario un cluster che esegue Windows Server 2016 con supporto del contenitore abilitato toocreate.</span><span class="sxs-lookup"><span data-stu-id="7bce0-141">toodeploy your containerized application, you need toocreate a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="7bce0-142">Il cluster può essere eseguito localmente o distribuito con Azure Resource Manager in Azure.</span><span class="sxs-lookup"><span data-stu-id="7bce0-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="7bce0-143">toodeploy un cluster usando Gestione risorse di Azure, scegliere hello **Windows Server 2016 con contenitori** immagine opzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="7bce0-143">toodeploy a cluster using Azure Resource Manager, choose hello **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="7bce0-144">Vedere l'articolo hello [creare un cluster di Service Fabric usando Gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7bce0-144">See hello article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="7bce0-145">Assicurarsi di usare hello seguendo le impostazioni di gestione risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="7bce0-145">Ensure that you use hello following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="7bce0-146">È inoltre possibile utilizzare hello [modello cinque nodi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate un cluster.</span><span class="sxs-lookup"><span data-stu-id="7bce0-146">You can also use hello [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate a cluster.</span></span> <span data-ttu-id="7bce0-147">In alternativa è consigliabile leggere un [post di blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) della community sull'uso di Service Fabric e dei contenitori di Windows.</span><span class="sxs-lookup"><span data-stu-id="7bce0-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="7bce0-148">Creare manualmente il pacchetto e distribuire un'immagine del contenitore</span><span class="sxs-lookup"><span data-stu-id="7bce0-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="7bce0-149">il processo di Hello di creare manualmente il pacchetto del servizio nei contenitori si basa su hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7bce0-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="7bce0-150">Pubblicare hello contenitori tooyour repository.</span><span class="sxs-lookup"><span data-stu-id="7bce0-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="7bce0-151">Creare una struttura di directory hello del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="7bce0-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="7bce0-152">Modificare i file manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="7bce0-153">Modificare i file manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="7bce0-154">Distribuire e attivare un'immagine contenitore</span><span class="sxs-lookup"><span data-stu-id="7bce0-154">Deploy and activate a container image</span></span>
<span data-ttu-id="7bce0-155">In Service Fabric hello [modello applicativo](service-fabric-application-model.md), un contenitore rappresenta un'applicazione host nel quale servizio più repliche vengono inserite.</span><span class="sxs-lookup"><span data-stu-id="7bce0-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="7bce0-156">toodeploy e attivare un contenitore, un nome di hello put dell'immagine contenitore hello in un `ContainerHost` elemento nel manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="7bce0-157">Nel manifesto del servizio hello, aggiungere un `ContainerHost` per il punto di ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="7bce0-158">Quindi set hello `ImageName` nome hello toobe del repository del contenitore hello e dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="7bce0-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="7bce0-159">Hello manifesto parziale seguente viene illustrato un esempio di come contenitore hello toodeploy chiamata `myimage:v1` da un repository denominato `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="7bce0-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

<span data-ttu-id="7bce0-160">È possibile specificare toorun facoltativo comandi all'avvio il contenitore di hello in hello `Commands` elemento.</span><span class="sxs-lookup"><span data-stu-id="7bce0-160">You can specify optional commands toorun upon starting hello container under hello `Commands` element.</span></span> <span data-ttu-id="7bce0-161">Per aggiungere più comandi, separarli con virgole.</span><span class="sxs-lookup"><span data-stu-id="7bce0-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="7bce0-162">Informazioni sulla governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="7bce0-162">Understand resource governance</span></span>
<span data-ttu-id="7bce0-163">Governance delle risorse è possibile utilizzare una funzionalità di contenitore hello che limita le risorse hello hello contenitore nell'host di hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="7bce0-164">Hello `ResourceGovernancePolicy`, ed è specificato nel manifesto dell'applicazione hello è toodeclare utilizzati i limiti delle risorse per un pacchetto di codice servizio.</span><span class="sxs-lookup"><span data-stu-id="7bce0-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="7bce0-165">È possibile impostare i limiti delle risorse per hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="7bce0-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="7bce0-166">Memoria</span><span class="sxs-lookup"><span data-stu-id="7bce0-166">Memory</span></span>
* <span data-ttu-id="7bce0-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="7bce0-167">MemorySwap</span></span>
* <span data-ttu-id="7bce0-168">CpuShares (peso relativo CPU)</span><span class="sxs-lookup"><span data-stu-id="7bce0-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="7bce0-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="7bce0-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="7bce0-170">BlkioWeight (peso relativo BlockIO)</span><span class="sxs-lookup"><span data-stu-id="7bce0-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="7bce0-171">Il supporto per la definizione di limiti di I/O di blocco specifici, come operazioni di I/O al secondo, BPS in lettura/scrittura e altro, è previsto per una versione futura.</span><span class="sxs-lookup"><span data-stu-id="7bce0-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a><span data-ttu-id="7bce0-172">Autenticare un repository</span><span class="sxs-lookup"><span data-stu-id="7bce0-172">Authenticate a repository</span></span>
<span data-ttu-id="7bce0-173">toodownload un contenitore, potrebbe essere repository del contenitore toohello tooprovide credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="7bce0-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="7bce0-174">Hello credenziali di accesso, specificate nel manifesto dell'applicazione hello, vengono utilizzati toospecify hello le informazioni di accesso o una chiave SSH, per il download di immagine contenitore hello dal repository immagini hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="7bce0-175">Hello esempio seguente viene illustrato un account denominato *TestUser* insieme password hello in testo non crittografato (*non* consigliato):</span><span class="sxs-lookup"><span data-stu-id="7bce0-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="7bce0-176">È consigliabile crittografare la password di hello usando un certificato che ha distribuito toohello macchina.</span><span class="sxs-lookup"><span data-stu-id="7bce0-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="7bce0-177">Hello esempio seguente viene illustrato un account denominato *TestUser*, in cui è stata crittografata utilizzando un certificato denominato password hello *NomeCert*.</span><span class="sxs-lookup"><span data-stu-id="7bce0-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="7bce0-178">È possibile utilizzare hello `Invoke-ServiceFabricEncryptText` PowerShell toocreate hello crittografia segreta testo del comando per la password di hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="7bce0-179">Per ulteriori informazioni, vedere l'articolo hello [dei dati segreti nelle applicazioni di Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="7bce0-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="7bce0-180">chiave privata di Hello del certificato di hello utilizzate password hello toodecrypt deve essere distribuito toohello computer locale in un metodo fuori banda.</span><span class="sxs-lookup"><span data-stu-id="7bce0-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="7bce0-181">(In Azure, questo metodo è Azure Resource Manager.) Quindi quando Service Fabric distribuisce computer toohello pacchetto del servizio hello, è possibile decrittografare il segreto hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="7bce0-182">Utilizzando la chiave privata hello insieme al nome account hello, quindi l'autenticazione con repository del contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <span data-ttu-id="7bce0-183"><a name ="Portsection"></a>Configurare i mapping delle porte toohost contenitore</span><span class="sxs-lookup"><span data-stu-id="7bce0-183"><a name ="Portsection"></a> Configure container toohost port mapping</span></span>
<span data-ttu-id="7bce0-184">È possibile configurare toocommunicate di porta usata un host con il contenitore di hello specificando un `PortBinding` nel manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="7bce0-185">Hello porta mappe hello porta toowhich hello servizio di associazione è in ascolto all'interno di hello contenitore tooa porta host hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="7bce0-186">Configurare individuazione e comunicazione da contenitore a contenitore</span><span class="sxs-lookup"><span data-stu-id="7bce0-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="7bce0-187">È possibile utilizzare hello `PortBinding` elemento toomap un endpoint di porta del contenitore tooan nel manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-187">You can use hello `PortBinding` element toomap a container port tooan endpoint in hello service manifest.</span></span> <span data-ttu-id="7bce0-188">Nell'esempio seguente di hello, hello endpoint `Endpoint1` specifica una porta fissa, 8905.</span><span class="sxs-lookup"><span data-stu-id="7bce0-188">In hello following example, hello endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="7bce0-189">Non può inoltre specificare alcuna porta, nel qual caso una porta casuale dall'intervallo di porte di applicazione del cluster hello viene scelto per l'utente.</span><span class="sxs-lookup"><span data-stu-id="7bce0-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
<span data-ttu-id="7bce0-190">Se si specifica un endpoint, utilizzando hello `Endpoint` tag nel manifesto del servizio hello di un contenitore di guest, Service Fabric è possibile pubblicare automaticamente questo toohello endpoint servizio di denominazione.</span><span class="sxs-lookup"><span data-stu-id="7bce0-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="7bce0-191">Altri servizi in esecuzione nel cluster hello in questo modo è in grado di individuare questo contenitore utilizzando le query REST hello per la risoluzione.</span><span class="sxs-lookup"><span data-stu-id="7bce0-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

<span data-ttu-id="7bce0-192">La registrazione con il servizio di denominazione hello, è possibile eseguire contenitore a comunicazione all'interno del contenitore tramite hello [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="7bce0-192">By registering with hello Naming service, you can perform container-to-container communication within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="7bce0-193">La comunicazione viene eseguita, fornendo una porta di attesa di hello proxy inverso http e il nome di hello dei servizi di hello che si desidera toocommunicate con come variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="7bce0-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="7bce0-194">Per ulteriori informazioni, vedere la sezione successiva di hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-194">For more information, see hello next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="7bce0-195">Configurare e impostare variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="7bce0-195">Configure and set environment variables</span></span>
<span data-ttu-id="7bce0-196">Le variabili di ambiente possono essere specificate per ogni pacchetto di codice nel manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-196">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="7bce0-197">Questa funzionalità è disponibile per tutti i servizi, siano essi distribuiti come contenitori, processi o eseguibili guest.</span><span class="sxs-lookup"><span data-stu-id="7bce0-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="7bce0-198">È possibile eseguire l'override di variabile di ambiente, i valori in un'applicazione hello manifesto o specificarli durante la distribuzione come parametri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7bce0-198">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="7bce0-199">Hello frammento XML del manifesto del servizio seguente viene illustrato un esempio di come le variabili di ambiente toospecify per un pacchetto di codice:</span><span class="sxs-lookup"><span data-stu-id="7bce0-199">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

<span data-ttu-id="7bce0-200">Queste variabili di ambiente possono essere sottoposto a override a livello di manifesto dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="7bce0-200">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="7bce0-201">Nell'esempio precedente hello è specificato un valore esplicito per hello `HttpGateway` variabile di ambiente (19000), mentre viene impostato il valore di hello per `BackendServiceName` parametro tramite hello `[BackendSvc]` parametro dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7bce0-201">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="7bce0-202">Queste impostazioni consentono di valore hello toospecify per `BackendServiceName`valore quando si distribuisce un'applicazione hello e non includere un valore fisso nel manifesto di hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-202">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="7bce0-203">Configurare la modalità di isolamento</span><span class="sxs-lookup"><span data-stu-id="7bce0-203">Configure isolation mode</span></span>

<span data-ttu-id="7bce0-204">Windows supporta due modalità di isolamento per i contenitori: la modalità processo e la modalità Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7bce0-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="7bce0-205">In modalità di isolamento hello processo in esecuzione in tutti i contenitori di hello hello stesso host macchina condivisione hello kernel con host hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-205">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="7bce0-206">Con la modalità di isolamento hello Hyper-V, sono isolate tra ogni contenitore di Hyper-V e host contenitore hello kernel hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-206">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="7bce0-207">viene specificata la modalità di isolamento Hello in hello `ContainerHostPolicies` tag nel file manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-207">hello isolation mode is specified in hello `ContainerHostPolicies` tag in hello application manifest file.</span></span>  <span data-ttu-id="7bce0-208">modalità di isolamento Hello che è possibile specificare sono `process`, `hyperv`, e `default`.</span><span class="sxs-lookup"><span data-stu-id="7bce0-208">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="7bce0-209">Hello `default` modalità di isolamento predefinita troppo`process` in Windows Server ospita e il valore predefinito troppo`hyperv` in host Windows 10.</span><span class="sxs-lookup"><span data-stu-id="7bce0-209">hello `default` isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="7bce0-210">Hello frammento di codice seguente viene illustrato come specificare la modalità di isolamento hello nel file manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7bce0-210">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="7bce0-211">Esempi completi per il manifesto dell'applicazione e del servizio</span><span class="sxs-lookup"><span data-stu-id="7bce0-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="7bce0-212">Di seguito è illustrato un manifesto dell'applicazione di esempio:</span><span class="sxs-lookup"><span data-stu-id="7bce0-212">An example application manifest follows:</span></span>

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

<span data-ttu-id="7bce0-213">Di seguito è riportato un esempio di manifesto del servizio (specificato nella precedente manifesto dell'applicazione hello):</span><span class="sxs-lookup"><span data-stu-id="7bce0-213">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a><span data-ttu-id="7bce0-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7bce0-214">Next steps</span></span>
<span data-ttu-id="7bce0-215">Dopo aver distribuito un servizio nei contenitori, consultare come toomanage il ciclo di vita leggendo [il ciclo di vita di Service Fabric applicazione](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="7bce0-215">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="7bce0-216">Panoramica di Service Fabric e contenitori</span><span class="sxs-lookup"><span data-stu-id="7bce0-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="7bce0-217">Per un esempio vedere gli [esempi di codice di contenitore Service Fabric su GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).</span><span class="sxs-lookup"><span data-stu-id="7bce0-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
