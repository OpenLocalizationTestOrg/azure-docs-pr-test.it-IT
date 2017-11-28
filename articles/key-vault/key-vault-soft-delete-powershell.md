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
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="1af60-103">Come insieme di credenziali chiave toouse soft-delete con PowerShell</span><span class="sxs-lookup"><span data-stu-id="1af60-103">How toouse Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="1af60-104">La funzionalità di eliminazione temporanea di Azure Key Vault consente il recupero di insiemi di credenziali e di oggetti di insiemi di credenziali eliminati.</span><span class="sxs-lookup"><span data-stu-id="1af60-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="1af60-105">In particolare, gli indirizzi di soft-eliminazione hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="1af60-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="1af60-106">Supporto per l'eliminazione reversibile di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="1af60-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="1af60-107">Supporto per l'eliminazione reversibile di oggetti di insiemi di credenziali delle chiavi: chiavi, segreti e certificati</span><span class="sxs-lookup"><span data-stu-id="1af60-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1af60-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1af60-108">Prerequisites</span></span>

- <span data-ttu-id="1af60-109">Azure PowerShell 4.0.0 o versione successiva, se non sono già questo programma di installazione, installare Azure PowerShell e associarlo a una sottoscrizione di Azure, vedere [come tooinstall e configurare Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1af60-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="1af60-110">È una versione obsoleta dei nostri la formattazione dell'output di PowerShell di insieme di credenziali chiave di file che **potrebbe** essere caricato in ambiente anziché la versione corretta di hello.</span><span class="sxs-lookup"><span data-stu-id="1af60-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of hello correct version.</span></span> <span data-ttu-id="1af60-111">Ci sono prevedono che una versione aggiornata di hello toocontain PowerShell necessari di correzione per la formattazione dell'output di hello e aggiorna questo argomento in quel momento.</span><span class="sxs-lookup"><span data-stu-id="1af60-111">We are anticipating an updated version of PowerShell toocontain hello needed correction for hello output formatting and will update this topic at that time.</span></span> <span data-ttu-id="1af60-112">Hello corrente soluzione alternativa, è consigliabile che il problema di formattazione, è:</span><span class="sxs-lookup"><span data-stu-id="1af60-112">hello current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="1af60-113">Hello utilizzare seguente query se si nota che non è visualizzato hello soft-eliminazione abilitata proprietà descritte in questo argomento: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="1af60-113">Use hello following query if you notice you're not seeing hello soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="1af60-114">Per informazioni sui comandi di PowerShell relativi a Key Vault, vedere [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0) (Documentazione su PowerShell per Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="1af60-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="1af60-115">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="1af60-115">Required permissions</span></span>

<span data-ttu-id="1af60-116">Le operazioni di Key Vault vengono gestite separatamente tramite autorizzazioni del controllo degli accessi in base al ruolo, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1af60-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="1af60-117">Operazione</span><span class="sxs-lookup"><span data-stu-id="1af60-117">Operation</span></span> | <span data-ttu-id="1af60-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1af60-118">Description</span></span> | <span data-ttu-id="1af60-119">Autorizzazione utente</span><span class="sxs-lookup"><span data-stu-id="1af60-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="1af60-120">Elenco</span><span class="sxs-lookup"><span data-stu-id="1af60-120">List</span></span>|<span data-ttu-id="1af60-121">Elenca gli insiemi di credenziali delle chiavi eliminati.</span><span class="sxs-lookup"><span data-stu-id="1af60-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="1af60-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="1af60-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="1af60-123">Recupera</span><span class="sxs-lookup"><span data-stu-id="1af60-123">Recover</span></span>|<span data-ttu-id="1af60-124">Recupera un insieme di credenziali delle chiavi eliminato.</span><span class="sxs-lookup"><span data-stu-id="1af60-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="1af60-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="1af60-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="1af60-126">Ripulisci</span><span class="sxs-lookup"><span data-stu-id="1af60-126">Purge</span></span>|<span data-ttu-id="1af60-127">Rimuove in modo permanente un insieme di credenziali delle chiavi eliminato e tutti i relativi contenuti.</span><span class="sxs-lookup"><span data-stu-id="1af60-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="1af60-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="1af60-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="1af60-129">Per altre informazioni sulle autorizzazioni e il controllo degli accessi, vedere [Proteggere l'insieme di credenziali delle chiavi](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="1af60-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="1af60-130">Abilitazione della funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="1af60-130">Enabling soft-delete</span></span>

<span data-ttu-id="1af60-131">toorecover in grado di toobe un insieme di credenziali chiave eliminato o gli oggetti archiviati in una chiave dell'insieme di credenziali, è innanzitutto necessario abilitare soft-eliminazione per tale chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1af60-131">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="1af60-132">Insieme di credenziali delle chiavi esistente</span><span class="sxs-lookup"><span data-stu-id="1af60-132">Existing key vault</span></span>

<span data-ttu-id="1af60-133">Per un insieme di credenziali delle chiavi esistente denominato ContosoVault, è possibile abilitare l'eliminazione temporanea come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1af60-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="1af60-134">Attualmente, è necessario toouse Azure Resource Manager hello scrittura di risorse manipolazione toodirectly *enableSoftDelete* toohello proprietà risorsa insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="1af60-134">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="1af60-135">Insieme di credenziali delle chiavi nuovo</span><span class="sxs-lookup"><span data-stu-id="1af60-135">New key vault</span></span>

<span data-ttu-id="1af60-136">Soft-eliminazione per un nuovo insieme di credenziali chiave di attivazione viene eseguita al momento della creazione tramite l'aggiunta di contrassegno di abilitazione di soft-eliminazione hello tooyour creare comando.</span><span class="sxs-lookup"><span data-stu-id="1af60-136">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="1af60-137">Verificare l'abilitazione della funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="1af60-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="1af60-138">tooverify un insieme di credenziali chiave è abilitata, l'eliminazione di soft hello esecuzione *ottenere* comandi e cercare hello 'Soft eliminare Enabled?'</span><span class="sxs-lookup"><span data-stu-id="1af60-138">tooverify that a key vault has soft-delete enabled, run hello *get* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="1af60-139">è impostato su true o false.</span><span class="sxs-lookup"><span data-stu-id="1af60-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="1af60-140">Eliminazione di un insieme di credenziali delle chiavi protetto dalla funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="1af60-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="1af60-141">toodelete comando di Hello (o rimuovere) un insieme di credenziali chiave rimane hello stesso, ma le relative modifiche di comportamento a seconda se è stata attivata soft-eliminazione o non.</span><span class="sxs-lookup"><span data-stu-id="1af60-141">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="1af60-142">Se si esegue il comando precedente di hello per un insieme di credenziali chiave che non dispone di soft-eliminazione abilitata, verrà eliminata definitivamente questo insieme di credenziali chiave che il suo contenuto senza opzioni per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="1af60-142">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="1af60-143">Come la funzione di eliminazione temporanea protegge gli insiemi di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="1af60-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="1af60-144">Con la funzione di eliminazione temporanea abilitata:</span><span class="sxs-lookup"><span data-stu-id="1af60-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="1af60-145">Quando viene eliminato un insieme di credenziali chiave, viene rimosso dal relativo gruppo di risorse e inserito in uno spazio dei nomi riservato solo associati hello percorso in cui è stato creato.</span><span class="sxs-lookup"><span data-stu-id="1af60-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="1af60-146">Gli oggetti in una chiave eliminata insieme di credenziali, ad esempio le chiavi, i segreti e i certificati, non sono accessibili e rimangono pertanto mentre il contenitore insieme di credenziali chiave si trova in stato di hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="1af60-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="1af60-147">nome DNS Hello per un insieme di credenziali chiave nello stato di eliminazione viene conservato in modo, non è possibile creare un nuovo insieme di credenziali chiave con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="1af60-147">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="1af60-148">È possibile visualizzare gli archivi chiave di stato eliminato, associati alla sottoscrizione, utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1af60-148">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

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

<span data-ttu-id="1af60-149">Hello *ID risorsa* in hello output fa riferimento toohello ID di risorsa originale di questo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1af60-149">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="1af60-150">Poiché l'insieme di credenziali delle chiavi è ora in stato "eliminato", non è presente alcuna risorsa con questo ID.</span><span class="sxs-lookup"><span data-stu-id="1af60-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="1af60-151">Hello *Id* campo può essere utilizzato tooidentify hello risorsa durante il recupero o l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="1af60-151">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="1af60-152">Hello *programmata data ripulire* campo indica l'insieme di credenziali hello quando verranno eliminati definitivamente (eliminati) se per questo insieme di credenziali eliminati viene eseguita alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="1af60-152">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="1af60-153">hello toocalculate periodo, utilizzato conservazione predefinito di Hello *programmata data ripulire*, è 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="1af60-153">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="1af60-154">Recupero di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="1af60-154">Recovering a key vault</span></span>

<span data-ttu-id="1af60-155">toorecover un insieme di credenziali chiave, è necessario nome insieme di credenziali chiave di hello toospecify, gruppo di risorse e posizione.</span><span class="sxs-lookup"><span data-stu-id="1af60-155">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="1af60-156">Si noti hello percorso e il gruppo di risorse hello dell'insieme di credenziali chiave hello eliminato in base alle esigenze per un processo di ripristino della chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1af60-156">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="1af60-157">Quando viene recuperato un insieme di credenziali chiave, il risultato di hello è una nuova risorsa all'ID risorsa originale. dell'archivio chiavi hello</span><span class="sxs-lookup"><span data-stu-id="1af60-157">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="1af60-158">Se è stato rimosso il gruppo di risorse hello in insieme di credenziali chiave hello esistenti, è necessario creato un nuovo gruppo di risorse con lo stesso nome prima di poter recuperare l'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="1af60-158">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="1af60-159">Oggetti di Key Vault ed eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="1af60-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="1af60-160">Per eliminare in modo definitivo una chiave "ContosoFirstKey" in un insieme di credenziali delle chiavi denominato "ContosoVault" con la funzione di eliminazione temporanea abilitata, seguire l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="1af60-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="1af60-161">Se in un insieme di credenziali delle chiavi è abilitata la funzione di eliminazione temporanea, una chiave eliminata continua a essere visualizzata come eliminata a meno che non venga elencata o recuperata in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="1af60-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="1af60-162">Ad eccezione di elenco di una chiave eliminata, Ripristina o eliminazione, la maggior parte delle operazioni su una chiave in stato di hello eliminato non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="1af60-162">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="1af60-163">Ad esempio, chiavi toolist eliminato toorequest in un insieme di credenziali chiave usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1af60-163">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="1af60-164">Stato di transizione</span><span class="sxs-lookup"><span data-stu-id="1af60-164">Transition state</span></span> 

<span data-ttu-id="1af60-165">Quando si elimina una chiave in un insieme di credenziali chiave con soft-eliminazione abilitata, potrebbe richiedere alcuni secondi per hello toocomplete di transizione.</span><span class="sxs-lookup"><span data-stu-id="1af60-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="1af60-166">Durante questo stato di transizione, potrebbe sembrare che tale chiave hello non è nello stato attivo hello o hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="1af60-166">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="1af60-167">Questo comando elencherà tutte le chiavi eliminate nell'insieme di credenziali delle chiavi denominato "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="1af60-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="1af60-168">Utilizzo della funzione di eliminazione temporanea con gli oggetti di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="1af60-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="1af60-169">Analogamente a insiemi di credenziali chiave, una chiave eliminata, privata o certificato rimarrà nello stato di eliminazione per i giorni too90 a meno che non si ripristinarlo o eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="1af60-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="1af60-170">Chiavi</span><span class="sxs-lookup"><span data-stu-id="1af60-170">Keys</span></span>

<span data-ttu-id="1af60-171">una chiave eliminata toorecover:</span><span class="sxs-lookup"><span data-stu-id="1af60-171">toorecover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="1af60-172">toopermanently eliminare una chiave:</span><span class="sxs-lookup"><span data-stu-id="1af60-172">toopermanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="1af60-173">Dopo essere stata eliminata in modo definitivo, una chiave non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="1af60-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="1af60-174">Hello **ripristinare** e **ripulire** azioni hanno le proprie autorizzazioni associate in un criterio di accesso della chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1af60-174">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="1af60-175">Per un tooexecute in grado di toobe dell'entità utente o un servizio un **ripristinare** o **ripulire** azione devono disporre hello autorizzazione corrispondente per l'oggetto (chiave o il segreto) nei criteri di accesso di hello insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="1af60-175">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="1af60-176">Per impostazione predefinita, hello **ripulire** autorizzazione non viene aggiunto i criteri di accesso dell'archivio chiavi tooa quando hello 'tutte' scelta rapida che viene utilizzato toogrant tutti gli utenti di tooa di autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="1af60-176">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="1af60-177">L'autorizzazione di **eliminazione definitiva** deve essere concessa esplicitamente.</span><span class="sxs-lookup"><span data-stu-id="1af60-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="1af60-178">Ad esempio, hello successivo comando concede user@contoso.com tooperform autorizzazioni diverse operazioni sulle chiavi in *ContosoVault* inclusi **ripulire**.</span><span class="sxs-lookup"><span data-stu-id="1af60-178">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="1af60-179">Configurare i criteri di accesso dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="1af60-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="1af60-180">Se si ha un insieme di credenziali delle chiavi in cui è stata appena abilitata la funzione di eliminazione temporanea, è possibile che non si disponga delle autorizzazioni di **recupero** ed **eliminazione definitiva**.</span><span class="sxs-lookup"><span data-stu-id="1af60-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="1af60-181">Segreti</span><span class="sxs-lookup"><span data-stu-id="1af60-181">Secrets</span></span>

<span data-ttu-id="1af60-182">Come per le chiavi, è possibile eseguire operazioni sui segreti presenti in un insieme di credenziali delle chiavi usando i relativi comandi.</span><span class="sxs-lookup"><span data-stu-id="1af60-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="1af60-183">Segue, sono comandi hello per l'eliminazione, elencare, recupero ed eliminazione dei segreti.</span><span class="sxs-lookup"><span data-stu-id="1af60-183">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="1af60-184">Eliminare un segreto denominato SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="1af60-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="1af60-185">Elencare tutti i segreti eliminati in un insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="1af60-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="1af60-186">Ripristinare un master secret in stato di hello eliminato:</span><span class="sxs-lookup"><span data-stu-id="1af60-186">Recover a secret in hello deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="1af60-187">Eliminare in modo definitivo un segreto in stato "eliminato":</span><span class="sxs-lookup"><span data-stu-id="1af60-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="1af60-188">Dopo essere stato eliminato in modo definitivo, un segreto non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="1af60-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="1af60-189">Eliminazione definitiva e insiemi di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="1af60-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="1af60-190">Oggetti nell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="1af60-190">Key vault objects</span></span>

<span data-ttu-id="1af60-191">Dopo essere stato eliminato in modo definitivo, una chiave, un segreto o un certificato non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="1af60-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="1af60-192">Hello chiave dell'insieme di credenziali che conteneva hello eliminato oggetto tuttavia rimarrà invariata come tutti gli altri oggetti nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="1af60-192">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="1af60-193">Insiemi di credenziali delle chiavi come contenitori</span><span class="sxs-lookup"><span data-stu-id="1af60-193">Key vaults as containers</span></span>
<span data-ttu-id="1af60-194">Quando viene eliminato un insieme di credenziali delle chiavi, vengono rimossi in modo permanente anche tutti i relativi contenuti, tra cui certificati, chiavi e segreti.</span><span class="sxs-lookup"><span data-stu-id="1af60-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="1af60-195">toopurge un insieme di credenziali chiave usare hello `Remove-AzureRmKeyVault` comando con l'opzione hello `-InRemovedState` e specificando il percorso di hello dell'insieme di credenziali chiave hello eliminato con hello `-Location location` argomento.</span><span class="sxs-lookup"><span data-stu-id="1af60-195">toopurge a key vault, use hello `Remove-AzureRmKeyVault` command with hello option `-InRemovedState` and by specifying hello location of hello deleted key vault with hello `-Location location` argument.</span></span> <span data-ttu-id="1af60-196">È possibile trovare il percorso di hello di un insieme di credenziali eliminate utilizzando il comando hello `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="1af60-196">You can find hello location of a deleted vault using hello command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="1af60-197">Dopo essere stato eliminato in modo definitivo, un insieme di credenziali delle chiavi non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="1af60-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="1af60-198">Autorizzazioni di eliminazione definitiva necessarie</span><span class="sxs-lookup"><span data-stu-id="1af60-198">Purge permissions required</span></span>
- <span data-ttu-id="1af60-199">toopurge un insieme di credenziali chiave eliminato, tale che l'insieme di credenziali hello e il relativo contenuto in modo permanente viene rimossi, hello utente deve RBAC autorizzazione tooperform un *Microsoft.KeyVault/locations/deletedVaults/purge/action* operazione.</span><span class="sxs-lookup"><span data-stu-id="1af60-199">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="1af60-200">chiave hello eliminato toolist, insieme di credenziali hello un utente deve RBAC autorizzazione tooperform *Microsoft.KeyVault/deletedVaults/read* autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="1af60-200">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="1af60-201">Per impostazione predefinita, solo un amministratore della sottoscrizione ha queste autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="1af60-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="1af60-202">Eliminazione temporanea programmata</span><span class="sxs-lookup"><span data-stu-id="1af60-202">Scheduled purge</span></span>

<span data-ttu-id="1af60-203">Elenca gli oggetti eliminati insieme di credenziali chiave Mostra quando vengono toobe schedled eliminati dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="1af60-203">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="1af60-204">Hello *programmata data ripulire* campo indica quando un oggetto chiave dell'insieme di credenziali verrà eliminato definitivamente, se viene eseguita alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="1af60-204">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="1af60-205">Per impostazione predefinita, il periodo di memorizzazione hello per un oggetto eliminato insieme di credenziali delle chiavi è 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="1af60-205">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="1af60-206">Un oggetto di un insieme di credenziali delle chiavi eliminato in modo permanente, attivato dal campo *Scheduled Purge Date* (Data eliminazione definitiva programmata), viene eliminato in modo definitivo</span><span class="sxs-lookup"><span data-stu-id="1af60-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="1af60-207">e non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="1af60-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="1af60-208">Altre risorse:</span><span class="sxs-lookup"><span data-stu-id="1af60-208">Other resources</span></span>

- <span data-ttu-id="1af60-209">Per una panoramica della funzionalità di eliminazione temporanea di Key Vault, vedere [Panoramica della funzionalità di eliminazione temporanea di Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="1af60-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="1af60-210">Per una panoramica generale dell'utilizzo di Azure Key Vault, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1af60-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

