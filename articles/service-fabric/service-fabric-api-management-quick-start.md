---
title: aaaAzure Service Fabric con avvio rapido di gestione API | Documenti Microsoft
description: "Questa guida viene spiegato come tooquickly può iniziare con l'API di gestione e Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="4d31d-103">Avvio rapido di Service Fabric con Gestione API</span><span class="sxs-lookup"><span data-stu-id="4d31d-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="4d31d-104">Questa guida viene spiegato come tooset gestione API di Azure con Service Fabric e configurare i primi API operazione toosend traffico tooback-end servizi nell'infrastruttura del servizio.</span><span class="sxs-lookup"><span data-stu-id="4d31d-104">This guide shows you how tooset up Azure API Management with Service Fabric and configure your first API operation toosend traffic tooback-end services in Service Fabric.</span></span> <span data-ttu-id="4d31d-105">toolearn più sugli scenari di gestione API di Azure con Service Fabric, vedere hello [Panoramica](service-fabric-api-management-overview.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="4d31d-105">toolearn more about Azure API Management scenarios with Service Fabric, see hello [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a><span data-ttu-id="4d31d-106">Distribuire l'API di gestione e infrastruttura a servizio tooAzure</span><span class="sxs-lookup"><span data-stu-id="4d31d-106">Deploy API Management and Service Fabric tooAzure</span></span>

<span data-ttu-id="4d31d-107">primo passaggio Hello è toodeploy gestione API e un tooAzure di cluster di Service Fabric in una rete virtuale condivisa.</span><span class="sxs-lookup"><span data-stu-id="4d31d-107">hello first step is toodeploy API Management and a Service Fabric cluster tooAzure in a shared Virtual Network.</span></span> <span data-ttu-id="4d31d-108">In questo modo toocommunicate gestione API direttamente con Service Fabric modo da poter eseguire l'individuazione del servizio, la risoluzione della partizione del servizio e inoltrare il traffico direttamente il servizio back-end tooany Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4d31d-108">This allows API Management toocommunicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly tooany backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="4d31d-109">Topologia</span><span class="sxs-lookup"><span data-stu-id="4d31d-109">Topology</span></span>

<span data-ttu-id="4d31d-110">Questa Guida consente di distribuire seguente hello tooAzure topologia in cui gestione API e infrastruttura a servizio presenti in subnet di hello stessa rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="4d31d-110">This guide deploys hello following topology tooAzure in which API Management and Service Fabric are in subnets of hello same Virtual Network:</span></span>

 ![Sottotitolo immagine][sf-apim-topology-overview]

<span data-ttu-id="4d31d-112">tooget iniziare rapidamente, sono disponibili modelli di gestione risorse per ogni passaggio di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="4d31d-112">tooget started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="4d31d-113">Topologia di rete:</span><span class="sxs-lookup"><span data-stu-id="4d31d-113">Network topology:</span></span>
    - <span data-ttu-id="4d31d-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="4d31d-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="4d31d-116">Cluster di Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="4d31d-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="4d31d-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="4d31d-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="4d31d-119">Gestione API:</span><span class="sxs-lookup"><span data-stu-id="4d31d-119">API Management:</span></span>
    - <span data-ttu-id="4d31d-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="4d31d-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-tooazure-and-select-your-subscription"></a><span data-ttu-id="4d31d-122">Accedi tooAzure e selezionare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="4d31d-122">Sign in tooAzure and select your subscription</span></span>

<span data-ttu-id="4d31d-123">Questa guida usa [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="4d31d-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="4d31d-124">Quando si avvia una nuova sessione PowerShell, accedi tooyour account Azure e selezionare la sottoscrizione prima di eseguire i comandi di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d31d-124">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="4d31d-125">Accedi tooyour account di Azure:</span><span class="sxs-lookup"><span data-stu-id="4d31d-125">Sign in tooyour Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="4d31d-126">Selezionare la propria sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="4d31d-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="4d31d-127">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="4d31d-127">Create a resource group</span></span>

<span data-ttu-id="4d31d-128">Creare un nuovo gruppo di risorse per la propria distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4d31d-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="4d31d-129">Assegnargli un nome e una posizione.</span><span class="sxs-lookup"><span data-stu-id="4d31d-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a><span data-ttu-id="4d31d-130">Distribuire la topologia di rete hello</span><span class="sxs-lookup"><span data-stu-id="4d31d-130">Deploy hello network topology</span></span>

<span data-ttu-id="4d31d-131">primo passaggio Hello è tooset backup toowhich topologia di rete hello gestione API e verrà distribuito il cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-131">hello first step is tooset up hello network topology toowhich API Management and hello Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="4d31d-132">Hello [network.json] [ network-arm] modello di gestione risorse è toocreate configurata una rete virtuale (VNET) con due subnet e due di sicurezza gruppi (rete).</span><span class="sxs-lookup"><span data-stu-id="4d31d-132">hello [network.json][network-arm] Resource Manager template is configured toocreate a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="4d31d-133">Hello [network.parameters.json] [ network-parameters-arm] file dei parametri contiene nomi di hello di subnet hello e NSGs che API di gestione e infrastruttura a servizio verrà distribuito.</span><span class="sxs-lookup"><span data-stu-id="4d31d-133">hello [network.parameters.json][network-parameters-arm] parameters file contains hello names of hello subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="4d31d-134">In questa Guida, i valori dei parametri hello non è necessario toobe modificato.</span><span class="sxs-lookup"><span data-stu-id="4d31d-134">For this guide, hello parameter values do not need toobe changed.</span></span> <span data-ttu-id="4d31d-135">modelli di gestione API e Gestione risorse di infrastruttura servizio Hello utilizzano questi valori, in modo che vengano modificati in questo caso, è necessario modificare in conseguenza hello altri modelli di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="4d31d-135">hello API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in hello other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="4d31d-136">Scaricare i seguenti file di modello e i parametri di gestione risorse hello:</span><span class="sxs-lookup"><span data-stu-id="4d31d-136">Download hello following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="4d31d-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="4d31d-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="4d31d-139">Utilizzare i seguenti PowerShell comando toodeploy hello Gestione risorse modello e parametro file per l'installazione di rete hello hello:</span><span class="sxs-lookup"><span data-stu-id="4d31d-139">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for hello network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a><span data-ttu-id="4d31d-140">Distribuire i cluster di Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="4d31d-140">Deploy hello Service Fabric cluster</span></span>

<span data-ttu-id="4d31d-141">Una volta terminata la distribuzione di risorse di rete hello, hello è toodeploy un toohello di cluster di Service Fabric tra reti VIRTUALI nella subnet hello e NSG designato per il cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-141">Once hello network resources have finished deploying, hello next step is toodeploy a Service Fabric cluster toohello VNET in hello subnet and NSG designated for hello Service Fabric cluster.</span></span> <span data-ttu-id="4d31d-142">Per questa esercitazione, il modello di gestione risorse di infrastruttura servizio hello è preconfigurato toouse hello nomi di hello rete virtuale, subnet e gruppo che è impostato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-142">For this tutorial, hello Service Fabric Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

<span data-ttu-id="4d31d-143">modello di gestione risorse del cluster di Service Fabric Hello è toocreate configurato un cluster protetto con protezione certificati.</span><span class="sxs-lookup"><span data-stu-id="4d31d-143">hello Service Fabric cluster Resource Manager template is configured toocreate a secure cluster with certificate security.</span></span> <span data-ttu-id="4d31d-144">certificato di Hello è comunicazione da nodo a nodo toosecure utilizzato per il cluster e il cluster di Service Fabric tooyour toomanage utente l'accesso.</span><span class="sxs-lookup"><span data-stu-id="4d31d-144">hello certificate is used toosecure node-to-node communication for your cluster and toomanage user access tooyour Service Fabric cluster.</span></span> <span data-ttu-id="4d31d-145">Gestione API utilizza questo hello tooaccess certificato servizio Service Fabric di denominazione per l'individuazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="4d31d-145">API Management uses this certificate tooaccess  hello Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="4d31d-146">Per questo passaggio è necessario disporre di un certificato nel Key Vault per la sicurezza del cluster.</span><span class="sxs-lookup"><span data-stu-id="4d31d-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="4d31d-147">Per ulteriori informazioni sull'impostazione di un cluster protetto con Key Vault, vedere [questa guida per la creazione di un cluster di Service Fabric mediante Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="4d31d-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="4d31d-148">In aggiunta toohello certificato utilizzato per l'accesso del cluster, è possibile aggiungere l'autenticazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4d31d-148">You may add Azure Active Directory authentication in addition toohello certificate used for cluster access.</span></span> <span data-ttu-id="4d31d-149">Azure Active Directory è hello consigliato del cluster di Service Fabric tooyour modo toomanage utente l'accesso, ma è toocomplete non necessari in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4d31d-149">Azure Active Directory is hello recommended way toomanage user access tooyour Service Fabric cluster, but is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="4d31d-150">In entrambi i casi, è richiesto un certificato per la sicurezza del cluster da nodo a nodo e per l'autenticazione di Gestione API di Azure, che attualmente non supporta l'autenticazione con Azure Active Directory per un back-end di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4d31d-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="4d31d-151">Scaricare i seguenti file di modello e i parametri di gestione risorse hello:</span><span class="sxs-lookup"><span data-stu-id="4d31d-151">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="4d31d-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="4d31d-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="4d31d-154">Specificare parametri vuoto di hello in hello `cluster.parameters.json` file per la distribuzione, tra cui hello [informazioni chiave dell'insieme di credenziali](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) per il certificato del cluster.</span><span class="sxs-lookup"><span data-stu-id="4d31d-154">Fill in hello empty parameters in hello `cluster.parameters.json` file for your deployment, including hello [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="4d31d-155">Utilizzare hello PowerShell comando toodeploy hello Gestione risorse modello e parametro file toocreate hello cluster di Service Fabric seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d31d-155">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files toocreate hello Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="4d31d-156">Distribuire Gestione API</span><span class="sxs-lookup"><span data-stu-id="4d31d-156">Deploy API Management</span></span>

<span data-ttu-id="4d31d-157">Infine, distribuire toohello API Gestione reti VIRTUALI nella subnet hello e NSG designato per la gestione API.</span><span class="sxs-lookup"><span data-stu-id="4d31d-157">Finally, deploy API Management toohello VNET in hello subnet and NSG designated for API Management.</span></span> <span data-ttu-id="4d31d-158">Non è necessario toowait per hello Service Fabric cluster distribuzione toofinish prima della distribuzione di gestione API.</span><span class="sxs-lookup"><span data-stu-id="4d31d-158">You do not need toowait for hello Service Fabric cluster deployment toofinish before deploying API Management.</span></span> 

<span data-ttu-id="4d31d-159">Per questa esercitazione, il modello di gestione risorse di gestione API hello è preconfigurato toouse hello nomi di hello rete virtuale, subnet e gruppo che è impostato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-159">For this tutorial, hello API Management Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

 1. <span data-ttu-id="4d31d-160">Scaricare i seguenti file di modello e i parametri di gestione risorse hello:</span><span class="sxs-lookup"><span data-stu-id="4d31d-160">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="4d31d-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="4d31d-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="4d31d-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="4d31d-163">Specificare parametri vuoto di hello in hello `apim.parameters.json` per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4d31d-163">Fill in hello empty parameters in hello `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="4d31d-164">Utilizzare hello seguenti PowerShell comando toodeploy hello Gestione risorse modello e parametro file per la gestione API:</span><span class="sxs-lookup"><span data-stu-id="4d31d-164">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="4d31d-165">Configurare Gestione API</span><span class="sxs-lookup"><span data-stu-id="4d31d-165">Configure API Management</span></span>

<span data-ttu-id="4d31d-166">Dopo aver distribuito Gestione API e il cluster di Service Fabric, è possibile configurare un back-end di Service Fabric in Gestione API.</span><span class="sxs-lookup"><span data-stu-id="4d31d-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="4d31d-167">In questo modo toocreate un criterio del servizio back-end che invia i cluster di Service Fabric tooyour traffico.</span><span class="sxs-lookup"><span data-stu-id="4d31d-167">This allows you toocreate a backend service policy that sends traffic tooyour Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="4d31d-168">Sicurezza di Gestione API</span><span class="sxs-lookup"><span data-stu-id="4d31d-168">API Management Security</span></span>

<span data-ttu-id="4d31d-169">Service Fabric hello tooconfigure back-end, è necessario innanzitutto le impostazioni di sicurezza di gestione API tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="4d31d-169">tooconfigure hello Service Fabric backend, you first need tooconfigure API Management security settings.</span></span> <span data-ttu-id="4d31d-170">le impostazioni di sicurezza tooconfigure, andare tooyour API servizio di gestione nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-170">tooconfigure security settings, go tooyour API Management service in hello Azure portal.</span></span>

#### <a name="enable-hello-api-management-rest-api"></a><span data-ttu-id="4d31d-171">Abilitare hello API REST gestione API</span><span class="sxs-lookup"><span data-stu-id="4d31d-171">Enable hello API Management REST API</span></span>

<span data-ttu-id="4d31d-172">API REST gestione API Hello è attualmente hello solo modo tooconfigure un servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="4d31d-172">hello API Management REST API is currently hello only way tooconfigure a backend service.</span></span> <span data-ttu-id="4d31d-173">primo passaggio Hello è hello tooenable API REST gestione API e proteggerla.</span><span class="sxs-lookup"><span data-stu-id="4d31d-173">hello first step is tooenable hello API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="4d31d-174">Nel servizio Gestione API hello, selezionare **API di gestione - anteprima** in **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="4d31d-174">In hello API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="4d31d-175">Controllare hello **Abilita API REST gestione API** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="4d31d-175">Check hello **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="4d31d-176">Nota hello URL delle API di gestione - URL hello utilizzeremo tooset successive di back-end di Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="4d31d-176">Note hello Management API URL - this is hello URL we'll use later tooset up hello Service Fabric backend</span></span>
 4. <span data-ttu-id="4d31d-177">Genera un **Token di accesso** selezionando una data di scadenza e una chiave, quindi fare clic su hello **genera** pulsante verso il basso hello hello pagina.</span><span class="sxs-lookup"><span data-stu-id="4d31d-177">Generate an **access Token** by selecting an expiry date and a key, then click hello **Generate** button toward hello bottom of hello page.</span></span>
 5. <span data-ttu-id="4d31d-178">Hello copia **token di accesso** e salvarlo, che verrà usata in hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="4d31d-178">Copy hello **access token** and save it - we'll use this in hello following steps.</span></span> <span data-ttu-id="4d31d-179">Tenere presente che questo comportamento è diverso da hello di chiave primaria e secondaria.</span><span class="sxs-lookup"><span data-stu-id="4d31d-179">Note this is different from hello primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="4d31d-180">Caricare un certificato client di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4d31d-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="4d31d-181">Gestione API deve eseguire l'autenticazione con il cluster di Service Fabric per l'individuazione del servizio mediante un certificato client con i cluster tooyour di accesso.</span><span class="sxs-lookup"><span data-stu-id="4d31d-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access tooyour cluster.</span></span> <span data-ttu-id="4d31d-182">Per semplicità, questa esercitazione viene utilizzato hello stesso certificato specificato durante la creazione di cluster di Service Fabric hello, che per impostazione predefinita può essere utilizzato tooaccess del cluster.</span><span class="sxs-lookup"><span data-stu-id="4d31d-182">For simplicity, this tutorial uses hello same certificate specified when creating hello Service Fabric cluster, which by default can be used tooaccess your cluster.</span></span>

 1. <span data-ttu-id="4d31d-183">Nel servizio Gestione API hello, selezionare **certificati Client - anteprima** in **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="4d31d-183">In hello API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="4d31d-184">Fare clic su hello **+ Aggiungi** pulsante</span><span class="sxs-lookup"><span data-stu-id="4d31d-184">Click hello **+ Add** button</span></span>
 2. <span data-ttu-id="4d31d-185">Selezionare hello file di chiave privata (con estensione pfx) del certificato cluster hello specificata durante la creazione del cluster di Service Fabric, assegnargli un nome e fornire una password della chiave privata hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-185">Select hello private key file (.pfx) of hello cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide hello private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="4d31d-186">Questa esercitazione Usa hello stesso certificato per la sicurezza del nodo a nodo cluster e di autenticazione client.</span><span class="sxs-lookup"><span data-stu-id="4d31d-186">This tutorial uses hello same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="4d31d-187">Se si dispone di un tooaccess configurato il cluster di Service Fabric, è possibile utilizzare un certificato client separato.</span><span class="sxs-lookup"><span data-stu-id="4d31d-187">You may use a separate client certificate if you have one configured tooaccess your Service Fabric cluster.</span></span>

### <a name="configure-hello-backend"></a><span data-ttu-id="4d31d-188">Configurare back-end hello</span><span class="sxs-lookup"><span data-stu-id="4d31d-188">Configure hello backend</span></span>

<span data-ttu-id="4d31d-189">Ora che viene configurata la sicurezza di gestione API, è possibile configurare back-end di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-189">Now that API Management security is configured, you can configure hello Service Fabric backend.</span></span> <span data-ttu-id="4d31d-190">Per back-end dell'infrastruttura di servizio, il cluster di Service Fabric hello è back-end hello, anziché uno specifico servizio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4d31d-190">For Service Fabric backends, hello Service Fabric cluster is hello backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="4d31d-191">In questo modo un toomore tooroute singolo criterio rispetto a un servizio cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-191">This allows a single policy tooroute toomore than one service in hello cluster.</span></span>

<span data-ttu-id="4d31d-192">Questo passaggio richiede il token di accesso hello generati in precedenza e identificazione personale per il certificato del cluster che è stata caricata tooAPI Management nel passaggio precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-192">This step requires hello access token you generated earlier and hello thumbprint for your cluster certificate you uploaded tooAPI Management in hello previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="4d31d-193">Se si utilizza un certificato client separato nel passaggio precedente hello di gestione API, è necessario identificazione personale hello per il certificato client hello in identificazione personale del certificato del cluster toohello aggiunta in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="4d31d-193">If you used a separate client certificate in hello previous step for API Management, you need hello thumbprint for hello client certificate in addition toohello cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="4d31d-194">Inviare hello seguente toohello di richiesta HTTP PUT URL API di gestione API annotati in precedenza durante l'abilitazione del servizio back-end di hello API REST gestione API tooconfigure hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4d31d-194">Send hello following HTTP PUT request toohello API Management API URL you noted earlier when enabling hello API Management REST API tooconfigure hello Service Fabric backend service.</span></span> <span data-ttu-id="4d31d-195">Verrà visualizzato un `HTTP 201 Created` risposta quando il comando hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="4d31d-195">You should see an `HTTP 201 Created` response when hello command succeeds.</span></span> <span data-ttu-id="4d31d-196">Per ulteriori informazioni su ogni campo, vedere Gestione API hello [la documentazione di riferimento API back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="4d31d-196">For more information on each field, see hello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="4d31d-197">Comando e URL HTTP:</span><span class="sxs-lookup"><span data-stu-id="4d31d-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="4d31d-198">Intestazioni della richiesta:</span><span class="sxs-lookup"><span data-stu-id="4d31d-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="4d31d-199">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="4d31d-199">Request body:</span></span>
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

<span data-ttu-id="4d31d-200">Hello **url** parametro qui è un nome di servizio completo di un servizio del cluster che tutte le richieste vengono indirizzate tooby predefinito se è specificato alcun nome di servizio in un criterio di back-end.</span><span class="sxs-lookup"><span data-stu-id="4d31d-200">hello **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed tooby default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="4d31d-201">È possibile utilizzare un nome di servizio fittizio, ad esempio "fabric: / false/servizio" Se non si intende toohave un servizio di fallback.</span><span class="sxs-lookup"><span data-stu-id="4d31d-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend toohave a fallback service.</span></span>

<span data-ttu-id="4d31d-202">Fare riferimento a gestione API toohello [la documentazione di riferimento API back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) per ulteriori informazioni su ogni campo.</span><span class="sxs-lookup"><span data-stu-id="4d31d-202">Refer toohello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="4d31d-203">Esempio</span><span class="sxs-lookup"><span data-stu-id="4d31d-203">Example</span></span>

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="4d31d-204">Distribuire un servizio back-end di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4d31d-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="4d31d-205">Dopo aver creato hello che Service Fabric è configurato come un tooAPI back-end, gestione, è possibile creare criteri di back-end per le API che inviano traffico tooyour servizi di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4d31d-205">Now that you have hello Service Fabric configured as a backend tooAPI Management, you can author backend policies for your APIs that send traffic tooyour Service Fabric services.</span></span> <span data-ttu-id="4d31d-206">Ma prima è necessario un servizio in esecuzione nelle richieste tooaccept Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4d31d-206">But first you need a service running in Service Fabric tooaccept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="4d31d-207">Creare un servizio Service Fabric con un endpoint HTTP</span><span class="sxs-lookup"><span data-stu-id="4d31d-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="4d31d-208">Per questa esercitazione si creerà una base ASP.NET Core servizio Reliable senza stato con modello di progetto API Web hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="4d31d-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using hello default Web API project template.</span></span> <span data-ttu-id="4d31d-209">Questo permetterà di generare un endpoint HTTP per il servizio, che verrà esposto tramite Gestione API di Azure:</span><span class="sxs-lookup"><span data-stu-id="4d31d-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="4d31d-210">Partire dall'[impostazione dell'ambiente per lo sviluppo di ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="4d31d-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="4d31d-211">Dopo aver impostato l'ambiente di sviluppo, avviare Visual Studio come Amministratore e creare un servizio ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="4d31d-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="4d31d-212">In Visual Studio selezionare File -> Nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="4d31d-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="4d31d-213">Selezionare il modello di applicazione di Service Fabric hello nel Cloud e denominarlo **"ApiApplication"**.</span><span class="sxs-lookup"><span data-stu-id="4d31d-213">Select hello Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="4d31d-214">Selezionare il modello di servizio ASP.NET Core hello e progetto hello nome **"WebApiService"**.</span><span class="sxs-lookup"><span data-stu-id="4d31d-214">Select hello ASP.NET Core service template and name hello project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="4d31d-215">Selezionare il modello di progetto di Web API ASP.NET Core 1.1 hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-215">Select hello Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="4d31d-216">Una volta creato il progetto di hello, aprire `PackageRoot\ServiceManifest.xml` e rimuovere hello `Port` attributo dalla configurazione di risorsa endpoint hello:</span><span class="sxs-lookup"><span data-stu-id="4d31d-216">Once hello project is created, open `PackageRoot\ServiceManifest.xml` and remove hello `Port` attribute from hello endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="4d31d-217">In questo modo toospecify Service Fabric una porta in modo dinamico da intervallo di porte applicazione hello, che è stata aperta tramite hello il gruppo di sicurezza di rete nel modello di gestione risorse di cluster hello, che consente il traffico tooflow tooit da Gestione API.</span><span class="sxs-lookup"><span data-stu-id="4d31d-217">This allows Service Fabric toospecify a port dynamically from hello application port range, which we opened through hello Network Security Group in hello cluster Resource Manager template, allowing traffic tooflow tooit from API Management.</span></span>
 
 6. <span data-ttu-id="4d31d-218">Premere F5 nell'API web hello tooverify di Visual Studio sono disponibili localmente.</span><span class="sxs-lookup"><span data-stu-id="4d31d-218">Press F5 in Visual Studio tooverify hello web API is available locally.</span></span> 

    <span data-ttu-id="4d31d-219">Aprire Service Fabric Explorer e il drill-down tooa istanza specifica di hello ASP.NET Core toosee hello indirizzo di base hello del servizio è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="4d31d-219">Open Service Fabric Explorer and drill down tooa specific instance of hello ASP.NET Core service toosee hello base address hello service is listening on.</span></span> <span data-ttu-id="4d31d-220">Aggiungere `/api/values` toohello indirizzo di base e aprirlo in un browser.</span><span class="sxs-lookup"><span data-stu-id="4d31d-220">Add `/api/values` toohello base address and open it in a browser.</span></span> <span data-ttu-id="4d31d-221">Viene richiamato il metodo Get su hello ValuesController nel modello API Web hello hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-221">This invokes hello Get method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="4d31d-222">Restituisce una risposta predefinita hello fornito dal modello hello, una matrice JSON contenente due stringhe:</span><span class="sxs-lookup"><span data-stu-id="4d31d-222">It returns hello default response that is provided by hello template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="4d31d-223">Si tratta di endpoint hello Esponi tramite Gestione API in Azure.</span><span class="sxs-lookup"><span data-stu-id="4d31d-223">This is hello endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="4d31d-224">Infine, distribuire cluster di tooyour applicazione hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="4d31d-224">Finally, deploy hello application tooyour cluster in Azure.</span></span> <span data-ttu-id="4d31d-225">[Utilizzo di Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box)del progetto di applicazione hello di mouse e scegliere **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="4d31d-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click hello Application project and select **Publish**.</span></span> <span data-ttu-id="4d31d-226">Specificare l'endpoint del cluster (ad esempio, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello applicazione tooyour dell'infrastruttura del servizio cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="4d31d-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="4d31d-227">In tale cluster dovrebbe essere ora in esecuzione un servizio ASP.NET Core senza stato denominato `fabric:/ApiApplication/WebApiService`.</span><span class="sxs-lookup"><span data-stu-id="4d31d-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="4d31d-228">Creare un'operazione per le API</span><span class="sxs-lookup"><span data-stu-id="4d31d-228">Create an API operation</span></span>

<span data-ttu-id="4d31d-229">Ora siamo toocreate pronto un'operazione in Gestione API toocommunicate di utilizzare tale client esterni con hello servizio senza stato di ASP.NET Core in esecuzione nel cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-229">Now we're ready toocreate an operation in API Management that external clients use toocommunicate with hello ASP.NET Core stateless service running in hello Service Fabric cluster.</span></span>

 1. <span data-ttu-id="4d31d-230">Accedi al portale di Azure toohello e passare tooyour distribuzione del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="4d31d-230">Log in toohello Azure portal and navigate tooyour API Management service deployment.</span></span>
 2. <span data-ttu-id="4d31d-231">Nel Pannello di servizio di gestione API hello, selezionare **API - anteprima**</span><span class="sxs-lookup"><span data-stu-id="4d31d-231">In hello API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="4d31d-232">Aggiungere una nuova API facendo hello **API vuoto** casella e compilare la finestra di dialogo hello:</span><span class="sxs-lookup"><span data-stu-id="4d31d-232">Add a new API by clicking hello **Blank API** box and filling out hello dialog box:</span></span>

     - <span data-ttu-id="4d31d-233">**URL del servizio Web**: per i back-end di Service Fabric, questo valore URL non viene usato.</span><span class="sxs-lookup"><span data-stu-id="4d31d-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="4d31d-234">È possibile inserire un valore qualsiasi nel campo.</span><span class="sxs-lookup"><span data-stu-id="4d31d-234">You can put any value here.</span></span> <span data-ttu-id="4d31d-235">Per questa esercitazione, usare `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="4d31d-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="4d31d-236">**Nome**: inserire il nome dell'API.</span><span class="sxs-lookup"><span data-stu-id="4d31d-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="4d31d-237">Per questa esercitazione, usare `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="4d31d-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="4d31d-238">**Schema URL**: selezionare HTTP, HTTPS o entrambi i valori.</span><span class="sxs-lookup"><span data-stu-id="4d31d-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="4d31d-239">Per questa esercitazione, usare `both`.</span><span class="sxs-lookup"><span data-stu-id="4d31d-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="4d31d-240">**Suffisso URL API**: inserire un suffisso per l'API.</span><span class="sxs-lookup"><span data-stu-id="4d31d-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="4d31d-241">Per questa esercitazione, usare `myapp`.</span><span class="sxs-lookup"><span data-stu-id="4d31d-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="4d31d-242">Una volta creato hello API, fare clic su **+ Aggiungi operazione** operazione tooadd un'API front-end.</span><span class="sxs-lookup"><span data-stu-id="4d31d-242">Once hello API is created, click **+ Add operation** tooadd a front-end API operation.</span></span> <span data-ttu-id="4d31d-243">Compilare i valori hello:</span><span class="sxs-lookup"><span data-stu-id="4d31d-243">Fill out hello values:</span></span>
    
     - <span data-ttu-id="4d31d-244">**URL**: selezionare `GET` e fornire un percorso URL per hello API.</span><span class="sxs-lookup"><span data-stu-id="4d31d-244">**URL**: Select `GET` and provide a URL path for hello API.</span></span> <span data-ttu-id="4d31d-245">Per questa esercitazione, usare `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="4d31d-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="4d31d-246">Per impostazione predefinita, il percorso di URL hello specificato qui è il percorso di URL hello inviato toohello servizio di Service Fabric back-end.</span><span class="sxs-lookup"><span data-stu-id="4d31d-246">By default, hello URL path specified here is hello URL path sent toohello backend Service Fabric service.</span></span> <span data-ttu-id="4d31d-247">Se si utilizza hello stesso percorso URL di seguito in questo caso il servizio utilizza `/api/values`, quindi operazione hello funziona senza ulteriori modifiche.</span><span class="sxs-lookup"><span data-stu-id="4d31d-247">If you use hello same URL path here that your service uses, in this case `/api/values`, then hello operation works without further modification.</span></span> <span data-ttu-id="4d31d-248">È inoltre possibile specificare un percorso URL qui è diverso dal percorso dell'URL hello utilizzato dal back-end del servizio Service Fabric, nel qual caso sarà anche necessario toospecify un percorso di riscrittura nei criteri di operazione in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="4d31d-248">You may also specify a URL path here that is different from hello URL path used by your backend Service Fabric service, in which case you will also need toospecify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="4d31d-249">**Nome visualizzato**: fornire un nome qualsiasi per hello API.</span><span class="sxs-lookup"><span data-stu-id="4d31d-249">**Display name**: Provide any name for hello API.</span></span> <span data-ttu-id="4d31d-250">Per questa esercitazione, usare `Values`.</span><span class="sxs-lookup"><span data-stu-id="4d31d-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="4d31d-251">Configurare un criterio di back-end</span><span class="sxs-lookup"><span data-stu-id="4d31d-251">Configure a backend policy</span></span>

<span data-ttu-id="4d31d-252">criteri di back-end Hello collega tutti gli elementi.</span><span class="sxs-lookup"><span data-stu-id="4d31d-252">hello backend policy ties everything together.</span></span> <span data-ttu-id="4d31d-253">Questo è possibile configurare hello back-end dell'infrastruttura di servizio vengono indirizzate le richieste di servizio toowhich.</span><span class="sxs-lookup"><span data-stu-id="4d31d-253">This is where you configure hello backend Service Fabric service toowhich requests are routed.</span></span> <span data-ttu-id="4d31d-254">È possibile applicare l'operazione API tooany di criteri.</span><span class="sxs-lookup"><span data-stu-id="4d31d-254">You can apply this policy tooany API operation.</span></span> <span data-ttu-id="4d31d-255">Hello [configurazione back-end per l'infrastruttura del servizio](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) seguente hello richiesta di routing controlli:</span><span class="sxs-lookup"><span data-stu-id="4d31d-255">hello [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides hello following request routing controls:</span></span> 
 - <span data-ttu-id="4d31d-256">Selezione dell'istanza del servizio specificando un nome di istanza di servizio di Service Fabric, entrambi hardcoded (ad esempio, `"fabric:/myapp/myservice"`) o generato dalla richiesta hello HTTP (ad esempio, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="4d31d-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from hello HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="4d31d-257">Risoluzione della partizione mediante la generazione di una chiave di partizione che usa uno schema di partizionamento di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4d31d-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="4d31d-258">Selezione della replica per i servizi con stato.</span><span class="sxs-lookup"><span data-stu-id="4d31d-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="4d31d-259">Risoluzione ripetere le condizioni che consentono di condizioni di hello toospecify per risolvere di nuovo una posizione del servizio e inviare una richiesta.</span><span class="sxs-lookup"><span data-stu-id="4d31d-259">Resolution retry conditions that allow you toospecify hello conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="4d31d-260">Per questa esercitazione, creare un criterio di back-end che le route richieste direttamente toohello servizio senza stato di ASP.NET Core distribuito in precedenza:</span><span class="sxs-lookup"><span data-stu-id="4d31d-260">For this tutorial, create a backend policy that routes requests directly toohello ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="4d31d-261">Selezionare e modificare hello **in ingresso criteri** per hello `Values` operazione facendo clic sull'icona di modifica hello e quindi selezionando **visualizzazione codice**.</span><span class="sxs-lookup"><span data-stu-id="4d31d-261">Select and edit hello **inbound policies** for hello `Values` operation by clicking hello edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="4d31d-262">Nell'editor di codice hello criteri, aggiungere un `set-backend-service` criteri in ingresso criteri, come illustrato di seguito e fare clic su hello **salvare** pulsante:</span><span class="sxs-lookup"><span data-stu-id="4d31d-262">In hello policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click hello **Save** button:</span></span>
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

<span data-ttu-id="4d31d-263">Per un set completo di attributi di criteri di back-end di Service Fabric, fare riferimento toohello [documentazione back-end di gestione API](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="4d31d-263">For a full set of Service Fabric back-end policy attributes, refer toohello [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-hello-api-tooa-product"></a><span data-ttu-id="4d31d-264">Aggiungere hello API tooa prodotto.</span><span class="sxs-lookup"><span data-stu-id="4d31d-264">Add hello API tooa product.</span></span> 

<span data-ttu-id="4d31d-265">Prima di chiamare API hello, è necessario aggiungerlo tooa prodotto in cui è possibile concedere l'accesso toousers.</span><span class="sxs-lookup"><span data-stu-id="4d31d-265">Before you can call hello API, it must be added tooa product where you can grant access toousers.</span></span> 

 1. <span data-ttu-id="4d31d-266">Nel servizio Gestione API hello, selezionare **prodotti - anteprima**.</span><span class="sxs-lookup"><span data-stu-id="4d31d-266">In hello API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="4d31d-267">Per impostazione predefinita, Gestione API include due prodotti: Starter e Illimitato.</span><span class="sxs-lookup"><span data-stu-id="4d31d-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="4d31d-268">Selezionare prodotto illimitato hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-268">Select hello Unlimited product.</span></span>
 3. <span data-ttu-id="4d31d-269">Selezionare API.</span><span class="sxs-lookup"><span data-stu-id="4d31d-269">Select APIs.</span></span>
 4. <span data-ttu-id="4d31d-270">Fare clic su hello **+ Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4d31d-270">Click hello **+ Add** button.</span></span>
 5. <span data-ttu-id="4d31d-271">Seleziona hello `Service Fabric App` API creata nei passaggi precedenti hello e fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4d31d-271">Select hello `Service Fabric App` API you created in hello previous steps and click hello **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="4d31d-272">Eseguirne il test</span><span class="sxs-lookup"><span data-stu-id="4d31d-272">Test it</span></span>

<span data-ttu-id="4d31d-273">È possibile ritentare l'invio di un servizio back-end di tooyour richiesta nell'infrastruttura del servizio tramite Gestione API direttamente dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-273">You can now try sending a request tooyour back-end service in Service Fabric through API Management directly from hello Azure portal.</span></span>

 1. <span data-ttu-id="4d31d-274">Nel servizio Gestione API hello, selezionare **API - anteprima**.</span><span class="sxs-lookup"><span data-stu-id="4d31d-274">In hello API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="4d31d-275">In hello `Service Fabric App` API creato nei passaggi precedenti hello, selezionare hello **Test** scheda.</span><span class="sxs-lookup"><span data-stu-id="4d31d-275">In hello `Service Fabric App` API you created in hello previous steps, select hello **Test** tab.</span></span>
 3. <span data-ttu-id="4d31d-276">Fare clic su hello **inviare** pulsante toosend un servizio back-end di test richiesta toohello.</span><span class="sxs-lookup"><span data-stu-id="4d31d-276">Click hello **Send** button toosend a test request toohello backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d31d-277">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d31d-277">Next steps</span></span>

<span data-ttu-id="4d31d-278">A questo punto, dovrebbe essere disponibile un'installazione di base con i servizi Service Fabric e Gestione API.</span><span class="sxs-lookup"><span data-stu-id="4d31d-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="4d31d-279">In questa esercitazione Usa l'autenticazione utente basata su certificati di base per impostare rapidamente il tooget di cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4d31d-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster tooget you set up quickly.</span></span> <span data-ttu-id="4d31d-280">È consigliabile eseguire un'autenticazione utente più avanzata per il cluster di Service Fabric basata su [Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="4d31d-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="4d31d-281">Successivamente, [creare e configurare le impostazioni di prodotto avanzate in Gestione API di Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare l'applicazione per il traffico reale.</span><span class="sxs-lookup"><span data-stu-id="4d31d-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare your application for real world traffic.</span></span>

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
