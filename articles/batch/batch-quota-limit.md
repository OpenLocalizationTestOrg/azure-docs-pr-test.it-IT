---
title: aaaService quote e limiti per il Batch di Azure | Documenti Microsoft
description: Informazioni sulle quote di Azure Batch predefinito, i limiti e i vincoli e come aumentare il livello toorequest quota
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="cd336-103">Quote e limiti del servizio Batch</span><span class="sxs-lookup"><span data-stu-id="cd336-103">Batch service quotas and limits</span></span>

<span data-ttu-id="cd336-104">Come con altri servizi di Azure, vi sono limiti di determinate risorse associate hello servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="cd336-104">As with other Azure services, there are limits on certain resources associated with hello Batch service.</span></span> <span data-ttu-id="cd336-105">Molti di questi limiti sono le quote predefinite applicate da Azure a livello di account o sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="cd336-105">Many of these limits are default quotas applied by Azure at hello subscription or account level.</span></span> <span data-ttu-id="cd336-106">Questo articolo illustra i valori predefiniti e come è possibile richiedere aumenti di quota.</span><span class="sxs-lookup"><span data-stu-id="cd336-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="cd336-107">Tenere presenti queste quote quando si progettano i carichi di lavoro di Batch e se ne aumentano le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cd336-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="cd336-108">Ad esempio, se il pool non è raggiunto il numero di destinazione hello dei nodi di calcolo che è stato specificato, potrebbe aver raggiunto limite di quota di core hello per l'account Batch o una quota di core VM internazionale per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cd336-108">For example, if your pool isn't reaching hello target number of compute nodes you've specified, you might have reached hello core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="cd336-109">È possibile eseguire i carichi di lavoro di più Batch in un singolo account di Batch o distribuire i carichi di lavoro tra gli account Batch in hello stessa sottoscrizione, ma in diverse aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd336-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in hello same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="cd336-110">Se si prevede di toorun i carichi di lavoro in Batch, si potrebbe essere necessario tooincrease uno o più quote hello sopra predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="cd336-110">If you plan toorun production workloads in Batch, you may need tooincrease one or more of hello quotas above hello default.</span></span> <span data-ttu-id="cd336-111">Se si desidera tooraise una quota, è possibile aprire in linea [richiesta di supporto clienti](#increase-a-quota) senza alcun costo.</span><span class="sxs-lookup"><span data-stu-id="cd336-111">If you want tooraise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="cd336-112">Una quota è un limite di credito, non una garanzia di capacità.</span><span class="sxs-lookup"><span data-stu-id="cd336-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="cd336-113">Se si hanno esigenze di capacità su larga scala, contattare il supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd336-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="cd336-114">Quote di risorse</span><span class="sxs-lookup"><span data-stu-id="cd336-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="cd336-115">Quote in modalità di sottoscrizione utente</span><span class="sxs-lookup"><span data-stu-id="cd336-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="cd336-116">Per un account Batch in modalità di allocazione del pool di troppo**sottoscrizione utente**, Batch macchine virtuali e altre risorse, quali gli account di archiviazione, vengono creati direttamente nella sottoscrizione quando viene creato un pool.</span><span class="sxs-lookup"><span data-stu-id="cd336-116">For a Batch account with pool allocation mode set too**user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="cd336-117">quota di core Hello Azure Batch non è applicabile tooan account creato in questa modalità.</span><span class="sxs-lookup"><span data-stu-id="cd336-117">hello Azure Batch cores quota does not apply tooan account created in this mode.</span></span> <span data-ttu-id="cd336-118">Al contrario, vengono applicate le quote di hello nella sottoscrizione per core di calcolo locali e altre risorse.</span><span class="sxs-lookup"><span data-stu-id="cd336-118">Instead, hello quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="cd336-119">Per altre informazioni su tali quote, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="cd336-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="cd336-120">Quando si pianifica l'utilizzo delle risorse per un account creato in modalità di sottoscrizione utente, sono necessarie per ogni 40 le macchine virtuali Linux, o 20 macchine virtuali di Windows hello nota seguente risorse Batch (in core toocompute aggiunta):</span><span class="sxs-lookup"><span data-stu-id="cd336-120">When planning resource usage for an account created in user subscription mode, note hello following Batch resources (in addition toocompute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="cd336-121">Risorsa</span><span class="sxs-lookup"><span data-stu-id="cd336-121">Resource</span></span> | <span data-ttu-id="cd336-122">Quota</span><span class="sxs-lookup"><span data-stu-id="cd336-122">Quota</span></span> | <span data-ttu-id="cd336-123">Provider</span><span class="sxs-lookup"><span data-stu-id="cd336-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="cd336-124">Un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="cd336-124">One storage account</span></span> | <span data-ttu-id="cd336-125">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="cd336-125">Storage Accounts</span></span> | <span data-ttu-id="cd336-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="cd336-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="cd336-127">Un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="cd336-127">One public IP address</span></span> | <span data-ttu-id="cd336-128">Indirizzi IP pubblici</span><span class="sxs-lookup"><span data-stu-id="cd336-128">Public IP Addresses</span></span> | <span data-ttu-id="cd336-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="cd336-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="cd336-130">Una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="cd336-130">One virtual network</span></span> | <span data-ttu-id="cd336-131">Reti virtuali</span><span class="sxs-lookup"><span data-stu-id="cd336-131">Virtual Networks</span></span> | <span data-ttu-id="cd336-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="cd336-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="cd336-133">Un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="cd336-133">One network security group</span></span> | <span data-ttu-id="cd336-134">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="cd336-134">Network Security Groups</span></span> | <span data-ttu-id="cd336-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="cd336-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="cd336-136">Un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="cd336-136">One virtual machine scale set</span></span> | <span data-ttu-id="cd336-137">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="cd336-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="cd336-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="cd336-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="cd336-139">Un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="cd336-139">One load balancer</span></span> | <span data-ttu-id="cd336-140">Servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="cd336-140">Load Balancers</span></span> | <span data-ttu-id="cd336-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="cd336-141">Microsoft.Network</span></span> | 

<span data-ttu-id="cd336-142">quota di core Hello livello regionale o per ogni famiglia di macchina virtuale deve essere set in base toohello dimensioni delle macchine Virtuali necessarie per il pool di Batch o il pool:</span><span class="sxs-lookup"><span data-stu-id="cd336-142">hello cores quota at a regional level or per VM family should be set according toohello VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="cd336-143">Quota</span><span class="sxs-lookup"><span data-stu-id="cd336-143">Quota</span></span> | <span data-ttu-id="cd336-144">Provider</span><span class="sxs-lookup"><span data-stu-id="cd336-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="cd336-145">Totale core regionali</span><span class="sxs-lookup"><span data-stu-id="cd336-145">Total Regional Cores</span></span> | <span data-ttu-id="cd336-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="cd336-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="cd336-147">…</span><span class="sxs-lookup"><span data-stu-id="cd336-147">…</span></span> <span data-ttu-id="cd336-148">Core a livello di famiglia</span><span class="sxs-lookup"><span data-stu-id="cd336-148">Family Cores</span></span> | <span data-ttu-id="cd336-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="cd336-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="cd336-150">Altri limiti</span><span class="sxs-lookup"><span data-stu-id="cd336-150">Other limits</span></span>
| <span data-ttu-id="cd336-151">**Risorsa**</span><span class="sxs-lookup"><span data-stu-id="cd336-151">**Resource**</span></span> | <span data-ttu-id="cd336-152">**Limite massimo**</span><span class="sxs-lookup"><span data-stu-id="cd336-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="cd336-153">[Attività simultanee](batch-parallel-node-tasks.md) per nodo di calcolo</span><span class="sxs-lookup"><span data-stu-id="cd336-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="cd336-154">4 x numero di core del nodo</span><span class="sxs-lookup"><span data-stu-id="cd336-154">4 x number of node cores</span></span> |
| <span data-ttu-id="cd336-155">[Applicazioni](batch-application-packages.md) per account Batch</span><span class="sxs-lookup"><span data-stu-id="cd336-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="cd336-156">20</span><span class="sxs-lookup"><span data-stu-id="cd336-156">20</span></span> |
| <span data-ttu-id="cd336-157">Pacchetti dell'applicazione per applicazione</span><span class="sxs-lookup"><span data-stu-id="cd336-157">Application packages per application</span></span> |<span data-ttu-id="cd336-158">40</span><span class="sxs-lookup"><span data-stu-id="cd336-158">40</span></span> |
| <span data-ttu-id="cd336-159">Dimensioni del pacchetto dell'applicazione (ciascuno)</span><span class="sxs-lookup"><span data-stu-id="cd336-159">Application package size (each)</span></span> |<span data-ttu-id="cd336-160">Circa 195 GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="cd336-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="cd336-161">Dimensione massima dell'attività di avvio</span><span class="sxs-lookup"><span data-stu-id="cd336-161">Maximum start task size</span></span> | <span data-ttu-id="cd336-162">32768 caratteri<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="cd336-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="cd336-163"><sup>1</sup> Limite di archiviazione di Azure per le dimensioni massime del BLOB in blocchi</span><span class="sxs-lookup"><span data-stu-id="cd336-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="cd336-164">
<sup>2</sup> include i file di risorse e le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="cd336-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="cd336-165">Visualizzare le quote Batch</span><span class="sxs-lookup"><span data-stu-id="cd336-165">View Batch quotas</span></span>
<span data-ttu-id="cd336-166">Visualizzare le quote di account di Batch in hello [portale di Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="cd336-166">View your Batch account quotas in hello [Azure portal][portal].</span></span>

1. <span data-ttu-id="cd336-167">Selezionare **Batch account** nel portale di hello, quindi selezionare account di Batch hello si è interessati.</span><span class="sxs-lookup"><span data-stu-id="cd336-167">Select **Batch accounts** in hello portal, then select hello Batch account you're interested in.</span></span>
2. <span data-ttu-id="cd336-168">Selezionare **proprietà** nel Pannello di menu dell'account Batch hello.</span><span class="sxs-lookup"><span data-stu-id="cd336-168">Select **Properties** on hello Batch account's menu blade.</span></span>
3. <span data-ttu-id="cd336-169">Pannello proprietà Hello Visualizza hello **quote** attualmente applicato account Batch toohello</span><span class="sxs-lookup"><span data-stu-id="cd336-169">hello Properties blade displays hello **quotas** currently applied toohello Batch account</span></span>
   
    ![Quote di account Batch][account_quotas]

<span data-ttu-id="cd336-171">Per un account Batch è stato creato in modalità di sottoscrizione utente, hello Vista correlate le quote della sottoscrizione nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="cd336-171">For a Batch account created in user subscription mode, view hello related subscription quotas in hello Azure Portal.</span></span>

1. <span data-ttu-id="cd336-172">Selezionare **sottoscrizioni**e selezionare hello sottoscrizione in uso per hello account Batch.</span><span class="sxs-lookup"><span data-stu-id="cd336-172">Select **Subscriptions**, and select hello subscription you are using for hello Batch account.</span></span>

2. <span data-ttu-id="cd336-173">In hello **sottoscrizione** pannello seleziona **utilizzo + quote**.</span><span class="sxs-lookup"><span data-stu-id="cd336-173">On hello **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="cd336-174">Aumentare una quota</span><span class="sxs-lookup"><span data-stu-id="cd336-174">Increase a quota</span></span>
<span data-ttu-id="cd336-175">Seguire questi toorequest passaggi aumentare di una quota per l'account Batch o la sottoscrizione utilizzando hello [portale di Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="cd336-175">Follow these steps toorequest a quota increase for your Batch account or your subscription using hello [Azure portal][portal].</span></span> <span data-ttu-id="cd336-176">tipo di Hello di aumento della quota dipende dalla modalità di allocazione del pool di hello dell'account di Batch.</span><span class="sxs-lookup"><span data-stu-id="cd336-176">hello type of quota increase depends on hello pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="cd336-177">Aumentare una quota di core Batch</span><span class="sxs-lookup"><span data-stu-id="cd336-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="cd336-178">Se l'account Batch è stato creato **Batch servizio** modalità, seguire questi toorequest passaggi un aumento della quota core Batch:</span><span class="sxs-lookup"><span data-stu-id="cd336-178">If your Batch account was created in **Batch service** mode, follow these steps toorequest a Batch cores quota increase:</span></span>

1. <span data-ttu-id="cd336-179">Seleziona hello **Guida e supporto** riquadro nel dashboard del portale o hello punto interrogativo (**?**) nell'angolo superiore destro di hello del portale hello.</span><span class="sxs-lookup"><span data-stu-id="cd336-179">Select hello **Help + support** tile on your portal dashboard, or hello question mark (**?**) in hello upper-right corner of hello portal.</span></span>
2. <span data-ttu-id="cd336-180">Selezionare **Nuova richiesta di supporto** > **Informazioni di base**.</span><span class="sxs-lookup"><span data-stu-id="cd336-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="cd336-181">In hello **nozioni di base** pannello:</span><span class="sxs-lookup"><span data-stu-id="cd336-181">On hello **Basics** blade:</span></span>
   
    <span data-ttu-id="cd336-182">a.</span><span class="sxs-lookup"><span data-stu-id="cd336-182">a.</span></span> <span data-ttu-id="cd336-183">**Tipo di problema** > **Quota**</span><span class="sxs-lookup"><span data-stu-id="cd336-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="cd336-184">b.</span><span class="sxs-lookup"><span data-stu-id="cd336-184">b.</span></span> <span data-ttu-id="cd336-185">Selezionare la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cd336-185">Select your subscription.</span></span>
   
    <span data-ttu-id="cd336-186">c.</span><span class="sxs-lookup"><span data-stu-id="cd336-186">c.</span></span> <span data-ttu-id="cd336-187">**Tipo di quota** > **Batch**</span><span class="sxs-lookup"><span data-stu-id="cd336-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="cd336-188">d.</span><span class="sxs-lookup"><span data-stu-id="cd336-188">d.</span></span> <span data-ttu-id="cd336-189">**Piano di supporto** > **Supporto per la quota - Incluso**</span><span class="sxs-lookup"><span data-stu-id="cd336-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="cd336-190">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="cd336-190">Click **Next**.</span></span>
4. <span data-ttu-id="cd336-191">In hello **problema** pannello:</span><span class="sxs-lookup"><span data-stu-id="cd336-191">On hello **Problem** blade:</span></span>
   
    <span data-ttu-id="cd336-192">a.</span><span class="sxs-lookup"><span data-stu-id="cd336-192">a.</span></span> <span data-ttu-id="cd336-193">Selezionare un **gravità** in base tooyour [impatto aziendale][support_sev].</span><span class="sxs-lookup"><span data-stu-id="cd336-193">Select a **Severity** according tooyour [business impact][support_sev].</span></span>
   
    <span data-ttu-id="cd336-194">b.</span><span class="sxs-lookup"><span data-stu-id="cd336-194">b.</span></span> <span data-ttu-id="cd336-195">In **dettagli**, specificare ogni quota si desidera toochange, nome dell'account Batch hello e hello nuovo limite.</span><span class="sxs-lookup"><span data-stu-id="cd336-195">In **Details**, specify each quota you want toochange, hello Batch account name, and hello new limit.</span></span>
   
    <span data-ttu-id="cd336-196">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="cd336-196">Click **Next**.</span></span>
5. <span data-ttu-id="cd336-197">In hello **le informazioni di contatto** pannello:</span><span class="sxs-lookup"><span data-stu-id="cd336-197">On hello **Contact information** blade:</span></span>
   
    <span data-ttu-id="cd336-198">a.</span><span class="sxs-lookup"><span data-stu-id="cd336-198">a.</span></span> <span data-ttu-id="cd336-199">Selezionare il **metodo di contatto preferito**.</span><span class="sxs-lookup"><span data-stu-id="cd336-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="cd336-200">b.</span><span class="sxs-lookup"><span data-stu-id="cd336-200">b.</span></span> <span data-ttu-id="cd336-201">Verificare e immettere i dettagli di contatto hello necessario.</span><span class="sxs-lookup"><span data-stu-id="cd336-201">Verify and enter hello required contact details.</span></span>
   
    <span data-ttu-id="cd336-202">Fare clic su **crea** toosubmit hello richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="cd336-202">Click **Create** toosubmit hello support request.</span></span>

<span data-ttu-id="cd336-203">Dopo aver inviato la richiesta di supporto, si verrà contattati dal supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd336-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="cd336-204">Nota: completamento hello richiesta può richiedere giorni lavorativi too2.</span><span class="sxs-lookup"><span data-stu-id="cd336-204">Note that completing hello request can take up too2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="cd336-205">Aumentare la quota di core della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="cd336-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="cd336-206">Se l'account Batch è stato creato in modalità di **sottoscrizione utente** ed è necessario disporre di core regionali o a livello di famiglia, richiedere un aumento di quote per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cd336-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="cd336-207">Per istruzioni, vedere [Richieste di aumento della quota di core per Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="cd336-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="cd336-208">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="cd336-208">Related topics</span></span>
* [<span data-ttu-id="cd336-209">Creare un account Azure Batch utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cd336-209">Create an Azure Batch account using hello Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="cd336-210">Cenni preliminari sulla funzionalità Azure Batch</span><span class="sxs-lookup"><span data-stu-id="cd336-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="cd336-211">Sottoscrizione di Azure e limiti, quote e vincoli dei servizi</span><span class="sxs-lookup"><span data-stu-id="cd336-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
