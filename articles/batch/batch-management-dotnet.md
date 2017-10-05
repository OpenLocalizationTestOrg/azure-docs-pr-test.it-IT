---
title: 'Gestire risorse di account Batch con la libreria client per .NET: Azure | Microsoft Docs'
description: Creare, eliminare e modificare le risorse dell'account Batch tramite la libreria Batch Management .NET.
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
ms.openlocfilehash: eafde9258222a2ab09ade2e366f9cc595a303dec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-batch-accounts-and-quotas-with-the-batch-management-client-library-for-net"></a><span data-ttu-id="11685-103">Gestire le quote e gli account Batch con la libreria client di gestione Batch per .NET</span><span class="sxs-lookup"><span data-stu-id="11685-103">Manage Batch accounts and quotas with the Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="11685-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="11685-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="11685-105">.NET per la gestione di Batch</span><span class="sxs-lookup"><span data-stu-id="11685-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="11685-106">È possibile ridurre il sovraccarico di manutenzione nelle applicazioni Azure Batch usando la libreria [Batch Management .NET][api_mgmt_net] per automatizzare le operazioni di creazione ed eliminazione di account Batch, gestione delle chiavi e individuazione delle quote.</span><span class="sxs-lookup"><span data-stu-id="11685-106">You can lower maintenance overhead in your Azure Batch applications by using the [Batch Management .NET][api_mgmt_net] library to automate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="11685-107">**Creare ed eliminare account Batch** in qualsiasi area.</span><span class="sxs-lookup"><span data-stu-id="11685-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="11685-108">Se, ad esempio, un fornitore di software indipendente (ISV) offre un servizio per cui a ogni cliente viene assegnato un account Batch separato per la fatturazione, è possibile aggiungere funzionalità di creazione ed eliminazione di account al portale per i clienti.</span><span class="sxs-lookup"><span data-stu-id="11685-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities to your customer portal.</span></span>
* <span data-ttu-id="11685-109">**Recuperare e rigenerare chiavi di account** a livello di programmazione per qualsiasi account Batch.</span><span class="sxs-lookup"><span data-stu-id="11685-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="11685-110">Questa operazione consente di conformarsi ai criteri di sicurezza che impongono rollover periodici o la scadenza delle chiavi dell'account.</span><span class="sxs-lookup"><span data-stu-id="11685-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="11685-111">In presenza di numerosi account Batch in diverse aree di Azure, l'automazione del processo di rollover permette di aumentare l'efficienza della soluzione.</span><span class="sxs-lookup"><span data-stu-id="11685-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="11685-112">**Controllare le quote degli account** e determinare senza errori i limiti dei singoli account Batch.</span><span class="sxs-lookup"><span data-stu-id="11685-112">**Check account quotas** and take the trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="11685-113">Il controllo delle quote degli account prima di avviare processi, creare pool o aggiungere nodi di calcolo permette di stabilire attivamente dove e quando creare risorse di calcolo.</span><span class="sxs-lookup"><span data-stu-id="11685-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="11685-114">È possibile determinare quali account richiedono un aumento della quota prima dell'allocazione di risorse aggiuntive in tali account.</span><span class="sxs-lookup"><span data-stu-id="11685-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="11685-115">**Integrare funzionalità di altri servizi di Azure** per un'esperienza di gestione completa sfruttando i vantaggi di Batch Management .NET, [Azure Active Directory][aad_about] e [Azure Resource Manager][resman_overview] nella stessa applicazione.</span><span class="sxs-lookup"><span data-stu-id="11685-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and the [Azure Resource Manager][resman_overview] together in the same application.</span></span> <span data-ttu-id="11685-116">Usando queste funzionalità e le relative API è possibile eliminare i problemi di autenticazione, consentire la creazione e l'eliminazione di gruppi di risorse e fornire le funzionalità descritte in precedenza per una soluzione di gestione end-to-end.</span><span class="sxs-lookup"><span data-stu-id="11685-116">By using these features and their APIs, you can provide a frictionless authentication experience, the ability to create and delete resource groups, and the capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="11685-117">Questo articolo è incentrato sulla gestione di quote, chiavi e account Batch a livello di codice, ma è possibile eseguire molte di queste attività usando il [portale di Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="11685-117">While this article focuses on the programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using the [Azure portal][azure_portal].</span></span> <span data-ttu-id="11685-118">Per altre informazioni, vedere [Creare un account Azure Batch usando il portale di Azure](batch-account-create-portal.md) e [Quote e limiti per il servizio Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="11685-118">For more information, see [Create an Azure Batch account using the Azure portal](batch-account-create-portal.md) and [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="11685-119">Creare ed eliminare account Batch</span><span class="sxs-lookup"><span data-stu-id="11685-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="11685-120">Come accennato, una delle principali funzionalità dell'API di gestione per Batch è la creazione ed eliminazione di account Batch in un'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="11685-120">As mentioned, one of the primary features of the Batch Management API is to create and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="11685-121">A questo scopo, usare [BatchManagementClient.Account.CreateAsync][net_create] e [DeleteAsync][net_delete] o le relative controparti sincrone.</span><span class="sxs-lookup"><span data-stu-id="11685-121">To do so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="11685-122">Il frammento di codice seguente crea un account, ottiene l'account appena creato dal servizio Batch e quindi lo elimina.</span><span class="sxs-lookup"><span data-stu-id="11685-122">The following code snippet creates an account, obtains the newly created account from the Batch service, and then deletes it.</span></span> <span data-ttu-id="11685-123">In questo e in altri frammenti di codice in questo articolo `batchManagementClient` è un'istanza completamente inizializzata di [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="11685-123">In this snippet and the others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get the new account from the Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete the account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="11685-124">Le applicazioni che usano la libreria Batch Management .NET e la relativa classe BatchManagementClient necessitano di accesso come **amministratore del servizio** o **coamministratore** alla sottoscrizione a cui appartiene l'account Batch da gestire.</span><span class="sxs-lookup"><span data-stu-id="11685-124">Applications that use the Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access to the subscription that owns the Batch account to be managed.</span></span> <span data-ttu-id="11685-125">Per altre informazioni, vedere la sezione [Azure Active Directory](#azure-active-directory) e l'esempio di codice [AccountManagement][acct_mgmt_sample].</span><span class="sxs-lookup"><span data-stu-id="11685-125">For more information, see the [Azure Active Directory](#azure-active-directory) section and the [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="11685-126">Recuperare e rigenerare chiavi di account</span><span class="sxs-lookup"><span data-stu-id="11685-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="11685-127">È possibile ottenere le chiavi primarie e secondarie da qualsiasi account Batch all'interno della sottoscrizione usando [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="11685-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="11685-128">Le chiavi possono essere rigenerate con [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="11685-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print the primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate the primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="11685-129">È possibile creare un flusso di lavoro di connessione ottimizzato per le applicazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="11685-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="11685-130">Ottenere prima una chiave per l'account Batch che si vuole gestire con [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="11685-130">First, obtain an account key for the Batch account you wish to manage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="11685-131">Usare poi questa chiave durante l'inizializzazione della classe [BatchSharedKeyCredentials][net_sharedkeycred] della libreria Batch .NET usata durante l'inizializzazione di [BatchClient][net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="11685-131">Then, use this key when initializing the Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="11685-132">Verificare le quote di sottoscrizioni di Azure e account Batch</span><span class="sxs-lookup"><span data-stu-id="11685-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="11685-133">Le sottoscrizioni di Azure e i singoli servizi di Azure come Batch hanno tutti quote predefinite che limitano il numero di determinate entità al loro interno.</span><span class="sxs-lookup"><span data-stu-id="11685-133">Azure subscriptions and the individual Azure services like Batch all have default quotas that limit the number of certain entities within them.</span></span> <span data-ttu-id="11685-134">Per informazioni sulle quote predefinite per le sottoscrizioni di Azure, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="11685-134">For the default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="11685-135">Per le quote predefinite del servizio Batch, vedere [Quote e limiti per il servizio Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="11685-135">For the default quotas of the Batch service, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="11685-136">Tramite la libreria Batch Management .NET è possibile controllare queste quote nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="11685-136">By using the Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="11685-137">In questo modo è possibile prendere decisioni relative all'allocazione prima di aggiungere account o risorse di calcolo come pool e nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="11685-137">This enables you to make allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="11685-138">Verificare le quote dell'account Batch di una sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="11685-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="11685-139">Prima di creare un account Batch in un'area, è possibile verificare se la sottoscrizione di Azure permette di aggiungere un account in quell'area.</span><span class="sxs-lookup"><span data-stu-id="11685-139">Before creating a Batch account in a region, you can check your Azure subscription to see whether you are able to add an account in that region.</span></span>

<span data-ttu-id="11685-140">Nel frammento di codice riportato di seguito viene usato prima di tutto [BatchManagementClient.Accounts.ListAsync][net_mgmt_listaccounts] per ottenere una raccolta di tutti gli account Batch all'interno di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="11685-140">In the code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] to get a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="11685-141">Una volta ottenuta questa raccolta, è possibile determinare il numero di account nell'area di destinazione.</span><span class="sxs-lookup"><span data-stu-id="11685-141">Once we've obtained this collection, we determine how many accounts are in the target region.</span></span> <span data-ttu-id="11685-142">Si userà quindi [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] per ottenere la quota dell'account Batch e determinare se e quanti account è possibile creare in quell'area.</span><span class="sxs-lookup"><span data-stu-id="11685-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] to obtain the Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within the subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within the target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get the account quota for the specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in the target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in the {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="11685-143">Nel frammento riportato sopra `creds` è un'istanza di [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="11685-143">In the snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="11685-144">Per un esempio relativo alla creazione di questo oggetto, vedere l'esempio di codice [AccountManagement][acct_mgmt_sample] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="11685-144">To see an example of creating this object, see the [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="11685-145">Verificare le quote di risorse di calcolo in un account Batch</span><span class="sxs-lookup"><span data-stu-id="11685-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="11685-146">Prima di aumentare le risorse di calcolo nella soluzione Batch, è possibile verificare che le risorse da allocare non superino le quote dell'account.</span><span class="sxs-lookup"><span data-stu-id="11685-146">Before increasing compute resources in your Batch solution, you can check to ensure the resources you want to allocate won't exceed the account's quotas.</span></span> <span data-ttu-id="11685-147">Nel frammento di codice riportato di seguito si procede alla stampa delle informazioni sulle quote per l'account Batch denominato `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="11685-147">In the code snippet below, we print the quota information for the Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="11685-148">Nell'applicazione è possibile usare queste informazioni per stabilire se l'account può gestire le risorse aggiuntive da creare.</span><span class="sxs-lookup"><span data-stu-id="11685-148">In your own application, you could use such information to determine whether the account can handle the additional resources to be created.</span></span>

```csharp
// First obtain the Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print the compute resource quotas for the account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="11685-149">Molti dei limiti delle quote predefinite per i servizi e le sottoscrizioni di Azure possono essere aumentati inviando una richiesta nel [portale di Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="11685-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in the [Azure portal][azure_portal].</span></span> <span data-ttu-id="11685-150">Per istruzioni su come aumentare le quote dell'account Batch, vedere ad esempio [Quote e limiti per il servizio Azure Batch](batch-quota-limit.md) .</span><span class="sxs-lookup"><span data-stu-id="11685-150">For example, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="11685-151">Usare Azure AD con la gestione .NET per Batch</span><span class="sxs-lookup"><span data-stu-id="11685-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="11685-152">La libreria della gestione .NET per Batch è un client del provider di risorse di Azure e viene usata in combinazione con [Azure Resource Manager][resman_overview] per gestire le risorse dell'account a livello di programmazione.</span><span class="sxs-lookup"><span data-stu-id="11685-152">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage account resources programmatically.</span></span> <span data-ttu-id="11685-153">Azure AD deve autenticare le richieste effettuate tramite un client del provider di risorse di Azure, inclusa la libreria della gestione .NET per Batch e con [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="11685-153">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="11685-154">Per informazioni sull'uso di Azure AD con la libreria della gestione .NET per Batch, vedere [Usare Azure Active Directory per autenticare le soluzioni Batch](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="11685-154">For information about using Azure AD with the Batch Management .NET library, see [Use Azure Active Directory to authenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="11685-155">Progetto di esempio su GitHub</span><span class="sxs-lookup"><span data-stu-id="11685-155">Sample project on GitHub</span></span>

<span data-ttu-id="11685-156">Il progetto di esempio [AccountManagment][acct_mgmt_sample] su GitHub permette di vedere Batch Management .NET in azione.</span><span class="sxs-lookup"><span data-stu-id="11685-156">To see Batch Management .NET in action, check out the [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="11685-157">L'applicazione di esempio AccountManagment illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="11685-157">The AccountManagment sample application demonstrates the following operations:</span></span>

1. <span data-ttu-id="11685-158">Acquisire un token di sicurezza da Azure AD con [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="11685-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="11685-159">Se l'utente non ha già eseguito l'accesso, gli viene richiesto di fornire le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="11685-159">If the user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="11685-160">Usando il token di sicurezza ottenuto da Azure AD, creare un oggetto [SubscriptionClient][resman_subclient] per richiedere ad Azure un elenco di sottoscrizioni associate all'account.</span><span class="sxs-lookup"><span data-stu-id="11685-160">With the security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] to query Azure for a list of subscriptions associated with the account.</span></span> <span data-ttu-id="11685-161">L'utente può selezionare una sottoscrizione dall'elenco se contiene più di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="11685-161">The user can select a subscription from the list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="11685-162">Ottenere le credenziali associate alla sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="11685-162">Get credentials associated with the selected subscription.</span></span>
4. <span data-ttu-id="11685-163">Creare un oggetto [ResourceManagementClient][resman_client] usando le credenziali.</span><span class="sxs-lookup"><span data-stu-id="11685-163">Create a [ResourceManagementClient][resman_client] object by using the credentials.</span></span>
5. <span data-ttu-id="11685-164">Usare l'oggetto [ResourceManagementClient][resman_client] per creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="11685-164">Use a [ResourceManagementClient][resman_client] object to create a resource group.</span></span>
6. <span data-ttu-id="11685-165">Usare l'oggetto [BatchManagementClient][net_mgmt_client] per eseguire una serie di operazioni sull'account Batch:</span><span class="sxs-lookup"><span data-stu-id="11685-165">Use a [BatchManagementClient][net_mgmt_client] object to perform several Batch account operations:</span></span>
   * <span data-ttu-id="11685-166">Creare un account Batch nel nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="11685-166">Create a Batch account in the new resource group.</span></span>
   * <span data-ttu-id="11685-167">Ottenere l'account appena creato dal servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="11685-167">Get the newly created account from the Batch service.</span></span>
   * <span data-ttu-id="11685-168">Stampare le chiavi dell'account per il nuovo account.</span><span class="sxs-lookup"><span data-stu-id="11685-168">Print the account keys for the new account.</span></span>
   * <span data-ttu-id="11685-169">Rigenerare una nuova chiave primaria per l'account.</span><span class="sxs-lookup"><span data-stu-id="11685-169">Regenerate a new primary key for the account.</span></span>
   * <span data-ttu-id="11685-170">Stampare le informazioni sulla quota per l'account.</span><span class="sxs-lookup"><span data-stu-id="11685-170">Print the quota information for the account.</span></span>
   * <span data-ttu-id="11685-171">Stampare le informazioni sulla quota per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="11685-171">Print the quota information for the subscription.</span></span>
   * <span data-ttu-id="11685-172">Stampare tutti gli account all'interno della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="11685-172">Print all accounts within the subscription.</span></span>
   * <span data-ttu-id="11685-173">Eliminare l'account appena creato.</span><span class="sxs-lookup"><span data-stu-id="11685-173">Delete newly created account.</span></span>
7. <span data-ttu-id="11685-174">Eliminare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="11685-174">Delete the resource group.</span></span>

<span data-ttu-id="11685-175">Prima di eliminare l'account Batch e il gruppo di risorse appena creati, è possibile esaminarli entrambi nel [portale di Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="11685-175">Before deleting the newly created Batch account and resource group, you can view them in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="11685-176">Per eseguire correttamente l'applicazione di esempio, è innanzitutto necessario registrarla con il tenant di Azure AD nel portale di Azure e concedere le autorizzazioni all'API di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="11685-176">To run the sample application successfully, you must first register it with your Azure AD tenant in the Azure portal and grant permissions to the Azure Resource Manager API.</span></span> <span data-ttu-id="11685-177">Seguire la procedura indicata in [Autenticare le soluzioni di gestione Batch con Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="11685-177">Follow the steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


<span data-ttu-id="11685-178">[aad_about]: ../active-directory/active-directory-whatis.md "Informazioni su Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="11685-178">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="11685-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenari di autenticazione per Azure AD"</span><span class="sxs-lookup"><span data-stu-id="11685-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="11685-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrazione di applicazioni con Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="11685-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
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
