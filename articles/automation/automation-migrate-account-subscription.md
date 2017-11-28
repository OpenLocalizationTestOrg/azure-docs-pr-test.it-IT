---
title: aaaMigrate risorse e Account di automazione | Documenti Microsoft
description: In questo articolo viene descritto come toomove un'automazione dell'Account di automazione di Azure e le risorse associate da tooanother una sottoscrizione.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="e6098-103">Eseguire la migrazione delle risorse e dell’account di Automazione</span><span class="sxs-lookup"><span data-stu-id="e6098-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="e6098-104">Per gli account di automazione e le risorse associate (ad esempio asset, i runbook, moduli, e così via) che sono stati creati nel portale di Azure hello e desidera toomigrate da una risorsa gruppo tooanother o da una sottoscrizione tooanother, è possibile farlo facilmente con Hello [lo spostamento di risorse](../azure-resource-manager/resource-group-move-resources.md) funzionalità disponibile in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6098-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in hello Azure portal and want toomigrate from one resource group tooanother or from one subscription tooanother, you can accomplish this easily with hello [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in hello Azure portal.</span></span> <span data-ttu-id="e6098-105">Tuttavia, prima di procedere con questa azione, è necessario vedere seguente hello [elenco di controllo prima di spostare risorse](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) e inoltre hello elenco sotto tooAutomation specifico.</span><span class="sxs-lookup"><span data-stu-id="e6098-105">However, before proceeding with this action, you should first review hello following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, hello list below specific tooAutomation.</span></span>   

1. <span data-ttu-id="e6098-106">gruppo di risorse di sottoscrizione/destinazione Hello deve essere nella stessa area come origine di hello.</span><span class="sxs-lookup"><span data-stu-id="e6098-106">hello destination subscription/resource group must be in same region as hello source.</span></span>  <span data-ttu-id="e6098-107">Pertanto, gli account di Automazione non possono essere spostati tra le aree.</span><span class="sxs-lookup"><span data-stu-id="e6098-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="e6098-108">Quando lo spostamento delle risorse (ad esempio, i runbook, processi, e così via), sia il gruppo di origine hello e il gruppo di destinazione hello sono bloccati per la durata di hello dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="e6098-108">When moving resources (e.g. runbooks, jobs, etc.), both hello source group and hello target group are locked for hello duration of hello operation.</span></span> <span data-ttu-id="e6098-109">Scrivere e le operazioni di eliminazione sono bloccati in gruppi di hello fino al completamento di spostamento hello.</span><span class="sxs-lookup"><span data-stu-id="e6098-109">Write and delete operations are blocked on hello groups until hello move completes.</span></span>  
3. <span data-ttu-id="e6098-110">Qualsiasi runbook o variabili che fanno riferimento a un ID di risorsa o sottoscrizione dalla sottoscrizione esistente hello necessario toobe aggiornato dopo il completamento della migrazione.</span><span class="sxs-lookup"><span data-stu-id="e6098-110">Any runbooks or variables which reference a resource or subscription ID from hello existing subscription will need toobe updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="e6098-111">Questa funzionalità non supporta lo spostamento delle risorse di automazione classica.</span><span class="sxs-lookup"><span data-stu-id="e6098-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a><span data-ttu-id="e6098-112">toomove hello tramite hello portale Account di automazione</span><span class="sxs-lookup"><span data-stu-id="e6098-112">toomove hello Automation Account using hello portal</span></span>
1. <span data-ttu-id="e6098-113">Scegliere l'account di automazione, **spostare** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="e6098-113">From your Automation account, click **Move** at hello top of hello blade.</span></span><br> <span data-ttu-id="e6098-114">![Opzione Sposta](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="e6098-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="e6098-115">In hello **lo spostamento di risorse** blade, si noti che presenta le risorse correlate tooboth l'account di automazione e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="e6098-115">On hello **Move resources** blade, note that it presents resources related tooboth your Automation account and your resource group(s).</span></span>  <span data-ttu-id="e6098-116">Seleziona hello **sottoscrizione** e **gruppo di risorse** da elenchi a discesa hello o opzione hello selezionare **creare un nuovo gruppo di risorse** e immettere un nuovo nome gruppo di risorse in campo Hello fornito.</span><span class="sxs-lookup"><span data-stu-id="e6098-116">Select hello **subscription** and **resource group** from hello drop-down lists, or select hello option **create a new resource group** and enter a new resource group name in hello field provided.</span></span>  
3. <span data-ttu-id="e6098-117">Revisione e hello selezionare la casella di controllo tooacknowledge è *comprendere strumenti e script sarà necessario toobe aggiornato toouse nuovi ID di risorsa dopo aver spostate le risorse* e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e6098-117">Review and select hello checkbox tooacknowledge you *understand tools and scripts will need toobe updated toouse new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="e6098-118">![Pannello Sposta risorse](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="e6098-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="e6098-119">Questa operazione richiederà diverse toocomplete minuti.</span><span class="sxs-lookup"><span data-stu-id="e6098-119">This action will take several minutes toocomplete.</span></span>  <span data-ttu-id="e6098-120">In **Notifiche**verrà visualizzato lo stato di ciascuna operazione eseguita: convalida, migrazione e completa.</span><span class="sxs-lookup"><span data-stu-id="e6098-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="toomove-hello-automation-account-using-powershell"></a><span data-ttu-id="e6098-121">toomove hello Account di automazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6098-121">toomove hello Automation Account using PowerShell</span></span>
<span data-ttu-id="e6098-122">esistente toomove gruppo di risorse di automazione risorse tooanother o sottoscrizione, utilizzare hello **Get-AzureRmResource** cmdlet tooget hello specifico account di automazione e quindi **Move-AzureRmResource** spostamento di hello tooperform cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e6098-122">toomove existing Automation resources tooanother resource group or subscription, use hello  **Get-AzureRmResource** cmdlet tooget hello specific Automation account and then **Move-AzureRmResource** cmdlet tooperform hello move.</span></span>

<span data-ttu-id="e6098-123">Hello primo esempio viene illustrato come un'automazione toomove account tooa nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e6098-123">hello first example shows how toomove an Automation account tooa new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="e6098-124">Dopo aver eseguito hello esempio di codice precedente, sarà richiesta tooverify tooperform si desidera che questa azione.</span><span class="sxs-lookup"><span data-stu-id="e6098-124">After you execute hello above code example, you will be prompted tooverify you want tooperform this action.</span></span>  <span data-ttu-id="e6098-125">Quando si fa clic su **Sì** e consentire hello tooproceed script, non si ricevano le notifiche durante l'esecuzione della migrazione hello.</span><span class="sxs-lookup"><span data-stu-id="e6098-125">Once you click **Yes** and allow hello script tooproceed, you will not receive any notifications while it's performing hello migration.</span></span>  

<span data-ttu-id="e6098-126">toomove tooa nuova sottoscrizione, includere un valore per hello *DestinationSubscriptionId* parametro.</span><span class="sxs-lookup"><span data-stu-id="e6098-126">toomove tooa new subscription, include a value for hello *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="e6098-127">Come con hello esempio precedente, sarà richiesta tooconfirm hello move.</span><span class="sxs-lookup"><span data-stu-id="e6098-127">As with hello previous example, you will be prompted tooconfirm hello move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e6098-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e6098-128">Next steps</span></span>
* <span data-ttu-id="e6098-129">Per ulteriori informazioni sul gruppo di risorse toonew risorse mobile o una sottoscrizione, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="e6098-129">For more information about moving resources toonew resource group or subscription, see [Move  resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="e6098-130">Per ulteriori informazioni sul controllo di accesso basato sui ruoli in automazione di Azure, vedere troppo[controllo di accesso basato sui ruoli in automazione di Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="e6098-130">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="e6098-131">toolearn sui cmdlet di PowerShell per gestire la sottoscrizione, vedere [tramite Azure PowerShell con Gestione risorse](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="e6098-131">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="e6098-132">toolearn sulle funzionalità del portale per gestire la sottoscrizione, vedere [utilizzando le risorse di hello Azure Portal toomanage](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e6098-132">toolearn about portal features for managing your subscription, see [Using hello Azure Portal toomanage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
