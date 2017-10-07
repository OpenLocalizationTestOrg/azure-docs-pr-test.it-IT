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
# <a name="azure-key-vault-storage-account-keys"></a>Chiavi dell'account di archiviazione Key Vault

Prima delle chiavi di Account di archiviazione insieme di credenziali chiave di Azure, gli sviluppatori ha toomanage le rispettive chiavi di Account di archiviazione di Azure (ASA) e ruotando manualmente o mediante un'automazione esterna. Al momento, le chiavi dell'account di archiviazione di Key Vault sono implementate come [segreti di Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) per l'autenticazione con un account di archiviazione di Azure. 

funzionalità chiave di Hello ASA gestisce rotazione segreta per l'utente e rimuove hello necessario per il contatto diretto con una chiave ASA offrendo accesso firme (condiviso) come metodo. 

Per informazioni più generali sugli account di archiviazione di Azure, vedere [Informazioni sugli account di archiviazione di Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

## <a name="supporting-interfaces"></a>Interfacce di supporto

Hello funzionalità delle chiavi di Account di archiviazione di Azure è inizialmente disponibile tramite hello REST, .NET / c# e PowerShell di interfacce. Per altre informazioni, vedere [Documentazione sull'insieme di credenziali delle chiavi](https://docs.microsoft.com/azure/key-vault/).


## <a name="storage-account-keys-behavior"></a>Ottenere il comportamento delle chiavi dell'account di archiviazione

### <a name="what-key-vault-manages"></a>Ciò che Key Vault gestisce

Key Vault esegue diverse funzioni di gestione interne per conto dell'utente quando si usano chiavi dell'account di archiviazione.

1. Azure Key Vault gestisce le chiavi di un account di archiviazione di Azure. 
    - Internamente Key Vault consente di elencare (sincronizzazione) le chiavi con un account di archiviazione di Azure.  
    - Rigenera insieme di credenziali chiave di Azure (Ruota) hello chiavi periodicamente. 
    - I valori di chiave non vengono mai restituiti nella risposta toocaller. 
    - Key Vault gestisce le chiavi sia degli account di archiviazione che degli account di archiviazione classici. 
2. Insieme di credenziali chiave di Azure consente, proprietario dell'insieme di credenziali/oggetto hello, definizioni di toocreate SAS (account o servizio di firma di accesso condiviso). 
    - Hello valore SAS, creato usando la definizione di firma di accesso condiviso, viene restituito come una chiave privata tramite percorso URI REST hello. Per altre informazioni, vedere [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations) (Operazioni dell'account di archiviazione di Azure Key Vault).

### <a name="naming-guidance"></a>Linee guida sulla denominazione

I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole.  
 
Un nome di una definizione SAS deve avere da 1 a 102 caratteri e contenere solo i caratteri da 0 a 9, da a a z e da A a Z.

## <a name="developer-experience"></a>Esperienza per sviluppatori 

### <a name="before-azure-key-vault-storage-keys"></a>Prima delle chiavi di archiviazione Key Vault 

Gli sviluppatori utilizzavano tooneed toodo hello ottimali con un archivio account tooget chiave accesso tooAzure di archiviazione. 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>Dopo le chiavi di archiviazione Key Vault 

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
 
 ### <a name="developer-best-practices"></a>Procedure consigliate per lo sviluppatore 

- Consentire solo toomanage chiave dell'insieme di credenziali delle chiavi ASA. Non tentare toomanage li manualmente, interferisce con i processi dell'insieme di credenziali di chiave. 
- Non consentire ASA chiavi toobe gestito da più di un oggetto insieme di credenziali chiave. 
- Se è necessario toomanually rigenerare le chiavi ASA, è consigliabile rigenerarli tramite l'insieme di credenziali chiave. 

## <a name="getting-started"></a>introduttiva

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>Configurazione per le autorizzazioni di controllo degli accessi in base al ruolo (RBAC)

Insieme di credenziali chiave deve disporre delle autorizzazioni troppo*elenco* e *rigenerare* chiavi per un account di archiviazione. Impostare queste autorizzazioni usando hello alla procedura seguente:

- Ottenere ObjectId di Key Vault: 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- Assegnare tooAzure ruolo operatore Key archiviazione chiave insieme di credenziali delle identità: 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > Per un tipo di account classico, impostare il parametro role hello troppo*"Classico archiviazione chiave operatore servizio ruolo di Account"*.

### <a name="storage-account-onboarding"></a>Onboarding dell'account di archiviazione 

Esempio: Come si aggiunge una risorsa di archiviazione un proprietario dell'oggetto insieme di credenziali chiave account oggetto tooyour insieme credenziali chiavi Azure tooonboard un account di archiviazione.

Durante il caricamento, l'insieme di credenziali chiave deve tooverify che hello identità dell'account di onboarding hello dispone delle autorizzazioni troppo*elenco* e troppo*rigenerare* chiavi per l'archiviazione. Ordinare tooverify queste autorizzazioni, insieme di credenziali chiave Ottiene un OBO (On per conto di) token dal servizio di autenticazione hello, impostare tooAzure Gestione risorse di destinatari e lo rende un *elenco* chiave chiamata toohello servizio di archiviazione Azure. Se hello *elenco* chiamata ha esito negativo, la creazione dell'oggetto ha esito negativo con codice di stato HTTP dell'insieme di credenziali chiave di hello *non consentito*. chiavi Hello elencate in questo modo vengono memorizzati nella cache con l'archiviazione di entità dell'insieme di credenziali chiave. 

Insieme di credenziali chiave è necessario verificare che disponga di identità hello *rigenerare* autorizzazioni prima di acquisire la proprietà di rigenerazione delle chiavi. tooverify hello identità, tramite il token OBO, nonché hello prima identità di terze parti insieme di credenziali chiave con queste autorizzazioni:

- Insieme di credenziali chiave vengono elencate le autorizzazioni RBAC nella risorsa di account di archiviazione hello.
- Insieme di credenziali chiave di convalida risposta hello tramite espressioni regolari di ricerca di azioni e non quelle. 

Trovare alcuni esempi di supporto in [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167) (Key Vault - Esempi di chiavi dell'account di archiviazione gestito).

Se non dispone di identità hello *rigenerare* autorizzazioni o se non dispone di identità di terze parti prima dell'insieme di credenziali di chiave *elenco* o *rigenerare* autorizzazioni, quindi hello onboarding richiesta ha esito negativo restituendo un messaggio e il codice di errore appropriato. 

token OBO Hello funziona solo quando si utilizza cookie, alle applicazioni client native di PowerShell o CLI.

## <a name="other-applications"></a>Altre applicazioni

- Token di firma di accesso condiviso, costruito utilizzando chiavi dell'account di archiviazione dell'insieme di credenziali chiave, forniscono tooan accesso controllato anche più account di archiviazione di Azure. Per altre informazioni, vedere [Uso delle firme di accesso condiviso](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

## <a name="see-also"></a>Vedere anche

- [Informazioni su chiavi, segreti e certificati](https://docs.microsoft.com/rest/api/keyvault/)
- [Blog del team di Key Vault](https://blogs.technet.microsoft.com/kv/)
