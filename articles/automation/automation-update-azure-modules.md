---
title: aaaUpdate Azure i moduli in automazione di Azure | Documenti Microsoft
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
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="dd391-103">Come i moduli di Azure PowerShell tooupdate in automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="dd391-103">How tooupdate Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="dd391-104">i moduli di PowerShell di Azure più comuni di Hello vengono forniti per impostazione predefinita in ogni account di automazione.</span><span class="sxs-lookup"><span data-stu-id="dd391-104">hello most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="dd391-105">gli aggiornamenti di Azure team Hello hello moduli di Azure regolarmente, pertanto nell'account di automazione hello è fornire un modo per si moduli hello tooupdate nell'account hello quando sono disponibili dal portale hello nuove versioni.</span><span class="sxs-lookup"><span data-stu-id="dd391-105">hello Azure team updates hello Azure modules regularly, so in hello Automation account we provide a way for you tooupdate hello modules in hello account when new versions are available from hello portal.</span></span>  

<span data-ttu-id="dd391-106">Poiché i moduli vengono aggiornati regolarmente per gruppo di prodotti hello, possono verificarsi modifiche con hello incluso cmdlet, che potrebbe compromettere i runbook in base al tipo di hello di modifica, ad esempio la ridenominazione di un parametro o deprecazione di un cmdlet completamente.</span><span class="sxs-lookup"><span data-stu-id="dd391-106">Because modules are updated regularly by hello product group, changes can occur with hello  included cmdlets, which may negatively impact your runbooks depending on hello type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="dd391-107">conseguenze per i runbook e hello tooavoid processi automatizzare, si consiglia di testare e convalidare prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="dd391-107">tooavoid impacting your runbooks and hello processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="dd391-108">Se non si dispone di un account di automazione dedicato a questo scopo, è consigliabile creare uno in modo da poter testare numerosi scenari diversi e permutazioni durante lo sviluppo di hello i runbook, le modifiche tooiterative aggiunta, come l'aggiornamento di hello Moduli di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd391-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during hello development of your runbooks, in addition tooiterative changes such as updating hello PowerShell modules.</span></span>  <span data-ttu-id="dd391-109">Dopo aver applicato le modifiche necessarie vengono convalidati i risultati di hello e procedere con il coordinamento di migrazione hello di tutti i runbook che hanno richiesto la modifica ed eseguire l'aggiornamento hello come descritto di seguito in produzione.</span><span class="sxs-lookup"><span data-stu-id="dd391-109">After hello results are validated and you have applied any changes required, proceed with coordinating hello migration of any runbooks that required modification and perform hello update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="dd391-110">Aggiornamento dei moduli di Azure</span><span class="sxs-lookup"><span data-stu-id="dd391-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="dd391-111">Nei moduli hello pannello dell'account di automazione sono è un'opzione denominata **i moduli di Azure Update**.</span><span class="sxs-lookup"><span data-stu-id="dd391-111">In hello Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="dd391-112">Tale opzione è sempre abilitata.</span><span class="sxs-lookup"><span data-stu-id="dd391-112">It is always enabled.</span></span><br><br> <span data-ttu-id="dd391-113">![Opzione di aggiornamento dei moduli di Azure nel pannello Moduli](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="dd391-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="dd391-114">Fare clic su **i moduli di Azure Update** e verrà visualizzata una notifica di conferma in cui viene chiesto se si desidera toocontinue.</span><span class="sxs-lookup"><span data-stu-id="dd391-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want toocontinue.</span></span><br><br> <span data-ttu-id="dd391-115">![Notifica di aggiornamento dei moduli di Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="dd391-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="dd391-116">Fare clic su **Sì** e processo di aggiornamento del modulo hello avrà inizio.</span><span class="sxs-lookup"><span data-stu-id="dd391-116">Click **Yes** and hello module update process will begin.</span></span>  <span data-ttu-id="dd391-117">il processo di aggiornamento Hello richiede circa hello tooupdate 15-20 minuti seguenti moduli:</span><span class="sxs-lookup"><span data-stu-id="dd391-117">hello update process takes about 15-20 minutes tooupdate hello following modules:</span></span>

  * <span data-ttu-id="dd391-118">Azure</span><span class="sxs-lookup"><span data-stu-id="dd391-118">Azure</span></span>
  * <span data-ttu-id="dd391-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="dd391-119">Azure.Storage</span></span>
  * <span data-ttu-id="dd391-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="dd391-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="dd391-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="dd391-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="dd391-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="dd391-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="dd391-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="dd391-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="dd391-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="dd391-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="dd391-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="dd391-125">AzureRm.Storage</span></span>

    <span data-ttu-id="dd391-126">Se i moduli di hello sono già backup toodate, processo hello verrà completata in pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="dd391-126">If hello modules are already up toodate, then hello process will complete in a few seconds.</span></span>  <span data-ttu-id="dd391-127">Dopo aver completato il processo di aggiornamento hello si riceverà la notifica.</span><span class="sxs-lookup"><span data-stu-id="dd391-127">When hello update process completes you will be notified.</span></span><br><br> ![Stato di aggiornamento dei moduli di Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="dd391-129">Quando viene eseguito un nuovo processo pianificato, automazione di Azure utilizzerà i moduli più recenti di hello nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="dd391-129">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="dd391-130">Se si utilizzano i cmdlet da questi moduli PowerShell di Azure nel toomanage runbook Azure le risorse, quindi si desidererà tooperform questo processo di aggiornamento ogni mese o così tooassure che è necessario hello moduli più recenti.</span><span class="sxs-lookup"><span data-stu-id="dd391-130">If you use cmdlets from these Azure PowerShell modules in your runbooks toomanage Azure resources, then you will want tooperform this update process every month or so tooassure that you have hello latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd391-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd391-131">Next steps</span></span>

* <span data-ttu-id="dd391-132">toolearn ulteriori informazioni sui moduli di integrazione e come toocreate moduli personalizzati toofurther integrare automazione con altri sistemi, servizi o soluzioni, vedere [moduli di integrazione](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="dd391-132">toolearn more about Integration Modules and how toocreate custom modules toofurther integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="dd391-133">Considerare l'utilizzo di integrazione controllo origine [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) o [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally gestire e controllare le versioni del portafoglio automazione di runbook e la configurazione.</span><span class="sxs-lookup"><span data-stu-id="dd391-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  
