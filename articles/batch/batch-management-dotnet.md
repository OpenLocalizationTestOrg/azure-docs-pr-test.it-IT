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
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a>Gestire quote alla libreria client di gestione dei Batch hello e account di Batch per .NET

> [!div class="op_single_selector"]
> * [Portale di Azure](batch-account-create-portal.md)
> * [.NET per la gestione di Batch](batch-management-dotnet.md)
> 
> 

È possibile ridurre il sovraccarico manutenzione nelle applicazioni Azure Batch utilizzando hello [gestione .NET per Batch] [ api_mgmt_net] creazione dell'account Batch tooautomate libreria, l'eliminazione, la gestione delle chiavi e individuazione di quota.

* **Creare ed eliminare account Batch** in qualsiasi area. Se, come un fornitore di software indipendenti (ISV), ad esempio, si fornisce un servizio per i client in cui ogni viene assegnato un account Batch separato per la fatturazione, è possibile aggiungere account creazione ed eliminazione funzionalità tooyour portale per i clienti.
* **Recuperare e rigenerare chiavi di account** a livello di programmazione per qualsiasi account Batch. Questa operazione consente di conformarsi ai criteri di sicurezza che impongono rollover periodici o la scadenza delle chiavi dell'account. In presenza di numerosi account Batch in diverse aree di Azure, l'automazione del processo di rollover permette di aumentare l'efficienza della soluzione.
* **Controllare le quote di account** e richiedere supporto per trial-and-error hello determinare quali account Batch sono i limiti. Il controllo delle quote degli account prima di avviare processi, creare pool o aggiungere nodi di calcolo permette di stabilire attivamente dove e quando creare risorse di calcolo. È possibile determinare quali account richiedono un aumento della quota prima dell'allocazione di risorse aggiuntive in tali account.
* **Combinare le funzionalità di altri servizi Azure** per un'esperienza di gestione completa, tramite gestione .NET per Batch, [Azure Active Directory][aad_about], hello e [Azure Gestione risorse] [ resman_overview] riuniti in hello stessa applicazione. Tramite queste funzionalità e le rispettive API, è possibile fornire un'esperienza di autenticazione disposizione, hello toocreate possibilità ed eliminare gruppi di risorse e le funzionalità di hello descritte in precedenza per una soluzione di gestione end-to-end.

> [!NOTE]
> Durante questo articolo è incentrato sulla gestione di livello di codice hello dell'account Batch, le chiavi e le quote, è possibile eseguire molte di queste attività tramite hello [portale di Azure][azure_portal]. Per ulteriori informazioni, vedere [creare un account di Azure Batch tramite il portale di Azure hello](batch-account-create-portal.md) e [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md).
> 
> 

## <a name="create-and-delete-batch-accounts"></a>Creare ed eliminare account Batch
Come accennato, una delle funzionalità principali di hello di hello API di gestione dei Batch è toocreate e quindi eliminare gli account Batch in un'area di Azure. toodo in tal caso, utilizzare [BatchManagementClient.Account.CreateAsync] [ net_create] e [DeleteAsync][net_delete], o controparte sincrona.

Hello frammento di codice seguente viene creato un account, ottiene hello appena creata account dal servizio Batch hello e quindi eliminarlo. In questo frammento di codice e altri hello in questo articolo, `batchManagementClient` è un'istanza completamente inizializzata di [BatchManagementClient][net_mgmt_client].

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
> Applicazioni che utilizzano una libreria di gestione .NET per Batch hello e la relativa classe BatchManagementClient richiedono **amministratore del servizio** o **coadministrator** accesso toohello sottoscrizione che possiede hello Toobe account batch è stato gestito. Per ulteriori informazioni, vedere hello [Azure Active Directory](#azure-active-directory) sezione e hello [AccountManagement] [ acct_mgmt_sample] nell'esempio di codice.
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a>Recuperare e rigenerare chiavi di account
È possibile ottenere le chiavi primarie e secondarie da qualsiasi account Batch all'interno della sottoscrizione usando [ListKeysAsync][net_list_keys]. Le chiavi possono essere rigenerate con [RegenerateKeyAsync][net_regenerate_keys].

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
> È possibile creare un flusso di lavoro di connessione ottimizzato per le applicazioni di gestione. Innanzitutto, ottenere una chiave dell'account per l'account Batch hello desiderato toomanage con [ListKeysAsync][net_list_keys]. Quindi, usare questa chiave durante l'inizializzazione della libreria .NET di Batch hello [BatchSharedKeyCredentials] [ net_sharedkeycred] (classe), che viene utilizzato durante l'inizializzazione [BatchClient] [net_batch_client].
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a>Verificare le quote di sottoscrizioni di Azure e account Batch
Le sottoscrizioni di Azure e hello singoli servizi di Azure come Batch tutti hanno le quote predefinite che limitano il numero di hello di determinate entità all'interno di essi. Per le quote predefinite di hello per le sottoscrizioni di Azure, vedere [sottoscrizione di Azure e limiti dei servizi, quote e vincoli](../azure-subscription-service-limits.md). Per le quote predefinite hello di hello servizio Batch, vedere [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md). Utilizzando libreria gestione .NET per Batch hello, è possibile controllare queste quote nelle applicazioni. In questo modo le decisioni di allocazione toomake prima di aggiungere gli account o le risorse come pool di calcolo e nodi di calcolo.

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a>Verificare le quote dell'account Batch di una sottoscrizione di Azure
Prima di creare un account Batch in un'area, è possibile controllare toosee la sottoscrizione di Azure, se si è in grado di tooadd un account in tale area.

Nel frammento di codice hello seguente, utilizziamo innanzitutto [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget una raccolta di tutti gli account di Batch che si trovano all'interno di una sottoscrizione. Una volta è stato ottenuto questo insieme, è determinare il numero di account nell'area di destinazione hello. Successivamente si utilizza [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain hello quota account Batch e determinare il numero di account (se presente) è possibile creare in tale area.

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

Nel frammento riportato hello sopra, `creds` è un'istanza di [TokenCloudCredentials][azure_tokencreds]. toosee un esempio di creazione di questo oggetto, vedere hello [AccountManagement] [ acct_mgmt_sample] nell'esempio di codice su GitHub.

### <a name="check-a-batch-account-for-compute-resource-quotas"></a>Verificare le quote di risorse di calcolo in un account Batch
Prima di aumentare le risorse di calcolo nella soluzione Batch, è possibile controllare le risorse di hello tooensure desiderato tooallocate non superano le quote dell'account hello. Nel frammento di codice hello riportato di seguito, è stampare le informazioni sulla quota hello per hello account Batch denominato `mybatchaccount`. Nell'applicazione, è possibile utilizzare tali toodetermine informazioni se l'account hello gestibili hello risorse aggiuntive toobe creato.

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
> Anche se sono presenti quote predefinite per le sottoscrizioni di Azure e servizi, molti di questi limiti possono essere generati eseguendo una richiesta di hello [portale di Azure][azure_portal]. Ad esempio, vedere [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md) per istruzioni su come aumentare le quote di account Batch.
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a>Usare Azure AD con la gestione .NET per Batch

libreria gestione .NET per Batch Hello è un client di provider di risorse di Azure e viene utilizzata in combinazione con [Azure Resource Manager] [ resman_overview] toomanage account alle risorse a livello di codice. Azure AD è obbligatorio tooauthenticate richieste tramite qualsiasi client di provider di risorse di Azure, incluso libreria gestione .NET per Batch hello e [Azure Resource Manager][resman_overview]. Per informazioni sull'uso di Azure AD con libreria di gestione .NET per Batch hello, vedere [soluzioni di Batch di utilizzare Azure Active Directory tooauthenticate](batch-aad-auth.md). 

## <a name="sample-project-on-github"></a>Progetto di esempio su GitHub

toosee gestione .NET per Batch in azione, estrarre hello [AccountManagment] [ acct_mgmt_sample] progetto di esempio su GitHub. Hello AccountManagment l'applicazione di esempio illustra hello seguenti operazioni:

1. Acquisire un token di sicurezza da Azure AD con [ADAL][aad_adal]. Se l'utente di hello non è già connesso, viene richiesto di fornire le credenziali di Azure.
2. Con token di sicurezza hello ottenuto da Azure AD, creare un [SubscriptionClient] [ resman_subclient] tooquery Azure per un elenco di sottoscrizioni associate all'account hello. utente Hello è possibile selezionare una sottoscrizione dall'elenco hello se contiene più di una sottoscrizione.
3. Ottenere le credenziali associate alla sottoscrizione hello selezionato.
4. Creare un [ResourceManagementClient] [ resman_client] oggetto utilizzando le credenziali di hello.
5. Utilizzare un [ResourceManagementClient] [ resman_client] toocreate un gruppo di risorse dell'oggetto.
6. Utilizzare un [BatchManagementClient] [ net_mgmt_client] oggetto tooperform diverse operazioni di account di Batch:
   * Creare un account di Batch nel nuovo gruppo di risorse hello.
   * Ottenere hello appena creata account dal servizio Batch hello.
   * Chiavi dell'account hello stampa per il nuovo account di hello.
   * Rigenerare una nuova chiave primaria per l'account di hello.
   * Stampare le informazioni sulla quota hello per conto di hello.
   * Hello stampa le informazioni sulla quota per la sottoscrizione di hello.
   * Stampare tutti gli account in sottoscrizione hello.
   * Eliminare l'account appena creato.
7. Eliminare il gruppo di risorse hello.

Prima di eliminare l'account e delle risorse gruppo di Batch di hello appena creato, è possibile visualizzarli in hello [portale di Azure][azure_portal]:

applicazione di esempio hello toorun correttamente, è necessario prima registrarlo con il tenant di Azure AD in hello Azure portal e concedere le autorizzazioni toohello API di gestione risorse di Azure. Hello procedure fornite in [soluzioni di gestione dei Batch l'autenticazione con Active Directory](batch-aad-auth-management.md).


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
