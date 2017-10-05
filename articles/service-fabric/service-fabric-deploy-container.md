---
title: Service Fabric e distribuzione di contenitori | Microsoft Docs
description: "Service Fabric e l'uso di contenitori per la distribuzione di applicazioni di microservizi. Questo articolo illustra le funzionalità offerte da Service Fabric per i contenitori e la modalità di distribuzione di un'immagine contenitore Windows in un cluster."
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
ms.openlocfilehash: 25d6b056421e71fa70ed20a39589f77dbbc25c69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-windows-container-to-service-fabric"></a><span data-ttu-id="38e14-104">Distribuire un contenitore Windows in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="38e14-104">Deploy a Windows container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38e14-105">Distribuire un contenitore Windows</span><span class="sxs-lookup"><span data-stu-id="38e14-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="38e14-106">Distribuire un contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="38e14-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="38e14-107">Questo articolo descrive in dettaglio il processo di creazione di servizi in contenitori Windows.</span><span class="sxs-lookup"><span data-stu-id="38e14-107">This article walks you through the process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="38e14-108">Service Fabric offre diverse funzionalità che consentono di creare applicazioni costituite da microservizi eseguiti in contenitori.</span><span class="sxs-lookup"><span data-stu-id="38e14-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="38e14-109">Le funzionalità includono:</span><span class="sxs-lookup"><span data-stu-id="38e14-109">The capabilities include:</span></span>

* <span data-ttu-id="38e14-110">Distribuzione e attivazione di immagini contenitore</span><span class="sxs-lookup"><span data-stu-id="38e14-110">Container image deployment and activation</span></span>
* <span data-ttu-id="38e14-111">Governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="38e14-111">Resource governance</span></span>
* <span data-ttu-id="38e14-112">Autenticazione nel repository</span><span class="sxs-lookup"><span data-stu-id="38e14-112">Repository authentication</span></span>
* <span data-ttu-id="38e14-113">Mapping tra porta del contenitore e porta dell'host</span><span class="sxs-lookup"><span data-stu-id="38e14-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="38e14-114">Individuazione e comunicazione da contenitore a contenitore</span><span class="sxs-lookup"><span data-stu-id="38e14-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="38e14-115">Possibilità di configurare e impostare variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="38e14-115">Ability to configure and set environment variables</span></span>

<span data-ttu-id="38e14-116">Verranno ora esaminate le singole funzionalità coinvolte nella creazione del pacchetto di un servizio in contenitori da includere nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38e14-116">Let's look at how each of capabilities works when you're packaging a containerized service to be included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="38e14-117">Creare il pacchetto di un contenitore Windows</span><span class="sxs-lookup"><span data-stu-id="38e14-117">Package a Windows container</span></span>
<span data-ttu-id="38e14-118">Quando si crea il pacchetto di un contenitore, si può scegliere di usare un modello di progetto di Visual Studio oppure di [creare manualmente il pacchetto dell'applicazione](#manually).</span><span class="sxs-lookup"><span data-stu-id="38e14-118">When you package a container, you can choose to use either a Visual Studio project template or [create the application package manually](#manually).</span></span>  <span data-ttu-id="38e14-119">Se si usa Visual Studio, la struttura del pacchetto dell'applicazione e i file manifesto vengono creati automaticamente dal modello Nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="38e14-119">When you use Visual Studio, the application package structure and manifest files are created by the New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="38e14-120">Il modo più semplice per creare il pacchetto di un'immagine contenitore esistente in un servizio consiste nell'usare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38e14-120">The easiest way to package an existing container image into a service is to use Visual Studio.</span></span>

## <a name="use-visual-studio-to-package-an-existing-container-image"></a><span data-ttu-id="38e14-121">Usare Visual Studio per creare il pacchetto di un'immagine contenitore esistente</span><span class="sxs-lookup"><span data-stu-id="38e14-121">Use Visual Studio to package an existing container image</span></span>
<span data-ttu-id="38e14-122">Visual Studio include un modello di servizio Service Fabric che consente di distribuire un contenitore in un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="38e14-122">Visual Studio provides a Service Fabric service template to help you deploy a container to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="38e14-123">Scegliere **File** > **Nuovo progetto** e creare un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="38e14-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="38e14-124">Scegliere **Guest Container (Contenitore guest)** come modello del servizio.</span><span class="sxs-lookup"><span data-stu-id="38e14-124">Choose **Guest Container** as the service template.</span></span>
3. <span data-ttu-id="38e14-125">Scegliere **Nome immagine** e specificare il percorso dell'immagine nell'archivio del contenitore.</span><span class="sxs-lookup"><span data-stu-id="38e14-125">Choose **Image Name** and provide the path to the image in your container repository.</span></span> <span data-ttu-id="38e14-126">Ad esempio `myrepo/myimage:v1` in https://hub.docker.com</span><span class="sxs-lookup"><span data-stu-id="38e14-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="38e14-127">Assegnare un nome al servizio e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="38e14-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="38e14-128">Se il servizio nel contenitore richiede un endpoint per la comunicazione, è ora possibile aggiungere il protocollo, la porta e il tipo al file ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="38e14-128">If your containerized service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="38e14-129">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="38e14-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="38e14-130">Se si specifica `UriScheme` Service Fabric registra automaticamente l'endpoint del contenitore con Naming Service per l'individuazione.</span><span class="sxs-lookup"><span data-stu-id="38e14-130">By providing the `UriScheme`, Service Fabric automatically registers the container endpoint with the Naming service for discoverability.</span></span> <span data-ttu-id="38e14-131">La porta può essere fissa (come nell'esempio precedente) o allocata in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="38e14-131">The port can either be fixed (as shown in the preceding example) or dynamically allocated.</span></span> <span data-ttu-id="38e14-132">Se non si specifica una porta, questa viene allocata in modo dinamico nell'intervallo di porte dell'applicazione (come per qualsiasi servizio).</span><span class="sxs-lookup"><span data-stu-id="38e14-132">If you don't specify a port, it is dynamically allocated from the application port range (as would happen with any service).</span></span>
    <span data-ttu-id="38e14-133">È anche necessario configurare il mapping tra contenitore e porta dell'host specificando una norma `PortBinding` nel manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38e14-133">You also need to configure the container to host port mapping by specifying a `PortBinding` policy in the application manifest.</span></span> <span data-ttu-id="38e14-134">Per altre informazioni, vedere [Configurare il mapping tra porta del contenitore e porta dell'host](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="38e14-134">For more information, see [Configure container to host port mapping](#Portsection).</span></span>
6. <span data-ttu-id="38e14-135">Se per il contenitore è necessaria una governance delle risorse, aggiungere un elemento `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="38e14-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="38e14-136">Se il contenitore deve eseguire l'autenticazione con un repository privato, aggiungere `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="38e14-136">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="38e14-137">Se si usa un computer Windows Server 2016 con il supporto dei contenitori abilitato è possibile usare l'azione di creazione pacchetto e pubblicazione per la distribuzione nel cluster locale.</span><span class="sxs-lookup"><span data-stu-id="38e14-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use the package and publish action to deploy to your local cluster.</span></span> 
8. <span data-ttu-id="38e14-138">Quando si è pronti, pubblicare l'applicazione in un cluster remoto o archiviare la soluzione nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="38e14-138">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span> 

<span data-ttu-id="38e14-139">Per un esempio vedere gli [esempi di codice di contenitore Service Fabric su GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).</span><span class="sxs-lookup"><span data-stu-id="38e14-139">For an example, checkout the [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="38e14-140">Creazione di un cluster di Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="38e14-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="38e14-141">Per distribuire l'applicazione nei contenitori, è necessario creare un cluster che esegue Windows Server 2016 con il supporto di contenitore abilitato.</span><span class="sxs-lookup"><span data-stu-id="38e14-141">To deploy your containerized application, you need to create a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="38e14-142">Il cluster può essere eseguito localmente o distribuito con Azure Resource Manager in Azure.</span><span class="sxs-lookup"><span data-stu-id="38e14-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="38e14-143">Per distribuire un cluster con Azure Resource Manager scegliere l'opzione di immagine **Windows Server 2016 with Containers** (Windows Server 2016 con contenitori) in Azure.</span><span class="sxs-lookup"><span data-stu-id="38e14-143">To deploy a cluster using Azure Resource Manager, choose the **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="38e14-144">Vedere l'articolo [Creare un cluster di Service Fabric usando Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="38e14-144">See the article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="38e14-145">Assicurarsi di usare le seguenti impostazioni di Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="38e14-145">Ensure that you use the following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="38e14-146">Per creare un cluster è anche possibile usare il [modello di Azure Resource Manager con cinque nodi](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="38e14-146">You can also use the [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) to create a cluster.</span></span> <span data-ttu-id="38e14-147">In alternativa è consigliabile leggere un [post di blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) della community sull'uso di Service Fabric e dei contenitori di Windows.</span><span class="sxs-lookup"><span data-stu-id="38e14-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="38e14-148">Creare manualmente il pacchetto e distribuire un'immagine del contenitore</span><span class="sxs-lookup"><span data-stu-id="38e14-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="38e14-149">Il processo per creare manualmente il pacchetto di un servizio in contenitore prevede i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="38e14-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="38e14-150">Pubblicare i contenitori nel repository.</span><span class="sxs-lookup"><span data-stu-id="38e14-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="38e14-151">Creare la struttura di directory del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="38e14-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="38e14-152">Modificare il file manifesto del servizio.</span><span class="sxs-lookup"><span data-stu-id="38e14-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="38e14-153">Modificare il file manifesto dell’applicazione.</span><span class="sxs-lookup"><span data-stu-id="38e14-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="38e14-154">Distribuire e attivare un'immagine contenitore</span><span class="sxs-lookup"><span data-stu-id="38e14-154">Deploy and activate a container image</span></span>
<span data-ttu-id="38e14-155">Nel [modello applicativo](service-fabric-application-model.md)di Service Fabric, un contenitore rappresenta un host applicazione in cui sono inserite più repliche dei servizi.</span><span class="sxs-lookup"><span data-stu-id="38e14-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="38e14-156">Per distribuire e attivare un contenitore, inserire il nome dell'immagine contenitore in un elemento `ContainerHost` nel manifesto del servizio.</span><span class="sxs-lookup"><span data-stu-id="38e14-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="38e14-157">Nel manifesto del servizio aggiungere un `ContainerHost` per il punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="38e14-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="38e14-158">Impostare quindi il nome dell'immagine e del repository del contenitore in `ImageName`.</span><span class="sxs-lookup"><span data-stu-id="38e14-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="38e14-159">Il manifesto parziale seguente mostra un esempio di come distribuire il contenitore denominato `myimage:v1` da un repository denominato `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="38e14-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="38e14-160">È possibile specificare i comandi facoltativi da eseguire all'avvio del contenitore all'interno dell'elemento `Commands`.</span><span class="sxs-lookup"><span data-stu-id="38e14-160">You can specify optional commands to run upon starting the container under the `Commands` element.</span></span> <span data-ttu-id="38e14-161">Per aggiungere più comandi, separarli con virgole.</span><span class="sxs-lookup"><span data-stu-id="38e14-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="38e14-162">Informazioni sulla governance delle risorse</span><span class="sxs-lookup"><span data-stu-id="38e14-162">Understand resource governance</span></span>
<span data-ttu-id="38e14-163">La governance delle risorse è una funzionalità del contenitore che limita le risorse che possono essere usate dal contenitore nell'host.</span><span class="sxs-lookup"><span data-stu-id="38e14-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="38e14-164">L'impostazione `ResourceGovernancePolicy`, specificata nel manifesto dell'applicazione, viene usata per dichiarare limiti di risorse per il pacchetto di codice di un servizio.</span><span class="sxs-lookup"><span data-stu-id="38e14-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="38e14-165">È possibile impostare limiti per le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="38e14-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="38e14-166">Memoria</span><span class="sxs-lookup"><span data-stu-id="38e14-166">Memory</span></span>
* <span data-ttu-id="38e14-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="38e14-167">MemorySwap</span></span>
* <span data-ttu-id="38e14-168">CpuShares (peso relativo CPU)</span><span class="sxs-lookup"><span data-stu-id="38e14-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="38e14-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="38e14-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="38e14-170">BlkioWeight (peso relativo BlockIO)</span><span class="sxs-lookup"><span data-stu-id="38e14-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="38e14-171">Il supporto per la definizione di limiti di I/O di blocco specifici, come operazioni di I/O al secondo, BPS in lettura/scrittura e altro, è previsto per una versione futura.</span><span class="sxs-lookup"><span data-stu-id="38e14-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="38e14-172">Autenticare un repository</span><span class="sxs-lookup"><span data-stu-id="38e14-172">Authenticate a repository</span></span>
<span data-ttu-id="38e14-173">Per scaricare un contenitore potrebbe essere necessario specificare credenziali di accesso per il relativo repository.</span><span class="sxs-lookup"><span data-stu-id="38e14-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="38e14-174">Le credenziali di accesso, specificate nel manifesto dell'applicazione, vengono usate per specificare le informazioni di accesso o la chiave SSH per scaricare l'immagine contenitore dal repository delle immagini.</span><span class="sxs-lookup"><span data-stu-id="38e14-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="38e14-175">L'esempio seguente illustra un account denominato *TestUser* con password non crittografata (scenario *non* consigliato):</span><span class="sxs-lookup"><span data-stu-id="38e14-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="38e14-176">È consigliabile crittografare la password con un certificato distribuito nel computer.</span><span class="sxs-lookup"><span data-stu-id="38e14-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="38e14-177">L'esempio seguente illustra un account denominato *TestUser* con password crittografata con un certificato denominato *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="38e14-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="38e14-178">È possibile usare il comando `Invoke-ServiceFabricEncryptText` di PowerShell per creare il testo crittografato segreto per la password.</span><span class="sxs-lookup"><span data-stu-id="38e14-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="38e14-179">Per altre informazioni, vedere [Gestione dei segreti nelle applicazioni di Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="38e14-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="38e14-180">La chiave privata del certificato usata per decrittografare la password deve essere distribuita nel computer locale con un metodo fuori banda.</span><span class="sxs-lookup"><span data-stu-id="38e14-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="38e14-181">(In Azure, questo metodo è Azure Resource Manager.) Quando Service Fabric distribuisce il pacchetto del servizio nel computer, potrà quindi decrittografare il segreto.</span><span class="sxs-lookup"><span data-stu-id="38e14-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="38e14-182">Usando il segreto insieme al nome dell'account, potrà quindi eseguire l'autenticazione nel repository del contenitore.</span><span class="sxs-lookup"><span data-stu-id="38e14-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <span data-ttu-id="38e14-183"><a name ="Portsection"></a> Configurare il mapping tra contenitore e porta dell'host</span><span class="sxs-lookup"><span data-stu-id="38e14-183"><a name ="Portsection"></a> Configure container to host port mapping</span></span>
<span data-ttu-id="38e14-184">È possibile configurare una porta dell'host per la comunicazione con il contenitore specificando `PortBinding` nel manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38e14-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="38e14-185">Il binding di porta esegue il mapping tra la porta su cui il servizio è in ascolto all'interno del contenitore e una porta nell'host.</span><span class="sxs-lookup"><span data-stu-id="38e14-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="38e14-186">Configurare individuazione e comunicazione da contenitore a contenitore</span><span class="sxs-lookup"><span data-stu-id="38e14-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="38e14-187">È possibile usare l'elemento `PortBinding` per eseguire il mapping di una porta del contenitore a un endpoint nel manifesto del servizio.</span><span class="sxs-lookup"><span data-stu-id="38e14-187">You can use the `PortBinding` element to map a container port to an endpoint in the service manifest.</span></span> <span data-ttu-id="38e14-188">Nell'esempio seguente l'endpoint `Endpoint1` specifica la porta fissa 8905.</span><span class="sxs-lookup"><span data-stu-id="38e14-188">In the following example, the endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="38e14-189">oppure non specificarne alcuna. Nel secondo caso verrà scelta automaticamente una porta casuale nell'intervallo di porte dell'applicazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="38e14-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="38e14-190">Se si specifica un endpoint, usando il tag `Endpoint` nel manifesto del servizio di un contenitore guest, Service Fabric può pubblicare automaticamente questo endpoint per Naming Service.</span><span class="sxs-lookup"><span data-stu-id="38e14-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="38e14-191">Altri servizi in esecuzione nel cluster possono così individuare questo contenitore usando query REST per la risoluzione.</span><span class="sxs-lookup"><span data-stu-id="38e14-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

<span data-ttu-id="38e14-192">Eseguendo la registrazione in Naming Service è possibile implementare la comunicazione tra contenitori all'interno del contenitore usando il [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="38e14-192">By registering with the Naming service, you can perform container-to-container communication within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="38e14-193">La comunicazione avviene specificando la porta di ascolto HTTP del proxy inverso e il nome dei servizi con cui si vuole comunicare come variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="38e14-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="38e14-194">Per altre informazioni, vedere la sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="38e14-194">For more information, see the next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="38e14-195">Configurare e impostare variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="38e14-195">Configure and set environment variables</span></span>
<span data-ttu-id="38e14-196">È possibile specificare variabili di ambiente per ogni pacchetto di codice nel manifesto del servizio.</span><span class="sxs-lookup"><span data-stu-id="38e14-196">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="38e14-197">Questa funzionalità è disponibile per tutti i servizi, siano essi distribuiti come contenitori, processi o eseguibili guest.</span><span class="sxs-lookup"><span data-stu-id="38e14-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="38e14-198">È possibile sostituire i valori delle variabili di ambiente nel manifesto dell'applicazione oppure specificarli durante la distribuzione come parametri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38e14-198">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="38e14-199">Il frammento XML del manifesto del servizio seguente offre un esempio di come specificare le variabili di ambiente per un pacchetto di codice:</span><span class="sxs-lookup"><span data-stu-id="38e14-199">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="38e14-200">È possibile eseguire l'override di queste variabili di ambiente a livello di manifesto dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="38e14-200">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="38e14-201">Nell'esempio precedente è stato specificato un valore esplicito per la variabile di ambiente `HttpGateway` (19000), mentre il valore per il parametro `BackendServiceName` viene impostato tramite il parametro dell'applicazione `[BackendSvc]`.</span><span class="sxs-lookup"><span data-stu-id="38e14-201">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="38e14-202">Queste impostazioni consentono di specificare il valore per `BackendServiceName` quando si distribuisce l'applicazione anziché avere un valore fisso nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="38e14-202">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="38e14-203">Configurare la modalità di isolamento</span><span class="sxs-lookup"><span data-stu-id="38e14-203">Configure isolation mode</span></span>

<span data-ttu-id="38e14-204">Windows supporta due modalità di isolamento per i contenitori: la modalità processo e la modalità Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="38e14-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="38e14-205">Nella modalità di isolamento del processo tutti i contenitori in esecuzione nello stesso computer host condividono il kernel con l'host.</span><span class="sxs-lookup"><span data-stu-id="38e14-205">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="38e14-206">Nella modalità di isolamento Hyper-V i kernel sono isolati tra i singoli contenitori Hyper-V e il contenitore host.</span><span class="sxs-lookup"><span data-stu-id="38e14-206">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="38e14-207">La modalità di isolamento è specificata nel tag `ContainerHostPolicies` nel file manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38e14-207">The isolation mode is specified in the `ContainerHostPolicies` tag in the application manifest file.</span></span>  <span data-ttu-id="38e14-208">Le modalità di isolamento specificabili sono `process`, `hyperv` e `default`.</span><span class="sxs-lookup"><span data-stu-id="38e14-208">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="38e14-209">La modalità di isolamento `default` assume come impostazione predefinita `process` negli host Windows Server e `hyperv` negli host Windows 10.</span><span class="sxs-lookup"><span data-stu-id="38e14-209">The `default` isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="38e14-210">Il frammento seguente indica come è specificata la modalità di isolamento nel file manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="38e14-210">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="38e14-211">Esempi completi per il manifesto dell'applicazione e del servizio</span><span class="sxs-lookup"><span data-stu-id="38e14-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="38e14-212">Di seguito è illustrato un manifesto dell'applicazione di esempio:</span><span class="sxs-lookup"><span data-stu-id="38e14-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="38e14-213">Di seguito è riportato un manifesto del servizio di esempio (specificato nel manifesto dell'applicazione precedente):</span><span class="sxs-lookup"><span data-stu-id="38e14-213">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="38e14-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38e14-214">Next steps</span></span>
<span data-ttu-id="38e14-215">Ora che è stato distribuito un servizio in contenitori, vedere [Ciclo di vita dell'applicazione Service Fabric](service-fabric-application-lifecycle.md) per informazioni su come gestire il ciclo di vita del servizio.</span><span class="sxs-lookup"><span data-stu-id="38e14-215">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="38e14-216">Panoramica di Service Fabric e contenitori</span><span class="sxs-lookup"><span data-stu-id="38e14-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="38e14-217">Per un esempio vedere gli [esempi di codice di contenitore Service Fabric su GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).</span><span class="sxs-lookup"><span data-stu-id="38e14-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
