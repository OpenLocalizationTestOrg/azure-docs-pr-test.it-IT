---
title: Gestire le soluzioni di Azure con PowerShell | Documentazione Microsoft
description: Usare Azure PowerShell e Resource Manager per gestire le risorse.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: ff42e5cb29005c5f4b97babdae58bef9382071f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="69564-103">Gestire le risorse con Azure PowerShell e Resource Manager</span><span class="sxs-lookup"><span data-stu-id="69564-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69564-104">Portale</span><span class="sxs-lookup"><span data-stu-id="69564-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="69564-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="69564-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="69564-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="69564-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="69564-107">API REST</span><span class="sxs-lookup"><span data-stu-id="69564-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="69564-108">Questo articolo illustra come gestire le soluzioni con Azure PowerShell e Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="69564-108">In this article, you learn how to manage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="69564-109">Se non si ha familiarità con Resource Manager, vedere [Panoramica di Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="69564-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="69564-110">Questo argomento è incentrato sulle attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="69564-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="69564-111">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="69564-111">You will:</span></span>

1. <span data-ttu-id="69564-112">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="69564-112">Create a resource group</span></span>
2. <span data-ttu-id="69564-113">Aggiungere una risorsa al gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="69564-113">Add a resource to the resource group</span></span>
3. <span data-ttu-id="69564-114">Aggiungere un tag alla risorsa</span><span class="sxs-lookup"><span data-stu-id="69564-114">Add a tag to the resource</span></span>
4. <span data-ttu-id="69564-115">Eseguire query sulle risorse in base ai nomi o ai valori dei tag</span><span class="sxs-lookup"><span data-stu-id="69564-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="69564-116">Applicare e rimuovere un blocco sulla risorsa</span><span class="sxs-lookup"><span data-stu-id="69564-116">Apply and remove a lock on the resource</span></span>
6. <span data-ttu-id="69564-117">Eliminare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="69564-117">Delete a resource group</span></span>

<span data-ttu-id="69564-118">Questo articolo non illustra come distribuire un modello di Resource Manager nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="69564-118">This article does not show how to deploy a Resource Manager template to your subscription.</span></span> <span data-ttu-id="69564-119">Per informazioni in merito, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="69564-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="69564-120">guida introduttiva ad Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="69564-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="69564-121">Se Azure PowerShell non è installato, vedere l'articolo su [come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="69564-121">If you have not installed Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="69564-122">Se Azure PowerShell è stato installato in passato ma non è stato aggiornato di recente, è consigliabile installare l'ultima versione.</span><span class="sxs-lookup"><span data-stu-id="69564-122">If you have installed Azure PowerShell in the past but have not updated it recently, consider installing the latest version.</span></span> <span data-ttu-id="69564-123">È possibile aggiornare la versione con lo stesso metodo usato per l'installazione.</span><span class="sxs-lookup"><span data-stu-id="69564-123">You can update the version through the same method you used to install it.</span></span> <span data-ttu-id="69564-124">Se è stata usata l'Installazione guidata piattaforma Web, ad esempio, avviarla di nuovo e cercare un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="69564-124">For example, if you used the Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="69564-125">Per controllare la versione del modulo Resources di Azure, usare il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="69564-125">To check your version of the Azure Resources module, use the following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="69564-126">Questo argomento è stato aggiornato per la versione 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="69564-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="69564-127">Se si ha una versione precedente, l'esperienza utente potrebbe non corrispondere ai passaggi illustrati in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="69564-127">If you have an earlier version, your experience might not match the steps shown in this topic.</span></span> <span data-ttu-id="69564-128">Per la documentazione sui cmdlet di questa versione, vedere [AzureRM.Resources Module](/powershell/module/azurerm.resources) (Modulo AzureRM.Resources).</span><span class="sxs-lookup"><span data-stu-id="69564-128">For documentation about the cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-to-your-azure-account"></a><span data-ttu-id="69564-129">Accedere all'account Azure</span><span class="sxs-lookup"><span data-stu-id="69564-129">Log in to your Azure account</span></span>
<span data-ttu-id="69564-130">Prima di usare la soluzione, è necessario accedere al proprio account.</span><span class="sxs-lookup"><span data-stu-id="69564-130">Before working on your solution, you must log in to your account.</span></span>

<span data-ttu-id="69564-131">Per accedere al proprio account Azure, usare il cmdlet **Login-AzureRmAccount**.</span><span class="sxs-lookup"><span data-stu-id="69564-131">To log in to your Azure account, use the **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="69564-132">Il cmdlet richiede le credenziali di accesso per l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="69564-132">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="69564-133">Dopo l'accesso, vengono scaricate le impostazioni dell'account in modo che siano disponibili per Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69564-133">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="69564-134">Il cmdlet restituisce informazioni sull'account e la sottoscrizione da usare per le attività.</span><span class="sxs-lookup"><span data-stu-id="69564-134">The cmdlet returns information about your account and the subscription to use for the tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="69564-135">Se si hanno più sottoscrizioni, è possibile passare a un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="69564-135">If you have more than one subscription, you can switch to a different subscription.</span></span> <span data-ttu-id="69564-136">Per prima cosa, visualizzare tutte le sottoscrizioni dell'account.</span><span class="sxs-lookup"><span data-stu-id="69564-136">First, let's see all the subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="69564-137">Vengono restituite le sottoscrizioni abilitate e disabilitate.</span><span class="sxs-lookup"><span data-stu-id="69564-137">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="69564-138">Per passare a un'altra sottoscrizione, specificarne il nome con il cmdlet **Set-AzureRmContext**.</span><span class="sxs-lookup"><span data-stu-id="69564-138">To switch to a different subscription, provide the subscription name with the **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="69564-139">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="69564-139">Create a resource group</span></span>
<span data-ttu-id="69564-140">Prima di distribuire risorse nella sottoscrizione, è necessario creare un gruppo di risorse che conterrà le risorse.</span><span class="sxs-lookup"><span data-stu-id="69564-140">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span></span>

<span data-ttu-id="69564-141">Per creare un gruppo di risorse, usare il cmdlet **New-AzureRmResourceGroup** .</span><span class="sxs-lookup"><span data-stu-id="69564-141">To create a resource group, use the **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="69564-142">Il comando usa il parametro **Name** per specificare un nome per il gruppo di risorse e il parametro **Location** per specificarne la posizione.</span><span class="sxs-lookup"><span data-stu-id="69564-142">The command uses the **Name** parameter to specify a name for the resource group and the **Location** parameter to specify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="69564-143">L'output presenta il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="69564-143">The output is in the following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="69564-144">Se è necessario recuperare il gruppo di risorse in un secondo momento, usare il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="69564-144">If you need to retrieve the resource group later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="69564-145">Per ottenere tutti i gruppi di risorse della sottoscrizione, non specificare un nome:</span><span class="sxs-lookup"><span data-stu-id="69564-145">To get all the resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-to-a-resource-group"></a><span data-ttu-id="69564-146">Aggiungere risorse a un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="69564-146">Add resources to a resource group</span></span>
<span data-ttu-id="69564-147">Per aggiungere una risorsa al gruppo di risorse, è possibile usare il cmdlet **New-AzureRmResource** oppure un cmdlet specifico del tipo di risorsa che viene creato (ad esempio, **New-AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="69564-147">To add a resource to the resource group, you can use the **New-AzureRmResource** cmdlet or a cmdlet that is specific to the type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="69564-148">Usare un cmdlet specifico di un tipo di risorsa può risultare più semplice perché il cmdlet include i parametri per le proprietà necessarie per la nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="69564-148">You might find it easier to use a cmdlet that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span></span> <span data-ttu-id="69564-149">Per usare **New-AzureRmResource**, è necessario conoscere tutte le proprietà da impostare senza che vengano richieste.</span><span class="sxs-lookup"><span data-stu-id="69564-149">To use **New-AzureRmResource**, you must know all the properties to set without being prompted for them.</span></span>

<span data-ttu-id="69564-150">Aggiungere una risorsa tramite i cmdlet, tuttavia, potrebbe causare confusione in futuro perché la nuova risorsa non è inclusa in un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="69564-150">However, adding a resource through cmdlets might cause future confusion because the new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="69564-151">È consigliabile definire l'infrastruttura per la soluzione di Azure in un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="69564-151">Microsoft recommends defining the infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="69564-152">I modelli consentono di distribuire la soluzione in modo affidabile e ripetutamente.</span><span class="sxs-lookup"><span data-stu-id="69564-152">Templates enable you to reliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="69564-153">Per questo argomento viene creato un account di archiviazione con un cmdlet di PowerShell, ma successivamente viene generato un modello dal gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="69564-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="69564-154">Il cmdlet seguente crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="69564-154">The following cmdlet creates a storage account.</span></span> <span data-ttu-id="69564-155">Anziché usare il nome indicato nell'esempio, specificare un nome univoco per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="69564-155">Instead of using the name shown in the example, provide a unique name for the storage account.</span></span> <span data-ttu-id="69564-156">Il nome deve essere di lunghezza compresa tra 3 e 24 caratteri e contenere solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="69564-156">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="69564-157">Se si usa il nome indicato nell'esempio, verrà visualizzato un errore perché tale nome è già in uso.</span><span class="sxs-lookup"><span data-stu-id="69564-157">If you use the name shown in the example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="69564-158">Se è necessario recuperare la risorsa in un secondo momento, usare il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="69564-158">If you need to retrieve this resource later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="69564-159">Aggiungere un tag</span><span class="sxs-lookup"><span data-stu-id="69564-159">Add a tag</span></span>

<span data-ttu-id="69564-160">I tag consentono di organizzare le risorse in base a diverse proprietà.</span><span class="sxs-lookup"><span data-stu-id="69564-160">Tags enable you to organize your resources according to different properties.</span></span> <span data-ttu-id="69564-161">È ad esempio possibile che diverse risorse in diversi gruppi di risorse appartengano allo stesso reparto.</span><span class="sxs-lookup"><span data-stu-id="69564-161">For example, you may have several resources in different resource groups that belong to the same department.</span></span> <span data-ttu-id="69564-162">È possibile applicare un tag e un valore di reparto a tali risorse per contrassegnarle come appartenenti alla stessa categoria</span><span class="sxs-lookup"><span data-stu-id="69564-162">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span></span> <span data-ttu-id="69564-163">oppure indicare se una risorsa viene usata in un ambiente di produzione o di testing.</span><span class="sxs-lookup"><span data-stu-id="69564-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="69564-164">In questo argomento si applicano tag a una sola risorsa, ma nell'ambiente in uso è probabilmente opportuno applicare tag a tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="69564-164">In this topic, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span></span>

<span data-ttu-id="69564-165">Il cmdlet seguente applica due tag all'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="69564-165">The following cmdlet applies two tags to your storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="69564-166">I tag vengono aggiornati come un singolo oggetto.</span><span class="sxs-lookup"><span data-stu-id="69564-166">Tags are updated as a single object.</span></span> <span data-ttu-id="69564-167">Per aggiungere un tag a una risorsa che già include tag, per prima cosa recuperare i tag esistenti.</span><span class="sxs-lookup"><span data-stu-id="69564-167">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span></span> <span data-ttu-id="69564-168">Aggiungere il nuovo tag all'oggetto contenente i tag esistenti e riapplicare tutti i tag alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="69564-168">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="69564-169">Cercare le risorse</span><span class="sxs-lookup"><span data-stu-id="69564-169">Search for resources</span></span>

<span data-ttu-id="69564-170">Per recuperare le risorse in base a diverse condizioni di ricerca, usare il cmdlet **Find-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="69564-170">Use the **Find-AzureRmResource** cmdlet to retrieve resources for different search conditions.</span></span>

* <span data-ttu-id="69564-171">Per ottenere una risorsa in base al nome, specificare il parametro **ResourceNameContains**:</span><span class="sxs-lookup"><span data-stu-id="69564-171">To get a resource by name, provide the **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="69564-172">Per ottenere tutte le risorse in un gruppo di risorse, specificare il parametro **ResourceGroupNameContains**:</span><span class="sxs-lookup"><span data-stu-id="69564-172">To get all the resources in a resource group, provide the **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="69564-173">Per ottenere tutte le risorse con un nome e un valore di tag, specificare i parametri **TagName** e **TagValue**:</span><span class="sxs-lookup"><span data-stu-id="69564-173">To get all the resources with a tag name and value, provide the **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="69564-174">Per ottenere tutte le risorse con un determinato tipo di risorsa, specificare il parametro **ResourceType**:</span><span class="sxs-lookup"><span data-stu-id="69564-174">To all the resources with a particular resource type, provide the **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="69564-175">Bloccare una risorsa</span><span class="sxs-lookup"><span data-stu-id="69564-175">Lock a resource</span></span>

<span data-ttu-id="69564-176">Quando è necessario assicurarsi che una risorsa strategica non venga eliminata o modificata accidentalmente, applicare un blocco alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="69564-176">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span></span> <span data-ttu-id="69564-177">È possibile specificare **CanNotDelete** o **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="69564-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="69564-178">Per creare o eliminare i blocchi di gestione, è necessario avere accesso alle azioni `Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*`.</span><span class="sxs-lookup"><span data-stu-id="69564-178">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="69564-179">Fra i ruoli predefiniti, solo a Proprietario e Amministratore Accesso utenti sono concesse tali azioni.</span><span class="sxs-lookup"><span data-stu-id="69564-179">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="69564-180">Per applicare un blocco, usare il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="69564-180">To apply a lock, use the following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="69564-181">La risorsa bloccata nell'esempio precedente non potrà essere eliminata finché non verrà rimosso il blocco.</span><span class="sxs-lookup"><span data-stu-id="69564-181">The locked resource in the preceding example cannot be deleted until the lock is removed.</span></span> <span data-ttu-id="69564-182">Per rimuovere un blocco, usare:</span><span class="sxs-lookup"><span data-stu-id="69564-182">To remove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="69564-183">Per altre informazioni sull'impostazione di blocchi, vedere l'articolo su come [bloccare le risorse con Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="69564-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="69564-184">Rimuovere risorse o un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="69564-184">Remove resources or resource group</span></span>
<span data-ttu-id="69564-185">È possibile rimuovere una risorsa o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="69564-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="69564-186">Quando si rimuove un gruppo di risorse, si rimuovono anche tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="69564-186">When you remove a resource group, you also remove all the resources within that resource group.</span></span>

* <span data-ttu-id="69564-187">Per eliminare una risorsa dal gruppo di risorse, usare il cmdlet **Remove-AzureRmResource** .</span><span class="sxs-lookup"><span data-stu-id="69564-187">To delete a resource from the resource group, use the **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="69564-188">Questo cmdlet elimina la risorsa, ma non il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="69564-188">This cmdlet deletes the resource, but does not delete the resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="69564-189">Per eliminare un gruppo di risorse e tutte le relative risorse, usare il cmdlet **Remove-AzureRmResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="69564-189">To delete a resource group and all its resources, use the **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="69564-190">Per entrambi i cmdlet viene richiesto di confermare che si vuole rimuovere la risorsa o il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="69564-190">For both cmdlets, you are asked to confirm that you wish to remove the resource or resource group.</span></span> <span data-ttu-id="69564-191">Se l'eliminazione della risorsa o del gruppo di risorse viene completata, l'operazione restituisce **True**.</span><span class="sxs-lookup"><span data-stu-id="69564-191">If the operation successfully deletes the resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="69564-192">Eseguire script di Resource Manager con Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="69564-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="69564-193">Questo argomento illustra come eseguire operazioni di base sulle risorse con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69564-193">This topic shows you how to perform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="69564-194">Per scenari di gestione più avanzati, è in genere opportuno creare uno script e riusare tale script in base alle esigenze o a una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="69564-194">For more advanced management scenarios, you typically want to create a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="69564-195">[Automazione di Azure](../automation/automation-intro.md) consente di automatizzare gli script di uso frequente che gestiscono le soluzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="69564-195">[Azure Automation](../automation/automation-intro.md) provides a way for you to automate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="69564-196">Gli argomenti seguenti illustrano come usare Automazione di Azure, Resource Manager e PowerShell per eseguire attività di gestione in modo efficace:</span><span class="sxs-lookup"><span data-stu-id="69564-196">The following topics show you how to use Azure Automation, Resource Manager, and PowerShell to effectively perform management tasks:</span></span>

- <span data-ttu-id="69564-197">Per informazioni sulla creazione di un runbook, vedere [Il primo runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="69564-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="69564-198">Per informazioni sull'uso di raccolte di script, vedere [Raccolte di runbook e moduli per Automazione di Azure](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="69564-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="69564-199">Per informazioni sui runbook per l'avvio e l'arresto di macchine virtuali, vedere [Scenario di Automazione di Azure: uso di tag in formato JSON per creare una pianificazione per l'avvio e l'arresto di una macchina virtuale di Azure](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="69564-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="69564-200">Per informazioni sui runbook per l'avvio e l'arresto di macchine virtuali durante gli orari di minore attività, vedere [Soluzione Avvio/Arresto di macchine virtuali durante gli orari di minore attività in Automazione di Azure](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="69564-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="69564-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69564-201">Next steps</span></span>
* <span data-ttu-id="69564-202">Per altre informazioni sulla creazione dei modelli, vedere [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md) (Creazione di modelli di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="69564-202">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="69564-203">Per altre informazioni sulla distribuzione di modelli, vedere  [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md) (Distribuire un'applicazione con un modello di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="69564-203">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="69564-204">È possibile spostare le risorse esistenti in un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="69564-204">You can move existing resources to a new resource group.</span></span> <span data-ttu-id="69564-205">Per esempi, vedere [Spostare le risorse in un gruppo di risorse o una sottoscrizione nuovi](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="69564-205">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="69564-206">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="69564-206">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

