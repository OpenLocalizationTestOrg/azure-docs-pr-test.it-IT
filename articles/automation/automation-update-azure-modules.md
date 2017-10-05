---
title: Aggiornare i moduli di Azure in Automazione di Azure | Microsoft Docs
description: "L'articolo descrive in che modo è ora possibile aggiornare i moduli di Azure PowerShell comuni disponibili per impostazione predefinita in Automazione di Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: ed8c97b642d406a05817ec6c67f31a1b4bce93b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="9373f-103">Come aggiornare i moduli di Azure PowerShell in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9373f-103">How to update Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="9373f-104">I moduli di Azure PowerShell più comuni sono forniti per impostazione predefinita in ogni account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="9373f-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="9373f-105">Il team di Azure aggiorna regolarmente i moduli di Azure. Pertanto, l'account di Automazione prevede una modalità di aggiornamento dei moduli non appena nel portale sono disponibili nuove versioni.</span><span class="sxs-lookup"><span data-stu-id="9373f-105">The Azure team updates the Azure modules regularly, so in the Automation account we provide a way for you to update the modules in the account when new versions are available from the portal.</span></span>  

<span data-ttu-id="9373f-106">Poiché i moduli vengono aggiornati regolarmente dal gruppo di prodotto, possono essere eseguite modifiche con i cmdlet inclusi, che potrebbero influire negativamente sui runbook a seconda del tipo di modifica, ad esempio ridenominando un parametro o deprecando completamente un cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9373f-106">Because modules are updated regularly by the product group, changes can occur with the  included cmdlets, which may negatively impact your runbooks depending on the type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="9373f-107">Per evitare conseguenze sui runbook e sui processi che vengono automatizzati, si consiglia di eseguire un test e di convalidare prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="9373f-107">To avoid impacting your runbooks and the processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="9373f-108">Se non si dispone di un account di automazione dedicato a questo scopo, è consigliabile crearne uno in modo da poter testare numerosi scenari e permutazioni diverse durante lo sviluppo dei runbook, oltre a poter eseguire modifiche iterative, ad esempio l'aggiornamento dei moduli PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9373f-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during the development of your runbooks, in addition to iterative changes such as updating the PowerShell modules.</span></span>  <span data-ttu-id="9373f-109">Dopo aver convalidato i risultati e applicato le modifiche necessarie, procedere con la coordinazione della migrazione di tutti i runbook modificati ed eseguire l'aggiornamento come descritto di seguito nella produzione.</span><span class="sxs-lookup"><span data-stu-id="9373f-109">After the results are validated and you have applied any changes required, proceed with coordinating the migration of any runbooks that required modification and perform the update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="9373f-110">Aggiornamento dei moduli di Azure</span><span class="sxs-lookup"><span data-stu-id="9373f-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="9373f-111">Nel pannello Moduli dell'account di Automazione è presente un'opzione denominata **Update Azure Modules** (Aggiorna i moduli di Azure).</span><span class="sxs-lookup"><span data-stu-id="9373f-111">In the Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="9373f-112">Tale opzione è sempre abilitata.</span><span class="sxs-lookup"><span data-stu-id="9373f-112">It is always enabled.</span></span><br><br> <span data-ttu-id="9373f-113">![Opzione di aggiornamento dei moduli di Azure nel pannello Moduli](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="9373f-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="9373f-114">Fare clic su **Update Azure Modules** (Aggiorna i moduli di Azure), quindi viene visualizzata una notifica di conferma dell'intenzione di continuare.</span><span class="sxs-lookup"><span data-stu-id="9373f-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want to continue.</span></span><br><br> <span data-ttu-id="9373f-115">![Notifica di aggiornamento dei moduli di Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="9373f-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="9373f-116">Fare clic su **Sì** per avviare il processo di aggiornamento del modulo.</span><span class="sxs-lookup"><span data-stu-id="9373f-116">Click **Yes** and the module update process will begin.</span></span>  <span data-ttu-id="9373f-117">Il processo richiede circa 15-20 minuti per aggiornare i seguenti moduli:</span><span class="sxs-lookup"><span data-stu-id="9373f-117">The update process takes about 15-20 minutes to update the following modules:</span></span>

  * <span data-ttu-id="9373f-118">Azure</span><span class="sxs-lookup"><span data-stu-id="9373f-118">Azure</span></span>
  * <span data-ttu-id="9373f-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="9373f-119">Azure.Storage</span></span>
  * <span data-ttu-id="9373f-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="9373f-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="9373f-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="9373f-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="9373f-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="9373f-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="9373f-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="9373f-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="9373f-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="9373f-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="9373f-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="9373f-125">AzureRm.Storage</span></span>

    <span data-ttu-id="9373f-126">Se i moduli sono già aggiornati, il processo verrà completato in pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="9373f-126">If the modules are already up to date, then the process will complete in a few seconds.</span></span>  <span data-ttu-id="9373f-127">Al termine del processo di aggiornamento si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="9373f-127">When the update process completes you will be notified.</span></span><br><br> ![Stato di aggiornamento dei moduli di Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="9373f-129">Quando viene eseguito un nuovo processo pianificato, Automazione di Azure utilizzerà i moduli più recenti nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="9373f-129">Azure Automation will use the latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="9373f-130">Se si usano i cmdlet di questi moduli di Azure PowerShell nei runbook per gestire le risorse di Azure, si potrebbe voler eseguire il processo di aggiornamento all'incirca ogni mese per assicurarsi di disporre dei moduli più recenti.</span><span class="sxs-lookup"><span data-stu-id="9373f-130">If you use cmdlets from these Azure PowerShell modules in your runbooks to manage Azure resources, then you will want to perform this update process every month or so to assure that you have the latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9373f-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9373f-131">Next steps</span></span>

* <span data-ttu-id="9373f-132">Per maggiori informazioni sui moduli di integrazione e sulla creazione di moduli personalizzati per l'ulteriore integrazione di Automazione con altri sistemi, servizi o soluzioni, vedere [Moduli di integrazione](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="9373f-132">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="9373f-133">Valutare la possibilità di utilizzare l’integrazione del controllo del codice sorgente tramite [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) o [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) per gestire e controllare le versioni del portfolio di configurazione e del runbook di automazione.</span><span class="sxs-lookup"><span data-stu-id="9373f-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) to centrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  