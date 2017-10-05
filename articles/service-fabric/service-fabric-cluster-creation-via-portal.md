---
title: Creare un cluster di Service Fabric nel portale di Azure | Documentazione Microsoft
description: Questo articolo descrive come configurare un cluster di Service Fabric protetto in Azure tramite il portale di Azure e l'insieme di credenziali delle chiavi di Azure.
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 7dda9520ce3d93bf0e86bd2481ad06c268d087c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-the-azure-portal"></a><span data-ttu-id="3fc73-103">Creare un cluster di Service Fabric in Azure tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3fc73-103">Create a Service Fabric cluster in Azure using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3fc73-104">Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="3fc73-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="3fc73-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3fc73-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="3fc73-106">Questo articolo contiene una guida dettagliata che illustra i passaggi per la configurazione di un cluster di Service Fabric protetto in Azure tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc73-106">This is a step-by-step guide that walks you through the steps of setting up a secure Service Fabric cluster in Azure using the Azure portal.</span></span> <span data-ttu-id="3fc73-107">La guida fornisce istruzioni dettagliate sulle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3fc73-107">This guide walks you through the following steps:</span></span>

* <span data-ttu-id="3fc73-108">Configurare l'insieme di credenziali delle chiavi per la gestione delle chiavi ai fini della protezione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-108">Set up Key Vault to manage keys for cluster security.</span></span>
* <span data-ttu-id="3fc73-109">Creare un cluster protetto in Azure tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc73-109">Create a secured cluster in Azure through the Azure portal.</span></span>
* <span data-ttu-id="3fc73-110">Autenticare gli amministratori che usano i certificati.</span><span class="sxs-lookup"><span data-stu-id="3fc73-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="3fc73-111">Per le opzioni di sicurezza avanzata, ad esempio l'autenticazione dell'utente con Azure Active Directory e la configurazione dei certificati per la protezione delle applicazioni, [creare il cluster usando Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="3fc73-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="3fc73-112">Un cluster protetto è un cluster che impedisce l'accesso non autorizzato alle operazioni di gestione, tra cui distribuzione, aggiornamento ed eliminazione di applicazioni, servizi e dati in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="3fc73-112">A secure cluster is a cluster that prevents unauthorized access to management operations, which includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="3fc73-113">Un cluster non protetto è un cluster a cui tutti gli utenti possono connettersi in qualsiasi momento ed eseguire operazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="3fc73-113">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="3fc73-114">Sebbene sia possibile creare un cluster non protetto, è **consigliabile creare un cluster protetto**.</span><span class="sxs-lookup"><span data-stu-id="3fc73-114">Although it is possible to create an unsecure cluster, it is **highly recommended to create a secure cluster**.</span></span> <span data-ttu-id="3fc73-115">Un cluster non protetto **non può essere protetto in un secondo momento**. Sarà necessario crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="3fc73-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="3fc73-116">I concetti sono gli stessi per la creazione di cluster protetti, sia Linux che Windows.</span><span class="sxs-lookup"><span data-stu-id="3fc73-116">The concepts are the same for creating secure clusters, whether the clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="3fc73-117">Per altre informazioni e script helper per la creazione di cluster Linux protetti, vedere [Creare cluster protetti in Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="3fc73-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="3fc73-118">I parametri ottenuti dallo script helper fornito possono essere immessi direttamente nel portale come descritto nella sezione [Creare un cluster nel portale di Azure](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="3fc73-118">The parameters obtained by the helper script provided can be input directly into the portal as described in the section [Create a cluster in the Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="3fc73-119">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="3fc73-119">Log in to Azure</span></span>
<span data-ttu-id="3fc73-120">Questa guida usa [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="3fc73-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="3fc73-121">Quando si avvia una nuova sessione di PowerShell, accedere al proprio account Azure e selezionare la sottoscrizione prima di eseguire i comandi di Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc73-121">When starting a new PowerShell session, log in to your Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="3fc73-122">Accedere all'account Azure:</span><span class="sxs-lookup"><span data-stu-id="3fc73-122">Log in to your azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3fc73-123">Selezionare la propria sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="3fc73-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="3fc73-124">Configurare l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3fc73-124">Set up Key Vault</span></span>
<span data-ttu-id="3fc73-125">Questa parte della guida illustra la creazione di un insieme di credenziali delle chiavi per un cluster di Service Fabric in Azure e per le applicazioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3fc73-125">This part of the guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="3fc73-126">Per una guida completa sull'insieme di credenziali delle chiavi, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="3fc73-126">For a complete guide on Key Vault, see the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="3fc73-127">Per la protezione del cluster, Service Fabric usa certificati X.509.</span><span class="sxs-lookup"><span data-stu-id="3fc73-127">Service Fabric uses X.509 certificates to secure a cluster.</span></span> <span data-ttu-id="3fc73-128">L'insieme di credenziali delle chiavi di Azure viene usato per gestire i certificati dei cluster di Service Fabric in Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc73-128">Azure Key Vault is used to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="3fc73-129">Quando viene distribuito un cluster in Azure, il provider di risorse di Azure responsabile della creazione di cluster Service Fabric estrae i certificati dall'insieme di credenziali delle chiavi e li installa nelle macchine virtuali del cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-129">When a cluster is deployed in Azure, the Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="3fc73-130">Nel diagramma seguente viene illustrata la relazione tra l'insieme di credenziali delle chiavi, un cluster di Service Fabric e il provider di risorse di Azure che usa i certificati archiviati nell'insieme di credenziali delle chiavi durante la creazione di un cluster:</span><span class="sxs-lookup"><span data-stu-id="3fc73-130">The following diagram illustrates the relationship between Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Installazione del certificato][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="3fc73-132">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="3fc73-132">Create a Resource Group</span></span>
<span data-ttu-id="3fc73-133">Il primo passaggio consiste nel creare un nuovo gruppo di risorse specifico per l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="3fc73-133">The first step is to create a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="3fc73-134">È consigliabile inserire l'insieme di credenziali delle chiavi nel proprio gruppo di risorse in modo che sia possibile rimuovere i gruppi di risorse di calcolo e archiviazione, ad esempio il gruppo di risorse con il cluster Service Fabric, senza perdere le chiavi e i segreti.</span><span class="sxs-lookup"><span data-stu-id="3fc73-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as the resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="3fc73-135">Il gruppo di risorse che contiene l'insieme di credenziali delle chiavi deve essere situato nella stessa area del cluster che lo usa.</span><span class="sxs-lookup"><span data-stu-id="3fc73-135">The resource group that has your Key Vault must be in the same region as the cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: The output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="3fc73-136">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3fc73-136">Create Key Vault</span></span>
<span data-ttu-id="3fc73-137">Creare un insieme di credenziali delle chiavi nel nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3fc73-137">Create a Key Vault in the new resource group.</span></span> <span data-ttu-id="3fc73-138">L'insieme di credenziali delle chiavi **deve essere abilitato per la distribuzione** per consentire al provider di risorse di Service Fabric di ottenere i certificati e installarli nei nodi del cluster:</span><span class="sxs-lookup"><span data-stu-id="3fc73-138">The Key Vault **must be enabled for deployment** to allow the Service Fabric resource provider to get certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```

<span data-ttu-id="3fc73-139">Se si dispone già di un insieme di credenziali delle chiavi, è possibile abilitarlo per la distribuzione tramite l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="3fc73-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-to-key-vault"></a><span data-ttu-id="3fc73-140">Aggiungere i certificati all'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3fc73-140">Add certificates to Key Vault</span></span>
<span data-ttu-id="3fc73-141">I certificati vengono usati in Service Fabric per fornire l'autenticazione e la crittografia e proteggere i vari aspetti di un cluster e delle sue applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3fc73-141">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="3fc73-142">Per altre informazioni sull'uso dei certificati in Service Fabric, vedere [Scenari di sicurezza di un cluster di Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="3fc73-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="3fc73-143">Cluster e certificato del server (obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="3fc73-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="3fc73-144">Questo certificato è richiesto per proteggere un cluster e impedirne accessi non autorizzati.</span><span class="sxs-lookup"><span data-stu-id="3fc73-144">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="3fc73-145">Il certificato fornisce protezione del cluster in due modi:</span><span class="sxs-lookup"><span data-stu-id="3fc73-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="3fc73-146">**Autenticazione del cluster:** autentica la comunicazione da nodo a nodo per la federazione di cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="3fc73-147">Solo i nodi che possono dimostrare la propria identità con il certificato possono essere aggiunti al cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-147">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="3fc73-148">**Autenticazione del server:** autentica gli endpoint di gestione del cluster in un client di gestione, in modo che il client di gestione sappia con certezza di comunicare con il cluster reale.</span><span class="sxs-lookup"><span data-stu-id="3fc73-148">**Server authentication:** Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="3fc73-149">Questo certificato fornisce anche SSL per l'API di gestione HTTPS e per Service Fabric Explorer tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3fc73-149">This certificate also provides SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="3fc73-150">A tale scopo, il certificato deve soddisfare i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3fc73-150">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="3fc73-151">Il certificato deve includere una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="3fc73-151">The certificate must contain a private key.</span></span>
* <span data-ttu-id="3fc73-152">Il certificato deve essere stato creato per lo scambio di chiave, esportabile in un file con estensione pfx (Personal Information Exchange).</span><span class="sxs-lookup"><span data-stu-id="3fc73-152">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="3fc73-153">Il nome del soggetto del certificato deve corrispondere al dominio usato per accedere al cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3fc73-153">The certificate's subject name must match the domain used to access the Service Fabric cluster.</span></span> <span data-ttu-id="3fc73-154">È necessario fornire il SSL per gli endpoint di gestione HTTPS del cluster e Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="3fc73-154">This is required to provide SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="3fc73-155">Non è possibile ottenere un certificato SSL da un'Autorità di certificazione (CA) per il dominio `.cloudapp.azure.com` .</span><span class="sxs-lookup"><span data-stu-id="3fc73-155">You cannot obtain an SSL certificate from a certificate authority (CA) for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="3fc73-156">Acquistare un nome di dominio personalizzato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="3fc73-157">Quando si richiede un certificato da una CA, il nome del soggetto del certificato deve corrispondere al nome di dominio personalizzato usato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-157">When you request a certificate from a CA the certificate's subject name must match the custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="3fc73-158">Certificati di autenticazione client</span><span class="sxs-lookup"><span data-stu-id="3fc73-158">Client authentication certificates</span></span>
<span data-ttu-id="3fc73-159">I certificati client aggiuntivi autenticano gli amministratori per le attività di gestione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="3fc73-160">Service Fabric ha due livelli di accesso: **admin** e **utente di sola lettura**.</span><span class="sxs-lookup"><span data-stu-id="3fc73-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="3fc73-161">Deve essere usato almeno un certificato per l'accesso amministrativo.</span><span class="sxs-lookup"><span data-stu-id="3fc73-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="3fc73-162">Per l'accesso aggiuntivo a livello di utente, è necessario specificare un certificato separato.</span><span class="sxs-lookup"><span data-stu-id="3fc73-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="3fc73-163">Per altre informazioni sui ruoli di accesso, vedere [Controllo degli accessi in base al ruolo per i client di Service Fabric][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="3fc73-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="3fc73-164">Per usare Service Fabric non è necessario caricare I certificati di autenticazione client nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="3fc73-164">You do not need to upload Client authentication certificates to Key Vault to work with Service Fabric.</span></span> <span data-ttu-id="3fc73-165">Questi certificati devono essere forniti solo agli utenti autorizzati alla gestione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-165">These certificates only need to be provided to users who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="3fc73-166">Azure Active Directory è il metodo consigliato per autenticare i client per le operazioni di gestione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-166">Azure Active Directory is the recommended way to authenticate clients for cluster management operations.</span></span> <span data-ttu-id="3fc73-167">Per usare Azure Active Directory, è necessario [creare un cluster tramite Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="3fc73-167">To use Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="3fc73-168">Certificati delle applicazioni (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="3fc73-168">Application certificates (optional)</span></span>
<span data-ttu-id="3fc73-169">Per motivi di sicurezza dell'applicazione, è possibile installare nel cluster numerosi certificati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="3fc73-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="3fc73-170">Prima di creare il cluster, considerare gli scenari di protezione delle applicazioni che richiedono l'installazione di un certificato sui nodi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3fc73-170">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="3fc73-171">Crittografia e decrittografia dei valori di configurazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="3fc73-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="3fc73-172">Crittografia dei dati tra i nodi durante la replica</span><span class="sxs-lookup"><span data-stu-id="3fc73-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="3fc73-173">I certificati delle applicazioni non possono essere configurati durante la creazione di un cluster tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc73-173">Application certificates cannot be configured when creating a cluster through the Azure portal.</span></span> <span data-ttu-id="3fc73-174">Per configurare i certificati delle applicazioni in fase di installazione del cluster, è necessario [creare un cluster tramite Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="3fc73-174">To configure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="3fc73-175">È anche possibile aggiungere certificati delle applicazione al cluster dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="3fc73-175">You can also add application certificates to the cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="3fc73-176">Formattazione dei certificati per l'uso di provider di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="3fc73-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="3fc73-177">I file di chiave privata (con estensione pfx) possono essere aggiunti e usati direttamente tramite l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="3fc73-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="3fc73-178">Tuttavia, il provider di risorse di Azure richiede l'archiviazione delle chiavi in un particolare formato JSON che include il file con estensione pfx come stringa con codifica Base64 e la password della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="3fc73-178">However, the Azure resource provider requires keys to be stored in a special JSON format that includes the .pfx as a base-64 encoded string and the private key password.</span></span> <span data-ttu-id="3fc73-179">Per soddisfare questi requisiti, le chiavi devono essere inserite in una stringa JSON e quindi archiviate come *segreti* nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="3fc73-179">To accommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="3fc73-180">Per semplificare questo processo, è [disponibile su GitHub][service-fabric-rp-helpers] un modulo di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3fc73-180">To make this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="3fc73-181">Per usare il modulo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3fc73-181">Follow these steps to use the module:</span></span>

1. <span data-ttu-id="3fc73-182">Scaricare l'intero contenuto del repository in una directory locale.</span><span class="sxs-lookup"><span data-stu-id="3fc73-182">Download the entire contents of the repo into a local directory.</span></span> 
2. <span data-ttu-id="3fc73-183">Importare il modulo nella finestra di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3fc73-183">Import the module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="3fc73-184">Il comando `Invoke-AddCertToKeyVault` in questo modulo di PowerShell formatta in modo automatico una chiave privata del certificato in una stringa JSON e la carica nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="3fc73-184">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to Key Vault.</span></span> <span data-ttu-id="3fc73-185">Usare il comando per aggiungere il certificato del cluster ed eventuali certificati aggiuntivi delle applicazioni all'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="3fc73-185">Use it to add the cluster certificate and any additional application certificates to Key Vault.</span></span> <span data-ttu-id="3fc73-186">Ripetere questo passaggio per tutti i certificati aggiuntivi che si vuole installare nel cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-186">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: The output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to myvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="3fc73-187">Questi sono tutti i prerequisiti dell'insieme di credenziali delle chiavi per la configurazione di un modello di Cluster Resource Manager di Service Fabric che consente di installare certificati per l'autenticazione dei nodi, per la protezione degli endpoint di gestione e per l'autenticazione, nonché qualsiasi funzionalità aggiuntiva per la sicurezza delle applicazioni che usano certificati X.509.</span><span class="sxs-lookup"><span data-stu-id="3fc73-187">These are all the Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="3fc73-188">A questo punto, dovrebbe essere visualizzata l'impostazione seguente in Azure:</span><span class="sxs-lookup"><span data-stu-id="3fc73-188">At this point, you should now have the following setup in Azure:</span></span>

* <span data-ttu-id="3fc73-189">Gruppo di risorse dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3fc73-189">Key Vault resource group</span></span>
  * <span data-ttu-id="3fc73-190">Insieme di credenziali di chiave</span><span class="sxs-lookup"><span data-stu-id="3fc73-190">Key Vault</span></span>
    * <span data-ttu-id="3fc73-191">Certificato di autenticazione del server del cluster</span><span class="sxs-lookup"><span data-stu-id="3fc73-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="3fc73-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="3fc73-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-the-azure-portal"></a><span data-ttu-id="3fc73-193">Creare un cluster nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3fc73-193">Create cluster in the Azure portal</span></span>
### <a name="search-for-the-service-fabric-cluster-resource"></a><span data-ttu-id="3fc73-194">Cercare la risorsa cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3fc73-194">Search for the Service Fabric cluster resource</span></span>
![ricerca del modello di cluster di Service Fabric nel portale di Azure.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="3fc73-196">Accedere al [portale di Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="3fc73-196">Sign in to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="3fc73-197">Fare clic su **+ Nuovo** per aggiungere un nuovo modello di risorsa.</span><span class="sxs-lookup"><span data-stu-id="3fc73-197">Click **New** to add a new resource template.</span></span> <span data-ttu-id="3fc73-198">Cercare il modello del cluster di Service Fabric in **Marketplace**, nella sezione **Tutto**.</span><span class="sxs-lookup"><span data-stu-id="3fc73-198">Search for the Service Fabric Cluster template in the **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="3fc73-199">Selezionare **Cluster di Service Fabric** nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="3fc73-199">Select **Service Fabric Cluster** from the list.</span></span>
4. <span data-ttu-id="3fc73-200">Passare al pannello **Cluster di Service Fabric** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3fc73-200">Navigate to the **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="3fc73-201">Il pannello **Crea cluster di Service Fabric** include i quattro passaggi descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="3fc73-201">The **Create Service Fabric cluster** blade has the following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="3fc73-202">1. Nozioni di base</span><span class="sxs-lookup"><span data-stu-id="3fc73-202">1. Basics</span></span>
![Schermata della creazione di un nuovo gruppo di risorse.][CreateRG]

<span data-ttu-id="3fc73-204">Nel pannello Informazioni di base è necessario fornire i dettagli di base per il cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-204">In the Basics blade you need to provide the basic details for your cluster.</span></span>

1. <span data-ttu-id="3fc73-205">Immettere il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-205">Enter the name of your cluster.</span></span>
2. <span data-ttu-id="3fc73-206">Scegliere un **nome utente** e una **Password** per il desktop remoto delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3fc73-206">Enter a **user name** and **password** for Remote Desktop for the VMs.</span></span>
3. <span data-ttu-id="3fc73-207">Assicurarsi di selezionare la **sottoscrizione** in cui si vuole distribuire il cluster, soprattutto se sono presenti più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="3fc73-207">Make sure to select the **Subscription** that you want your cluster to be deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="3fc73-208">Creare un **nuovo gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="3fc73-208">Create a **new resource group**.</span></span> <span data-ttu-id="3fc73-209">Assegnare al gruppo lo stesso nome del cluster per poterlo trovare più facilmente in seguito, soprattutto quando si cerca di apportare modifiche alla distribuzione e/o eliminare il cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-209">It is best to give it the same name as the cluster, since it helps in finding them later, especially when you are trying to make changes to your deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3fc73-210">Anche se è possibile decidere di usare un gruppo di risorse esistente, è meglio crearne uno nuovo,</span><span class="sxs-lookup"><span data-stu-id="3fc73-210">Although you can decide to use an existing resource group, it is a good practice to create a new resource group.</span></span> <span data-ttu-id="3fc73-211">in modo da poter eliminare facilmente i cluster non più necessari.</span><span class="sxs-lookup"><span data-stu-id="3fc73-211">This makes it easy to delete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="3fc73-212">Selezionare l' **area** in cui si desidera creare il cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-212">Select the **region** in which you want to create the cluster.</span></span> <span data-ttu-id="3fc73-213">È necessario usare la stessa area in cui è situato l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="3fc73-213">You must use the same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="3fc73-214">2. Configurazione del cluster</span><span class="sxs-lookup"><span data-stu-id="3fc73-214">2. Cluster configuration</span></span>
![Creare un tipo di nodo][CreateNodeType]

<span data-ttu-id="3fc73-216">Configurare i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-216">Configure your cluster nodes.</span></span> <span data-ttu-id="3fc73-217">poiché definiscono le dimensioni delle VM, il numero di VM e le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="3fc73-217">Node types define the VM sizes, the number of VMs, and their properties.</span></span> <span data-ttu-id="3fc73-218">Il cluster può avere più di un tipo di nodo, ma il tipo di nodo primario, ovvero il primo che si definisce nel portale, deve essere costituito da almeno cinque macchine virtuali, poiché in questo tipo di nodo si trovano i servizi di sistema di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3fc73-218">Your cluster can have more than one node type, but the primary node type (the first one that you define on the portal) must have at least five VMs, as this is the node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="3fc73-219">Non è necessario configurare le **proprietà relative alla posizione**, perché una proprietà relativa alla posizione predefinita "NodeTypeName" viene aggiunta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3fc73-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="3fc73-220">Uno scenario comune per diversi tipi di nodi è costituito da un'applicazione contenente un servizio front-end e un servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="3fc73-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="3fc73-221">Si vuole inserire il servizio front-end in macchine virtuali più piccole, ad esempio con dimensioni D2, con porte aperte a Internet e il servizio back-end in macchine virtuali più grandi, ad esempio con dimensioni D4, D6, D15 e così via, senza porte con connessione Internet aperte.</span><span class="sxs-lookup"><span data-stu-id="3fc73-221">You want to put the front-end service on smaller VMs (VM sizes like D2) with ports open to the Internet, but you want to put the back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="3fc73-222">Scegliere un nome per il tipo di nodo (da 1 a 12 caratteri, contenenti solo lettere e numeri).</span><span class="sxs-lookup"><span data-stu-id="3fc73-222">Choose a name for your node type (1 to 12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="3fc73-223">Le **dimensioni minime** delle macchine virtuali per il tipo di nodo primario sono determinate dal livello di **durabilità** scelto per il cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-223">The minimum **size** of VMs for the primary node type is driven by the **durability** tier you choose for the cluster.</span></span> <span data-ttu-id="3fc73-224">Il valore predefinito per il livello di durabilità è Bronze.</span><span class="sxs-lookup"><span data-stu-id="3fc73-224">The default for the durability tier is bronze.</span></span> <span data-ttu-id="3fc73-225">Per altre informazioni sulla durabilità, vedere [come scegliere l'affidabilità e la durabilità di un cluster di Service Fabric][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="3fc73-225">For more information on durability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="3fc73-226">Selezionare le dimensioni della macchina virtuale e il piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="3fc73-226">Select the VM size and pricing tier.</span></span> <span data-ttu-id="3fc73-227">Le macchine virtuali della serie D dispongono di unità SSD e sono consigliate per applicazioni con stato.</span><span class="sxs-lookup"><span data-stu-id="3fc73-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="3fc73-228">Non usare SKU di VM con core parziali o meno di 7 GB di capacità disco disponibile.</span><span class="sxs-lookup"><span data-stu-id="3fc73-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="3fc73-229">Il **numero** minimo di macchine virtuali per il tipo di nodo primario è determinato dal livello di **affidabilità** scelto per il cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-229">The minimum **number** of VMs for the primary node type is driven by the **reliability** tier you choose.</span></span> <span data-ttu-id="3fc73-230">Il valore predefinito per il livello di affidabilità è Silver.</span><span class="sxs-lookup"><span data-stu-id="3fc73-230">The default for the reliability tier is Silver.</span></span> <span data-ttu-id="3fc73-231">Per altre informazioni sull'affidabilità, vedere [come scegliere l'affidabilità e la durabilità di un cluster di Service Fabric][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="3fc73-231">For more information on reliability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="3fc73-232">Scegliere il numero di macchine virtuali per il tipo di nodo.</span><span class="sxs-lookup"><span data-stu-id="3fc73-232">Choose the number of VMs for the node type.</span></span> <span data-ttu-id="3fc73-233">È possibile aumentare o ridurre il numero di macchine virtuali in un tipo di nodo in un secondo momento ma, per il tipo di nodo primario, il minimo è determinato dal livello di affidabilità che si è scelto.</span><span class="sxs-lookup"><span data-stu-id="3fc73-233">You can scale up or down the number of VMs in a node type later on, but on the primary node type, the minimum is driven by the reliability level that you have chosen.</span></span> <span data-ttu-id="3fc73-234">Gli altri tipi di nodo possono avere un minimo di 1 VM.</span><span class="sxs-lookup"><span data-stu-id="3fc73-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="3fc73-235">Configurare gli endpoint personalizzati.</span><span class="sxs-lookup"><span data-stu-id="3fc73-235">Configure custom endpoints.</span></span> <span data-ttu-id="3fc73-236">Questo campo consente di immettere un elenco di porte delimitato da virgole che si desidera esporre tramite Azure Load Balancer alla rete Internet pubblica per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3fc73-236">This field allows you to enter a comma-separated list of ports that you want to expose through the Azure Load Balancer to the public Internet for your applications.</span></span> <span data-ttu-id="3fc73-237">Ad esempio, se si prevede di distribuire un'applicazione Web nel cluster, immettere "80" per consentire il traffico sulla porta 80 del cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-237">For example, if you plan to deploy a web application to your cluster, enter "80" here to allow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="3fc73-238">Per altre informazioni sugli endpoint, vedere [Comunicazioni con le applicazioni][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="3fc73-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="3fc73-239">Configurare la **diagnostica**del cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="3fc73-240">Per impostazione predefinita, la diagnostica è abilitata nel cluster come supporto per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="3fc73-240">By default, diagnostics are enabled on your cluster to assist with troubleshooting issues.</span></span> <span data-ttu-id="3fc73-241">Per disabilitare la diagnostica, impostare lo **stato** su **No**.</span><span class="sxs-lookup"><span data-stu-id="3fc73-241">If you want to disable diagnostics change the **Status** toggle to **Off**.</span></span> <span data-ttu-id="3fc73-242">**Non** è consigliabile disattivare la diagnostica.</span><span class="sxs-lookup"><span data-stu-id="3fc73-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="3fc73-243">Selezionare la modalità di aggiornamento di Fabric che si vuole impostare per il cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-243">Select the Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="3fc73-244">Selezionare **Automatic**(Automatici) se si vuole che il sistema acquisisca automaticamente la versione più recente disponibile e provi ad aggiornare il cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-244">Select **Automatic**, if you want the system to automatically pick up the latest available version and try to upgrade your cluster to it.</span></span> <span data-ttu-id="3fc73-245">Impostare la modalità su **Manual**(Manuali) se si vuole scegliere una versione supportata.</span><span class="sxs-lookup"><span data-stu-id="3fc73-245">Set the mode to **Manual**, if you want to choose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="3fc73-246">Microsoft supporta solo i cluster che eseguono versioni supportate di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3fc73-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="3fc73-247">Selezionando la modalità **Manual** (Manuali), l'utente si assume la responsabilità di aggiornare il cluster a una versione supportata.</span><span class="sxs-lookup"><span data-stu-id="3fc73-247">By selecting the **Manual** mode, you are taking on the responsibility to upgrade your cluster to a supported version.</span></span> <span data-ttu-id="3fc73-248">Per altri dettagli sulla modalità di aggiornamento di Fabric, vedere il documento sull'[aggiornamento di un cluster di Service Fabric][service-fabric-cluster-upgrade].</span><span class="sxs-lookup"><span data-stu-id="3fc73-248">For more details on the Fabric upgrade mode see the [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="3fc73-249">3. Sicurezza</span><span class="sxs-lookup"><span data-stu-id="3fc73-249">3. Security</span></span>
![Schermata delle configurazioni di sicurezza nel portale di Azure.][SecurityConfigs]

<span data-ttu-id="3fc73-251">Il passaggio finale consiste nel fornire informazioni sul certificato per proteggere il cluster tramite l'insieme di credenziali delle chiavi e il certificato creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3fc73-251">The final step is to provide certificate information to secure the cluster using the Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="3fc73-252">Compilare i campi del certificato primario con l'output ottenuto dal caricamento del **certificato del cluster** nell'insieme di credenziali delle chiavi usando il comando `Invoke-AddCertToKeyVault` di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3fc73-252">Populate the primary certificate fields with the output obtained from uploading the **cluster certificate** to Key Vault using the `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="3fc73-253">Selezionare la casella **Configura impostazioni avanzate** per l'immissione dei certificati client per **amministratore client** e **client di sola lettura**.</span><span class="sxs-lookup"><span data-stu-id="3fc73-253">Check the **Configure advanced settings** box to enter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="3fc73-254">In questi campi, immettere l'identificazione personale del certificato client amministratore e l'identificazione personale del certificato client utente di sola lettura, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="3fc73-254">In these fields, enter the thumbprint of your admin client certificate and the thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="3fc73-255">Quando gli amministratori provano a connettersi al cluster, viene concesso l'accesso solo se hanno un certificato con identificazione personale corrispondente ai valori di identificazione personale immessi in questi campi.</span><span class="sxs-lookup"><span data-stu-id="3fc73-255">When administrators attempt to connect to the cluster, they are granted access only if they have a certificate with a thumbprint that matches the thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="3fc73-256">4. Riepilogo</span><span class="sxs-lookup"><span data-stu-id="3fc73-256">4. Summary</span></span>
![<span data-ttu-id="3fc73-257">Schermata iniziale con la voce "Distribuzione di un cluster di Service Fabric" visualizzata.</span><span class="sxs-lookup"><span data-stu-id="3fc73-257">Screen shot of the start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="3fc73-258">Per completare la creazione del cluster, fare clic su **Riepilogo** per visualizzare le configurazioni specificate oppure scaricare il modello di Azure Resource Manager usato per distribuire il cluster.</span><span class="sxs-lookup"><span data-stu-id="3fc73-258">To complete the cluster creation, click **Summary** to see the configurations that you have provided, or download the Azure Resource Manager template that that used to deploy your cluster.</span></span> <span data-ttu-id="3fc73-259">Dopo che sono state specificate le impostazioni obbligatorie, il pulsante **OK** diventa di colore verde ed è possibile avviare il processo di creazione del cluster facendo clic su di esso.</span><span class="sxs-lookup"><span data-stu-id="3fc73-259">After you have provided the mandatory settings, the **OK** button becomes green and you can start the cluster creation process by clicking it.</span></span>

<span data-ttu-id="3fc73-260">È possibile visualizzare lo stato di avanzamento del processo di creazione nell'area delle notifiche:</span><span class="sxs-lookup"><span data-stu-id="3fc73-260">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="3fc73-261">fare clic sull'icona a forma di campana accanto alla barra di stato nell'angolo superiore destro della schermata. Se durante la creazione del cluster si è fatto clic su **Aggiungi alla Schermata iniziale**, la **distribuzione del cluster di Service Fabric** verrà indicata nella **schermata iniziale**.</span><span class="sxs-lookup"><span data-stu-id="3fc73-261">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you will see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="3fc73-262">Visualizzare lo stato del cluster</span><span class="sxs-lookup"><span data-stu-id="3fc73-262">View your cluster status</span></span>
![Schermata dei dettagli del cluster nel dashboard.][ClusterDashboard]

<span data-ttu-id="3fc73-264">Al termine della creazione del cluster è possibile esaminare il cluster nel portale.</span><span class="sxs-lookup"><span data-stu-id="3fc73-264">Once your cluster is created, you can inspect your cluster in the portal:</span></span>

1. <span data-ttu-id="3fc73-265">Selezionare **Sfoglia** e fare clic su **Cluster di Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="3fc73-265">Go to **Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="3fc73-266">Trovare il cluster e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="3fc73-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="3fc73-267">È ora possibile visualizzare i dettagli del cluster nel dashboard, inclusi l'endpoint pubblico del cluster e un link per Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="3fc73-267">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

<span data-ttu-id="3fc73-268">La sezione **Node Monitor** (Monitoraggio dei nodi) nel pannello del dashboard del cluster indica il numero di macchine virtuali integre e di quelle non integre.</span><span class="sxs-lookup"><span data-stu-id="3fc73-268">The **Node Monitor** section on the cluster's dashboard blade indicates the number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="3fc73-269">Per altre informazioni sull'integrità del cluster, vedere [Introduzione al monitoraggio dell'integrità di Service Fabric][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="3fc73-269">You can find more details about the cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="3fc73-270">I cluster di Service Fabric richiedono che sia sempre attivo un certo numero di nodi allo scopo di mantenere la disponibilità e lo stato, ossia per "mantenere il quorum".</span><span class="sxs-lookup"><span data-stu-id="3fc73-270">Service Fabric clusters require a certain number of nodes to be up always to maintain availability and preserve state - referred to as "maintaining quorum".</span></span> <span data-ttu-id="3fc73-271">Di conseguenza, in genere non è sicuro arrestare tutti i computer del cluster se prima non è stato eseguito un [backup completo dello stato][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="3fc73-271">Therfore, it is typically not safe to shut down all machines in the cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-to-a-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="3fc73-272">Connessione remota a un'istanza di set di scalabilità di macchine virtuali o a un nodo del cluster</span><span class="sxs-lookup"><span data-stu-id="3fc73-272">Remote connect to a Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="3fc73-273">Ognuno dei tipi di nodo specificati nel cluster determina la configurazione di un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3fc73-273">Each of the NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="3fc73-274">Per i dettagli, vedere [Connessione remota a un'istanza di set di scalabilità di macchine virtuali][remote-connect-to-a-vm-scale-set].</span><span class="sxs-lookup"><span data-stu-id="3fc73-274">See [Remote connect to a Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fc73-275">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3fc73-275">Next steps</span></span>
<span data-ttu-id="3fc73-276">A questo punto, è stato creato un cluster protetto tramite i certificati per l'autenticazione di gestione.</span><span class="sxs-lookup"><span data-stu-id="3fc73-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="3fc73-277">Successivamente, [connettersi al cluster](service-fabric-connect-to-secure-cluster.md) e scoprire come [gestire i segreti delle applicazioni](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="3fc73-277">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="3fc73-278">Vedere anche [Service Fabric support options](service-fabric-support.md) (Opzioni di supporto di Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="3fc73-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
