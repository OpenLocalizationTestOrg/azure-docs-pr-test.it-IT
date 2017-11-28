---
title: aaaCreate un Azure Service Fabric del cluster da un modello | Documenti Microsoft
description: In questo articolo viene descritto come tooset di un'infrastruttura protetta di servizio cluster in Azure tramite Gestione risorse di Azure, insieme di credenziali chiave di Azure e Azure Active Directory (Azure AD) per l'autenticazione client.
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="738ec-103">Creare un cluster di Service Fabric usando Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="738ec-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="738ec-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="738ec-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="738ec-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="738ec-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="738ec-106">Questo articolo contiene una guida dettagliata che illustra la configurazione di un cluster di Azure Service Fabric sicuro in Azure tramite Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="738ec-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="738ec-107">È consapevole di che tale articolo hello è lungo.</span><span class="sxs-lookup"><span data-stu-id="738ec-107">We acknowledge that hello article is long.</span></span> <span data-ttu-id="738ec-108">Tuttavia, a meno che non si conoscono già accuratamente il contenuto di hello, essere toofollow verificare ogni passaggio con attenzione.</span><span class="sxs-lookup"><span data-stu-id="738ec-108">Nevertheless, unless you are already thoroughly familiar with hello content, be sure toofollow each step carefully.</span></span>

<span data-ttu-id="738ec-109">Hello vengono trattate hello seguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="738ec-109">hello guide covers hello following procedures:</span></span>

* <span data-ttu-id="738ec-110">Configurazione dei certificati di tooupload insieme di credenziali chiave Azure per la sicurezza del cluster e dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="738ec-110">Setting up an Azure key vault tooupload certificates for cluster and application security</span></span>
* <span data-ttu-id="738ec-111">Creazione di un cluster sicuro in Azure con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="738ec-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="738ec-112">Autenticazione degli utenti con Azure Active Directory (Azure AD) per la gestione dei cluster</span><span class="sxs-lookup"><span data-stu-id="738ec-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="738ec-113">Un cluster sicura è un cluster che impedisce le operazioni toomanagement accesso non autorizzato.</span><span class="sxs-lookup"><span data-stu-id="738ec-113">A secure cluster is a cluster that prevents unauthorized access toomanagement operations.</span></span> <span data-ttu-id="738ec-114">Ciò include la distribuzione, l'aggiornamento e l'eliminazione di applicazioni, servizi e dati hello in che essi contenuti.</span><span class="sxs-lookup"><span data-stu-id="738ec-114">This includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="738ec-115">Un cluster non sicuro da un cluster che chiunque può connettersi tooat qualsiasi momento ed eseguire operazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="738ec-115">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="738ec-116">Sebbene sia possibile toocreate un cluster non sicuro, si consiglia di creare un cluster protetto sin hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-116">Although it is possible toocreate an unsecure cluster, we highly recommend that you create a secure cluster from hello outset.</span></span> <span data-ttu-id="738ec-117">Poiché un cluster non sicuro non può essere protetto in un secondo momento, è necessario crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="738ec-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="738ec-118">il concetto di Hello di creazione di cluster sicuri è hello stesso, che si tratti di cluster Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="738ec-118">hello concept of creating secure clusters is hello same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="738ec-119">Per altre informazioni e script helper per la creazione di cluster Linux sicuri, vedere [Creare cluster protetti in Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="738ec-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="738ec-120">Accedi tooyour account Azure</span><span class="sxs-lookup"><span data-stu-id="738ec-120">Sign in tooyour Azure account</span></span>
<span data-ttu-id="738ec-121">Questa guida usa [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="738ec-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="738ec-122">Quando si avvia una nuova sessione PowerShell, accedi tooyour account Azure e selezionare la sottoscrizione prima di eseguire i comandi di Azure.</span><span class="sxs-lookup"><span data-stu-id="738ec-122">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="738ec-123">Accedi tooyour account di Azure:</span><span class="sxs-lookup"><span data-stu-id="738ec-123">Sign in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="738ec-124">Selezionare la propria sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="738ec-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="738ec-125">Configurare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="738ec-125">Set up a key vault</span></span>
<span data-ttu-id="738ec-126">Questa sezione illustra la creazione di un insieme di credenziali delle chiavi per un cluster di Service Fabric in Azure e per le applicazioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="738ec-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="738ec-127">Per una guida completa tooAzure insieme di credenziali chiave, vedere toohello [Guida introduttiva di insieme di credenziali chiave][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="738ec-127">For a complete guide tooAzure Key Vault, refer toohello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="738ec-128">Service Fabric utilizza toosecure certificati x. 509 un cluster e fornisce le funzionalità di sicurezza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="738ec-128">Service Fabric uses X.509 certificates toosecure a cluster and provide application security features.</span></span> <span data-ttu-id="738ec-129">Utilizzare i certificati toomanage insieme di credenziali chiave per i cluster di Service Fabric in Azure.</span><span class="sxs-lookup"><span data-stu-id="738ec-129">You use Key Vault toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="738ec-130">Quando viene distribuito un cluster in Azure, i provider di risorse di Azure hello che è responsabili della creazione di cluster di Service Fabric estrae i certificati dall'insieme di credenziali chiave e li installa nel cluster hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="738ec-130">When a cluster is deployed in Azure, hello Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="738ec-131">Hello diagramma seguente viene illustrata hello relazione tra l'insieme di credenziali chiave di Azure, un cluster di Service Fabric e provider di risorse di Azure hello che utilizza i certificati archiviati in un insieme di credenziali chiave durante la creazione di un cluster:</span><span class="sxs-lookup"><span data-stu-id="738ec-131">hello following diagram illustrates hello relationship between Azure Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagramma dell'installazione del certificato][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="738ec-133">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="738ec-133">Create a resource group</span></span>
<span data-ttu-id="738ec-134">primo passaggio Hello è toocreate un gruppo di risorse in modo specifico per l'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="738ec-134">hello first step is toocreate a resource group specifically for your key vault.</span></span> <span data-ttu-id="738ec-135">Si consiglia di inserire l'insieme di credenziali chiave hello nel proprio gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="738ec-135">We recommend that you put hello key vault into its own resource group.</span></span> <span data-ttu-id="738ec-136">Questa azione consente di rimuovere hello calcolo e archiviazione gruppi di risorse, tra cui gruppo di risorse hello che contiene il cluster di Service Fabric, senza perdere le chiavi e segreti.</span><span class="sxs-lookup"><span data-stu-id="738ec-136">This action lets you remove hello compute and storage resource groups, including hello resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="738ec-137">gruppo di risorse Hello che contiene l'insieme di credenziali chiave _deve essere in hello stessa regione_ come cluster hello che lo usa.</span><span class="sxs-lookup"><span data-stu-id="738ec-137">hello resource group that contains your key vault _must be in hello same region_ as hello cluster that is using it.</span></span>

<span data-ttu-id="738ec-138">Se si prevede di cluster toodeploy in più aree, si consiglia di assegnare un nome gruppo di risorse hello e hello chiave dell'insieme di credenziali in modo che indica quale regione a cui appartiene.</span><span class="sxs-lookup"><span data-stu-id="738ec-138">If you plan toodeploy clusters in multiple regions, we suggest that you name hello resource group and hello key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="738ec-139">output di Hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="738ec-139">hello output should look like this:</span></span>

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a><span data-ttu-id="738ec-140">Creare un insieme di credenziali chiave nel nuovo gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="738ec-140">Create a key vault in hello new resource group</span></span>
<span data-ttu-id="738ec-141">insieme di credenziali chiave Hello _deve essere abilitato per la distribuzione_ tooallow hello calcolo certificati tooget provider di risorse da esso e installarla su istanze di macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="738ec-141">hello key vault _must be enabled for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="738ec-142">output di Hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="738ec-142">hello output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
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
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="738ec-143">Usare un insieme di credenziali delle chiavi esistente</span><span class="sxs-lookup"><span data-stu-id="738ec-143">Use an existing key vault</span></span>

<span data-ttu-id="738ec-144">toouse un insieme di credenziali esistente, si _deve essere abilitata per la distribuzione_ tooallow hello calcolo certificati tooget provider di risorse da esso e installarlo nei nodi del cluster:</span><span class="sxs-lookup"><span data-stu-id="738ec-144">toouse an existing key vault, you _must enable it for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a><span data-ttu-id="738ec-145">Aggiungere certificati tooyour insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="738ec-145">Add certificates tooyour key vault</span></span>

<span data-ttu-id="738ec-146">I certificati vengono usati in Service Fabric tooprovide autenticazione e crittografia toosecure vari aspetti di un cluster e le relative applicazioni.</span><span class="sxs-lookup"><span data-stu-id="738ec-146">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="738ec-147">Per altre informazioni sull'uso dei certificati in Service Fabric, vedere [Scenari di sicurezza di un cluster di Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="738ec-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="738ec-148">Cluster e certificato del server (obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="738ec-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="738ec-149">Questo certificato è obbligatorio toosecure un cluster e impedire l'accesso non autorizzato tooit.</span><span class="sxs-lookup"><span data-stu-id="738ec-149">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="738ec-150">Il certificato fornisce protezione del cluster in due modi:</span><span class="sxs-lookup"><span data-stu-id="738ec-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="738ec-151">Autenticazione del cluster: autentica la comunicazione da nodo a nodo per la federazione di cluster.</span><span class="sxs-lookup"><span data-stu-id="738ec-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="738ec-152">Solo i nodi che è possano provare la propria identità con il certificato è possono aggiungere il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-152">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="738ec-153">L'autenticazione del server: hello cluster Gestione endpoint tooa gestione client viene autenticato in modo che hello client management sa stia comunicando toohello reale cluster.</span><span class="sxs-lookup"><span data-stu-id="738ec-153">Server authentication: Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="738ec-154">Questo certificato fornisce inoltre SSL per l'API di gestione HTTPS hello e per Service Fabric Explorer tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="738ec-154">This certificate also provides an SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="738ec-155">tooserve questi scopi, certificato hello deve soddisfare i seguenti requisiti hello:</span><span class="sxs-lookup"><span data-stu-id="738ec-155">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="738ec-156">certificato di Hello deve contenere una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="738ec-156">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="738ec-157">Hello certificato deve essere creato per lo scambio di chiave, ovvero esportabile tooa file di scambio di informazioni personali (PFX).</span><span class="sxs-lookup"><span data-stu-id="738ec-157">hello certificate must be created for key exchange, which is exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="738ec-158">nome del soggetto del certificato Hello deve corrispondere dominio hello utilizzare cluster di Service Fabric tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-158">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="738ec-159">Questo tipo di associazione è obbligatorio tooprovide SSL per l'endpoint di gestione del cluster hello HTTPS e Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="738ec-159">This matching is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="738ec-160">È possibile ottenere un certificato SSL da un'autorità di certificazione (CA) per hello. cloudapp.azure.com dominio.</span><span class="sxs-lookup"><span data-stu-id="738ec-160">You cannot obtain an SSL certificate from a certificate authority (CA) for hello .cloudapp.azure.com domain.</span></span> <span data-ttu-id="738ec-161">È necessario ottenere un nome di dominio personalizzato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="738ec-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="738ec-162">Quando si richiede un certificato da un'autorità di certificazione, hello Nome soggetto del certificato deve corrispondere nome di dominio personalizzato hello utilizzati per il cluster.</span><span class="sxs-lookup"><span data-stu-id="738ec-162">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="738ec-163">Certificati delle applicazioni (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="738ec-163">Application certificates (optional)</span></span>
<span data-ttu-id="738ec-164">Per motivi di sicurezza dell'applicazione, è possibile installare nel cluster numerosi certificati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="738ec-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="738ec-165">Prima di creare il cluster, considerare gli scenari di sicurezza dell'applicazione hello che richiedono un toobe certificato installato nei nodi di hello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="738ec-165">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="738ec-166">Crittografia e decrittografia dei valori di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="738ec-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="738ec-167">Crittografia dei dati tra i nodi durante la replica.</span><span class="sxs-lookup"><span data-stu-id="738ec-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="738ec-168">Formattazione dei certificati per l'uso di provider di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="738ec-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="738ec-169">È possibile aggiungere e usare file di chiave privata (PFX) direttamente tramite l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="738ec-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="738ec-170">Tuttavia, i provider di risorse di calcolo di Azure hello richiede toobe chiavi archiviate in un particolare formato JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="738ec-170">However, hello Azure compute resource provider requires keys toobe stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="738ec-171">formato di Hello include file con estensione pfx hello come una stringa base 64 codificata in formato e la password della chiave privata hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-171">hello format includes hello .pfx file as a base 64-encoded string and hello private key password.</span></span> <span data-ttu-id="738ec-172">tooaccommodate questi requisiti, hello chiavi devono essere inserite in una stringa JSON e quindi archiviate come "segreti" nella chiave hello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="738ec-172">tooaccommodate these requirements, hello keys must be placed in a JSON string and then stored as "secrets" in hello key vault.</span></span>

<span data-ttu-id="738ec-173">Questo processo più semplice, toomake un [modulo PowerShell è disponibile in GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="738ec-173">toomake this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="738ec-174">modulo hello toouse, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="738ec-174">toouse hello module, do hello following:</span></span>

1. <span data-ttu-id="738ec-175">Scaricare l'intero contenuto di hello del repository hello in una directory locale.</span><span class="sxs-lookup"><span data-stu-id="738ec-175">Download hello entire contents of hello repo into a local directory.</span></span>
2. <span data-ttu-id="738ec-176">Passare toohello directory locale.</span><span class="sxs-lookup"><span data-stu-id="738ec-176">Go toohello local directory.</span></span>
2. <span data-ttu-id="738ec-177">Importare il modulo ServiceFabricRPHelpers hello nella finestra di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="738ec-177">Import hello ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="738ec-178">Hello `Invoke-AddCertToKeyVault` comando in questo modulo di PowerShell Formatta automaticamente una chiave privata del certificato in una stringa JSON e ne carica toohello insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="738ec-178">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it toohello key vault.</span></span> <span data-ttu-id="738ec-179">Utilizzare il certificato del cluster hello di hello comando tooadd e qualsiasi applicazione aggiuntiva certificati toohello chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="738ec-179">Use hello command tooadd hello cluster certificate and any additional application certificates toohello key vault.</span></span> <span data-ttu-id="738ec-180">Ripetere questo passaggio per tutti i certificati aggiuntivi desiderate tooinstall del cluster.</span><span class="sxs-lookup"><span data-stu-id="738ec-180">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="738ec-181">Caricamento di un certificato esistente</span><span class="sxs-lookup"><span data-stu-id="738ec-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="738ec-182">Se si verifica un errore, ad esempio hello uno riportati di seguito, significa in genere la presenza di un conflitto di risorse URL.</span><span class="sxs-lookup"><span data-stu-id="738ec-182">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="738ec-183">conflitto di hello tooresolve, nome dell'insieme di credenziali chiave hello di modifica.</span><span class="sxs-lookup"><span data-stu-id="738ec-183">tooresolve hello conflict, change hello key vault name.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="738ec-184">Dopo la risoluzione dei conflitti di hello, l'output di hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="738ec-184">After hello conflict is resolved, hello output should look like this:</span></span>

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="738ec-185">È necessario hello tre precedente stringhe, CertificateThumbprint SourceVault e CertificateURL, tooset di un cluster di Service Fabric sicuro e tooobtain tutti i certificati dell'applicazione che è possibile utilizzare per la sicurezza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="738ec-185">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="738ec-186">Se non si salva le stringhe di hello, può essere difficile tooretrieve li eseguendo una ricerca chiave hello insieme di credenziali in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="738ec-186">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a><span data-ttu-id="738ec-187">Creazione di un certificato autofirmato e caricarlo insieme di credenziali chiave toohello</span><span class="sxs-lookup"><span data-stu-id="738ec-187">Creating a self-signed certificate and uploading it toohello key vault</span></span>

<span data-ttu-id="738ec-188">Se è già stato caricato nell'insieme di credenziali chiave di certificati toohello, ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="738ec-188">If you have already uploaded your certificates toohello key vault, skip this step.</span></span> <span data-ttu-id="738ec-189">Questo passaggio è per la generazione di un nuovo certificato autofirmato e caricarlo insieme di credenziali chiave tooyour.</span><span class="sxs-lookup"><span data-stu-id="738ec-189">This step is for generating a new self-signed certificate and uploading it tooyour key vault.</span></span> <span data-ttu-id="738ec-190">Dopo avere modificato i parametri di hello in hello lo script seguente e quindi eseguirlo, verrà richiesto di immettere una password del certificato.</span><span class="sxs-lookup"><span data-stu-id="738ec-190">After you change hello parameters in hello following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="738ec-191">Se si verifica un errore, ad esempio hello uno riportati di seguito, significa in genere la presenza di un conflitto di risorse URL.</span><span class="sxs-lookup"><span data-stu-id="738ec-191">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="738ec-192">conflitto hello tooresolve, insieme di credenziali chiave di hello Modifica nome, nome RG e così via.</span><span class="sxs-lookup"><span data-stu-id="738ec-192">tooresolve hello conflict, change hello key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="738ec-193">Dopo la risoluzione dei conflitti di hello, l'output di hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="738ec-193">After hello conflict is resolved, hello output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="738ec-194">È necessario hello tre precedente stringhe, CertificateThumbprint SourceVault e CertificateURL, tooset di un cluster di Service Fabric sicuro e tooobtain tutti i certificati dell'applicazione che è possibile utilizzare per la sicurezza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="738ec-194">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="738ec-195">Se non si salva le stringhe di hello, può essere difficile tooretrieve li eseguendo una ricerca chiave hello insieme di credenziali in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="738ec-195">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

 <span data-ttu-id="738ec-196">A questo punto, è necessario disporre di hello degli elementi sul posto di seguito:</span><span class="sxs-lookup"><span data-stu-id="738ec-196">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="738ec-197">gruppo di risorse dell'insieme di credenziali chiave Hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-197">hello key vault resource group.</span></span>
* <span data-ttu-id="738ec-198">Hello insieme di credenziali chiave e il relativo URL (denominato SourceVault nelle hello precede l'output di PowerShell).</span><span class="sxs-lookup"><span data-stu-id="738ec-198">hello key vault and its URL (called SourceVault in hello preceding PowerShell output).</span></span>
* <span data-ttu-id="738ec-199">certificato di autenticazione server cluster Hello e il relativo URL nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-199">hello cluster server authentication certificate and its URL in hello key vault.</span></span>
* <span data-ttu-id="738ec-200">i certificati dell'applicazione Hello e gli URL nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-200">hello application certificates and their URLs in hello key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="738ec-201">Configurare Azure Active Directory per l'autenticazione client</span><span class="sxs-lookup"><span data-stu-id="738ec-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="738ec-202">Azure AD consente alle organizzazioni (noto come tenant) toomanage utente accesso tooapplications.</span><span class="sxs-lookup"><span data-stu-id="738ec-202">Azure AD enables organizations (known as tenants) toomanage user access tooapplications.</span></span> <span data-ttu-id="738ec-203">Alcune applicazioni sono caratterizzate da un'interfaccia utente di accesso basata sul Web, altre invece da un'esperienza client nativa.</span><span class="sxs-lookup"><span data-stu-id="738ec-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="738ec-204">In questo articolo si presuppone che sia già stato creato un tenant.</span><span class="sxs-lookup"><span data-stu-id="738ec-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="738ec-205">In caso contrario, iniziare leggendo [come tenant di Azure Active Directory tooget][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="738ec-205">If you have not, start by reading [How tooget an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="738ec-206">Un cluster di Service Fabric offre tooits punti di ingresso diverse funzionalità di gestione, tra cui hello basata sul web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] e [Visual Studio] [service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="738ec-206">A Service Fabric cluster offers several entry points tooits management functionality, including hello web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="738ec-207">Di conseguenza, creare due cluster di toohello accesso Azure AD applicazioni toocontrol, un'applicazione web e un'applicazione nativa.</span><span class="sxs-lookup"><span data-stu-id="738ec-207">As a result, you create two Azure AD applications toocontrol access toohello cluster, one web application and one native application.</span></span>

<span data-ttu-id="738ec-208">toosimplify alcuni dei passaggi di hello coinvolti nella configurazione di Azure AD con un cluster di Service Fabric, è stato creato un set di script di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="738ec-208">toosimplify some of hello steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="738ec-209">È necessario completare i seguenti passaggi prima di creare cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-209">You must complete hello following steps before you create hello cluster.</span></span> <span data-ttu-id="738ec-210">Poiché gli script hello prevedono che gli endpoint e i nomi dei cluster, i valori di hello devono essere pianificati e non i valori che è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="738ec-210">Because hello scripts expect cluster names and endpoints, hello values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="738ec-211">[Scaricare gli script hello] [ sf-aad-ps-script-download] tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="738ec-211">[Download hello scripts][sf-aad-ps-script-download] tooyour computer.</span></span>
2. <span data-ttu-id="738ec-212">Pulsante destro del mouse hello file zip, selezionare **proprietà**selezionare hello **Unblock** casella di controllo e quindi fare clic su **applica**.</span><span class="sxs-lookup"><span data-stu-id="738ec-212">Right-click hello zip file, select **Properties**, select hello **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="738ec-213">Estrarre il file zip hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-213">Extract hello zip file.</span></span>
4. <span data-ttu-id="738ec-214">Eseguire `SetupApplications.ps1`e fornire hello TenantId, ClusterName e WebApplicationReplyUrl come parametri.</span><span class="sxs-lookup"><span data-stu-id="738ec-214">Run `SetupApplications.ps1`, and provide hello TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="738ec-215">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="738ec-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="738ec-216">È possibile trovare l'ID tenant eseguendo il comando di PowerShell hello `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="738ec-216">You can find your TenantId by executing hello PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="738ec-217">L'esecuzione di questo comando Visualizza hello TenantId per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="738ec-217">Executing this command displays hello TenantId for every subscription.</span></span>

    <span data-ttu-id="738ec-218">ClusterName è applicazioni hello Azure AD usato tooprefix creati dallo script hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-218">ClusterName is used tooprefix hello Azure AD applications that are created by hello script.</span></span> <span data-ttu-id="738ec-219">Non è necessario toomatch hello nome effettivo del cluster esattamente.</span><span class="sxs-lookup"><span data-stu-id="738ec-219">It does not need toomatch hello actual cluster name exactly.</span></span> <span data-ttu-id="738ec-220">È previsto toomake solo è più facile toomap Azure AD artefatti toohello cluster di Service Fabric è utilizzato con.</span><span class="sxs-lookup"><span data-stu-id="738ec-220">It is intended only toomake it easier toomap Azure AD artifacts toohello Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="738ec-221">WebApplicationReplyUrl è l'endpoint predefinito hello restituiti da Azure AD utenti tooyour dopo aver effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="738ec-221">WebApplicationReplyUrl is hello default endpoint that Azure AD returns tooyour users after they finish signing in.</span></span> <span data-ttu-id="738ec-222">Impostare questo endpoint come endpoint di Service Fabric Explorer hello per il cluster, che per impostazione predefinita è:</span><span class="sxs-lookup"><span data-stu-id="738ec-222">Set this endpoint as hello Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="738ec-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="738ec-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="738ec-224">Si è toosign richiesta nell'account tooan che dispone di privilegi amministrativi per il tenant hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="738ec-224">You are prompted toosign in tooan account that has administrative privileges for hello Azure AD tenant.</span></span> <span data-ttu-id="738ec-225">Dopo l'accesso, hello script crea web hello e applicazioni native toorepresent il cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="738ec-225">After you sign in, hello script creates hello web and native applications toorepresent your Service Fabric cluster.</span></span> <span data-ttu-id="738ec-226">Se si osservano le applicazioni del tenant hello hello su [portale di Azure classico][azure-classic-portal], verranno visualizzate due voci di nuovo:</span><span class="sxs-lookup"><span data-stu-id="738ec-226">If you look at hello tenant's applications in hello [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="738ec-227">*ClusterName*\_Cluster</span><span class="sxs-lookup"><span data-stu-id="738ec-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="738ec-228">*ClusterName*\_Client</span><span class="sxs-lookup"><span data-stu-id="738ec-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="738ec-229">script Hello stampa hello JSON richiesto dal modello di Azure Resource Manager hello quando si crea il cluster hello nella sezione successiva hello, pertanto è una finestra di PowerShell buona tookeep hello aprire.</span><span class="sxs-lookup"><span data-stu-id="738ec-229">hello script prints hello JSON required by hello Azure Resource Manager template when you create hello cluster in hello next section, so it's a good idea tookeep hello PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="738ec-230">Creare un modello di Cluster Resource Manager di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="738ec-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="738ec-231">In questa sezione, hello output di hello precedente vengono utilizzati i comandi di PowerShell in un modello di gestione risorse di cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="738ec-231">In this section, hello outputs of hello preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="738ec-232">Modelli di gestione risorse di esempio sono disponibili in hello [raccolta di modelli di avvio rapido di Azure su GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="738ec-232">Sample Resource Manager templates are available in hello [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="738ec-233">Questi modelli possono essere usati come punto di partenza per il modello del cluster.</span><span class="sxs-lookup"><span data-stu-id="738ec-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-hello-resource-manager-template"></a><span data-ttu-id="738ec-234">Creare il modello di gestione risorse di hello</span><span class="sxs-lookup"><span data-stu-id="738ec-234">Create hello Resource Manager template</span></span>
<span data-ttu-id="738ec-235">Questa Guida Usa hello [5 nodi cluster sicuro] [ service-fabric-secure-cluster-5-node-1-nodetype] modello di esempio e i parametri di modello.</span><span class="sxs-lookup"><span data-stu-id="738ec-235">This guide uses hello [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="738ec-236">Scaricare `azuredeploy.json` e `azuredeploy.parameters.json` tooyour computer e aprire entrambi i file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="738ec-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` tooyour computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="738ec-237">Aggiungere certificati</span><span class="sxs-lookup"><span data-stu-id="738ec-237">Add certificates</span></span>
<span data-ttu-id="738ec-238">Aggiungere modello di gestione risorse di cluster tooa certificati facendo riferimento hello chiave dell'insieme di credenziali contenente le chiavi di hello certificato.</span><span class="sxs-lookup"><span data-stu-id="738ec-238">You add certificates tooa cluster Resource Manager template by referencing hello key vault that contains hello certificate keys.</span></span> <span data-ttu-id="738ec-239">Si consiglia di posizionare i valori di insieme di credenziali chiave hello in un file di parametri di modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="738ec-239">We recommend that you place hello key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="738ec-240">In questo modo consente di mantenere hello Gestione risorse file modello riutilizzabile e privo di distribuzione tooa specifico di valori.</span><span class="sxs-lookup"><span data-stu-id="738ec-240">Doing so keeps hello Resource Manager template file reusable and free of values specific tooa deployment.</span></span>

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="738ec-241">Aggiungere che set di scalabilità di macchine virtuali di tutti i certificati toohello osProfile</span><span class="sxs-lookup"><span data-stu-id="738ec-241">Add all certificates toohello virtual machine scale set osProfile</span></span>
<span data-ttu-id="738ec-242">Ogni certificato installato nel cluster hello deve essere configurato nella sezione osProfile hello della risorsa di set di scalabilità hello (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="738ec-242">Every certificate that's installed in hello cluster must be configured in hello osProfile section of hello scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="738ec-243">Questa azione indica certificato hello risorsa provider tooinstall hello in hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="738ec-243">This action instructs hello resource provider tooinstall hello certificate on hello VMs.</span></span> <span data-ttu-id="738ec-244">Questa installazione include sia il certificato di cluster hello e i certificati di sicurezza dell'applicazione che si prevede di toouse per le applicazioni:</span><span class="sxs-lookup"><span data-stu-id="738ec-244">This installation includes both hello cluster certificate and any application security certificates that you plan toouse for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a><span data-ttu-id="738ec-245">Configurare il certificato del cluster di Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="738ec-245">Configure hello Service Fabric cluster certificate</span></span>
<span data-ttu-id="738ec-246">certificato di autenticazione Hello cluster deve essere configurato in entrambe le risorse di cluster Service Fabric hello (Microsoft.ServiceFabric/clusters) e imposta hello estensione Service Fabric per la scalabilità della macchina virtuale nella risorsa set di scalabilità della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-246">hello cluster authentication certificate must be configured in both hello Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and hello Service Fabric extension for virtual machine scale sets in hello virtual machine scale set resource.</span></span> <span data-ttu-id="738ec-247">In questo modo hello Service Fabric resource provider tooconfigure per utilizzare per l'autenticazione del cluster e l'autenticazione server per l'endpoint di gestione.</span><span class="sxs-lookup"><span data-stu-id="738ec-247">This arrangement allows hello Service Fabric resource provider tooconfigure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="738ec-248">Risorsa del set di scalabilità di macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="738ec-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="738ec-249">Risorsa di Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="738ec-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="738ec-250">Inserire la configurazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="738ec-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="738ec-251">configurazione di Hello Azure Active Directory creato in precedenza può essere inseriti direttamente nel modello di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="738ec-251">hello Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="738ec-252">Tuttavia, è consigliabile prima di estrarre i valori hello in riutilizzabile modello parametri file tookeep hello Gestione risorse e privi di distribuzione tooa specifico di valori.</span><span class="sxs-lookup"><span data-stu-id="738ec-252">However, we recommended that you first extract hello values into a parameters file tookeep hello Resource Manager template reusable and free of values specific tooa deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <span data-ttu-id="738ec-253"><a "configure-arm" ></a>Configurare i parametri del modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="738ec-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
<span data-ttu-id="738ec-254">Infine, usare valori di output di hello dall'insieme di credenziali chiave di hello e file dei parametri di Azure AD PowerShell comandi toopopulate hello:</span><span class="sxs-lookup"><span data-stu-id="738ec-254">Finally, use hello output values from hello key vault and Azure AD PowerShell commands toopopulate hello parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="738ec-255">A questo punto, è necessario disporre di hello degli elementi sul posto di seguito:</span><span class="sxs-lookup"><span data-stu-id="738ec-255">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="738ec-256">Gruppo di risorse dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="738ec-256">Key vault resource group</span></span>
  * <span data-ttu-id="738ec-257">Insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="738ec-257">Key vault</span></span>
  * <span data-ttu-id="738ec-258">Certificato di autenticazione del server del cluster</span><span class="sxs-lookup"><span data-stu-id="738ec-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="738ec-259">Certificato di crittografia dei dati</span><span class="sxs-lookup"><span data-stu-id="738ec-259">Data encipherment certificate</span></span>
* <span data-ttu-id="738ec-260">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="738ec-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="738ec-261">Applicazione Azure AD per la gestione basata su Web e Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="738ec-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="738ec-262">Applicazione Azure AD per la gestione dei client nativi</span><span class="sxs-lookup"><span data-stu-id="738ec-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="738ec-263">Utenti e ruoli assegnati</span><span class="sxs-lookup"><span data-stu-id="738ec-263">Users and their assigned roles</span></span>
* <span data-ttu-id="738ec-264">Modello di Cluster Resource Manager di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="738ec-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="738ec-265">Certificati configurati tramite l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="738ec-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="738ec-266">Azure Active Directory configurato</span><span class="sxs-lookup"><span data-stu-id="738ec-266">Azure Active Directory configured</span></span>

<span data-ttu-id="738ec-267">Hello seguente diagramma viene illustrato dove la chiave dell'insieme di credenziali e la configurazione di Azure AD rientrano nel modello di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="738ec-267">hello following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Mappa di dipendenza di Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a><span data-ttu-id="738ec-269">Creare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="738ec-269">Create hello cluster</span></span>
<span data-ttu-id="738ec-270">Si è ora cluster hello toocreate pronto utilizzando [la distribuzione dei modelli di risorse di Azure][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="738ec-270">You are now ready toocreate hello cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="738ec-271">Eseguirne il test</span><span class="sxs-lookup"><span data-stu-id="738ec-271">Test it</span></span>
<span data-ttu-id="738ec-272">Utilizzare il modello di gestione risorse di hello tootest comando PowerShell seguente con un file dei parametri:</span><span class="sxs-lookup"><span data-stu-id="738ec-272">Use hello following PowerShell command tootest your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="738ec-273">Distribuirlo</span><span class="sxs-lookup"><span data-stu-id="738ec-273">Deploy it</span></span>
<span data-ttu-id="738ec-274">Se hello Gestione risorse modello test viene superato, utilizzare hello toodeploy comando PowerShell seguente un modello di gestione delle risorse con un file dei parametri:</span><span class="sxs-lookup"><span data-stu-id="738ec-274">If hello Resource Manager template test passes, use hello following PowerShell command toodeploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a><span data-ttu-id="738ec-275">Assegnare gli utenti tooroles</span><span class="sxs-lookup"><span data-stu-id="738ec-275">Assign users tooroles</span></span>
<span data-ttu-id="738ec-276">Dopo aver creato hello toorepresent di applicazioni del cluster, assegnare gli utenti ruoli toohello supportati dall'infrastruttura di servizio: sola lettura e l'amministratore. È possibile assegnare ruoli hello utilizzando hello [portale di Azure classico][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="738ec-276">After you have created hello applications toorepresent your cluster, assign your users toohello roles supported by Service Fabric: read-only and admin. You can assign hello roles by using hello [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="738ec-277">Nel portale di Azure hello, andare tooyour tenant e quindi selezionare **applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="738ec-277">In hello Azure portal, go tooyour tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="738ec-278">Selezionare l'applicazione web hello, che ha un nome come `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="738ec-278">Select hello web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="738ec-279">Fare clic su hello **utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="738ec-279">Click hello **Users** tab.</span></span>
4. <span data-ttu-id="738ec-280">Selezionare un tooassign utente e quindi fare clic su hello **assegnare** pulsante in basso hello hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-280">Select a user tooassign, and then click hello **Assign** button at hello bottom of hello screen.</span></span>

    ![Gli utenti tooroles pulsante Assegna][assign-users-to-roles-button]
5. <span data-ttu-id="738ec-282">Selezionare hello ruolo tooassign toohello utente.</span><span class="sxs-lookup"><span data-stu-id="738ec-282">Select hello role tooassign toohello user.</span></span>

    ![Finestra di dialogo "Assegna utenti"][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="738ec-284">Per altre informazioni sui ruoli in Service Fabric, vedere [Controllo degli accessi in base al ruolo per i client di Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="738ec-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="738ec-285">Creare cluster protetti in Linux</span><span class="sxs-lookup"><span data-stu-id="738ec-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="738ec-286">processo di hello toomake più semplice, sono disponibili un [script helper](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="738ec-286">toomake hello process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="738ec-287">Prima di usare questo script helper, assicurarsi che sia già installata un'interfaccia della riga di comando di Azure e che sia nel percorso in uso.</span><span class="sxs-lookup"><span data-stu-id="738ec-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="738ec-288">Assicurarsi che script hello disponga delle autorizzazioni tooexecute eseguendo `chmod +x cert_helper.py` dopo averlo scaricato.</span><span class="sxs-lookup"><span data-stu-id="738ec-288">Make sure that hello script has permissions tooexecute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="738ec-289">Hello primo passaggio consiste nell'account Azure tooyour toosign con CLI hello `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="738ec-289">hello first step is toosign in tooyour Azure account by using CLI with hello `azure login` command.</span></span> <span data-ttu-id="738ec-290">Dopo aver effettuato l'accesso tooyour account Azure, utilizzare hello helper script con l'autorità di certificazione firmato certificato, come hello seguente comando Mostra:</span><span class="sxs-lookup"><span data-stu-id="738ec-290">After signing in tooyour Azure account, use hello helper script with your CA signed certificate, as hello following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="738ec-291">il parametro - ifile Hello può accettare un file con estensione pfx o un file con estensione PEM come input, con un tipo di hello certificato (pfx o pem oppure ss se si tratta di un certificato autofirmato).</span><span class="sxs-lookup"><span data-stu-id="738ec-291">hello -ifile parameter can take a .pfx file or a .pem file as input, with hello certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="738ec-292">parametro -h Hello stampato il testo della Guida hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-292">hello parameter -h prints out hello help text.</span></span>


<span data-ttu-id="738ec-293">Questo comando restituisce i seguenti tre stringhe come output di hello hello:</span><span class="sxs-lookup"><span data-stu-id="738ec-293">This command returns hello following three strings as hello output:</span></span>

* <span data-ttu-id="738ec-294">SourceVaultID, ovvero ID hello per hello nuovo KeyVault ResourceGroup è creato per l'utente</span><span class="sxs-lookup"><span data-stu-id="738ec-294">SourceVaultID, which is hello ID for hello new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="738ec-295">CertificateUrl per l'accesso a hello certificato</span><span class="sxs-lookup"><span data-stu-id="738ec-295">CertificateUrl for accessing hello certificate</span></span>
* <span data-ttu-id="738ec-296">CertificateThumbprint, usata per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="738ec-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="738ec-297">Hello di esempio seguente viene illustrato come toouse hello comando:</span><span class="sxs-lookup"><span data-stu-id="738ec-297">hello following example shows how toouse hello command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="738ec-298">L'esecuzione di hello precedente consente di comando hello tre stringhe, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="738ec-298">Executing hello preceding command gives you hello three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="738ec-299">nome del soggetto del certificato Hello deve corrispondere dominio hello utilizzare cluster di Service Fabric tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-299">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="738ec-300">Questa corrispondenza è obbligatorio tooprovide SSL per l'endpoint di gestione del cluster hello HTTPS e Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="738ec-300">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="738ec-301">È possibile ottenere un certificato SSL da un'autorità di certificazione per hello `.cloudapp.azure.com` dominio.</span><span class="sxs-lookup"><span data-stu-id="738ec-301">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="738ec-302">È necessario ottenere un nome di dominio personalizzato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="738ec-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="738ec-303">Quando si richiede un certificato da un'autorità di certificazione, hello Nome soggetto del certificato deve corrispondere nome di dominio personalizzato hello utilizzati per il cluster.</span><span class="sxs-lookup"><span data-stu-id="738ec-303">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="738ec-304">Questi nomi di oggetto sono voci hello è necessario toocreate un cluster di Service Fabric sicuro (senza Azure AD), come descritto in [parametri di modello Configure Resource Manager](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="738ec-304">These subject names are hello entries you need toocreate a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="738ec-305">È possibile connettersi toohello sicura cluster seguendo le istruzioni di hello per [cluster tooa di accesso client di autenticazione](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="738ec-305">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="738ec-306">I cluster di anteprima Linux non supportano l'autenticazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="738ec-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="738ec-307">È possibile assegnare ruoli amministratore e client, come descritto in hello [assegnare ruoli toousers](#assign-roles) sezione.</span><span class="sxs-lookup"><span data-stu-id="738ec-307">You can assign admin and client roles as described in hello [Assign roles toousers](#assign-roles) section.</span></span> <span data-ttu-id="738ec-308">Quando si specificano i ruoli di amministratore e il client per un cluster di anteprima di Linux, è necessario tooprovide identificazioni personali del certificato per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="738ec-308">When you specify admin and client roles for a Linux preview cluster, you have tooprovide certificate thumbprints for authentication.</span></span> <span data-ttu-id="738ec-309">(Non si specifica il nome di soggetto hello, perché non viene eseguita alcuna convalida della catena o revoche di certificati in questa versione di anteprima.)</span><span class="sxs-lookup"><span data-stu-id="738ec-309">(You do not provide hello subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="738ec-310">Se si desidera toouse un certificato autofirmato per il test, è possibile utilizzare hello toogenerate script stesso uno.</span><span class="sxs-lookup"><span data-stu-id="738ec-310">If you want toouse a self-signed certificate for testing, you can use hello same script toogenerate one.</span></span> <span data-ttu-id="738ec-311">È quindi possibile caricare l'insieme di credenziali chiave hello certificato tooyour fornendo flag hello `ss` anziché specificare il nome del certificato hello percorso e il certificato.</span><span class="sxs-lookup"><span data-stu-id="738ec-311">You can then upload hello certificate tooyour key vault by providing hello flag `ss` instead of providing hello certificate path and certificate name.</span></span> <span data-ttu-id="738ec-312">Ad esempio, vedere hello comando per la creazione e caricamento di un certificato autofirmato seguente:</span><span class="sxs-lookup"><span data-stu-id="738ec-312">For example, see hello following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="738ec-313">Questo comando restituisce hello stesso tre stringhe: SourceVault CertificateUrl e CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="738ec-313">This command returns hello same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="738ec-314">È quindi possibile utilizzare hello stringhe toocreate sia un cluster protetto di Linux e un percorso in cui viene inserito certificato autofirmato hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-314">You can then use hello strings toocreate both a secure Linux cluster and a location where hello self-signed certificate is placed.</span></span> <span data-ttu-id="738ec-315">È necessario hello certificato autofirmato tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="738ec-315">You need hello self-signed certificate tooconnect toohello cluster.</span></span> <span data-ttu-id="738ec-316">È possibile connettersi toohello sicura cluster seguendo le istruzioni di hello per [cluster tooa di accesso client di autenticazione](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="738ec-316">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="738ec-317">nome del soggetto del certificato Hello deve corrispondere dominio hello utilizzare cluster di Service Fabric tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-317">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="738ec-318">Questa corrispondenza è obbligatorio tooprovide SSL per l'endpoint di gestione del cluster hello HTTPS e Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="738ec-318">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="738ec-319">È possibile ottenere un certificato SSL da un'autorità di certificazione per hello `.cloudapp.azure.com` dominio.</span><span class="sxs-lookup"><span data-stu-id="738ec-319">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="738ec-320">È necessario ottenere un nome di dominio personalizzato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="738ec-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="738ec-321">Quando si richiede un certificato da un'autorità di certificazione, hello Nome soggetto del certificato deve corrispondere nome di dominio personalizzato hello utilizzati per il cluster.</span><span class="sxs-lookup"><span data-stu-id="738ec-321">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="738ec-322">È possibile compilare i parametri di hello dallo script di supporto hello in hello portale di Azure, come descritto in hello [creare un cluster nel portale di Azure hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) sezione.</span><span class="sxs-lookup"><span data-stu-id="738ec-322">You can fill hello parameters from hello helper script in hello Azure portal, as described in hello [Create a cluster in hello Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="738ec-323">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="738ec-323">Next steps</span></span>
<span data-ttu-id="738ec-324">A questo punto, è stato creato un cluster con Azure Active Directory che fornisce l'autenticazione per la gestione.</span><span class="sxs-lookup"><span data-stu-id="738ec-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="738ec-325">Successivamente, [connettersi cluster tooyour](service-fabric-connect-to-secure-cluster.md) e informazioni su come troppo[gestire segreti applicazione](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="738ec-325">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="738ec-326">Risoluzione dei problemi di configurazione di Azure Active Directory per l'autenticazione client</span><span class="sxs-lookup"><span data-stu-id="738ec-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="738ec-327">Se verifica un problema mentre si sta configurando Azure AD per l'autenticazione client, esaminare le potenziali soluzioni hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="738ec-327">If you run into an issue while you're setting up Azure AD for client authentication, review hello potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a><span data-ttu-id="738ec-328">Si tooselect un certificato viene richiesto di Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="738ec-328">Service Fabric Explorer prompts you tooselect a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="738ec-329">Problema</span><span class="sxs-lookup"><span data-stu-id="738ec-329">Problem</span></span>
<span data-ttu-id="738ec-330">Dopo l'accesso correttamente in Service Fabric Explorer tooAzure Active Directory, il browser hello restituisce toohello home page di ma si tooselect un certificato verrà visualizzato un messaggio.</span><span class="sxs-lookup"><span data-stu-id="738ec-330">After you sign in successfully tooAzure AD in Service Fabric Explorer, hello browser returns toohello home page but a message prompts you tooselect a certificate.</span></span>

![Finestra di dialogo di selezione certificato in SFX][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="738ec-332">Motivo</span><span class="sxs-lookup"><span data-stu-id="738ec-332">Reason</span></span>
<span data-ttu-id="738ec-333">utente Hello non è assegnato un ruolo in hello applicazione cluster di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="738ec-333">hello user isn’t assigned a role in hello Azure AD cluster application.</span></span> <span data-ttu-id="738ec-334">Di conseguenza, l'autenticazione di Azure AD non riesce nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="738ec-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="738ec-335">Service Fabric Explorer fallback toocertificate autenticazione.</span><span class="sxs-lookup"><span data-stu-id="738ec-335">Service Fabric Explorer falls back toocertificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="738ec-336">Soluzione</span><span class="sxs-lookup"><span data-stu-id="738ec-336">Solution</span></span>
<span data-ttu-id="738ec-337">Seguire le istruzioni di hello per la configurazione di Azure AD e Assegna ruoli utente.</span><span class="sxs-lookup"><span data-stu-id="738ec-337">Follow hello instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="738ec-338">Inoltre, è consigliabile attivare "Utente assegnazione tooaccess obbligatorio app", come `SetupApplications.ps1` does.</span><span class="sxs-lookup"><span data-stu-id="738ec-338">Also, we recommend that you turn on “User assignment required tooaccess app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a><span data-ttu-id="738ec-339">Connessione con PowerShell non riesce con errore: "hello specificato credenziali non sono valide"</span><span class="sxs-lookup"><span data-stu-id="738ec-339">Connection with PowerShell fails with an error: "hello specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="738ec-340">Problema</span><span class="sxs-lookup"><span data-stu-id="738ec-340">Problem</span></span>
<span data-ttu-id="738ec-341">Quando si usa PowerShell tooconnect toohello cluster utilizzando la modalità di sicurezza "AzureActiveDirectory", dopo l'accesso correttamente tooAzure Active Directory, connessione hello ha esito negativo con errore: "hello specificato credenziali non sono valide."</span><span class="sxs-lookup"><span data-stu-id="738ec-341">When you use PowerShell tooconnect toohello cluster by using “AzureActiveDirectory” security mode, after you sign in successfully tooAzure AD, hello connection fails with an error: "hello specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="738ec-342">Soluzione</span><span class="sxs-lookup"><span data-stu-id="738ec-342">Solution</span></span>
<span data-ttu-id="738ec-343">Questa soluzione è hello che identico hello uno precedente.</span><span class="sxs-lookup"><span data-stu-id="738ec-343">This solution is hello same as hello preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="738ec-344">Service Fabric Explorer restituisce un errore durante l'accesso: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="738ec-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="738ec-345">Problema</span><span class="sxs-lookup"><span data-stu-id="738ec-345">Problem</span></span>
<span data-ttu-id="738ec-346">Quando si tenta di toosign in tooAzure AD in Service Fabric Explorer, pagina hello restituisce un errore: "AADSTS50011: hello indirizzo di risposta &lt;url&gt; non corrispondono agli indirizzi di risposta hello configurati per l'applicazione hello: &lt;guid&gt;."</span><span class="sxs-lookup"><span data-stu-id="738ec-346">When you try toosign in tooAzure AD in Service Fabric Explorer, hello page returns a failure: "AADSTS50011: hello reply address &lt;url&gt; does not match hello reply addresses configured for hello application: &lt;guid&gt;."</span></span>

![Indirizzo di risposta di SFX non corrispondente][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="738ec-348">Motivo</span><span class="sxs-lookup"><span data-stu-id="738ec-348">Reason</span></span>
<span data-ttu-id="738ec-349">un'applicazione Hello cluster (web) che rappresenta Service Fabric Explorer tenta tooauthenticate con Azure AD e come parte della richiesta di hello fornisce hello URL restituito di reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="738ec-349">hello cluster (web) application that represents Service Fabric Explorer attempts tooauthenticate against Azure AD, and as part of hello request it provides hello redirect return URL.</span></span> <span data-ttu-id="738ec-350">Ma hello URL non è elencato in un'applicazione hello Azure AD **URL di risposta** elenco.</span><span class="sxs-lookup"><span data-stu-id="738ec-350">But hello URL is not listed in hello Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="738ec-351">Soluzione</span><span class="sxs-lookup"><span data-stu-id="738ec-351">Solution</span></span>
<span data-ttu-id="738ec-352">In hello **configura** scheda di hello cluster applicazione (web), aggiungere hello URL di Service Fabric Explorer toohello **URL di risposta** elenco o sostituire uno degli elementi di hello nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="738ec-352">On hello **Configure** tab of hello cluster (web) application, add hello URL of Service Fabric Explorer toohello **REPLY URL** list or replace one of hello items in hello list.</span></span> <span data-ttu-id="738ec-353">Al termine, salvare la modifica.</span><span class="sxs-lookup"><span data-stu-id="738ec-353">When you have finished, save your change.</span></span>

![URL di risposta dell'applicazione Web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="738ec-355">Connettere il cluster di hello utilizzando l'autenticazione di Azure AD tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="738ec-355">Connect hello cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="738ec-356">cluster di Service Fabric hello tooconnect, utilizzare hello esempio di comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="738ec-356">tooconnect hello Service Fabric cluster, use hello following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="738ec-357">toolearn sul cmdlet Connect-ServiceFabricCluster hello, vedere [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="738ec-357">toolearn about hello Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="738ec-358">È possibile riutilizzare il tenant di hello stesso Azure Active Directory in più cluster?</span><span class="sxs-lookup"><span data-stu-id="738ec-358">Can I reuse hello same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="738ec-359">Sì.</span><span class="sxs-lookup"><span data-stu-id="738ec-359">Yes.</span></span> <span data-ttu-id="738ec-360">Ma tenere presente che un'applicazione tooadd hello URL di Service Fabric Explorer tooyour cluster (web).</span><span class="sxs-lookup"><span data-stu-id="738ec-360">But remember tooadd hello URL of Service Fabric Explorer tooyour cluster (web) application.</span></span> <span data-ttu-id="738ec-361">In caso contrario, Service Fabric Explorer non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="738ec-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="738ec-362">Perché è ancora necessario un certificato del server se Azure AD è abilitato?</span><span class="sxs-lookup"><span data-stu-id="738ec-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="738ec-363">FabricClient e FabricGateway eseguono un'autenticazione reciproca.</span><span class="sxs-lookup"><span data-stu-id="738ec-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="738ec-364">Durante l'autenticazione di Azure AD, integrazione di Azure AD fornisce un client server toohello delle identità e certificato del server hello è l'identità del server hello tooverify utilizzato.</span><span class="sxs-lookup"><span data-stu-id="738ec-364">During Azure AD authentication, Azure AD integration provides a client identity toohello server, and hello server certificate is used tooverify hello server identity.</span></span> <span data-ttu-id="738ec-365">Per altre informazioni sui certificati di Service Fabric, vedere [Certificati X.509 e Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="738ec-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

