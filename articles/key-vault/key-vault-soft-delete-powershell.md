---
ms.assetid: 
title: insieme di credenziali delle chiave di aaaAzure - come toouse soft-delete con PowerShell
description: "Esempi di casi d'uso della funzionalità di eliminazione temporanea con frammenti di codice di PowerShell"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 4968b700a14f764ea1be7de2bf3697664f255f95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a>Come insieme di credenziali chiave toouse soft-delete con PowerShell

La funzionalità di eliminazione temporanea di Azure Key Vault consente il recupero di insiemi di credenziali e di oggetti di insiemi di credenziali eliminati. In particolare, gli indirizzi di soft-eliminazione hello seguenti scenari:

- Supporto per l'eliminazione reversibile di un insieme di credenziali delle chiavi
- Supporto per l'eliminazione reversibile di oggetti di insiemi di credenziali delle chiavi: chiavi, segreti e certificati

## <a name="prerequisites"></a>Prerequisiti

- Azure PowerShell 4.0.0 o versione successiva, se non sono già questo programma di installazione, installare Azure PowerShell e associarlo a una sottoscrizione di Azure, vedere [come tooinstall e configurare Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview). 

>[!NOTE]
> È una versione obsoleta dei nostri la formattazione dell'output di PowerShell di insieme di credenziali chiave di file che **potrebbe** essere caricato in ambiente anziché la versione corretta di hello. Ci sono prevedono che una versione aggiornata di hello toocontain PowerShell necessari di correzione per la formattazione dell'output di hello e aggiorna questo argomento in quel momento. Hello corrente soluzione alternativa, è consigliabile che il problema di formattazione, è:
> - Hello utilizzare seguente query se si nota che non è visualizzato hello soft-eliminazione abilitata proprietà descritte in questo argomento: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.


Per informazioni sui comandi di PowerShell relativi a Key Vault, vedere [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0) (Documentazione su PowerShell per Azure Key Vault).

## <a name="required-permissions"></a>Autorizzazioni necessarie

Le operazioni di Key Vault vengono gestite separatamente tramite autorizzazioni del controllo degli accessi in base al ruolo, come indicato di seguito:

| Operazione | Descrizione | Autorizzazione utente |
|:--|:--|:--|
|Elenco|Elenca gli insiemi di credenziali delle chiavi eliminati.|Microsoft.KeyVault/deletedVaults/read|
|Recupera|Recupera un insieme di credenziali delle chiavi eliminato.|Microsoft.KeyVault/vaults/write|
|Ripulisci|Rimuove in modo permanente un insieme di credenziali delle chiavi eliminato e tutti i relativi contenuti.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

Per altre informazioni sulle autorizzazioni e il controllo degli accessi, vedere [Proteggere l'insieme di credenziali delle chiavi](key-vault-secure-your-key-vault.md).

## <a name="enabling-soft-delete"></a>Abilitazione della funzione di eliminazione temporanea

toorecover in grado di toobe un insieme di credenziali chiave eliminato o gli oggetti archiviati in una chiave dell'insieme di credenziali, è innanzitutto necessario abilitare soft-eliminazione per tale chiave dell'insieme di credenziali.

### <a name="existing-key-vault"></a>Insieme di credenziali delle chiavi esistente

Per un insieme di credenziali delle chiavi esistente denominato ContosoVault, è possibile abilitare l'eliminazione temporanea come indicato di seguito. 

>[!NOTE]
>Attualmente, è necessario toouse Azure Resource Manager hello scrittura di risorse manipolazione toodirectly *enableSoftDelete* toohello proprietà risorsa insieme di credenziali chiave.

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a>Insieme di credenziali delle chiavi nuovo

Soft-eliminazione per un nuovo insieme di credenziali chiave di attivazione viene eseguita al momento della creazione tramite l'aggiunta di contrassegno di abilitazione di soft-eliminazione hello tooyour creare comando.

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a>Verificare l'abilitazione della funzione di eliminazione temporanea

tooverify un insieme di credenziali chiave è abilitata, l'eliminazione di soft hello esecuzione *ottenere* comandi e cercare hello 'Soft eliminare Enabled?' è impostato su true o false.

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Eliminazione di un insieme di credenziali delle chiavi protetto dalla funzione di eliminazione temporanea

toodelete comando di Hello (o rimuovere) un insieme di credenziali chiave rimane hello stesso, ma le relative modifiche di comportamento a seconda se è stata attivata soft-eliminazione o non.

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
>Se si esegue il comando precedente di hello per un insieme di credenziali chiave che non dispone di soft-eliminazione abilitata, verrà eliminata definitivamente questo insieme di credenziali chiave che il suo contenuto senza opzioni per il ripristino.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Come la funzione di eliminazione temporanea protegge gli insiemi di credenziali delle chiavi

Con la funzione di eliminazione temporanea abilitata:

- Quando viene eliminato un insieme di credenziali chiave, viene rimosso dal relativo gruppo di risorse e inserito in uno spazio dei nomi riservato solo associati hello percorso in cui è stato creato. 
- Gli oggetti in una chiave eliminata insieme di credenziali, ad esempio le chiavi, i segreti e i certificati, non sono accessibili e rimangono pertanto mentre il contenitore insieme di credenziali chiave si trova in stato di hello eliminato. 
- nome DNS Hello per un insieme di credenziali chiave nello stato di eliminazione viene conservato in modo, non è possibile creare un nuovo insieme di credenziali chiave con lo stesso nome.  

È possibile visualizzare gli archivi chiave di stato eliminato, associati alla sottoscrizione, utilizzando hello comando seguente:

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedStateVault 

Name           : ContosoVault
Location             : westus
Id                   : /subscriptions/xxx/providers/Microsoft.KeyVault/locations/westus/deletedVaults/ContosoVault
Resource ID          : /subscriptions/xxx/resourceGroups/ContosoVault/providers/Microsoft.KeyVault/vaults/ContosoVault
Deletion Date        : 5/9/2017 12:14:14 AM
Scheduled Purge Date : 8/7/2017 12:14:14 AM
Tags                 :
```

Hello *ID risorsa* in hello output fa riferimento toohello ID di risorsa originale di questo insieme di credenziali. Poiché l'insieme di credenziali delle chiavi è ora in stato "eliminato", non è presente alcuna risorsa con questo ID. Hello *Id* campo può essere utilizzato tooidentify hello risorsa durante il recupero o l'eliminazione. Hello *programmata data ripulire* campo indica l'insieme di credenziali hello quando verranno eliminati definitivamente (eliminati) se per questo insieme di credenziali eliminati viene eseguita alcuna azione. hello toocalculate periodo, utilizzato conservazione predefinito di Hello *programmata data ripulire*, è 90 giorni.

## <a name="recovering-a-key-vault"></a>Recupero di un insieme di credenziali delle chiavi

toorecover un insieme di credenziali chiave, è necessario nome insieme di credenziali chiave di hello toospecify, gruppo di risorse e posizione. Si noti hello percorso e il gruppo di risorse hello dell'insieme di credenziali chiave hello eliminato in base alle esigenze per un processo di ripristino della chiave dell'insieme di credenziali.

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

Quando viene recuperato un insieme di credenziali chiave, il risultato di hello è una nuova risorsa all'ID risorsa originale. dell'archivio chiavi hello Se è stato rimosso il gruppo di risorse hello in insieme di credenziali chiave hello esistenti, è necessario creato un nuovo gruppo di risorse con lo stesso nome prima di poter recuperare l'insieme di credenziali chiave hello.

## <a name="key-vault-objects-and-soft-delete"></a>Oggetti di Key Vault ed eliminazione temporanea

Per eliminare in modo definitivo una chiave "ContosoFirstKey" in un insieme di credenziali delle chiavi denominato "ContosoVault" con la funzione di eliminazione temporanea abilitata, seguire l'esempio seguente.

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

Se in un insieme di credenziali delle chiavi è abilitata la funzione di eliminazione temporanea, una chiave eliminata continua a essere visualizzata come eliminata a meno che non venga elencata o recuperata in modo esplicito. Ad eccezione di elenco di una chiave eliminata, Ripristina o eliminazione, la maggior parte delle operazioni su una chiave in stato di hello eliminato non riuscirà. 

Ad esempio, chiavi toolist eliminato toorequest in un insieme di credenziali chiave usare hello comando seguente:

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a>Stato di transizione 

Quando si elimina una chiave in un insieme di credenziali chiave con soft-eliminazione abilitata, potrebbe richiedere alcuni secondi per hello toocomplete di transizione. Durante questo stato di transizione, potrebbe sembrare che tale chiave hello non è nello stato attivo hello o hello eliminato. Questo comando elencherà tutte le chiavi eliminate nell'insieme di credenziali delle chiavi denominato "ContosoVault".

```powershell
  Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
  Vault Name           : ContosoVault
  Name                 : ContosoFirstKey
  Id                   : https://ContosoVault.vault.azure.net:443/keys/ContosoFirstKey
  Deleted Date         : 2/14/2017 8:20:52 PM
  Scheduled Purge Date : 5/15/2017 8:20:52 PM
  Enabled              : True
  Expires              :
  Not Before           :
  Created              : 2/14/2017 8:16:07 PM
  Updated              : 2/14/2017 8:16:07 PM
  Tags                 :
```

### <a name="using-soft-delete-with-key-vault-objects"></a>Utilizzo della funzione di eliminazione temporanea con gli oggetti di un insieme di credenziali delle chiavi

Analogamente a insiemi di credenziali chiave, una chiave eliminata, privata o certificato rimarrà nello stato di eliminazione per i giorni too90 a meno che non si ripristinarlo o eliminarlo. 

#### <a name="keys"></a>Chiavi

una chiave eliminata toorecover:

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

toopermanently eliminare una chiave:

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
>Dopo essere stata eliminata in modo definitivo, una chiave non è più recuperabile.

Hello **ripristinare** e **ripulire** azioni hanno le proprie autorizzazioni associate in un criterio di accesso della chiave dell'insieme di credenziali. Per un tooexecute in grado di toobe dell'entità utente o un servizio un **ripristinare** o **ripulire** azione devono disporre hello autorizzazione corrispondente per l'oggetto (chiave o il segreto) nei criteri di accesso di hello insieme di credenziali chiave. Per impostazione predefinita, hello **ripulire** autorizzazione non viene aggiunto i criteri di accesso dell'archivio chiavi tooa quando hello 'tutte' scelta rapida che viene utilizzato toogrant tutti gli utenti di tooa di autorizzazioni. L'autorizzazione di **eliminazione definitiva** deve essere concessa esplicitamente. Ad esempio, hello successivo comando concede user@contoso.com tooperform autorizzazioni diverse operazioni sulle chiavi in *ContosoVault* inclusi **ripulire**.

#### <a name="set-a-key-vault-access-policy"></a>Configurare i criteri di accesso dell'insieme di credenziali delle chiavi

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> Se si ha un insieme di credenziali delle chiavi in cui è stata appena abilitata la funzione di eliminazione temporanea, è possibile che non si disponga delle autorizzazioni di **recupero** ed **eliminazione definitiva**.

#### <a name="secrets"></a>Segreti

Come per le chiavi, è possibile eseguire operazioni sui segreti presenti in un insieme di credenziali delle chiavi usando i relativi comandi. Segue, sono comandi hello per l'eliminazione, elencare, recupero ed eliminazione dei segreti.

- Eliminare un segreto denominato SQLPassword: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- Elencare tutti i segreti eliminati in un insieme di credenziali delle chiavi: 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- Ripristinare un master secret in stato di hello eliminato: 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- Eliminare in modo definitivo un segreto in stato "eliminato": 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
>Dopo essere stato eliminato in modo definitivo, un segreto non è più recuperabile.

## <a name="purging-and-key-vaults"></a>Eliminazione definitiva e insiemi di credenziali delle chiavi

### <a name="key-vault-objects"></a>Oggetti nell'insieme di credenziali delle chiavi

Dopo essere stato eliminato in modo definitivo, una chiave, un segreto o un certificato non è più recuperabile. Hello chiave dell'insieme di credenziali che conteneva hello eliminato oggetto tuttavia rimarrà invariata come tutti gli altri oggetti nell'insieme di credenziali chiave hello. 

### <a name="key-vaults-as-containers"></a>Insiemi di credenziali delle chiavi come contenitori
Quando viene eliminato un insieme di credenziali delle chiavi, vengono rimossi in modo permanente anche tutti i relativi contenuti, tra cui certificati, chiavi e segreti. toopurge un insieme di credenziali chiave usare hello `Remove-AzureRmKeyVault` comando con l'opzione hello `-InRemovedState` e specificando il percorso di hello dell'insieme di credenziali chiave hello eliminato con hello `-Location location` argomento. È possibile trovare il percorso di hello di un insieme di credenziali eliminate utilizzando il comando hello `Get-AzureRmKeyVault -InRemovedState`.

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
>Dopo essere stato eliminato in modo definitivo, un insieme di credenziali delle chiavi non è più recuperabile.

### <a name="purge-permissions-required"></a>Autorizzazioni di eliminazione definitiva necessarie
- toopurge un insieme di credenziali chiave eliminato, tale che l'insieme di credenziali hello e il relativo contenuto in modo permanente viene rimossi, hello utente deve RBAC autorizzazione tooperform un *Microsoft.KeyVault/locations/deletedVaults/purge/action* operazione. 
- chiave hello eliminato toolist, insieme di credenziali hello un utente deve RBAC autorizzazione tooperform *Microsoft.KeyVault/deletedVaults/read* autorizzazione. 
- Per impostazione predefinita, solo un amministratore della sottoscrizione ha queste autorizzazioni. 

### <a name="scheduled-purge"></a>Eliminazione temporanea programmata

Elenca gli oggetti eliminati insieme di credenziali chiave Mostra quando vengono toobe schedled eliminati dall'insieme di credenziali chiave. Hello *programmata data ripulire* campo indica quando un oggetto chiave dell'insieme di credenziali verrà eliminato definitivamente, se viene eseguita alcuna azione. Per impostazione predefinita, il periodo di memorizzazione hello per un oggetto eliminato insieme di credenziali delle chiavi è 90 giorni.

>[!NOTE]
>Un oggetto di un insieme di credenziali delle chiavi eliminato in modo permanente, attivato dal campo *Scheduled Purge Date* (Data eliminazione definitiva programmata), viene eliminato in modo definitivo e non è più recuperabile.

## <a name="other-resources"></a>Altre risorse:

- Per una panoramica della funzionalità di eliminazione temporanea di Key Vault, vedere [Panoramica della funzionalità di eliminazione temporanea di Azure Key Vault](key-vault-ovw-soft-delete.md).
- Per una panoramica generale dell'utilizzo di Azure Key Vault, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md).

