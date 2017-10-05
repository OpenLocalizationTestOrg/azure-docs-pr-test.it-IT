---
title: Gestire i criteri di base di un lab in Azure DevTest Labs| Microsoft Docs
description: Come configurare alcuni dei criteri (impostazioni) di base di un lab in DevTest Labs
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
ms.openlocfilehash: ed35d081b191ec41ed9e5970515057a4715c0d59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="5d0f3-103">Gestire i criteri di base di un lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5d0f3-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="5d0f3-104">Azure DevTest Labs consente di gestire i criteri (impostazioni) in ogni lab, in modo da controllare i costi e ridurre al minimo gli sprechi.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="5d0f3-105">Questo articolo è una guida introduttiva ai criteri per configurare due dei più importanti criteri: la limitazione del numero di macchine virtuali che un singolo utente può creare o attestare e la configurazione di arresto automatico.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="5d0f3-106">Per vedere come impostare ogni criterio del lab, fare riferimento all'articolo [Definire i criteri di lab in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="5d0f3-106">To view how to set every lab policy, see the article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="5d0f3-107">Accesso ai criteri di lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5d0f3-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="5d0f3-108">I passaggi seguenti consentono di impostare i criteri per un lab in Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="5d0f3-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="5d0f3-109">Per visualizzare e modificare i criteri per un lab, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="5d0f3-109">To view (and change) the policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="5d0f3-110">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="5d0f3-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="5d0f3-111">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="5d0f3-112">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-112">From the list of labs, select the desired lab.</span></span>   

1. <span data-ttu-id="5d0f3-113">Selezionare **Configuration and policies** (Configurazione e criteri).</span><span class="sxs-lookup"><span data-stu-id="5d0f3-113">Select **Configuration and policies**.</span></span>

    ![Pannello Impostazioni criteri](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="5d0f3-115">Il pannello **Configuration and policies** (Configurazione e criteri) contiene un menu di impostazioni che è possibile specificare.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-115">The **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="5d0f3-116">In questo articolo vengono illustrate solo le impostazioni per **Virtual machines per user** (Macchine virtuali per utente) e **Arresto automatico**.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-116">This article covers only the settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="5d0f3-117">Per maggiori informazioni sulle altre impostazioni, vedere [Gestire tutti i criteri per un lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="5d0f3-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="5d0f3-118">Impostazione delle macchine virtuali per utente</span><span class="sxs-lookup"><span data-stu-id="5d0f3-118">Set virtual machines per user</span></span>
<span data-ttu-id="5d0f3-119">I criteri per **Macchine virtuali per utente** consentono di specificare il numero massimo di VM che possono essere create da un singolo utente.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="5d0f3-120">Se un utente prova a creare o attestare una macchina virtuale quando è stato raggiunto il limite per utente, un messaggio di errore indica che non è possibile creare o attestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="5d0f3-121">Dal menu **Configuration and policies** (Configurazione e criteri) del lab selezionare **Virtual machines per user** (Macchine virtuali per utente).</span><span class="sxs-lookup"><span data-stu-id="5d0f3-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Macchine virtuali per utente](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="5d0f3-123">Selezionare **Sì** per limitare il numero di macchine virtuali per utente.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-123">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="5d0f3-124">Se non si desidera limitare il numero di macchine virtuali per utente, selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-124">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="5d0f3-125">Se si seleziona **Sì**, immettere un valore numerico per indicare il numero massimo di macchine virtuali che un utente può creare o attestare.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="5d0f3-126">Selezionare **Sì** per limitare il numero di macchine virtuali che possono usare unità SSD.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="5d0f3-127">Se non si desidera limitare il numero di macchine virtuali che possono usare unità SSD, selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="5d0f3-128">Se si seleziona **Sì**, immettere un valore numerico per indicare il numero massimo di macchine virtuali che possono essere create usando unità SSD.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="5d0f3-129">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="5d0f3-130">Impostazione dell'arresto automatico</span><span class="sxs-lookup"><span data-stu-id="5d0f3-130">Set auto-shutdown</span></span>
<span data-ttu-id="5d0f3-131">I criteri di arresto automatico consentono di ridurre al minimo gli sprechi nel lab permettendo di specificare l'ora dell'arresto delle macchine virtuali del lab.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="5d0f3-132">Nel pannello **Configuration and policies** (Configurazione e criteri) del lab selezionare **Arresto automatico**.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-132">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Arresto automatico](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="5d0f3-134">Selezionare **Attivo** per abilitare i criteri e **Non attivo** per disabilitarli.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-134">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="5d0f3-135">Se si abilita questo criterio, specificare l'ora e il fuso orario per l'arresto di tutte le macchine virtuali nel lab attuale.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="5d0f3-136">Specificare **Sì** o **No** per questa opzione per inviare una notifica 15 minuti prima del momento specificato per l'arresto automatico.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="5d0f3-137">Se si specifica **Sì**, immettere un endpoint dell'URL webhook per ricevere la notifica.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-137">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="5d0f3-138">Per altre informazioni sui webhook, vedere [Creare un webhook o una funzione API di Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="5d0f3-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="5d0f3-139">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-139">Select **Save**.</span></span>

    <span data-ttu-id="5d0f3-140">Per impostazione predefinita, dopo l'abilitazione questi criteri verranno applicati a tutte le macchine virtuali nel lab corrente.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-140">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="5d0f3-141">Per rimuovere questa impostazione da una VM specifica, aprire il pannello della VM e modificare l'impostazione **Arresto automatico** .</span><span class="sxs-lookup"><span data-stu-id="5d0f3-141">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="5d0f3-142">Impostazione dell'avvio automatico</span><span class="sxs-lookup"><span data-stu-id="5d0f3-142">Set auto-start</span></span>
<span data-ttu-id="5d0f3-143">I criteri di avvio automatico consentono di specificare l'ora in cui devono essere avviate le macchine virtuali nel lab corrente.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-143">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="5d0f3-144">Dal pannello **Configuration and policies** (Configurazione e criteri) del lab selezionare **Avvio automatico**.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-144">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Avvio automatico](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="5d0f3-146">Selezionare **Attivo** per abilitare i criteri e **Non attivo** per disabilitarli.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-146">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="5d0f3-147">Se si abilita questo criterio, specificare l'ora di avvio pianificata, il fuso orario e i giorni della settimana a cui è applicabile questo orario.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-147">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="5d0f3-148">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-148">Select **Save**.</span></span>

    <span data-ttu-id="5d0f3-149">Dopo l'abilitazione, questi criteri non vengono applicati automaticamente alle VM del lab corrente.</span><span class="sxs-lookup"><span data-stu-id="5d0f3-149">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="5d0f3-150">Per applicare questa impostazione a una VM specifica, aprire il pannello della VM e modificare l'impostazione **Avvio automatico** .</span><span class="sxs-lookup"><span data-stu-id="5d0f3-150">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5d0f3-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d0f3-151">Next steps</span></span>

- <span data-ttu-id="5d0f3-152">[Definire i criteri di lab in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Informazioni su come modificare altri criteri di lab</span><span class="sxs-lookup"><span data-stu-id="5d0f3-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies</span></span> 
