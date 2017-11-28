---
title: "Disponibilità di SAP HANA in macchine virtuali di Azure (VM) aaaHigh | Documenti Microsoft"
description: "Configurare la disponibilità elevata di SAP HANA in Macchine virtuali di Azure (VM)."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="5d7b2-103">Disponibilità elevata di SAP HANA in Macchine virtuali di Azure (VM)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="5d7b2-113">In locale, è possibile usare la replica di sistema HANA o archiviazione condivisa tooestablish la disponibilità elevata per SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-113">On-premises, you can use either HANA System Replication or use shared storage tooestablish high availability for SAP HANA.</span></span>
<span data-ttu-id="5d7b2-114">Attualmente è supportata solo l'impostazione della replica di sistema HANA in Azure.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="5d7b2-115">La replica SAP HANA è costituita da un nodo master e almeno un nodo slave.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="5d7b2-116">Modifiche toohello dati sul nodo principale hello vengono replicati nodi slave toohello in modo sincrono o asincrono.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-116">Changes toohello data on hello master node are replicated toohello slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="5d7b2-117">In questo articolo viene descritto come toodeploy hello macchine virtuali, configurare le macchine virtuali di hello, installare framework cluster hello, installare e configurare la replica di sistema di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-117">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="5d7b2-118">Nelle configurazioni di esempio hello, del numero di istanza e così via 03 i comandi di installazione e HANA sistema ID HDB viene utilizzata.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-118">In hello example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="5d7b2-119">Leggere hello seguenti prima di note su SAP e documenti</span><span class="sxs-lookup"><span data-stu-id="5d7b2-119">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="5d7b2-120">Nota SAP [1928533], contenente:</span><span class="sxs-lookup"><span data-stu-id="5d7b2-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="5d7b2-121">Elenco di dimensioni di macchina virtuale di Azure sono supportati per la distribuzione del software SAP hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-121">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="5d7b2-122">Importanti informazioni sulla capacità per le dimensioni delle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="5d7b2-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="5d7b2-123">Software SAP e combinazioni di sistemi operativi e database supportati</span><span class="sxs-lookup"><span data-stu-id="5d7b2-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="5d7b2-124">Versione del kernel SAP richiesta per Windows e Linux in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5d7b2-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="5d7b2-125">La nota SAP [2015553] elenca i prerequisiti per le distribuzioni di software SAP supportate da SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="5d7b2-126">La nota SAP [2205917] contiene le impostazioni consigliate del sistema operativo per SUSE Linux Enterprise Server for SAP Applications</span><span class="sxs-lookup"><span data-stu-id="5d7b2-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="5d7b2-127">La nota SAP [1944799] contiene linee guida per SAP HANA per SUSE Linux Enterprise Server for SAP Applications</span><span class="sxs-lookup"><span data-stu-id="5d7b2-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="5d7b2-128">La nota SAP [2178632] contiene informazioni dettagliate su tutte le metriche di monitoraggio segnalate per SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="5d7b2-129">Nota SAP [2191498] hello necessario versione dell'agente Host SAP per Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-129">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="5d7b2-130">La nota SAP [2243692] contiene informazioni sulle licenze SAP in Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="5d7b2-131">La nota SAP [1984787] contiene informazioni generali su SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="5d7b2-132">Nota SAP [1999351] contiene altre informazioni sulla risoluzione dei problemi per hello Azure Enhanced Monitoring Extension per SAP.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-132">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="5d7b2-133">[Community WIKI SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene tutte le note su SAP necessarie per Linux.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="5d7b2-134">[Pianificazione e implementazione di Macchine virtuali di Azure per SAP in Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="5d7b2-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="5d7b2-135">[Distribuzione di Macchine virtuali di Azure per SAP in Linux (questo articolo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="5d7b2-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="5d7b2-136">[Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="5d7b2-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="5d7b2-137">[SAP HANA SR prestazioni ottimizzate Scenario] [ suse-hana-ha-guide] Guida hello contiene tutte le informazioni necessarie tooset di SAP HANA sistema replica locale.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="5d7b2-138">Usare la guida per le indicazioni di base.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="5d7b2-139">Distribuzione di Linux</span><span class="sxs-lookup"><span data-stu-id="5d7b2-139">Deploying Linux</span></span>

<span data-ttu-id="5d7b2-140">agente di risorsa Hello per SAP HANA è incluso in SUSE Linux Enterprise Server per le applicazioni SAP.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-140">hello resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="5d7b2-141">Hello Azure Marketplace contiene un'immagine per SUSE Linux Enterprise Server per SAP applicazioni 12 con BYOS (portare il propria sottoscrizione) che è possibile utilizzare toodeploy nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-141">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use toodeploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="5d7b2-142">Distribuzione manuale</span><span class="sxs-lookup"><span data-stu-id="5d7b2-142">Manual Deployment</span></span>

1. <span data-ttu-id="5d7b2-143">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5d7b2-143">Create a Resource Group</span></span>
1. <span data-ttu-id="5d7b2-144">Creare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="5d7b2-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="5d7b2-145">Creare due account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="5d7b2-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="5d7b2-146">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="5d7b2-146">Create an Availability Set</span></span>  
   <span data-ttu-id="5d7b2-147">Impostare il numero massimo di domini di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="5d7b2-147">Set max update domain</span></span>
1. <span data-ttu-id="5d7b2-148">Creare un servizio di bilanciamento del carico (interno)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="5d7b2-149">Selezionare la rete virtuale del passaggio precedente</span><span class="sxs-lookup"><span data-stu-id="5d7b2-149">Select VNET of step above</span></span>
1. <span data-ttu-id="5d7b2-150">Creare la macchina virtuale 1</span><span class="sxs-lookup"><span data-stu-id="5d7b2-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="5d7b2-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="5d7b2-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="5d7b2-152">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="5d7b2-153">Selezionare l'account di archiviazione 1</span><span class="sxs-lookup"><span data-stu-id="5d7b2-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="5d7b2-154">Selezionare il set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="5d7b2-154">Select Availability Set</span></span>  
1. <span data-ttu-id="5d7b2-155">Creare la macchina virtuale 2</span><span class="sxs-lookup"><span data-stu-id="5d7b2-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="5d7b2-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="5d7b2-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="5d7b2-157">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="5d7b2-158">Selezionare l'account di archiviazione 2</span><span class="sxs-lookup"><span data-stu-id="5d7b2-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="5d7b2-159">Selezionare il set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="5d7b2-159">Select Availability Set</span></span>  
1. <span data-ttu-id="5d7b2-160">Aggiungere dischi dati</span><span class="sxs-lookup"><span data-stu-id="5d7b2-160">Add Data Disks</span></span>
1. <span data-ttu-id="5d7b2-161">Configurare il bilanciamento del carico hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-161">Configure hello load balancer</span></span>
    1. <span data-ttu-id="5d7b2-162">Creare un pool di indirizzi IP front-end</span><span class="sxs-lookup"><span data-stu-id="5d7b2-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="5d7b2-163">Aprire servizio di bilanciamento del carico hello, selezionare il pool IP front-end e fare clic su Aggiungi</span><span class="sxs-lookup"><span data-stu-id="5d7b2-163">Open hello load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="5d7b2-164">Immettere il nome di hello hello nuovo front-end del pool di IP (ad esempio hana-front-end)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-164">Enter hello name of hello new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="5d7b2-165">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-165">Click OK</span></span>
        1. <span data-ttu-id="5d7b2-166">Dopo aver creato il nuovo pool di IP front-end di hello, annotare il relativo indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="5d7b2-166">After hello new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="5d7b2-167">Creare un pool back-end</span><span class="sxs-lookup"><span data-stu-id="5d7b2-167">Create a backend pool</span></span>
        1. <span data-ttu-id="5d7b2-168">Aprire servizio di bilanciamento del carico hello, selezionare il pool back-end e fare clic su Aggiungi</span><span class="sxs-lookup"><span data-stu-id="5d7b2-168">Open hello load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="5d7b2-169">Immettere il nome di hello del pool back-end nuovo hello (ad esempio hana-back-end)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-169">Enter hello name of hello new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="5d7b2-170">Fare clic su Aggiungi una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="5d7b2-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="5d7b2-171">Selezionare i Set di disponibilità creato in precedenza hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-171">Select hello Availability Set you created earlier</span></span>
        1. <span data-ttu-id="5d7b2-172">Selezionare le macchine virtuali hello del cluster di SAP HANA hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-172">Select hello virtual machines of hello SAP HANA cluster</span></span>
        1. <span data-ttu-id="5d7b2-173">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-173">Click OK</span></span>
    1. <span data-ttu-id="5d7b2-174">Creare un probe di integrità</span><span class="sxs-lookup"><span data-stu-id="5d7b2-174">Create a health probe</span></span>
       1. <span data-ttu-id="5d7b2-175">Aprire hello bilanciamento del carico, selezionare i probe di integrità e fare clic su Aggiungi</span><span class="sxs-lookup"><span data-stu-id="5d7b2-175">Open hello load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="5d7b2-176">Immettere il nome di hello del probe di integrità nuovo hello (ad esempio hana hp)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-176">Enter hello name of hello new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="5d7b2-177">Selezionare TCP come protocollo, la porta 625**03**, mantenere 5 per Intervallo e impostare il valore di Soglia di non integrità su 2</span><span class="sxs-lookup"><span data-stu-id="5d7b2-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="5d7b2-178">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-178">Click OK</span></span>
    1. <span data-ttu-id="5d7b2-179">Creare le regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="5d7b2-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="5d7b2-180">Aprire servizio di bilanciamento del carico hello, selezionare regole di bilanciamento del carico e fare clic su Aggiungi</span><span class="sxs-lookup"><span data-stu-id="5d7b2-180">Open hello load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="5d7b2-181">Immettere il nome di hello della regola di bilanciamento del carico nuovo hello (ad esempio hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-181">Enter hello name of hello new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="5d7b2-182">Indirizzo IP di front-end Select hello, pool back-end e integrità probe è creato in precedenza (ad esempio hana-front-end)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-182">Select hello frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="5d7b2-183">Mantenere il protocollo TCP, immettere la porta 3**03**15</span><span class="sxs-lookup"><span data-stu-id="5d7b2-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="5d7b2-184">Aumentare il timeout di inattività too30 minuti</span><span class="sxs-lookup"><span data-stu-id="5d7b2-184">Increase idle timeout too30 minutes</span></span>
       1. <span data-ttu-id="5d7b2-185">**Verificare che tooenable IP mobile**</span><span class="sxs-lookup"><span data-stu-id="5d7b2-185">**Make sure tooenable Floating IP**</span></span>
        1. <span data-ttu-id="5d7b2-186">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-186">Click OK</span></span>
        1. <span data-ttu-id="5d7b2-187">Ripetere i passaggi di hello sopra per la porta 3**03**17</span><span class="sxs-lookup"><span data-stu-id="5d7b2-187">Repeat hello steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="5d7b2-188">Eseguire la distribuzione con un modello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-188">Deploy with template</span></span>
<span data-ttu-id="5d7b2-189">È possibile utilizzare uno dei modelli di avvio rapido hello in github toodeploy tutte le risorse necessarie.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-189">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="5d7b2-190">Consente di distribuire il modello di Hello hello le macchine virtuali, bilanciamento del carico hello, disponibilità, set e così via. Seguire questi modelli di hello toodeploy passaggi:</span><span class="sxs-lookup"><span data-stu-id="5d7b2-190">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="5d7b2-191">Aprire hello [modello di database] [ template-multisid-db] o hello [convergente modello] [ template-converged] nel portale di Azure hello hello database modello solo consente di creare hello regole di bilanciamento del carico per un database mentre hello convergente modello crea anche hello regole di bilanciamento del carico per un ASCS/SCS e un'istanza di Hiamanti (solo Linux).</span><span class="sxs-lookup"><span data-stu-id="5d7b2-191">Open hello [database template][template-multisid-db] or hello [converged template][template-converged] on hello Azure Portal hello database template only creates hello load-balancing rules for a database whereas hello converged template also creates hello load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="5d7b2-192">Se si prevede un sistema basate su SAP NetWeaver tooinstall e si desidera anche hello tooinstall ASCS/SCS istanza su hello stesso computer, utilizzare hello [convergente modello][template-converged].</span><span class="sxs-lookup"><span data-stu-id="5d7b2-192">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello ASCS/SCS instance on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="5d7b2-193">Immettere i seguenti parametri hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-193">Enter hello following parameters</span></span>
    1. <span data-ttu-id="5d7b2-194">ID sistema SAP</span><span class="sxs-lookup"><span data-stu-id="5d7b2-194">Sap System Id</span></span>  
       <span data-ttu-id="5d7b2-195">Immettere il sistema SAP hello Id di sistema SAP si desidera tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-195">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="5d7b2-196">Hello Id verrà considerato come prefisso per le risorse di hello che vengono distribuite.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-196">hello Id will be used as a prefix for hello resources that are deployed.</span></span>
    1. <span data-ttu-id="5d7b2-197">Tipo di stack (applicabile solo se si Usa modello convergente hello)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-197">Stack Type (only applicable if you use hello converged template)</span></span>  
       <span data-ttu-id="5d7b2-198">Selezionare tipo di stack hello SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="5d7b2-198">Select hello SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="5d7b2-199">Tipo di sistema operativo</span><span class="sxs-lookup"><span data-stu-id="5d7b2-199">Os Type</span></span>  
       <span data-ttu-id="5d7b2-200">Selezionare una delle distribuzioni di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-200">Select one of hello Linux distributions.</span></span> <span data-ttu-id="5d7b2-201">Per questo esempio, selezionare SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="5d7b2-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="5d7b2-202">Tipo di database</span><span class="sxs-lookup"><span data-stu-id="5d7b2-202">Db Type</span></span>  
       <span data-ttu-id="5d7b2-203">Selezionare HANA</span><span class="sxs-lookup"><span data-stu-id="5d7b2-203">Select HANA</span></span>
    1. <span data-ttu-id="5d7b2-204">Dimensioni del sistema SAP</span><span class="sxs-lookup"><span data-stu-id="5d7b2-204">Sap System Size</span></span>  
       <span data-ttu-id="5d7b2-205">quantità di Hello del nuovo sistema SAP hello fornirà.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-205">hello amount of SAPS hello new system will provide.</span></span> <span data-ttu-id="5d7b2-206">Se non si conoscono quanti valori SAPS hello sistema richiederà, chiedere il Partner di tecnologia di SAP o l'integratore di sistema</span><span class="sxs-lookup"><span data-stu-id="5d7b2-206">If you are not sure how many SAPS hello system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="5d7b2-207">Disponibilità del sistema</span><span class="sxs-lookup"><span data-stu-id="5d7b2-207">System Availability</span></span>  
       <span data-ttu-id="5d7b2-208">Selezionare la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-208">Select HA</span></span>
    1. <span data-ttu-id="5d7b2-209">Nome utente e password amministratore</span><span class="sxs-lookup"><span data-stu-id="5d7b2-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="5d7b2-210">Viene creato un nuovo utente che può essere utilizzato toolog toohello computer.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-210">A new user is created that can be used toolog on toohello machine.</span></span>
    1. <span data-ttu-id="5d7b2-211">Subnet nuova o esistente</span><span class="sxs-lookup"><span data-stu-id="5d7b2-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="5d7b2-212">Determina se devono essere create una nuova rete virtuale e una nuova subnet o deve essere usata una subnet esistente.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="5d7b2-213">Se si dispone già di una rete virtuale è una rete locale tooyour connesso, selezionare esistente.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-213">If you already have a virtual network that is connected tooyour on-premises network, select existing.</span></span>
    1. <span data-ttu-id="5d7b2-214">ID subnet</span><span class="sxs-lookup"><span data-stu-id="5d7b2-214">Subnet Id</span></span>  
    <span data-ttu-id="5d7b2-215">ID Hello delle macchine virtuali di hello subnet toowhich hello deve essere connessa a.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-215">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="5d7b2-216">Selezionare hello subnet della rete VPN o Express Route rete virtuale tooconnect hello macchina virtuale tooyour locale rete.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-216">Select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="5d7b2-217">ID Hello in genere è simile /Subscriptions/<ID`<subscription id`>/ResourceGroups /`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="5d7b2-217">hello ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="5d7b2-218">Configurazione della disponibilità elevata di Linux</span><span class="sxs-lookup"><span data-stu-id="5d7b2-218">Setting up Linux HA</span></span>

<span data-ttu-id="5d7b2-219">Hello seguenti elementi è preceduto da uno [A] - nodi tooall applicabile, toonode applicabile solo [1] - toonode applicabile solo 1 o [2] - 2.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-219">hello following items are prefixed with either [A] - applicable tooall nodes, [1] - only applicable toonode 1 or [2] - only applicable toonode 2.</span></span>

1. <span data-ttu-id="5d7b2-220">[A] SLES per SAP BYOS solo - repository hello toouse in grado di registrare SLES toobe</span><span class="sxs-lookup"><span data-stu-id="5d7b2-220">[A] SLES for SAP BYOS only - Register SLES toobe able toouse hello repositories</span></span>
1. <span data-ttu-id="5d7b2-221">[A] Solo SLES per SAP BYOS - Aggiungere il modulo cloud pubblico</span><span class="sxs-lookup"><span data-stu-id="5d7b2-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="5d7b2-222">[A] Aggiornare SLES</span><span class="sxs-lookup"><span data-stu-id="5d7b2-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="5d7b2-223">[1] Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="5d7b2-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="5d7b2-224">[2] Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="5d7b2-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="5d7b2-225">[1] Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="5d7b2-225">[1] Enable ssh access</span></span>
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="5d7b2-226">[A] Installare l'estensione per la disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="5d7b2-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="5d7b2-227">[A] Configurare il layout dei dischi</span><span class="sxs-lookup"><span data-stu-id="5d7b2-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="5d7b2-228">LVM</span><span class="sxs-lookup"><span data-stu-id="5d7b2-228">LVM</span></span>  
    <span data-ttu-id="5d7b2-229">In genere è consigliabile toouse LVM per volumi in cui archiviare i dati e i file di log.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-229">We generally recommend toouse LVM for volumes that store data and log files.</span></span> <span data-ttu-id="5d7b2-230">esempio Hello riportato di seguito presuppone che le macchine virtuali hello disponga di quattro dischi dati collegati che devono essere utilizzati toocreate due volumi.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-230">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
        * <span data-ttu-id="5d7b2-231">Creare volumi fisici per tutti i dischi che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-231">Create physical volumes for all disks that you want toouse.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="5d7b2-232">Creare un gruppo di volumi per il file di dati di hello, un gruppo di volumi per il file di log hello e una directory condivisa hello SAP HANA</span><span class="sxs-lookup"><span data-stu-id="5d7b2-232">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="5d7b2-233">Creare hello volumi logici</span><span class="sxs-lookup"><span data-stu-id="5d7b2-233">Create hello logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="5d7b2-234">Creare le directory di montaggio hello e copiare hello UUID di tutti i volumi logici</span><span class="sxs-lookup"><span data-stu-id="5d7b2-234">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="5d7b2-235">Creare le voci di fstab per hello tre volumi logici</span><span class="sxs-lookup"><span data-stu-id="5d7b2-235">Create fstab entries for hello three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="5d7b2-236">Inserire questa riga troppo/ecc/fstab</span><span class="sxs-lookup"><span data-stu-id="5d7b2-236">Insert this line too/etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="5d7b2-237">Montare i volumi di nuovo hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-237">Mount hello new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="5d7b2-238">Dischi normali</span><span class="sxs-lookup"><span data-stu-id="5d7b2-238">Plain Disks</span></span>  
       <span data-ttu-id="5d7b2-239">Per sistemi demo o di piccole dimensioni, è possibile inserire i dati e i file di log HANA su un disco.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="5d7b2-240">Hello seguenti comandi creare una partizione su /dev/sdc e formattarla con xfs.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-240">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a><span data-ttu-id="5d7b2-241">Annotare l'id di hello di /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="5d7b2-241">write down hello id of /dev/sdc1</span></span>
    <span data-ttu-id="5d7b2-242">sudo /sbin/blkid sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="5d7b2-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="5d7b2-243">[A] Configurare la risoluzione dei nomi host per tutti gli host</span><span class="sxs-lookup"><span data-stu-id="5d7b2-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="5d7b2-244">È possibile usare un server DNS o modificare /etc/hosts hello in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-244">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="5d7b2-245">Questo esempio mostra come toouse hello file /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-245">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="5d7b2-246">Sostituire l'indirizzo IP hello e nome host hello in hello seguenti comandi</span><span class="sxs-lookup"><span data-stu-id="5d7b2-246">Replace hello IP address and hello hostname in hello following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="5d7b2-247">Inserire hello seguenti righe troppo/ecc/host.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-247">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="5d7b2-248">Modificare l'ambiente di hello IP indirizzo e nome host toomatch</span><span class="sxs-lookup"><span data-stu-id="5d7b2-248">Change hello IP address and hostname toomatch your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="5d7b2-249">[1] Installare il cluster</span><span class="sxs-lookup"><span data-stu-id="5d7b2-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="5d7b2-250">[2] Aggiungi nodo toocluster</span><span class="sxs-lookup"><span data-stu-id="5d7b2-250">[2] Add node toocluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="5d7b2-251">[A] modifica di hacluster password toohello stessa password</span><span class="sxs-lookup"><span data-stu-id="5d7b2-251">[A] Change hacluster password toohello same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="5d7b2-252">[A] configurare corosync toouse altro trasporto e aggiungere nodelist.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-252">[A] Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="5d7b2-253">In caso contrario, il cluster non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="5d7b2-254">Aggiungere i seguenti file grassetto toohello contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-254">Add hello following bold content toohello file.</span></span>
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    <span data-ttu-id="5d7b2-255">Riavviare il servizio di corosync hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-255">Then restart hello corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="5d7b2-256">[A] Installare pacchetti HANA a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="5d7b2-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="5d7b2-257">Installazione di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="5d7b2-257">Installing SAP HANA</span></span>

<span data-ttu-id="5d7b2-258">Seguire il capitolo 4 di hello [SAP HANA SR prestazioni ottimizzate Scenario guide] [ suse-hana-ha-guide] tooinstall SAP HANA sistema di replica.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-258">Follow chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span>

1. <span data-ttu-id="5d7b2-259">[A] eseguire hdblcm da hello HANA DVD</span><span class="sxs-lookup"><span data-stu-id="5d7b2-259">[A] Run hdblcm from hello HANA DVD</span></span>
    * <span data-ttu-id="5d7b2-260">Scegliere l'installazione -> 1</span><span class="sxs-lookup"><span data-stu-id="5d7b2-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="5d7b2-261">Selezionare i componenti aggiuntivi per l'installazione -> 1</span><span class="sxs-lookup"><span data-stu-id="5d7b2-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="5d7b2-262">Immettere il percorso di installazione [/hana/shared]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-263">Immettere il nome host locale [..]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-264">Sistema di toohello tooadd ulteriori host si desidera?</span><span class="sxs-lookup"><span data-stu-id="5d7b2-264">Do you want tooadd additional hosts toohello system?</span></span> <span data-ttu-id="5d7b2-265">(y/n) [n]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-266">Immettere l'ID di sistema SAP HANA: <SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="5d7b2-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="5d7b2-267">Immettere il numero di istanza [00]:</span><span class="sxs-lookup"><span data-stu-id="5d7b2-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="5d7b2-268">Numero di istanza di HANA.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-268">HANA Instance number.</span></span> <span data-ttu-id="5d7b2-269">Utilizzare 03 se è utilizzato il modello di Azure hello o esempio hello sopra riportato di seguito</span><span class="sxs-lookup"><span data-stu-id="5d7b2-269">Use 03 if you used hello Azure Template or followed hello example above</span></span>
    * <span data-ttu-id="5d7b2-270">Selezionare la modalità di database/immettere l'indice [1]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-271">Selezionare l'utilizzo del sistema/immettere l'indice [4]:</span><span class="sxs-lookup"><span data-stu-id="5d7b2-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="5d7b2-272">Selezionare il sistema di hello utilizzo</span><span class="sxs-lookup"><span data-stu-id="5d7b2-272">Select hello system Usage</span></span>
    * <span data-ttu-id="5d7b2-273">Immettere il percorso dei volumi di dati [/hana/data/HDB]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-274">Immettere il percorso dei volumi di log [/hana/log/HDB]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-275">Limitare l'allocazione massima della memoria?</span><span class="sxs-lookup"><span data-stu-id="5d7b2-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="5d7b2-276">[n]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-277">Immettere nome Host del certificato per l'Host '...' […]: -> Invio</span><span class="sxs-lookup"><span data-stu-id="5d7b2-277">Enter Certificate Host Name For Host '...' [...]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-278">Immettere la password dell'utente agente host SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="5d7b2-278">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="5d7b2-279">Confermare la password dell'utente agente host SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="5d7b2-279">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="5d7b2-280">Immettere la password dell'amministratore di sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="5d7b2-280">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="5d7b2-281">Confermare la password dell'amministratore di sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="5d7b2-281">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="5d7b2-282">Immettere la home directory dell'amministratore di sistema [/usr/sap/HDB/home]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-282">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-283">Immettere la shell di accesso dell'amministratore di sistema [/bin/sh]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-283">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-284">Immettere l'ID utente dell'amministratore di sistema [1001]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-284">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-285">Immettere l'ID del gruppo di utenti (sapsys) [79]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-285">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-286">Immettere la password dell'utente del database (SYSTEM):</span><span class="sxs-lookup"><span data-stu-id="5d7b2-286">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="5d7b2-287">Confermare la password dell'utente del database (SYSTEM):</span><span class="sxs-lookup"><span data-stu-id="5d7b2-287">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="5d7b2-288">Riavviare il sistema dopo il riavvio della macchina?</span><span class="sxs-lookup"><span data-stu-id="5d7b2-288">Restart system after machine reboot?</span></span> <span data-ttu-id="5d7b2-289">[n]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="5d7b2-289">[n]: -> ENTER</span></span>
    * <span data-ttu-id="5d7b2-290">Si desidera toocontinue?</span><span class="sxs-lookup"><span data-stu-id="5d7b2-290">Do you want toocontinue?</span></span> <span data-ttu-id="5d7b2-291">(y/n):</span><span class="sxs-lookup"><span data-stu-id="5d7b2-291">(y/n):</span></span>  
  <span data-ttu-id="5d7b2-292">Convalidare hello riepilogo e immettere y toocontinue</span><span class="sxs-lookup"><span data-stu-id="5d7b2-292">Validate hello summary and enter y toocontinue</span></span>
1. <span data-ttu-id="5d7b2-293">[A] Aggiornare l'agente host SAP</span><span class="sxs-lookup"><span data-stu-id="5d7b2-293">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="5d7b2-294">Scaricare l'archivio agente Host SAP più recente hello da hello [SAP Softwarecenter] [ sap-swcenter] ed eseguiti hello seguenti comando tooupgrade hello agente.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-294">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="5d7b2-295">Sostituire hello percorso toohello archivio toopoint toohello file scaricato.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-295">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. <span data-ttu-id="5d7b2-296">[1] Creare la replica HANA (come radice)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-296">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="5d7b2-297">Eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-297">Run hello following command.</span></span> <span data-ttu-id="5d7b2-298">Verificare che tooreplace grassetto stringhe (HANA sistema ID HDB e numero di istanza 03) con valori di hello dell'installazione di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-298">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="5d7b2-299">[A] Creare una voce di archivio chiavi (come radice)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-299">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="5d7b2-300">[1] Eseguire il backup del database (come radice)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-300">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="5d7b2-301">[1] passare toohello sapsid utente (ad esempio hdbadm) e creare il sito primario di hello.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-301">[1] Switch toohello sapsid user (for example hdbadm) and create hello primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="5d7b2-302">[2] passare toohello sapsid utente (ad esempio hdbadm) e creare il sito secondario di hello.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-302">[2] Switch toohello sapsid user (for example hdbadm) and create hello secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="5d7b2-303">Configurare il framework del cluster</span><span class="sxs-lookup"><span data-stu-id="5d7b2-303">Configure Cluster Framework</span></span>

<span data-ttu-id="5d7b2-304">Modificare le impostazioni predefinite di hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-304">Change hello default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="5d7b2-305">ora di caricare cluster toohello di file hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-305">now we load hello file toohello cluster</span></span>
<span data-ttu-id="5d7b2-306">sudo crm configure load update crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="5d7b2-306">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="5d7b2-307">Creare il dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="5d7b2-307">Create STONITH device</span></span>

<span data-ttu-id="5d7b2-308">dispositivo STONITH Hello utilizza un tooauthorize dell'entità servizio in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-308">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="5d7b2-309">Seguire questi toocreate passaggi un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-309">Please follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="5d7b2-310">Andare troppo<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="5d7b2-310">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="5d7b2-311">Pannello di Azure Active Directory aprire hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-311">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="5d7b2-312">Passare tooProperties e annotare hello ID di Directory. Si tratta di hello **id tenant**.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-312">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="5d7b2-313">Fare clic su Registrazioni per l'app</span><span class="sxs-lookup"><span data-stu-id="5d7b2-313">Click App registrations</span></span>
1. <span data-ttu-id="5d7b2-314">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-314">Click Add</span></span>
1. <span data-ttu-id="5d7b2-315">Immettere un nome, selezionare il tipo di applicazione "App Web/API", immettere un URL di accesso (ad esempio http://localhost) e fare clic su Crea</span><span class="sxs-lookup"><span data-stu-id="5d7b2-315">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="5d7b2-316">URL Hello-sign-on non viene utilizzato e può essere un URL valido</span><span class="sxs-lookup"><span data-stu-id="5d7b2-316">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="5d7b2-317">Selezionare hello nuova App e fare clic su chiavi nella scheda Impostazioni hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-317">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="5d7b2-318">Immettere una descrizione per una nuova chiave, selezionare "Non scade mai" e fare clic su Salva</span><span class="sxs-lookup"><span data-stu-id="5d7b2-318">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="5d7b2-319">Annotare hello valore.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-319">Write down hello Value.</span></span> <span data-ttu-id="5d7b2-320">Viene utilizzato come hello **password** per hello dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="5d7b2-320">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="5d7b2-321">Annotare hello ID dell'applicazione. Viene utilizzato come nome utente di hello (**id di accesso** in seguito hello) di hello dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="5d7b2-321">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="5d7b2-322">Hello dell'entità servizio non dispone delle autorizzazioni tooaccess le risorse di Azure per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-322">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="5d7b2-323">È necessario toogive hello dell'entità servizio autorizzazioni toostart e l'arresto (deallocazione) tutte le macchine virtuali del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-323">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="5d7b2-324">Passare toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="5d7b2-324">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="5d7b2-325">Apri hello tutti pannello risorse</span><span class="sxs-lookup"><span data-stu-id="5d7b2-325">Open hello All resources blade</span></span>
1. <span data-ttu-id="5d7b2-326">Selezionare la macchina virtuale di hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-326">Select hello virtual machine</span></span>
1. <span data-ttu-id="5d7b2-327">Fare clic su Controllo di accesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="5d7b2-327">Click Access control (IAM)</span></span>
1. <span data-ttu-id="5d7b2-328">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-328">Click Add</span></span>
1. <span data-ttu-id="5d7b2-329">Selezionare il ruolo di hello proprietario</span><span class="sxs-lookup"><span data-stu-id="5d7b2-329">Select hello role Owner</span></span>
1. <span data-ttu-id="5d7b2-330">Immettere il nome di hello dell'applicazione hello creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="5d7b2-330">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="5d7b2-331">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-331">Click OK</span></span>

<span data-ttu-id="5d7b2-332">Dopo le autorizzazioni di hello per le macchine virtuali hello modificato, è possibile configurare i dispositivi STONITH hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-332">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="5d7b2-333">ora di caricare cluster toohello di file hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-333">now we load hello file toohello cluster</span></span>
<span data-ttu-id="5d7b2-334">sudo crm configure load update crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="5d7b2-334">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="5d7b2-335">Creare risorse SAP HANA</span><span class="sxs-lookup"><span data-stu-id="5d7b2-335">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="5d7b2-336">ora di caricare cluster toohello di file hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-336">now we load hello file toohello cluster</span></span>
<span data-ttu-id="5d7b2-337">sudo crm configure load update crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="5d7b2-337">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="5d7b2-338">ora di caricare cluster toohello di file hello</span><span class="sxs-lookup"><span data-stu-id="5d7b2-338">now we load hello file toohello cluster</span></span>
<span data-ttu-id="5d7b2-339">sudo crm configure load update crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="5d7b2-339">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="5d7b2-340">Testare la configurazione del cluster</span><span class="sxs-lookup"><span data-stu-id="5d7b2-340">Test cluster setup</span></span>
<span data-ttu-id="5d7b2-341">Hello seguente capitolo viene descritto come è possibile testare il programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-341">hello following chapter describe how you can test your setup.</span></span> <span data-ttu-id="5d7b2-342">Ogni test si presuppone che sono radice e master di SAP HANA hello è in esecuzione in hello saphanavm1 di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-342">Every test assumes that you are root and hello SAP HANA master is running on hello virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="5d7b2-343">Test di isolamento</span><span class="sxs-lookup"><span data-stu-id="5d7b2-343">Fencing Test</span></span>

<span data-ttu-id="5d7b2-344">È possibile verificare l'installazione di hello dell'agente fencing hello disabilitando l'interfaccia di rete hello saphanavm1 nodo.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-344">You can test hello setup of hello fencing agent by disabling hello network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="5d7b2-345">macchina virtuale Hello deve ora ottenere riavviato o arrestato a seconda della configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-345">hello virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="5d7b2-346">Se si imposta toooff stonith azione hello, macchina virtuale hello verrà arrestato e risorse hello toohello migrato in esecuzione sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-346">If you set hello stonith-action toooff, hello virtual machine will be stopped and hello resources are migrated toohello running virtual machine.</span></span>

<span data-ttu-id="5d7b2-347">Quando si avvia macchina virtuale hello nuovamente, hello risorse SAP HANA avrà esito negativo toostart come database secondario se si imposta AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="5d7b2-347">Once you start hello virtual machine again, hello SAP HANA resource will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="5d7b2-348">In questo caso, è necessario tooconfigure hello HANA istanza secondaria eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5d7b2-348">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="5d7b2-349">Test di un failover manuale</span><span class="sxs-lookup"><span data-stu-id="5d7b2-349">Testing a manual failover</span></span>

<span data-ttu-id="5d7b2-350">È possibile testare un failover manuale per l'arresto del servizio di pacemaker hello nel nodo saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-350">You can test a manual failover by stopping hello pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="5d7b2-351">Dopo il failover hello, è possibile avviare il servizio hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-351">After hello failover, you can start hello service again.</span></span> <span data-ttu-id="5d7b2-352">Hello risorse SAP HANA in saphanavm1 avrà esito negativo toostart come database secondario se si imposta AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="5d7b2-352">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="5d7b2-353">In questo caso, è necessario tooconfigure hello HANA istanza secondaria eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5d7b2-353">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="5d7b2-354">Test di una migrazione</span><span class="sxs-lookup"><span data-stu-id="5d7b2-354">Testing a migration</span></span>

<span data-ttu-id="5d7b2-355">È possibile eseguire la migrazione di nodo principale di SAP HANA hello eseguendo hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="5d7b2-355">You can migrate hello SAP HANA master node by executing hello following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="5d7b2-356">Si deve eseguire la migrazione di nodo principale di SAP HANA hello e gruppo hello contenente toosaphanavm2 di indirizzo IP virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-356">This should migrate hello SAP HANA master node and hello group that contains hello virtual IP address toosaphanavm2.</span></span>
<span data-ttu-id="5d7b2-357">Hello risorse SAP HANA in saphanavm1 avrà esito negativo toostart come database secondario se si imposta AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="5d7b2-357">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="5d7b2-358">In questo caso, è necessario tooconfigure hello HANA istanza secondaria eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5d7b2-358">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="5d7b2-359">la migrazione di Hello crea vincoli di percorso che è necessario toobe nuovamente.</span><span class="sxs-lookup"><span data-stu-id="5d7b2-359">hello migration creates location contraints that need toobe deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="5d7b2-360">È inoltre necessario stato hello toocleanup della risorsa di hello nodo secondario</span><span class="sxs-lookup"><span data-stu-id="5d7b2-360">You also need toocleanup hello state of hello secondary node resource</span></span>

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="5d7b2-361">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d7b2-361">Next steps</span></span>
* <span data-ttu-id="5d7b2-362">[Pianificazione e implementazione di Macchine virtuali di Azure per SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="5d7b2-362">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="5d7b2-363">[Distribuzione di Macchine virtuali di Azure per SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="5d7b2-363">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="5d7b2-364">[Distribuzione DBMS di Macchine virtuali di Azure per SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="5d7b2-364">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="5d7b2-365">toolearn tooestablish la disponibilità elevata e piano di ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni), vedere [SAP HANA (istanze di grandi dimensioni) ad alto disponibilità e ripristino di emergenza in Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="5d7b2-365">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
