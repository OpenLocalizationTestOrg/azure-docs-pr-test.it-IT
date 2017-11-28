---
title: aaaCreate dell'infrastruttura del servizio cluster nel portale di Azure hello | Documenti Microsoft
description: In questo articolo viene descritto come tooset di un cluster di Service Fabric protetto in Azure tramite hello portale di Azure e l'insieme di credenziali chiave di Azure.
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
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a><span data-ttu-id="ae140-103">Creare un cluster di Service Fabric in Azure utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ae140-103">Create a Service Fabric cluster in Azure using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae140-104">Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="ae140-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="ae140-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ae140-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="ae140-106">Si tratta di una Guida dettagliata che illustra hello passaggi di configurazione di un cluster di Service Fabric sicuro in Azure utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae140-106">This is a step-by-step guide that walks you through hello steps of setting up a secure Service Fabric cluster in Azure using hello Azure portal.</span></span> <span data-ttu-id="ae140-107">Questa guida illustra hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ae140-107">This guide walks you through hello following steps:</span></span>

* <span data-ttu-id="ae140-108">Impostare le chiavi di toomanage insieme di credenziali chiave per la sicurezza del cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-108">Set up Key Vault toomanage keys for cluster security.</span></span>
* <span data-ttu-id="ae140-109">Creare un cluster protetto in Azure tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae140-109">Create a secured cluster in Azure through hello Azure portal.</span></span>
* <span data-ttu-id="ae140-110">Autenticare gli amministratori che usano i certificati.</span><span class="sxs-lookup"><span data-stu-id="ae140-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="ae140-111">Per le opzioni di sicurezza avanzata, ad esempio l'autenticazione dell'utente con Azure Active Directory e la configurazione dei certificati per la protezione delle applicazioni, [creare il cluster usando Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="ae140-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="ae140-112">Un cluster protetto è un cluster che impedisce le operazioni di accesso non autorizzato toomanagement, che include la distribuzione, aggiornamento ed eliminazione di applicazioni, servizi e dati hello in che essi contenuti.</span><span class="sxs-lookup"><span data-stu-id="ae140-112">A secure cluster is a cluster that prevents unauthorized access toomanagement operations, which includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="ae140-113">Un cluster non sicuro da un cluster che chiunque può connettersi tooat qualsiasi momento ed eseguire operazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="ae140-113">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="ae140-114">Sebbene sia possibile toocreate un cluster non sicuro, è **consiglia un cluster protetto toocreate**.</span><span class="sxs-lookup"><span data-stu-id="ae140-114">Although it is possible toocreate an unsecure cluster, it is **highly recommended toocreate a secure cluster**.</span></span> <span data-ttu-id="ae140-115">Un cluster non protetto **non può essere protetto in un secondo momento**. Sarà necessario crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="ae140-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="ae140-116">concetti di Hello sono hello stesso per la creazione di cluster sicuri, se il cluster hello è cluster Linux o i cluster di Windows.</span><span class="sxs-lookup"><span data-stu-id="ae140-116">hello concepts are hello same for creating secure clusters, whether hello clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="ae140-117">Per altre informazioni e script helper per la creazione di cluster Linux protetti, vedere [Creare cluster protetti in Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="ae140-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="ae140-118">Hello parametri ottenuti dallo script di supporto hello fornito possono essere immesso direttamente nel portale di hello come descritto nella sezione hello [creare un cluster nel portale di Azure hello](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="ae140-118">hello parameters obtained by hello helper script provided can be input directly into hello portal as described in hello section [Create a cluster in hello Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="ae140-119">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="ae140-119">Log in tooAzure</span></span>
<span data-ttu-id="ae140-120">Questa guida usa [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="ae140-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="ae140-121">Quando si avvia una nuova sessione PowerShell, accedi tooyour account Azure e selezionare la sottoscrizione prima di eseguire i comandi di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae140-121">When starting a new PowerShell session, log in tooyour Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="ae140-122">Log nell'account azure tooyour:</span><span class="sxs-lookup"><span data-stu-id="ae140-122">Log in tooyour azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="ae140-123">Selezionare la propria sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="ae140-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="ae140-124">Configurare l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="ae140-124">Set up Key Vault</span></span>
<span data-ttu-id="ae140-125">Questa parte della Guida hello viene illustrata la creazione di un insieme di credenziali chiave per un cluster di Service Fabric in Azure e per le applicazioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ae140-125">This part of hello guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="ae140-126">Per una guida completa in insieme di credenziali chiave, vedere hello [Guida introduttiva di insieme di credenziali chiave][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="ae140-126">For a complete guide on Key Vault, see hello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="ae140-127">Service Fabric utilizza toosecure certificati x. 509 un cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-127">Service Fabric uses X.509 certificates toosecure a cluster.</span></span> <span data-ttu-id="ae140-128">Insieme di credenziali chiave di Azure è toomanage utilizzati certificati per i cluster di Service Fabric in Azure.</span><span class="sxs-lookup"><span data-stu-id="ae140-128">Azure Key Vault is used toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="ae140-129">Quando viene distribuito un cluster in Azure, provider di risorse di Azure hello responsabile per la creazione di cluster di Service Fabric estrae i certificati dall'insieme di credenziali chiave e li installa nel cluster hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ae140-129">When a cluster is deployed in Azure, hello Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="ae140-130">Hello diagramma seguente illustra la relazione hello tra l'insieme di credenziali chiave, un cluster di Service Fabric e provider di risorse di Azure hello che utilizza i certificati archiviati nell'insieme di credenziali chiave durante la creazione di un cluster:</span><span class="sxs-lookup"><span data-stu-id="ae140-130">hello following diagram illustrates hello relationship between Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Installazione del certificato][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="ae140-132">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="ae140-132">Create a Resource Group</span></span>
<span data-ttu-id="ae140-133">primo passaggio Hello è toocreate un nuovo gruppo di risorse in modo specifico per l'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="ae140-133">hello first step is toocreate a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="ae140-134">Inserimento di insieme di credenziali chiave nel proprio gruppo di risorse, in modo che sia possibile rimuovere gruppi di risorse di calcolo e archiviazione, ad esempio gruppo di risorse hello con il cluster di Service Fabric - è consigliabile senza perdere le chiavi e segreti.</span><span class="sxs-lookup"><span data-stu-id="ae140-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as hello resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="ae140-135">gruppo di risorse Hello con l'insieme di credenziali chiave deve essere in hello stessa area geografica hello cluster che lo usa.</span><span class="sxs-lookup"><span data-stu-id="ae140-135">hello resource group that has your Key Vault must be in hello same region as hello cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="ae140-136">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="ae140-136">Create Key Vault</span></span>
<span data-ttu-id="ae140-137">Creare un insieme di credenziali chiave nel nuovo gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="ae140-137">Create a Key Vault in hello new resource group.</span></span> <span data-ttu-id="ae140-138">insieme di credenziali chiave Hello **deve essere abilitato per la distribuzione** tooallow hello certificati di infrastruttura servizio risorsa provider tooget da esso e installare nei nodi del cluster:</span><span class="sxs-lookup"><span data-stu-id="ae140-138">hello Key Vault **must be enabled for deployment** tooallow hello Service Fabric resource provider tooget certificates from it and install on cluster nodes:</span></span>

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
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

<span data-ttu-id="ae140-139">Se si dispone già di un insieme di credenziali delle chiavi, è possibile abilitarlo per la distribuzione tramite l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="ae140-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a><span data-ttu-id="ae140-140">Aggiungere certificati tooKey insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="ae140-140">Add certificates tooKey Vault</span></span>
<span data-ttu-id="ae140-141">I certificati vengono usati in Service Fabric tooprovide autenticazione e crittografia toosecure vari aspetti di un cluster e le relative applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ae140-141">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="ae140-142">Per altre informazioni sull'uso dei certificati in Service Fabric, vedere [Scenari di sicurezza di un cluster di Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="ae140-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="ae140-143">Cluster e certificato del server (obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="ae140-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="ae140-144">Questo certificato è obbligatorio toosecure un cluster e impedire l'accesso non autorizzato tooit.</span><span class="sxs-lookup"><span data-stu-id="ae140-144">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="ae140-145">Il certificato fornisce protezione del cluster in due modi:</span><span class="sxs-lookup"><span data-stu-id="ae140-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="ae140-146">**Autenticazione del cluster:** autentica la comunicazione da nodo a nodo per la federazione di cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="ae140-147">Solo i nodi che è possano provare la propria identità con il certificato è possono aggiungere il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ae140-147">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="ae140-148">**L'autenticazione del server:** autentica hello cluster Gestione endpoint tooa client di gestione, in modo che hello gestione client riconosce stia comunicando toohello reale cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-148">**Server authentication:** Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="ae140-149">Questo certificato fornisce inoltre SSL per l'API di gestione HTTPS hello e per Service Fabric Explorer tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ae140-149">This certificate also provides SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="ae140-150">tooserve questi scopi, certificato hello deve soddisfare i seguenti requisiti hello:</span><span class="sxs-lookup"><span data-stu-id="ae140-150">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="ae140-151">certificato di Hello deve contenere una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="ae140-151">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="ae140-152">Hello certificato deve essere creato per lo scambio di chiave, esportabile tooa file di scambio di informazioni personali (PFX).</span><span class="sxs-lookup"><span data-stu-id="ae140-152">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="ae140-153">Hello nome soggetto del certificato deve corrispondere hello dominio utilizzato tooaccess hello dell'infrastruttura del servizio cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-153">hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="ae140-154">Questo è necessario tooprovide SSL per l'endpoint di gestione HTTPS del cluster hello e Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="ae140-154">This is required tooprovide SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="ae140-155">È possibile ottenere un certificato SSL da un'autorità di certificazione (CA) per hello `.cloudapp.azure.com` dominio.</span><span class="sxs-lookup"><span data-stu-id="ae140-155">You cannot obtain an SSL certificate from a certificate authority (CA) for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="ae140-156">Acquistare un nome di dominio personalizzato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="ae140-157">Quando si richiede un certificato dal nome del soggetto del certificato CA hello deve corrispondere il nome di dominio personalizzato hello utilizzato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-157">When you request a certificate from a CA hello certificate's subject name must match hello custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="ae140-158">Certificati di autenticazione client</span><span class="sxs-lookup"><span data-stu-id="ae140-158">Client authentication certificates</span></span>
<span data-ttu-id="ae140-159">I certificati client aggiuntivi autenticano gli amministratori per le attività di gestione del cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="ae140-160">Service Fabric ha due livelli di accesso: **admin** e **utente di sola lettura**.</span><span class="sxs-lookup"><span data-stu-id="ae140-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="ae140-161">Deve essere usato almeno un certificato per l'accesso amministrativo.</span><span class="sxs-lookup"><span data-stu-id="ae140-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="ae140-162">Per l'accesso aggiuntivo a livello di utente, è necessario specificare un certificato separato.</span><span class="sxs-lookup"><span data-stu-id="ae140-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="ae140-163">Per altre informazioni sui ruoli di accesso, vedere [Controllo degli accessi in base al ruolo per i client di Service Fabric][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="ae140-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="ae140-164">Non è necessario tooupload Client l'autenticazione dei certificati tooKey insieme di credenziali toowork con Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ae140-164">You do not need tooupload Client authentication certificates tooKey Vault toowork with Service Fabric.</span></span> <span data-ttu-id="ae140-165">Questi certificati sufficiente toobe fornita toousers autorizzati per la gestione di cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-165">These certificates only need toobe provided toousers who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="ae140-166">Azure Active Directory è hello consigliato client tooauthenticate modo per cluster di operazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="ae140-166">Azure Active Directory is hello recommended way tooauthenticate clients for cluster management operations.</span></span> <span data-ttu-id="ae140-167">toouse Azure Active Directory, è necessario [creare un cluster con Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="ae140-167">toouse Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="ae140-168">Certificati delle applicazioni (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="ae140-168">Application certificates (optional)</span></span>
<span data-ttu-id="ae140-169">Per motivi di sicurezza dell'applicazione, è possibile installare nel cluster numerosi certificati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="ae140-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="ae140-170">Prima di creare il cluster, considerare gli scenari di sicurezza dell'applicazione hello che richiedono un toobe certificato installato nei nodi di hello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ae140-170">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="ae140-171">Crittografia e decrittografia dei valori di configurazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ae140-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="ae140-172">Crittografia dei dati tra i nodi durante la replica</span><span class="sxs-lookup"><span data-stu-id="ae140-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="ae140-173">I certificati dell'applicazione non possono essere configurati durante la creazione di un cluster tramite il portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ae140-173">Application certificates cannot be configured when creating a cluster through hello Azure portal.</span></span> <span data-ttu-id="ae140-174">tooconfigure i certificati dell'applicazione in fase di installazione del cluster, è necessario [creare un cluster con Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="ae140-174">tooconfigure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="ae140-175">È anche possibile aggiungere cluster toohello certificati di applicazione dopo che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="ae140-175">You can also add application certificates toohello cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="ae140-176">Formattazione dei certificati per l'uso di provider di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="ae140-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="ae140-177">I file di chiave privata (con estensione pfx) possono essere aggiunti e usati direttamente tramite l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="ae140-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="ae140-178">Tuttavia, il provider di risorse di Azure hello richiede toobe chiavi archiviate in un particolare formato JSON che include PFX hello come una base 64 codificata stringa hello e la password della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="ae140-178">However, hello Azure resource provider requires keys toobe stored in a special JSON format that includes hello .pfx as a base-64 encoded string and hello private key password.</span></span> <span data-ttu-id="ae140-179">tooaccommodate questi requisiti, le chiavi devono essere inseriti in una stringa JSON e quindi archiviati come *segreti* nell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="ae140-179">tooaccommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="ae140-180">è un modulo di PowerShell toomake questo processo più semplice, [disponibile in GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="ae140-180">toomake this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="ae140-181">Seguire questi modulo hello toouse di passaggi:</span><span class="sxs-lookup"><span data-stu-id="ae140-181">Follow these steps toouse hello module:</span></span>

1. <span data-ttu-id="ae140-182">Scaricare l'intero contenuto di hello del repository hello in una directory locale.</span><span class="sxs-lookup"><span data-stu-id="ae140-182">Download hello entire contents of hello repo into a local directory.</span></span> 
2. <span data-ttu-id="ae140-183">Importare il modulo hello nella finestra di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ae140-183">Import hello module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="ae140-184">Hello `Invoke-AddCertToKeyVault` comando in questo modulo di PowerShell Formatta automaticamente una chiave privata del certificato in una stringa JSON e ne carica tooKey insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ae140-184">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it tooKey Vault.</span></span> <span data-ttu-id="ae140-185">Usarlo certificato di cluster tooadd hello e qualsiasi tooKey certificati applicazione aggiuntiva dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ae140-185">Use it tooadd hello cluster certificate and any additional application certificates tooKey Vault.</span></span> <span data-ttu-id="ae140-186">Ripetere questo passaggio per tutti i certificati aggiuntivi desiderate tooinstall del cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-186">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="ae140-187">Questi sono tutti i prerequisiti di hello insieme di credenziali chiave per la configurazione di un modello di gestione risorse di cluster di Service Fabric che consente di installare i certificati per l'autenticazione di nodo, protezione di endpoint di gestione e l'autenticazione e qualsiasi maggiore sicurezza dell'applicazione funzionalità che utilizzano certificati x. 509.</span><span class="sxs-lookup"><span data-stu-id="ae140-187">These are all hello Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="ae140-188">A questo punto, è ora necessario hello dopo l'installazione in Azure:</span><span class="sxs-lookup"><span data-stu-id="ae140-188">At this point, you should now have hello following setup in Azure:</span></span>

* <span data-ttu-id="ae140-189">Gruppo di risorse dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="ae140-189">Key Vault resource group</span></span>
  * <span data-ttu-id="ae140-190">Insieme di credenziali di chiave</span><span class="sxs-lookup"><span data-stu-id="ae140-190">Key Vault</span></span>
    * <span data-ttu-id="ae140-191">Certificato di autenticazione del server del cluster</span><span class="sxs-lookup"><span data-stu-id="ae140-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="ae140-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="ae140-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-hello-azure-portal"></a><span data-ttu-id="ae140-193">Creare cluster in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ae140-193">Create cluster in hello Azure portal</span></span>
### <a name="search-for-hello-service-fabric-cluster-resource"></a><span data-ttu-id="ae140-194">Cercare hello risorsa cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ae140-194">Search for hello Service Fabric cluster resource</span></span>
![ricerca per il modello di cluster di Service Fabric nel portale di Azure hello.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="ae140-196">Accedi toohello [portale di Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="ae140-196">Sign in toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="ae140-197">Fare clic su **New** tooadd un nuovo modello di risorsa.</span><span class="sxs-lookup"><span data-stu-id="ae140-197">Click **New** tooadd a new resource template.</span></span> <span data-ttu-id="ae140-198">Ricerca per il modello di Cluster di Service Fabric hello in hello **Marketplace** in **tutto**.</span><span class="sxs-lookup"><span data-stu-id="ae140-198">Search for hello Service Fabric Cluster template in hello **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="ae140-199">Selezionare **Cluster di Service Fabric** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="ae140-199">Select **Service Fabric Cluster** from hello list.</span></span>
4. <span data-ttu-id="ae140-200">Passare toohello **Cluster di Service Fabric** pannello, fare clic su **crea**,</span><span class="sxs-lookup"><span data-stu-id="ae140-200">Navigate toohello **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="ae140-201">Hello **cluster di Service Fabric crea** pannello è hello seguenti quattro passaggi.</span><span class="sxs-lookup"><span data-stu-id="ae140-201">hello **Create Service Fabric cluster** blade has hello following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="ae140-202">1. Nozioni di base</span><span class="sxs-lookup"><span data-stu-id="ae140-202">1. Basics</span></span>
![Schermata della creazione di un nuovo gruppo di risorse.][CreateRG]

<span data-ttu-id="ae140-204">Nel Pannello di nozioni di base hello tooprovide dettagli di base hello è necessario per il cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-204">In hello Basics blade you need tooprovide hello basic details for your cluster.</span></span>

1. <span data-ttu-id="ae140-205">Immettere il nome di hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-205">Enter hello name of your cluster.</span></span>
2. <span data-ttu-id="ae140-206">Immettere un **nome utente** e **password** per Desktop remoto per hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ae140-206">Enter a **user name** and **password** for Remote Desktop for hello VMs.</span></span>
3. <span data-ttu-id="ae140-207">Verificare che hello tooselect **sottoscrizione** che si desidera toobe il cluster della distribuzione, soprattutto se si dispone di più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="ae140-207">Make sure tooselect hello **Subscription** that you want your cluster toobe deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="ae140-208">Creare un **nuovo gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="ae140-208">Create a **new resource group**.</span></span> <span data-ttu-id="ae140-209">È migliore toogive hello stesso nome cluster hello, poiché è utile nella ricerca in un secondo momento, soprattutto quando si sta tentando di toomake modifiche tooyour distribuzione o Elimina il cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-209">It is best toogive it hello same name as hello cluster, since it helps in finding them later, especially when you are trying toomake changes tooyour deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ae140-210">Sebbene sia possibile decidere toouse un gruppo di risorse esistente, è toocreate una buona norma un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ae140-210">Although you can decide toouse an existing resource group, it is a good practice toocreate a new resource group.</span></span> <span data-ttu-id="ae140-211">Questo rende facile toodelete cluster che non è necessario.</span><span class="sxs-lookup"><span data-stu-id="ae140-211">This makes it easy toodelete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="ae140-212">Seleziona hello **area** in cui si desidera che il cluster di hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ae140-212">Select hello **region** in which you want toocreate hello cluster.</span></span> <span data-ttu-id="ae140-213">È necessario utilizzare hello stessa regione che la chiave dell'insieme di credenziali è in.</span><span class="sxs-lookup"><span data-stu-id="ae140-213">You must use hello same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="ae140-214">2. Configurazione del cluster</span><span class="sxs-lookup"><span data-stu-id="ae140-214">2. Cluster configuration</span></span>
![Creare un tipo di nodo][CreateNodeType]

<span data-ttu-id="ae140-216">Configurare i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-216">Configure your cluster nodes.</span></span> <span data-ttu-id="ae140-217">Tipi di nodo definiscono dimensioni di macchina virtuale hello, hello numero di macchine virtuali e le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="ae140-217">Node types define hello VM sizes, hello number of VMs, and their properties.</span></span> <span data-ttu-id="ae140-218">Il cluster può avere più di un tipo di nodo, ma il tipo di nodo primario hello (primo definiti nel portale di hello hello) deve disporre di almeno cinque macchine virtuali, come questo è il tipo di nodo hello in cui vengono collocati i servizi di sistema di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ae140-218">Your cluster can have more than one node type, but hello primary node type (hello first one that you define on hello portal) must have at least five VMs, as this is hello node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="ae140-219">Non è necessario configurare le **proprietà relative alla posizione**, perché una proprietà relativa alla posizione predefinita "NodeTypeName" viene aggiunta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ae140-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="ae140-220">Uno scenario comune per diversi tipi di nodi è costituito da un'applicazione contenente un servizio front-end e un servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="ae140-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="ae140-221">Si desidera tooput servizio front-end di hello in macchine virtuali più piccoli (dimensioni di macchina virtuale come D2) con le porte aperte toohello Internet, ma si vuole servizio back-end di hello tooput nelle macchine virtuali di dimensioni maggiori (con dimensioni di macchina virtuale come D4, D6, D15 e così via) e senza con connessione Internet di porte aperte.</span><span class="sxs-lookup"><span data-stu-id="ae140-221">You want tooput hello front-end service on smaller VMs (VM sizes like D2) with ports open toohello Internet, but you want tooput hello back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="ae140-222">Scegliere un nome per il tipo di nodo (1 too12 caratteri contenente solo lettere e numeri).</span><span class="sxs-lookup"><span data-stu-id="ae140-222">Choose a name for your node type (1 too12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="ae140-223">Hello minimo **dimensioni** dovuto di macchine virtuali per nodo primario hello hello tipo **durabilità** livello scelto per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ae140-223">hello minimum **size** of VMs for hello primary node type is driven by hello **durability** tier you choose for hello cluster.</span></span> <span data-ttu-id="ae140-224">valore predefinito di Hello per il livello di durabilità hello è Bronzo.</span><span class="sxs-lookup"><span data-stu-id="ae140-224">hello default for hello durability tier is bronze.</span></span> <span data-ttu-id="ae140-225">Per ulteriori informazioni sulla durabilità, vedere [come toochoose hello Service Fabric cluster e affidabilità][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="ae140-225">For more information on durability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="ae140-226">Selezionare dimensioni della macchina virtuale hello e il piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="ae140-226">Select hello VM size and pricing tier.</span></span> <span data-ttu-id="ae140-227">Le macchine virtuali della serie D dispongono di unità SSD e sono consigliate per applicazioni con stato.</span><span class="sxs-lookup"><span data-stu-id="ae140-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="ae140-228">Non usare SKU di VM con core parziali o meno di 7 GB di capacità disco disponibile.</span><span class="sxs-lookup"><span data-stu-id="ae140-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="ae140-229">Hello minimo **numero** dovuto di macchine virtuali per nodo primario hello hello tipo **affidabilità** livello desiderato.</span><span class="sxs-lookup"><span data-stu-id="ae140-229">hello minimum **number** of VMs for hello primary node type is driven by hello **reliability** tier you choose.</span></span> <span data-ttu-id="ae140-230">valore predefinito di Hello per il livello di affidabilità hello è Silver.</span><span class="sxs-lookup"><span data-stu-id="ae140-230">hello default for hello reliability tier is Silver.</span></span> <span data-ttu-id="ae140-231">Per ulteriori informazioni sull'affidabilità, vedere [come toochoose hello Service Fabric cluster e affidabilità][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="ae140-231">For more information on reliability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="ae140-232">Scegliere hello numero di macchine virtuali per il tipo di nodo hello.</span><span class="sxs-lookup"><span data-stu-id="ae140-232">Choose hello number of VMs for hello node type.</span></span> <span data-ttu-id="ae140-233">È possibile ridimensionare verso l'alto o verso il basso numero hello di macchine virtuali in un tipo di nodo in un secondo momento, ma nel tipo di nodo primario hello, hello minima dipende dal livello di affidabilità hello che si è scelto.</span><span class="sxs-lookup"><span data-stu-id="ae140-233">You can scale up or down hello number of VMs in a node type later on, but on hello primary node type, hello minimum is driven by hello reliability level that you have chosen.</span></span> <span data-ttu-id="ae140-234">Gli altri tipi di nodo possono avere un minimo di 1 VM.</span><span class="sxs-lookup"><span data-stu-id="ae140-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="ae140-235">Configurare gli endpoint personalizzati.</span><span class="sxs-lookup"><span data-stu-id="ae140-235">Configure custom endpoints.</span></span> <span data-ttu-id="ae140-236">Questo campo consente un elenco delimitato da virgole di porte che si desidera tooexpose tramite hello bilanciamento del carico di Azure toohello tooenter rete Internet pubblica per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ae140-236">This field allows you tooenter a comma-separated list of ports that you want tooexpose through hello Azure Load Balancer toohello public Internet for your applications.</span></span> <span data-ttu-id="ae140-237">Ad esempio, se si prevede un cluster di tooyour applicazione web toodeploy, immettere "80" tooallow traffico sulla porta 80 in cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-237">For example, if you plan toodeploy a web application tooyour cluster, enter "80" here tooallow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="ae140-238">Per altre informazioni sugli endpoint, vedere [Comunicazioni con le applicazioni][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="ae140-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="ae140-239">Configurare la **diagnostica**del cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="ae140-240">Per impostazione predefinita, in tooassist il cluster con la risoluzione dei problemi è abilitata la diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ae140-240">By default, diagnostics are enabled on your cluster tooassist with troubleshooting issues.</span></span> <span data-ttu-id="ae140-241">Se si desidera modifica di diagnostica toodisable hello **stato** attivare o disattivare troppo**Off**.</span><span class="sxs-lookup"><span data-stu-id="ae140-241">If you want toodisable diagnostics change hello **Status** toggle too**Off**.</span></span> <span data-ttu-id="ae140-242">**Non** è consigliabile disattivare la diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ae140-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="ae140-243">Selezionare hello modalità si desidera impostare il cluster di aggiornamento dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="ae140-243">Select hello Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="ae140-244">Selezionare **automatico**, se si desidera hello sistema tooautomatically preleva hello versione più recente e provare tooupgrade tooit il cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-244">Select **Automatic**, if you want hello system tooautomatically pick up hello latest available version and try tooupgrade your cluster tooit.</span></span> <span data-ttu-id="ae140-245">Impostare la modalità di hello troppo**manuale**, se si desidera toochoose una versione supportata.</span><span class="sxs-lookup"><span data-stu-id="ae140-245">Set hello mode too**Manual**, if you want toochoose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="ae140-246">Microsoft supporta solo i cluster che eseguono versioni supportate di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ae140-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="ae140-247">Selezionando hello **manuale** modalità, si assume hello responsabilità tooupgrade versione tooa supportato cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-247">By selecting hello **Manual** mode, you are taking on hello responsibility tooupgrade your cluster tooa supported version.</span></span> <span data-ttu-id="ae140-248">Per ulteriori informazioni sulle modalità di aggiornamento dell'infrastruttura di hello vedere hello [documento di aggiornamento del cluster di infrastruttura del servizio.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="ae140-248">For more details on hello Fabric upgrade mode see hello [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="ae140-249">3. Sicurezza</span><span class="sxs-lookup"><span data-stu-id="ae140-249">3. Security</span></span>
![Schermata delle configurazioni di sicurezza nel portale di Azure.][SecurityConfigs]

<span data-ttu-id="ae140-251">passaggio finale Hello è cluster tooprovide certificato informazioni toosecure hello utilizzando hello insieme di credenziali chiave e un certificato creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ae140-251">hello final step is tooprovide certificate information toosecure hello cluster using hello Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="ae140-252">Compilare i campi di un certificato primario hello con output di hello ottenuto dal caricamento hello **certificato cluster** tooKey insieme di credenziali usando hello `Invoke-AddCertToKeyVault` comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae140-252">Populate hello primary certificate fields with hello output obtained from uploading hello **cluster certificate** tooKey Vault using hello `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="ae140-253">Controllare hello **configurare le impostazioni avanzate** casella certificati client tooenter per **amministratore client** e **client di sola lettura**.</span><span class="sxs-lookup"><span data-stu-id="ae140-253">Check hello **Configure advanced settings** box tooenter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="ae140-254">In questi campi, immettere identificazione personale hello del certificato client di amministrazione e l'identificazione personale hello del certificato client utente di sola lettura, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="ae140-254">In these fields, enter hello thumbprint of your admin client certificate and hello thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="ae140-255">Quando gli amministratori tentano tooconnect toohello cluster, essi vengono concesse immesso accesso solo se dispongono di un certificato con identificazione personale che corrispondono ai valori hello identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="ae140-255">When administrators attempt tooconnect toohello cluster, they are granted access only if they have a certificate with a thumbprint that matches hello thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="ae140-256">4. Riepilogo</span><span class="sxs-lookup"><span data-stu-id="ae140-256">4. Summary</span></span>
![<span data-ttu-id="ae140-257">Cattura di schermata della scheda avvio hello visualizzazione "Distribuzione Cluster di Service Fabric."</span><span class="sxs-lookup"><span data-stu-id="ae140-257">Screen shot of hello start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="ae140-258">creazione del cluster hello toocomplete, fare clic su **riepilogo** le configurazioni di hello toosee che hanno fornito o scaricare hello modello di gestione risorse di Azure che utilizzato toodeploy del cluster.</span><span class="sxs-lookup"><span data-stu-id="ae140-258">toocomplete hello cluster creation, click **Summary** toosee hello configurations that you have provided, or download hello Azure Resource Manager template that that used toodeploy your cluster.</span></span> <span data-ttu-id="ae140-259">Dopo aver fornito le impostazioni obbligatorie hello, hello **OK** pulsante diventa di colore verde, è possibile iniziare il processo hello facendovi clic sopra.</span><span class="sxs-lookup"><span data-stu-id="ae140-259">After you have provided hello mandatory settings, hello **OK** button becomes green and you can start hello cluster creation process by clicking it.</span></span>

<span data-ttu-id="ae140-260">È possibile visualizzare lo stato di avanzamento di hello creazione nelle notifiche hello.</span><span class="sxs-lookup"><span data-stu-id="ae140-260">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="ae140-261">(Fare clic sull'icona di campanello"hello" nella barra di stato hello in alto hello destra dello schermo). Se fa clic su **Pin tooStartboard** durante la creazione di cluster hello, si noterà **la distribuzione di Cluster di Service Fabric** bloccato toohello **avviare** Lavagna.</span><span class="sxs-lookup"><span data-stu-id="ae140-261">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you will see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="ae140-262">Visualizzare lo stato del cluster</span><span class="sxs-lookup"><span data-stu-id="ae140-262">View your cluster status</span></span>
![Cattura di schermata dei dettagli di cluster nel dashboard di hello.][ClusterDashboard]

<span data-ttu-id="ae140-264">Una volta creato il cluster, è possibile controllare il cluster nel portale di hello:</span><span class="sxs-lookup"><span data-stu-id="ae140-264">Once your cluster is created, you can inspect your cluster in hello portal:</span></span>

1. <span data-ttu-id="ae140-265">Andare troppo**Sfoglia** e fare clic su **servizio infrastruttura cluster**.</span><span class="sxs-lookup"><span data-stu-id="ae140-265">Go too**Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="ae140-266">Trovare il cluster e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="ae140-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="ae140-267">È ora possibile visualizzare i dettagli di hello del cluster nel dashboard di hello, tra cui endpoint pubblico del cluster hello e tooService un collegamento Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="ae140-267">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

<span data-ttu-id="ae140-268">Hello **nodo Monitoraggio** sezione nel Pannello di dashboard del cluster hello indica il numero di hello di macchine virtuali che sono integri e non integro.</span><span class="sxs-lookup"><span data-stu-id="ae140-268">hello **Node Monitor** section on hello cluster's dashboard blade indicates hello number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="ae140-269">È possibile trovare altre informazioni sull'integrità del cluster hello in [introduzione di modello di integrità dell'infrastruttura a servizio][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="ae140-269">You can find more details about hello cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="ae140-270">I cluster di Service Fabric richiedono un certo numero di nodi toobe di disponibilità AlwaysOn toomaintain e mantengono lo stato, di cui viene fatto riferimento tooas "gestione quorum".</span><span class="sxs-lookup"><span data-stu-id="ae140-270">Service Fabric clusters require a certain number of nodes toobe up always toomaintain availability and preserve state - referred tooas "maintaining quorum".</span></span> <span data-ttu-id="ae140-271">Pertanto, non è in genere sicura tooshut verso il basso tutti i computer nel cluster hello a meno che non è stata innanzitutto eseguita una [backup completo dello stato del][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="ae140-271">Therfore, it is typically not safe tooshut down all machines in hello cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="ae140-272">Istanza di tooa Set di scalabilità della macchina virtuale o un nodo del cluster della connessione remota</span><span class="sxs-lookup"><span data-stu-id="ae140-272">Remote connect tooa Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="ae140-273">Ognuno di hello NodeTypes specificate nei risultati del cluster in un riquadro attività di configurazione Set di scalabilità macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ae140-273">Each of hello NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="ae140-274">Vedere [tooa istanza del Set di scalabilità della macchina virtuale di connettersi in remoto] [ remote-connect-to-a-vm-scale-set] per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="ae140-274">See [Remote connect tooa Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae140-275">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ae140-275">Next steps</span></span>
<span data-ttu-id="ae140-276">A questo punto, è stato creato un cluster protetto tramite i certificati per l'autenticazione di gestione.</span><span class="sxs-lookup"><span data-stu-id="ae140-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="ae140-277">Successivamente, [connettersi cluster tooyour](service-fabric-connect-to-secure-cluster.md) e informazioni su come troppo[gestire segreti applicazione](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="ae140-277">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="ae140-278">Vedere anche [Service Fabric support options](service-fabric-support.md) (Opzioni di supporto di Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="ae140-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

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
