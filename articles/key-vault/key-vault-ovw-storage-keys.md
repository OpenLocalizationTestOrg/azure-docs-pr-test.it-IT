---
ms.assetid: 
title: Chiavi dell'account di archiviazione Key Vault
description: Le chiavi dell'account di archiviazione forniscono un'integrazione diretta tra Azure Key Vault e l'accesso basato sulla chiave dell'account di Archiviazione di Azure.
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: 3148088c88236c64e089fd25c98eb8ac7cdcbfea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="265d9-103">Chiavi dell'account di archiviazione Key Vault</span><span class="sxs-lookup"><span data-stu-id="265d9-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="265d9-104">Prima delle chiavi dell'account di archiviazione Key Vault gli sviluppatori dovevano gestire le proprie chiavi dell'account di archiviazione di Azure (ASA) e ruotarle manualmente o mediante automazione esterna.</span><span class="sxs-lookup"><span data-stu-id="265d9-104">Before Azure Key Vault Storage Account Keys, developers had to manage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="265d9-105">Al momento, le chiavi dell'account di archiviazione di Key Vault sono implementate come [segreti di Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) per l'autenticazione con un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="265d9-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="265d9-106">La funzionalità di chiave ASA gestisce la rotazione segreta per conto dell'utente e rimuove la necessità di un contatto diretto con una chiave SA, offrendo le firme di accesso condiviso (SAS) come metodo.</span><span class="sxs-lookup"><span data-stu-id="265d9-106">The ASA key feature manages secret rotation for you and removes the need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="265d9-107">Per informazioni più generali sugli account di archiviazione di Azure, vedere [Informazioni sugli account di archiviazione di Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="265d9-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="265d9-108">Interfacce di supporto</span><span class="sxs-lookup"><span data-stu-id="265d9-108">Supporting interfaces</span></span>

<span data-ttu-id="265d9-109">La funzionalità chiavi dell'account di archiviazione di Azure è inizialmente disponibile attraverso le interfacce REST, .NET/C# e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="265d9-109">The Azure Storage Account keys feature is initially available through the REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="265d9-110">Per altre informazioni, vedere [Documentazione sull'insieme di credenziali delle chiavi](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="265d9-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="265d9-111">Ottenere il comportamento delle chiavi dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="265d9-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="265d9-112">Ciò che Key Vault gestisce</span><span class="sxs-lookup"><span data-stu-id="265d9-112">What Key Vault manages</span></span>

<span data-ttu-id="265d9-113">Key Vault esegue diverse funzioni di gestione interne per conto dell'utente quando si usano chiavi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="265d9-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="265d9-114">Azure Key Vault gestisce le chiavi di un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="265d9-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="265d9-115">Internamente Key Vault consente di elencare (sincronizzazione) le chiavi con un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="265d9-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="265d9-116">Key Vault rigenera (ruota) le chiavi periodicamente.</span><span class="sxs-lookup"><span data-stu-id="265d9-116">Azure Key Vault regenerates (rotates) the keys periodically.</span></span> 
    - <span data-ttu-id="265d9-117">I valori di chiave non vengono mai restituiti in risposta al chiamante.</span><span class="sxs-lookup"><span data-stu-id="265d9-117">Key values are never returned in response to caller.</span></span> 
    - <span data-ttu-id="265d9-118">Key Vault gestisce le chiavi sia degli account di archiviazione che degli account di archiviazione classici.</span><span class="sxs-lookup"><span data-stu-id="265d9-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="265d9-119">Key Vault consente al proprietario dell'insieme di credenziali/oggetto di creare definizioni SAS (SAS di account o di servizio).</span><span class="sxs-lookup"><span data-stu-id="265d9-119">Azure Key Vault allows you, the vault/object owner, to create SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="265d9-120">Il valore SAS, creato utilizzando la definizione SAS, viene restituito come una chiave privata tramite il percorso dell'URI REST.</span><span class="sxs-lookup"><span data-stu-id="265d9-120">The SAS value, created using SAS definition, is returned as a secret via the REST URI path.</span></span> <span data-ttu-id="265d9-121">Per altre informazioni, vedere [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations) (Operazioni dell'account di archiviazione di Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="265d9-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="265d9-122">Linee guida sulla denominazione</span><span class="sxs-lookup"><span data-stu-id="265d9-122">Naming guidance</span></span>

<span data-ttu-id="265d9-123">I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="265d9-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="265d9-124">Un nome di una definizione SAS deve avere da 1 a 102 caratteri e contenere solo i caratteri da 0 a 9, da a a z e da A a Z.</span><span class="sxs-lookup"><span data-stu-id="265d9-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="265d9-125">Esperienza per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="265d9-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="265d9-126">Prima delle chiavi di archiviazione Key Vault</span><span class="sxs-lookup"><span data-stu-id="265d9-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="265d9-127">Gli sviluppatori in precedenza dovevano eseguire le seguenti procedure con una chiave di account di archiviazione per ottenere l'accesso all'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="265d9-127">Developers used to need to do the following practices with a storage account key to get access to Azure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and the storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="265d9-128">Dopo le chiavi di archiviazione Key Vault</span><span class="sxs-lookup"><span data-stu-id="265d9-128">After Azure Key Vault Storage Keys</span></span> 

```
//Please make sure to set storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command to get Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using the SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and the Blob storage endpoint to create a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about to expire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="265d9-129">Procedure consigliate per lo sviluppatore</span><span class="sxs-lookup"><span data-stu-id="265d9-129">Developer best practices</span></span> 

- <span data-ttu-id="265d9-130">Consentire solo a Key Vault di gestire le chiavi ASA.</span><span class="sxs-lookup"><span data-stu-id="265d9-130">Only allow Key Vault to manage your ASA keys.</span></span> <span data-ttu-id="265d9-131">Non tentare di gestirle manualmente onde evitare di interferire con i processi di Key Vault.</span><span class="sxs-lookup"><span data-stu-id="265d9-131">Do not attempt to manage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="265d9-132">Non consentire alle chiavi ASA di essere gestite da più di un oggetto di Key Vault.</span><span class="sxs-lookup"><span data-stu-id="265d9-132">Do not allow ASA keys to be managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="265d9-133">Se è necessario rigenerare manualmente le chiavi ASA, è consigliabile rigenerarle tramite Key Vault.</span><span class="sxs-lookup"><span data-stu-id="265d9-133">If you need to manually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="265d9-134">Introduzione</span><span class="sxs-lookup"><span data-stu-id="265d9-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="265d9-135">Configurazione per le autorizzazioni di controllo degli accessi in base al ruolo (RBAC)</span><span class="sxs-lookup"><span data-stu-id="265d9-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="265d9-136">Key Vault necessita di autorizzazioni per *elencare* e *rigenerare* le chiavi per un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="265d9-136">Key Vault needs permissions to *list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="265d9-137">Impostare queste autorizzazioni usando la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="265d9-137">Set up these permissions using the following steps:</span></span>

- <span data-ttu-id="265d9-138">Ottenere ObjectId di Key Vault:</span><span class="sxs-lookup"><span data-stu-id="265d9-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="265d9-139">Assegnare il ruolo "Operatore chiave di archiviazione" all'identità di Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="265d9-139">Assign Storage Key Operator role to Azure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="265d9-140">Per un tipo di account classico, impostare il parametro del ruolo su *"Ruolo del servizio dell'operatore della chiave dell'account di archiviazione classico"*.</span><span class="sxs-lookup"><span data-stu-id="265d9-140">For a classic account type, set the role parameter to *"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="265d9-141">Onboarding dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="265d9-141">Storage account onboarding</span></span> 

<span data-ttu-id="265d9-142">Esempio: il proprietario di un oggetto Key Vault aggiunge un oggetto account di archiviazione in Azure Key Vault per eseguire l'onboarding di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="265d9-142">Example: As a Key Vault object owner you add a storage account object to your Azure Key Vault to onboard a storage account.</span></span>

<span data-ttu-id="265d9-143">Durante il caricamento, Key Vault deve verificare che l'identità dell'account onboarding abbia le autorizzazioni per accedere agli *elenchi* e *rigenerare* le chiavi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="265d9-143">During onboarding, Key Vault needs to verify that the identity of the onboarding account has permissions to *list* and to *regenerate* storage keys.</span></span> <span data-ttu-id="265d9-144">Per verificare queste autorizzazioni, Key Vault ottiene un token OBO (per conto di) dal servizio di autenticazione, pubblico impostato su Gestione Risorse di Azure e crea una chiamata chiave dell'*elenco* al servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="265d9-144">In order to verify these permissions, Key Vault gets an OBO (On Behalf Of) token from the authentication service, audience set to Azure Resource Manager, and makes a *list* key call to the Azure Storage service.</span></span> <span data-ttu-id="265d9-145">Se la chiamata di *elenco* ha esito negativo, la creazione dell'oggetto Key Vault ha esito negativo con il codice di stato HTTP *Forbidden*.</span><span class="sxs-lookup"><span data-stu-id="265d9-145">If the *list* call fails, the Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="265d9-146">Le chiavi elencate in questo modo vengono memorizzate nella cache con l'archiviazione di entità key vault.</span><span class="sxs-lookup"><span data-stu-id="265d9-146">The keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="265d9-147">Key Vault deve verificare che l'identità disponga delle autorizzazioni *rigenera* prima di acquisire la proprietà della rigenerazione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="265d9-147">Key Vault must verify that the identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="265d9-148">Per verificare che l'identità, tramite il token OBO, nonché l'identità Key Vault propria possieda queste autorizzazioni:</span><span class="sxs-lookup"><span data-stu-id="265d9-148">To verify that the identity, via OBO token, as well as the Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="265d9-149">Key Vault elenca le autorizzazioni RBAC per la risorsa dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="265d9-149">Key Vault lists RBAC permissions on the storage account resource.</span></span>
- <span data-ttu-id="265d9-150">Key Vault convalida la risposta tramite la corrispondenza mediante espressioni regolari di azioni e non-azioni.</span><span class="sxs-lookup"><span data-stu-id="265d9-150">Key Vault validates the response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="265d9-151">Trovare alcuni esempi di supporto in [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167) (Key Vault - Esempi di chiavi dell'account di archiviazione gestito).</span><span class="sxs-lookup"><span data-stu-id="265d9-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="265d9-152">Se l'identità non dispone dell'autorizzazione *rigenera* o l'identità Key Vault propria non dispone dell'autorizzazione *elenca* o *rigenera*, la richiesta di onboarding ha esito negativo restituendo un messaggio e codice di errore appropriati.</span><span class="sxs-lookup"><span data-stu-id="265d9-152">If the identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then the onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="265d9-153">Il token OBO funziona solo quando si usano applicazioni client native e proprie di PowerShell o dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="265d9-153">The OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="265d9-154">Altre applicazioni</span><span class="sxs-lookup"><span data-stu-id="265d9-154">Other applications</span></span>

- <span data-ttu-id="265d9-155">I token SAS, costruiti usando le chiavi dell'account di archiviazione Key Vault, forniscono un accesso ancora più controllato a un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="265d9-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access to an Azure storage account.</span></span> <span data-ttu-id="265d9-156">Per altre informazioni, vedere [Uso delle firme di accesso condiviso](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="265d9-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="265d9-157">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="265d9-157">See also</span></span>

- [<span data-ttu-id="265d9-158">Informazioni su chiavi, segreti e certificati</span><span class="sxs-lookup"><span data-stu-id="265d9-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="265d9-159">Blog del team di Key Vault</span><span class="sxs-lookup"><span data-stu-id="265d9-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
