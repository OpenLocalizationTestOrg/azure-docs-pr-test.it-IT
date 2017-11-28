---
title: modifiche di tooprevent aaaLock risorse di Azure | Documenti Microsoft
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
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a><span data-ttu-id="ee59d-103">Bloccare le risorse tooprevent modifiche impreviste</span><span class="sxs-lookup"><span data-stu-id="ee59d-103">Lock resources tooprevent unexpected changes</span></span> 
<span data-ttu-id="ee59d-104">Come amministratore, potrebbe essere necessario toolock una sottoscrizione, gruppo di risorse o tooprevent risorse ad altri utenti nell'organizzazione da un'accidentale eliminazione o modifica di risorse critiche.</span><span class="sxs-lookup"><span data-stu-id="ee59d-104">As an administrator, you may need toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="ee59d-105">È possibile impostare il livello di blocco hello troppo**CanNotDelete** o **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="ee59d-105">You can set hello lock level too**CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="ee59d-106">**CanNotDelete** significa che gli utenti autorizzati possano comunque leggere e modificare una risorsa, ma non eliminare la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="ee59d-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete hello resource.</span></span> 
* <span data-ttu-id="ee59d-107">**ReadOnly** significa che gli utenti autorizzati possono leggere una risorsa, ma non possono eliminare o aggiornare la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="ee59d-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update hello resource.</span></span> <span data-ttu-id="ee59d-108">L'applicazione di questo blocco è simile toorestricting tutti autorizzato agli utenti toohello le autorizzazioni concesse da hello **lettore** ruolo.</span><span class="sxs-lookup"><span data-stu-id="ee59d-108">Applying this lock is similar toorestricting all authorized users toohello permissions granted by hello **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="ee59d-109">Come vengono applicati i blocchi</span><span class="sxs-lookup"><span data-stu-id="ee59d-109">How locks are applied</span></span>

<span data-ttu-id="ee59d-110">Quando si applica un blocco a un ambito padre, tutte le risorse in tale ambito ereditano hello stesso blocco.</span><span class="sxs-lookup"><span data-stu-id="ee59d-110">When you apply a lock at a parent scope, all resources within that scope inherit hello same lock.</span></span> <span data-ttu-id="ee59d-111">Anche le risorse in seguito si aggiungono ereditano blocco hello dall'elemento padre di hello.</span><span class="sxs-lookup"><span data-stu-id="ee59d-111">Even resources you add later inherit hello lock from hello parent.</span></span> <span data-ttu-id="ee59d-112">blocco di più restrittivo Hello nell'ereditarietà hello ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="ee59d-112">hello most restrictive lock in hello inheritance takes precedence.</span></span>

<span data-ttu-id="ee59d-113">A differenza di controllo di accesso basato sui ruoli, si utilizza Gestione blocchi tooapply una restrizione in tutti gli utenti e ruoli.</span><span class="sxs-lookup"><span data-stu-id="ee59d-113">Unlike role-based access control, you use management locks tooapply a restriction across all users and roles.</span></span> <span data-ttu-id="ee59d-114">toolearn sull'impostazione delle autorizzazioni per utenti e ruoli, vedere [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ee59d-114">toolearn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="ee59d-115">Blocchi di gestione risorse di si applicano solo toooperations che si verificano nel piano di gestione di hello, che include le operazioni inviate troppo`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ee59d-115">Resource Manager locks apply only toooperations that happen in hello management plane, which consists of operations sent too`https://management.azure.com`.</span></span> <span data-ttu-id="ee59d-116">blocchi di Hello non limitano come risorse di eseguono le proprie funzioni.</span><span class="sxs-lookup"><span data-stu-id="ee59d-116">hello locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="ee59d-117">Vengono limitate le modifiche alle risorse, ma non le operazioni delle risorse.</span><span class="sxs-lookup"><span data-stu-id="ee59d-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="ee59d-118">Ad esempio, un blocco di sola lettura su un Database SQL impedisce l'eliminazione o Modifica database hello, ma non impedisce la creazione, aggiornamento o eliminazione di dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="ee59d-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying hello database, but it does not prevent you from creating, updating, or deleting data in hello database.</span></span> <span data-ttu-id="ee59d-119">Le transazioni di dati sono consentite perché queste operazioni non vengono inviate troppo`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ee59d-119">Data transactions are permitted because those operations are not sent too`https://management.azure.com`.</span></span>

<span data-ttu-id="ee59d-120">L'applicazione **ReadOnly** può generare risultati toounexpected perché alcune operazioni che sembrano leggere operazioni effettivamente richiedono ulteriori azioni.</span><span class="sxs-lookup"><span data-stu-id="ee59d-120">Applying **ReadOnly** can lead toounexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="ee59d-121">Ad esempio, inserire un **ReadOnly** blocco su un account di archiviazione impedisce l'elenco di chiavi hello tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="ee59d-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing hello keys.</span></span> <span data-ttu-id="ee59d-122">elenco di Hello operazione delle chiavi viene gestita tramite una richiesta POST hello ha restituito le chiavi sono disponibili per le operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="ee59d-122">hello list keys operation is handled through a POST request because hello returned keys are available for write operations.</span></span> <span data-ttu-id="ee59d-123">Per un altro esempio, inserire un **ReadOnly** blocco su una risorsa di servizio App che impedisce la visualizzazione di file per la risorsa hello perché tale interazione richiede l'accesso in scrittura di Esplora Server Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee59d-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for hello resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="ee59d-124">Chi può creare o eliminare i blocchi nell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="ee59d-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="ee59d-125">i blocchi di gestione toocreate o delete, è necessario avere accesso troppo`Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*` azioni.</span><span class="sxs-lookup"><span data-stu-id="ee59d-125">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="ee59d-126">Di hello ruoli predefiniti, solo **proprietario** e **amministratore di accesso utente** vengono concesse tali azioni.</span><span class="sxs-lookup"><span data-stu-id="ee59d-126">Of hello built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="ee59d-127">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ee59d-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="ee59d-128">Modello</span><span class="sxs-lookup"><span data-stu-id="ee59d-128">Template</span></span>
<span data-ttu-id="ee59d-129">Hello esempio seguente viene illustrato un modello che crea un blocco su un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ee59d-129">hello following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="ee59d-130">account di archiviazione Hello su quali tooapply blocco hello viene fornito come parametro.</span><span class="sxs-lookup"><span data-stu-id="ee59d-130">hello storage account on which tooapply hello lock is provided as a parameter.</span></span> <span data-ttu-id="ee59d-131">Hello nome del blocco hello viene creato concatenando il nome di risorsa hello con **/Microsoft.Authorization/** e hello nome del blocco di hello, in questo caso **myLock**.</span><span class="sxs-lookup"><span data-stu-id="ee59d-131">hello name of hello lock is created by concatenating hello resource name with **/Microsoft.Authorization/** and hello name of hello lock, in this case **myLock**.</span></span>

<span data-ttu-id="ee59d-132">tipo di Hello fornito è il tipo di risorsa specifico toohello.</span><span class="sxs-lookup"><span data-stu-id="ee59d-132">hello type provided is specific toohello resource type.</span></span> <span data-ttu-id="ee59d-133">Per l'archiviazione, impostare too"Microsoft.Storage/storageaccounts/providers/locks tipo hello".</span><span class="sxs-lookup"><span data-stu-id="ee59d-133">For storage, set hello type too"Microsoft.Storage/storageaccounts/providers/locks".</span></span>

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

## <a name="powershell"></a><span data-ttu-id="ee59d-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee59d-134">PowerShell</span></span>
<span data-ttu-id="ee59d-135">Blocco è distribuita risorse con Azure PowerShell con hello [New AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) comando.</span><span class="sxs-lookup"><span data-stu-id="ee59d-135">You lock deployed resources with Azure PowerShell by using hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="ee59d-136">toolock una risorsa, specificare il nome di hello della risorsa hello, il tipo di risorsa e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ee59d-136">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="ee59d-137">toolock un gruppo di risorse, fornire il nome di hello hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ee59d-137">toolock a resource group, provide hello name of hello resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="ee59d-138">un blocco, l'utilizzo di informazioni tooget [Get AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="ee59d-138">tooget information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="ee59d-139">tooget tutti i blocchi di hello nella sottoscrizione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="ee59d-139">tooget all hello locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="ee59d-140">tooget tutti i blocchi per una risorsa, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="ee59d-140">tooget all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="ee59d-141">tooget tutti i blocchi per un gruppo di risorse, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="ee59d-141">tooget all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="ee59d-142">Azure PowerShell fornisce altri comandi per i blocchi di lavoro, ad esempio [Set AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate un blocco, e [Remove AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete un blocco.</span><span class="sxs-lookup"><span data-stu-id="ee59d-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="ee59d-143">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="ee59d-143">Azure CLI</span></span>

<span data-ttu-id="ee59d-144">Si blocca distribuiti risorse con CLI di Azure tramite hello [blocco az creare](/cli/azure/lock#create) comando.</span><span class="sxs-lookup"><span data-stu-id="ee59d-144">You lock deployed resources with Azure CLI by using hello [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="ee59d-145">toolock una risorsa, specificare il nome di hello della risorsa hello, il tipo di risorsa e il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ee59d-145">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="ee59d-146">toolock un gruppo di risorse, fornire il nome di hello hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ee59d-146">toolock a resource group, provide hello name of hello resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="ee59d-147">un blocco, l'utilizzo di informazioni tooget [elenco blocchi az](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="ee59d-147">tooget information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="ee59d-148">tooget tutti i blocchi di hello nella sottoscrizione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="ee59d-148">tooget all hello locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="ee59d-149">tooget tutti i blocchi per una risorsa, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="ee59d-149">tooget all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="ee59d-150">tooget tutti i blocchi per un gruppo di risorse, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="ee59d-150">tooget all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="ee59d-151">CLI di Azure fornisce altri comandi per i blocchi di lavoro, ad esempio [aggiornamento blocco az](/cli/azure/lock#update) tooupdate un blocco, e [blocco az eliminare](/cli/azure/lock#delete) toodelete un blocco.</span><span class="sxs-lookup"><span data-stu-id="ee59d-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) tooupdate a lock, and [az lock delete](/cli/azure/lock#delete) toodelete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="ee59d-152">API REST</span><span class="sxs-lookup"><span data-stu-id="ee59d-152">REST API</span></span>
<span data-ttu-id="ee59d-153">È possibile bloccare le risorse distribuite con hello [API REST per blocchi di gestione](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="ee59d-153">You can lock deployed resources with hello [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="ee59d-154">API REST Hello consente toocreate Elimina i blocchi e recuperare informazioni sui blocchi esistenti.</span><span class="sxs-lookup"><span data-stu-id="ee59d-154">hello REST API enables you toocreate and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="ee59d-155">toocreate un blocco, eseguire:</span><span class="sxs-lookup"><span data-stu-id="ee59d-155">toocreate a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="ee59d-156">Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="ee59d-156">hello scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="ee59d-157">Hello-nome del blocco è qualsiasi blocco hello toocall.</span><span class="sxs-lookup"><span data-stu-id="ee59d-157">hello lock-name is whatever you want toocall hello lock.</span></span> <span data-ttu-id="ee59d-158">Per api-version, usare **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="ee59d-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="ee59d-159">Nella richiesta di hello, includere un oggetto JSON che specifica le proprietà di hello blocco hello.</span><span class="sxs-lookup"><span data-stu-id="ee59d-159">In hello request, include a JSON object that specifies hello properties for hello lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="ee59d-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee59d-160">Next steps</span></span>
* <span data-ttu-id="ee59d-161">Per altre informazioni sull'uso dei blocchi di risorse, vedere [Blocco delle risorse di Azure](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="ee59d-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="ee59d-162">toolearn sull'organizzazione in modo logico le risorse, vedere [tramite tag tooorganize le risorse](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="ee59d-162">toolearn about logically organizing your resources, see [Using tags tooorganize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="ee59d-163">vedere toochange quale gruppo di risorse una risorsa in cui risiede [spostamento risorse toonew risorse del gruppo](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="ee59d-163">toochange which resource group a resource resides in, see [Move resources toonew resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="ee59d-164">È possibile applicare restrizioni e convenzioni all’interno della sottoscrizione con criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="ee59d-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="ee59d-165">Per ulteriori informazioni, vedere [risorse toomanage criteri di utilizzo e controllare l'accesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ee59d-165">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="ee59d-166">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ee59d-166">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

