---
title: aaaAzure Centro sicurezza PC e Windows virtuali in Azure | Documenti Microsoft
description: Informazioni sulla sicurezza delle macchine virtuali Windows in Azure con il Centro sicurezza di Azure.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 238bf4e266a24a536d35dd647db6056ab39a1f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="d5985-103">Monitorare la sicurezza delle macchine virtuali con il Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="d5985-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="d5985-104">Il Centro sicurezza di Azure consente di ottenere visibilità nelle procedure per la sicurezza delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5985-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="d5985-105">Il Centro sicurezza offre il monitoraggio della sicurezza integrato.</span><span class="sxs-lookup"><span data-stu-id="d5985-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="d5985-106">Consente di rilevare minacce che altrimenti non verrebbero rilevate.</span><span class="sxs-lookup"><span data-stu-id="d5985-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="d5985-107">Questa esercitazione illustra il Centro sicurezza di Azure e come:</span><span class="sxs-lookup"><span data-stu-id="d5985-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="d5985-108">configurare la raccolta dei dati</span><span class="sxs-lookup"><span data-stu-id="d5985-108">Set up data collection</span></span>
> * <span data-ttu-id="d5985-109">configurare i criteri di sicurezza</span><span class="sxs-lookup"><span data-stu-id="d5985-109">Set up security policies</span></span>
> * <span data-ttu-id="d5985-110">visualizzare e risolvere i problemi di integrità della configurazione</span><span class="sxs-lookup"><span data-stu-id="d5985-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="d5985-111">esaminare le minacce rilevate</span><span class="sxs-lookup"><span data-stu-id="d5985-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="d5985-112">Panoramica del Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="d5985-112">Security Center overview</span></span>

<span data-ttu-id="d5985-113">Il Centro sicurezza aiuta a identificare i potenziali problemi di configurazione e le minacce specifiche alla sicurezza delle macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d5985-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="d5985-114">Questi possono includere macchine virtuali mancanti dei gruppi di sicurezza di rete, dischi non crittografati e attacchi di forza bruta Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="d5985-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="d5985-115">Hello informazioni vengono visualizzate nel dashboard di Centro sicurezza PC hello nei grafici di facile lettura.</span><span class="sxs-lookup"><span data-stu-id="d5985-115">hello information is shown on hello Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="d5985-116">tooaccess hello dashboard Centro sicurezza PC, nel portale di Azure, dal menu di hello, seleziona hello **Centro sicurezza PC**.</span><span class="sxs-lookup"><span data-stu-id="d5985-116">tooaccess hello Security Center dashboard, in hello Azure portal, on hello menu, select  **Security Center**.</span></span> <span data-ttu-id="d5985-117">Nel dashboard di hello, può visualizzare hello integrità di protezione dell'ambiente Azure, trovare un conteggio dei consigli correnti e hello lo stato corrente degli avvisi di minaccia di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="d5985-117">On hello dashboard, you can see hello security health of your Azure environment, find a count of current recommendations, and view hello current state of threat alerts.</span></span> <span data-ttu-id="d5985-118">È possibile espandere ogni toosee grafico di alto livello dettaglio.</span><span class="sxs-lookup"><span data-stu-id="d5985-118">You can expand each high-level chart toosee more detail.</span></span>

![Dashboard del Centro sicurezza](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="d5985-120">Centro sicurezza PC va oltre indicazioni tooprovide di individuazione dati per i problemi rilevati.</span><span class="sxs-lookup"><span data-stu-id="d5985-120">Security Center goes beyond data discovery tooprovide recommendations for issues that it detects.</span></span> <span data-ttu-id="d5985-121">Ad esempio, se una macchina virtuale è stata distribuita senza un gruppo di sicurezza di rete collegato, il Centro sicurezza consente di visualizzare una raccomandazione, con una procedura di correzione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="d5985-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="d5985-122">Monitoraggio e aggiornamento automatizzato viene visualizzato senza uscire da contesto hello del Centro sicurezza PC.</span><span class="sxs-lookup"><span data-stu-id="d5985-122">You get automated remediation without leaving hello context of Security Center.</span></span>  

![Raccomandazioni](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="d5985-124">configurare la raccolta dei dati</span><span class="sxs-lookup"><span data-stu-id="d5985-124">Set up data collection</span></span>

<span data-ttu-id="d5985-125">Prima di poter ottenere visibilità in configurazioni di protezione VM, è necessario tooset Centro sicurezza PC la raccolta dei dati.</span><span class="sxs-lookup"><span data-stu-id="d5985-125">Before you can get visibility into VM security configurations, you need tooset up Security Center data collection.</span></span> <span data-ttu-id="d5985-126">Ciò comporta l'abilitazione della raccolta di dati e la creazione di un account di archiviazione di Azure toohold raccolti dati.</span><span class="sxs-lookup"><span data-stu-id="d5985-126">This involves turning on data collection and creating an Azure storage account toohold collected data.</span></span> 

1. <span data-ttu-id="d5985-127">Nel dashboard del Centro sicurezza PC hello, fare clic su **criteri di sicurezza**, quindi selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d5985-127">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="d5985-128">Per **Raccolta di dati** selezionare **On** (Abilitata).</span><span class="sxs-lookup"><span data-stu-id="d5985-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="d5985-129">Selezionare un account di archiviazione, toocreate **scegliere un account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="d5985-129">toocreate a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="d5985-130">Quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5985-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="d5985-131">In hello **criteri di sicurezza** pannello seleziona **salvare**.</span><span class="sxs-lookup"><span data-stu-id="d5985-131">On hello **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="d5985-132">agente di raccolta dati di Hello Centro sicurezza PC viene installato in tutte le macchine virtuali e inizi la raccolta dei dati.</span><span class="sxs-lookup"><span data-stu-id="d5985-132">hello Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="d5985-133">Configurare un criterio di sicurezza</span><span class="sxs-lookup"><span data-stu-id="d5985-133">Set up a security policy</span></span>

<span data-ttu-id="d5985-134">Criteri di sicurezza sono elementi di hello toodefine utilizzato per il quale il Centro sicurezza PC raccoglie i dati e fornisce consigli.</span><span class="sxs-lookup"><span data-stu-id="d5985-134">Security policies are used toodefine hello items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="d5985-135">È possibile applicare set toodifferent criteri di sicurezza diversi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5985-135">You can apply different security policies toodifferent sets of Azure resources.</span></span> <span data-ttu-id="d5985-136">Sebbene per impostazione predefinita le risorse di Azure vengono valutate per tutti gli elementi dei criteri, è possibile disattivare gli elementi di criteri individuali per tutte le risorse di Azure o per un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d5985-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="d5985-137">Per informazioni approfondite sui criteri di sicurezza del Centro sicurezza, vedere [Impostare i criteri di sicurezza nel Centro sicurezza di Azure](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d5985-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="d5985-138">tooset i criteri di sicurezza per tutte le risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="d5985-138">tooset up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="d5985-139">Nel dashboard del Centro sicurezza PC hello, selezionare **criteri di sicurezza**, quindi selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d5985-139">On hello Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="d5985-140">Selezionare **Prevention policy** (Criteri di protezione).</span><span class="sxs-lookup"><span data-stu-id="d5985-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="d5985-141">Attivare o disattivare gli elementi dei criteri che si desidera tooapply tooall risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5985-141">Turn on or turn off policy items that you want tooapply tooall Azure resources.</span></span>
4. <span data-ttu-id="d5985-142">Al termine della selezione delle impostazioni, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5985-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="d5985-143">In hello **criteri di sicurezza** pannello seleziona **salvare**.</span><span class="sxs-lookup"><span data-stu-id="d5985-143">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="d5985-144">tooset i criteri per un determinato gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="d5985-144">tooset up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="d5985-145">Nel dashboard del Centro sicurezza PC hello, selezionare **criteri di sicurezza**, quindi selezionare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d5985-145">On hello Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="d5985-146">Selezionare **Prevention policy** (Criteri di protezione).</span><span class="sxs-lookup"><span data-stu-id="d5985-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="d5985-147">Attivare o disattivare gli elementi dei criteri che si desidera tooapply toohello gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d5985-147">Turn on or turn off policy items that you want tooapply toohello resource group.</span></span>
4. <span data-ttu-id="d5985-148">In **EREDITARIETÀ** selezionare **Univoco**.</span><span class="sxs-lookup"><span data-stu-id="d5985-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="d5985-149">Al termine della selezione delle impostazioni, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5985-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="d5985-150">In hello **criteri di sicurezza** pannello seleziona **salvare**.</span><span class="sxs-lookup"><span data-stu-id="d5985-150">On hello **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="d5985-151">È anche possibile disattivare la raccolta dei dati per un gruppo di risorse specifico in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="d5985-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="d5985-152">Nell'esempio seguente di hello, un criterio univoco è stato creato per un gruppo di risorse denominato *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="d5985-152">In hello following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="d5985-153">In questi criteri sono state disabilitate le raccomandazioni relative alla crittografia del disco e al firewall dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d5985-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Criteri univoci](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="d5985-155">Visualizzare lo stato della configurazione delle VM</span><span class="sxs-lookup"><span data-stu-id="d5985-155">View VM configuration health</span></span>

<span data-ttu-id="d5985-156">Dopo aver attivato la raccolta dei dati e impostare un criterio di sicurezza, il Centro sicurezza PC inizia indicazioni e tooprovide avvisi.</span><span class="sxs-lookup"><span data-stu-id="d5985-156">After you've turned on data collection and set a security policy, Security Center begins tooprovide alerts and recommendations.</span></span> <span data-ttu-id="d5985-157">Come vengono distribuite le macchine virtuali, è installato l'agente di raccolta dati hello.</span><span class="sxs-lookup"><span data-stu-id="d5985-157">As VMs are deployed, hello data collection agent is installed.</span></span> <span data-ttu-id="d5985-158">Centro sicurezza PC viene quindi popolato con i dati per hello nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d5985-158">Security Center is then populated with data for hello new VMs.</span></span> <span data-ttu-id="d5985-159">Per informazioni dettagliate sullo stato di configurazione delle macchine virtuali, vedere [Protezione delle macchine virtuali nel Centro sicurezza di Azure](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="d5985-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="d5985-160">Come vengono raccolti i dati vengono aggregati integrità delle risorse hello per ogni macchina virtuale e le risorse di Azure correlate.</span><span class="sxs-lookup"><span data-stu-id="d5985-160">As data is collected, hello resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="d5985-161">Hello informazioni vengono visualizzate in un grafico di facile lettura.</span><span class="sxs-lookup"><span data-stu-id="d5985-161">hello information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="d5985-162">integrità delle risorse tooview:</span><span class="sxs-lookup"><span data-stu-id="d5985-162">tooview resource health:</span></span>

1.  <span data-ttu-id="d5985-163">Nel dashboard del Centro sicurezza PC hello, in **integrità delle risorse di sicurezza**selezionare **calcolo**.</span><span class="sxs-lookup"><span data-stu-id="d5985-163">On hello Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="d5985-164">In hello **calcolo** pannello seleziona **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="d5985-164">On hello **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="d5985-165">Questa visualizzazione fornisce un riepilogo dello stato di configurazione hello per tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d5985-165">This view provides a summary of hello configuration status for all your VMs.</span></span>

![Stato del calcolo](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="d5985-167">toosee tutte le indicazioni per una macchina virtuale, selezionare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d5985-167">toosee all recommendations for a VM, select hello VM.</span></span> <span data-ttu-id="d5985-168">Risoluzione di problemi e suggerimenti sono descritte più dettagliatamente nella sezione successiva di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d5985-168">Recommendations and remediation are covered in more detail in hello next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="d5985-169">Risolvere i problemi di configurazione</span><span class="sxs-lookup"><span data-stu-id="d5985-169">Remediate configuration issues</span></span>

<span data-ttu-id="d5985-170">Dopo l'avvio di Centro sicurezza PC toopopulate con dati di configurazione, raccomandazioni in base ai criteri di sicurezza hello impostati.</span><span class="sxs-lookup"><span data-stu-id="d5985-170">After Security Center begins toopopulate with configuration data, recommendations are made based on hello security policy you set up.</span></span> <span data-ttu-id="d5985-171">Se una macchina virtuale è stata configurata senza un gruppo di sicurezza di rete associati, ad esempio, un'indicazione è toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="d5985-171">For instance, if a VM was set up without an associated network security group, a recommendation is made toocreate one.</span></span> 

<span data-ttu-id="d5985-172">toosee un elenco di tutte le indicazioni:</span><span class="sxs-lookup"><span data-stu-id="d5985-172">toosee a list of all recommendations:</span></span> 

1. <span data-ttu-id="d5985-173">Nel dashboard del Centro sicurezza PC hello, selezionare **indicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d5985-173">On hello Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="d5985-174">Selezionare una raccomandazione specifica.</span><span class="sxs-lookup"><span data-stu-id="d5985-174">Select a specific recommendation.</span></span> <span data-ttu-id="d5985-175">Viene visualizzato un elenco di tutte le risorse per cui si applica l'indicazione di hello.</span><span class="sxs-lookup"><span data-stu-id="d5985-175">A list of all resources for which hello recommendation applies appears.</span></span>
3. <span data-ttu-id="d5985-176">tooapply una raccomandazione, selezionare una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="d5985-176">tooapply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="d5985-177">Seguire le istruzioni di hello per la procedura di correzione.</span><span class="sxs-lookup"><span data-stu-id="d5985-177">Follow hello instructions for remediation steps.</span></span> 

<span data-ttu-id="d5985-178">In molti casi, il Centro sicurezza PC viene descritta la procedura che è possibile eseguire una raccomandazione tooaddress senza uscire da Centro sicurezza PC.</span><span class="sxs-lookup"><span data-stu-id="d5985-178">In many cases, Security Center provides actionable steps you can take tooaddress a recommendation without leaving Security Center.</span></span> <span data-ttu-id="d5985-179">Nell'esempio seguente di hello, Centro sicurezza PC rileva un gruppo di sicurezza di rete con una regola in entrata senza restrizioni.</span><span class="sxs-lookup"><span data-stu-id="d5985-179">In hello following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="d5985-180">Nella pagina di raccomandazione hello, è possibile selezionare hello **modificare le regole in entrata** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d5985-180">On hello recommendation page, you can select hello **Edit inbound rules** button.</span></span> <span data-ttu-id="d5985-181">verrà visualizzata la finestra di Hello dell'interfaccia utente che è necessario toomodify hello regola.</span><span class="sxs-lookup"><span data-stu-id="d5985-181">hello UI that is needed toomodify hello rule appears.</span></span> 

![Raccomandazioni](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="d5985-183">Le raccomandazioni risolte vengono contrassegnate come tali.</span><span class="sxs-lookup"><span data-stu-id="d5985-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="d5985-184">Visualizzare le minacce rilevate</span><span class="sxs-lookup"><span data-stu-id="d5985-184">View detected threats</span></span>

<span data-ttu-id="d5985-185">Inoltre consigli sulla configurazione di tooresource, centro di sicurezza consente di visualizzare gli avvisi di rilevamento minacce.</span><span class="sxs-lookup"><span data-stu-id="d5985-185">In addition tooresource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="d5985-186">funzionalità degli avvisi di sicurezza Hello aggrega i dati raccolti da ogni macchina virtuale, i log di rete di Azure e partner connesso soluzioni toodetect minacce per la sicurezza contro le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5985-186">hello security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions toodetect security threats against Azure resources.</span></span> <span data-ttu-id="d5985-187">Per informazioni dettagliate sulle funzionalità di rilevamento delle minacce nel Centro sicurezza, vedere [Funzionalità di rilevamento del Centro sicurezza di Azure](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="d5985-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="d5985-188">funzionalità degli avvisi di sicurezza Hello richiede il Centro sicurezza PC hello prezzi toobe livello aumentato da *libero* troppo*Standard*.</span><span class="sxs-lookup"><span data-stu-id="d5985-188">hello security alerts feature requires hello Security Center pricing tier toobe increased from *Free* too*Standard*.</span></span> <span data-ttu-id="d5985-189">30 giorni **versione di valutazione gratuita** è disponibile quando si sposta toothis maggiore livello di prezzo.</span><span class="sxs-lookup"><span data-stu-id="d5985-189">A 30-day **free trial** is available when you move toothis higher pricing tier.</span></span> 

<span data-ttu-id="d5985-190">livello di prezzo hello toochange:</span><span class="sxs-lookup"><span data-stu-id="d5985-190">toochange hello pricing tier:</span></span>  

1. <span data-ttu-id="d5985-191">Nel dashboard del Centro sicurezza PC hello, fare clic su **criteri di sicurezza**, quindi selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d5985-191">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="d5985-192">Selezionare **Piano tariffario**.</span><span class="sxs-lookup"><span data-stu-id="d5985-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="d5985-193">Selezionare il nuovo livello di hello, quindi **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="d5985-193">Select hello new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="d5985-194">In hello **criteri di sicurezza** pannello seleziona **salvare**.</span><span class="sxs-lookup"><span data-stu-id="d5985-194">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="d5985-195">Dopo aver modificato hello a livello di prezzo, grafico gli avvisi di sicurezza hello inizia toopopulate quando vengono rilevati minacce alla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d5985-195">After you've changed hello pricing tier, hello security alerts graph begins toopopulate as security threats are detected.</span></span>

![Avvisi di sicurezza](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="d5985-197">Selezionare un avviso tooview informazioni.</span><span class="sxs-lookup"><span data-stu-id="d5985-197">Select an alert tooview information.</span></span> <span data-ttu-id="d5985-198">Ad esempio, è possibile visualizzare una descrizione del rischio di hello, ora del rilevamento hello, tutti i tentativi di minaccia e hello correzione consigliata.</span><span class="sxs-lookup"><span data-stu-id="d5985-198">For example, you can see a description of hello threat, hello detection time, all threat attempts, and hello recommended remediation.</span></span> <span data-ttu-id="d5985-199">Nell'esempio seguente di hello, è stato rilevato un attacco di forza bruta RDP, con 294 tentativi non riusciti RDP.</span><span class="sxs-lookup"><span data-stu-id="d5985-199">In hello following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="d5985-200">Viene indicata una risoluzione consigliata.</span><span class="sxs-lookup"><span data-stu-id="d5985-200">A recommended resolution is provided.</span></span>

![Attacco RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="d5985-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5985-202">Next steps</span></span>
<span data-ttu-id="d5985-203">In questa esercitazione viene configurato il Centro sicurezza di Azure e vengono quindi esaminate le macchine virtuali nel Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d5985-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="d5985-204">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="d5985-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d5985-205">configurare la raccolta dei dati</span><span class="sxs-lookup"><span data-stu-id="d5985-205">Set up data collection</span></span>
> * <span data-ttu-id="d5985-206">configurare i criteri di sicurezza</span><span class="sxs-lookup"><span data-stu-id="d5985-206">Set up security policies</span></span>
> * <span data-ttu-id="d5985-207">visualizzare e risolvere i problemi di integrità della configurazione</span><span class="sxs-lookup"><span data-stu-id="d5985-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="d5985-208">esaminare le minacce rilevate</span><span class="sxs-lookup"><span data-stu-id="d5985-208">Review detected threats</span></span>

<span data-ttu-id="d5985-209">Spostare toolearn esercitazione successiva toohello come un elemento di configurazione/CD toocreate pipeline con Visual Studio Team Services e di una macchina virtuale Windows in esecuzione IIS.</span><span class="sxs-lookup"><span data-stu-id="d5985-209">Advance toohello next tutorial toolearn how toocreate a CI/CD pipeline with Visual Studio Team Services and a Windows VM running IIS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5985-210">Pipeline CI/CD di Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="d5985-210">Visual Studio Team Services CI/CD pipeline</span></span>](./tutorial-vsts-iis-cicd.md)
