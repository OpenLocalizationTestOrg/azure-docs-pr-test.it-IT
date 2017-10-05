---
title: Centro sicurezza di Azure e macchine virtuali Linux in Azure | Microsoft Docs
description: Informazioni sulla sicurezza per macchine virtuali Linux in Azure con il Centro sicurezza di Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7f76da8cd5f4299c64c6e99d0521829c454d8c6c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="0198a-103">Monitorare la sicurezza delle macchine virtuali con il Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="0198a-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="0198a-104">Il Centro sicurezza di Azure consente di ottenere visibilità nelle procedure per la sicurezza delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="0198a-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="0198a-105">Il Centro sicurezza offre il monitoraggio della sicurezza integrato.</span><span class="sxs-lookup"><span data-stu-id="0198a-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="0198a-106">Consente di rilevare minacce che altrimenti non verrebbero rilevate.</span><span class="sxs-lookup"><span data-stu-id="0198a-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="0198a-107">Questa esercitazione illustra il Centro sicurezza di Azure e come:</span><span class="sxs-lookup"><span data-stu-id="0198a-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="0198a-108">configurare la raccolta dei dati</span><span class="sxs-lookup"><span data-stu-id="0198a-108">Set up data collection</span></span>
> * <span data-ttu-id="0198a-109">configurare i criteri di sicurezza</span><span class="sxs-lookup"><span data-stu-id="0198a-109">Set up security policies</span></span>
> * <span data-ttu-id="0198a-110">visualizzare e risolvere i problemi di integrità della configurazione</span><span class="sxs-lookup"><span data-stu-id="0198a-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="0198a-111">esaminare le minacce rilevate</span><span class="sxs-lookup"><span data-stu-id="0198a-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="0198a-112">Panoramica del Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="0198a-112">Security Center overview</span></span>

<span data-ttu-id="0198a-113">Il Centro sicurezza aiuta a identificare i potenziali problemi di configurazione e le minacce specifiche alla sicurezza delle macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0198a-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="0198a-114">Questi possono includere macchine virtuali mancanti dei gruppi di sicurezza di rete, dischi non crittografati e attacchi di forza bruta Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="0198a-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="0198a-115">Queste informazioni vengono mostrate nel dashboard del Centro sicurezza sotto forma di grafici di facile lettura.</span><span class="sxs-lookup"><span data-stu-id="0198a-115">The information is shown on the Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="0198a-116">Per accedere al dashboard del Centro sicurezza, nel portale di Azure selezionare nel menu **Centro sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="0198a-116">To access the Security Center dashboard, in the Azure portal, on the menu, select  **Security Center**.</span></span> <span data-ttu-id="0198a-117">Nel dashboard è possibile visualizzare l'integrità della sicurezza dell'ambiente Azure, accedere a una serie di raccomandazioni valide e visualizzare lo stato corrente degli avvisi di minaccia.</span><span class="sxs-lookup"><span data-stu-id="0198a-117">On the dashboard, you can see the security health of your Azure environment, find a count of current recommendations, and view the current state of threat alerts.</span></span> <span data-ttu-id="0198a-118">È possibile espandere ogni grafico di alto livello per visualizzare altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="0198a-118">You can expand each high-level chart to see more detail.</span></span>

![Dashboard del Centro sicurezza](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="0198a-120">Il Centro sicurezza va oltre l'individuazione dei dati per offrire raccomandazioni sui problemi rilevati.</span><span class="sxs-lookup"><span data-stu-id="0198a-120">Security Center goes beyond data discovery to provide recommendations for issues that it detects.</span></span> <span data-ttu-id="0198a-121">Ad esempio, se una macchina virtuale è stata distribuita senza un gruppo di sicurezza di rete collegato, il Centro sicurezza consente di visualizzare una raccomandazione, con una procedura di correzione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="0198a-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="0198a-122">Offre la correzione automatica senza lasciare il contesto del Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="0198a-122">You get automated remediation without leaving the context of Security Center.</span></span>  

![Consigli](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="0198a-124">Configurare la raccolta dei dati</span><span class="sxs-lookup"><span data-stu-id="0198a-124">Set up data collection</span></span>

<span data-ttu-id="0198a-125">Per ottenere la visibilità sulle configurazioni di sicurezza delle macchine virtuali, è necessario prima configurare la raccolta dei dati nel Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="0198a-125">Before you can get visibility into VM security configurations, you need to set up Security Center data collection.</span></span> <span data-ttu-id="0198a-126">Ciò comporta l'abilitazione della raccolta dei dati e la creazione di un account di archiviazione di Azure per contenere i dati raccolti.</span><span class="sxs-lookup"><span data-stu-id="0198a-126">This involves turning on data collection and creating an Azure storage account to hold collected data.</span></span> 

1. <span data-ttu-id="0198a-127">Nel dashboard del Centro sicurezza fare clic su **Criteri di sicurezza** e selezionare la sottoscrizione in uso.</span><span class="sxs-lookup"><span data-stu-id="0198a-127">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="0198a-128">Per **Raccolta di dati** selezionare **On** (Abilitata).</span><span class="sxs-lookup"><span data-stu-id="0198a-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="0198a-129">Per creare un account di archiviazione, selezionare **Scegliere un account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="0198a-129">To create a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="0198a-130">Quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="0198a-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="0198a-131">Nel pannello **Criteri di sicurezza** selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0198a-131">On the **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="0198a-132">L'agente di raccolta dati del Centro sicurezza viene quindi installato in tutte le macchine virtuali e la raccolta dei dati ha inizio.</span><span class="sxs-lookup"><span data-stu-id="0198a-132">The Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="0198a-133">Configurare un criterio di sicurezza</span><span class="sxs-lookup"><span data-stu-id="0198a-133">Set up a security policy</span></span>

<span data-ttu-id="0198a-134">I criteri di sicurezza vengono usati per definire gli elementi per cui il Centro sicurezza raccoglie i dati e genera raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="0198a-134">Security policies are used to define the items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="0198a-135">È possibile applicare criteri di sicurezza diversi per set di risorse di Azure diversi.</span><span class="sxs-lookup"><span data-stu-id="0198a-135">You can apply different security policies to different sets of Azure resources.</span></span> <span data-ttu-id="0198a-136">Sebbene per impostazione predefinita le risorse di Azure vengono valutate per tutti gli elementi dei criteri, è possibile disattivare gli elementi di criteri individuali per tutte le risorse di Azure o per un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0198a-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="0198a-137">Per informazioni approfondite sui criteri di sicurezza del Centro sicurezza, vedere [Impostare i criteri di sicurezza nel Centro sicurezza di Azure](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="0198a-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="0198a-138">Per configurare i criteri di sicurezza per tutte le risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="0198a-138">To set up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="0198a-139">Nel dashboard del Centro sicurezza selezionare **Criteri di sicurezza** e quindi la sottoscrizione in uso.</span><span class="sxs-lookup"><span data-stu-id="0198a-139">On the Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="0198a-140">Selezionare **Prevention policy** (Criteri di protezione).</span><span class="sxs-lookup"><span data-stu-id="0198a-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="0198a-141">Attivare o disattivare gli elementi dei criteri che si desidera applicare a tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="0198a-141">Turn on or turn off policy items that you want to apply to all Azure resources.</span></span>
4. <span data-ttu-id="0198a-142">Al termine della selezione delle impostazioni, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="0198a-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="0198a-143">Nel pannello **Criteri di sicurezza** selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0198a-143">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="0198a-144">Per configurare un criterio per un gruppo di risorse specifico:</span><span class="sxs-lookup"><span data-stu-id="0198a-144">To set up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="0198a-145">Nel dashboard del Centro sicurezza selezionare **Criteri di sicurezza** e quindi un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0198a-145">On the Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="0198a-146">Selezionare **Prevention policy** (Criteri di protezione).</span><span class="sxs-lookup"><span data-stu-id="0198a-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="0198a-147">Attivare o disattivare gli elementi dei criteri che si desidera applicare al gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0198a-147">Turn on or turn off policy items that you want to apply to the resource group.</span></span>
4. <span data-ttu-id="0198a-148">In **EREDITARIETÀ** selezionare **Univoco**.</span><span class="sxs-lookup"><span data-stu-id="0198a-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="0198a-149">Al termine della selezione delle impostazioni, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="0198a-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="0198a-150">Nel pannello **Criteri di sicurezza** selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0198a-150">On the **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="0198a-151">È anche possibile disattivare la raccolta dei dati per un gruppo di risorse specifico in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="0198a-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="0198a-152">Nell'esempio seguente sono stati creati criteri univoci per un gruppo di risorse denominato *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="0198a-152">In the following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="0198a-153">In questi criteri sono state disabilitate le raccomandazioni relative alla crittografia del disco e al firewall dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="0198a-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Criteri univoci](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="0198a-155">Visualizzare lo stato della configurazione delle VM</span><span class="sxs-lookup"><span data-stu-id="0198a-155">View VM configuration health</span></span>

<span data-ttu-id="0198a-156">Dopo aver attivato la raccolta dei dati e impostato un criterio di sicurezza, il Centro sicurezza inizia a generare avvisi e raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="0198a-156">After you've turned on data collection and set a security policy, Security Center begins to provide alerts and recommendations.</span></span> <span data-ttu-id="0198a-157">Man mano che le macchine virtuali vengono distribuite, viene installato l'agente di raccolta dati.</span><span class="sxs-lookup"><span data-stu-id="0198a-157">As VMs are deployed, the data collection agent is installed.</span></span> <span data-ttu-id="0198a-158">Il Centro sicurezza viene quindi popolato con i dati per le nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0198a-158">Security Center is then populated with data for the new VMs.</span></span> <span data-ttu-id="0198a-159">Per informazioni dettagliate sullo stato di configurazione delle macchine virtuali, vedere [Protezione delle macchine virtuali nel Centro sicurezza di Azure](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="0198a-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="0198a-160">Man mano che i dati vengono raccolti, i dati relativi all'integrità delle risorse di ogni macchina virtuale e delle risorse di Azure correlate vengono aggregati.</span><span class="sxs-lookup"><span data-stu-id="0198a-160">As data is collected, the resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="0198a-161">Le informazioni vengono mostrate in un grafico di facile lettura.</span><span class="sxs-lookup"><span data-stu-id="0198a-161">The information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="0198a-162">Per visualizzare l'integrità risorse:</span><span class="sxs-lookup"><span data-stu-id="0198a-162">To view resource health:</span></span>

1.  <span data-ttu-id="0198a-163">Nel dashboard del Centro sicurezza, in **Integrità della sicurezza delle risorse** selezionare **Calcolo**.</span><span class="sxs-lookup"><span data-stu-id="0198a-163">On the Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="0198a-164">Nel pannello **Calcolo** selezionare **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="0198a-164">On the **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="0198a-165">Questa visualizzazione riepiloga lo stato della configurazione di tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0198a-165">This view provides a summary of the configuration status for all your VMs.</span></span>

![Stato del calcolo](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="0198a-167">Per visualizzare tutte le raccomandazioni per una macchina virtuale, selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0198a-167">To see all recommendations for a VM, select the VM.</span></span> <span data-ttu-id="0198a-168">Le raccomandazioni e le correzioni sono descritte più dettagliatamente nella sezione successiva di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0198a-168">Recommendations and remediation are covered in more detail in the next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="0198a-169">Risolvere i problemi di configurazione</span><span class="sxs-lookup"><span data-stu-id="0198a-169">Remediate configuration issues</span></span>

<span data-ttu-id="0198a-170">Quando il Centro sicurezza inizia a popolarsi con i dati di configurazione, le raccomandazioni vengono generate in base ai criteri di sicurezza configurati.</span><span class="sxs-lookup"><span data-stu-id="0198a-170">After Security Center begins to populate with configuration data, recommendations are made based on the security policy you set up.</span></span> <span data-ttu-id="0198a-171">Se ad esempio è stata configurata una macchina virtuale senza un gruppo di sicurezza di rete associato, viene generata una raccomandazione per crearne uno.</span><span class="sxs-lookup"><span data-stu-id="0198a-171">For instance, if a VM was set up without an associated network security group, a recommendation is made to create one.</span></span> 

<span data-ttu-id="0198a-172">Per visualizzare un elenco di tutte le raccomandazioni:</span><span class="sxs-lookup"><span data-stu-id="0198a-172">To see a list of all recommendations:</span></span> 

1. <span data-ttu-id="0198a-173">Nel dashboard del Centro sicurezza selezionare **Raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="0198a-173">On the Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="0198a-174">Selezionare una raccomandazione specifica.</span><span class="sxs-lookup"><span data-stu-id="0198a-174">Select a specific recommendation.</span></span> <span data-ttu-id="0198a-175">Viene visualizzato un elenco di tutte le risorse per cui si applica la raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="0198a-175">A list of all resources for which the recommendation applies appears.</span></span>
3. <span data-ttu-id="0198a-176">Per applicare una raccomandazione, selezionare una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="0198a-176">To apply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="0198a-177">Seguire le istruzioni per la procedura di correzione.</span><span class="sxs-lookup"><span data-stu-id="0198a-177">Follow the instructions for remediation steps.</span></span> 

<span data-ttu-id="0198a-178">Il Centro sicurezza offre in molti casi le procedure pratiche per applicare una raccomandazione senza uscire dal Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="0198a-178">In many cases, Security Center provides actionable steps you can take to address a recommendation without leaving Security Center.</span></span> <span data-ttu-id="0198a-179">Nell'esempio seguente il Centro sicurezza rileva un gruppo di sicurezza di rete che dispone di una regola in entrata senza restrizioni.</span><span class="sxs-lookup"><span data-stu-id="0198a-179">In the following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="0198a-180">Nella pagina di raccomandazione è possibile selezionare il pulsante **Modifica le regole in ingresso**.</span><span class="sxs-lookup"><span data-stu-id="0198a-180">On the recommendation page, you can select the **Edit inbound rules** button.</span></span> <span data-ttu-id="0198a-181">Viene visualizzata l'interfaccia utente necessaria per modificare la regola.</span><span class="sxs-lookup"><span data-stu-id="0198a-181">The UI that is needed to modify the rule appears.</span></span> 

![Consigli](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="0198a-183">Le raccomandazioni risolte vengono contrassegnate come tali.</span><span class="sxs-lookup"><span data-stu-id="0198a-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="0198a-184">Visualizzare le minacce rilevate</span><span class="sxs-lookup"><span data-stu-id="0198a-184">View detected threats</span></span>

<span data-ttu-id="0198a-185">Oltre alle raccomandazioni per la configurazione delle risorse, il Centro sicurezza mostra avvisi di rilevamento di minacce.</span><span class="sxs-lookup"><span data-stu-id="0198a-185">In addition to resource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="0198a-186">La funzionalità di avviso di sicurezza aggrega i dati raccolti da ogni macchina virtuale, dai log di rete di Azure e dalle soluzioni partner collegate per rilevare le minacce alla sicurezza per le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="0198a-186">The security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions to detect security threats against Azure resources.</span></span> <span data-ttu-id="0198a-187">Per informazioni dettagliate sulle funzionalità di rilevamento delle minacce nel Centro sicurezza, vedere [Funzionalità di rilevamento del Centro sicurezza di Azure](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="0198a-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="0198a-188">Per accedere alla funzionalità degli avvisi di sicurezza, è necessario aumentare il piano tariffario del Centro sicurezza da *Gratuito* a *Standard*.</span><span class="sxs-lookup"><span data-stu-id="0198a-188">The security alerts feature requires the Security Center pricing tier to be increased from *Free* to *Standard*.</span></span> <span data-ttu-id="0198a-189">Quando si passa a questo piano tariffario superiore, è disponibile una **versione di prova gratuita** di 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="0198a-189">A 30-day **free trial** is available when you move to this higher pricing tier.</span></span> 

<span data-ttu-id="0198a-190">Per modificare il piano tariffario:</span><span class="sxs-lookup"><span data-stu-id="0198a-190">To change the pricing tier:</span></span>  

1. <span data-ttu-id="0198a-191">Nel dashboard del Centro sicurezza fare clic su **Criteri di sicurezza** e selezionare la sottoscrizione in uso.</span><span class="sxs-lookup"><span data-stu-id="0198a-191">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="0198a-192">Selezionare **Piano tariffario**.</span><span class="sxs-lookup"><span data-stu-id="0198a-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="0198a-193">Selezionare il nuovo piano e quindi **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="0198a-193">Select the new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="0198a-194">Nel pannello **Criteri di sicurezza** selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0198a-194">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="0198a-195">Dopo che il piano tariffario è stato modificato, il grafico degli avvisi di sicurezza inizia a popolarsi man mano che vengono rilevate minacce alla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="0198a-195">After you've changed the pricing tier, the security alerts graph begins to populate as security threats are detected.</span></span>

![Avvisi di sicurezza](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="0198a-197">Selezionare un avviso per visualizzare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="0198a-197">Select an alert to view information.</span></span> <span data-ttu-id="0198a-198">Ad esempio, è possibile visualizzare una descrizione della minaccia, il tempo di rilevamento, tutti i tentativi di minaccia e la correzione consigliata.</span><span class="sxs-lookup"><span data-stu-id="0198a-198">For example, you can see a description of the threat, the detection time, all threat attempts, and the recommended remediation.</span></span> <span data-ttu-id="0198a-199">Nell'esempio seguente è stato rilevato un attacco di forza bruta RDP, con 294 tentativi RDP non riusciti.</span><span class="sxs-lookup"><span data-stu-id="0198a-199">In the following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="0198a-200">Viene indicata una risoluzione consigliata.</span><span class="sxs-lookup"><span data-stu-id="0198a-200">A recommended resolution is provided.</span></span>

![Attacco RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="0198a-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0198a-202">Next steps</span></span>
<span data-ttu-id="0198a-203">In questa esercitazione viene configurato il Centro sicurezza di Azure e vengono quindi esaminate le macchine virtuali nel Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="0198a-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="0198a-204">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="0198a-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0198a-205">configurare la raccolta dei dati</span><span class="sxs-lookup"><span data-stu-id="0198a-205">Set up data collection</span></span>
> * <span data-ttu-id="0198a-206">configurare i criteri di sicurezza</span><span class="sxs-lookup"><span data-stu-id="0198a-206">Set up security policies</span></span>
> * <span data-ttu-id="0198a-207">visualizzare e risolvere i problemi di integrità della configurazione</span><span class="sxs-lookup"><span data-stu-id="0198a-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="0198a-208">Esaminare le minacce rilevate</span><span class="sxs-lookup"><span data-stu-id="0198a-208">Review detected threats</span></span>

<span data-ttu-id="0198a-209">Passare all'esercitazione successiva per altre informazioni sulla creazione di una pipeline CI/CD con Jenkins, GitHub e Docker.</span><span class="sxs-lookup"><span data-stu-id="0198a-209">Advance to the next tutorial to learn more about creating a CI/CD pipeline with Jenkins, GitHub, and Docker.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0198a-210">Creare un'infrastruttura di integrazione continua e di distribuzione continua con Jenkins, GitHub e Docker</span><span class="sxs-lookup"><span data-stu-id="0198a-210">Create CI/CD infrastructure with Jenkins, GitHub, and Docker</span></span>](tutorial-jenkins-github-docker-cicd.md)

