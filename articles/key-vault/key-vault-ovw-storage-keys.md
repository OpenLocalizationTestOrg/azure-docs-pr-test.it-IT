---
ms.assetid: 
title: aaaAzure chiave insieme di credenziali delle chiavi dell'Account di archiviazione
description: Chiavi dell'account di archiviazione forniscono un'integrazione diretto tra l'insieme di credenziali chiave di Azure e tooAzure chiave di accesso basato su Account di archiviazione.
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: becdf97798a08164c48d3a7a14aea6ca54085c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="916a2-103">Chiavi dell'account di archiviazione Key Vault</span><span class="sxs-lookup"><span data-stu-id="916a2-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="916a2-104">Prima delle chiavi di Account di archiviazione insieme di credenziali chiave di Azure, gli sviluppatori ha toomanage le rispettive chiavi di Account di archiviazione di Azure (ASA) e ruotando manualmente o mediante un'automazione esterna.</span><span class="sxs-lookup"><span data-stu-id="916a2-104">Before Azure Key Vault Storage Account Keys, developers had toomanage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="916a2-105">Al momento, le chiavi dell'account di archiviazione di Key Vault sono implementate come [segreti di Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) per l'autenticazione con un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="916a2-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="916a2-106">funzionalità chiave di Hello ASA gestisce rotazione segreta per l'utente e rimuove hello necessario per il contatto diretto con una chiave ASA offrendo accesso firme (condiviso) come metodo.</span><span class="sxs-lookup"><span data-stu-id="916a2-106">hello ASA key feature manages secret rotation for you and removes hello need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="916a2-107">Per informazioni più generali sugli account di archiviazione di Azure, vedere [Informazioni sugli account di archiviazione di Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="916a2-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="916a2-108">Interfacce di supporto</span><span class="sxs-lookup"><span data-stu-id="916a2-108">Supporting interfaces</span></span>

<span data-ttu-id="916a2-109">Hello funzionalità delle chiavi di Account di archiviazione di Azure è inizialmente disponibile tramite hello REST, .NET / c# e PowerShell di interfacce.</span><span class="sxs-lookup"><span data-stu-id="916a2-109">hello Azure Storage Account keys feature is initially available through hello REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="916a2-110">Per altre informazioni, vedere [Documentazione sull'insieme di credenziali delle chiavi](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="916a2-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="916a2-111">Ottenere il comportamento delle chiavi dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="916a2-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="916a2-112">Ciò che Key Vault gestisce</span><span class="sxs-lookup"><span data-stu-id="916a2-112">What Key Vault manages</span></span>

<span data-ttu-id="916a2-113">Key Vault esegue diverse funzioni di gestione interne per conto dell'utente quando si usano chiavi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="916a2-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="916a2-114">Azure Key Vault gestisce le chiavi di un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="916a2-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="916a2-115">Internamente Key Vault consente di elencare (sincronizzazione) le chiavi con un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="916a2-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="916a2-116">Rigenera insieme di credenziali chiave di Azure (Ruota) hello chiavi periodicamente.</span><span class="sxs-lookup"><span data-stu-id="916a2-116">Azure Key Vault regenerates (rotates) hello keys periodically.</span></span> 
    - <span data-ttu-id="916a2-117">I valori di chiave non vengono mai restituiti nella risposta toocaller.</span><span class="sxs-lookup"><span data-stu-id="916a2-117">Key values are never returned in response toocaller.</span></span> 
    - <span data-ttu-id="916a2-118">Key Vault gestisce le chiavi sia degli account di archiviazione che degli account di archiviazione classici.</span><span class="sxs-lookup"><span data-stu-id="916a2-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="916a2-119">Insieme di credenziali chiave di Azure consente, proprietario dell'insieme di credenziali/oggetto hello, definizioni di toocreate SAS (account o servizio di firma di accesso condiviso).</span><span class="sxs-lookup"><span data-stu-id="916a2-119">Azure Key Vault allows you, hello vault/object owner, toocreate SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="916a2-120">Hello valore SAS, creato usando la definizione di firma di accesso condiviso, viene restituito come una chiave privata tramite percorso URI REST hello.</span><span class="sxs-lookup"><span data-stu-id="916a2-120">hello SAS value, created using SAS definition, is returned as a secret via hello REST URI path.</span></span> <span data-ttu-id="916a2-121">Per altre informazioni, vedere [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations) (Operazioni dell'account di archiviazione di Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="916a2-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="916a2-122">Linee guida sulla denominazione</span><span class="sxs-lookup"><span data-stu-id="916a2-122">Naming guidance</span></span>

<span data-ttu-id="916a2-123">I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="916a2-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="916a2-124">Un nome di una definizione SAS deve avere da 1 a 102 caratteri e contenere solo i caratteri da 0 a 9, da a a z e da A a Z.</span><span class="sxs-lookup"><span data-stu-id="916a2-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="916a2-125">Esperienza per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="916a2-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="916a2-126">Prima delle chiavi di archiviazione Key Vault</span><span class="sxs-lookup"><span data-stu-id="916a2-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="916a2-127">Gli sviluppatori utilizzavano tooneed toodo hello ottimali con un archivio account tooget chiave accesso tooAzure di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="916a2-127">Developers used tooneed toodo hello following practices with a storage account key tooget access tooAzure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="916a2-128">Dopo le chiavi di archiviazione Key Vault</span><span class="sxs-lookup"><span data-stu-id="916a2-128">After Azure Key Vault Storage Keys</span></span> 

```
//Please make sure tooset storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command tooget Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using hello SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and hello Blob storage endpoint toocreate a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about tooexpire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="916a2-129">Procedure consigliate per lo sviluppatore</span><span class="sxs-lookup"><span data-stu-id="916a2-129">Developer best practices</span></span> 

- <span data-ttu-id="916a2-130">Consentire solo toomanage chiave dell'insieme di credenziali delle chiavi ASA.</span><span class="sxs-lookup"><span data-stu-id="916a2-130">Only allow Key Vault toomanage your ASA keys.</span></span> <span data-ttu-id="916a2-131">Non tentare toomanage li manualmente, interferisce con i processi dell'insieme di credenziali di chiave.</span><span class="sxs-lookup"><span data-stu-id="916a2-131">Do not attempt toomanage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="916a2-132">Non consentire ASA chiavi toobe gestito da più di un oggetto insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="916a2-132">Do not allow ASA keys toobe managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="916a2-133">Se è necessario toomanually rigenerare le chiavi ASA, è consigliabile rigenerarli tramite l'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="916a2-133">If you need toomanually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="916a2-134">introduttiva</span><span class="sxs-lookup"><span data-stu-id="916a2-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="916a2-135">Configurazione per le autorizzazioni di controllo degli accessi in base al ruolo (RBAC)</span><span class="sxs-lookup"><span data-stu-id="916a2-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="916a2-136">Insieme di credenziali chiave deve disporre delle autorizzazioni troppo*elenco* e *rigenerare* chiavi per un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="916a2-136">Key Vault needs permissions too*list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="916a2-137">Impostare queste autorizzazioni usando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="916a2-137">Set up these permissions using hello following steps:</span></span>

- <span data-ttu-id="916a2-138">Ottenere ObjectId di Key Vault:</span><span class="sxs-lookup"><span data-stu-id="916a2-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="916a2-139">Assegnare tooAzure ruolo operatore Key archiviazione chiave insieme di credenziali delle identità:</span><span class="sxs-lookup"><span data-stu-id="916a2-139">Assign Storage Key Operator role tooAzure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="916a2-140">Per un tipo di account classico, impostare il parametro role hello troppo*"Classico archiviazione chiave operatore servizio ruolo di Account"*.</span><span class="sxs-lookup"><span data-stu-id="916a2-140">For a classic account type, set hello role parameter too*"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="916a2-141">Onboarding dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="916a2-141">Storage account onboarding</span></span> 

<span data-ttu-id="916a2-142">Esempio: Come si aggiunge una risorsa di archiviazione un proprietario dell'oggetto insieme di credenziali chiave account oggetto tooyour insieme credenziali chiavi Azure tooonboard un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="916a2-142">Example: As a Key Vault object owner you add a storage account object tooyour Azure Key Vault tooonboard a storage account.</span></span>

<span data-ttu-id="916a2-143">Durante il caricamento, l'insieme di credenziali chiave deve tooverify che hello identità dell'account di onboarding hello dispone delle autorizzazioni troppo*elenco* e troppo*rigenerare* chiavi per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="916a2-143">During onboarding, Key Vault needs tooverify that hello identity of hello onboarding account has permissions too*list* and too*regenerate* storage keys.</span></span> <span data-ttu-id="916a2-144">Ordinare tooverify queste autorizzazioni, insieme di credenziali chiave Ottiene un OBO (On per conto di) token dal servizio di autenticazione hello, impostare tooAzure Gestione risorse di destinatari e lo rende un *elenco* chiave chiamata toohello servizio di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="916a2-144">In order tooverify these permissions, Key Vault gets an OBO (On Behalf Of) token from hello authentication service, audience set tooAzure Resource Manager, and makes a *list* key call toohello Azure Storage service.</span></span> <span data-ttu-id="916a2-145">Se hello *elenco* chiamata ha esito negativo, la creazione dell'oggetto ha esito negativo con codice di stato HTTP dell'insieme di credenziali chiave di hello *non consentito*.</span><span class="sxs-lookup"><span data-stu-id="916a2-145">If hello *list* call fails, hello Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="916a2-146">chiavi Hello elencate in questo modo vengono memorizzati nella cache con l'archiviazione di entità dell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="916a2-146">hello keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="916a2-147">Insieme di credenziali chiave è necessario verificare che disponga di identità hello *rigenerare* autorizzazioni prima di acquisire la proprietà di rigenerazione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="916a2-147">Key Vault must verify that hello identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="916a2-148">tooverify hello identità, tramite il token OBO, nonché hello prima identità di terze parti insieme di credenziali chiave con queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="916a2-148">tooverify that hello identity, via OBO token, as well as hello Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="916a2-149">Insieme di credenziali chiave vengono elencate le autorizzazioni RBAC nella risorsa di account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="916a2-149">Key Vault lists RBAC permissions on hello storage account resource.</span></span>
- <span data-ttu-id="916a2-150">Insieme di credenziali chiave di convalida risposta hello tramite espressioni regolari di ricerca di azioni e non quelle.</span><span class="sxs-lookup"><span data-stu-id="916a2-150">Key Vault validates hello response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="916a2-151">Trovare alcuni esempi di supporto in [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167) (Key Vault - Esempi di chiavi dell'account di archiviazione gestito).</span><span class="sxs-lookup"><span data-stu-id="916a2-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="916a2-152">Se non dispone di identità hello *rigenerare* autorizzazioni o se non dispone di identità di terze parti prima dell'insieme di credenziali di chiave *elenco* o *rigenerare* autorizzazioni, quindi hello onboarding richiesta ha esito negativo restituendo un messaggio e il codice di errore appropriato.</span><span class="sxs-lookup"><span data-stu-id="916a2-152">If hello identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then hello onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="916a2-153">token OBO Hello funziona solo quando si utilizza cookie, alle applicazioni client native di PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="916a2-153">hello OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="916a2-154">Altre applicazioni</span><span class="sxs-lookup"><span data-stu-id="916a2-154">Other applications</span></span>

- <span data-ttu-id="916a2-155">Token di firma di accesso condiviso, costruito utilizzando chiavi dell'account di archiviazione dell'insieme di credenziali chiave, forniscono tooan accesso controllato anche più account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="916a2-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access tooan Azure storage account.</span></span> <span data-ttu-id="916a2-156">Per altre informazioni, vedere [Uso delle firme di accesso condiviso](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="916a2-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="916a2-157">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="916a2-157">See also</span></span>

- [<span data-ttu-id="916a2-158">Informazioni su chiavi, segreti e certificati</span><span class="sxs-lookup"><span data-stu-id="916a2-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="916a2-159">Blog del team di Key Vault</span><span class="sxs-lookup"><span data-stu-id="916a2-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
