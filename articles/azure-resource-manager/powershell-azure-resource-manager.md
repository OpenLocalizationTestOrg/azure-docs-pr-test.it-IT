---
title: aaaManage Azure soluzioni con PowerShell | Documenti Microsoft
description: Usare le risorse di Azure PowerShell e toomanage Gestione risorse.
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
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="86a56-103">Gestire le risorse con Azure PowerShell e Resource Manager</span><span class="sxs-lookup"><span data-stu-id="86a56-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="86a56-104">Portale</span><span class="sxs-lookup"><span data-stu-id="86a56-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="86a56-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="86a56-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="86a56-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="86a56-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="86a56-107">API REST</span><span class="sxs-lookup"><span data-stu-id="86a56-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="86a56-108">In questo articolo viene illustrato come toomanage soluzioni con Azure PowerShell e Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="86a56-108">In this article, you learn how toomanage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="86a56-109">Se non si ha familiarità con Resource Manager, vedere [Panoramica di Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="86a56-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="86a56-110">Questo argomento è incentrato sulle attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="86a56-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="86a56-111">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="86a56-111">You will:</span></span>

1. <span data-ttu-id="86a56-112">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="86a56-112">Create a resource group</span></span>
2. <span data-ttu-id="86a56-113">Aggiungere un gruppo di risorse toohello</span><span class="sxs-lookup"><span data-stu-id="86a56-113">Add a resource toohello resource group</span></span>
3. <span data-ttu-id="86a56-114">Aggiungere una risorsa toohello tag</span><span class="sxs-lookup"><span data-stu-id="86a56-114">Add a tag toohello resource</span></span>
4. <span data-ttu-id="86a56-115">Eseguire query sulle risorse in base ai nomi o ai valori dei tag</span><span class="sxs-lookup"><span data-stu-id="86a56-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="86a56-116">Applicare e rimuovere un blocco sulla risorsa hello</span><span class="sxs-lookup"><span data-stu-id="86a56-116">Apply and remove a lock on hello resource</span></span>
6. <span data-ttu-id="86a56-117">Eliminare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="86a56-117">Delete a resource group</span></span>

<span data-ttu-id="86a56-118">In questo articolo non vengono visualizzati come una sottoscrizione di gestione risorse modello tooyour toodeploy.</span><span class="sxs-lookup"><span data-stu-id="86a56-118">This article does not show how toodeploy a Resource Manager template tooyour subscription.</span></span> <span data-ttu-id="86a56-119">Per informazioni in merito, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="86a56-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="86a56-120">guida introduttiva ad Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="86a56-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="86a56-121">Se non è installato Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="86a56-121">If you have not installed Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="86a56-122">Se è installato Azure PowerShell in hello precedente ma abbia non aggiornato di recente, è consigliabile installare la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="86a56-122">If you have installed Azure PowerShell in hello past but have not updated it recently, consider installing hello latest version.</span></span> <span data-ttu-id="86a56-123">È possibile aggiornare una versione di hello tramite hello stesso metodo usato tooinstall è.</span><span class="sxs-lookup"><span data-stu-id="86a56-123">You can update hello version through hello same method you used tooinstall it.</span></span> <span data-ttu-id="86a56-124">Ad esempio, se si utilizza l'installazione guidata piattaforma Web hello, avviarla di nuovo e cercare un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="86a56-124">For example, if you used hello Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="86a56-125">Utilizzare la versione del modulo di risorse di Azure, hello toocheck hello seguenti cmdlet:</span><span class="sxs-lookup"><span data-stu-id="86a56-125">toocheck your version of hello Azure Resources module, use hello following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="86a56-126">Questo argomento è stato aggiornato per la versione 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="86a56-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="86a56-127">Se si dispone di una versione precedente, l'esperienza potrebbe non corrispondere passaggi hello illustrati in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="86a56-127">If you have an earlier version, your experience might not match hello steps shown in this topic.</span></span> <span data-ttu-id="86a56-128">Per la documentazione sui cmdlet di hello in questa versione, vedere [AzureRM.Resources modulo](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="86a56-128">For documentation about hello cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="86a56-129">Accedi tooyour account Azure</span><span class="sxs-lookup"><span data-stu-id="86a56-129">Log in tooyour Azure account</span></span>
<span data-ttu-id="86a56-130">Per eseguire la soluzione, è necessario accedere tooyour account.</span><span class="sxs-lookup"><span data-stu-id="86a56-130">Before working on your solution, you must log in tooyour account.</span></span>

<span data-ttu-id="86a56-131">toolog in tooyour account Azure, utilizzare hello **accesso AzureRmAccount** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="86a56-131">toolog in tooyour Azure account, use hello **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="86a56-132">cmdlet di Hello richiede le credenziali di accesso hello per l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="86a56-132">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="86a56-133">Dopo l'accesso, scarica le impostazioni dell'account in modo che siano disponibili tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86a56-133">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="86a56-134">Hello cmdlet restituisce informazioni su toouse di sottoscrizione l'account e hello per le attività di hello.</span><span class="sxs-lookup"><span data-stu-id="86a56-134">hello cmdlet returns information about your account and hello subscription toouse for hello tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="86a56-135">Se si dispone di più di una sottoscrizione, è possibile passare tooa altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="86a56-135">If you have more than one subscription, you can switch tooa different subscription.</span></span> <span data-ttu-id="86a56-136">In primo luogo, esaminare tutte le sottoscrizioni di hello per l'account.</span><span class="sxs-lookup"><span data-stu-id="86a56-136">First, let's see all hello subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="86a56-137">Vengono restituite le sottoscrizioni abilitate e disabilitate.</span><span class="sxs-lookup"><span data-stu-id="86a56-137">It returns enabled and disabled subscriptions.</span></span>

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

<span data-ttu-id="86a56-138">tooswitch tooa altra sottoscrizione, fornire il nome di sottoscrizione hello hello **Set AzureRmContext** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="86a56-138">tooswitch tooa different subscription, provide hello subscription name with hello **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="86a56-139">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="86a56-139">Create a resource group</span></span>
<span data-ttu-id="86a56-140">Prima di distribuire qualsiasi sottoscrizione tooyour risorse, è necessario creare un gruppo di risorse contenenti risorse hello.</span><span class="sxs-lookup"><span data-stu-id="86a56-140">Before deploying any resources tooyour subscription, you must create a resource group that will contain hello resources.</span></span>

<span data-ttu-id="86a56-141">toocreate un gruppo di risorse, utilizzare hello **New AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="86a56-141">toocreate a resource group, use hello **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="86a56-142">comando Hello utilizza hello **nome** toospecify parametro un nome per il gruppo di risorse hello e hello **percorso** toospecify parametro relativo percorso.</span><span class="sxs-lookup"><span data-stu-id="86a56-142">hello command uses hello **Name** parameter toospecify a name for hello resource group and hello **Location** parameter toospecify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="86a56-143">output di Hello è nel seguente formato hello:</span><span class="sxs-lookup"><span data-stu-id="86a56-143">hello output is in hello following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="86a56-144">Gruppo di risorse tooretrieve hello in un secondo momento, utilizzare hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="86a56-144">If you need tooretrieve hello resource group later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="86a56-145">tooget tutti hello gruppi di risorse nella sottoscrizione, non si specifica un nome:</span><span class="sxs-lookup"><span data-stu-id="86a56-145">tooget all hello resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a><span data-ttu-id="86a56-146">Aggiungi gruppo di risorse tooa risorse</span><span class="sxs-lookup"><span data-stu-id="86a56-146">Add resources tooa resource group</span></span>
<span data-ttu-id="86a56-147">un gruppo di risorse toohello tooadd, è possibile utilizzare hello **New-AzureRmResource** cmdlet o un cmdlet che fa toohello specifico tipo di risorsa che si sta creando (ad esempio **New AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="86a56-147">tooadd a resource toohello resource group, you can use hello **New-AzureRmResource** cmdlet or a cmdlet that is specific toohello type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="86a56-148">Può risultare più semplice toouse un cmdlet che è il tipo di risorsa specifico tooa poiché include parametri per le proprietà di hello che sono necessari per le nuove risorse hello.</span><span class="sxs-lookup"><span data-stu-id="86a56-148">You might find it easier toouse a cmdlet that is specific tooa resource type because it includes parameters for hello properties that are needed for hello new resource.</span></span> <span data-ttu-id="86a56-149">toouse **New-AzureRmResource**, è necessario conoscere tutti hello proprietà tooset senza che venga richiesto per loro.</span><span class="sxs-lookup"><span data-stu-id="86a56-149">toouse **New-AzureRmResource**, you must know all hello properties tooset without being prompted for them.</span></span>

<span data-ttu-id="86a56-150">Tuttavia, l'aggiunta di una risorsa tramite i cmdlet potrebbe causare confusione future perché hello nuova risorsa non esiste in un modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="86a56-150">However, adding a resource through cmdlets might cause future confusion because hello new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="86a56-151">Si consiglia di definizione dell'infrastruttura di hello per la soluzione di Azure in un modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="86a56-151">Microsoft recommends defining hello infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="86a56-152">I modelli consentono tooreliably e distribuire ripetutamente la soluzione.</span><span class="sxs-lookup"><span data-stu-id="86a56-152">Templates enable you tooreliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="86a56-153">Per questo argomento viene creato un account di archiviazione con un cmdlet di PowerShell, ma successivamente viene generato un modello dal gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="86a56-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="86a56-154">Hello seguente cmdlet crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="86a56-154">hello following cmdlet creates a storage account.</span></span> <span data-ttu-id="86a56-155">Anziché il nome di hello illustrato nell'esempio hello, specificare un nome univoco per l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="86a56-155">Instead of using hello name shown in hello example, provide a unique name for hello storage account.</span></span> <span data-ttu-id="86a56-156">nome Hello deve essere di lunghezza compresa tra 3 e 24 caratteri e utilizzare solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="86a56-156">hello name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="86a56-157">Se si utilizza il nome di hello illustrato nell'esempio hello, viene visualizzato un errore perché tale nome è già in uso.</span><span class="sxs-lookup"><span data-stu-id="86a56-157">If you use hello name shown in hello example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="86a56-158">Se occorre tooretrieve questa risorsa in un secondo momento, utilizzare hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="86a56-158">If you need tooretrieve this resource later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="86a56-159">Aggiungere un tag</span><span class="sxs-lookup"><span data-stu-id="86a56-159">Add a tag</span></span>

<span data-ttu-id="86a56-160">Tag consentono di tooorganize le risorse in base a proprietà toodifferent.</span><span class="sxs-lookup"><span data-stu-id="86a56-160">Tags enable you tooorganize your resources according toodifferent properties.</span></span> <span data-ttu-id="86a56-161">Ad esempio, è possibile diverse risorse in gruppi di risorse diversi appartenenti toohello stesso reparto.</span><span class="sxs-lookup"><span data-stu-id="86a56-161">For example, you may have several resources in different resource groups that belong toohello same department.</span></span> <span data-ttu-id="86a56-162">È possibile applicare un toomark reparto tag e il valore toothose risorse come appartenenti toohello stessa categoria.</span><span class="sxs-lookup"><span data-stu-id="86a56-162">You can apply a department tag and value toothose resources toomark them as belonging toohello same category.</span></span> <span data-ttu-id="86a56-163">oppure indicare se una risorsa viene usata in un ambiente di produzione o di testing.</span><span class="sxs-lookup"><span data-stu-id="86a56-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="86a56-164">In questo argomento si applica a una risorsa di tag tooonly, ma nell'ambiente in uso è molto probabile senso tooapply tag tooall le risorse.</span><span class="sxs-lookup"><span data-stu-id="86a56-164">In this topic, you apply tags tooonly one resource, but in your environment it most likely makes sense tooapply tags tooall your resources.</span></span>

<span data-ttu-id="86a56-165">Hello seguente cmdlet applica due account di archiviazione tooyour tag:</span><span class="sxs-lookup"><span data-stu-id="86a56-165">hello following cmdlet applies two tags tooyour storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="86a56-166">I tag vengono aggiornati come un singolo oggetto.</span><span class="sxs-lookup"><span data-stu-id="86a56-166">Tags are updated as a single object.</span></span> <span data-ttu-id="86a56-167">tooadd una risorsa tooa tag che include già tag, recuperare innanzitutto i tag esistenti hello.</span><span class="sxs-lookup"><span data-stu-id="86a56-167">tooadd a tag tooa resource that already includes tags, first retrieve hello existing tags.</span></span> <span data-ttu-id="86a56-168">Aggiungere hello nuovo tag toohello oggetto contenente i tag esistenti hello e riapplicare tutte le risorse toohello tag hello.</span><span class="sxs-lookup"><span data-stu-id="86a56-168">Add hello new tag toohello object that contains hello existing tags, and reapply all hello tags toohello resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="86a56-169">Cercare le risorse</span><span class="sxs-lookup"><span data-stu-id="86a56-169">Search for resources</span></span>

<span data-ttu-id="86a56-170">Hello utilizzare **Find-AzureRmResource** cmdlet tooretrieve risorse per le condizioni di ricerca diverso.</span><span class="sxs-lookup"><span data-stu-id="86a56-170">Use hello **Find-AzureRmResource** cmdlet tooretrieve resources for different search conditions.</span></span>

* <span data-ttu-id="86a56-171">tooget una risorsa in base al nome, fornire hello **ResourceNameContains** parametro:</span><span class="sxs-lookup"><span data-stu-id="86a56-171">tooget a resource by name, provide hello **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="86a56-172">tooget tutte le risorse di hello in un gruppo di risorse, fornire hello **ResourceGroupNameContains** parametro:</span><span class="sxs-lookup"><span data-stu-id="86a56-172">tooget all hello resources in a resource group, provide hello **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="86a56-173">tooget tutte le risorse di hello con un nome di tag e il valore fornire hello **TagName** e **TagValue** parametri:</span><span class="sxs-lookup"><span data-stu-id="86a56-173">tooget all hello resources with a tag name and value, provide hello **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="86a56-174">risorse di hello tooall con un determinato tipo di risorsa, forniscono hello **ResourceType** parametro:</span><span class="sxs-lookup"><span data-stu-id="86a56-174">tooall hello resources with a particular resource type, provide hello **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="86a56-175">Bloccare una risorsa</span><span class="sxs-lookup"><span data-stu-id="86a56-175">Lock a resource</span></span>

<span data-ttu-id="86a56-176">Quando è necessario che una risorsa critica viene accidentalmente eliminata o modificata toomake, applicare una risorsa di blocco toohello.</span><span class="sxs-lookup"><span data-stu-id="86a56-176">When you need toomake sure a critical resource is not accidentally deleted or modified, apply a lock toohello resource.</span></span> <span data-ttu-id="86a56-177">È possibile specificare **CanNotDelete** o **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="86a56-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="86a56-178">i blocchi di gestione toocreate o delete, è necessario avere accesso troppo`Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*` azioni.</span><span class="sxs-lookup"><span data-stu-id="86a56-178">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="86a56-179">Ruoli predefiniti, hello solo proprietario e amministratore di accesso utente vengono concesse tali azioni.</span><span class="sxs-lookup"><span data-stu-id="86a56-179">Of hello built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="86a56-180">tooapply un blocco, utilizzare hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="86a56-180">tooapply a lock, use hello following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="86a56-181">Hello risorsa bloccata nel precedente esempio hello non è possibile eliminare il blocco di hello viene rimosso.</span><span class="sxs-lookup"><span data-stu-id="86a56-181">hello locked resource in hello preceding example cannot be deleted until hello lock is removed.</span></span> <span data-ttu-id="86a56-182">tooremove un blocco, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="86a56-182">tooremove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="86a56-183">Per altre informazioni sull'impostazione di blocchi, vedere l'articolo su come [bloccare le risorse con Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="86a56-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="86a56-184">Rimuovere risorse o un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="86a56-184">Remove resources or resource group</span></span>
<span data-ttu-id="86a56-185">È possibile rimuovere una risorsa o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="86a56-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="86a56-186">Quando si rimuove un gruppo di risorse, è inoltre possibile rimuovere tutte le risorse di hello all'interno del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="86a56-186">When you remove a resource group, you also remove all hello resources within that resource group.</span></span>

* <span data-ttu-id="86a56-187">una risorsa dal gruppo di risorse hello, utilizzare hello toodelete **Remove-AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="86a56-187">toodelete a resource from hello resource group, use hello **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="86a56-188">Questo cmdlet Elimina risorsa hello, ma non elimina il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="86a56-188">This cmdlet deletes hello resource, but does not delete hello resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="86a56-189">toodelete un gruppo di risorse e tutte le relative risorse, utilizzare hello **Remove AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="86a56-189">toodelete a resource group and all its resources, use hello **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="86a56-190">Per entrambi i cmdlet, viene chiesto tooconfirm che si desidera tooremove hello risorsa o il gruppo.</span><span class="sxs-lookup"><span data-stu-id="86a56-190">For both cmdlets, you are asked tooconfirm that you wish tooremove hello resource or resource group.</span></span> <span data-ttu-id="86a56-191">Se operazione hello consente di eliminare correttamente la risorsa hello o un gruppo di risorse, restituisce **True**.</span><span class="sxs-lookup"><span data-stu-id="86a56-191">If hello operation successfully deletes hello resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="86a56-192">Eseguire script di Resource Manager con Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="86a56-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="86a56-193">In questo argomento illustra come operazioni di base tooperform le risorse con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86a56-193">This topic shows you how tooperform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="86a56-194">Per gli scenari di gestione più avanzati, in genere desiderato toocreate uno script e riutilizzare tale script in base alle esigenze o in una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="86a56-194">For more advanced management scenarios, you typically want toocreate a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="86a56-195">[Automazione di Azure](../automation/automation-intro.md) fornisce un modo per consentire script tooautomate utilizzati di frequente per la gestione di soluzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="86a56-195">[Azure Automation](../automation/automation-intro.md) provides a way for you tooautomate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="86a56-196">Hello argomenti seguenti illustrano come PowerShell tooeffectively toouse automazione di Azure e Gestione risorse di eseguire attività di gestione:</span><span class="sxs-lookup"><span data-stu-id="86a56-196">hello following topics show you how toouse Azure Automation, Resource Manager, and PowerShell tooeffectively perform management tasks:</span></span>

- <span data-ttu-id="86a56-197">Per informazioni sulla creazione di un runbook, vedere [Il primo runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="86a56-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="86a56-198">Per informazioni sull'uso di raccolte di script, vedere [Raccolte di runbook e moduli per Automazione di Azure](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="86a56-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="86a56-199">Per i runbook che avviare e arrestare le macchine virtuali, vedere [uno scenario di automazione di Azure: toocreate tag in formato JSON con una pianificazione per la macchina virtuale di Azure avvio e arresto](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="86a56-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="86a56-200">Per informazioni sui runbook per l'avvio e l'arresto di macchine virtuali durante gli orari di minore attività, vedere [Soluzione Avvio/Arresto di macchine virtuali durante gli orari di minore attività in Automazione di Azure](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="86a56-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a56-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86a56-201">Next steps</span></span>
* <span data-ttu-id="86a56-202">toolearn sulla creazione di modelli di gestione delle risorse, vedere [la creazione di modelli di gestione risorse di Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="86a56-202">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="86a56-203">toolearn sulla distribuzione di modelli, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="86a56-203">toolearn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="86a56-204">È possibile spostare le risorse tooa nuovo gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="86a56-204">You can move existing resources tooa new resource group.</span></span> <span data-ttu-id="86a56-205">Per esempi, vedere [tooNew di spostare risorse gruppo di risorse o sottoscrizione](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="86a56-205">For examples, see [Move Resources tooNew Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="86a56-206">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="86a56-206">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

