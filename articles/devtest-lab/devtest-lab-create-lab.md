---
title: un laboratorio di Azure DevTest Labs aaaCreate | Documenti Microsoft
description: Creare un lab in Azure DevTest Labs per macchine virtuali
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="d55a9-103">Creare un lab di sviluppo/test di Azure</span><span class="sxs-lookup"><span data-stu-id="d55a9-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="d55a9-104">Un laboratorio di Azure DevTest Labs è infrastruttura hello che comprende un gruppo di risorse, ad esempio macchine virtuali (VM), che consente una migliore gestione di tali risorse specificando i limiti e quote.</span><span class="sxs-lookup"><span data-stu-id="d55a9-104">A lab in Azure DevTest Labs is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="d55a9-105">In questo articolo illustra hello processo di creazione di un ambiente lab tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d55a9-105">This article walks you through hello process of creating a lab using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d55a9-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d55a9-106">Prerequisites</span></span>
<span data-ttu-id="d55a9-107">toocreate un ambiente lab, è necessario:</span><span class="sxs-lookup"><span data-stu-id="d55a9-107">toocreate a lab, you need:</span></span>

* <span data-ttu-id="d55a9-108">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d55a9-108">An Azure subscription.</span></span> <span data-ttu-id="d55a9-109">toolearn sulle opzioni di acquisto di Azure, vedere [come toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) o [la versione di un mese valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d55a9-109">toolearn about Azure purchase options, see [How toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="d55a9-110">È necessario essere proprietari di hello lab hello toocreate di hello sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d55a9-110">You must be hello owner of hello subscription toocreate hello lab.</span></span>

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="d55a9-111">Passaggi toocreate un laboratorio di Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="d55a9-111">Steps toocreate a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="d55a9-112">Hello alla procedura seguente viene illustrato come toouse hello toocreate portale Azure un laboratorio di DevTest Labs di Azure.</span><span class="sxs-lookup"><span data-stu-id="d55a9-112">hello following steps illustrate how toouse hello Azure portal toocreate a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="d55a9-113">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d55a9-113">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="d55a9-114">Dal menu principale di hello sul lato sinistro di hello, selezionare **più servizi** (nella parte inferiore di hello dell'elenco di hello).</span><span class="sxs-lookup"><span data-stu-id="d55a9-114">From hello main menu on hello left side, select **More Services** (at hello bottom of hello list).</span></span>

    ![Opzione di menu Altri servizi](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="d55a9-116">Dall'elenco di hello dei servizi disponibili, **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-116">From hello list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="d55a9-117">In hello **DevTest Labs** pannello seleziona **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-117">On hello **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Aggiungere un lab](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="d55a9-119">In hello **creare un laboratorio di DevTest** pannello:</span><span class="sxs-lookup"><span data-stu-id="d55a9-119">On hello **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="d55a9-120">Immettere un **nome Lab** per lab nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="d55a9-120">Enter a **Lab Name** for hello new lab.</span></span>
    2. <span data-ttu-id="d55a9-121">Seleziona hello **sottoscrizione** tooassociate con lab hello.</span><span class="sxs-lookup"><span data-stu-id="d55a9-121">Select hello **Subscription** tooassociate with hello lab.</span></span>
    3. <span data-ttu-id="d55a9-122">Selezionare un **percorso** in cui lab hello toostore.</span><span class="sxs-lookup"><span data-stu-id="d55a9-122">Select a **Location** in which toostore hello lab.</span></span>
    4. <span data-ttu-id="d55a9-123">Selezionare **arresto automatici** toospecify se si desidera tooenable - e definire parametri hello - hello automatica in corso l'arresto delle macchine virtuali del laboratorio di hello tutti.</span><span class="sxs-lookup"><span data-stu-id="d55a9-123">Select **Auto-shutdown** toospecify if you want tooenable - and define hello parameters for - hello automatic shutting down of all hello lab's VMs.</span></span> <span data-ttu-id="d55a9-124">funzionalità di arresto automatici Hello è essenzialmente una funzionalità di riduzione dei costi in base al quale è possibile specificare quando si desidera hello VM tooautomatically essere arrestato.</span><span class="sxs-lookup"><span data-stu-id="d55a9-124">hello auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want hello VM tooautomatically be shut down.</span></span> <span data-ttu-id="d55a9-125">È possibile modificare le impostazioni di arresto automatico dopo la creazione di lab hello seguendo i passaggi di hello descritti nell'articolo hello, [gestire tutti i criteri per un ambiente lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="d55a9-125">You can change auto-shutdown settings after creating hello lab by following hello steps outlined in hello article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="d55a9-126">Selezionare **tooDashboard Pin** se si desidera creare un collegamento di hello lab tooappear nel dashboard del portale hello.</span><span class="sxs-lookup"><span data-stu-id="d55a9-126">Select **Pin tooDashboard** if you want a shortcut of hello lab tooappear on hello portal dashboard.</span></span>
    6. <span data-ttu-id="d55a9-127">Selezionare **opzioni di automazione** tooget modelli di gestione risorse di Azure per l'automazione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="d55a9-127">Select **Automation options** tooget Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="d55a9-128">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d55a9-128">Select **Create**.</span></span> <span data-ttu-id="d55a9-129">Dopo aver selezionato **crea**, hello **DevTest Labs** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="d55a9-129">After selecting **Create**, hello **DevTest Labs** blade displays.</span></span> <span data-ttu-id="d55a9-130">È possibile monitorare lo stato di hello del processo di creazione di hello lab, è possibile guardare hello **notifiche** area.</span><span class="sxs-lookup"><span data-stu-id="d55a9-130">You can monitor hello status of hello lab creation process by watching hello **Notifications** area.</span></span> <span data-ttu-id="d55a9-131">Una volta completato, aggiornamento hello pagina toosee hello creato appena lab nell'elenco di hello del lab.</span><span class="sxs-lookup"><span data-stu-id="d55a9-131">Once completed, refresh hello page toosee hello newly created lab in hello list of labs.</span></span>  
    
    ![Creare un pannello lab](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="d55a9-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d55a9-133">Next steps</span></span>
<span data-ttu-id="d55a9-134">Dopo aver creato l'ambiente lab, ecco alcuni tooconsider passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="d55a9-134">Once you've created your lab, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="d55a9-135">[Lab tooa accesso sicuro](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="d55a9-135">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="d55a9-136">[Definire i criteri del lab](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d55a9-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="d55a9-137">[Creare un modello di lab](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="d55a9-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="d55a9-138">[Creare elementi personalizzati per le VM](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="d55a9-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="d55a9-139">[Aggiungere una macchina virtuale con lab tooa elementi](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="d55a9-139">[Add a VM with artifacts tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

