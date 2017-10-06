---
title: criteri di base lab aaaManage in Azure DevTest Labs | Documenti Microsoft
description: Informazioni su come tooset alcuni criteri base hello (impostazioni) per un laboratorio di DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="378f4-103">Gestire i criteri di base di un lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="378f4-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="378f4-104">Azure DevTest Labs consente toocontrol costo e ridurre al minimo i rifiuti nei propri laboratori dalla gestione dei criteri (impostazioni) per ogni ambiente lab.</span><span class="sxs-lookup"><span data-stu-id="378f4-104">Azure DevTest Labs enables you toocontrol cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="378f4-105">In questo articolo, iniziare con i criteri da apprendere come tooset due dei criteri più critici hello - limitazione hello numero di macchine virtuali (VM) che può essere create o richiesto da un singolo utente e la configurazione automatica-arresto.</span><span class="sxs-lookup"><span data-stu-id="378f4-105">In this article, you get started with policies by learning how tooset two of hello most critical policies - limiting hello number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="378f4-106">tooview come tooset ogni criterio lab, vedere l'articolo hello, [definire criteri lab in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="378f4-106">tooview how tooset every lab policy, see hello article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="378f4-107">Accesso ai criteri di lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="378f4-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="378f4-108">Hello passaggi seguenti consentono di configurare i criteri per un ambiente lab in Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="378f4-108">hello following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="378f4-109">i criteri di hello tooview (ed eventualmente) per un ambiente lab, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="378f4-109">tooview (and change) hello policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="378f4-110">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="378f4-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="378f4-111">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="378f4-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="378f4-112">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="378f4-112">From hello list of labs, select hello desired lab.</span></span>   

1. <span data-ttu-id="378f4-113">Selezionare **Configuration and policies** (Configurazione e criteri).</span><span class="sxs-lookup"><span data-stu-id="378f4-113">Select **Configuration and policies**.</span></span>

    ![Pannello Impostazioni criteri](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="378f4-115">Hello **criteri di configurazione e** pannello contiene un menu di impostazioni che è possibile specificare.</span><span class="sxs-lookup"><span data-stu-id="378f4-115">hello **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="378f4-116">Questo articolo vengono illustrate solo le impostazioni di hello per **macchine virtuali per utente** e **arresto automatici**.</span><span class="sxs-lookup"><span data-stu-id="378f4-116">This article covers only hello settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="378f4-117">toolearn su hello rimanenti impostazioni, vedere [gestire tutti i criteri per un ambiente lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="378f4-117">toolearn about hello remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="378f4-118">Impostazione delle macchine virtuali per utente</span><span class="sxs-lookup"><span data-stu-id="378f4-118">Set virtual machines per user</span></span>
<span data-ttu-id="378f4-119">criteri per Hello **macchine virtuali per utente** consente un numero massimo di hello toospecify delle macchine virtuali che possono essere creati da un singolo utente.</span><span class="sxs-lookup"><span data-stu-id="378f4-119">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="378f4-120">Se un utente tenta di toocreate o attestazione basata su una macchina virtuale quando è stato raggiunto il limite di utenti di hello, un messaggio di errore indica che hello che macchina virtuale non può essere creato/richiesta.</span><span class="sxs-lookup"><span data-stu-id="378f4-120">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="378f4-121">Nel lab di hello **criteri di configurazione e** dal menu **macchine virtuali per utente**.</span><span class="sxs-lookup"><span data-stu-id="378f4-121">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Macchine virtuali per utente](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="378f4-123">Selezionare **Sì** toolimit hello numerose macchine virtuali per utente.</span><span class="sxs-lookup"><span data-stu-id="378f4-123">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="378f4-124">Se non si desidera toolimit hello numerose macchine virtuali per utente, selezionare **n**.</span><span class="sxs-lookup"><span data-stu-id="378f4-124">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="378f4-125">Se si seleziona **Sì**, immettere un valore numerico che indica il numero massimo di hello di macchine virtuali che può essere creato o richiesto da un utente.</span><span class="sxs-lookup"><span data-stu-id="378f4-125">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="378f4-126">Selezionare **Sì** numero hello toolimit di macchine virtuali che è possibile utilizzare unità SSD (disco SSD).</span><span class="sxs-lookup"><span data-stu-id="378f4-126">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="378f4-127">Se non si desidera numero hello toolimit di macchine virtuali che è possibile utilizzare unità SSD, selezionare **n**.</span><span class="sxs-lookup"><span data-stu-id="378f4-127">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="378f4-128">Se si seleziona **Sì**, immettere un valore che indica il numero massimo di hello di macchine virtuali che possono essere creati utilizzando unità SSD.</span><span class="sxs-lookup"><span data-stu-id="378f4-128">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="378f4-129">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="378f4-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="378f4-130">Impostazione dell'arresto automatico</span><span class="sxs-lookup"><span data-stu-id="378f4-130">Set auto-shutdown</span></span>
<span data-ttu-id="378f4-131">criteri di arresto automatici Hello consente toominimize lab rifiuti consentono ora di hello toospecify arrestare le macchine virtuali dell'ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="378f4-131">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="378f4-132">Nel lab di hello **criteri di configurazione e** pannello seleziona **arresto automatici**.</span><span class="sxs-lookup"><span data-stu-id="378f4-132">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Arresto automatico](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="378f4-134">Selezionare **su** tooenable questo criterio, e **Off** toodisable è.</span><span class="sxs-lookup"><span data-stu-id="378f4-134">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="378f4-135">Se si abilita questo criterio, è possibile specificare tooshut (ora e fuso orario) di hello verso il basso tutte le macchine virtuali nel lab corrente hello.</span><span class="sxs-lookup"><span data-stu-id="378f4-135">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="378f4-136">Specificare **Sì** o **n** per hello opzione toosend un toohello precedente 15 minuti di notifica specificato il tempo di arresto automatici.</span><span class="sxs-lookup"><span data-stu-id="378f4-136">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="378f4-137">Se si specifica **Sì**, immettere una notifica di hello webhook URL endpoint tooreceive.</span><span class="sxs-lookup"><span data-stu-id="378f4-137">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="378f4-138">Per altre informazioni sui webhook, vedere [Creare un webhook o una funzione API di Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="378f4-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="378f4-139">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="378f4-139">Select **Save**.</span></span>

    <span data-ttu-id="378f4-140">Per impostazione predefinita, una volta abilitato, questi criteri si applicano tooall macchine virtuali nel lab corrente hello.</span><span class="sxs-lookup"><span data-stu-id="378f4-140">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="378f4-141">tooremove questa impostazione di una macchina virtuale specifica, aprire Pannello hello della macchina virtuale e modificare il relativo **arresto automatici** impostazione</span><span class="sxs-lookup"><span data-stu-id="378f4-141">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="378f4-142">Impostazione dell'avvio automatico</span><span class="sxs-lookup"><span data-stu-id="378f4-142">Set auto-start</span></span>
<span data-ttu-id="378f4-143">criteri di avvio automatico di Hello consentono toospecify quando hello macchine virtuali nel lab corrente hello deve essere avviato.</span><span class="sxs-lookup"><span data-stu-id="378f4-143">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="378f4-144">Nel lab di hello **criteri di configurazione e** pannello seleziona **avvio automatico**.</span><span class="sxs-lookup"><span data-stu-id="378f4-144">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Avvio automatico](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="378f4-146">Selezionare **su** tooenable questo criterio, e **Off** toodisable è.</span><span class="sxs-lookup"><span data-stu-id="378f4-146">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="378f4-147">Se si abilita questo criterio, specificare l'ora di inizio pianificata hello, fuso orario e hello giorni della settimana hello per cui hello Applica ora.</span><span class="sxs-lookup"><span data-stu-id="378f4-147">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="378f4-148">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="378f4-148">Select **Save**.</span></span>

    <span data-ttu-id="378f4-149">Una volta abilitato, questo criterio non è macchine virtuali tooany applicato automaticamente nel lab corrente hello.</span><span class="sxs-lookup"><span data-stu-id="378f4-149">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="378f4-150">tooapply tooa questa impostazione macchina virtuale specifica, della macchina virtuale aprire hello blade e modificare il relativo **avvio automatico** impostazione</span><span class="sxs-lookup"><span data-stu-id="378f4-150">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="378f4-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="378f4-151">Next steps</span></span>

- <span data-ttu-id="378f4-152">[Definire i criteri di laboratorio in Azure DevTest Labs](devtest-lab-set-lab-policy.md) -informazioni su come toomodify altri criteri lab</span><span class="sxs-lookup"><span data-stu-id="378f4-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how toomodify other lab policies</span></span> 
