---
title: risorse dell'account Batch aaaManage alla libreria client hello per .NET - Azure | Documenti Microsoft
description: Creare, eliminare e modificare le risorse di account Azure Batch con libreria di gestione .NET per Batch hello.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 638d8129f3841ffcfb2e10f5d531a319bcbb7701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a><span data-ttu-id="152e4-103">Gestire quote alla libreria client di gestione dei Batch hello e account di Batch per .NET</span><span class="sxs-lookup"><span data-stu-id="152e4-103">Manage Batch accounts and quotas with hello Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="152e4-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="152e4-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="152e4-105">.NET per la gestione di Batch</span><span class="sxs-lookup"><span data-stu-id="152e4-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="152e4-106">È possibile ridurre il sovraccarico manutenzione nelle applicazioni Azure Batch utilizzando hello [gestione .NET per Batch] [ api_mgmt_net] creazione dell'account Batch tooautomate libreria, l'eliminazione, la gestione delle chiavi e individuazione di quota.</span><span class="sxs-lookup"><span data-stu-id="152e4-106">You can lower maintenance overhead in your Azure Batch applications by using hello [Batch Management .NET][api_mgmt_net] library tooautomate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="152e4-107">**Creare ed eliminare account Batch** in qualsiasi area.</span><span class="sxs-lookup"><span data-stu-id="152e4-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="152e4-108">Se, come un fornitore di software indipendenti (ISV), ad esempio, si fornisce un servizio per i client in cui ogni viene assegnato un account Batch separato per la fatturazione, è possibile aggiungere account creazione ed eliminazione funzionalità tooyour portale per i clienti.</span><span class="sxs-lookup"><span data-stu-id="152e4-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities tooyour customer portal.</span></span>
* <span data-ttu-id="152e4-109">**Recuperare e rigenerare chiavi di account** a livello di programmazione per qualsiasi account Batch.</span><span class="sxs-lookup"><span data-stu-id="152e4-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="152e4-110">Questa operazione consente di conformarsi ai criteri di sicurezza che impongono rollover periodici o la scadenza delle chiavi dell'account.</span><span class="sxs-lookup"><span data-stu-id="152e4-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="152e4-111">In presenza di numerosi account Batch in diverse aree di Azure, l'automazione del processo di rollover permette di aumentare l'efficienza della soluzione.</span><span class="sxs-lookup"><span data-stu-id="152e4-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="152e4-112">**Controllare le quote di account** e richiedere supporto per trial-and-error hello determinare quali account Batch sono i limiti.</span><span class="sxs-lookup"><span data-stu-id="152e4-112">**Check account quotas** and take hello trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="152e4-113">Il controllo delle quote degli account prima di avviare processi, creare pool o aggiungere nodi di calcolo permette di stabilire attivamente dove e quando creare risorse di calcolo.</span><span class="sxs-lookup"><span data-stu-id="152e4-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="152e4-114">È possibile determinare quali account richiedono un aumento della quota prima dell'allocazione di risorse aggiuntive in tali account.</span><span class="sxs-lookup"><span data-stu-id="152e4-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="152e4-115">**Combinare le funzionalità di altri servizi Azure** per un'esperienza di gestione completa, tramite gestione .NET per Batch, [Azure Active Directory][aad_about], hello e [Azure Gestione risorse] [ resman_overview] riuniti in hello stessa applicazione.</span><span class="sxs-lookup"><span data-stu-id="152e4-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and hello [Azure Resource Manager][resman_overview] together in hello same application.</span></span> <span data-ttu-id="152e4-116">Tramite queste funzionalità e le rispettive API, è possibile fornire un'esperienza di autenticazione disposizione, hello toocreate possibilità ed eliminare gruppi di risorse e le funzionalità di hello descritte in precedenza per una soluzione di gestione end-to-end.</span><span class="sxs-lookup"><span data-stu-id="152e4-116">By using these features and their APIs, you can provide a frictionless authentication experience, hello ability toocreate and delete resource groups, and hello capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="152e4-117">Durante questo articolo è incentrato sulla gestione di livello di codice hello dell'account Batch, le chiavi e le quote, è possibile eseguire molte di queste attività tramite hello [portale di Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="152e4-117">While this article focuses on hello programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="152e4-118">Per ulteriori informazioni, vedere [creare un account di Azure Batch tramite il portale di Azure hello](batch-account-create-portal.md) e [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="152e4-118">For more information, see [Create an Azure Batch account using hello Azure portal](batch-account-create-portal.md) and [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="152e4-119">Creare ed eliminare account Batch</span><span class="sxs-lookup"><span data-stu-id="152e4-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="152e4-120">Come accennato, una delle funzionalità principali di hello di hello API di gestione dei Batch è toocreate e quindi eliminare gli account Batch in un'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="152e4-120">As mentioned, one of hello primary features of hello Batch Management API is toocreate and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="152e4-121">toodo in tal caso, utilizzare [BatchManagementClient.Account.CreateAsync] [ net_create] e [DeleteAsync][net_delete], o controparte sincrona.</span><span class="sxs-lookup"><span data-stu-id="152e4-121">toodo so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="152e4-122">Hello frammento di codice seguente viene creato un account, ottiene hello appena creata account dal servizio Batch hello e quindi eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="152e4-122">hello following code snippet creates an account, obtains hello newly created account from hello Batch service, and then deletes it.</span></span> <span data-ttu-id="152e4-123">In questo frammento di codice e altri hello in questo articolo, `batchManagementClient` è un'istanza completamente inizializzata di [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="152e4-123">In this snippet and hello others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get hello new account from hello Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete hello account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="152e4-124">Applicazioni che utilizzano una libreria di gestione .NET per Batch hello e la relativa classe BatchManagementClient richiedono **amministratore del servizio** o **coadministrator** accesso toohello sottoscrizione che possiede hello Toobe account batch è stato gestito.</span><span class="sxs-lookup"><span data-stu-id="152e4-124">Applications that use hello Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access toohello subscription that owns hello Batch account toobe managed.</span></span> <span data-ttu-id="152e4-125">Per ulteriori informazioni, vedere hello [Azure Active Directory](#azure-active-directory) sezione e hello [AccountManagement] [ acct_mgmt_sample] nell'esempio di codice.</span><span class="sxs-lookup"><span data-stu-id="152e4-125">For more information, see hello [Azure Active Directory](#azure-active-directory) section and hello [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="152e4-126">Recuperare e rigenerare chiavi di account</span><span class="sxs-lookup"><span data-stu-id="152e4-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="152e4-127">È possibile ottenere le chiavi primarie e secondarie da qualsiasi account Batch all'interno della sottoscrizione usando [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="152e4-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="152e4-128">Le chiavi possono essere rigenerate con [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="152e4-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print hello primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate hello primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="152e4-129">È possibile creare un flusso di lavoro di connessione ottimizzato per le applicazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="152e4-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="152e4-130">Innanzitutto, ottenere una chiave dell'account per l'account Batch hello desiderato toomanage con [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="152e4-130">First, obtain an account key for hello Batch account you wish toomanage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="152e4-131">Quindi, usare questa chiave durante l'inizializzazione della libreria .NET di Batch hello [BatchSharedKeyCredentials] [ net_sharedkeycred] (classe), che viene utilizzato durante l'inizializzazione [BatchClient] [net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="152e4-131">Then, use this key when initializing hello Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="152e4-132">Verificare le quote di sottoscrizioni di Azure e account Batch</span><span class="sxs-lookup"><span data-stu-id="152e4-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="152e4-133">Le sottoscrizioni di Azure e hello singoli servizi di Azure come Batch tutti hanno le quote predefinite che limitano il numero di hello di determinate entità all'interno di essi.</span><span class="sxs-lookup"><span data-stu-id="152e4-133">Azure subscriptions and hello individual Azure services like Batch all have default quotas that limit hello number of certain entities within them.</span></span> <span data-ttu-id="152e4-134">Per le quote predefinite di hello per le sottoscrizioni di Azure, vedere [sottoscrizione di Azure e limiti dei servizi, quote e vincoli](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="152e4-134">For hello default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="152e4-135">Per le quote predefinite hello di hello servizio Batch, vedere [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="152e4-135">For hello default quotas of hello Batch service, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="152e4-136">Utilizzando libreria gestione .NET per Batch hello, è possibile controllare queste quote nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="152e4-136">By using hello Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="152e4-137">In questo modo le decisioni di allocazione toomake prima di aggiungere gli account o le risorse come pool di calcolo e nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="152e4-137">This enables you toomake allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="152e4-138">Verificare le quote dell'account Batch di una sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="152e4-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="152e4-139">Prima di creare un account Batch in un'area, è possibile controllare toosee la sottoscrizione di Azure, se si è in grado di tooadd un account in tale area.</span><span class="sxs-lookup"><span data-stu-id="152e4-139">Before creating a Batch account in a region, you can check your Azure subscription toosee whether you are able tooadd an account in that region.</span></span>

<span data-ttu-id="152e4-140">Nel frammento di codice hello seguente, utilizziamo innanzitutto [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget una raccolta di tutti gli account di Batch che si trovano all'interno di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="152e4-140">In hello code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] tooget a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="152e4-141">Una volta è stato ottenuto questo insieme, è determinare il numero di account nell'area di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-141">Once we've obtained this collection, we determine how many accounts are in hello target region.</span></span> <span data-ttu-id="152e4-142">Successivamente si utilizza [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain hello quota account Batch e determinare il numero di account (se presente) è possibile creare in tale area.</span><span class="sxs-lookup"><span data-stu-id="152e4-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] tooobtain hello Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within hello subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within hello target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get hello account quota for hello specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in hello target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in hello {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="152e4-143">Nel frammento riportato hello sopra, `creds` è un'istanza di [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="152e4-143">In hello snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="152e4-144">toosee un esempio di creazione di questo oggetto, vedere hello [AccountManagement] [ acct_mgmt_sample] nell'esempio di codice su GitHub.</span><span class="sxs-lookup"><span data-stu-id="152e4-144">toosee an example of creating this object, see hello [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="152e4-145">Verificare le quote di risorse di calcolo in un account Batch</span><span class="sxs-lookup"><span data-stu-id="152e4-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="152e4-146">Prima di aumentare le risorse di calcolo nella soluzione Batch, è possibile controllare le risorse di hello tooensure desiderato tooallocate non superano le quote dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-146">Before increasing compute resources in your Batch solution, you can check tooensure hello resources you want tooallocate won't exceed hello account's quotas.</span></span> <span data-ttu-id="152e4-147">Nel frammento di codice hello riportato di seguito, è stampare le informazioni sulla quota hello per hello account Batch denominato `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="152e4-147">In hello code snippet below, we print hello quota information for hello Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="152e4-148">Nell'applicazione, è possibile utilizzare tali toodetermine informazioni se l'account hello gestibili hello risorse aggiuntive toobe creato.</span><span class="sxs-lookup"><span data-stu-id="152e4-148">In your own application, you could use such information toodetermine whether hello account can handle hello additional resources toobe created.</span></span>

```csharp
// First obtain hello Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print hello compute resource quotas for hello account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="152e4-149">Anche se sono presenti quote predefinite per le sottoscrizioni di Azure e servizi, molti di questi limiti possono essere generati eseguendo una richiesta di hello [portale di Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="152e4-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="152e4-150">Ad esempio, vedere [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md) per istruzioni su come aumentare le quote di account Batch.</span><span class="sxs-lookup"><span data-stu-id="152e4-150">For example, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="152e4-151">Usare Azure AD con la gestione .NET per Batch</span><span class="sxs-lookup"><span data-stu-id="152e4-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="152e4-152">libreria gestione .NET per Batch Hello è un client di provider di risorse di Azure e viene utilizzata in combinazione con [Azure Resource Manager] [ resman_overview] toomanage account alle risorse a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="152e4-152">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage account resources programmatically.</span></span> <span data-ttu-id="152e4-153">Azure AD è obbligatorio tooauthenticate richieste tramite qualsiasi client di provider di risorse di Azure, incluso libreria gestione .NET per Batch hello e [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="152e4-153">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="152e4-154">Per informazioni sull'uso di Azure AD con libreria di gestione .NET per Batch hello, vedere [soluzioni di Batch di utilizzare Azure Active Directory tooauthenticate](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="152e4-154">For information about using Azure AD with hello Batch Management .NET library, see [Use Azure Active Directory tooauthenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="152e4-155">Progetto di esempio su GitHub</span><span class="sxs-lookup"><span data-stu-id="152e4-155">Sample project on GitHub</span></span>

<span data-ttu-id="152e4-156">toosee gestione .NET per Batch in azione, estrarre hello [AccountManagment] [ acct_mgmt_sample] progetto di esempio su GitHub.</span><span class="sxs-lookup"><span data-stu-id="152e4-156">toosee Batch Management .NET in action, check out hello [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="152e4-157">Hello AccountManagment l'applicazione di esempio illustra hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="152e4-157">hello AccountManagment sample application demonstrates hello following operations:</span></span>

1. <span data-ttu-id="152e4-158">Acquisire un token di sicurezza da Azure AD con [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="152e4-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="152e4-159">Se l'utente di hello non è già connesso, viene richiesto di fornire le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="152e4-159">If hello user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="152e4-160">Con token di sicurezza hello ottenuto da Azure AD, creare un [SubscriptionClient] [ resman_subclient] tooquery Azure per un elenco di sottoscrizioni associate all'account hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-160">With hello security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] tooquery Azure for a list of subscriptions associated with hello account.</span></span> <span data-ttu-id="152e4-161">utente Hello è possibile selezionare una sottoscrizione dall'elenco hello se contiene più di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="152e4-161">hello user can select a subscription from hello list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="152e4-162">Ottenere le credenziali associate alla sottoscrizione hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="152e4-162">Get credentials associated with hello selected subscription.</span></span>
4. <span data-ttu-id="152e4-163">Creare un [ResourceManagementClient] [ resman_client] oggetto utilizzando le credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-163">Create a [ResourceManagementClient][resman_client] object by using hello credentials.</span></span>
5. <span data-ttu-id="152e4-164">Utilizzare un [ResourceManagementClient] [ resman_client] toocreate un gruppo di risorse dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="152e4-164">Use a [ResourceManagementClient][resman_client] object toocreate a resource group.</span></span>
6. <span data-ttu-id="152e4-165">Utilizzare un [BatchManagementClient] [ net_mgmt_client] oggetto tooperform diverse operazioni di account di Batch:</span><span class="sxs-lookup"><span data-stu-id="152e4-165">Use a [BatchManagementClient][net_mgmt_client] object tooperform several Batch account operations:</span></span>
   * <span data-ttu-id="152e4-166">Creare un account di Batch nel nuovo gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-166">Create a Batch account in hello new resource group.</span></span>
   * <span data-ttu-id="152e4-167">Ottenere hello appena creata account dal servizio Batch hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-167">Get hello newly created account from hello Batch service.</span></span>
   * <span data-ttu-id="152e4-168">Chiavi dell'account hello stampa per il nuovo account di hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-168">Print hello account keys for hello new account.</span></span>
   * <span data-ttu-id="152e4-169">Rigenerare una nuova chiave primaria per l'account di hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-169">Regenerate a new primary key for hello account.</span></span>
   * <span data-ttu-id="152e4-170">Stampare le informazioni sulla quota hello per conto di hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-170">Print hello quota information for hello account.</span></span>
   * <span data-ttu-id="152e4-171">Hello stampa le informazioni sulla quota per la sottoscrizione di hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-171">Print hello quota information for hello subscription.</span></span>
   * <span data-ttu-id="152e4-172">Stampare tutti gli account in sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-172">Print all accounts within hello subscription.</span></span>
   * <span data-ttu-id="152e4-173">Eliminare l'account appena creato.</span><span class="sxs-lookup"><span data-stu-id="152e4-173">Delete newly created account.</span></span>
7. <span data-ttu-id="152e4-174">Eliminare il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="152e4-174">Delete hello resource group.</span></span>

<span data-ttu-id="152e4-175">Prima di eliminare l'account e delle risorse gruppo di Batch di hello appena creato, è possibile visualizzarli in hello [portale di Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="152e4-175">Before deleting hello newly created Batch account and resource group, you can view them in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="152e4-176">applicazione di esempio hello toorun correttamente, è necessario prima registrarlo con il tenant di Azure AD in hello Azure portal e concedere le autorizzazioni toohello API di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="152e4-176">toorun hello sample application successfully, you must first register it with your Azure AD tenant in hello Azure portal and grant permissions toohello Azure Resource Manager API.</span></span> <span data-ttu-id="152e4-177">Hello procedure fornite in [soluzioni di gestione dei Batch l'autenticazione con Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="152e4-177">Follow hello steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


[aad_about]: ../active-directory/active-directory-whatis.md "Informazioni su Azure Active Directory"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenari di autenticazione per Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrazione di applicazioni con Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
