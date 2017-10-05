---
title: Creare un cluster di Azure Service Fabric da un modello | Documentazione Microsoft
description: Questo articolo descrive come configurare un cluster di Service Fabric sicuro in Azure usando Azure Resource Manager, Azure Key Vault e Azure Active Directory (Azure AD) per l'autenticazione client.
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
ms.openlocfilehash: 420ea486e626763af65a23e49ce04033ea418fb4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="29110-103">Creare un cluster di Service Fabric usando Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29110-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29110-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29110-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="29110-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="29110-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="29110-106">Questo articolo contiene una guida dettagliata che illustra la configurazione di un cluster di Azure Service Fabric sicuro in Azure tramite Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29110-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="29110-107">Anche se l'articolo è lungo,</span><span class="sxs-lookup"><span data-stu-id="29110-107">We acknowledge that the article is long.</span></span> <span data-ttu-id="29110-108">a meno che non si conosca già a fondo il contenuto, assicurarsi di seguire con attenzione ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="29110-108">Nevertheless, unless you are already thoroughly familiar with the content, be sure to follow each step carefully.</span></span>

<span data-ttu-id="29110-109">La guida illustra le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="29110-109">The guide covers the following procedures:</span></span>

* <span data-ttu-id="29110-110">Configurazione di un insieme di credenziali delle chiavi di Azure per caricare certificati per la sicurezza di cluster e applicazioni</span><span class="sxs-lookup"><span data-stu-id="29110-110">Setting up an Azure key vault to upload certificates for cluster and application security</span></span>
* <span data-ttu-id="29110-111">Creazione di un cluster sicuro in Azure con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29110-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="29110-112">Autenticazione degli utenti con Azure Active Directory (Azure AD) per la gestione dei cluster</span><span class="sxs-lookup"><span data-stu-id="29110-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="29110-113">Un cluster sicuro impedisce l'accesso non autorizzato alle operazioni di gestione,</span><span class="sxs-lookup"><span data-stu-id="29110-113">A secure cluster is a cluster that prevents unauthorized access to management operations.</span></span> <span data-ttu-id="29110-114">tra cui distribuzione, aggiornamento ed eliminazione di applicazioni e servizi e dei dati contenuti.</span><span class="sxs-lookup"><span data-stu-id="29110-114">This includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="29110-115">Un cluster non protetto è un cluster a cui tutti gli utenti possono connettersi in qualsiasi momento ed eseguire operazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="29110-115">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="29110-116">Anche se è possibile creare un cluster non sicuro, è consigliabile creare un cluster sicuro fin dall'inizio.</span><span class="sxs-lookup"><span data-stu-id="29110-116">Although it is possible to create an unsecure cluster, we highly recommend that you create a secure cluster from the outset.</span></span> <span data-ttu-id="29110-117">Poiché un cluster non sicuro non può essere protetto in un secondo momento, è necessario crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="29110-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="29110-118">Il concetto di creazione di cluster sicuri è lo stesso per i cluster sia Linux che Windows.</span><span class="sxs-lookup"><span data-stu-id="29110-118">The concept of creating secure clusters is the same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="29110-119">Per altre informazioni e script helper per la creazione di cluster Linux sicuri, vedere [Creare cluster protetti in Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="29110-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="29110-120">Accedere con l'account Azure</span><span class="sxs-lookup"><span data-stu-id="29110-120">Sign in to your Azure account</span></span>
<span data-ttu-id="29110-121">Questa guida usa [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="29110-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="29110-122">Quando si avvia una nuova sessione di PowerShell, accedere al proprio account Azure e selezionare la sottoscrizione prima di eseguire i comandi di Azure.</span><span class="sxs-lookup"><span data-stu-id="29110-122">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="29110-123">Accedere all'account Azure:</span><span class="sxs-lookup"><span data-stu-id="29110-123">Sign in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="29110-124">Selezionare la propria sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="29110-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="29110-125">Configurare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="29110-125">Set up a key vault</span></span>
<span data-ttu-id="29110-126">Questa sezione illustra la creazione di un insieme di credenziali delle chiavi per un cluster di Service Fabric in Azure e per le applicazioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29110-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="29110-127">Per una guida completa su Azure Key Vault, vedere la [guida introduttiva a Key Vault][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="29110-127">For a complete guide to Azure Key Vault, refer to the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="29110-128">Service Fabric usa certificati X.509 per proteggere un cluster e fornire le funzionalità di sicurezza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="29110-128">Service Fabric uses X.509 certificates to secure a cluster and provide application security features.</span></span> <span data-ttu-id="29110-129">Si usa Key Vault per gestire i certificati dei cluster di Service Fabric in Azure.</span><span class="sxs-lookup"><span data-stu-id="29110-129">You use Key Vault to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="29110-130">Quando viene distribuito un cluster in Azure, il provider di risorse di Azure responsabile della creazione di cluster Service Fabric estrae i certificati da Key Vault e li installa nelle macchine virtuali del cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-130">When a cluster is deployed in Azure, the Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="29110-131">Nel diagramma seguente viene illustrata la relazione tra Azure Key Vault, un cluster di Service Fabric e il provider di risorse di Azure che usa i certificati archiviati in un insieme di credenziali delle chiavi durante la creazione di un cluster:</span><span class="sxs-lookup"><span data-stu-id="29110-131">The following diagram illustrates the relationship between Azure Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagramma dell'installazione del certificato][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="29110-133">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="29110-133">Create a resource group</span></span>
<span data-ttu-id="29110-134">Il primo passaggio consiste nel creare un gruppo di risorse specifico per l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-134">The first step is to create a resource group specifically for your key vault.</span></span> <span data-ttu-id="29110-135">È consigliabile inserire l'insieme di credenziali delle chiavi in un proprio gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="29110-135">We recommend that you put the key vault into its own resource group.</span></span> <span data-ttu-id="29110-136">Questa azione consente di rimuovere i gruppi di risorse di calcolo e di archiviazione, incluso il gruppo di risorse contenente il cluster di Service Fabric, senza perdere le chiavi e i segreti.</span><span class="sxs-lookup"><span data-stu-id="29110-136">This action lets you remove the compute and storage resource groups, including the resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="29110-137">Il gruppo di risorse che contiene l'insieme di credenziali delle chiavi _deve essere situato nella stessa area_ del cluster che lo usa.</span><span class="sxs-lookup"><span data-stu-id="29110-137">The resource group that contains your key vault _must be in the same region_ as the cluster that is using it.</span></span>

<span data-ttu-id="29110-138">Se si prevede di distribuire i cluster in più aree, è consigliabile assegnare al gruppo di risorse e all'insieme di credenziali delle chiavi un nome indicante a quale area appartiene.</span><span class="sxs-lookup"><span data-stu-id="29110-138">If you plan to deploy clusters in multiple regions, we suggest that you name the resource group and the key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="29110-139">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="29110-139">The output should look like this:</span></span>

```powershell

    WARNING: The output object type of this cmdlet is going to be modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-the-new-resource-group"></a><span data-ttu-id="29110-140">Creare un insieme di credenziali delle chiavi nel nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="29110-140">Create a key vault in the new resource group</span></span>
<span data-ttu-id="29110-141">L'insieme di credenziali delle chiavi _deve essere abilitato per la distribuzione_ per consentire al provider di risorse di calcolo di ottenere i certificati e installarli nelle istanze delle macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="29110-141">The key vault _must be enabled for deployment_ to allow the compute resource provider to get certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="29110-142">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="29110-142">The output should look like this:</span></span>

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
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="29110-143">Usare un insieme di credenziali delle chiavi esistente</span><span class="sxs-lookup"><span data-stu-id="29110-143">Use an existing key vault</span></span>

<span data-ttu-id="29110-144">Per usare un insieme di credenziali delle chiavi esistente, è _necessario abilitarlo per la distribuzione_ per consentire al provider di risorse di calcolo di ottenere i certificati e installarli nei nodi del cluster:</span><span class="sxs-lookup"><span data-stu-id="29110-144">To use an existing key vault, you _must enable it for deployment_ to allow the compute resource provider to get certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-to-your-key-vault"></a><span data-ttu-id="29110-145">Aggiungere i certificati all'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="29110-145">Add certificates to your key vault</span></span>

<span data-ttu-id="29110-146">I certificati vengono usati in Service Fabric per fornire l'autenticazione e la crittografia e proteggere i vari aspetti di un cluster e delle sue applicazioni.</span><span class="sxs-lookup"><span data-stu-id="29110-146">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="29110-147">Per altre informazioni sull'uso dei certificati in Service Fabric, vedere [Scenari di sicurezza di un cluster di Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="29110-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="29110-148">Cluster e certificato del server (obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="29110-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="29110-149">Questo certificato è richiesto per proteggere un cluster e impedirne accessi non autorizzati.</span><span class="sxs-lookup"><span data-stu-id="29110-149">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="29110-150">Il certificato fornisce protezione del cluster in due modi:</span><span class="sxs-lookup"><span data-stu-id="29110-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="29110-151">Autenticazione del cluster: autentica la comunicazione da nodo a nodo per la federazione di cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="29110-152">Solo i nodi che possono dimostrare la propria identità con il certificato possono essere aggiunti al cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-152">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="29110-153">Autenticazione del server: autentica gli endpoint di gestione del cluster in un client di gestione, in modo che il client di gestione sappia con certezza di comunicare con il cluster reale.</span><span class="sxs-lookup"><span data-stu-id="29110-153">Server authentication: Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="29110-154">Questo certificato fornisce anche un certificato SSL per l'API di gestione HTTPS e per Service Fabric Explorer tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="29110-154">This certificate also provides an SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="29110-155">A tale scopo, il certificato deve soddisfare i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="29110-155">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="29110-156">Il certificato deve includere una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="29110-156">The certificate must contain a private key.</span></span>
* <span data-ttu-id="29110-157">Il certificato deve essere stato creato per lo scambio di chiave, esportabile in un file con estensione pfx (Personal Information Exchange).</span><span class="sxs-lookup"><span data-stu-id="29110-157">The certificate must be created for key exchange, which is exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="29110-158">Il nome del soggetto del certificato deve corrispondere al dominio usato per accedere al cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29110-158">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="29110-159">Questa corrispondenza è necessaria per fornire un certificato SSL per gli endpoint di gestione HTTPS del cluster e Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="29110-159">This matching is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="29110-160">Non è possibile ottenere un certificato SSL da un'Autorità di certificazione (CA) per il dominio .cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="29110-160">You cannot obtain an SSL certificate from a certificate authority (CA) for the .cloudapp.azure.com domain.</span></span> <span data-ttu-id="29110-161">È necessario ottenere un nome di dominio personalizzato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="29110-162">Quando si richiede un certificato da una CA, il nome del soggetto del certificato deve corrispondere al nome di dominio personalizzato usato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-162">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="29110-163">Certificati delle applicazioni (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="29110-163">Application certificates (optional)</span></span>
<span data-ttu-id="29110-164">Per motivi di sicurezza dell'applicazione, è possibile installare nel cluster numerosi certificati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="29110-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="29110-165">Prima di creare il cluster, considerare gli scenari di protezione delle applicazioni che richiedono l'installazione di un certificato sui nodi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="29110-165">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="29110-166">Crittografia e decrittografia dei valori di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="29110-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="29110-167">Crittografia dei dati tra i nodi durante la replica.</span><span class="sxs-lookup"><span data-stu-id="29110-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="29110-168">Formattazione dei certificati per l'uso di provider di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="29110-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="29110-169">È possibile aggiungere e usare file di chiave privata (PFX) direttamente tramite l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="29110-170">Il provider di risorse di calcolo di Azure richiede tuttavia che le chiavi vengano archiviate in uno speciale formato JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="29110-170">However, the Azure compute resource provider requires keys to be stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="29110-171">Il formato include il file PFX come stringa con codifica Base 64 e la password della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="29110-171">The format includes the .pfx file as a base 64-encoded string and the private key password.</span></span> <span data-ttu-id="29110-172">Per soddisfare questi requisiti, le chiavi devono essere inserite in una stringa JSON e quindi archiviate come "segreti" nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-172">To accommodate these requirements, the keys must be placed in a JSON string and then stored as "secrets" in the key vault.</span></span>

<span data-ttu-id="29110-173">Per semplificare questo processo, è [disponibile su GitHub un modulo di PowerShell][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="29110-173">To make this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="29110-174">Per usare il modulo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="29110-174">To use the module, do the following:</span></span>

1. <span data-ttu-id="29110-175">Scaricare l'intero contenuto del repository in una directory locale.</span><span class="sxs-lookup"><span data-stu-id="29110-175">Download the entire contents of the repo into a local directory.</span></span>
2. <span data-ttu-id="29110-176">Andare alla directory locale.</span><span class="sxs-lookup"><span data-stu-id="29110-176">Go to the local directory.</span></span>
2. <span data-ttu-id="29110-177">Importare il modulo ServiceFabricRPHelpers nella finestra di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="29110-177">Import the ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="29110-178">Il comando `Invoke-AddCertToKeyVault` in questo modulo di PowerShell formatta in modo automatico una chiave privata del certificato in una stringa JSON e la carica nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-178">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to the key vault.</span></span> <span data-ttu-id="29110-179">Usare il comando per aggiungere il certificato del cluster ed eventuali altri certificati delle applicazioni all'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-179">Use the command to add the cluster certificate and any additional application certificates to the key vault.</span></span> <span data-ttu-id="29110-180">Ripetere questo passaggio per tutti i certificati aggiuntivi che si vuole installare nel cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-180">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="29110-181">Caricamento di un certificato esistente</span><span class="sxs-lookup"><span data-stu-id="29110-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="29110-182">Se si verifica un errore, come quello illustrato qui, in genere significa che è presente un conflitto tra URL di risorsa.</span><span class="sxs-lookup"><span data-stu-id="29110-182">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="29110-183">Per risolvere il conflitto, modificare il nome dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-183">To resolve the conflict, change the key vault name.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="29110-184">Dopo avere risolto il conflitto, l'output sarà il seguente:</span><span class="sxs-lookup"><span data-stu-id="29110-184">After the conflict is resolved, the output should look like this:</span></span>

```

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: The output object type of this cmdlet is going to be modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to mywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="29110-185">Sono necessarie le tre stringhe precedenti, CertificateThumbprint, SourceVault e CertificateURL, per configurare un cluster di Service Fabric sicuro e per ottenere i certificati dell'applicazione che potrebbero essere usati per la sicurezza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="29110-185">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="29110-186">Se non si salvano le stringhe, può essere difficile recuperarle in seguito effettuando una query dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-186">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-to-the-key-vault"></a><span data-ttu-id="29110-187">Creazione di un certificato autofirmato e caricamento nell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="29110-187">Creating a self-signed certificate and uploading it to the key vault</span></span>

<span data-ttu-id="29110-188">Se i certificati sono già stati caricati nell'insieme di credenziali delle chiavi, saltare questo passaggio</span><span class="sxs-lookup"><span data-stu-id="29110-188">If you have already uploaded your certificates to the key vault, skip this step.</span></span> <span data-ttu-id="29110-189">che serve a generare un nuovo certificato autofirmato e a caricarlo nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-189">This step is for generating a new self-signed certificate and uploading it to your key vault.</span></span> <span data-ttu-id="29110-190">Dopo avere modificato i parametri nello script seguente e averlo eseguito, verrà chiesta una password per il certificato.</span><span class="sxs-lookup"><span data-stu-id="29110-190">After you change the parameters in the following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #The certificate's subject name must match the domain used to access the Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want the .PFX to be stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="29110-191">Se si verifica un errore, come quello illustrato qui, in genere significa che è presente un conflitto tra URL di risorsa.</span><span class="sxs-lookup"><span data-stu-id="29110-191">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="29110-192">Per risolvere il conflitto, modificare il nome dell'insieme di credenziali delle chiavi, il nome del gruppo di risorse e così via.</span><span class="sxs-lookup"><span data-stu-id="29110-192">To resolve the conflict, change the key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="29110-193">Dopo avere risolto il conflitto, l'output sarà il seguente:</span><span class="sxs-lookup"><span data-stu-id="29110-193">After the conflict is resolved, the output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context to SubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: The output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret to chackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="29110-194">Sono necessarie le tre stringhe precedenti, CertificateThumbprint, SourceVault e CertificateURL, per configurare un cluster di Service Fabric sicuro e per ottenere i certificati dell'applicazione che potrebbero essere usati per la sicurezza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="29110-194">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="29110-195">Se non si salvano le stringhe, può essere difficile recuperarle in seguito effettuando una query dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-195">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

 <span data-ttu-id="29110-196">A questo punto, dovrebbero essere visualizzati gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="29110-196">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="29110-197">Gruppo di risorse dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-197">The key vault resource group.</span></span>
* <span data-ttu-id="29110-198">Insieme di credenziali delle chiavi e URL (denominato SourceVault nell'output di PowerShell precedente).</span><span class="sxs-lookup"><span data-stu-id="29110-198">The key vault and its URL (called SourceVault in the preceding PowerShell output).</span></span>
* <span data-ttu-id="29110-199">Certificato di autenticazione server del cluster e URL nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-199">The cluster server authentication certificate and its URL in the key vault.</span></span>
* <span data-ttu-id="29110-200">Certificati dell'applicazione e URL nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="29110-200">The application certificates and their URLs in the key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="29110-201">Configurare Azure Active Directory per l'autenticazione client</span><span class="sxs-lookup"><span data-stu-id="29110-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="29110-202">Azure AD consente alle organizzazioni (note come tenant) di gestire l'accesso utenti alle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="29110-202">Azure AD enables organizations (known as tenants) to manage user access to applications.</span></span> <span data-ttu-id="29110-203">Alcune applicazioni sono caratterizzate da un'interfaccia utente di accesso basata sul Web, altre invece da un'esperienza client nativa.</span><span class="sxs-lookup"><span data-stu-id="29110-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="29110-204">In questo articolo si presuppone che sia già stato creato un tenant.</span><span class="sxs-lookup"><span data-stu-id="29110-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="29110-205">In caso contrario, vedere prima di tutto [Come ottenere un tenant di Azure Active Directory][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="29110-205">If you have not, start by reading [How to get an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="29110-206">I cluster di Service Fabric offrono numerosi punti di ingresso alle relative funzionalità di gestione, tra cui [Service Fabric Explorer][service-fabric-visualizing-your-cluster], basato sul Web, e [Visual Studio][service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="29110-206">A Service Fabric cluster offers several entry points to its management functionality, including the web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="29110-207">Verranno quindi create due applicazioni Azure AD per controllare l'accesso al cluster, un'applicazione Web e un'applicazione nativa.</span><span class="sxs-lookup"><span data-stu-id="29110-207">As a result, you create two Azure AD applications to control access to the cluster, one web application and one native application.</span></span>

<span data-ttu-id="29110-208">Per semplificare alcuni dei passaggi richiesti per la configurazione di Azure AD con un cluster di Service Fabric è stato creato un set di script di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29110-208">To simplify some of the steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="29110-209">È necessario completare i passaggi seguenti prima di creare il cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-209">You must complete the following steps before you create the cluster.</span></span> <span data-ttu-id="29110-210">Poiché per gli script sono previsti nomi ed endpoint dei cluster, i valori devono essere pianificati e non quelli già creati.</span><span class="sxs-lookup"><span data-stu-id="29110-210">Because the scripts expect cluster names and endpoints, the values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="29110-211">[Scaricare gli script][sf-aad-ps-script-download] nel computer.</span><span class="sxs-lookup"><span data-stu-id="29110-211">[Download the scripts][sf-aad-ps-script-download] to your computer.</span></span>
2. <span data-ttu-id="29110-212">Fare clic con il pulsante destro del mouse sul file ZIP, scegliere **Proprietà**, selezionare la casella di controllo **Sblocca** e quindi fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="29110-212">Right-click the zip file, select **Properties**, select the **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="29110-213">Estrarre il file con estensione zip.</span><span class="sxs-lookup"><span data-stu-id="29110-213">Extract the zip file.</span></span>
4. <span data-ttu-id="29110-214">Eseguire `SetupApplications.ps1` e indicare i parametri TenantId, ClusterName e WebApplicationReplyUrl.</span><span class="sxs-lookup"><span data-stu-id="29110-214">Run `SetupApplications.ps1`, and provide the TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="29110-215">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="29110-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="29110-216">È possibile trovare il TenantId eseguendo il comando di PowerShell `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="29110-216">You can find your TenantId by executing the PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="29110-217">Eseguendo questo comando, viene visualizzato il TenantId per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="29110-217">Executing this command displays the TenantId for every subscription.</span></span>

    <span data-ttu-id="29110-218">ClusterName viene usato come prefisso per le applicazioni Azure AD create dallo script.</span><span class="sxs-lookup"><span data-stu-id="29110-218">ClusterName is used to prefix the Azure AD applications that are created by the script.</span></span> <span data-ttu-id="29110-219">Non è necessario che corrisponda esattamente al nome effettivo del cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-219">It does not need to match the actual cluster name exactly.</span></span> <span data-ttu-id="29110-220">Ha solo lo scopo di facilitare il mapping degli elementi di Azure AD al cluster di Service Fabric con cui vengono usati.</span><span class="sxs-lookup"><span data-stu-id="29110-220">It is intended only to make it easier to map Azure AD artifacts to the Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="29110-221">WebApplicationReplyUrl è l'endpoint predefinito che Azure AD restituisce agli utenti dopo che hanno completato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="29110-221">WebApplicationReplyUrl is the default endpoint that Azure AD returns to your users after they finish signing in.</span></span> <span data-ttu-id="29110-222">Impostare questo endpoint come endpoint di Service Fabric Explorer per il cluster, che per impostazione predefinita è:</span><span class="sxs-lookup"><span data-stu-id="29110-222">Set this endpoint as the Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="29110-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="29110-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="29110-224">Verrà richiesto di accedere a un account con privilegi amministrativi per il tenant Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29110-224">You are prompted to sign in to an account that has administrative privileges for the Azure AD tenant.</span></span> <span data-ttu-id="29110-225">Dopo avere eseguito l'accesso, lo script crea l'applicazione Web e l'applicazione nativa per rappresentare il cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29110-225">After you sign in, the script creates the web and native applications to represent your Service Fabric cluster.</span></span> <span data-ttu-id="29110-226">Tra le applicazioni del tenant nel [portale di Azure classico][azure-classic-portal] dovrebbero essere visualizzate due nuove voci:</span><span class="sxs-lookup"><span data-stu-id="29110-226">If you look at the tenant's applications in the [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="29110-227">*ClusterName*\_Cluster</span><span class="sxs-lookup"><span data-stu-id="29110-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="29110-228">*ClusterName*\_Client</span><span class="sxs-lookup"><span data-stu-id="29110-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="29110-229">È consigliabile tenere aperta la finestra di PowerShell perché, durante la creazione del cluster nella sezione successiva, lo script stamperà il codice JSON richiesto dal modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29110-229">The script prints the JSON required by the Azure Resource Manager template when you create the cluster in the next section, so it's a good idea to keep the PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="29110-230">Creare un modello di Cluster Resource Manager di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="29110-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="29110-231">In questa sezione, gli output dei comandi di PowerShell precedenti verranno usati in un modello di Resource Manager per cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29110-231">In this section, the outputs of the preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="29110-232">Nella [raccolta di modelli di avvio rapido di Azure in GitHub][azure-quickstart-templates] sono disponibili alcuni modelli di Resource Manager di esempio.</span><span class="sxs-lookup"><span data-stu-id="29110-232">Sample Resource Manager templates are available in the [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="29110-233">Questi modelli possono essere usati come punto di partenza per il modello del cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-the-resource-manager-template"></a><span data-ttu-id="29110-234">Creare il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29110-234">Create the Resource Manager template</span></span>
<span data-ttu-id="29110-235">Questa guida usa il modello di esempio di un [cluster protetto a 5 nodi][service-fabric-secure-cluster-5-node-1-nodetype] e i relativi parametri.</span><span class="sxs-lookup"><span data-stu-id="29110-235">This guide uses the [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="29110-236">Scaricare `azuredeploy.json` e `azuredeploy.parameters.json` sul computer e aprire entrambi i file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="29110-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` to your computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="29110-237">Aggiungere certificati</span><span class="sxs-lookup"><span data-stu-id="29110-237">Add certificates</span></span>
<span data-ttu-id="29110-238">I certificati vengono aggiunti a un modello di Resource Manager per cluster facendo riferimento all'insieme di credenziali delle chiavi che contiene le chiavi del certificato.</span><span class="sxs-lookup"><span data-stu-id="29110-238">You add certificates to a cluster Resource Manager template by referencing the key vault that contains the certificate keys.</span></span> <span data-ttu-id="29110-239">È consigliabile inserire i valori dell'insieme di credenziali delle chiavi in un file di parametri del modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29110-239">We recommend that you place the key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="29110-240">In questo modo, il file di modello di Resource Manager è riutilizzabile e non contiene valori specifici di una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="29110-240">Doing so keeps the Resource Manager template file reusable and free of values specific to a deployment.</span></span>

#### <a name="add-all-certificates-to-the-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="29110-241">Aggiungere tutti i certificati all'elemento osProfile del set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="29110-241">Add all certificates to the virtual machine scale set osProfile</span></span>
<span data-ttu-id="29110-242">Ogni certificato che viene installato nel cluster deve essere configurato nella sezione osProfile della risorsa del set di scalabilità (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="29110-242">Every certificate that's installed in the cluster must be configured in the osProfile section of the scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="29110-243">Questa azione indica al provider di risorse di installare il certificato nelle macchine virtuali,</span><span class="sxs-lookup"><span data-stu-id="29110-243">This action instructs the resource provider to install the certificate on the VMs.</span></span> <span data-ttu-id="29110-244">includendo sia il certificato del cluster che eventuali certificati di sicurezza dell'applicazione che si intende usare per le applicazioni:</span><span class="sxs-lookup"><span data-stu-id="29110-244">This installation includes both the cluster certificate and any application security certificates that you plan to use for your applications:</span></span>

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

#### <a name="configure-the-service-fabric-cluster-certificate"></a><span data-ttu-id="29110-245">Configurare il certificato del cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="29110-245">Configure the Service Fabric cluster certificate</span></span>
<span data-ttu-id="29110-246">Il certificato di autenticazione del cluster deve essere configurato sia nella risorsa del cluster di Service Fabric (Microsoft.ServiceFabric/clusters) che nell'estensione di Service Fabric per i set di scalabilità di macchine virtuali nella risorsa del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="29110-246">The cluster authentication certificate must be configured in both the Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and the Service Fabric extension for virtual machine scale sets in the virtual machine scale set resource.</span></span> <span data-ttu-id="29110-247">Questa disposizione consente al provider di risorse di Service Fabric di configurarlo per l'uso dell'autenticazione del cluster e del server per gli endpoint di gestione.</span><span class="sxs-lookup"><span data-stu-id="29110-247">This arrangement allows the Service Fabric resource provider to configure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="29110-248">Risorsa del set di scalabilità di macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="29110-248">Virtual machine scale set resource:</span></span>
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

##### <a name="service-fabric-resource"></a><span data-ttu-id="29110-249">Risorsa di Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="29110-249">Service Fabric resource:</span></span>
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

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="29110-250">Inserire la configurazione di Azure AD</span><span class="sxs-lookup"><span data-stu-id="29110-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="29110-251">La configurazione di Azure AD creata prima può essere inserita nel modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29110-251">The Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="29110-252">È tuttavia consigliabile estrarre prima i valori in un file di parametri in modo che il modello di Resource Manager sia riutilizzabile e non contenga valori specifici di una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="29110-252">However, we recommended that you first extract the values into a parameters file to keep the Resource Manager template reusable and free of values specific to a deployment.</span></span>

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

### <span data-ttu-id="29110-253"><a "configure-arm" ></a>Configurare i parametri del modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29110-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since the link seems not to be redirecting correctly --->
<span data-ttu-id="29110-254">Infine, usare i valori di output dei comandi di PowerShell per Azure AD e dell'insieme di credenziali delle chiavi per compilare il file dei parametri:</span><span class="sxs-lookup"><span data-stu-id="29110-254">Finally, use the output values from the key vault and Azure AD PowerShell commands to populate the parameters file:</span></span>

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
<span data-ttu-id="29110-255">A questo punto, dovrebbero essere visualizzati gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="29110-255">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="29110-256">Gruppo di risorse dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="29110-256">Key vault resource group</span></span>
  * <span data-ttu-id="29110-257">Insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="29110-257">Key vault</span></span>
  * <span data-ttu-id="29110-258">Certificato di autenticazione del server del cluster</span><span class="sxs-lookup"><span data-stu-id="29110-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="29110-259">Certificato di crittografia dei dati</span><span class="sxs-lookup"><span data-stu-id="29110-259">Data encipherment certificate</span></span>
* <span data-ttu-id="29110-260">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29110-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="29110-261">Applicazione Azure AD per la gestione basata su Web e Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="29110-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="29110-262">Applicazione Azure AD per la gestione dei client nativi</span><span class="sxs-lookup"><span data-stu-id="29110-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="29110-263">Utenti e ruoli assegnati</span><span class="sxs-lookup"><span data-stu-id="29110-263">Users and their assigned roles</span></span>
* <span data-ttu-id="29110-264">Modello di Cluster Resource Manager di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="29110-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="29110-265">Certificati configurati tramite l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="29110-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="29110-266">Azure Active Directory configurato</span><span class="sxs-lookup"><span data-stu-id="29110-266">Azure Active Directory configured</span></span>

<span data-ttu-id="29110-267">Il diagramma seguente illustra i punti in cui la configurazione dell'insieme di credenziali delle chiavi e di Azure AD rientra nel modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29110-267">The following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Mappa di dipendenza di Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-the-cluster"></a><span data-ttu-id="29110-269">Creare il cluster</span><span class="sxs-lookup"><span data-stu-id="29110-269">Create the cluster</span></span>
<span data-ttu-id="29110-270">A questo punto si è pronti per creare il cluster usando la [distribuzione del modello di risorsa di Azure][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="29110-270">You are now ready to create the cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="29110-271">Eseguirne il test</span><span class="sxs-lookup"><span data-stu-id="29110-271">Test it</span></span>
<span data-ttu-id="29110-272">Usare il comando PowerShell seguente per testare il modello di Resource Manager con un file di parametri:</span><span class="sxs-lookup"><span data-stu-id="29110-272">Use the following PowerShell command to test your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="29110-273">Distribuirlo</span><span class="sxs-lookup"><span data-stu-id="29110-273">Deploy it</span></span>
<span data-ttu-id="29110-274">Se viene superato il test del modello di Resource Manager, usare il comando PowerShell seguente per distribuire il modello di Resource Manager con un file di parametri:</span><span class="sxs-lookup"><span data-stu-id="29110-274">If the Resource Manager template test passes, use the following PowerShell command to deploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-to-roles"></a><span data-ttu-id="29110-275">Assegnare utenti ai ruoli</span><span class="sxs-lookup"><span data-stu-id="29110-275">Assign users to roles</span></span>
<span data-ttu-id="29110-276">Dopo aver creato le applicazioni per rappresentare il cluster, assegnare gli utenti ai ruoli supportati da Service Fabric: sola lettura e amministratore. È possibile assegnare i ruoli usando il [portale di Azure classico][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="29110-276">After you have created the applications to represent your cluster, assign your users to the roles supported by Service Fabric: read-only and admin. You can assign the roles by using the [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="29110-277">Nel portale di Azure andare al tenant e quindi selezionare **Applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="29110-277">In the Azure portal, go to your tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="29110-278">Selezionare l'applicazione Web, che avrà un nome simile a `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="29110-278">Select the web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="29110-279">Fare clic sulla scheda **Utenti** .</span><span class="sxs-lookup"><span data-stu-id="29110-279">Click the **Users** tab.</span></span>
4. <span data-ttu-id="29110-280">Selezionare un utente per l'assegnazione e quindi fare clic sul pulsante **Assegna** nella parte inferiore della schermata.</span><span class="sxs-lookup"><span data-stu-id="29110-280">Select a user to assign, and then click the **Assign** button at the bottom of the screen.</span></span>

    ![Pulsante di assegnazione di utenti ai ruoli][assign-users-to-roles-button]
5. <span data-ttu-id="29110-282">Selezionare il ruolo da assegnare all'utente.</span><span class="sxs-lookup"><span data-stu-id="29110-282">Select the role to assign to the user.</span></span>

    ![Finestra di dialogo "Assegna utenti"][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="29110-284">Per altre informazioni sui ruoli in Service Fabric, vedere [Controllo degli accessi in base al ruolo per i client di Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="29110-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused the wrong redirection of the link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="29110-285">Creare cluster protetti in Linux</span><span class="sxs-lookup"><span data-stu-id="29110-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="29110-286">Per facilitare il processo, è disponibile uno [script helper](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="29110-286">To make the process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="29110-287">Prima di usare questo script helper, assicurarsi che sia già installata un'interfaccia della riga di comando di Azure e che sia nel percorso in uso.</span><span class="sxs-lookup"><span data-stu-id="29110-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="29110-288">Verificare che lo script abbia le autorizzazioni necessarie per l'esecuzione eseguendo `chmod +x cert_helper.py` al termine del download.</span><span class="sxs-lookup"><span data-stu-id="29110-288">Make sure that the script has permissions to execute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="29110-289">Il primo passaggio consiste nell'accedere al proprio account Azure usando il comando `azure login` nell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="29110-289">The first step is to sign in to your Azure account by using CLI with the `azure login` command.</span></span> <span data-ttu-id="29110-290">Dopo aver eseguito l'accesso all'account Azure, usare lo script helper con il certificato firmato di una CA, come illustrato dai comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="29110-290">After signing in to your Azure account, use the helper script with your CA signed certificate, as the following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="29110-291">Il parametro -ifile può accettare un file PFX o un file PEM come input, con il tipo di certificato (pfx o pem oppure ss se è un certificato autofirmato).</span><span class="sxs-lookup"><span data-stu-id="29110-291">The -ifile parameter can take a .pfx file or a .pem file as input, with the certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="29110-292">Il parametro -h visualizza il testo della guida.</span><span class="sxs-lookup"><span data-stu-id="29110-292">The parameter -h prints out the help text.</span></span>


<span data-ttu-id="29110-293">Questo comando restituisce come output le tre stringhe seguenti:</span><span class="sxs-lookup"><span data-stu-id="29110-293">This command returns the following three strings as the output:</span></span>

* <span data-ttu-id="29110-294">SourceVaultID, che è l'ID del nuovo gruppo di risorse dell'insieme di credenziali delle chiavi creato.</span><span class="sxs-lookup"><span data-stu-id="29110-294">SourceVaultID, which is the ID for the new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="29110-295">CertificateUrl per l'accesso al certificato.</span><span class="sxs-lookup"><span data-stu-id="29110-295">CertificateUrl for accessing the certificate</span></span>
* <span data-ttu-id="29110-296">CertificateThumbprint, usata per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="29110-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="29110-297">L'esempio seguente illustra come usare il comando:</span><span class="sxs-lookup"><span data-stu-id="29110-297">The following example shows how to use the command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="29110-298">Eseguendo il comando precedente si ottengono le tre stringhe come segue:</span><span class="sxs-lookup"><span data-stu-id="29110-298">Executing the preceding command gives you the three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="29110-299">Il nome del soggetto del certificato deve corrispondere al dominio usato per accedere al cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29110-299">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="29110-300">Questa corrispondenza è necessaria per fornire un certificato SSL per gli endpoint di gestione HTTPS del cluster e Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="29110-300">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="29110-301">Non è possibile ottenere un certificato SSL da una CA per il dominio `.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="29110-301">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="29110-302">È necessario ottenere un nome di dominio personalizzato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="29110-303">Quando si richiede un certificato da una CA, il nome del soggetto del certificato deve corrispondere al nome di dominio personalizzato usato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-303">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="29110-304">Questi nomi di soggetto sono le voci necessarie per creare un cluster di Service Fabric sicuro (senza Azure AD), come descritto in [Configurare i parametri del modello di Resource Manager](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="29110-304">These subject names are the entries you need to create a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="29110-305">È possibile connettersi al cluster sicuro seguendo le istruzioni per [autenticare l'accesso client a un cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="29110-305">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="29110-306">I cluster di anteprima Linux non supportano l'autenticazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29110-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="29110-307">È possibile assegnare ruoli amministratore e client come descritto nella sezione [Assegnare utenti ai ruoli](#assign-roles).</span><span class="sxs-lookup"><span data-stu-id="29110-307">You can assign admin and client roles as described in the [Assign roles to users](#assign-roles) section.</span></span> <span data-ttu-id="29110-308">Quando si specificano ruoli amministrativi e client per un cluster di anteprima Linux, è necessario fornire le identificazioni personali del certificato per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="29110-308">When you specify admin and client roles for a Linux preview cluster, you have to provide certificate thumbprints for authentication.</span></span> <span data-ttu-id="29110-309">Non si specifica il nome del soggetto perché non vengono eseguite convalide o revoche della catena in questa versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="29110-309">(You do not provide the subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="29110-310">Per usare un certificato autofirmato per il test, è possibile usare lo stesso script per generarne uno.</span><span class="sxs-lookup"><span data-stu-id="29110-310">If you want to use a self-signed certificate for testing, you can use the same script to generate one.</span></span> <span data-ttu-id="29110-311">È quindi possibile caricare il certificato nell'insieme di credenziali delle chiavi specificando il flag `ss` invece del percorso e del nome del certificato.</span><span class="sxs-lookup"><span data-stu-id="29110-311">You can then upload the certificate to your key vault by providing the flag `ss` instead of providing the certificate path and certificate name.</span></span> <span data-ttu-id="29110-312">Per la creazione e il caricamento di un certificato autofirmato, vedere ad esempio il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="29110-312">For example, see the following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="29110-313">Questo comando restituisce le stesse tre stringhe: SourceVault, CertificateUrl e CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="29110-313">This command returns the same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="29110-314">È quindi possibile usare le stringhe per creare sia un cluster Linux sicuro che una posizione in cui inserire il certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="29110-314">You can then use the strings to create both a secure Linux cluster and a location where the self-signed certificate is placed.</span></span> <span data-ttu-id="29110-315">Per connettersi al cluster, è necessario il certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="29110-315">You need the self-signed certificate to connect to the cluster.</span></span> <span data-ttu-id="29110-316">È possibile connettersi al cluster sicuro seguendo le istruzioni per [autenticare l'accesso client a un cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="29110-316">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="29110-317">Il nome del soggetto del certificato deve corrispondere al dominio usato per accedere al cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29110-317">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="29110-318">Questa corrispondenza è necessaria per fornire un certificato SSL per gli endpoint di gestione HTTPS del cluster e Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="29110-318">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="29110-319">Non è possibile ottenere un certificato SSL da una CA per il dominio `.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="29110-319">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="29110-320">È necessario ottenere un nome di dominio personalizzato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="29110-321">Quando si richiede un certificato da una CA, il nome del soggetto del certificato deve corrispondere al nome di dominio personalizzato usato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="29110-321">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="29110-322">È possibile immettere i parametri dello script helper nel portale di Azure, come descritto nella sezione [Creare un cluster nel portale di Azure](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="29110-322">You can fill the parameters from the helper script in the Azure portal, as described in the [Create a cluster in the Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29110-323">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="29110-323">Next steps</span></span>
<span data-ttu-id="29110-324">A questo punto, è stato creato un cluster con Azure Active Directory che fornisce l'autenticazione per la gestione.</span><span class="sxs-lookup"><span data-stu-id="29110-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="29110-325">Successivamente, [connettersi al cluster](service-fabric-connect-to-secure-cluster.md) e scoprire come [gestire i segreti delle applicazioni](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="29110-325">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="29110-326">Risoluzione dei problemi di configurazione di Azure Active Directory per l'autenticazione client</span><span class="sxs-lookup"><span data-stu-id="29110-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="29110-327">Se si verifica un problema durante la configurazione di Azure AD per l'autenticazione client, vedere le potenziali soluzioni in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="29110-327">If you run into an issue while you're setting up Azure AD for client authentication, review the potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-to-select-a-certificate"></a><span data-ttu-id="29110-328">Service Fabric Explorer richiede di selezionare un certificato</span><span class="sxs-lookup"><span data-stu-id="29110-328">Service Fabric Explorer prompts you to select a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="29110-329">Problema</span><span class="sxs-lookup"><span data-stu-id="29110-329">Problem</span></span>
<span data-ttu-id="29110-330">Dopo avere eseguito l'accesso ad Azure AD in Service Fabric Explorer, il browser torna alla home page, ma un messaggio chiede di selezionare un certificato.</span><span class="sxs-lookup"><span data-stu-id="29110-330">After you sign in successfully to Azure AD in Service Fabric Explorer, the browser returns to the home page but a message prompts you to select a certificate.</span></span>

![Finestra di dialogo di selezione certificato in SFX][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="29110-332">Motivo</span><span class="sxs-lookup"><span data-stu-id="29110-332">Reason</span></span>
<span data-ttu-id="29110-333">All'utente non è assegnato un ruolo nell'applicazione cluster Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29110-333">The user isn’t assigned a role in the Azure AD cluster application.</span></span> <span data-ttu-id="29110-334">Di conseguenza, l'autenticazione di Azure AD non riesce nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29110-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="29110-335">Service Fabric Explorer ritorna all'autenticazione del certificato.</span><span class="sxs-lookup"><span data-stu-id="29110-335">Service Fabric Explorer falls back to certificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="29110-336">Soluzione</span><span class="sxs-lookup"><span data-stu-id="29110-336">Solution</span></span>
<span data-ttu-id="29110-337">Seguire le istruzioni per la configurazione di Azure AD e assegnare i ruoli utente.</span><span class="sxs-lookup"><span data-stu-id="29110-337">Follow the instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="29110-338">È anche consigliabile attivare "Assegnazione utente obbligatoria per l'accesso all'app", come in `SetupApplications.ps1`.</span><span class="sxs-lookup"><span data-stu-id="29110-338">Also, we recommend that you turn on “User assignment required to access app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-the-specified-credentials-are-invalid"></a><span data-ttu-id="29110-339">La connessione a PowerShell non riesce con un errore: "Le credenziali specificate non sono valide"</span><span class="sxs-lookup"><span data-stu-id="29110-339">Connection with PowerShell fails with an error: "The specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="29110-340">Problema</span><span class="sxs-lookup"><span data-stu-id="29110-340">Problem</span></span>
<span data-ttu-id="29110-341">Quando si usa PowerShell per connettersi al cluster con la modalità di sicurezza "AzureActiveDirectory", eseguito l'accesso ad Azure AD, la connessione ha esito negativo con un errore: "Le credenziali specificate non sono valide".</span><span class="sxs-lookup"><span data-stu-id="29110-341">When you use PowerShell to connect to the cluster by using “AzureActiveDirectory” security mode, after you sign in successfully to Azure AD, the connection fails with an error: "The specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="29110-342">Soluzione</span><span class="sxs-lookup"><span data-stu-id="29110-342">Solution</span></span>
<span data-ttu-id="29110-343">Questa soluzione è identica a quella precedente.</span><span class="sxs-lookup"><span data-stu-id="29110-343">This solution is the same as the preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="29110-344">Service Fabric Explorer restituisce un errore durante l'accesso: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="29110-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="29110-345">Problema</span><span class="sxs-lookup"><span data-stu-id="29110-345">Problem</span></span>
<span data-ttu-id="29110-346">Quando si prova a eseguire l'accesso ad Azure AD in Service Fabric Explorer, la pagina restituisce l'errore AADSTS50011, che indica che l'&lt;URL&gt; dell'indirizzo di risposta non corrisponde agli indirizzi configurati per l'applicazione: &lt;GUID&gt;.</span><span class="sxs-lookup"><span data-stu-id="29110-346">When you try to sign in to Azure AD in Service Fabric Explorer, the page returns a failure: "AADSTS50011: The reply address &lt;url&gt; does not match the reply addresses configured for the application: &lt;guid&gt;."</span></span>

![Indirizzo di risposta di SFX non corrispondente][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="29110-348">Motivo</span><span class="sxs-lookup"><span data-stu-id="29110-348">Reason</span></span>
<span data-ttu-id="29110-349">L'applicazione cluster (Web) che rappresenta Service Fabric Explorer prova a eseguire l'autenticazione per Azure AD e come parte della richiesta indica l'URL di reindirizzamento restituito.</span><span class="sxs-lookup"><span data-stu-id="29110-349">The cluster (web) application that represents Service Fabric Explorer attempts to authenticate against Azure AD, and as part of the request it provides the redirect return URL.</span></span> <span data-ttu-id="29110-350">L'URL non è presente nell'elenco degli **URL DI RISPOSTA** dell'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29110-350">But the URL is not listed in the Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="29110-351">Soluzione</span><span class="sxs-lookup"><span data-stu-id="29110-351">Solution</span></span>
<span data-ttu-id="29110-352">Nella scheda **Configura** dell'applicazione cluster (Web) aggiungere l'URL di Service Fabric Explorer all'elenco **URL DI RISPOSTA** o sostituire una delle voci dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="29110-352">On the **Configure** tab of the cluster (web) application, add the URL of Service Fabric Explorer to the **REPLY URL** list or replace one of the items in the list.</span></span> <span data-ttu-id="29110-353">Al termine, salvare la modifica.</span><span class="sxs-lookup"><span data-stu-id="29110-353">When you have finished, save your change.</span></span>

![URL di risposta dell'applicazione Web][web-application-reply-url]

### <a name="connect-the-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="29110-355">Connettere il cluster usando l'autenticazione di Azure AD tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="29110-355">Connect the cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="29110-356">Per connettere il cluster di Service Fabric, usare il comando di PowerShell di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="29110-356">To connect the Service Fabric cluster, use the following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="29110-357">Per informazioni sul cmdlet Connect-ServiceFabricCluster, vedere [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="29110-357">To learn about the Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-the-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="29110-358">È possibile usare di nuovo lo stesso tenant di Azure AD in più cluster?</span><span class="sxs-lookup"><span data-stu-id="29110-358">Can I reuse the same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="29110-359">Sì.</span><span class="sxs-lookup"><span data-stu-id="29110-359">Yes.</span></span> <span data-ttu-id="29110-360">Ricordarsi però di aggiungere l'URL di Service Fabric Explorer all'applicazione cluster (Web).</span><span class="sxs-lookup"><span data-stu-id="29110-360">But remember to add the URL of Service Fabric Explorer to your cluster (web) application.</span></span> <span data-ttu-id="29110-361">In caso contrario, Service Fabric Explorer non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="29110-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="29110-362">Perché è ancora necessario un certificato del server se Azure AD è abilitato?</span><span class="sxs-lookup"><span data-stu-id="29110-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="29110-363">FabricClient e FabricGateway eseguono un'autenticazione reciproca.</span><span class="sxs-lookup"><span data-stu-id="29110-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="29110-364">Durante l'autenticazione di Azure AD, l'integrazione di Azure AD consente di assegnare un'identità del client al server e il certificato del server viene usato per verificare l'identità del server.</span><span class="sxs-lookup"><span data-stu-id="29110-364">During Azure AD authentication, Azure AD integration provides a client identity to the server, and the server certificate is used to verify the server identity.</span></span> <span data-ttu-id="29110-365">Per altre informazioni sui certificati di Service Fabric, vedere [Certificati X.509 e Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="29110-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

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

