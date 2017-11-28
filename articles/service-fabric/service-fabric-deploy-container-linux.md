---
title: aaaService dell'infrastruttura e la distribuzione di contenitori di Linux | Documenti Microsoft
description: "Service Fabric e hello uso di applicazioni microservizio toodeploy contenitori di Linux. Questo articolo descrive le funzionalità di hello forniti per i contenitori e come toodeploy immagine di un contenitore di Linux in un cluster di Service Fabric"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a><span data-ttu-id="7641d-104">Distribuire un tooService contenitore Linux dell'infrastruttura</span><span class="sxs-lookup"><span data-stu-id="7641d-104">Deploy a Linux container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7641d-105">Distribuire un contenitore Windows</span><span class="sxs-lookup"><span data-stu-id="7641d-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="7641d-106">Distribuire un contenitore Linux</span><span class="sxs-lookup"><span data-stu-id="7641d-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="7641d-107">Questo articolo descrive la creazione di servizi in contenitori Docker su Linux.</span><span class="sxs-lookup"><span data-stu-id="7641d-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="7641d-108">Service Fabric offre diverse funzionalità relative ai contenitori che consentono di creare applicazioni costituite da microservizi inseriti in contenitori,</span><span class="sxs-lookup"><span data-stu-id="7641d-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="7641d-109">Questi servizi sono denominati servizi in contenitori.</span><span class="sxs-lookup"><span data-stu-id="7641d-109">These services are called containerized services.</span></span>

<span data-ttu-id="7641d-110">include funzionalità di Hello;</span><span class="sxs-lookup"><span data-stu-id="7641d-110">hello capabilities include;</span></span>

* <span data-ttu-id="7641d-111">Distribuzione e attivazione di immagini contenitore</span><span class="sxs-lookup"><span data-stu-id="7641d-111">Container image deployment and activation</span></span>
* <span data-ttu-id="7641d-112">Governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="7641d-112">Resource governance</span></span>
* <span data-ttu-id="7641d-113">Autenticazione nel repository</span><span class="sxs-lookup"><span data-stu-id="7641d-113">Repository authentication</span></span>
* <span data-ttu-id="7641d-114">Mapping delle porte toohost porta del contenitore</span><span class="sxs-lookup"><span data-stu-id="7641d-114">Container port toohost port mapping</span></span>
* <span data-ttu-id="7641d-115">Individuazione e comunicazione da contenitore a contenitore</span><span class="sxs-lookup"><span data-stu-id="7641d-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="7641d-116">Tooconfigure possibilità e impostare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="7641d-116">Ability tooconfigure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="7641d-117">Creazione del pacchetto di un contenitore Docker con yeoman</span><span class="sxs-lookup"><span data-stu-id="7641d-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="7641d-118">Quando il pacchetto di un contenitore in Linux, è possibile scegliere entrambi toouse un modello yeoman o [creare manualmente il pacchetto di applicazione hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="7641d-118">When packaging a container on Linux, you can choose either toouse a yeoman template or [create hello application package manually](#manually).</span></span>

<span data-ttu-id="7641d-119">Un'applicazione di Service Fabric può contenere uno o più contenitori, ognuno con un ruolo specifico nell'offerta di funzionalità dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="7641d-120">Hello Service Fabric SDK per Linux include un [Yeoman](http://yeoman.io/) generatore che rende facile toocreate l'applicazione e aggiungere un'immagine contenitore.</span><span class="sxs-lookup"><span data-stu-id="7641d-120">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="7641d-121">Consente di usare Yeoman toocreate chiamata un'applicazione con un singolo contenitore Docker *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="7641d-121">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="7641d-122">È possibile aggiungere più servizi in un secondo momento modificando i file manifesto hello generato.</span><span class="sxs-lookup"><span data-stu-id="7641d-122">You can add more services later by editing hello generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="7641d-123">Installare Docker nell'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="7641d-123">Install Docker on your development box</span></span>

<span data-ttu-id="7641d-124">La seguente esecuzione hello comandi docker tooinstall nella casella di sviluppo di Linux (se si utilizza immagine vagrant hello in OSX, docker è già installato):</span><span class="sxs-lookup"><span data-stu-id="7641d-124">Run hello following commands tooinstall docker on your Linux development box (if you are using hello vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a><span data-ttu-id="7641d-125">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="7641d-125">Create hello application</span></span>
1. <span data-ttu-id="7641d-126">In un terminale digitare `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="7641d-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="7641d-127">Assegnare un nome all'applicazione, ad esempio mycontainerap</span><span class="sxs-lookup"><span data-stu-id="7641d-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="7641d-128">Specificare l'URL di hello per l'immagine del contenitore da un repository DockerHub hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-128">Provide hello URL for hello container image from a DockerHub repo.</span></span> <span data-ttu-id="7641d-129">Hello immagine parametro accetta hello modulo [repository] / [nome immagine]</span><span class="sxs-lookup"><span data-stu-id="7641d-129">hello image parameter takes hello form [repo]/[image name]</span></span>
4. <span data-ttu-id="7641d-130">Se hello immagine non ha un punto di ingresso del carico di lavoro definito, quindi è necessario tooexplicitly specificare i comandi di input con un set delimitato da virgole di comandi toorun hello contenitore, in modo che i contenitori di hello in esecuzione dopo l'avvio.</span><span class="sxs-lookup"><span data-stu-id="7641d-130">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

![Generatore Yeoman di Service Fabric per i contenitori][sf-yeoman]

## <a name="deploy-hello-application"></a><span data-ttu-id="7641d-132">Distribuire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="7641d-132">Deploy hello application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="7641d-133">Uso dell'interfaccia della riga di comando di XPlat</span><span class="sxs-lookup"><span data-stu-id="7641d-133">Using XPlat CLI</span></span>
<span data-ttu-id="7641d-134">Una volta creata l'applicazione hello, è possibile distribuire cluster locale di toohello utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="7641d-134">Once hello application is built, you can deploy it toohello local cluster using hello Azure CLI.</span></span>

1. <span data-ttu-id="7641d-135">Connettere il cluster di Service Fabric locale toohello.</span><span class="sxs-lookup"><span data-stu-id="7641d-135">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="7641d-136">Hello utilizzare lo script di installazione fornite in hello modello toocopy applicazione hello pacchetto archivio immagini toohello del cluster, registrare il tipo di applicazione hello e creare un'istanza di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-136">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="7641d-137">Aprire un browser e passare tooService Fabric Explorer in http://localhost:19080/Esplora (sostituire localhost con indirizzo IP privato di hello di hello VM se utilizza Vagrant su Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="7641d-137">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="7641d-138">Espandere il nodo di applicazioni hello e si noti che è ora disponibile una voce per il tipo di applicazione e un altro per hello prima istanza di quel tipo.</span><span class="sxs-lookup"><span data-stu-id="7641d-138">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>
5. <span data-ttu-id="7641d-139">Utilizza script di disinstallazione hello fornito nell'istanza di applicazione hello toodelete modello hello e annullare la registrazione del tipo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-139">Use hello uninstall script provided in hello template toodelete hello application instance and unregister hello application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="7641d-140">Tramite l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="7641d-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="7641d-141">Vedere il documento di riferimento hello sulla gestione di un [con ciclo di vita dell'applicazione hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="7641d-141">See hello reference doc on managing an [application life cycle using hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="7641d-142">Per un'applicazione di esempio, [hello estrazione codice contenitore Service Fabric esempi su GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="7641d-142">For an example application, [checkout hello Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="7641d-143">Aggiunta di ulteriori servizi tooan esistente dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="7641d-143">Adding more services tooan existing application</span></span>

<span data-ttu-id="7641d-144">tooadd un altro contenitore del servizio applicazione tooan già creato utilizzando `yo`, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7641d-144">tooadd another container service tooan application already created using `yo`, perform hello following steps:</span></span>

1. <span data-ttu-id="7641d-145">Cambiare directory toohello principale di un'applicazione hello esistente.</span><span class="sxs-lookup"><span data-stu-id="7641d-145">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="7641d-146">Ad esempio, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` è un'applicazione hello creata da Yeoman.</span><span class="sxs-lookup"><span data-stu-id="7641d-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="7641d-147">Eseguire `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="7641d-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="7641d-148">Creare manualmente il pacchetto e distribuire un'immagine del contenitore</span><span class="sxs-lookup"><span data-stu-id="7641d-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="7641d-149">il processo di Hello di creare manualmente il pacchetto del servizio nei contenitori si basa su hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7641d-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="7641d-150">Pubblicare hello contenitori tooyour repository.</span><span class="sxs-lookup"><span data-stu-id="7641d-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="7641d-151">Creare una struttura di directory hello del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="7641d-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="7641d-152">Modificare i file manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="7641d-153">Modificare i file manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="7641d-154">Distribuire e attivare un'immagine contenitore</span><span class="sxs-lookup"><span data-stu-id="7641d-154">Deploy and activate a container image</span></span>
<span data-ttu-id="7641d-155">In Service Fabric hello [modello applicativo](service-fabric-application-model.md), un contenitore rappresenta un'applicazione host nel quale servizio più repliche vengono inserite.</span><span class="sxs-lookup"><span data-stu-id="7641d-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="7641d-156">toodeploy e attivare un contenitore, un nome di hello put dell'immagine contenitore hello in un `ContainerHost` elemento nel manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="7641d-157">Nel manifesto del servizio hello, aggiungere un `ContainerHost` per il punto di ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="7641d-158">Quindi set hello `ImageName` nome hello toobe del repository del contenitore hello e dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="7641d-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="7641d-159">Hello manifesto parziale seguente viene illustrato un esempio di come contenitore hello toodeploy chiamata `myimage:v1` da un repository denominato `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="7641d-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="7641d-160">È possibile specificare i comandi di input specificando hello facoltativo `Commands` elemento con un set delimitato da virgole di comandi toorun hello contenitore.</span><span class="sxs-lookup"><span data-stu-id="7641d-160">You can provide input commands by specifying hello optional `Commands` element with a comma-delimited set of commands toorun inside hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="7641d-161">Se hello immagine non ha un punto di ingresso del carico di lavoro definito, quindi è necessario tooexplicitly specificare i comandi di input all'interno di `Commands` elemento con un set delimitato da virgole di comandi toorun hello contenitore, in modo che i contenitori di hello in esecuzione avvio.</span><span class="sxs-lookup"><span data-stu-id="7641d-161">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands inside `Commands` element with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="7641d-162">Informazioni sulla governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="7641d-162">Understand resource governance</span></span>
<span data-ttu-id="7641d-163">Governance delle risorse è possibile utilizzare una funzionalità di contenitore hello che limita le risorse hello hello contenitore nell'host di hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="7641d-164">Hello `ResourceGovernancePolicy`, ed è specificato nel manifesto dell'applicazione hello è toodeclare utilizzati i limiti delle risorse per un pacchetto di codice servizio.</span><span class="sxs-lookup"><span data-stu-id="7641d-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="7641d-165">È possibile impostare i limiti delle risorse per hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="7641d-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="7641d-166">Memoria</span><span class="sxs-lookup"><span data-stu-id="7641d-166">Memory</span></span>
* <span data-ttu-id="7641d-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="7641d-167">MemorySwap</span></span>
* <span data-ttu-id="7641d-168">CpuShares (peso relativo CPU)</span><span class="sxs-lookup"><span data-stu-id="7641d-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="7641d-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="7641d-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="7641d-170">BlkioWeight (peso relativo BlockIO)</span><span class="sxs-lookup"><span data-stu-id="7641d-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="7641d-171">In una versione futura sarà incluso il supporto della definizione di specifici limiti di I/O di blocco, come operazioni di I/O al secondo, BPS in lettura/scrittura e altri.</span><span class="sxs-lookup"><span data-stu-id="7641d-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="7641d-172">Autenticare un repository</span><span class="sxs-lookup"><span data-stu-id="7641d-172">Authenticate a repository</span></span>
<span data-ttu-id="7641d-173">toodownload un contenitore, potrebbe essere repository del contenitore toohello tooprovide credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="7641d-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="7641d-174">Hello credenziali di accesso, specificate nel manifesto dell'applicazione hello, vengono utilizzati toospecify hello le informazioni di accesso o una chiave SSH, per il download di immagine contenitore hello dal repository immagini hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="7641d-175">Hello esempio seguente viene illustrato un account denominato *TestUser* insieme password hello in testo non crittografato (*non* consigliato):</span><span class="sxs-lookup"><span data-stu-id="7641d-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="7641d-176">È consigliabile crittografare la password di hello usando un certificato che ha distribuito toohello macchina.</span><span class="sxs-lookup"><span data-stu-id="7641d-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="7641d-177">Hello esempio seguente viene illustrato un account denominato *TestUser*, in cui è stata crittografata utilizzando un certificato denominato password hello *NomeCert*.</span><span class="sxs-lookup"><span data-stu-id="7641d-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="7641d-178">È possibile utilizzare hello `Invoke-ServiceFabricEncryptText` PowerShell toocreate hello crittografia segreta testo del comando per la password di hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="7641d-179">Per ulteriori informazioni, vedere l'articolo hello [dei dati segreti nelle applicazioni di Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="7641d-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="7641d-180">chiave privata di Hello del certificato di hello utilizzate password hello toodecrypt deve essere distribuito toohello computer locale in un metodo fuori banda.</span><span class="sxs-lookup"><span data-stu-id="7641d-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="7641d-181">(In Azure, questo metodo è Azure Resource Manager.) Quindi quando Service Fabric distribuisce computer toohello pacchetto del servizio hello, è possibile decrittografare il segreto hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="7641d-182">Utilizzando la chiave privata hello insieme al nome account hello, quindi l'autenticazione con repository del contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="7641d-183">Configurare il mapping tra porta del contenitore e porta dell'host</span><span class="sxs-lookup"><span data-stu-id="7641d-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="7641d-184">È possibile configurare toocommunicate di porta usata un host con il contenitore di hello specificando un `PortBinding` nel manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="7641d-185">Hello porta mappe hello porta toowhich hello servizio di associazione è in ascolto all'interno di hello contenitore tooa porta host hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="7641d-186">Configurare individuazione e comunicazione da contenitore a contenitore</span><span class="sxs-lookup"><span data-stu-id="7641d-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="7641d-187">Utilizzando hello `PortBinding` criteri, è possibile mappare una porta del contenitore di tooan `Endpoint` nel manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-187">By using hello `PortBinding` policy, you can map a container port tooan `Endpoint` in hello service manifest.</span></span> <span data-ttu-id="7641d-188">Hello endpoint `Endpoint1` possibile specificare una porta fissa (ad esempio, la porta 80).</span><span class="sxs-lookup"><span data-stu-id="7641d-188">hello endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="7641d-189">Non può inoltre specificare alcuna porta, nel qual caso una porta casuale dall'intervallo di porte di applicazione del cluster hello viene scelto per l'utente.</span><span class="sxs-lookup"><span data-stu-id="7641d-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="7641d-190">Se si specifica un endpoint, utilizzando hello `Endpoint` tag nel manifesto del servizio hello di un contenitore di guest, Service Fabric è possibile pubblicare automaticamente questo toohello endpoint servizio di denominazione.</span><span class="sxs-lookup"><span data-stu-id="7641d-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="7641d-191">Altri servizi in esecuzione nel cluster hello in questo modo è in grado di individuare questo contenitore utilizzando le query REST hello per la risoluzione.</span><span class="sxs-lookup"><span data-stu-id="7641d-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

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

<span data-ttu-id="7641d-192">La registrazione con il servizio di denominazione hello, è possibile utilizzare comunicazione di contenitore a nel codice hello all'interno del contenitore tramite hello [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="7641d-192">By registering with hello Naming service, you can easily do container-to-container communication in hello code within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="7641d-193">La comunicazione viene eseguita, fornendo una porta di attesa di hello proxy inverso http e il nome di hello dei servizi di hello che si desidera toocommunicate con come variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="7641d-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="7641d-194">Per ulteriori informazioni, vedere la sezione successiva di hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-194">For more information, see hello next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="7641d-195">Configurare e impostare variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="7641d-195">Configure and set environment variables</span></span>
<span data-ttu-id="7641d-196">Le variabili di ambiente possono essere specificate per ogni pacchetto di codice nel manifesto del servizio hello, sia per i servizi che vengono distribuiti in contenitori o per i servizi che vengono distribuiti i file eseguibili di processi/guest.</span><span class="sxs-lookup"><span data-stu-id="7641d-196">Environment variables can be specified for each code package in hello service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="7641d-197">Questi valori di variabile di ambiente possono essere sottoposto a override in modo specifico nel manifesto dell'applicazione hello o specificati durante la distribuzione come parametri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7641d-197">These environment variable values can be overridden specifically in hello application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="7641d-198">Hello frammento XML del manifesto del servizio seguente viene illustrato un esempio di come le variabili di ambiente toospecify per un pacchetto di codice:</span><span class="sxs-lookup"><span data-stu-id="7641d-198">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

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

<span data-ttu-id="7641d-199">Queste variabili di ambiente possono essere sottoposto a override a livello di manifesto dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="7641d-199">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="7641d-200">Nell'esempio precedente hello è specificato un valore esplicito per hello `HttpGateway` variabile di ambiente (19000), mentre viene impostato il valore di hello per `BackendServiceName` parametro tramite hello `[BackendSvc]` parametro dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7641d-200">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="7641d-201">Queste impostazioni consentono di valore hello toospecify per `BackendServiceName`valore quando si distribuisce un'applicazione hello e non includere un valore fisso nel manifesto di hello.</span><span class="sxs-lookup"><span data-stu-id="7641d-201">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="7641d-202">Esempi completi per il manifesto dell'applicazione e del servizio</span><span class="sxs-lookup"><span data-stu-id="7641d-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="7641d-203">Di seguito è illustrato un manifesto dell'applicazione di esempio:</span><span class="sxs-lookup"><span data-stu-id="7641d-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="7641d-204">Di seguito è riportato un esempio di manifesto del servizio (specificato nella precedente manifesto dell'applicazione hello):</span><span class="sxs-lookup"><span data-stu-id="7641d-204">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7641d-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7641d-205">Next steps</span></span>
<span data-ttu-id="7641d-206">Dopo aver distribuito un servizio nei contenitori, consultare come toomanage il ciclo di vita leggendo [il ciclo di vita di Service Fabric applicazione](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="7641d-206">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="7641d-207">Panoramica di Service Fabric e contenitori</span><span class="sxs-lookup"><span data-stu-id="7641d-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="7641d-208">L'interazione con i cluster di Service Fabric usando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="7641d-208">Interacting with Service Fabric clusters using hello Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="7641d-209">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="7641d-209">Related articles</span></span>

* [<span data-ttu-id="7641d-210">Introduzione a Service Fabric e all'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="7641d-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="7641d-211">Introduzione all'interfaccia della riga di comando di XPlat per Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7641d-211">Getting started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
