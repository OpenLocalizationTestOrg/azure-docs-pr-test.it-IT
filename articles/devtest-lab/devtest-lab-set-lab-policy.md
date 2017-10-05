---
title: Gestire i criteri di lab in Azure DevTest Labs| Microsoft Docs
description: Informazioni su come definire i criteri del lab, ad esempio per le dimensioni delle macchine virtuali, il numero massimo di macchine virtuali per ogni utente e l'arresto automatico.
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
ms.openlocfilehash: 328a4d893637d7150807855e118b485a2c3bbfc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="fafb0-103">Gestire tutti i criteri per un lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="fafb0-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="fafb0-104">Azure DevTest Labs consente di gestire i criteri (impostazioni) in ogni lab, in modo da controllare i costi e ridurre al minimo gli sprechi.</span><span class="sxs-lookup"><span data-stu-id="fafb0-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="fafb0-105">In questo articolo viene illustrato in modo dettagliato come impostare ogni criterio.</span><span class="sxs-lookup"><span data-stu-id="fafb0-105">This article explains in step-by-step detail how to set each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="fafb0-106">Impostazione delle dimensioni consentite per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="fafb0-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="fafb0-107">I criteri per l'impostazione delle dimensioni consentite per le macchine virtuali permettono di ridurre al minimo gli sprechi specificando le dimensioni consentite per le macchine virtuali nel lab.</span><span class="sxs-lookup"><span data-stu-id="fafb0-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span></span> <span data-ttu-id="fafb0-108">Se questi criteri sono attivati, per la creazione di macchine virtuali è possibile utilizzare solo le dimensioni selezionate da questo elenco.</span><span class="sxs-lookup"><span data-stu-id="fafb0-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span></span>

1. <span data-ttu-id="fafb0-109">Nel pannello **Configuration and policies** (Configurazione e criteri) del lab selezionare **Allowed virtual machines sizes** (Dimensioni consentite per le macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="fafb0-109">On the lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Dimensioni consentite per le macchine virtuali](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="fafb0-111">Selezionare **Attivo** per abilitare i criteri e **Non attivo** per disabilitarli.</span><span class="sxs-lookup"><span data-stu-id="fafb0-111">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="fafb0-112">Se si abilitano questi criteri, selezionare una o più dimensioni per definire quali possono essere usate per creare macchine virtuali nel lab.</span><span class="sxs-lookup"><span data-stu-id="fafb0-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="fafb0-113">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fafb0-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="fafb0-114">Impostazione delle macchine virtuali per utente</span><span class="sxs-lookup"><span data-stu-id="fafb0-114">Set virtual machines per user</span></span>
<span data-ttu-id="fafb0-115">I criteri per **Macchine virtuali per utente** consentono di specificare il numero massimo di VM che possono essere create da un singolo utente.</span><span class="sxs-lookup"><span data-stu-id="fafb0-115">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="fafb0-116">Se un utente prova a creare o attestare una macchina virtuale quando è stato raggiunto il limite per utente, un messaggio di errore indica che non è possibile creare o attestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fafb0-116">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="fafb0-117">Dal menu **Configuration and policies** (Configurazione e criteri) del lab selezionare **Virtual machines per user** (Macchine virtuali per utente).</span><span class="sxs-lookup"><span data-stu-id="fafb0-117">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Macchine virtuali per utente](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="fafb0-119">Selezionare **Sì** per limitare il numero di macchine virtuali per utente.</span><span class="sxs-lookup"><span data-stu-id="fafb0-119">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="fafb0-120">Se non si desidera limitare il numero di macchine virtuali per utente, selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="fafb0-120">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="fafb0-121">Se si seleziona **Sì**, immettere un valore numerico per indicare il numero massimo di macchine virtuali che un utente può creare o attestare.</span><span class="sxs-lookup"><span data-stu-id="fafb0-121">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="fafb0-122">Selezionare **Sì** per limitare il numero di macchine virtuali che possono usare unità SSD.</span><span class="sxs-lookup"><span data-stu-id="fafb0-122">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="fafb0-123">Se non si desidera limitare il numero di macchine virtuali che possono usare unità SSD, selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="fafb0-123">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="fafb0-124">Se si seleziona **Sì**, immettere un valore numerico per indicare il numero massimo di macchine virtuali che possono essere create usando unità SSD.</span><span class="sxs-lookup"><span data-stu-id="fafb0-124">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="fafb0-125">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fafb0-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="fafb0-126">Impostazione delle macchine virtuali per lab</span><span class="sxs-lookup"><span data-stu-id="fafb0-126">Set virtual machines per lab</span></span>
<span data-ttu-id="fafb0-127">I criteri per **Macchine virtuali per lab** consentono di specificare il numero massimo di VM che è possibile creare per il lab corrente.</span><span class="sxs-lookup"><span data-stu-id="fafb0-127">The policy for **Virtual machines per lab** allows you to specify the maximum number of VMs that can be created for the current lab.</span></span> <span data-ttu-id="fafb0-128">Se un utente prova a creare una VM quando è stato raggiunto il limite per lab, un messaggio di errore indica che non è possibile creare la VM.</span><span class="sxs-lookup"><span data-stu-id="fafb0-128">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span></span> 

1. <span data-ttu-id="fafb0-129">Dal menu **Configuration and policies** del lab selezionare **Virtual machines per lab** (Macchine virtuali per lab).</span><span class="sxs-lookup"><span data-stu-id="fafb0-129">On the lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Macchine virtuali per lab](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="fafb0-131">Selezionare **Sì** per limitare il numero di macchine virtuali per lab.</span><span class="sxs-lookup"><span data-stu-id="fafb0-131">Select **Yes** to limit the number of VMs per lab.</span></span> <span data-ttu-id="fafb0-132">Se non si desidera limitare il numero di macchine virtuali per lab, selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="fafb0-132">If you do not want to limit the number of VMs per lab, select **No**.</span></span> <span data-ttu-id="fafb0-133">Se si seleziona **Sì**, immettere un valore numerico per indicare il numero massimo di macchine virtuali che un utente può creare o attestare.</span><span class="sxs-lookup"><span data-stu-id="fafb0-133">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="fafb0-134">Selezionare **Sì** per limitare il numero di macchine virtuali che possono usare unità SSD.</span><span class="sxs-lookup"><span data-stu-id="fafb0-134">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="fafb0-135">Se non si desidera limitare il numero di macchine virtuali che possono usare unità SSD, selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="fafb0-135">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="fafb0-136">Se si seleziona **Sì**, immettere un valore numerico per indicare il numero massimo di macchine virtuali che possono essere create usando unità SSD.</span><span class="sxs-lookup"><span data-stu-id="fafb0-136">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="fafb0-137">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fafb0-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="fafb0-138">Impostazione dell'arresto automatico</span><span class="sxs-lookup"><span data-stu-id="fafb0-138">Set auto-shutdown</span></span>
<span data-ttu-id="fafb0-139">I criteri di arresto automatico consentono di ridurre al minimo gli sprechi nel lab permettendo di specificare l'ora dell'arresto delle macchine virtuali del lab.</span><span class="sxs-lookup"><span data-stu-id="fafb0-139">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="fafb0-140">Nel pannello **Configuration and policies** (Configurazione e criteri) del lab selezionare **Arresto automatico**.</span><span class="sxs-lookup"><span data-stu-id="fafb0-140">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Arresto automatico](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="fafb0-142">Selezionare **Attivo** per abilitare i criteri e **Non attivo** per disabilitarli.</span><span class="sxs-lookup"><span data-stu-id="fafb0-142">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="fafb0-143">Se si abilita questo criterio, specificare l'ora e il fuso orario per l'arresto di tutte le macchine virtuali nel lab attuale.</span><span class="sxs-lookup"><span data-stu-id="fafb0-143">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="fafb0-144">Specificare **Sì** o **No** per questa opzione per inviare una notifica 15 minuti prima del momento specificato per l'arresto automatico.</span><span class="sxs-lookup"><span data-stu-id="fafb0-144">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="fafb0-145">Se si specifica **Sì**, immettere un endpoint dell'URL webhook per ricevere la notifica.</span><span class="sxs-lookup"><span data-stu-id="fafb0-145">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="fafb0-146">Per altre informazioni sui webhook, vedere [Creare un webhook o una funzione API di Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="fafb0-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="fafb0-147">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fafb0-147">Select **Save**.</span></span>

    <span data-ttu-id="fafb0-148">Per impostazione predefinita, dopo l'abilitazione questi criteri verranno applicati a tutte le macchine virtuali nel lab corrente.</span><span class="sxs-lookup"><span data-stu-id="fafb0-148">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="fafb0-149">Per rimuovere questa impostazione da una VM specifica, aprire il pannello della VM e modificare l'impostazione **Arresto automatico** .</span><span class="sxs-lookup"><span data-stu-id="fafb0-149">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="fafb0-150">Impostazione dell'avvio automatico</span><span class="sxs-lookup"><span data-stu-id="fafb0-150">Set auto-start</span></span>
<span data-ttu-id="fafb0-151">I criteri di avvio automatico consentono di specificare l'ora in cui devono essere avviate le macchine virtuali nel lab corrente.</span><span class="sxs-lookup"><span data-stu-id="fafb0-151">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="fafb0-152">Dal pannello **Configuration and policies** (Configurazione e criteri) del lab selezionare **Avvio automatico**.</span><span class="sxs-lookup"><span data-stu-id="fafb0-152">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Avvio automatico](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="fafb0-154">Selezionare **Attivo** per abilitare i criteri e **Non attivo** per disabilitarli.</span><span class="sxs-lookup"><span data-stu-id="fafb0-154">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="fafb0-155">Se si abilita questo criterio, specificare l'ora di avvio pianificata, il fuso orario e i giorni della settimana a cui è applicabile questo orario.</span><span class="sxs-lookup"><span data-stu-id="fafb0-155">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="fafb0-156">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fafb0-156">Select **Save**.</span></span>

    <span data-ttu-id="fafb0-157">Dopo l'abilitazione, questi criteri non vengono applicati automaticamente alle VM del lab corrente.</span><span class="sxs-lookup"><span data-stu-id="fafb0-157">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="fafb0-158">Per applicare questa impostazione a una VM specifica, aprire il pannello della VM e modificare l'impostazione **Avvio automatico** .</span><span class="sxs-lookup"><span data-stu-id="fafb0-158">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="fafb0-159">Impostare la data di scadenza</span><span class="sxs-lookup"><span data-stu-id="fafb0-159">Set expiration date</span></span>
<span data-ttu-id="fafb0-160">È possibile impostare una data di scadenza quando si [crea la macchina virtuale](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="fafb0-160">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="fafb0-161">In **Impostazioni avanzate** scegliere l'icona del calendario per specificare una data in cui la macchina virtuale verrà eliminata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fafb0-161">In **Advanced settings**, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="fafb0-162">Per impostazione predefinita, la macchina virtuale non scadrà.</span><span class="sxs-lookup"><span data-stu-id="fafb0-162">By default, the VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="fafb0-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fafb0-163">Next steps</span></span>
<span data-ttu-id="fafb0-164">Dopo avere definito e applicato i diversi criteri per le VM per il lab, è possibile eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fafb0-164">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span></span>

* <span data-ttu-id="fafb0-165">[Understand shared IP addresses ](devtest-lab-shared-ip.md) (Comprendere gli indirizzi IP condivisi) - Illustra come vengono usati gli indirizzi IP condivisi in DevTest Labs per ridurre al minimo il numero di indirizzi IP pubblici necessari per connettersi a macchine virtuali nel lab.</span><span class="sxs-lookup"><span data-stu-id="fafb0-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span></span>
* <span data-ttu-id="fafb0-166">[Configurare la gestione dei costi](devtest-lab-configure-cost-management.md): viene illustrato come usare il grafico **Tendenza dei costi mensili stimati**</span><span class="sxs-lookup"><span data-stu-id="fafb0-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="fafb0-167">per visualizzare il costo stimato per il mese in corso fino alla data odierna e il costo stimato per la fine del mese.</span><span class="sxs-lookup"><span data-stu-id="fafb0-167">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span></span>
* <span data-ttu-id="fafb0-168">[Creare un'immagine personalizzata](devtest-lab-create-template.md): quando si crea una VM, si specifica una base, che può essere un'immagine personalizzata o un'immagine del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fafb0-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="fafb0-169">Questo articolo illustra come creare un'immagine personalizzata da un file VHD.</span><span class="sxs-lookup"><span data-stu-id="fafb0-169">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="fafb0-170">[Configurare immagini del Marketplace](devtest-lab-configure-marketplace-images.md): Azure DevTest Labs supporta la creazione di VM basate su immagini di Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fafb0-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="fafb0-171">Questo articolo illustra come specificare eventuali immagini di Azure Marketplace da usare durante la creazione di VM in un lab.</span><span class="sxs-lookup"><span data-stu-id="fafb0-171">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="fafb0-172">[Creare una VM in un lab](devtest-lab-add-vm-with-artifacts.md): questo articolo illustra come creare una VM da un'immagine di base, personalizzata o del Marketplace, e come usare gli elementi nella VM.</span><span class="sxs-lookup"><span data-stu-id="fafb0-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

