---
title: criteri di lab aaaManage in Azure DevTest Labs | Documenti Microsoft
description: Informazioni su come criteri di lab toodefine, ad esempio macchine Virtuali con dimensioni, massime macchine virtuali per utente e l'automazione di arresto.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="38b5b-103">Gestire tutti i criteri per un lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="38b5b-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="38b5b-104">Azure DevTest Labs consente di gestire i criteri (impostazioni) in ogni lab, in modo da controllare i costi e ridurre al minimo gli sprechi.</span><span class="sxs-lookup"><span data-stu-id="38b5b-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="38b5b-105">In questo articolo illustra in dettaglio dettagliata come tooset tutti i criteri.</span><span class="sxs-lookup"><span data-stu-id="38b5b-105">This article explains in step-by-step detail how tooset each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="38b5b-106">Impostazione delle dimensioni consentite per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="38b5b-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="38b5b-107">Hello criteri per hello impostazione consentito dimensioni delle macchine Virtuali consente toominimize lab rifiuti abilitando toospecify sono consentite le dimensioni delle macchine Virtuali nel lab hello.</span><span class="sxs-lookup"><span data-stu-id="38b5b-107">hello policy for setting hello allowed VM sizes helps toominimize lab waste by enabling you toospecify which VM sizes are allowed in hello lab.</span></span> <span data-ttu-id="38b5b-108">Se questo criterio è attivato, solo le dimensioni di macchina virtuale da questo elenco possono essere macchine virtuali toocreate utilizzato.</span><span class="sxs-lookup"><span data-stu-id="38b5b-108">If this policy is activated, only VM sizes from this list can be used toocreate VMs.</span></span>

1. <span data-ttu-id="38b5b-109">Nel lab di hello **criteri di configurazione e** pannello seleziona **dimensioni delle macchine virtuali è consentita**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-109">On hello lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Dimensioni consentite per le macchine virtuali](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="38b5b-111">Selezionare **su** tooenable questo criterio, e **Off** toodisable è.</span><span class="sxs-lookup"><span data-stu-id="38b5b-111">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="38b5b-112">Se si abilitano questi criteri, selezionare una o più dimensioni per definire quali possono essere usate per creare macchine virtuali nel lab.</span><span class="sxs-lookup"><span data-stu-id="38b5b-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="38b5b-113">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="38b5b-114">Impostazione delle macchine virtuali per utente</span><span class="sxs-lookup"><span data-stu-id="38b5b-114">Set virtual machines per user</span></span>
<span data-ttu-id="38b5b-115">criteri per Hello **macchine virtuali per utente** consente un numero massimo di hello toospecify delle macchine virtuali che possono essere creati da un singolo utente.</span><span class="sxs-lookup"><span data-stu-id="38b5b-115">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="38b5b-116">Se un utente tenta di toocreate o attestazione basata su una macchina virtuale quando è stato raggiunto il limite di utenti di hello, un messaggio di errore indica che hello che macchina virtuale non può essere creato/richiesta.</span><span class="sxs-lookup"><span data-stu-id="38b5b-116">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="38b5b-117">Nel lab di hello **criteri di configurazione e** dal menu **macchine virtuali per utente**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-117">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Macchine virtuali per utente](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="38b5b-119">Selezionare **Sì** toolimit hello numerose macchine virtuali per utente.</span><span class="sxs-lookup"><span data-stu-id="38b5b-119">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="38b5b-120">Se non si desidera toolimit hello numerose macchine virtuali per utente, selezionare **n**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-120">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="38b5b-121">Se si seleziona **Sì**, immettere un valore numerico che indica il numero massimo di hello di macchine virtuali che può essere creato o richiesto da un utente.</span><span class="sxs-lookup"><span data-stu-id="38b5b-121">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="38b5b-122">Selezionare **Sì** numero hello toolimit di macchine virtuali che è possibile utilizzare unità SSD (disco SSD).</span><span class="sxs-lookup"><span data-stu-id="38b5b-122">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="38b5b-123">Se non si desidera numero hello toolimit di macchine virtuali che è possibile utilizzare unità SSD, selezionare **n**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-123">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="38b5b-124">Se si seleziona **Sì**, immettere un valore che indica il numero massimo di hello di macchine virtuali che possono essere creati utilizzando unità SSD.</span><span class="sxs-lookup"><span data-stu-id="38b5b-124">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="38b5b-125">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="38b5b-126">Impostazione delle macchine virtuali per lab</span><span class="sxs-lookup"><span data-stu-id="38b5b-126">Set virtual machines per lab</span></span>
<span data-ttu-id="38b5b-127">criteri per Hello **macchine virtuali per lab** consente numero massimo di hello toospecify delle macchine virtuali che possono essere creati per il lab di hello corrente.</span><span class="sxs-lookup"><span data-stu-id="38b5b-127">hello policy for **Virtual machines per lab** allows you toospecify hello maximum number of VMs that can be created for hello current lab.</span></span> <span data-ttu-id="38b5b-128">Se un utente tenta di toocreate una macchina virtuale quando è stato raggiunto il limite di lab hello, un messaggio di errore indica che hello che macchina virtuale non può essere creata.</span><span class="sxs-lookup"><span data-stu-id="38b5b-128">If a user attempts toocreate a VM when hello lab limit has been met, an error message indicates that hello VM cannot be created.</span></span> 

1. <span data-ttu-id="38b5b-129">Nel lab di hello **criteri di configurazione e** dal menu **macchine virtuali per lab**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-129">On hello lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Macchine virtuali per lab](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="38b5b-131">Selezionare **Sì** toolimit un numero di hello di macchine virtuali per lab.</span><span class="sxs-lookup"><span data-stu-id="38b5b-131">Select **Yes** toolimit hello number of VMs per lab.</span></span> <span data-ttu-id="38b5b-132">Se non si desidera toolimit un numero di hello di macchine virtuali per lab, selezionare **n**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-132">If you do not want toolimit hello number of VMs per lab, select **No**.</span></span> <span data-ttu-id="38b5b-133">Se si seleziona **Sì**, immettere un valore numerico che indica il numero massimo di hello di macchine virtuali che può essere creato o richiesto da un utente.</span><span class="sxs-lookup"><span data-stu-id="38b5b-133">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="38b5b-134">Selezionare **Sì** numero hello toolimit di macchine virtuali che è possibile utilizzare unità SSD (disco SSD).</span><span class="sxs-lookup"><span data-stu-id="38b5b-134">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="38b5b-135">Se non si desidera numero hello toolimit di macchine virtuali che è possibile utilizzare unità SSD, selezionare **n**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-135">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="38b5b-136">Se si seleziona **Sì**, immettere un valore che indica il numero massimo di hello di macchine virtuali che possono essere creati utilizzando unità SSD.</span><span class="sxs-lookup"><span data-stu-id="38b5b-136">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="38b5b-137">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="38b5b-138">Impostazione dell'arresto automatico</span><span class="sxs-lookup"><span data-stu-id="38b5b-138">Set auto-shutdown</span></span>
<span data-ttu-id="38b5b-139">criteri di arresto automatici Hello consente toominimize lab rifiuti consentono ora di hello toospecify arrestare le macchine virtuali dell'ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="38b5b-139">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="38b5b-140">Nel lab di hello **criteri di configurazione e** pannello seleziona **arresto automatici**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-140">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Arresto automatico](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="38b5b-142">Selezionare **su** tooenable questo criterio, e **Off** toodisable è.</span><span class="sxs-lookup"><span data-stu-id="38b5b-142">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="38b5b-143">Se si abilita questo criterio, è possibile specificare tooshut (ora e fuso orario) di hello verso il basso tutte le macchine virtuali nel lab corrente hello.</span><span class="sxs-lookup"><span data-stu-id="38b5b-143">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="38b5b-144">Specificare **Sì** o **n** per hello opzione toosend un toohello precedente 15 minuti di notifica specificato il tempo di arresto automatici.</span><span class="sxs-lookup"><span data-stu-id="38b5b-144">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="38b5b-145">Se si specifica **Sì**, immettere una notifica di hello webhook URL endpoint tooreceive.</span><span class="sxs-lookup"><span data-stu-id="38b5b-145">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="38b5b-146">Per altre informazioni sui webhook, vedere [Creare un webhook o una funzione API di Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="38b5b-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="38b5b-147">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-147">Select **Save**.</span></span>

    <span data-ttu-id="38b5b-148">Per impostazione predefinita, una volta abilitato, questi criteri si applicano tooall macchine virtuali nel lab corrente hello.</span><span class="sxs-lookup"><span data-stu-id="38b5b-148">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="38b5b-149">tooremove questa impostazione di una macchina virtuale specifica, aprire Pannello hello della macchina virtuale e modificare il relativo **arresto automatici** impostazione</span><span class="sxs-lookup"><span data-stu-id="38b5b-149">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="38b5b-150">Impostazione dell'avvio automatico</span><span class="sxs-lookup"><span data-stu-id="38b5b-150">Set auto-start</span></span>
<span data-ttu-id="38b5b-151">criteri di avvio automatico di Hello consentono toospecify quando hello macchine virtuali nel lab corrente hello deve essere avviato.</span><span class="sxs-lookup"><span data-stu-id="38b5b-151">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="38b5b-152">Nel lab di hello **criteri di configurazione e** pannello seleziona **avvio automatico**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-152">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Avvio automatico](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="38b5b-154">Selezionare **su** tooenable questo criterio, e **Off** toodisable è.</span><span class="sxs-lookup"><span data-stu-id="38b5b-154">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="38b5b-155">Se si abilita questo criterio, specificare l'ora di inizio pianificata hello, fuso orario e hello giorni della settimana hello per cui hello Applica ora.</span><span class="sxs-lookup"><span data-stu-id="38b5b-155">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="38b5b-156">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="38b5b-156">Select **Save**.</span></span>

    <span data-ttu-id="38b5b-157">Una volta abilitato, questo criterio non è macchine virtuali tooany applicato automaticamente nel lab corrente hello.</span><span class="sxs-lookup"><span data-stu-id="38b5b-157">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="38b5b-158">tooapply tooa questa impostazione macchina virtuale specifica, della macchina virtuale aprire hello blade e modificare il relativo **avvio automatico** impostazione</span><span class="sxs-lookup"><span data-stu-id="38b5b-158">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="38b5b-159">Impostare la data di scadenza</span><span class="sxs-lookup"><span data-stu-id="38b5b-159">Set expiration date</span></span>
<span data-ttu-id="38b5b-160">È possibile impostare la scadenza della data è [creare hello VM](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="38b5b-160">You can set an expiration date when you [create hello VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="38b5b-161">In **impostazioni avanzate**, scegliere toospecify icona di calendario hello una data in cui hello VM verrà eliminata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="38b5b-161">In **Advanced settings**, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="38b5b-162">Per impostazione predefinita, hello VM non ha scadenza.</span><span class="sxs-lookup"><span data-stu-id="38b5b-162">By default, hello VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="38b5b-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38b5b-163">Next steps</span></span>
<span data-ttu-id="38b5b-164">Dopo aver definito e applicato hello diverse impostazioni di criteri di macchina virtuale per l'ambiente lab, ecco alcuni aspetti tootry successivamente:</span><span class="sxs-lookup"><span data-stu-id="38b5b-164">Once you've defined and applied hello various VM policy settings for your lab, here are some things tootry next:</span></span>

* <span data-ttu-id="38b5b-165">[Comprendere gli indirizzi IP condivisi](devtest-lab-shared-ip.md) -illustra come condiviso IP vengono utilizzati indirizzi in numero di hello toominimize DevTest Labs pubblica IP indirizzi necessari tooconnect tooyour lab di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="38b5b-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs toominimize hello number of public IP addresses required tooconnect tooyour lab VMs.</span></span>
* <span data-ttu-id="38b5b-166">[Configurare la gestione dei costi](devtest-lab-configure-cost-management.md) -illustra come hello toouse **tendenza mensile del costo stimato** grafico</span><span class="sxs-lookup"><span data-stu-id="38b5b-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how toouse hello **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="38b5b-167">tooview hello stimato costo-to-date del mese corrente e i costi di fine mese hello proiettato.</span><span class="sxs-lookup"><span data-stu-id="38b5b-167">tooview hello current month's estimated cost-to-date and hello projected end-of-month cost.</span></span>
* <span data-ttu-id="38b5b-168">[Creare un'immagine personalizzata](devtest-lab-create-template.md): quando si crea una VM, si specifica una base, che può essere un'immagine personalizzata o un'immagine del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="38b5b-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="38b5b-169">Questo articolo illustra come toocreate immagine personalizzata da un file VHD.</span><span class="sxs-lookup"><span data-stu-id="38b5b-169">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="38b5b-170">[Configurare immagini del Marketplace](devtest-lab-configure-marketplace-images.md): Azure DevTest Labs supporta la creazione di VM basate su immagini di Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="38b5b-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="38b5b-171">Questo articolo illustra come toospecify che, se presente, le immagini di Azure Marketplace possono essere utilizzati durante la creazione di macchine virtuali in un ambiente lab.</span><span class="sxs-lookup"><span data-stu-id="38b5b-171">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="38b5b-172">[Creare una macchina virtuale in un ambiente lab](devtest-lab-add-vm-with-artifacts.md) -illustra come toocreate una macchina virtuale da un'immagine di base (entrambi personalizzato o Marketplace) e come toowork con gli elementi di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="38b5b-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

