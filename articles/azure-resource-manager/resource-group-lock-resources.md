---
title: Bloccare le risorse di Azure per impedire modifiche | Microsoft Docs
description: Impedire agli utenti di aggiornare o eliminare le risorse critiche di Azure applicando un blocco per tutti gli utenti e i ruoli.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 44c87b00f4fc63dbfd45a07d9a8cddc5eaf1a65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="lock-resources-to-prevent-unexpected-changes"></a><span data-ttu-id="407bc-103">Bloccare le risorse per impedire modifiche impreviste</span><span class="sxs-lookup"><span data-stu-id="407bc-103">Lock resources to prevent unexpected changes</span></span> 
<span data-ttu-id="407bc-104">L'amministratore può avere la necessità di bloccare una sottoscrizione, una risorsa o un gruppo di risorse per impedire che altri utenti nell'organizzazione modifichino o eliminino accidentalmente risorse strategiche.</span><span class="sxs-lookup"><span data-stu-id="407bc-104">As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="407bc-105">È possibile impostare il livello di blocco **CanNotDelete** o **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="407bc-105">You can set the lock level to **CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="407bc-106">**CanNotDelete** significa che gli utenti autorizzati possono leggere e modificare una risorsa, ma non eliminarla.</span><span class="sxs-lookup"><span data-stu-id="407bc-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.</span></span> 
* <span data-ttu-id="407bc-107">**ReadOnly** significa che gli utenti autorizzati possono leggere una risorsa, ma non eliminarla o aggiornarla.</span><span class="sxs-lookup"><span data-stu-id="407bc-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update the resource.</span></span> <span data-ttu-id="407bc-108">L'applicazione di questo blocco è simile alla concessione a tutti gli utenti autorizzati solo le autorizzazioni concesse dal ruolo **Lettore**.</span><span class="sxs-lookup"><span data-stu-id="407bc-108">Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="407bc-109">Come vengono applicati i blocchi</span><span class="sxs-lookup"><span data-stu-id="407bc-109">How locks are applied</span></span>

<span data-ttu-id="407bc-110">Quando si applica un blocco in un ambito padre, tutte le risorse in tale ambito ereditano lo stesso blocco.</span><span class="sxs-lookup"><span data-stu-id="407bc-110">When you apply a lock at a parent scope, all resources within that scope inherit the same lock.</span></span> <span data-ttu-id="407bc-111">Anche le risorse aggiunte successivamente ereditano il blocco dal padre.</span><span class="sxs-lookup"><span data-stu-id="407bc-111">Even resources you add later inherit the lock from the parent.</span></span> <span data-ttu-id="407bc-112">Il blocco più restrittivo nell'ereditarietà ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="407bc-112">The most restrictive lock in the inheritance takes precedence.</span></span>

<span data-ttu-id="407bc-113">Diversamente dal controllo degli accessi in base al ruolo, i blocchi di gestione consentono di applicare una restrizione a tutti gli utenti e i ruoli.</span><span class="sxs-lookup"><span data-stu-id="407bc-113">Unlike role-based access control, you use management locks to apply a restriction across all users and roles.</span></span> <span data-ttu-id="407bc-114">Per informazioni sull'impostazione delle autorizzazioni per utenti e ruoli, vedere [Controllo degli accessi in base al ruolo nel Portale di Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="407bc-114">To learn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="407bc-115">I blocchi di Resource Manager si applicano solo alle operazioni che si verificano nel piano di gestione, costituito da operazioni inviate a `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="407bc-115">Resource Manager locks apply only to operations that happen in the management plane, which consists of operations sent to `https://management.azure.com`.</span></span> <span data-ttu-id="407bc-116">I blocchi non limitano il modo in cui le risorse eseguono le proprie funzioni.</span><span class="sxs-lookup"><span data-stu-id="407bc-116">The locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="407bc-117">Vengono limitate le modifiche alle risorse, ma non le operazioni delle risorse.</span><span class="sxs-lookup"><span data-stu-id="407bc-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="407bc-118">Un blocco di sola lettura in un database SQL impedisce ad esempio l'eliminazione o la modifica del database, ma non impedisce la creazione, l'aggiornamento o l'eliminazione dei dati nel database.</span><span class="sxs-lookup"><span data-stu-id="407bc-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying the database, but it does not prevent you from creating, updating, or deleting data in the database.</span></span> <span data-ttu-id="407bc-119">Le transazioni di dati sono consentite in quanto tali operazioni non vengono inviate a `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="407bc-119">Data transactions are permitted because those operations are not sent to `https://management.azure.com`.</span></span>

<span data-ttu-id="407bc-120">L'applicazione di **ReadOnly** può causare risultati imprevisti, perché alcune operazioni che sembrano operazioni di lettura richiedono in effetti azioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="407bc-120">Applying **ReadOnly** can lead to unexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="407bc-121">Ad esempio, l'inserimento di un blocco **ReadOnly** in un account di archiviazione impedisce a tutti gli utenti di ottenere un elenco delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="407bc-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing the keys.</span></span> <span data-ttu-id="407bc-122">L'operazione di elenco delle chiavi viene gestita tramite una richiesta POST, perché le chiavi restituite sono disponibili per operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="407bc-122">The list keys operation is handled through a POST request because the returned keys are available for write operations.</span></span> <span data-ttu-id="407bc-123">Per fare un altro esempio, l'inserimento di un blocco **ReadOnly** in una risorsa del servizio app impedisce a Esplora Server di Visual Studio di visualizzare i file relativi alla risorsa, perché tale interazione richiede l'accesso in scrittura.</span><span class="sxs-lookup"><span data-stu-id="407bc-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for the resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="407bc-124">Chi può creare o eliminare i blocchi nell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="407bc-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="407bc-125">Per creare o eliminare i blocchi di gestione, è necessario avere accesso alle azioni `Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*`.</span><span class="sxs-lookup"><span data-stu-id="407bc-125">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="407bc-126">Dei ruoli predefiniti, solo **Proprietario** e **Amministratore Accesso utenti** garantiscono tali azioni.</span><span class="sxs-lookup"><span data-stu-id="407bc-126">Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="407bc-127">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="407bc-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="407bc-128">Modello</span><span class="sxs-lookup"><span data-stu-id="407bc-128">Template</span></span>
<span data-ttu-id="407bc-129">L'esempio seguente mostra un modello che crea un blocco in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="407bc-129">The following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="407bc-130">L'account di archiviazione a cui applicare il blocco viene specificato come parametro.</span><span class="sxs-lookup"><span data-stu-id="407bc-130">The storage account on which to apply the lock is provided as a parameter.</span></span> <span data-ttu-id="407bc-131">Il nome del blocco viene creato concatenando il nome della risorsa con **/Microsoft.Authorization/** e il nome del blocco stesso, in questo caso **myLock**.</span><span class="sxs-lookup"><span data-stu-id="407bc-131">The name of the lock is created by concatenating the resource name with **/Microsoft.Authorization/** and the name of the lock, in this case **myLock**.</span></span>

<span data-ttu-id="407bc-132">Il tipo fornito è specifico del tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="407bc-132">The type provided is specific to the resource type.</span></span> <span data-ttu-id="407bc-133">Per l'archiviazione, impostare il tipo su "Microsoft.Storage/storageaccounts/providers/locks".</span><span class="sxs-lookup"><span data-stu-id="407bc-133">For storage, set the type to "Microsoft.Storage/storageaccounts/providers/locks".</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a><span data-ttu-id="407bc-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="407bc-134">PowerShell</span></span>
<span data-ttu-id="407bc-135">Per bloccare le risorse distribuite con Azure PowerShell, usare il comando [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="407bc-135">You lock deployed resources with Azure PowerShell by using the [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="407bc-136">Per bloccare una risorsa, specificare il nome, il tipo e il gruppo di risorse della risorsa.</span><span class="sxs-lookup"><span data-stu-id="407bc-136">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="407bc-137">Per bloccare un gruppo di risorse, specificare il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="407bc-137">To lock a resource group, provide the name of the resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="407bc-138">Per ottenere informazioni su un blocco, usare [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="407bc-138">To get information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="407bc-139">Per ottenere tutti i blocchi nella sottoscrizione, usare:</span><span class="sxs-lookup"><span data-stu-id="407bc-139">To get all the locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="407bc-140">Per ottenere tutti i blocchi per una risorsa, usare:</span><span class="sxs-lookup"><span data-stu-id="407bc-140">To get all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="407bc-141">Per ottenere tutti i blocchi per un gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="407bc-141">To get all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="407bc-142">Azure PowerShell fornisce altri comandi per la gestione dei blocchi, ad esempio [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) per aggiornare un blocco e [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) per eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="407bc-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) to update a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) to delete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="407bc-143">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="407bc-143">Azure CLI</span></span>

<span data-ttu-id="407bc-144">Per bloccare le risorse distribuite con l'interfaccia della riga di comando di Azure, usare il comando [az lock create](/cli/azure/lock#create).</span><span class="sxs-lookup"><span data-stu-id="407bc-144">You lock deployed resources with Azure CLI by using the [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="407bc-145">Per bloccare una risorsa, specificare il nome, il tipo e il gruppo di risorse della risorsa.</span><span class="sxs-lookup"><span data-stu-id="407bc-145">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="407bc-146">Per bloccare un gruppo di risorse, specificare il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="407bc-146">To lock a resource group, provide the name of the resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="407bc-147">Per ottenere informazioni su un blocco, usare [az lock list](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="407bc-147">To get information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="407bc-148">Per ottenere tutti i blocchi nella sottoscrizione, usare:</span><span class="sxs-lookup"><span data-stu-id="407bc-148">To get all the locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="407bc-149">Per ottenere tutti i blocchi per una risorsa, usare:</span><span class="sxs-lookup"><span data-stu-id="407bc-149">To get all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="407bc-150">Per ottenere tutti i blocchi per un gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="407bc-150">To get all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="407bc-151">L'interfaccia della riga di comando di Azure fornisce altri comandi per i blocchi funzionanti, ad esempio [az lock update](/cli/azure/lock#update) per aggiornare un blocco e [az lock delete](/cli/azure/lock#delete) per eliminare un blocco.</span><span class="sxs-lookup"><span data-stu-id="407bc-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) to update a lock, and [az lock delete](/cli/azure/lock#delete) to delete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="407bc-152">API REST</span><span class="sxs-lookup"><span data-stu-id="407bc-152">REST API</span></span>
<span data-ttu-id="407bc-153">È possibile bloccare le risorse distribuite tramite l'[API REST per i blocchi di gestione](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="407bc-153">You can lock deployed resources with the [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="407bc-154">L'API REST consente di creare ed eliminare i blocchi e recuperare informazioni sui blocchi esistenti.</span><span class="sxs-lookup"><span data-stu-id="407bc-154">The REST API enables you to create and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="407bc-155">Per creare un blocco, eseguire:</span><span class="sxs-lookup"><span data-stu-id="407bc-155">To create a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="407bc-156">L'ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="407bc-156">The scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="407bc-157">Lock-name indica il nome che si desidera assegnare al blocco.</span><span class="sxs-lookup"><span data-stu-id="407bc-157">The lock-name is whatever you want to call the lock.</span></span> <span data-ttu-id="407bc-158">Per api-version, usare **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="407bc-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="407bc-159">Nella richiesta includere un oggetto JSON che specifica le proprietà per il blocco.</span><span class="sxs-lookup"><span data-stu-id="407bc-159">In the request, include a JSON object that specifies the properties for the lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="407bc-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="407bc-160">Next steps</span></span>
* <span data-ttu-id="407bc-161">Per altre informazioni sull'uso dei blocchi di risorse, vedere [Blocco delle risorse di Azure](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="407bc-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="407bc-162">Per informazioni sull'organizzazione logica delle risorse, vedere [Uso dei tag per organizzare le risorse](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="407bc-162">To learn about logically organizing your resources, see [Using tags to organize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="407bc-163">Per modificare il gruppo di risorse in cui si trova una risorsa, vedere [Spostamento delle risorse in un nuovo gruppo di risorse](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="407bc-163">To change which resource group a resource resides in, see [Move resources to new resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="407bc-164">È possibile applicare restrizioni e convenzioni all’interno della sottoscrizione con criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="407bc-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="407bc-165">Per altre informazioni, vedere [Usare i criteri per gestire le risorse e controllare l'accesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="407bc-165">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="407bc-166">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="407bc-166">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

