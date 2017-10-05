---
title: Progettare e implementare un database Oracle in Azure | Microsoft Docs
description: Progettare e implementare un database Oracle nell'ambiente Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 1af7e1d40a0eb129875dd6a30ac899f2025bee13
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="e448d-103">Progettare e implementare un database Oracle in Azure</span><span class="sxs-lookup"><span data-stu-id="e448d-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="e448d-104">Presupposti</span><span class="sxs-lookup"><span data-stu-id="e448d-104">Assumptions</span></span>

- <span data-ttu-id="e448d-105">Si sta pianificando la migrazione di un database Oracle da locale ad Azure.</span><span class="sxs-lookup"><span data-stu-id="e448d-105">You're planning to migrate an Oracle database from on-premises to Azure.</span></span>
- <span data-ttu-id="e448d-106">Si conoscono le varie metriche dei report AWR di Oracle.</span><span class="sxs-lookup"><span data-stu-id="e448d-106">You have an understanding of the various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="e448d-107">Si ha una conoscenza di base delle prestazioni delle applicazioni e dell'utilizzo della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="e448d-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="e448d-108">Obiettivi</span><span class="sxs-lookup"><span data-stu-id="e448d-108">Goals</span></span>

- <span data-ttu-id="e448d-109">Sapere come ottimizzare la distribuzione di Oracle in Azure.</span><span class="sxs-lookup"><span data-stu-id="e448d-109">Understand how to optimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="e448d-110">Esplorare le opzioni di ottimizzazione delle prestazioni per un database Oracle in un ambiente Azure.</span><span class="sxs-lookup"><span data-stu-id="e448d-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="the-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="e448d-111">Differenze tra un'implementazione locale e in Azure</span><span class="sxs-lookup"><span data-stu-id="e448d-111">The differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="e448d-112">Di seguito sono descritti alcuni importanti elementi da tenere in considerazione quando si esegue la migrazione di applicazioni locali ad Azure.</span><span class="sxs-lookup"><span data-stu-id="e448d-112">Following are some important things to keep in mind when you're migrating on-premises applications to Azure.</span></span> 

<span data-ttu-id="e448d-113">Una differenza importante è che in un'implementazione in Azure le risorse, ad esempio VM, dischi e reti virtuali, vengono condivise con gli altri client.</span><span class="sxs-lookup"><span data-stu-id="e448d-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="e448d-114">Le risorse possono anche essere limitate in base ai requisiti.</span><span class="sxs-lookup"><span data-stu-id="e448d-114">In addition, resources can be throttled based on the requirements.</span></span> <span data-ttu-id="e448d-115">Invece di focalizzarsi sull'evitare gli errori (MTBF), Azure è più orientato alla sopravvivenza agli errori (MTTR).</span><span class="sxs-lookup"><span data-stu-id="e448d-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving the failure (MTTR).</span></span>

<span data-ttu-id="e448d-116">La tabella seguente elenca alcune differenze tra un'implementazione locale e un'implementazione in Azure di un database Oracle.</span><span class="sxs-lookup"><span data-stu-id="e448d-116">The following table lists some of the differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="e448d-117">**Implementazione locale**</span><span class="sxs-lookup"><span data-stu-id="e448d-117">**On-premises implementation**</span></span> | <span data-ttu-id="e448d-118">**Implementazione in Azure**</span><span class="sxs-lookup"><span data-stu-id="e448d-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="e448d-119">**Rete**</span><span class="sxs-lookup"><span data-stu-id="e448d-119">**Networking**</span></span> |<span data-ttu-id="e448d-120">LAN/WAN</span><span class="sxs-lookup"><span data-stu-id="e448d-120">LAN/WAN</span></span>  |<span data-ttu-id="e448d-121">SDN (Software Defined Networking)</span><span class="sxs-lookup"><span data-stu-id="e448d-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="e448d-122">**Gruppo di sicurezza**</span><span class="sxs-lookup"><span data-stu-id="e448d-122">**Security group**</span></span> |<span data-ttu-id="e448d-123">Strumenti di restrizione per indirizzi IP/porte</span><span class="sxs-lookup"><span data-stu-id="e448d-123">IP/port restriction tools</span></span> |[<span data-ttu-id="e448d-124">Gruppo di sicurezza di rete (NSG)</span><span class="sxs-lookup"><span data-stu-id="e448d-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="e448d-125">**Resilienza**</span><span class="sxs-lookup"><span data-stu-id="e448d-125">**Resilience**</span></span> |<span data-ttu-id="e448d-126">MTBF (tempo medio tra gli errori)</span><span class="sxs-lookup"><span data-stu-id="e448d-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="e448d-127">MTTR (tempo medio per il ripristino)</span><span class="sxs-lookup"><span data-stu-id="e448d-127">MTTR (mean time to recovery)</span></span>|
> | <span data-ttu-id="e448d-128">**Manutenzione pianificata**</span><span class="sxs-lookup"><span data-stu-id="e448d-128">**Planned maintenance**</span></span> |<span data-ttu-id="e448d-129">Applicazione di patch/aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="e448d-129">Patching/upgrades</span></span>|<span data-ttu-id="e448d-130">[Set di disponibilità](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (applicazione di patch/aggiornamenti gestita da Azure)</span><span class="sxs-lookup"><span data-stu-id="e448d-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="e448d-131">**Risorsa**</span><span class="sxs-lookup"><span data-stu-id="e448d-131">**Resource**</span></span> |<span data-ttu-id="e448d-132">Dedicato</span><span class="sxs-lookup"><span data-stu-id="e448d-132">Dedicated</span></span>  |<span data-ttu-id="e448d-133">Condivisa con altri client</span><span class="sxs-lookup"><span data-stu-id="e448d-133">Shared with other clients</span></span>|
> | <span data-ttu-id="e448d-134">**Aree**</span><span class="sxs-lookup"><span data-stu-id="e448d-134">**Regions**</span></span> |<span data-ttu-id="e448d-135">Data center</span><span class="sxs-lookup"><span data-stu-id="e448d-135">Datacenters</span></span> |[<span data-ttu-id="e448d-136">Coppie di aree</span><span class="sxs-lookup"><span data-stu-id="e448d-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="e448d-137">**Archiviazione**</span><span class="sxs-lookup"><span data-stu-id="e448d-137">**Storage**</span></span> |<span data-ttu-id="e448d-138">Dischi fisici/SAN</span><span class="sxs-lookup"><span data-stu-id="e448d-138">SAN/physical disks</span></span> |[<span data-ttu-id="e448d-139">Archiviazione gestita da Azure</span><span class="sxs-lookup"><span data-stu-id="e448d-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="e448d-140">**Ridimensionare**</span><span class="sxs-lookup"><span data-stu-id="e448d-140">**Scale**</span></span> |<span data-ttu-id="e448d-141">Scalabilità verticale</span><span class="sxs-lookup"><span data-stu-id="e448d-141">Vertical scale</span></span> |<span data-ttu-id="e448d-142">Scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="e448d-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="e448d-143">Requisiti</span><span class="sxs-lookup"><span data-stu-id="e448d-143">Requirements</span></span>

- <span data-ttu-id="e448d-144">Determinare le dimensioni e il tasso di crescita del database.</span><span class="sxs-lookup"><span data-stu-id="e448d-144">Determine the database size and growth rate.</span></span>
- <span data-ttu-id="e448d-145">Determinare i requisiti IOPS, che è possibile stimare in base ai report AWR di Oracle o ad altri strumenti di monitoraggio della rete.</span><span class="sxs-lookup"><span data-stu-id="e448d-145">Determine the IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="e448d-146">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="e448d-146">Configuration options</span></span>

<span data-ttu-id="e448d-147">Esistono quattro potenziali aree che è possibile ottimizzare per migliorare le prestazioni in un ambiente Azure:</span><span class="sxs-lookup"><span data-stu-id="e448d-147">There are four potential areas that you can tune to improve performance in an Azure environment:</span></span>

- <span data-ttu-id="e448d-148">Dimensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e448d-148">Virtual machine size</span></span>
- <span data-ttu-id="e448d-149">Velocità effettiva della rete</span><span class="sxs-lookup"><span data-stu-id="e448d-149">Network throughput</span></span>
- <span data-ttu-id="e448d-150">Tipi di disco e configurazioni</span><span class="sxs-lookup"><span data-stu-id="e448d-150">Disk types and configurations</span></span>
- <span data-ttu-id="e448d-151">Impostazioni della cache su disco</span><span class="sxs-lookup"><span data-stu-id="e448d-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="e448d-152">Generare un report AWR</span><span class="sxs-lookup"><span data-stu-id="e448d-152">Generate an AWR report</span></span>

<span data-ttu-id="e448d-153">Se è già disponibile database Oracle di cui si sta pianificando la migrazione ad Azure, esistono diverse opzioni.</span><span class="sxs-lookup"><span data-stu-id="e448d-153">If you have an existing an Oracle database and are planning to migrate to Azure, you have several options.</span></span> <span data-ttu-id="e448d-154">È possibile eseguire il report AWR di Oracle per ottenere le metriche (operazioni di I/O al secondo, Mbps, GiB e così via).</span><span class="sxs-lookup"><span data-stu-id="e448d-154">You can run the Oracle AWR report to get the metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="e448d-155">Scegliere quindi la VM in base alle metriche raccolte.</span><span class="sxs-lookup"><span data-stu-id="e448d-155">Then choose the VM based on the metrics that you collected.</span></span> <span data-ttu-id="e448d-156">In alternativa, è possibile contattare il team dell'infrastruttura per ottenere informazioni simili.</span><span class="sxs-lookup"><span data-stu-id="e448d-156">Or you can contact your infrastructure team to get similar information.</span></span>

<span data-ttu-id="e448d-157">È possibile valutare se eseguire il report AWR durante i carichi di lavoro sia normali che di picco, per poter effettuare un confronto.</span><span class="sxs-lookup"><span data-stu-id="e448d-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="e448d-158">Attraverso questi report, è possibile ridimensionare le macchine virtuali in base al carico di lavoro medio o al carico di lavoro massimo.</span><span class="sxs-lookup"><span data-stu-id="e448d-158">Based on these reports, you can size the VMs based on either the average workload or the maximum workload.</span></span>

<span data-ttu-id="e448d-159">Di seguito è riportato un esempio di come generare un report AWR:</span><span class="sxs-lookup"><span data-stu-id="e448d-159">Following is an example of how to generate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="e448d-160">Metriche principali</span><span class="sxs-lookup"><span data-stu-id="e448d-160">Key metrics</span></span>

<span data-ttu-id="e448d-161">Di seguito sono indicate le metriche che è possibile ottenere dal report AWR:</span><span class="sxs-lookup"><span data-stu-id="e448d-161">Following are the metrics that you can obtain from the AWR report:</span></span>

- <span data-ttu-id="e448d-162">Numero totale di core</span><span class="sxs-lookup"><span data-stu-id="e448d-162">Total number of cores</span></span>
- <span data-ttu-id="e448d-163">Velocità di clock della CPU</span><span class="sxs-lookup"><span data-stu-id="e448d-163">CPU clock speed</span></span>
- <span data-ttu-id="e448d-164">Memoria totale in GB</span><span class="sxs-lookup"><span data-stu-id="e448d-164">Total memory in GB</span></span>
- <span data-ttu-id="e448d-165">Uso della CPU</span><span class="sxs-lookup"><span data-stu-id="e448d-165">CPU utilization</span></span>
- <span data-ttu-id="e448d-166">Velocità di trasferimento dati di picco</span><span class="sxs-lookup"><span data-stu-id="e448d-166">Peak data transfer rate</span></span>
- <span data-ttu-id="e448d-167">Frequenza delle modifiche di I/O (lettura/scrittura)</span><span class="sxs-lookup"><span data-stu-id="e448d-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="e448d-168">Velocità del log di ripristino (Mbps)</span><span class="sxs-lookup"><span data-stu-id="e448d-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="e448d-169">Velocità effettiva della rete</span><span class="sxs-lookup"><span data-stu-id="e448d-169">Network throughput</span></span>
- <span data-ttu-id="e448d-170">Latenza di rete (bassa/alta)</span><span class="sxs-lookup"><span data-stu-id="e448d-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="e448d-171">Dimensioni del database in GB</span><span class="sxs-lookup"><span data-stu-id="e448d-171">Database size in GB</span></span>
- <span data-ttu-id="e448d-172">Byte ricevuti tramite SQL*Net da e verso il client</span><span class="sxs-lookup"><span data-stu-id="e448d-172">Bytes received via SQL*Net from/to client</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="e448d-173">Dimensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e448d-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-the-awr-report"></a><span data-ttu-id="e448d-174">1. Stimare le dimensioni della macchina virtuale in base a utilizzo di CPU, memoria e I/O dal report AWR</span><span class="sxs-lookup"><span data-stu-id="e448d-174">1. Estimate VM size based on CPU, memory, and I/O usage from the AWR report</span></span>

<span data-ttu-id="e448d-175">Un elemento che è possibile osservare sono i primi cinque eventi in primo piano, che indicano dove sono presenti i colli di bottiglia del sistema.</span><span class="sxs-lookup"><span data-stu-id="e448d-175">One thing you might look at is the top five timed foreground events that indicate where the system bottlenecks are.</span></span>

<span data-ttu-id="e448d-176">Nel diagramma seguente, ad esempio, la sincronizzazione dei file di log è all'inizio.</span><span class="sxs-lookup"><span data-stu-id="e448d-176">For example, in the following diagram, the log file sync is at the top.</span></span> <span data-ttu-id="e448d-177">Indica il numero di attese necessarie prima che LGWR scriva il buffer del log nel file di log di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e448d-177">It indicates the number of waits that are required before the LGWR writes the log buffer to the redo log file.</span></span> <span data-ttu-id="e448d-178">Questi risultati indicano che è necessario migliorare le prestazioni della risorsa di archiviazione o dei dischi.</span><span class="sxs-lookup"><span data-stu-id="e448d-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="e448d-179">Il diagramma indica anche il numero di CPU (core) e la quantità di memoria.</span><span class="sxs-lookup"><span data-stu-id="e448d-179">In addition, the diagram also shows the number of CPU (cores) and the amount of memory.</span></span>

![Screenshot della pagina del report AWR](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="e448d-181">Il diagramma seguente mostra l'I/O totale di lettura e scrittura.</span><span class="sxs-lookup"><span data-stu-id="e448d-181">The following diagram shows the total I/O of read and write.</span></span> <span data-ttu-id="e448d-182">Sono stati registrati 59 GB in lettura e 247,3 GB in scrittura durante il periodo di esecuzione del report.</span><span class="sxs-lookup"><span data-stu-id="e448d-182">There were 59 GB read and 247.3 GB written during the time of the report.</span></span>

![Screenshot della pagina del report AWR](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="e448d-184">2. Scegliere una VM</span><span class="sxs-lookup"><span data-stu-id="e448d-184">2. Choose a VM</span></span>

<span data-ttu-id="e448d-185">In base alle informazioni raccolte dal report AWR, il passaggio successivo è scegliere una macchina virtuale di dimensioni simili che soddisfi i requisiti.</span><span class="sxs-lookup"><span data-stu-id="e448d-185">Based on the information that you collected from the AWR report, the next step is to choose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="e448d-186">È possibile trovare un elenco delle VM disponibili nell'articolo [Ottimizzate per la memoria](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span><span class="sxs-lookup"><span data-stu-id="e448d-186">You can find a list of available VMs in the article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-the-vm-sizing-with-a-similar-vm-series-based-on-the-acu"></a><span data-ttu-id="e448d-187">3. Ottimizzare il dimensionamento delle macchine virtuali con una serie di macchine virtuali simili basate sull'ACU</span><span class="sxs-lookup"><span data-stu-id="e448d-187">3. Fine-tune the VM sizing with a similar VM series based on the ACU</span></span>

<span data-ttu-id="e448d-188">Dopo avere scelto la VM, prestare attenzione all'ACU per la VM.</span><span class="sxs-lookup"><span data-stu-id="e448d-188">After you've chosen the VM, pay attention to the ACU for the VM.</span></span> <span data-ttu-id="e448d-189">In base al valore ACU, è possibile scegliere una macchina virtuale diversa più adatta agli specifici requisiti.</span><span class="sxs-lookup"><span data-stu-id="e448d-189">You might choose a different VM based on the ACU value that better suits your requirements.</span></span> <span data-ttu-id="e448d-190">Per altre informazioni, vedere [Unità di calcolo di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span><span class="sxs-lookup"><span data-stu-id="e448d-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![Screenshot della pagina delle unità ACU](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="e448d-192">Velocità effettiva della rete</span><span class="sxs-lookup"><span data-stu-id="e448d-192">Network throughput</span></span>

<span data-ttu-id="e448d-193">Come illustra il diagramma seguente, esiste una relazione tra velocità effettiva e IOPS:</span><span class="sxs-lookup"><span data-stu-id="e448d-193">The following diagram shows the relation between throughput and IOPS:</span></span>

![Screenshot della velocità effettiva](./media/oracle-design/throughput.png)

<span data-ttu-id="e448d-195">La velocità effettiva totale della rete viene stimata in base alle informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e448d-195">The total network throughput is estimated based on the following information:</span></span>
- <span data-ttu-id="e448d-196">Traffico SQL*Net</span><span class="sxs-lookup"><span data-stu-id="e448d-196">SQL*Net traffic</span></span>
- <span data-ttu-id="e448d-197">Mbps x numero di server (flusso in uscita, ad esempio Oracle Data Guard)</span><span class="sxs-lookup"><span data-stu-id="e448d-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="e448d-198">Altri fattori, ad esempio la replica dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e448d-198">Other factors, such as application replication</span></span>

![Screenshot della velocità effettiva SQL*Net](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="e448d-200">In base ai requisiti di larghezza di banda della rete, sono disponibili diversi tipi di gateway tra cui scegliere,</span><span class="sxs-lookup"><span data-stu-id="e448d-200">Based on your network bandwidth requirements, there are various gateway types for you to choose from.</span></span> <span data-ttu-id="e448d-201">ad esempio Basic, VpnGw e Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e448d-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="e448d-202">Per altre informazioni, vedere la [pagina Prezzi di Gateway VPN](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span><span class="sxs-lookup"><span data-stu-id="e448d-202">For more information, see the [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="e448d-203">**Raccomandazioni**</span><span class="sxs-lookup"><span data-stu-id="e448d-203">**Recommendations**</span></span>

- <span data-ttu-id="e448d-204">La latenza di rete è superiore rispetto a una distribuzione locale.</span><span class="sxs-lookup"><span data-stu-id="e448d-204">Network latency is higher compared to an on-premises deployment.</span></span> <span data-ttu-id="e448d-205">La riduzione dei round trip di rete può migliorare notevolmente le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e448d-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="e448d-206">Per ridurre i round trip, consolidare le applicazioni con transazioni elevate o con un livello di comunicazioni elevato nella stessa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e448d-206">To reduce round-trips, consolidate applications that have high transactions or “chatty” apps on the same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="e448d-207">Tipi di disco e configurazioni</span><span class="sxs-lookup"><span data-stu-id="e448d-207">Disk types and configurations</span></span>

- <span data-ttu-id="e448d-208">*Dischi del sistema operativo predefiniti*: questi tipi di dischi offrono dati persistenti e memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="e448d-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="e448d-209">Sono ottimizzati per l'accesso del sistema operativo all'avvio e non sono progettati per i carichi di lavoro transazionali o di data warehouse (analitici).</span><span class="sxs-lookup"><span data-stu-id="e448d-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="e448d-210">*Dischi non gestiti*: con questo tipi di dischi, si gestiscono gli account di archiviazione che archiviano i file di disco rigido virtuale (VHD) che corrispondono ai dischi delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e448d-210">*Unmanaged disks*: With these disk types, you manage the storage accounts that store the virtual hard disk (VHD) files that correspond to your VM disks.</span></span> <span data-ttu-id="e448d-211">I file VHD vengono archiviati come BLOB di pagine in account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e448d-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="e448d-212">*Dischi gestiti*: Azure gestisce gli account di archiviazione usati per i dischi delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e448d-212">*Managed disks*: Azure manages the storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="e448d-213">Specificare il tipo di disco (Premium o Standard) e la dimensione del disco necessaria.</span><span class="sxs-lookup"><span data-stu-id="e448d-213">You specify the disk type (premium or standard) and the size of the disk that you need.</span></span> <span data-ttu-id="e448d-214">Azure crea e gestisce il disco automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e448d-214">Azure creates and manages the disk for you.</span></span>

- <span data-ttu-id="e448d-215">*Dischi di archiviazione Premium*: questi tipi di dischi sono ideali per i carichi di lavoro di produzione.</span><span class="sxs-lookup"><span data-stu-id="e448d-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="e448d-216">Archiviazione Premium supporta i dischi di VM che possono essere collegati a VM di serie con dimensioni specifiche, ad esempio VM serie DS, DSv2, GS e F.</span><span class="sxs-lookup"><span data-stu-id="e448d-216">Premium storage supports VM disks that can be attached to specific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="e448d-217">Il disco Premium può essere di varie dimensioni ed è possibile scegliere tra dischi compresi tra 32 GB e 4.096 GB.</span><span class="sxs-lookup"><span data-stu-id="e448d-217">The premium disk comes with different sizes, and you can choose between disks ranging from 32 GB to 4,096 GB.</span></span> <span data-ttu-id="e448d-218">Ciascuna dimensione di disco ha le proprie specifiche in termini di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e448d-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="e448d-219">A seconda dei requisiti dell'applicazione è possibile collegare uno o più dischi alla VM.</span><span class="sxs-lookup"><span data-stu-id="e448d-219">Depending on your application requirements, you can attach one or more disks to your VM.</span></span>

<span data-ttu-id="e448d-220">Quando si crea un nuovo disco gestito dal portale, è possibile scegliere il **tipo di account** per il tipo di disco da usare.</span><span class="sxs-lookup"><span data-stu-id="e448d-220">When you create a new managed disk from the portal, you can choose the **Account type** for the type of disk you want to use.</span></span> <span data-ttu-id="e448d-221">Tenere presente che non tutti i dischi disponibili sono visualizzati nel menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="e448d-221">Keep in mind that not all available disks are shown in the drop-down menu.</span></span> <span data-ttu-id="e448d-222">Dopo avere scelto determinate dimensioni per la VM, il menu mostra solo gli SKU di Archiviazione Premium disponibili in base a tali dimensioni della VM.</span><span class="sxs-lookup"><span data-stu-id="e448d-222">After you choose a particular VM size, the menu shows only the available premium storage SKUs that are based on that VM size.</span></span>

![Screenshot della pagina del disco gestito](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="e448d-224">Per altre informazioni, vedere [Archiviazione Premium a prestazioni elevate e dischi gestiti per le VM](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="e448d-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="e448d-225">Dopo avere configurato la risorsa di archiviazione in una macchina virtuale, è possibile sottoporre i dischi a test di carico prima di creare un database.</span><span class="sxs-lookup"><span data-stu-id="e448d-225">After you configure your storage on a VM, you might want to load test the disks before creating a database.</span></span> <span data-ttu-id="e448d-226">Conoscendo la velocità di I/O in termini di latenza e velocità effettiva, è possibile determinare se le macchine virtuali supportano la velocità effettiva prevista con gli obiettivi di latenza.</span><span class="sxs-lookup"><span data-stu-id="e448d-226">Knowing the I/O rate in terms of both latency and throughput can help you determine if the VMs support the expected throughput with latency targets.</span></span>

<span data-ttu-id="e448d-227">Sono disponibili numerosi strumenti per il test di carico delle applicazioni, ad esempio Oracle Orion, Sysbench e Fio.</span><span class="sxs-lookup"><span data-stu-id="e448d-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="e448d-228">Dopo avere distribuito un database Oracle, eseguire nuovamente il test di carico.</span><span class="sxs-lookup"><span data-stu-id="e448d-228">Run the load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="e448d-229">Avviare i carico di lavoro normali e di picco. I risultati indicheranno la baseline dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="e448d-229">Start your regular and peak workloads, and the results show you the baseline of your environment.</span></span>

<span data-ttu-id="e448d-230">Può essere più importante ridimensionare l'archiviazione in base alla frequenza di operazioni di I/O al secondo invece che alle dimensioni di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e448d-230">It might be more important to size the storage based on the IOPS rate rather than the storage size.</span></span> <span data-ttu-id="e448d-231">Se ad esempio le operazioni di I/O al secondo necessarie sono 5.000, ma servono solo 200 GB, si potrebbe comunque scegliere il disco Premium classe P30 anche se ha più di 200 GB di spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e448d-231">For example, if the required IOPS is 5,000, but you only need 200 GB, you might still get the P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="e448d-232">Dal report AWR si può ottenere la frequenza di operazioni di I/O,</span><span class="sxs-lookup"><span data-stu-id="e448d-232">The IOPS rate can be obtained from the AWR report.</span></span> <span data-ttu-id="e448d-233">che è determinata da log di rollforward, letture fisiche e frequenza delle scritture.</span><span class="sxs-lookup"><span data-stu-id="e448d-233">It's determined by the redo log, physical reads, and writes rate.</span></span>

![Screenshot della pagina del report AWR](./media/oracle-design/awr_report.png)

<span data-ttu-id="e448d-235">Ad esempio: la dimensione di rollforward è 12.200.000 byte al secondo, equivalente a 11,63 Mbps.</span><span class="sxs-lookup"><span data-stu-id="e448d-235">For example, the redo size is 12,200,000 bytes per second, which is equal to 11.63 MBPs.</span></span>
<span data-ttu-id="e448d-236">Le operazioni di I/O al secondo corrispondono a 12.200.000/2.358 = 5.174.</span><span class="sxs-lookup"><span data-stu-id="e448d-236">The IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="e448d-237">Dopo avere ottenuto un quadro preciso dei requisiti di I/O, è possibile scegliere la combinazione delle unità più adatte per soddisfare tali requisiti.</span><span class="sxs-lookup"><span data-stu-id="e448d-237">After you have a clear picture of the I/O requirements, you can choose a combination of drives that are best suited to meet those requirements.</span></span>

<span data-ttu-id="e448d-238">**Raccomandazioni**</span><span class="sxs-lookup"><span data-stu-id="e448d-238">**Recommendations**</span></span>

- <span data-ttu-id="e448d-239">Per lo spazio di tabella dei dati, ripartire il carico di lavoro di I/O tra diversi dischi usando l'archiviazione gestita o Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="e448d-239">For data tablespace, spread the I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="e448d-240">Con l'aumento della dimensione dei blocchi di I/O, per le operazioni intensive di lettura e di scrittura, aggiungere più dischi dati.</span><span class="sxs-lookup"><span data-stu-id="e448d-240">As the I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="e448d-241">Aumentare la dimensione dei blocchi per i processi sequenziali di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="e448d-241">Increase the block size for large sequential processes.</span></span>
- <span data-ttu-id="e448d-242">Usare la compressione dei dati per ridurre le operazioni di I/O (per i dati e gli indici).</span><span class="sxs-lookup"><span data-stu-id="e448d-242">Use data compression to reduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="e448d-243">Separare i log di rollforward, di sistema e temporanei e annullare TS nei dischi dati separati.</span><span class="sxs-lookup"><span data-stu-id="e448d-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="e448d-244">Non inserire alcun file dell'applicazione nei dischi del sistema operativo predefiniti (dev/sda).</span><span class="sxs-lookup"><span data-stu-id="e448d-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="e448d-245">Questi dischi non sono ottimizzati per l'avvio rapido delle macchine virtuali e potrebbero non offrire prestazioni valide per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e448d-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="e448d-246">Impostazioni della cache su disco</span><span class="sxs-lookup"><span data-stu-id="e448d-246">Disk cache settings</span></span>

<span data-ttu-id="e448d-247">Sono disponibili tre opzioni per la memorizzazione nella cache dell'host:</span><span class="sxs-lookup"><span data-stu-id="e448d-247">There are three options for host caching:</span></span>

- <span data-ttu-id="e448d-248">*Sola lettura*: tutte le richieste sono memorizzate nella cache per le letture future.</span><span class="sxs-lookup"><span data-stu-id="e448d-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="e448d-249">Tutte le scritture vengono rese persistenti direttamente nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="e448d-249">All writes are persisted directly to Azure Blob storage.</span></span>

- <span data-ttu-id="e448d-250">*Lettura/scrittura*: si tratta di un algoritmo "read-ahead".</span><span class="sxs-lookup"><span data-stu-id="e448d-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="e448d-251">Le letture e le scritture sono memorizzate nella cache per le letture future.</span><span class="sxs-lookup"><span data-stu-id="e448d-251">The reads and writes are cached for future reads.</span></span> <span data-ttu-id="e448d-252">Le scritture non write-through sono rese persistenti prima nella cache locale.</span><span class="sxs-lookup"><span data-stu-id="e448d-252">Non-write-through writes are persisted to the local cache first.</span></span> <span data-ttu-id="e448d-253">Per SQL Server, le scritture sono rese persistenti in Archiviazione di Microsoft Azure perché usa le scritture write-through.</span><span class="sxs-lookup"><span data-stu-id="e448d-253">For SQL Server, writes are persisted to Azure Storage because it uses write-through.</span></span> <span data-ttu-id="e448d-254">Offre anche la latenza del disco più bassa per i carichi di lavoro leggeri.</span><span class="sxs-lookup"><span data-stu-id="e448d-254">It also provides the lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="e448d-255">*Nessuna* (disabilitata): usando questa opzione, è possibile ignorare la cache.</span><span class="sxs-lookup"><span data-stu-id="e448d-255">*None* (disabled): By using this option, you can bypass the cache.</span></span> <span data-ttu-id="e448d-256">Tutti i dati vengono trasferiti sul disco e resi persistenti in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e448d-256">All the data is transferred to disk and persisted to Azure Storage.</span></span> <span data-ttu-id="e448d-257">Questo metodo offre la massima frequenza di I/O per i carichi di lavoro con un uso intensivo dell'I/O.</span><span class="sxs-lookup"><span data-stu-id="e448d-257">This method gives you the highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="e448d-258">È anche necessario considerare il costo delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="e448d-258">You also need to take “transaction cost” into consideration.</span></span>

<span data-ttu-id="e448d-259">**Raccomandazioni**</span><span class="sxs-lookup"><span data-stu-id="e448d-259">**Recommendations**</span></span>

<span data-ttu-id="e448d-260">Per ottimizzare la velocità effettiva, è consigliabile iniziare con l'opzione **Nessuna** per la memorizzazione nella cache dell'host.</span><span class="sxs-lookup"><span data-stu-id="e448d-260">To maximize the throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="e448d-261">Per Archiviazione Premium, tenere presente che è necessario disabilitare le "barriere" quando si esegue il montaggio del file system con le opzioni **Sola lettura** o **Nessuna**.</span><span class="sxs-lookup"><span data-stu-id="e448d-261">For Premium Storage, keep in mind that you must disable the "barriers" when you mount the file system with the **ReadOnly** or **None** options.</span></span> <span data-ttu-id="e448d-262">Aggiornare il file /etc/fstab con l'UUID dei dischi.</span><span class="sxs-lookup"><span data-stu-id="e448d-262">Update the /etc/fstab file with the UUID to the disks.</span></span>

<span data-ttu-id="e448d-263">Per altre informazioni, vedere [Archiviazione Premium per VM Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span><span class="sxs-lookup"><span data-stu-id="e448d-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![Screenshot della pagina del disco gestito](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="e448d-265">Per i dischi del sistema operativo, usare la memorizzazione nella cache **Lettura/scrittura** predefinita.</span><span class="sxs-lookup"><span data-stu-id="e448d-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="e448d-266">Per SYSTEM, TEMP e UNDO usare **Nessuna** per la memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="e448d-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="e448d-267">Per DATA usare **Nessuna** per la memorizzazione nella cache,</span><span class="sxs-lookup"><span data-stu-id="e448d-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="e448d-268">ma se il database è di sola lettura o esegue un'intensa attività di lettura, usare la memorizzazione nella cache **Sola lettura**.</span><span class="sxs-lookup"><span data-stu-id="e448d-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="e448d-269">Dopo avere salvato l'impostazione del disco dati, non è possibile modificare l'impostazione della cache host, a meno che l'unità a livello di sistema operativo non venga smontata e quindi rimontata dopo avere apportato la modifica.</span><span class="sxs-lookup"><span data-stu-id="e448d-269">After your data disk setting is saved, you can't change the host cache setting unless you unmount the drive at the OS level and then remount it after you've made the change.</span></span>


## <a name="security"></a><span data-ttu-id="e448d-270">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="e448d-270">Security</span></span>

<span data-ttu-id="e448d-271">Dopo avere installato e configurato l'ambiente Azure, il passaggio successivo consiste nel proteggere la rete.</span><span class="sxs-lookup"><span data-stu-id="e448d-271">After you have set up and configured your Azure environment, the next step is to secure your network.</span></span> <span data-ttu-id="e448d-272">Di seguito sono elencati alcuni suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="e448d-272">Here are some recommendations:</span></span>

- <span data-ttu-id="e448d-273">*Criteri del gruppo di sicurezza di rete*: il gruppo di sicurezza di rete può essere definito da una subnet o una scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="e448d-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="e448d-274">È più semplice controllare l'accesso a livello di subnet per la sicurezza e forzare il routing per elementi come i firewall per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e448d-274">It's simpler to control access at the subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="e448d-275">*Jumpbox*: per una maggiore sicurezza dell'accesso, gli amministratori non devono connettersi direttamente al servizio dell'applicazione o al database.</span><span class="sxs-lookup"><span data-stu-id="e448d-275">*Jumpbox*: For more secure access, administrators should not directly connect to the application service or database.</span></span> <span data-ttu-id="e448d-276">Viene usato un jumpbox come elemento intermedio tra il computer dell'amministratore e le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e448d-276">A jumpbox is used as a media between the administrator machine and Azure resources.</span></span>
<span data-ttu-id="e448d-277">![Screenshot della pagina della topologia jumpbox](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="e448d-277">![Screenshot of the Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="e448d-278">Il computer dell'amministratore deve offrire accesso con restrizioni IP al solo jumpbox.</span><span class="sxs-lookup"><span data-stu-id="e448d-278">The administrator machine should offer IP-restricted access to the jumpbox only.</span></span> <span data-ttu-id="e448d-279">Il jumpbox deve avere accesso all'applicazione e al database.</span><span class="sxs-lookup"><span data-stu-id="e448d-279">The jumpbox should have access to the application and database.</span></span>

- <span data-ttu-id="e448d-280">*Rete privata* (subnet): è consigliabile tenere il servizio dell'applicazione e il database in subnet separate, per garantire un maggiore controllo ai criteri del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e448d-280">*Private network* (subnets): We recommend that you have the application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="e448d-281">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e448d-281">Additional reading</span></span>

- [<span data-ttu-id="e448d-282">Configurare Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="e448d-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="e448d-283">Configurare Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="e448d-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="e448d-284">Configurare Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="e448d-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="e448d-285">Backup e ripristino di Oracle</span><span class="sxs-lookup"><span data-stu-id="e448d-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="e448d-286">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e448d-286">Next steps</span></span>

- [<span data-ttu-id="e448d-287">Esercitazione: Creare VM a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="e448d-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="e448d-288">Esplorare gli esempi dell'interfaccia della riga di comando di Azure per la distribuzione della VM</span><span class="sxs-lookup"><span data-stu-id="e448d-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
