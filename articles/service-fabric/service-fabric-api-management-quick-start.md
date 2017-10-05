---
title: Avvio rapido di Azure Service Fabric con Gestione API | Microsoft Docs
description: Questa guida illustra le procedure per iniziare a usare subito Gestione API di Azure con Service Fabric.
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
ms.openlocfilehash: e9f44d8a43d274768f43261fea68f0da9c681ae1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="88447-103">Avvio rapido di Service Fabric con Gestione API</span><span class="sxs-lookup"><span data-stu-id="88447-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="88447-104">Questa guida mostra come impostare il servizio Gestione API di Azure con Service Fabric e configurare la prima operazione API per l'invio di traffico ai servizi back-end di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-104">This guide shows you how to set up Azure API Management with Service Fabric and configure your first API operation to send traffic to back-end services in Service Fabric.</span></span> <span data-ttu-id="88447-105">Per ulteriori informazioni sugli scenari di Gestione API di Azure con Service Fabric, vedere l'articolo [Panoramica](service-fabric-api-management-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88447-105">To learn more about Azure API Management scenarios with Service Fabric, see the [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-to-azure"></a><span data-ttu-id="88447-106">Distribuire Gestione API e Service Fabric in Azure</span><span class="sxs-lookup"><span data-stu-id="88447-106">Deploy API Management and Service Fabric to Azure</span></span>

<span data-ttu-id="88447-107">Il primo passaggio consiste nel distribuire un cluster di Gestione API e Service Fabric in Azure tramite una rete virtuale condivisa.</span><span class="sxs-lookup"><span data-stu-id="88447-107">The first step is to deploy API Management and a Service Fabric cluster to Azure in a shared Virtual Network.</span></span> <span data-ttu-id="88447-108">In questo modo Gestione API può comunicare direttamente con Service Fabric in modo da poter eseguire l'individuazione del servizio, la risoluzione della partizione del servizio e inoltrare il traffico direttamente a un servizio back-end in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-108">This allows API Management to communicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly to any backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="88447-109">Topologia</span><span class="sxs-lookup"><span data-stu-id="88447-109">Topology</span></span>

<span data-ttu-id="88447-110">Le informazioni contenute in questa guida consentono di distribuire in Azure la topologia mostrata di seguito, dove Gestione API e Service Fabric si trovano in subnet della stessa rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="88447-110">This guide deploys the following topology to Azure in which API Management and Service Fabric are in subnets of the same Virtual Network:</span></span>

 ![Sottotitolo immagine][sf-apim-topology-overview]

<span data-ttu-id="88447-112">Per iniziare rapidamente, vengono forniti modelli di Resource Manager per ogni passaggio di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="88447-112">To get started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="88447-113">Topologia di rete:</span><span class="sxs-lookup"><span data-stu-id="88447-113">Network topology:</span></span>
    - <span data-ttu-id="88447-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="88447-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="88447-116">Cluster di Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="88447-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="88447-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="88447-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="88447-119">Gestione API:</span><span class="sxs-lookup"><span data-stu-id="88447-119">API Management:</span></span>
    - <span data-ttu-id="88447-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="88447-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-to-azure-and-select-your-subscription"></a><span data-ttu-id="88447-122">Accedere ad Azure e selezionare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="88447-122">Sign in to Azure and select your subscription</span></span>

<span data-ttu-id="88447-123">Questa guida usa [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="88447-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="88447-124">Quando si avvia una nuova sessione di PowerShell, accedere al proprio account Azure e selezionare la sottoscrizione prima di eseguire i comandi di Azure.</span><span class="sxs-lookup"><span data-stu-id="88447-124">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="88447-125">Accedere all'account Azure:</span><span class="sxs-lookup"><span data-stu-id="88447-125">Sign in to your Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="88447-126">Selezionare la propria sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="88447-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="88447-127">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="88447-127">Create a resource group</span></span>

<span data-ttu-id="88447-128">Creare un nuovo gruppo di risorse per la propria distribuzione.</span><span class="sxs-lookup"><span data-stu-id="88447-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="88447-129">Assegnargli un nome e una posizione.</span><span class="sxs-lookup"><span data-stu-id="88447-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-the-network-topology"></a><span data-ttu-id="88447-130">Distribuire la topologia di rete</span><span class="sxs-lookup"><span data-stu-id="88447-130">Deploy the network topology</span></span>

<span data-ttu-id="88447-131">Il primo passaggio consiste nella configurazione della topologia di rete nella quale verrà distribuito il cluster di Gestione API e Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-131">The first step is to set up the network topology to which API Management and the Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="88447-132">Il modello di Resource Manager [network.json][network-arm] viene configurato per creare una rete virtuale (VNET) con due subnet e due gruppi di sicurezza di rete (NSG).</span><span class="sxs-lookup"><span data-stu-id="88447-132">The [network.json][network-arm] Resource Manager template is configured to create a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="88447-133">Il file di parametri [network.parameters.json][network-parameters-arm] contiene i nomi delle subnet e i gruppi di sicurezza di rete in cui verranno distribuiti Gestione API e Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-133">The [network.parameters.json][network-parameters-arm] parameters file contains the names of the subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="88447-134">In questa guida non è necessario modificare i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="88447-134">For this guide, the parameter values do not need to be changed.</span></span> <span data-ttu-id="88447-135">I modelli di Resource Manager di Gestione API e Service Fabric usano questi valori, pertanto se vengono modificati qui, sarà necessario modificarli anche negli altri modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="88447-135">The API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in the other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="88447-136">Scaricare il modello e il file di parametri di Resource Manager seguenti:</span><span class="sxs-lookup"><span data-stu-id="88447-136">Download the following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="88447-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="88447-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="88447-139">Per distribuire il modello e il file di parametri di Resource Manager per la configurazione di rete, usare il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="88447-139">Use the following PowerShell command to deploy the Resource Manager template and parameter files for the network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-the-service-fabric-cluster"></a><span data-ttu-id="88447-140">Distribuire il cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="88447-140">Deploy the Service Fabric cluster</span></span>

<span data-ttu-id="88447-141">Una volta terminata la distribuzione delle risorse di rete, il passaggio successivo consiste nel distribuire un cluster Service Fabric per la rete virtuale nella subnet e nel gruppo NSG designato per tale cluster.</span><span class="sxs-lookup"><span data-stu-id="88447-141">Once the network resources have finished deploying, the next step is to deploy a Service Fabric cluster to the VNET in the subnet and NSG designated for the Service Fabric cluster.</span></span> <span data-ttu-id="88447-142">Per questa esercitazione, il modello di Resource Manager di Service Fabric è preconfigurato per l'uso dei nomi di rete virtuale, subnet e gruppo NSG impostati nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="88447-142">For this tutorial, the Service Fabric Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

<span data-ttu-id="88447-143">Il modello di Resource Manager del cluster di Service Fabric è configurato per la creazione di un cluster protetto mediante un'architettura di sicurezza basata sui certificati.</span><span class="sxs-lookup"><span data-stu-id="88447-143">The Service Fabric cluster Resource Manager template is configured to create a secure cluster with certificate security.</span></span> <span data-ttu-id="88447-144">Il certificato viene usato per proteggere la comunicazione da nodo a nodo per il cluster e per gestire l'accesso utente al cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-144">The certificate is used to secure node-to-node communication for your cluster and to manage user access to your Service Fabric cluster.</span></span> <span data-ttu-id="88447-145">Gestione API usa questo certificato per accedere al Service Fabric Naming Service per l'individuazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="88447-145">API Management uses this certificate to access  the Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="88447-146">Per questo passaggio è necessario disporre di un certificato nel Key Vault per la sicurezza del cluster.</span><span class="sxs-lookup"><span data-stu-id="88447-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="88447-147">Per ulteriori informazioni sull'impostazione di un cluster protetto con Key Vault, vedere [questa guida per la creazione di un cluster di Service Fabric mediante Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="88447-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="88447-148">È possibile aggiungere l'autenticazione di Azure Active Directory oltre al certificato usato per l'accesso al cluster.</span><span class="sxs-lookup"><span data-stu-id="88447-148">You may add Azure Active Directory authentication in addition to the certificate used for cluster access.</span></span> <span data-ttu-id="88447-149">Azure Active Directory è il modo consigliato per gestire l'accesso utente al cluster di Service Fabric, ma non è necessario per completare questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="88447-149">Azure Active Directory is the recommended way to manage user access to your Service Fabric cluster, but is not necessary to complete this tutorial.</span></span> <span data-ttu-id="88447-150">In entrambi i casi, è richiesto un certificato per la sicurezza del cluster da nodo a nodo e per l'autenticazione di Gestione API di Azure, che attualmente non supporta l'autenticazione con Azure Active Directory per un back-end di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="88447-151">Scaricare il modello e il file di parametri di Resource Manager seguenti:</span><span class="sxs-lookup"><span data-stu-id="88447-151">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="88447-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="88447-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="88447-154">Compilare i parametri vuoti nel file `cluster.parameters.json` per la distribuzione, incluse le [informazioni sul Key Vault](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) per il certificato del cluster.</span><span class="sxs-lookup"><span data-stu-id="88447-154">Fill in the empty parameters in the `cluster.parameters.json` file for your deployment, including the [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="88447-155">Per distribuire il modello e i file di parametri di Resource Manager per creare il cluster di Service Fabric, usare il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="88447-155">Use the following PowerShell command to deploy the Resource Manager template and parameter files to create the Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="88447-156">Distribuire Gestione API</span><span class="sxs-lookup"><span data-stu-id="88447-156">Deploy API Management</span></span>

<span data-ttu-id="88447-157">Infine, distribuire Gestione API per la rete virtuale nella subnet e il gruppo NSG designato per Gestione API.</span><span class="sxs-lookup"><span data-stu-id="88447-157">Finally, deploy API Management to the VNET in the subnet and NSG designated for API Management.</span></span> <span data-ttu-id="88447-158">Non è necessario attendere il completamento della distribuzione del cluster di Service Fabric per poter distribuire Gestione API.</span><span class="sxs-lookup"><span data-stu-id="88447-158">You do not need to wait for the Service Fabric cluster deployment to finish before deploying API Management.</span></span> 

<span data-ttu-id="88447-159">Per questa esercitazione, il modello di Resource Manager di Gestione API è preconfigurato per l'uso dei nomi di rete virtuale, subnet e gruppo NSG impostati nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="88447-159">For this tutorial, the API Management Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

 1. <span data-ttu-id="88447-160">Scaricare il modello e il file di parametri di Resource Manager seguenti:</span><span class="sxs-lookup"><span data-stu-id="88447-160">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="88447-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="88447-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="88447-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="88447-163">Specificare i parametri vuoti nel file `apim.parameters.json` per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="88447-163">Fill in the empty parameters in the `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="88447-164">Per distribuire il modello e il file di parametri di Resource Manager per Gestione API, usare il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="88447-164">Use the following PowerShell command to deploy the Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="88447-165">Configurare Gestione API</span><span class="sxs-lookup"><span data-stu-id="88447-165">Configure API Management</span></span>

<span data-ttu-id="88447-166">Dopo aver distribuito Gestione API e il cluster di Service Fabric, è possibile configurare un back-end di Service Fabric in Gestione API.</span><span class="sxs-lookup"><span data-stu-id="88447-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="88447-167">Questo consente di creare un criterio del servizio back-end che invia il traffico al cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-167">This allows you to create a backend service policy that sends traffic to your Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="88447-168">Sicurezza di Gestione API</span><span class="sxs-lookup"><span data-stu-id="88447-168">API Management Security</span></span>

<span data-ttu-id="88447-169">Per configurare il back-end di Service Fabric, è innanzitutto necessario configurare le impostazioni di sicurezza di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="88447-169">To configure the Service Fabric backend, you first need to configure API Management security settings.</span></span> <span data-ttu-id="88447-170">A questo scopo, passare al servizio Gestione API nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="88447-170">To configure security settings, go to your API Management service in the Azure portal.</span></span>

#### <a name="enable-the-api-management-rest-api"></a><span data-ttu-id="88447-171">Abilitare l'API REST di Gestione API</span><span class="sxs-lookup"><span data-stu-id="88447-171">Enable the API Management REST API</span></span>

<span data-ttu-id="88447-172">L'API REST di Gestione API rappresenta al momento l'unico modo per configurare un servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="88447-172">The API Management REST API is currently the only way to configure a backend service.</span></span> <span data-ttu-id="88447-173">È innanzitutto necessario abilitare l'API REST di Gestione API e proteggerla.</span><span class="sxs-lookup"><span data-stu-id="88447-173">The first step is to enable the API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="88447-174">Nel servizio Gestione API selezionare **Gestione API - ANTEPRIMA** in **Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="88447-174">In the API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="88447-175">Selezionare la casella di controllo **Abilita API REST di Gestione API**.</span><span class="sxs-lookup"><span data-stu-id="88447-175">Check the **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="88447-176">Prendere nota dell'URL dell'API di gestione, ovvero l'URL che verrà usato successivamente per configurare il back-end di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-176">Note the Management API URL - this is the URL we'll use later to set up the Service Fabric backend</span></span>
 4. <span data-ttu-id="88447-177">Generare un **token di accesso** selezionando una data di scadenza e una chiave, quindi fare clic sul pulsante **Genera** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="88447-177">Generate an **access Token** by selecting an expiry date and a key, then click the **Generate** button toward the bottom of the page.</span></span>
 5. <span data-ttu-id="88447-178">Copiare il **token di accesso** e salvarlo per usarlo nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="88447-178">Copy the **access token** and save it - we'll use this in the following steps.</span></span> <span data-ttu-id="88447-179">Tenere presente che questo token è diverso dalla chiave primaria e dalla chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="88447-179">Note this is different from the primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="88447-180">Caricare un certificato client di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="88447-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="88447-181">Gestione API deve eseguire l'autenticazione con il cluster di Service Fabric per individuare il servizio mediante un certificato client che dispone di accesso al cluster.</span><span class="sxs-lookup"><span data-stu-id="88447-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access to your cluster.</span></span> <span data-ttu-id="88447-182">Per semplicità, in questa esercitazione viene usato lo stesso certificato specificato durante la creazione del cluster di Service Fabric, che per impostazione predefinita può essere usato per accedere al cluster.</span><span class="sxs-lookup"><span data-stu-id="88447-182">For simplicity, this tutorial uses the same certificate specified when creating the Service Fabric cluster, which by default can be used to access your cluster.</span></span>

 1. <span data-ttu-id="88447-183">Nel servizio Gestione API selezionare **Certificati client - ANTEPRIMA** in **Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="88447-183">In the API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="88447-184">Fare clic sul pulsante **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="88447-184">Click the **+ Add** button</span></span>
 2. <span data-ttu-id="88447-185">Selezionare il file di chiave privata (con estensione pfx) del certificato del cluster specificato durante la creazione del cluster di Service Fabric, assegnargli un nome e immettere la password della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="88447-185">Select the private key file (.pfx) of the cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide the private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="88447-186">In questa esercitazione viene usato lo stesso certificato per l'autenticazione client e la sicurezza del cluster da nodo a nodo.</span><span class="sxs-lookup"><span data-stu-id="88447-186">This tutorial uses the same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="88447-187">È possibile usare un certificato client separato se ne è stato configurato uno per l'accesso al cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-187">You may use a separate client certificate if you have one configured to access your Service Fabric cluster.</span></span>

### <a name="configure-the-backend"></a><span data-ttu-id="88447-188">Configurare il back-end</span><span class="sxs-lookup"><span data-stu-id="88447-188">Configure the backend</span></span>

<span data-ttu-id="88447-189">Dopo aver configurato la sicurezza di Gestione API, è possibile configurare il back-end di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-189">Now that API Management security is configured, you can configure the Service Fabric backend.</span></span> <span data-ttu-id="88447-190">Per i back-end di Service Fabric, il cluster di Service Fabric è il back-end, anziché uno specifico servizio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-190">For Service Fabric backends, the Service Fabric cluster is the backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="88447-191">Questo consente di eseguire il routing di un singolo criterio in più servizi del cluster.</span><span class="sxs-lookup"><span data-stu-id="88447-191">This allows a single policy to route to more than one service in the cluster.</span></span>

<span data-ttu-id="88447-192">Per eseguire questo passaggio è necessario specificare il token di accesso generato prima e l'identificazione personale per il certificato cluster caricato in Gestione API nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="88447-192">This step requires the access token you generated earlier and the thumbprint for your cluster certificate you uploaded to API Management in the previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="88447-193">Se nel passaggio precedente è stato usato un certificato client separato per Gestione API, in questo passaggio sarà necessario specificare l'identificazione personale per il certificato client oltre all'identificazione personale per il certificato cluster.</span><span class="sxs-lookup"><span data-stu-id="88447-193">If you used a separate client certificate in the previous step for API Management, you need the thumbprint for the client certificate in addition to the cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="88447-194">Inviare la richiesta HTTP PUT all'URL API di Gestione API annotato in precedenza durante l'abilitazione dell'API REST di Gestione API per configurare il servizio back-end di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-194">Send the following HTTP PUT request to the API Management API URL you noted earlier when enabling the API Management REST API to configure the Service Fabric backend service.</span></span> <span data-ttu-id="88447-195">Al completamento del comando, dovrebbe essere visualizzata la risposta `HTTP 201 Created`.</span><span class="sxs-lookup"><span data-stu-id="88447-195">You should see an `HTTP 201 Created` response when the command succeeds.</span></span> <span data-ttu-id="88447-196">Per ulteriori informazioni su ciascun campo, vedere la [documentazione di riferimento dell'API di back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="88447-196">For more information on each field, see the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="88447-197">Comando e URL HTTP:</span><span class="sxs-lookup"><span data-stu-id="88447-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="88447-198">Intestazioni della richiesta:</span><span class="sxs-lookup"><span data-stu-id="88447-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="88447-199">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="88447-199">Request body:</span></span>
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

<span data-ttu-id="88447-200">Il parametro **url** è il nome completo di un servizio nel cluster al quale, per impostazione predefinita, vengono indirizzate tutte le richieste se non viene specificato alcun servizio in un criterio di back-end.</span><span class="sxs-lookup"><span data-stu-id="88447-200">The **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed to by default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="88447-201">È possibile usare un nome di servizio fittizio, ad esempio "fabric:/fake/service", non se non si desidera un servizio di fallback.</span><span class="sxs-lookup"><span data-stu-id="88447-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend to have a fallback service.</span></span>

<span data-ttu-id="88447-202">Per ulteriori informazioni su ciascun campo, vedere la [documentazione di riferimento dell'API di back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="88447-202">Refer to the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="88447-203">Esempio</span><span class="sxs-lookup"><span data-stu-id="88447-203">Example</span></span>

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

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="88447-204">Distribuire un servizio back-end di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="88447-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="88447-205">Dopo aver configurato Service Fabric come back-end di Gestione API, è possibile creare criteri di back-end per le API che inviano il traffico nei propri servizi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-205">Now that you have the Service Fabric configured as a backend to API Management, you can author backend policies for your APIs that send traffic to your Service Fabric services.</span></span> <span data-ttu-id="88447-206">A questo scopo, è innanzitutto necessario un servizio in esecuzione in Service Fabric per accettare le richieste.</span><span class="sxs-lookup"><span data-stu-id="88447-206">But first you need a service running in Service Fabric to accept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="88447-207">Creare un servizio Service Fabric con un endpoint HTTP</span><span class="sxs-lookup"><span data-stu-id="88447-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="88447-208">Per questa esercitazione verrà creato un Reliable Service senza stato di base per ASP.NET Core usando il modello di progetto API Web predefinito.</span><span class="sxs-lookup"><span data-stu-id="88447-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using the default Web API project template.</span></span> <span data-ttu-id="88447-209">Questo permetterà di generare un endpoint HTTP per il servizio, che verrà esposto tramite Gestione API di Azure:</span><span class="sxs-lookup"><span data-stu-id="88447-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="88447-210">Partire dall'[impostazione dell'ambiente per lo sviluppo di ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="88447-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="88447-211">Dopo aver impostato l'ambiente di sviluppo, avviare Visual Studio come Amministratore e creare un servizio ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="88447-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="88447-212">In Visual Studio selezionare File -> Nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="88447-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="88447-213">Selezionare il modello Applicazione di Service Fabric nel Cloud e denominarlo **"ApiApplication"**.</span><span class="sxs-lookup"><span data-stu-id="88447-213">Select the Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="88447-214">Selezionare il modello di servizio ASP.NET Core e denominare il progetto **"WebApiService"**.</span><span class="sxs-lookup"><span data-stu-id="88447-214">Select the ASP.NET Core service template and name the project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="88447-215">Selezionare il modello di progetto Web API ASP.NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="88447-215">Select the Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="88447-216">Una volta creato il progetto, aprire `PackageRoot\ServiceManifest.xml` e rimuovere l'attributo `Port` dalla configurazione delle risorse endpoint:</span><span class="sxs-lookup"><span data-stu-id="88447-216">Once the project is created, open `PackageRoot\ServiceManifest.xml` and remove the `Port` attribute from the endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="88447-217">Questo consente a Service Fabric di specificare in modo dinamico una porta dell'intervallo di porte dell'applicazione, che è stata aperta nel gruppo NSG del modello di Resource Manager del cluster, permettendo il flusso del traffico in tale porta da Gestione API.</span><span class="sxs-lookup"><span data-stu-id="88447-217">This allows Service Fabric to specify a port dynamically from the application port range, which we opened through the Network Security Group in the cluster Resource Manager template, allowing traffic to flow to it from API Management.</span></span>
 
 6. <span data-ttu-id="88447-218">Premere F5 in Visual Studio per verificare che l'API Web sia disponibile in locale.</span><span class="sxs-lookup"><span data-stu-id="88447-218">Press F5 in Visual Studio to verify the web API is available locally.</span></span> 

    <span data-ttu-id="88447-219">Aprire Service Fabric Explorer ed eseguire il drill-down fino a un'istanza specifica del servizio ASP.NET Core per visualizzare l'indirizzo di base di ascolto del servizio.</span><span class="sxs-lookup"><span data-stu-id="88447-219">Open Service Fabric Explorer and drill down to a specific instance of the ASP.NET Core service to see the base address the service is listening on.</span></span> <span data-ttu-id="88447-220">Aggiungere `/api/values` all'indirizzo di base e aprirlo in un browser.</span><span class="sxs-lookup"><span data-stu-id="88447-220">Add `/api/values` to the base address and open it in a browser.</span></span> <span data-ttu-id="88447-221">Questa operazione chiama il metodo Get su ValuesController nel modello API Web</span><span class="sxs-lookup"><span data-stu-id="88447-221">This invokes the Get method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="88447-222">e restituisce la risposta predefinita trasmessa dal modello, ovvero una matrice JSON contenente due stringhe:</span><span class="sxs-lookup"><span data-stu-id="88447-222">It returns the default response that is provided by the template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="88447-223">Questo è l'endpoint che verrà esposto tramite Gestione API in Azure.</span><span class="sxs-lookup"><span data-stu-id="88447-223">This is the endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="88447-224">Infine, distribuire l'applicazione nel cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="88447-224">Finally, deploy the application to your cluster in Azure.</span></span> <span data-ttu-id="88447-225">[Usando Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), fare clic con il pulsante destro del mouse sul progetto Applicazione e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="88447-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click the Application project and select **Publish**.</span></span> <span data-ttu-id="88447-226">Specificare l'endpoint del cluster, ad esempio `mycluster.westus.cloudapp.azure.com:19000`, per distribuire l'applicazione nel cluster di Service Fabric in Azure.</span><span class="sxs-lookup"><span data-stu-id="88447-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) to deploy the application to your Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="88447-227">In tale cluster dovrebbe essere ora in esecuzione un servizio ASP.NET Core senza stato denominato `fabric:/ApiApplication/WebApiService`.</span><span class="sxs-lookup"><span data-stu-id="88447-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="88447-228">Creare un'operazione per le API</span><span class="sxs-lookup"><span data-stu-id="88447-228">Create an API operation</span></span>

<span data-ttu-id="88447-229">A questo punto è possibile creare in Gestione API un'operazione usata dai client esterni per comunicare con il servizio ASP.NET Core senza stato in esecuzione nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-229">Now we're ready to create an operation in API Management that external clients use to communicate with the ASP.NET Core stateless service running in the Service Fabric cluster.</span></span>

 1. <span data-ttu-id="88447-230">Accedere al portale di Azure e passare alla distribuzione del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="88447-230">Log in to the Azure portal and navigate to your API Management service deployment.</span></span>
 2. <span data-ttu-id="88447-231">Nel pannello del servizio Gestione API selezionare **API - Anteprima**.</span><span class="sxs-lookup"><span data-stu-id="88447-231">In the API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="88447-232">Aggiungere una nuova API facendo sulla casella **API vuota** e completare la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="88447-232">Add a new API by clicking the **Blank API** box and filling out the dialog box:</span></span>

     - <span data-ttu-id="88447-233">**URL del servizio Web**: per i back-end di Service Fabric, questo valore URL non viene usato.</span><span class="sxs-lookup"><span data-stu-id="88447-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="88447-234">È possibile inserire un valore qualsiasi nel campo.</span><span class="sxs-lookup"><span data-stu-id="88447-234">You can put any value here.</span></span> <span data-ttu-id="88447-235">Per questa esercitazione, usare `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="88447-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="88447-236">**Nome**: inserire il nome dell'API.</span><span class="sxs-lookup"><span data-stu-id="88447-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="88447-237">Per questa esercitazione, usare `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="88447-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="88447-238">**Schema URL**: selezionare HTTP, HTTPS o entrambi i valori.</span><span class="sxs-lookup"><span data-stu-id="88447-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="88447-239">Per questa esercitazione, usare `both`.</span><span class="sxs-lookup"><span data-stu-id="88447-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="88447-240">**Suffisso URL API**: inserire un suffisso per l'API.</span><span class="sxs-lookup"><span data-stu-id="88447-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="88447-241">Per questa esercitazione, usare `myapp`.</span><span class="sxs-lookup"><span data-stu-id="88447-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="88447-242">Una volta creata l'API, fare clic su **+ Aggiungi operazione** per aggiungere un'operazione API front-end.</span><span class="sxs-lookup"><span data-stu-id="88447-242">Once the API is created, click **+ Add operation** to add a front-end API operation.</span></span> <span data-ttu-id="88447-243">Compilare i valori come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="88447-243">Fill out the values:</span></span>
    
     - <span data-ttu-id="88447-244">**URL**: selezionare `GET` e specificare un percorso URL per l'API.</span><span class="sxs-lookup"><span data-stu-id="88447-244">**URL**: Select `GET` and provide a URL path for the API.</span></span> <span data-ttu-id="88447-245">Per questa esercitazione, usare `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="88447-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="88447-246">Per impostazione predefinita, il percorso URL specificato qui è il percorso URL inviato al servizio Service Fabric di back-end.</span><span class="sxs-lookup"><span data-stu-id="88447-246">By default, the URL path specified here is the URL path sent to the backend Service Fabric service.</span></span> <span data-ttu-id="88447-247">Se si specifica lo stesso percorso URL usato dal servizio, in questo caso `/api/values`, non è necessario apportare ulteriori modifiche.</span><span class="sxs-lookup"><span data-stu-id="88447-247">If you use the same URL path here that your service uses, in this case `/api/values`, then the operation works without further modification.</span></span> <span data-ttu-id="88447-248">È anche possibile specificare un percorso URL diverso da quello usato dal servizio Service Fabric di back-end. In questo caso, sarà necessario immettere successivamente anche un'indicazione di riscrittura del percorso nel criterio dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="88447-248">You may also specify a URL path here that is different from the URL path used by your backend Service Fabric service, in which case you will also need to specify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="88447-249">**Nome visualizzato**: specificare un nome per l'API.</span><span class="sxs-lookup"><span data-stu-id="88447-249">**Display name**: Provide any name for the API.</span></span> <span data-ttu-id="88447-250">Per questa esercitazione, usare `Values`.</span><span class="sxs-lookup"><span data-stu-id="88447-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="88447-251">Configurare un criterio di back-end</span><span class="sxs-lookup"><span data-stu-id="88447-251">Configure a backend policy</span></span>

<span data-ttu-id="88447-252">Il criterio di back-end collega tutti gli elementi</span><span class="sxs-lookup"><span data-stu-id="88447-252">The backend policy ties everything together.</span></span> <span data-ttu-id="88447-253">e consente di configurare il servizio Service Fabric di back-end a cui vengono indirizzate le richieste.</span><span class="sxs-lookup"><span data-stu-id="88447-253">This is where you configure the backend Service Fabric service to which requests are routed.</span></span> <span data-ttu-id="88447-254">È possibile applicare questo criterio a qualsiasi operazione API.</span><span class="sxs-lookup"><span data-stu-id="88447-254">You can apply this policy to any API operation.</span></span> <span data-ttu-id="88447-255">La [configurazione back-end per Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) fornisce i controlli di indirizzamento delle richieste seguenti:</span><span class="sxs-lookup"><span data-stu-id="88447-255">The [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides the following request routing controls:</span></span> 
 - <span data-ttu-id="88447-256">Selezione dell'istanza del servizio mediante la specifica di un nome di istanza del servizio Service Fabric, hardcoded (ad esempio, `"fabric:/myapp/myservice"`) o generato dalla richiesta HTTP (ad esempio, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="88447-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from the HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="88447-257">Risoluzione della partizione mediante la generazione di una chiave di partizione che usa uno schema di partizionamento di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88447-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="88447-258">Selezione della replica per i servizi con stato.</span><span class="sxs-lookup"><span data-stu-id="88447-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="88447-259">Condizioni per i nuovi tentativi di risoluzione della posizione di un servizio e il nuovo invio di una richiesta.</span><span class="sxs-lookup"><span data-stu-id="88447-259">Resolution retry conditions that allow you to specify the conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="88447-260">Per questa esercitazione, creare un criterio di back-end che consenta di indirizzare le richieste direttamente al servizio ASP.NET Core senza stato distribuito in precedenza:</span><span class="sxs-lookup"><span data-stu-id="88447-260">For this tutorial, create a backend policy that routes requests directly to the ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="88447-261">Selezionare e modificare i **criteri in ingresso** per l'operazione `Values` facendo clic sull'icona di modifica, quindi scegliere **Visualizzazione Codice**.</span><span class="sxs-lookup"><span data-stu-id="88447-261">Select and edit the **inbound policies** for the `Values` operation by clicking the edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="88447-262">Nell'editor del codice dei criteri aggiungere un criterio `set-backend-service` nei criteri in ingresso, come illustrato di seguito, e fare clic sul pulsante **Salva**:</span><span class="sxs-lookup"><span data-stu-id="88447-262">In the policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click the **Save** button:</span></span>
    
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

<span data-ttu-id="88447-263">Per un set completo di attributi di criteri di back-end di Service Fabric, vedere la [documentazione back-end di Gestione API](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService).</span><span class="sxs-lookup"><span data-stu-id="88447-263">For a full set of Service Fabric back-end policy attributes, refer to the [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-the-api-to-a-product"></a><span data-ttu-id="88447-264">Aggiungere l'API a un prodotto.</span><span class="sxs-lookup"><span data-stu-id="88447-264">Add the API to a product.</span></span> 

<span data-ttu-id="88447-265">Prima di chiamare l'API, è innanzitutto necessario aggiungerla a un prodotto per il quale sia possibile concedere l'accesso agli utenti.</span><span class="sxs-lookup"><span data-stu-id="88447-265">Before you can call the API, it must be added to a product where you can grant access to users.</span></span> 

 1. <span data-ttu-id="88447-266">Nel servizio Gestione API selezionare **Prodotti - ANTEPRIMA**.</span><span class="sxs-lookup"><span data-stu-id="88447-266">In the API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="88447-267">Per impostazione predefinita, Gestione API include due prodotti: Starter e Illimitato.</span><span class="sxs-lookup"><span data-stu-id="88447-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="88447-268">Selezionare il prodotto Illimitato.</span><span class="sxs-lookup"><span data-stu-id="88447-268">Select the Unlimited product.</span></span>
 3. <span data-ttu-id="88447-269">Selezionare API.</span><span class="sxs-lookup"><span data-stu-id="88447-269">Select APIs.</span></span>
 4. <span data-ttu-id="88447-270">Fare clic sul pulsante **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="88447-270">Click the **+ Add** button.</span></span>
 5. <span data-ttu-id="88447-271">Selezionare l'API `Service Fabric App` creata nei passaggi precedenti e fare clic sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="88447-271">Select the `Service Fabric App` API you created in the previous steps and click the **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="88447-272">Eseguirne il test</span><span class="sxs-lookup"><span data-stu-id="88447-272">Test it</span></span>

<span data-ttu-id="88447-273">È ora possibile provare a inviare una richiesta al servizio back-end in Service Fabric tramite Gestione API direttamente dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="88447-273">You can now try sending a request to your back-end service in Service Fabric through API Management directly from the Azure portal.</span></span>

 1. <span data-ttu-id="88447-274">Nel servizio Gestione API selezionare **API - ANTEPRIMA**.</span><span class="sxs-lookup"><span data-stu-id="88447-274">In the API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="88447-275">Selezionare l'API `Service Fabric App` creata nei passaggi precedenti e fare clic sul pulsante **Test**.</span><span class="sxs-lookup"><span data-stu-id="88447-275">In the `Service Fabric App` API you created in the previous steps, select the **Test** tab.</span></span>
 3. <span data-ttu-id="88447-276">Fare clic sul pulsante **Invia** per inviare una richiesta di test al servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="88447-276">Click the **Send** button to send a test request to the backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88447-277">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="88447-277">Next steps</span></span>

<span data-ttu-id="88447-278">A questo punto, dovrebbe essere disponibile un'installazione di base con i servizi Service Fabric e Gestione API.</span><span class="sxs-lookup"><span data-stu-id="88447-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="88447-279">In questa esercitazione viene usata l'autenticazione utente basata su certificato per il cluster di Service Fabric per consentire una procedura di configurazione rapida.</span><span class="sxs-lookup"><span data-stu-id="88447-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster to get you set up quickly.</span></span> <span data-ttu-id="88447-280">È consigliabile eseguire un'autenticazione utente più avanzata per il cluster di Service Fabric basata su [Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="88447-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="88447-281">Successivamente, [creare e configurare impostazioni di prodotto avanzate in Gestione API di Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) per preparare l'applicazione al traffico reale.</span><span class="sxs-lookup"><span data-stu-id="88447-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) to prepare your application for real world traffic.</span></span>

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
