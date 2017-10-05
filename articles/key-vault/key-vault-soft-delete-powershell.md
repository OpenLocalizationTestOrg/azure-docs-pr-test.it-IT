---
ms.assetid: 
title: "Azure Key Vault - Come usare la funzionalità di eliminazione temporanea con PowerShell"
description: "Esempi di casi d'uso della funzionalità di eliminazione temporanea con frammenti di codice di PowerShell"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 8cf0674f7eb139e50da4a3c22a8d8376a86b0dcc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="44db7-103">Come usare l'eliminazione temporanea di Key Vault con PowerShell</span><span class="sxs-lookup"><span data-stu-id="44db7-103">How to use Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="44db7-104">La funzionalità di eliminazione temporanea di Azure Key Vault consente il recupero di insiemi di credenziali e di oggetti di insiemi di credenziali eliminati.</span><span class="sxs-lookup"><span data-stu-id="44db7-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="44db7-105">In particolare, l'eliminazione temporanea viene applicata negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="44db7-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="44db7-106">Supporto per l'eliminazione reversibile di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="44db7-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="44db7-107">Supporto per l'eliminazione reversibile di oggetti di insiemi di credenziali delle chiavi: chiavi, segreti e certificati</span><span class="sxs-lookup"><span data-stu-id="44db7-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44db7-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="44db7-108">Prerequisites</span></span>

- <span data-ttu-id="44db7-109">Azure PowerShell 4.0.0 o versione successiva - Se non è già installato, installare Azure PowerShell e associarlo alla sottoscrizione di Azure. A questo proposito, vedere [Come installare e configurare Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="44db7-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="44db7-110">È **possibile** che nell'ambiente venga caricata una versione obsoleta del file di formattazione dell'output di PowerShell per Azure Key Vault, anziché la versione corretta.</span><span class="sxs-lookup"><span data-stu-id="44db7-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of the correct version.</span></span> <span data-ttu-id="44db7-111">È prevista una versione aggiornata di PowerShell contenente la correzione necessaria per la formattazione dell'output, al cui rilascio questo argomento verrà aggiornato.</span><span class="sxs-lookup"><span data-stu-id="44db7-111">We are anticipating an updated version of PowerShell to contain the needed correction for the output formatting and will update this topic at that time.</span></span> <span data-ttu-id="44db7-112">Di seguito è indicata la soluzione alternativa corrente, qualora si riscontri questo problema di formattazione:</span><span class="sxs-lookup"><span data-stu-id="44db7-112">The current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="44db7-113">Usare la query seguente se non viene visualizzata la proprietà abilitata per l'eliminazione temporanea descritta in questo argomento: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="44db7-113">Use the following query if you notice you're not seeing the soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="44db7-114">Per informazioni sui comandi di PowerShell relativi a Key Vault, vedere [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0) (Documentazione su PowerShell per Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="44db7-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="44db7-115">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="44db7-115">Required permissions</span></span>

<span data-ttu-id="44db7-116">Le operazioni di Key Vault vengono gestite separatamente tramite autorizzazioni del controllo degli accessi in base al ruolo, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="44db7-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="44db7-117">Operazione</span><span class="sxs-lookup"><span data-stu-id="44db7-117">Operation</span></span> | <span data-ttu-id="44db7-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="44db7-118">Description</span></span> | <span data-ttu-id="44db7-119">Autorizzazione utente</span><span class="sxs-lookup"><span data-stu-id="44db7-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="44db7-120">Elenco</span><span class="sxs-lookup"><span data-stu-id="44db7-120">List</span></span>|<span data-ttu-id="44db7-121">Elenca gli insiemi di credenziali delle chiavi eliminati.</span><span class="sxs-lookup"><span data-stu-id="44db7-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="44db7-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="44db7-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="44db7-123">Recupera</span><span class="sxs-lookup"><span data-stu-id="44db7-123">Recover</span></span>|<span data-ttu-id="44db7-124">Recupera un insieme di credenziali delle chiavi eliminato.</span><span class="sxs-lookup"><span data-stu-id="44db7-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="44db7-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="44db7-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="44db7-126">Ripulisci</span><span class="sxs-lookup"><span data-stu-id="44db7-126">Purge</span></span>|<span data-ttu-id="44db7-127">Rimuove in modo permanente un insieme di credenziali delle chiavi eliminato e tutti i relativi contenuti.</span><span class="sxs-lookup"><span data-stu-id="44db7-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="44db7-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="44db7-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="44db7-129">Per altre informazioni sulle autorizzazioni e il controllo degli accessi, vedere [Proteggere l'insieme di credenziali delle chiavi](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="44db7-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="44db7-130">Abilitazione della funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="44db7-130">Enabling soft-delete</span></span>

<span data-ttu-id="44db7-131">Per poter recuperare un insieme di credenziali delle chiavi eliminato o oggetti archiviati in un insieme di credenziali delle chiavi eliminato, è necessario prima abilitare la funzione di eliminazione temporanea per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="44db7-131">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="44db7-132">Insieme di credenziali delle chiavi esistente</span><span class="sxs-lookup"><span data-stu-id="44db7-132">Existing key vault</span></span>

<span data-ttu-id="44db7-133">Per un insieme di credenziali delle chiavi esistente denominato ContosoVault, è possibile abilitare l'eliminazione temporanea come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="44db7-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="44db7-134">Attualmente è necessario usare la funzione di modifica delle risorse di Azure Resource Manager per scrivere direttamente la proprietà *enableSoftDelete* nella risorsa di Key Vault.</span><span class="sxs-lookup"><span data-stu-id="44db7-134">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="44db7-135">Insieme di credenziali delle chiavi nuovo</span><span class="sxs-lookup"><span data-stu-id="44db7-135">New key vault</span></span>

<span data-ttu-id="44db7-136">È possibile abilitare la funzione di eliminazione temporanea per un nuovo insieme di credenziali delle chiavi al momento della creazione aggiungendo "soft-delete enable" al comando di creazione.</span><span class="sxs-lookup"><span data-stu-id="44db7-136">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="44db7-137">Verificare l'abilitazione della funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="44db7-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="44db7-138">Per verificare che in un insieme di credenziali delle chiavi sia abilitata la funzione di eliminazione temporanea, eseguire il comando *get* e controllare se l'attributo "Soft Delete Enabled?" ("Eliminazione temporanea abilitata?")</span><span class="sxs-lookup"><span data-stu-id="44db7-138">To verify that a key vault has soft-delete enabled, run the *get* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="44db7-139">è impostato su true o false.</span><span class="sxs-lookup"><span data-stu-id="44db7-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="44db7-140">Eliminazione di un insieme di credenziali delle chiavi protetto dalla funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="44db7-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="44db7-141">Il comando per eliminare (o rimuovere) un insieme di credenziali delle chiavi rimane invariato, ma il comportamento cambia a seconda che la funzione di eliminazione temporanea sia abilitata o meno.</span><span class="sxs-lookup"><span data-stu-id="44db7-141">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="44db7-142">Se si esegue il comando precedente per un insieme di credenziali delle chiavi in cui la funzione di eliminazione temporanea non è abilitata, l'insieme di credenziali delle chiavi e tutti i relativi contenuti verranno eliminati in modo permanente, senza possibilità di recupero.</span><span class="sxs-lookup"><span data-stu-id="44db7-142">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="44db7-143">Come la funzione di eliminazione temporanea protegge gli insiemi di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="44db7-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="44db7-144">Con la funzione di eliminazione temporanea abilitata:</span><span class="sxs-lookup"><span data-stu-id="44db7-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="44db7-145">Quando un insieme di credenziali delle chiavi viene eliminato, l'insieme viene rimosso dal relativo gruppo di risorse e inserito in uno spazio dei nomi riservato associato solo al percorso in cui è stato creato.</span><span class="sxs-lookup"><span data-stu-id="44db7-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="44db7-146">Gli oggetti inclusi in un insieme di credenziali delle chiavi, come chiavi, segreti e certificati, risultano non accessibili per tutto il tempo in cui l'insieme di credenziali delle chiavi in cui sono contenuti è in stato "eliminato".</span><span class="sxs-lookup"><span data-stu-id="44db7-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="44db7-147">Il nome DNS relativo a un insieme di credenziali delle chiavi in stato "eliminato" rimane riservato e non è quindi possibile creare un insieme di credenziali delle chiavi con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="44db7-147">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="44db7-148">È possibile visualizzare gli insiemi di credenziali delle chiavi in stato "eliminato" associati alla propria sottoscrizione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="44db7-148">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

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

<span data-ttu-id="44db7-149">Il valore *ID risorsa* nell'output fa riferimento all'ID risorsa originale di questo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="44db7-149">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="44db7-150">Poiché l'insieme di credenziali delle chiavi è ora in stato "eliminato", non è presente alcuna risorsa con questo ID.</span><span class="sxs-lookup"><span data-stu-id="44db7-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="44db7-151">Il campo *Id* può essere usato per identificare la risorsa durante il recupero o l'eliminazione definitiva.</span><span class="sxs-lookup"><span data-stu-id="44db7-151">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="44db7-152">Il campo *Scheduled Purge Date* (Data eliminazione definitiva programmata) indica il momento in cui l'insieme di credenziali delle chiavi verrà eliminato in modo definitivo se sull'insieme di credenziali non viene eseguita alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="44db7-152">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="44db7-153">Il periodo di memorizzazione predefinito usato per calcolare il campo *Scheduled Purge Date* (Data eliminazione definitiva programmata) è di 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="44db7-153">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="44db7-154">Recupero di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="44db7-154">Recovering a key vault</span></span>

<span data-ttu-id="44db7-155">Per recuperare un insieme di credenziali delle chiavi, è necessario specificarne il nome, il gruppo di risorse e il percorso.</span><span class="sxs-lookup"><span data-stu-id="44db7-155">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="44db7-156">Annotare il percorso e il gruppo di risorse dell'insieme di credenziali delle chiavi eliminato, poiché saranno necessari nel processo di recupero dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="44db7-156">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="44db7-157">Quando viene recuperato un insieme di credenziali delle chiavi, il risultato è una nuova risorsa con l'ID risorsa originale dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="44db7-157">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="44db7-158">Se il gruppo di risorse in cui si trova l'insieme di credenziali delle chiavi è stato rimosso, prima di poter recuperare l'insieme di credenziali delle chiavi è necessario creare un nuovo gruppo di risorse con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="44db7-158">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="44db7-159">Oggetti di Key Vault ed eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="44db7-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="44db7-160">Per eliminare in modo definitivo una chiave "ContosoFirstKey" in un insieme di credenziali delle chiavi denominato "ContosoVault" con la funzione di eliminazione temporanea abilitata, seguire l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="44db7-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="44db7-161">Se in un insieme di credenziali delle chiavi è abilitata la funzione di eliminazione temporanea, una chiave eliminata continua a essere visualizzata come eliminata a meno che non venga elencata o recuperata in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="44db7-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="44db7-162">La maggior parte delle operazioni eseguite su una chiave in stato "eliminato" ha esito negativo. Una chiave eliminata, infatti, può essere solo elencata, recuperata o eliminata in modo definitivo.</span><span class="sxs-lookup"><span data-stu-id="44db7-162">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="44db7-163">Per richiedere di compilare un elenco delle chiavi eliminate in un insieme di credenziali delle chiavi, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="44db7-163">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="44db7-164">Stato di transizione</span><span class="sxs-lookup"><span data-stu-id="44db7-164">Transition state</span></span> 

<span data-ttu-id="44db7-165">Quando si elimina una chiave in un insieme di credenziali delle chiavi con eliminazione temporanea abilitata, per completare la transizione possono essere necessari alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="44db7-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="44db7-166">Durante questo stato di transizione, è possibile che la chiave non risulti in stato attivo o in stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="44db7-166">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="44db7-167">Questo comando elencherà tutte le chiavi eliminate nell'insieme di credenziali delle chiavi denominato "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="44db7-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="44db7-168">Utilizzo della funzione di eliminazione temporanea con gli oggetti di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="44db7-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="44db7-169">Analogamente agli insiemi di credenziali delle chiavi, anche una chiave, un segreto o un certificato eliminato rimarrà in stato "eliminato" per un massimo di 90 giorni a meno che non si scelga di recuperarlo o eliminarlo in modo definitivo.</span><span class="sxs-lookup"><span data-stu-id="44db7-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="44db7-170">Chiavi</span><span class="sxs-lookup"><span data-stu-id="44db7-170">Keys</span></span>

<span data-ttu-id="44db7-171">Per recuperare una chiave eliminata:</span><span class="sxs-lookup"><span data-stu-id="44db7-171">To recover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="44db7-172">Per eliminare in modo definitivo una chiave:</span><span class="sxs-lookup"><span data-stu-id="44db7-172">To permanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="44db7-173">Dopo essere stata eliminata in modo definitivo, una chiave non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="44db7-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="44db7-174">Alle azioni di **recupero** ed **eliminazione definitiva** sono associate autorizzazioni specifiche nei criteri di accesso dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="44db7-174">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="44db7-175">Per poter eseguire un'azione di **recupero** o **eliminazione definitiva**, quindi, un utente o un'entità servizio deve avere la relativa autorizzazione sull'oggetto (chiave o segreto) nell'ambito dei criteri di accesso dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="44db7-175">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="44db7-176">Per impostazione predefinita, l'autorizzazione di **eliminazione definitiva** non viene aggiunta ai criteri di accesso dell'insieme di credenziali delle chiavi se viene usato il collegamento "all" per concedere tutte le autorizzazioni a un utente.</span><span class="sxs-lookup"><span data-stu-id="44db7-176">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="44db7-177">L'autorizzazione di **eliminazione definitiva** deve essere concessa esplicitamente.</span><span class="sxs-lookup"><span data-stu-id="44db7-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="44db7-178">Il comando seguente, ad esempio, concede l'autorizzazione user@contoso.com per eseguire varie operazioni sulle chiavi nell'insieme *ContosoVault*, tra cui l'**eliminazione definitiva**.</span><span class="sxs-lookup"><span data-stu-id="44db7-178">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="44db7-179">Configurare i criteri di accesso dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="44db7-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="44db7-180">Se si ha un insieme di credenziali delle chiavi in cui è stata appena abilitata la funzione di eliminazione temporanea, è possibile che non si disponga delle autorizzazioni di **recupero** ed **eliminazione definitiva**.</span><span class="sxs-lookup"><span data-stu-id="44db7-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="44db7-181">Segreti</span><span class="sxs-lookup"><span data-stu-id="44db7-181">Secrets</span></span>

<span data-ttu-id="44db7-182">Come per le chiavi, è possibile eseguire operazioni sui segreti presenti in un insieme di credenziali delle chiavi usando i relativi comandi.</span><span class="sxs-lookup"><span data-stu-id="44db7-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="44db7-183">Di seguito sono elencati i comandi per eliminare, elencare, recuperare ed eliminare in modo definitivo i segreti.</span><span class="sxs-lookup"><span data-stu-id="44db7-183">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="44db7-184">Eliminare un segreto denominato SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="44db7-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="44db7-185">Elencare tutti i segreti eliminati in un insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="44db7-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="44db7-186">Ripristinare un segreto in stato "eliminato":</span><span class="sxs-lookup"><span data-stu-id="44db7-186">Recover a secret in the deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="44db7-187">Eliminare in modo definitivo un segreto in stato "eliminato":</span><span class="sxs-lookup"><span data-stu-id="44db7-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="44db7-188">Dopo essere stato eliminato in modo definitivo, un segreto non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="44db7-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="44db7-189">Eliminazione definitiva e insiemi di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="44db7-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="44db7-190">Oggetti nell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="44db7-190">Key vault objects</span></span>

<span data-ttu-id="44db7-191">Dopo essere stato eliminato in modo definitivo, una chiave, un segreto o un certificato non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="44db7-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="44db7-192">L'insieme di credenziali delle chiavi che conteneva l'oggetto eliminato rimarrà tuttavia invariato, così come qualsiasi altro oggetto presente nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="44db7-192">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="44db7-193">Insiemi di credenziali delle chiavi come contenitori</span><span class="sxs-lookup"><span data-stu-id="44db7-193">Key vaults as containers</span></span>
<span data-ttu-id="44db7-194">Quando viene eliminato un insieme di credenziali delle chiavi, vengono rimossi in modo permanente anche tutti i relativi contenuti, tra cui certificati, chiavi e segreti.</span><span class="sxs-lookup"><span data-stu-id="44db7-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="44db7-195">Per eliminare in modo definitivo un insieme di credenziali delle chiavi, usare il comando `Remove-AzureRmKeyVault` con l'opzione `-InRemovedState` e specificare il percorso dell'insieme di credenziali delle chiavi eliminato con l'argomento `-Location location`.</span><span class="sxs-lookup"><span data-stu-id="44db7-195">To purge a key vault, use the `Remove-AzureRmKeyVault` command with the option `-InRemovedState` and by specifying the location of the deleted key vault with the `-Location location` argument.</span></span> <span data-ttu-id="44db7-196">È possibile trovare il percorso di un insieme di credenziali delle chiavi eliminato usando il comando `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="44db7-196">You can find the location of a deleted vault using the command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="44db7-197">Dopo essere stato eliminato in modo definitivo, un insieme di credenziali delle chiavi non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="44db7-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="44db7-198">Autorizzazioni di eliminazione definitiva necessarie</span><span class="sxs-lookup"><span data-stu-id="44db7-198">Purge permissions required</span></span>
- <span data-ttu-id="44db7-199">Per eliminare in modo definitivo un insieme di credenziali delle chiavi eliminato, così che l'insieme di credenziali e i relativi contenuti vengano rimossi in modo permanente, l'utente deve avere l'autorizzazione RBAC per eseguire un'operazione *Microsoft.KeyVault/locations/deletedVaults/purge/action*.</span><span class="sxs-lookup"><span data-stu-id="44db7-199">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="44db7-200">Per elencare la chiave eliminata in un insieme di credenziali delle chiavi, un utente deve avere l'autorizzazione RBAC per eseguire l'autorizzazione *Microsoft.KeyVault/deletedVaults/read*.</span><span class="sxs-lookup"><span data-stu-id="44db7-200">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="44db7-201">Per impostazione predefinita, solo un amministratore della sottoscrizione ha queste autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="44db7-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="44db7-202">Eliminazione temporanea programmata</span><span class="sxs-lookup"><span data-stu-id="44db7-202">Scheduled purge</span></span>

<span data-ttu-id="44db7-203">Quando si elencano gli oggetti di un insieme di credenziali eliminato, viene indicato anche quando ne è programmata l'eliminazione definitiva da Key Vault.</span><span class="sxs-lookup"><span data-stu-id="44db7-203">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="44db7-204">Il campo *Scheduled Purge Date* (Data eliminazione definitiva programmata) indica il momento in cui un oggetto dell'insieme di credenziali delle chiavi verrà eliminato in modo definitivo se non viene eseguita alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="44db7-204">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="44db7-205">Per impostazione predefinita, il periodo di memorizzazione di un oggetto di un insieme di credenziali delle chiavi eliminato è di 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="44db7-205">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="44db7-206">Un oggetto di un insieme di credenziali delle chiavi eliminato in modo permanente, attivato dal campo *Scheduled Purge Date* (Data eliminazione definitiva programmata), viene eliminato in modo definitivo</span><span class="sxs-lookup"><span data-stu-id="44db7-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="44db7-207">e non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="44db7-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="44db7-208">Altre risorse:</span><span class="sxs-lookup"><span data-stu-id="44db7-208">Other resources</span></span>

- <span data-ttu-id="44db7-209">Per una panoramica della funzionalità di eliminazione temporanea di Key Vault, vedere [Panoramica della funzionalità di eliminazione temporanea di Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="44db7-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="44db7-210">Per una panoramica generale dell'utilizzo di Azure Key Vault, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="44db7-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

