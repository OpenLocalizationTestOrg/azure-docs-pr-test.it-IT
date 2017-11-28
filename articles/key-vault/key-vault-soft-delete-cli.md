---
ms.assetid: 
title: insieme di credenziali delle chiave di aaaAzure - come toouse soft eliminare con CLI
description: "Esempi di casi d'uso della funzionalità di eliminazione temporanea con frammenti di codice dell'interfaccia della riga di comando"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a><span data-ttu-id="d5f14-103">Come insieme di credenziali chiave toouse soft-eliminazione con CLI</span><span class="sxs-lookup"><span data-stu-id="d5f14-103">How toouse Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="d5f14-104">La funzionalità di eliminazione temporanea di Azure Key Vault consente il recupero di insiemi di credenziali e di oggetti di insiemi di credenziali eliminati.</span><span class="sxs-lookup"><span data-stu-id="d5f14-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="d5f14-105">In particolare, gli indirizzi di soft-eliminazione hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="d5f14-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="d5f14-106">Supporto per l'eliminazione reversibile di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d5f14-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="d5f14-107">Supporto per l'eliminazione reversibile di oggetti di insiemi di credenziali delle chiavi: chiavi, segreti e certificati</span><span class="sxs-lookup"><span data-stu-id="d5f14-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5f14-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d5f14-108">Prerequisites</span></span>

- <span data-ttu-id="d5f14-109">Interfaccia della riga di comando di Azure 2.0: se non è ancora installata nell'ambiente di lavoro, vedere [Gestire Key Vault tramite l'interfaccia della riga di comando 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="d5f14-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="d5f14-110">Per informazioni sui comandi dell'interfaccia della riga di comando relativi a Key Vault, vedere [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault) (Documentazione sull'interfaccia della riga di comando 2.0 di Azure per Key Vault).</span><span class="sxs-lookup"><span data-stu-id="d5f14-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="d5f14-111">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="d5f14-111">Required permissions</span></span>

<span data-ttu-id="d5f14-112">Le operazioni di Key Vault vengono gestite separatamente tramite autorizzazioni del controllo degli accessi in base al ruolo, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d5f14-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="d5f14-113">Operazione</span><span class="sxs-lookup"><span data-stu-id="d5f14-113">Operation</span></span> | <span data-ttu-id="d5f14-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5f14-114">Description</span></span> | <span data-ttu-id="d5f14-115">Autorizzazione utente</span><span class="sxs-lookup"><span data-stu-id="d5f14-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="d5f14-116">Elenco</span><span class="sxs-lookup"><span data-stu-id="d5f14-116">List</span></span>|<span data-ttu-id="d5f14-117">Elenca gli insiemi di credenziali delle chiavi eliminati.</span><span class="sxs-lookup"><span data-stu-id="d5f14-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="d5f14-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="d5f14-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="d5f14-119">Recupera</span><span class="sxs-lookup"><span data-stu-id="d5f14-119">Recover</span></span>|<span data-ttu-id="d5f14-120">Recupera un insieme di credenziali delle chiavi eliminato.</span><span class="sxs-lookup"><span data-stu-id="d5f14-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="d5f14-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="d5f14-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="d5f14-122">Ripulisci</span><span class="sxs-lookup"><span data-stu-id="d5f14-122">Purge</span></span>|<span data-ttu-id="d5f14-123">Rimuove in modo permanente un insieme di credenziali delle chiavi eliminato e tutti i relativi contenuti.</span><span class="sxs-lookup"><span data-stu-id="d5f14-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="d5f14-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="d5f14-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="d5f14-125">Per altre informazioni sulle autorizzazioni e il controllo degli accessi, vedere [Proteggere l'insieme di credenziali delle chiavi](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d5f14-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="d5f14-126">Abilitazione della funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="d5f14-126">Enabling soft-delete</span></span>

<span data-ttu-id="d5f14-127">toorecover in grado di toobe un insieme di credenziali chiave eliminato o gli oggetti archiviati in una chiave dell'insieme di credenziali, è innanzitutto necessario abilitare soft-eliminazione per tale chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d5f14-127">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="d5f14-128">Insieme di credenziali delle chiavi esistente</span><span class="sxs-lookup"><span data-stu-id="d5f14-128">Existing key vault</span></span>

<span data-ttu-id="d5f14-129">Per un insieme di credenziali delle chiavi esistente denominato ContosoVault, è possibile abilitare l'eliminazione temporanea come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d5f14-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="d5f14-130">Attualmente, è necessario toouse Azure Resource Manager hello scrittura di risorse manipolazione toodirectly *enableSoftDelete* toohello proprietà risorsa insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="d5f14-130">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="d5f14-131">Insieme di credenziali delle chiavi nuovo</span><span class="sxs-lookup"><span data-stu-id="d5f14-131">New key vault</span></span>

<span data-ttu-id="d5f14-132">Soft-eliminazione per un nuovo insieme di credenziali chiave di attivazione viene eseguita al momento della creazione tramite l'aggiunta di contrassegno di abilitazione di soft-eliminazione hello tooyour creare comando.</span><span class="sxs-lookup"><span data-stu-id="d5f14-132">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="d5f14-133">Verificare l'abilitazione della funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="d5f14-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="d5f14-134">tooverify un insieme di credenziali chiave è abilitata, l'eliminazione di soft hello esecuzione *Mostra* comandi e cercare hello 'Soft eliminare Enabled?'</span><span class="sxs-lookup"><span data-stu-id="d5f14-134">tooverify that a key vault has soft-delete enabled, run hello *show* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="d5f14-135">è impostato su true o false.</span><span class="sxs-lookup"><span data-stu-id="d5f14-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="d5f14-136">Eliminazione di un insieme di credenziali delle chiavi protetto dalla funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="d5f14-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="d5f14-137">toodelete comando di Hello (o rimuovere) un insieme di credenziali chiave rimane hello stesso, ma le relative modifiche di comportamento a seconda se è stata attivata soft-eliminazione o non.</span><span class="sxs-lookup"><span data-stu-id="d5f14-137">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="d5f14-138">Se si esegue il comando precedente di hello per un insieme di credenziali chiave che non dispone di soft-eliminazione abilitata, verrà eliminata definitivamente questo insieme di credenziali chiave che il suo contenuto senza opzioni per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="d5f14-138">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="d5f14-139">Come la funzione di eliminazione temporanea protegge gli insiemi di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d5f14-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="d5f14-140">Con la funzione di eliminazione temporanea abilitata:</span><span class="sxs-lookup"><span data-stu-id="d5f14-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="d5f14-141">Quando viene eliminato un insieme di credenziali chiave, viene rimosso dal relativo gruppo di risorse e inserito in uno spazio dei nomi riservato solo associati hello percorso in cui è stato creato.</span><span class="sxs-lookup"><span data-stu-id="d5f14-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="d5f14-142">Gli oggetti in una chiave eliminata insieme di credenziali, ad esempio le chiavi, i segreti e i certificati, non sono accessibili e rimangono pertanto mentre il contenitore insieme di credenziali chiave si trova in stato di hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="d5f14-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="d5f14-143">nome DNS Hello per un insieme di credenziali chiave nello stato di eliminazione viene conservato in modo, non è possibile creare un nuovo insieme di credenziali chiave con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="d5f14-143">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="d5f14-144">È possibile visualizzare gli archivi chiave di stato eliminato, associati alla sottoscrizione, utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d5f14-144">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="d5f14-145">Hello *ID risorsa* in hello output fa riferimento toohello ID di risorsa originale di questo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d5f14-145">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="d5f14-146">Poiché l'insieme di credenziali delle chiavi è ora in stato "eliminato", non è presente alcuna risorsa con questo ID.</span><span class="sxs-lookup"><span data-stu-id="d5f14-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="d5f14-147">Hello *Id* campo può essere utilizzato tooidentify hello risorsa durante il recupero o l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="d5f14-147">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="d5f14-148">Hello *programmata data ripulire* campo indica l'insieme di credenziali hello quando verranno eliminati definitivamente (eliminati) se per questo insieme di credenziali eliminati viene eseguita alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="d5f14-148">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="d5f14-149">hello toocalculate periodo, utilizzato conservazione predefinito di Hello *programmata data ripulire*, è 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="d5f14-149">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="d5f14-150">Recupero di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d5f14-150">Recovering a key vault</span></span>

<span data-ttu-id="d5f14-151">toorecover un insieme di credenziali chiave, è necessario nome insieme di credenziali chiave di hello toospecify, gruppo di risorse e posizione.</span><span class="sxs-lookup"><span data-stu-id="d5f14-151">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="d5f14-152">Si noti hello percorso e il gruppo di risorse hello dell'insieme di credenziali chiave hello eliminato in base alle esigenze per un processo di ripristino della chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d5f14-152">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="d5f14-153">Quando viene recuperato un insieme di credenziali chiave, il risultato di hello è una nuova risorsa all'ID risorsa originale. dell'archivio chiavi hello</span><span class="sxs-lookup"><span data-stu-id="d5f14-153">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="d5f14-154">Se è stato rimosso il gruppo di risorse hello in insieme di credenziali chiave hello esistenti, è necessario creato un nuovo gruppo di risorse con lo stesso nome prima di poter recuperare l'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="d5f14-154">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="d5f14-155">Oggetti di Key Vault ed eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="d5f14-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="d5f14-156">Per eliminare in modo definitivo una chiave "ContosoFirstKey" in un insieme di credenziali delle chiavi denominato "ContosoVault" con la funzione di eliminazione temporanea abilitata, seguire l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="d5f14-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="d5f14-157">Se in un insieme di credenziali delle chiavi è abilitata la funzione di eliminazione temporanea, una chiave eliminata continua a essere visualizzata come eliminata a meno che non venga elencata o recuperata in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="d5f14-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="d5f14-158">Ad eccezione di elenco di una chiave eliminata, Ripristina o eliminazione, la maggior parte delle operazioni su una chiave in stato di hello eliminato non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="d5f14-158">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="d5f14-159">Ad esempio, chiavi toolist eliminato toorequest in un insieme di credenziali chiave usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d5f14-159">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="d5f14-160">Stato di transizione</span><span class="sxs-lookup"><span data-stu-id="d5f14-160">Transition state</span></span> 

<span data-ttu-id="d5f14-161">Quando si elimina una chiave in un insieme di credenziali chiave con soft-eliminazione abilitata, potrebbe richiedere alcuni secondi per hello toocomplete di transizione.</span><span class="sxs-lookup"><span data-stu-id="d5f14-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="d5f14-162">Durante questo stato di transizione, potrebbe sembrare che tale chiave hello non è nello stato attivo hello o hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="d5f14-162">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="d5f14-163">Questo comando elencherà tutte le chiavi eliminate nell'insieme di credenziali delle chiavi denominato "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="d5f14-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="d5f14-164">Utilizzo della funzione di eliminazione temporanea con gli oggetti di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d5f14-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="d5f14-165">Analogamente a insiemi di credenziali chiave, una chiave eliminata, privata o certificato rimarrà nello stato di eliminazione per i giorni too90 a meno che non si ripristinarlo o eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="d5f14-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="d5f14-166">Chiavi</span><span class="sxs-lookup"><span data-stu-id="d5f14-166">Keys</span></span>

<span data-ttu-id="d5f14-167">una chiave eliminata toorecover:</span><span class="sxs-lookup"><span data-stu-id="d5f14-167">toorecover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="d5f14-168">toopermanently eliminare una chiave:</span><span class="sxs-lookup"><span data-stu-id="d5f14-168">toopermanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="d5f14-169">Dopo essere stata eliminata in modo definitivo, una chiave non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="d5f14-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="d5f14-170">Hello **ripristinare** e **ripulire** azioni hanno le proprie autorizzazioni associate in un criterio di accesso della chiave dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="d5f14-170">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="d5f14-171">Per un tooexecute in grado di toobe dell'entità utente o un servizio un **ripristinare** o **ripulire** azione devono disporre hello autorizzazione corrispondente per l'oggetto (chiave o il segreto) nei criteri di accesso di hello insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="d5f14-171">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="d5f14-172">Per impostazione predefinita, hello **ripulire** autorizzazione non viene aggiunto i criteri di accesso dell'archivio chiavi tooa quando hello 'tutte' scelta rapida che viene utilizzato toogrant tutti gli utenti di tooa di autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="d5f14-172">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="d5f14-173">L'autorizzazione di **eliminazione definitiva** deve essere concessa esplicitamente.</span><span class="sxs-lookup"><span data-stu-id="d5f14-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="d5f14-174">Ad esempio, hello successivo comando concede user@contoso.com tooperform autorizzazioni diverse operazioni sulle chiavi in *ContosoVault* inclusi **ripulire**.</span><span class="sxs-lookup"><span data-stu-id="d5f14-174">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="d5f14-175">Configurare i criteri di accesso dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d5f14-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="d5f14-176">Se si ha un insieme di credenziali delle chiavi in cui è stata appena abilitata la funzione di eliminazione temporanea, è possibile che non si disponga delle autorizzazioni di **recupero** ed **eliminazione definitiva**.</span><span class="sxs-lookup"><span data-stu-id="d5f14-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="d5f14-177">Segreti</span><span class="sxs-lookup"><span data-stu-id="d5f14-177">Secrets</span></span>

<span data-ttu-id="d5f14-178">Come per le chiavi, è possibile eseguire operazioni sui segreti presenti in un insieme di credenziali delle chiavi usando i relativi comandi.</span><span class="sxs-lookup"><span data-stu-id="d5f14-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="d5f14-179">Segue, sono comandi hello per l'eliminazione, elencare, recupero ed eliminazione dei segreti.</span><span class="sxs-lookup"><span data-stu-id="d5f14-179">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="d5f14-180">Eliminare un segreto denominato SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="d5f14-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="d5f14-181">Elencare tutti i segreti eliminati in un insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="d5f14-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="d5f14-182">Ripristinare un master secret in stato di hello eliminato:</span><span class="sxs-lookup"><span data-stu-id="d5f14-182">Recover a secret in hello deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="d5f14-183">Eliminare in modo definitivo un segreto in stato "eliminato":</span><span class="sxs-lookup"><span data-stu-id="d5f14-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="d5f14-184">Dopo essere stato eliminato in modo definitivo, un segreto non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="d5f14-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="d5f14-185">Eliminazione definitiva e insiemi di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d5f14-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="d5f14-186">Oggetti nell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d5f14-186">Key vault objects</span></span>

<span data-ttu-id="d5f14-187">Dopo essere stato eliminato in modo definitivo, una chiave, un segreto o un certificato non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="d5f14-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="d5f14-188">Hello chiave dell'insieme di credenziali che conteneva hello eliminato oggetto tuttavia rimarrà invariata come tutti gli altri oggetti nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="d5f14-188">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="d5f14-189">Insiemi di credenziali delle chiavi come contenitori</span><span class="sxs-lookup"><span data-stu-id="d5f14-189">Key vaults as containers</span></span>
<span data-ttu-id="d5f14-190">Quando viene eliminato un insieme di credenziali delle chiavi, vengono rimossi in modo permanente anche tutti i relativi contenuti, tra cui certificati, chiavi e segreti.</span><span class="sxs-lookup"><span data-stu-id="d5f14-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="d5f14-191">toopurge un insieme di credenziali chiave usare hello `az keyvault purge` comando.</span><span class="sxs-lookup"><span data-stu-id="d5f14-191">toopurge a key vault, use hello `az keyvault purge` command.</span></span> <span data-ttu-id="d5f14-192">È possibile trovare il percorso di hello eliminata chiave insiemi di credenziali della sottoscrizione usando il comando hello `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="d5f14-192">You can find hello location your subscription's deleted key vaults using hello command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="d5f14-193">Dopo essere stato eliminato in modo definitivo, un insieme di credenziali delle chiavi non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="d5f14-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="d5f14-194">Autorizzazioni di eliminazione definitiva necessarie</span><span class="sxs-lookup"><span data-stu-id="d5f14-194">Purge permissions required</span></span>
- <span data-ttu-id="d5f14-195">toopurge un insieme di credenziali chiave eliminato, tale che l'insieme di credenziali hello e il relativo contenuto in modo permanente viene rimossi, hello utente deve RBAC autorizzazione tooperform un *Microsoft.KeyVault/locations/deletedVaults/purge/action* operazione.</span><span class="sxs-lookup"><span data-stu-id="d5f14-195">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="d5f14-196">chiave hello eliminato toolist, insieme di credenziali hello un utente deve RBAC autorizzazione tooperform *Microsoft.KeyVault/deletedVaults/read* autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="d5f14-196">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="d5f14-197">Per impostazione predefinita, solo un amministratore della sottoscrizione ha queste autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="d5f14-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="d5f14-198">Eliminazione temporanea programmata</span><span class="sxs-lookup"><span data-stu-id="d5f14-198">Scheduled purge</span></span>

<span data-ttu-id="d5f14-199">Elenca gli oggetti eliminati insieme di credenziali chiave Mostra quando vengono toobe schedled eliminati dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="d5f14-199">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="d5f14-200">Hello *programmata data ripulire* campo indica quando un oggetto chiave dell'insieme di credenziali verrà eliminato definitivamente, se viene eseguita alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="d5f14-200">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="d5f14-201">Per impostazione predefinita, il periodo di memorizzazione hello per un oggetto eliminato insieme di credenziali delle chiavi è 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="d5f14-201">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="d5f14-202">Un oggetto di un insieme di credenziali delle chiavi eliminato in modo permanente, attivato dal campo *Scheduled Purge Date* (Data eliminazione definitiva programmata), viene eliminato in modo definitivo</span><span class="sxs-lookup"><span data-stu-id="d5f14-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="d5f14-203">e non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="d5f14-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="d5f14-204">Altre risorse:</span><span class="sxs-lookup"><span data-stu-id="d5f14-204">Other resources</span></span>

- <span data-ttu-id="d5f14-205">Per una panoramica della funzionalità di eliminazione temporanea di Key Vault, vedere [Panoramica della funzionalità di eliminazione temporanea di Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="d5f14-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="d5f14-206">Per una panoramica generale dell'utilizzo di Azure Key Vault, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d5f14-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

