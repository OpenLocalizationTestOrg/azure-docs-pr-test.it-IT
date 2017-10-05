---
ms.assetid: 
title: "Azure Key Vault - Come usare la funzionalità di eliminazione temporanea con l'interfaccia della riga di comando"
description: "Esempi di casi d'uso della funzionalità di eliminazione temporanea con frammenti di codice dell'interfaccia della riga di comando"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 3ee2c5dfb99d734cde25894174466b8e49823c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-cli"></a><span data-ttu-id="8d8e3-103">Come usare l'eliminazione temporanea di Key Vault con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="8d8e3-103">How to use Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="8d8e3-104">La funzionalità di eliminazione temporanea di Azure Key Vault consente il recupero di insiemi di credenziali e di oggetti di insiemi di credenziali eliminati.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="8d8e3-105">In particolare, l'eliminazione temporanea viene applicata negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d8e3-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="8d8e3-106">Supporto per l'eliminazione reversibile di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="8d8e3-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="8d8e3-107">Supporto per l'eliminazione reversibile di oggetti di insiemi di credenziali delle chiavi: chiavi, segreti e certificati</span><span class="sxs-lookup"><span data-stu-id="8d8e3-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d8e3-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8d8e3-108">Prerequisites</span></span>

- <span data-ttu-id="8d8e3-109">Interfaccia della riga di comando di Azure 2.0: se non è ancora installata nell'ambiente di lavoro, vedere [Gestire Key Vault tramite l'interfaccia della riga di comando 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="8d8e3-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="8d8e3-110">Per informazioni sui comandi dell'interfaccia della riga di comando relativi a Key Vault, vedere [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault) (Documentazione sull'interfaccia della riga di comando 2.0 di Azure per Key Vault).</span><span class="sxs-lookup"><span data-stu-id="8d8e3-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="8d8e3-111">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="8d8e3-111">Required permissions</span></span>

<span data-ttu-id="8d8e3-112">Le operazioni di Key Vault vengono gestite separatamente tramite autorizzazioni del controllo degli accessi in base al ruolo, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8d8e3-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="8d8e3-113">Operazione</span><span class="sxs-lookup"><span data-stu-id="8d8e3-113">Operation</span></span> | <span data-ttu-id="8d8e3-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8d8e3-114">Description</span></span> | <span data-ttu-id="8d8e3-115">Autorizzazione utente</span><span class="sxs-lookup"><span data-stu-id="8d8e3-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="8d8e3-116">Elenco</span><span class="sxs-lookup"><span data-stu-id="8d8e3-116">List</span></span>|<span data-ttu-id="8d8e3-117">Elenca gli insiemi di credenziali delle chiavi eliminati.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="8d8e3-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="8d8e3-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="8d8e3-119">Recupera</span><span class="sxs-lookup"><span data-stu-id="8d8e3-119">Recover</span></span>|<span data-ttu-id="8d8e3-120">Recupera un insieme di credenziali delle chiavi eliminato.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="8d8e3-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="8d8e3-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="8d8e3-122">Ripulisci</span><span class="sxs-lookup"><span data-stu-id="8d8e3-122">Purge</span></span>|<span data-ttu-id="8d8e3-123">Rimuove in modo permanente un insieme di credenziali delle chiavi eliminato e tutti i relativi contenuti.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="8d8e3-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="8d8e3-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="8d8e3-125">Per altre informazioni sulle autorizzazioni e il controllo degli accessi, vedere [Proteggere l'insieme di credenziali delle chiavi](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="8d8e3-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="8d8e3-126">Abilitazione della funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="8d8e3-126">Enabling soft-delete</span></span>

<span data-ttu-id="8d8e3-127">Per poter recuperare un insieme di credenziali delle chiavi eliminato o oggetti archiviati in un insieme di credenziali delle chiavi eliminato, è necessario prima abilitare la funzione di eliminazione temporanea per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-127">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="8d8e3-128">Insieme di credenziali delle chiavi esistente</span><span class="sxs-lookup"><span data-stu-id="8d8e3-128">Existing key vault</span></span>

<span data-ttu-id="8d8e3-129">Per un insieme di credenziali delle chiavi esistente denominato ContosoVault, è possibile abilitare l'eliminazione temporanea come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="8d8e3-130">Attualmente è necessario usare la funzione di modifica delle risorse di Azure Resource Manager per scrivere direttamente la proprietà *enableSoftDelete* nella risorsa di Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-130">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="8d8e3-131">Insieme di credenziali delle chiavi nuovo</span><span class="sxs-lookup"><span data-stu-id="8d8e3-131">New key vault</span></span>

<span data-ttu-id="8d8e3-132">È possibile abilitare la funzione di eliminazione temporanea per un nuovo insieme di credenziali delle chiavi al momento della creazione aggiungendo "soft-delete enable" al comando di creazione.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-132">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="8d8e3-133">Verificare l'abilitazione della funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="8d8e3-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="8d8e3-134">Per verificare che in un insieme di credenziali delle chiavi sia abilitata la funzione di eliminazione temporanea, eseguire il comando *show* e controllare se l'attributo "Soft Delete Enabled?" ("Eliminazione temporanea abilitata?")</span><span class="sxs-lookup"><span data-stu-id="8d8e3-134">To verify that a key vault has soft-delete enabled, run the *show* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="8d8e3-135">è impostato su true o false.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="8d8e3-136">Eliminazione di un insieme di credenziali delle chiavi protetto dalla funzione di eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="8d8e3-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="8d8e3-137">Il comando per eliminare (o rimuovere) un insieme di credenziali delle chiavi rimane invariato, ma il comportamento cambia a seconda che la funzione di eliminazione temporanea sia abilitata o meno.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-137">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="8d8e3-138">Se si esegue il comando precedente per un insieme di credenziali delle chiavi in cui la funzione di eliminazione temporanea non è abilitata, l'insieme di credenziali delle chiavi e tutti i relativi contenuti verranno eliminati in modo permanente, senza possibilità di recupero.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-138">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="8d8e3-139">Come la funzione di eliminazione temporanea protegge gli insiemi di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="8d8e3-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="8d8e3-140">Con la funzione di eliminazione temporanea abilitata:</span><span class="sxs-lookup"><span data-stu-id="8d8e3-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="8d8e3-141">Quando un insieme di credenziali delle chiavi viene eliminato, l'insieme viene rimosso dal relativo gruppo di risorse e inserito in uno spazio dei nomi riservato associato solo al percorso in cui è stato creato.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="8d8e3-142">Gli oggetti inclusi in un insieme di credenziali delle chiavi, come chiavi, segreti e certificati, risultano non accessibili per tutto il tempo in cui l'insieme di credenziali delle chiavi in cui sono contenuti è in stato "eliminato".</span><span class="sxs-lookup"><span data-stu-id="8d8e3-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="8d8e3-143">Il nome DNS relativo a un insieme di credenziali delle chiavi in stato "eliminato" rimane riservato e non è quindi possibile creare un insieme di credenziali delle chiavi con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-143">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="8d8e3-144">È possibile visualizzare gli insiemi di credenziali delle chiavi in stato "eliminato" associati alla propria sottoscrizione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8d8e3-144">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="8d8e3-145">Il valore *ID risorsa* nell'output fa riferimento all'ID risorsa originale di questo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-145">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="8d8e3-146">Poiché l'insieme di credenziali delle chiavi è ora in stato "eliminato", non è presente alcuna risorsa con questo ID.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="8d8e3-147">Il campo *Id* può essere usato per identificare la risorsa durante il recupero o l'eliminazione definitiva.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-147">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="8d8e3-148">Il campo *Scheduled Purge Date* (Data eliminazione definitiva programmata) indica il momento in cui l'insieme di credenziali delle chiavi verrà eliminato in modo definitivo se sull'insieme di credenziali non viene eseguita alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-148">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="8d8e3-149">Il periodo di memorizzazione predefinito usato per calcolare il campo *Scheduled Purge Date* (Data eliminazione definitiva programmata) è di 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-149">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="8d8e3-150">Recupero di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="8d8e3-150">Recovering a key vault</span></span>

<span data-ttu-id="8d8e3-151">Per recuperare un insieme di credenziali delle chiavi, è necessario specificarne il nome, il gruppo di risorse e il percorso.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-151">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="8d8e3-152">Annotare il percorso e il gruppo di risorse dell'insieme di credenziali delle chiavi eliminato, poiché saranno necessari nel processo di recupero dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-152">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="8d8e3-153">Quando viene recuperato un insieme di credenziali delle chiavi, il risultato è una nuova risorsa con l'ID risorsa originale dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-153">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="8d8e3-154">Se il gruppo di risorse in cui si trova l'insieme di credenziali delle chiavi è stato rimosso, prima di poter recuperare l'insieme di credenziali delle chiavi è necessario creare un nuovo gruppo di risorse con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-154">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="8d8e3-155">Oggetti di Key Vault ed eliminazione temporanea</span><span class="sxs-lookup"><span data-stu-id="8d8e3-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="8d8e3-156">Per eliminare in modo definitivo una chiave "ContosoFirstKey" in un insieme di credenziali delle chiavi denominato "ContosoVault" con la funzione di eliminazione temporanea abilitata, seguire l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="8d8e3-157">Se in un insieme di credenziali delle chiavi è abilitata la funzione di eliminazione temporanea, una chiave eliminata continua a essere visualizzata come eliminata a meno che non venga elencata o recuperata in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="8d8e3-158">La maggior parte delle operazioni eseguite su una chiave in stato "eliminato" ha esito negativo. Una chiave eliminata, infatti, può essere solo elencata, recuperata o eliminata in modo definitivo.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-158">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="8d8e3-159">Per richiedere di compilare un elenco delle chiavi eliminate in un insieme di credenziali delle chiavi, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8d8e3-159">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="8d8e3-160">Stato di transizione</span><span class="sxs-lookup"><span data-stu-id="8d8e3-160">Transition state</span></span> 

<span data-ttu-id="8d8e3-161">Quando si elimina una chiave in un insieme di credenziali delle chiavi con eliminazione temporanea abilitata, per completare la transizione possono essere necessari alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="8d8e3-162">Durante questo stato di transizione, è possibile che la chiave non risulti in stato attivo o in stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-162">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="8d8e3-163">Questo comando elencherà tutte le chiavi eliminate nell'insieme di credenziali delle chiavi denominato "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="8d8e3-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="8d8e3-164">Utilizzo della funzione di eliminazione temporanea con gli oggetti di un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="8d8e3-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="8d8e3-165">Analogamente agli insiemi di credenziali delle chiavi, anche una chiave, un segreto o un certificato eliminato rimarrà in stato "eliminato" per un massimo di 90 giorni a meno che non si scelga di recuperarlo o eliminarlo in modo definitivo.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="8d8e3-166">Chiavi</span><span class="sxs-lookup"><span data-stu-id="8d8e3-166">Keys</span></span>

<span data-ttu-id="8d8e3-167">Per recuperare una chiave eliminata:</span><span class="sxs-lookup"><span data-stu-id="8d8e3-167">To recover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="8d8e3-168">Per eliminare in modo definitivo una chiave:</span><span class="sxs-lookup"><span data-stu-id="8d8e3-168">To permanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="8d8e3-169">Dopo essere stata eliminata in modo definitivo, una chiave non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="8d8e3-170">Alle azioni di **recupero** ed **eliminazione definitiva** sono associate autorizzazioni specifiche nei criteri di accesso dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-170">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="8d8e3-171">Per poter eseguire un'azione di **recupero** o **eliminazione definitiva**, quindi, un utente o un'entità servizio deve avere la relativa autorizzazione sull'oggetto (chiave o segreto) nell'ambito dei criteri di accesso dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-171">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="8d8e3-172">Per impostazione predefinita, l'autorizzazione di **eliminazione definitiva** non viene aggiunta ai criteri di accesso dell'insieme di credenziali delle chiavi se viene usato il collegamento "all" per concedere tutte le autorizzazioni a un utente.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-172">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="8d8e3-173">L'autorizzazione di **eliminazione definitiva** deve essere concessa esplicitamente.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="8d8e3-174">Il comando seguente, ad esempio, concede l'autorizzazione user@contoso.com per eseguire varie operazioni sulle chiavi nell'insieme *ContosoVault*, tra cui l'**eliminazione definitiva**.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-174">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="8d8e3-175">Configurare i criteri di accesso dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="8d8e3-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="8d8e3-176">Se si ha un insieme di credenziali delle chiavi in cui è stata appena abilitata la funzione di eliminazione temporanea, è possibile che non si disponga delle autorizzazioni di **recupero** ed **eliminazione definitiva**.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="8d8e3-177">Segreti</span><span class="sxs-lookup"><span data-stu-id="8d8e3-177">Secrets</span></span>

<span data-ttu-id="8d8e3-178">Come per le chiavi, è possibile eseguire operazioni sui segreti presenti in un insieme di credenziali delle chiavi usando i relativi comandi.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="8d8e3-179">Di seguito sono elencati i comandi per eliminare, elencare, recuperare ed eliminare in modo definitivo i segreti.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-179">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="8d8e3-180">Eliminare un segreto denominato SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="8d8e3-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="8d8e3-181">Elencare tutti i segreti eliminati in un insieme di credenziali delle chiavi:</span><span class="sxs-lookup"><span data-stu-id="8d8e3-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="8d8e3-182">Ripristinare un segreto in stato "eliminato":</span><span class="sxs-lookup"><span data-stu-id="8d8e3-182">Recover a secret in the deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="8d8e3-183">Eliminare in modo definitivo un segreto in stato "eliminato":</span><span class="sxs-lookup"><span data-stu-id="8d8e3-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="8d8e3-184">Dopo essere stato eliminato in modo definitivo, un segreto non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="8d8e3-185">Eliminazione definitiva e insiemi di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="8d8e3-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="8d8e3-186">Oggetti nell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="8d8e3-186">Key vault objects</span></span>

<span data-ttu-id="8d8e3-187">Dopo essere stato eliminato in modo definitivo, una chiave, un segreto o un certificato non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="8d8e3-188">L'insieme di credenziali delle chiavi che conteneva l'oggetto eliminato rimarrà tuttavia invariato, così come qualsiasi altro oggetto presente nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-188">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="8d8e3-189">Insiemi di credenziali delle chiavi come contenitori</span><span class="sxs-lookup"><span data-stu-id="8d8e3-189">Key vaults as containers</span></span>
<span data-ttu-id="8d8e3-190">Quando viene eliminato un insieme di credenziali delle chiavi, vengono rimossi in modo permanente anche tutti i relativi contenuti, tra cui certificati, chiavi e segreti.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="8d8e3-191">Per eliminare in modo definitivo un insieme di credenziali delle chiavi, usare il comando `az keyvault purge`.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-191">To purge a key vault, use the `az keyvault purge` command.</span></span> <span data-ttu-id="8d8e3-192">È possibile trovare il percorso degli insiemi di credenziali delle chiavi eliminati nella sottoscrizione usando il comando `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-192">You can find the location your subscription's deleted key vaults using the command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="8d8e3-193">Dopo essere stato eliminato in modo definitivo, un insieme di credenziali delle chiavi non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="8d8e3-194">Autorizzazioni di eliminazione definitiva necessarie</span><span class="sxs-lookup"><span data-stu-id="8d8e3-194">Purge permissions required</span></span>
- <span data-ttu-id="8d8e3-195">Per eliminare in modo definitivo un insieme di credenziali delle chiavi eliminato, così che l'insieme di credenziali e i relativi contenuti vengano rimossi in modo permanente, l'utente deve avere l'autorizzazione RBAC per eseguire un'operazione *Microsoft.KeyVault/locations/deletedVaults/purge/action*.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-195">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="8d8e3-196">Per elencare la chiave eliminata in un insieme di credenziali delle chiavi, un utente deve avere l'autorizzazione RBAC per eseguire l'autorizzazione *Microsoft.KeyVault/deletedVaults/read*.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-196">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="8d8e3-197">Per impostazione predefinita, solo un amministratore della sottoscrizione ha queste autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="8d8e3-198">Eliminazione temporanea programmata</span><span class="sxs-lookup"><span data-stu-id="8d8e3-198">Scheduled purge</span></span>

<span data-ttu-id="8d8e3-199">Quando si elencano gli oggetti di un insieme di credenziali eliminato, viene indicato anche quando ne è programmata l'eliminazione definitiva da Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-199">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="8d8e3-200">Il campo *Scheduled Purge Date* (Data eliminazione definitiva programmata) indica il momento in cui un oggetto dell'insieme di credenziali delle chiavi verrà eliminato in modo definitivo se non viene eseguita alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-200">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="8d8e3-201">Per impostazione predefinita, il periodo di memorizzazione di un oggetto di un insieme di credenziali delle chiavi eliminato è di 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-201">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="8d8e3-202">Un oggetto di un insieme di credenziali delle chiavi eliminato in modo permanente, attivato dal campo *Scheduled Purge Date* (Data eliminazione definitiva programmata), viene eliminato in modo definitivo</span><span class="sxs-lookup"><span data-stu-id="8d8e3-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="8d8e3-203">e non è più recuperabile.</span><span class="sxs-lookup"><span data-stu-id="8d8e3-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="8d8e3-204">Altre risorse:</span><span class="sxs-lookup"><span data-stu-id="8d8e3-204">Other resources</span></span>

- <span data-ttu-id="8d8e3-205">Per una panoramica della funzionalità di eliminazione temporanea di Key Vault, vedere [Panoramica della funzionalità di eliminazione temporanea di Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="8d8e3-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="8d8e3-206">Per una panoramica generale dell'utilizzo di Azure Key Vault, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8d8e3-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

