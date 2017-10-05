---
title: Quote e limiti del servizio per Azure Batch | Microsoft Docs
description: Informazioni sui vincoli, limiti e quote di Azure Batch predefiniti e su come richiedere incrementi di quota
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
ms.openlocfilehash: f3f69ed8d3a985afe07e648e7512a88b25278ced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="52c6f-103">Quote e limiti del servizio Batch</span><span class="sxs-lookup"><span data-stu-id="52c6f-103">Batch service quotas and limits</span></span>

<span data-ttu-id="52c6f-104">Come con altri servizi di Azure, sono previsti limiti per determinate risorse associate al servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="52c6f-104">As with other Azure services, there are limits on certain resources associated with the Batch service.</span></span> <span data-ttu-id="52c6f-105">Molti di questi limiti sono quote predefinite applicate da Azure a livello di account o di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="52c6f-105">Many of these limits are default quotas applied by Azure at the subscription or account level.</span></span> <span data-ttu-id="52c6f-106">Questo articolo illustra i valori predefiniti e come è possibile richiedere aumenti di quota.</span><span class="sxs-lookup"><span data-stu-id="52c6f-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="52c6f-107">Tenere presenti queste quote quando si progettano i carichi di lavoro di Batch e se ne aumentano le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="52c6f-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="52c6f-108">Se, ad esempio, il pool non raggiunge il numero di destinazione di nodi di calcolo specificato, potrebbe essere stato raggiunto il limite di quota di core per l'account Batch o una quota di core di macchine virtuali regionali per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="52c6f-108">For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="52c6f-109">È possibile eseguire più carichi di lavoro Batch in un solo account Batch o distribuire i carichi di lavoro tra gli account Batch nella stessa sottoscrizione, ma in aree di Azure diverse.</span><span class="sxs-lookup"><span data-stu-id="52c6f-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="52c6f-110">Se si prevede di eseguire carichi di lavoro di produzione in Batch, potrebbe essere necessario incrementare il valore predefinito di una o più quote.</span><span class="sxs-lookup"><span data-stu-id="52c6f-110">If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default.</span></span> <span data-ttu-id="52c6f-111">Per aumentare una quota, è possibile aprire una [richiesta di assistenza clienti](#increase-a-quota) online gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="52c6f-111">If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="52c6f-112">Una quota è un limite di credito, non una garanzia di capacità.</span><span class="sxs-lookup"><span data-stu-id="52c6f-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="52c6f-113">Se si hanno esigenze di capacità su larga scala, contattare il supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="52c6f-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="52c6f-114">Quote di risorse</span><span class="sxs-lookup"><span data-stu-id="52c6f-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="52c6f-115">Quote in modalità di sottoscrizione utente</span><span class="sxs-lookup"><span data-stu-id="52c6f-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="52c6f-116">Per un account Batch con modalità di allocazione di pool impostata su **sottoscrizione utente**, le macchine virtuali Batch e altre risorse, ad esempio gli account di archiviazione, vengono create direttamente nella sottoscrizione al momento della creazione di un pool.</span><span class="sxs-lookup"><span data-stu-id="52c6f-116">For a Batch account with pool allocation mode set to **user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="52c6f-117">La quota di core di Azure Batch non è applicabile a un account creato in questa modalità.</span><span class="sxs-lookup"><span data-stu-id="52c6f-117">The Azure Batch cores quota does not apply to an account created in this mode.</span></span> <span data-ttu-id="52c6f-118">Vengono applicati invece le quote della sottoscrizione per i core di calcolo regionali e altre risorse.</span><span class="sxs-lookup"><span data-stu-id="52c6f-118">Instead, the quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="52c6f-119">Per altre informazioni su tali quote, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="52c6f-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="52c6f-120">Quando si pianifica l'uso delle risorse per un account creato in modalità di sottoscrizione utente, tenere presente che le risorse di Batch seguenti (oltre ai core di calcolo) sono obbligatorie per ogni 40 macchine virtuali Linux o 20 macchine virtuali Windows:</span><span class="sxs-lookup"><span data-stu-id="52c6f-120">When planning resource usage for an account created in user subscription mode, note the following Batch resources (in addition to compute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="52c6f-121">Risorsa</span><span class="sxs-lookup"><span data-stu-id="52c6f-121">Resource</span></span> | <span data-ttu-id="52c6f-122">Quota</span><span class="sxs-lookup"><span data-stu-id="52c6f-122">Quota</span></span> | <span data-ttu-id="52c6f-123">Provider</span><span class="sxs-lookup"><span data-stu-id="52c6f-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="52c6f-124">Un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="52c6f-124">One storage account</span></span> | <span data-ttu-id="52c6f-125">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="52c6f-125">Storage Accounts</span></span> | <span data-ttu-id="52c6f-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="52c6f-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="52c6f-127">Un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="52c6f-127">One public IP address</span></span> | <span data-ttu-id="52c6f-128">Indirizzi IP pubblici</span><span class="sxs-lookup"><span data-stu-id="52c6f-128">Public IP Addresses</span></span> | <span data-ttu-id="52c6f-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="52c6f-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="52c6f-130">Una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="52c6f-130">One virtual network</span></span> | <span data-ttu-id="52c6f-131">Reti virtuali</span><span class="sxs-lookup"><span data-stu-id="52c6f-131">Virtual Networks</span></span> | <span data-ttu-id="52c6f-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="52c6f-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="52c6f-133">Un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="52c6f-133">One network security group</span></span> | <span data-ttu-id="52c6f-134">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="52c6f-134">Network Security Groups</span></span> | <span data-ttu-id="52c6f-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="52c6f-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="52c6f-136">Un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="52c6f-136">One virtual machine scale set</span></span> | <span data-ttu-id="52c6f-137">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="52c6f-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="52c6f-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="52c6f-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="52c6f-139">Un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="52c6f-139">One load balancer</span></span> | <span data-ttu-id="52c6f-140">Servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="52c6f-140">Load Balancers</span></span> | <span data-ttu-id="52c6f-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="52c6f-141">Microsoft.Network</span></span> | 

<span data-ttu-id="52c6f-142">La quota di core a livello di area o per ogni famiglia di macchine virtuali deve essere impostata in base alle dimensioni di macchina virtuale necessarie per il pool o i pool di Batch:</span><span class="sxs-lookup"><span data-stu-id="52c6f-142">The cores quota at a regional level or per VM family should be set according to the VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="52c6f-143">Quota</span><span class="sxs-lookup"><span data-stu-id="52c6f-143">Quota</span></span> | <span data-ttu-id="52c6f-144">Provider</span><span class="sxs-lookup"><span data-stu-id="52c6f-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="52c6f-145">Totale core regionali</span><span class="sxs-lookup"><span data-stu-id="52c6f-145">Total Regional Cores</span></span> | <span data-ttu-id="52c6f-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="52c6f-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="52c6f-147">…</span><span class="sxs-lookup"><span data-stu-id="52c6f-147">…</span></span> <span data-ttu-id="52c6f-148">Core a livello di famiglia</span><span class="sxs-lookup"><span data-stu-id="52c6f-148">Family Cores</span></span> | <span data-ttu-id="52c6f-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="52c6f-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="52c6f-150">Altri limiti</span><span class="sxs-lookup"><span data-stu-id="52c6f-150">Other limits</span></span>
| <span data-ttu-id="52c6f-151">**Risorsa**</span><span class="sxs-lookup"><span data-stu-id="52c6f-151">**Resource**</span></span> | <span data-ttu-id="52c6f-152">**Limite massimo**</span><span class="sxs-lookup"><span data-stu-id="52c6f-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="52c6f-153">[Attività simultanee](batch-parallel-node-tasks.md) per nodo di calcolo</span><span class="sxs-lookup"><span data-stu-id="52c6f-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="52c6f-154">4 x numero di core del nodo</span><span class="sxs-lookup"><span data-stu-id="52c6f-154">4 x number of node cores</span></span> |
| <span data-ttu-id="52c6f-155">[Applicazioni](batch-application-packages.md) per account Batch</span><span class="sxs-lookup"><span data-stu-id="52c6f-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="52c6f-156">20</span><span class="sxs-lookup"><span data-stu-id="52c6f-156">20</span></span> |
| <span data-ttu-id="52c6f-157">Pacchetti dell'applicazione per applicazione</span><span class="sxs-lookup"><span data-stu-id="52c6f-157">Application packages per application</span></span> |<span data-ttu-id="52c6f-158">40</span><span class="sxs-lookup"><span data-stu-id="52c6f-158">40</span></span> |
| <span data-ttu-id="52c6f-159">Dimensioni del pacchetto dell'applicazione (ciascuno)</span><span class="sxs-lookup"><span data-stu-id="52c6f-159">Application package size (each)</span></span> |<span data-ttu-id="52c6f-160">Circa 195 GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="52c6f-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="52c6f-161">Dimensione massima dell'attività di avvio</span><span class="sxs-lookup"><span data-stu-id="52c6f-161">Maximum start task size</span></span> | <span data-ttu-id="52c6f-162">32768 caratteri<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="52c6f-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="52c6f-163"><sup>1</sup> Limite di archiviazione di Azure per le dimensioni massime del BLOB in blocchi</span><span class="sxs-lookup"><span data-stu-id="52c6f-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="52c6f-164">
<sup>2</sup> include i file di risorse e le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="52c6f-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="52c6f-165">Visualizzare le quote Batch</span><span class="sxs-lookup"><span data-stu-id="52c6f-165">View Batch quotas</span></span>
<span data-ttu-id="52c6f-166">Visualizzare le quote dell'account Batch nel [portale di Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="52c6f-166">View your Batch account quotas in the [Azure portal][portal].</span></span>

1. <span data-ttu-id="52c6f-167">Selezionare **Account Batch** nel portale, quindi selezionare l'account Batch di interesse.</span><span class="sxs-lookup"><span data-stu-id="52c6f-167">Select **Batch accounts** in the portal, then select the Batch account you're interested in.</span></span>
2. <span data-ttu-id="52c6f-168">Selezionare **Proprietà** nel pannello del menu dell'account Batch.</span><span class="sxs-lookup"><span data-stu-id="52c6f-168">Select **Properties** on the Batch account's menu blade.</span></span>
3. <span data-ttu-id="52c6f-169">Il pannello **Proprietà** mostra le quote attualmente applicate all'account Batch</span><span class="sxs-lookup"><span data-stu-id="52c6f-169">The Properties blade displays the **quotas** currently applied to the Batch account</span></span>
   
    ![Quote di account Batch][account_quotas]

<span data-ttu-id="52c6f-171">Per un account Batch creato in modalità di sottoscrizione utente, visualizzare le quote delle sottoscrizioni correlate nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="52c6f-171">For a Batch account created in user subscription mode, view the related subscription quotas in the Azure Portal.</span></span>

1. <span data-ttu-id="52c6f-172">Selezionare **Sottoscrizioni** e quindi scegliere la sottoscrizione in uso per l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="52c6f-172">Select **Subscriptions**, and select the subscription you are using for the Batch account.</span></span>

2. <span data-ttu-id="52c6f-173">Nel pannello **Sottoscrizione** selezionare **Utilizzo e quote**.</span><span class="sxs-lookup"><span data-stu-id="52c6f-173">On the **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="52c6f-174">Aumentare una quota</span><span class="sxs-lookup"><span data-stu-id="52c6f-174">Increase a quota</span></span>
<span data-ttu-id="52c6f-175">Per richiedere un aumento di quota per la sottoscrizione o l'account Batch usando il [portale di Azure][portal], seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="52c6f-175">Follow these steps to request a quota increase for your Batch account or your subscription using the [Azure portal][portal].</span></span> <span data-ttu-id="52c6f-176">Il tipo di aumento delle quote dipende dalla modalità di allocazione del pool dell'account Batch.</span><span class="sxs-lookup"><span data-stu-id="52c6f-176">The type of quota increase depends on the pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="52c6f-177">Aumentare una quota di core Batch</span><span class="sxs-lookup"><span data-stu-id="52c6f-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="52c6f-178">Se l'account Batch è stato creato in modalità **servizio Batch**, seguire questa procedura per richiedere l'aumento di una quota di core Batch:</span><span class="sxs-lookup"><span data-stu-id="52c6f-178">If your Batch account was created in **Batch service** mode, follow these steps to request a Batch cores quota increase:</span></span>

1. <span data-ttu-id="52c6f-179">Selezionare il riquadro **Guida e supporto** nel dashboard del portale o il punto interrogativo (**?**) nell'angolo superiore destro del portale.</span><span class="sxs-lookup"><span data-stu-id="52c6f-179">Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.</span></span>
2. <span data-ttu-id="52c6f-180">Selezionare **Nuova richiesta di supporto** > **Informazioni di base**.</span><span class="sxs-lookup"><span data-stu-id="52c6f-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="52c6f-181">Nel pannello **Informazioni di base** :</span><span class="sxs-lookup"><span data-stu-id="52c6f-181">On the **Basics** blade:</span></span>
   
    <span data-ttu-id="52c6f-182">a.</span><span class="sxs-lookup"><span data-stu-id="52c6f-182">a.</span></span> <span data-ttu-id="52c6f-183">**Tipo di problema** > **Quota**</span><span class="sxs-lookup"><span data-stu-id="52c6f-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="52c6f-184">b.</span><span class="sxs-lookup"><span data-stu-id="52c6f-184">b.</span></span> <span data-ttu-id="52c6f-185">Selezionare la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="52c6f-185">Select your subscription.</span></span>
   
    <span data-ttu-id="52c6f-186">c.</span><span class="sxs-lookup"><span data-stu-id="52c6f-186">c.</span></span> <span data-ttu-id="52c6f-187">**Tipo di quota** > **Batch**</span><span class="sxs-lookup"><span data-stu-id="52c6f-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="52c6f-188">d.</span><span class="sxs-lookup"><span data-stu-id="52c6f-188">d.</span></span> <span data-ttu-id="52c6f-189">**Piano di supporto** > **Supporto per la quota - Incluso**</span><span class="sxs-lookup"><span data-stu-id="52c6f-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="52c6f-190">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="52c6f-190">Click **Next**.</span></span>
4. <span data-ttu-id="52c6f-191">Nel pannello **Problema** :</span><span class="sxs-lookup"><span data-stu-id="52c6f-191">On the **Problem** blade:</span></span>
   
    <span data-ttu-id="52c6f-192">a.</span><span class="sxs-lookup"><span data-stu-id="52c6f-192">a.</span></span> <span data-ttu-id="52c6f-193">Selezionare una **Gravità** in base all'[impatto sull'attività aziendale][support_sev].</span><span class="sxs-lookup"><span data-stu-id="52c6f-193">Select a **Severity** according to your [business impact][support_sev].</span></span>
   
    <span data-ttu-id="52c6f-194">b.</span><span class="sxs-lookup"><span data-stu-id="52c6f-194">b.</span></span> <span data-ttu-id="52c6f-195">In **Dettagli**specificare ogni quota che si desidera modificare, il nome dell'account Batch e il nuovo limite.</span><span class="sxs-lookup"><span data-stu-id="52c6f-195">In **Details**, specify each quota you want to change, the Batch account name, and the new limit.</span></span>
   
    <span data-ttu-id="52c6f-196">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="52c6f-196">Click **Next**.</span></span>
5. <span data-ttu-id="52c6f-197">Nel pannello **Informazioni di contatto** :</span><span class="sxs-lookup"><span data-stu-id="52c6f-197">On the **Contact information** blade:</span></span>
   
    <span data-ttu-id="52c6f-198">a.</span><span class="sxs-lookup"><span data-stu-id="52c6f-198">a.</span></span> <span data-ttu-id="52c6f-199">Selezionare il **metodo di contatto preferito**.</span><span class="sxs-lookup"><span data-stu-id="52c6f-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="52c6f-200">b.</span><span class="sxs-lookup"><span data-stu-id="52c6f-200">b.</span></span> <span data-ttu-id="52c6f-201">Verificare e immettere i dettagli di contatto richiesti.</span><span class="sxs-lookup"><span data-stu-id="52c6f-201">Verify and enter the required contact details.</span></span>
   
    <span data-ttu-id="52c6f-202">Fare clic su **Crea** per inviare la richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="52c6f-202">Click **Create** to submit the support request.</span></span>

<span data-ttu-id="52c6f-203">Dopo aver inviato la richiesta di supporto, si verrà contattati dal supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="52c6f-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="52c6f-204">Si noti che il completamento della richiesta può richiedere fino a 2 giorni lavorativi.</span><span class="sxs-lookup"><span data-stu-id="52c6f-204">Note that completing the request can take up to 2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="52c6f-205">Aumentare la quota di core della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="52c6f-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="52c6f-206">Se l'account Batch è stato creato in modalità di **sottoscrizione utente** ed è necessario disporre di core regionali o a livello di famiglia, richiedere un aumento di quote per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="52c6f-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="52c6f-207">Per istruzioni, vedere [Richieste di aumento della quota di core per Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="52c6f-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="52c6f-208">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="52c6f-208">Related topics</span></span>
* [<span data-ttu-id="52c6f-209">Creare un account Azure Batch usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="52c6f-209">Create an Azure Batch account using the Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="52c6f-210">Cenni preliminari sulla funzionalità Azure Batch</span><span class="sxs-lookup"><span data-stu-id="52c6f-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="52c6f-211">Sottoscrizione di Azure e limiti, quote e vincoli dei servizi</span><span class="sxs-lookup"><span data-stu-id="52c6f-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
