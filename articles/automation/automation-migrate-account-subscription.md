---
title: Eseguire la migrazione delle risorse e dell'account di Automazione | Microsoft Docs
description: "L’articolo illustra come spostare un account di Automazione in Automazione di Azure e le risorse associate da una sottoscrizione all’altra."
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
ms.openlocfilehash: 687da15bdaf854254321b59350f47549781676f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="224d9-103">Eseguire la migrazione delle risorse e dell’account di Automazione</span><span class="sxs-lookup"><span data-stu-id="224d9-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="224d9-104">Per gli account di Automazione e le risorse associate (ad esempio asset, runbook, moduli, e così via) creati nel portale di Azure per i quali si vuole eseguire la migrazione da un gruppo di risorse a un altro o da una sottoscrizione a un'altra, è possibile farlo facilmente grazie alla funzionalità per [spostare le risorse](../azure-resource-manager/resource-group-move-resources.md) disponibile nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="224d9-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span></span> <span data-ttu-id="224d9-105">Tuttavia, prima di procedere, è necessario rivedere il [Controllo prima di spostare le risorse](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) e, in più, l'elenco seguente specifico per Automazione.</span><span class="sxs-lookup"><span data-stu-id="224d9-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span></span>   

1. <span data-ttu-id="224d9-106">Il gruppo di risorse/sottoscrizioni di destinazione deve essere nella stessa area di origine.</span><span class="sxs-lookup"><span data-stu-id="224d9-106">The destination subscription/resource group must be in same region as the source.</span></span>  <span data-ttu-id="224d9-107">Pertanto, gli account di Automazione non possono essere spostati tra le aree.</span><span class="sxs-lookup"><span data-stu-id="224d9-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="224d9-108">Durante lo spostamento di risorse (ad es. runbook, processi, ecc.), sia il gruppo di origine che il gruppo di destinazione sono bloccati per la durata dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="224d9-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span></span> <span data-ttu-id="224d9-109">Le operazioni di scrittura ed eliminazione sono bloccate nei gruppi fino al completamento dello spostamento.</span><span class="sxs-lookup"><span data-stu-id="224d9-109">Write and delete operations are blocked on the groups until the move completes.</span></span>  
3. <span data-ttu-id="224d9-110">I runbook o le variabili che fanno riferimento a un ID sottoscrizione o risorsa dalla sottoscrizione esistente devono essere aggiornati al termine della migrazione.</span><span class="sxs-lookup"><span data-stu-id="224d9-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="224d9-111">Questa funzionalità non supporta lo spostamento delle risorse di automazione classica.</span><span class="sxs-lookup"><span data-stu-id="224d9-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a><span data-ttu-id="224d9-112">Per spostare l'account di automazione tramite il portale</span><span class="sxs-lookup"><span data-stu-id="224d9-112">To move the Automation Account using the portal</span></span>
1. <span data-ttu-id="224d9-113">Dall'account di Automazione fare clic su **Sposta** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="224d9-113">From your Automation account, click **Move** at the top of the blade.</span></span><br> <span data-ttu-id="224d9-114">![Opzione Sposta](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="224d9-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="224d9-115">Nel pannello **Sposta risorse** , sono presenti le risorse relative all'account di Automazione e ai gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="224d9-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span></span>  <span data-ttu-id="224d9-116">Selezionare la **sottoscrizione** e il **gruppo di risorse** dagli elenchi a discesa, oppure selezionare l'opzione **creare un nuovo gruppo di risorse** e immettere il nome di un nuovo gruppo di risorse nel campo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="224d9-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span></span>  
3. <span data-ttu-id="224d9-117">Esaminare e selezionare la casella di controllo per confermare di *comprendere che gli strumenti e gli script dovranno essere aggiornati per poter utilizzare nuovi ID risorsa dopo lo spostamento delle risorse*, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="224d9-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="224d9-118">![Pannello Sposta risorse](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="224d9-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="224d9-119">Il completamento di questa operazione può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="224d9-119">This action will take several minutes to complete.</span></span>  <span data-ttu-id="224d9-120">In **Notifiche**verrà visualizzato lo stato di ciascuna operazione eseguita: convalida, migrazione e completa.</span><span class="sxs-lookup"><span data-stu-id="224d9-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="to-move-the-automation-account-using-powershell"></a><span data-ttu-id="224d9-121">Per spostare l'account di Automazione tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="224d9-121">To move the Automation Account using PowerShell</span></span>
<span data-ttu-id="224d9-122">Per spostare le risorse di Automazione esistenti in un altro gruppo di risorse o sottoscrizione, usare prima il cmdlet **Get-AzureRmResource** per ottenere l'account di Automazione specifico, poi usare il cmdlet **Move-AzureRmResource** per eseguire lo spostamento.</span><span class="sxs-lookup"><span data-stu-id="224d9-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span></span>

<span data-ttu-id="224d9-123">Nel primo esempio viene illustrato come spostare un account di Automazione in un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="224d9-123">The first example shows how to move an Automation account to a new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="224d9-124">Dopo aver eseguito l'esempio di codice riportato sopra, viene chiesto di confermare l’operazione.</span><span class="sxs-lookup"><span data-stu-id="224d9-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span></span>  <span data-ttu-id="224d9-125">Una volta fatto clic su **Sì** e dopo aver consentito allo script di continuare, l’utente non riceverà altre notifiche mentre è in corso la migrazione.</span><span class="sxs-lookup"><span data-stu-id="224d9-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span></span>  

<span data-ttu-id="224d9-126">Per eseguire lo spostamento in una nuova sottoscrizione, includere un valore per il parametro *DestinationSubscriptionId* .</span><span class="sxs-lookup"><span data-stu-id="224d9-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="224d9-127">Come per l’esempio precedente, viene chiesto di confermare l’operazione di spostamento.</span><span class="sxs-lookup"><span data-stu-id="224d9-127">As with the previous example, you will be prompted to confirm the move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="224d9-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="224d9-128">Next steps</span></span>
* <span data-ttu-id="224d9-129">Per altre informazioni sullo spostamento delle risorse in un nuovo gruppo di risorse o sottoscrizione, vedere [Spostare le risorse in un nuovo gruppo di risorse o sottoscrizione](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="224d9-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="224d9-130">Per altre informazioni sul controllo degli accessi in base al ruolo in Automazione di Azure, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="224d9-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="224d9-131">Per informazioni sui cmdlet di PowerShell per la gestione della sottoscrizione, vedere [Uso di Azure PowerShell con Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="224d9-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="224d9-132">Per informazioni sulle funzionalità del portale per la gestione della sottoscrizione, vedere [Gestire le risorse mediante il Portale di Azure](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="224d9-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
