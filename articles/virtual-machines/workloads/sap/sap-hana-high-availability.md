---
title: "Disponibilità elevata di SAP HANA in Macchine virtuali di Azure (VM) | Microsoft Docs"
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
ms.openlocfilehash: 951150e621d21037b0adde7287b9f985290d8d11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="2d785-103">Disponibilità elevata di SAP HANA in Macchine virtuali di Azure (VM)</span><span class="sxs-lookup"><span data-stu-id="2d785-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="2d785-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="2d785-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="2d785-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="2d785-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="2d785-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="2d785-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="2d785-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="2d785-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="2d785-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="2d785-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="2d785-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="2d785-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="2d785-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="2d785-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="2d785-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="2d785-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="2d785-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="2d785-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="2d785-113">In locale è possibile usare la replica di sistema HANA oppure l'archiviazione condivisa per stabilire la disponibilità elevata per SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="2d785-113">On-premises, you can use either HANA System Replication or use shared storage to establish high availability for SAP HANA.</span></span>
<span data-ttu-id="2d785-114">Attualmente è supportata solo l'impostazione della replica di sistema HANA in Azure.</span><span class="sxs-lookup"><span data-stu-id="2d785-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="2d785-115">La replica SAP HANA è costituita da un nodo master e almeno un nodo slave.</span><span class="sxs-lookup"><span data-stu-id="2d785-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="2d785-116">Le modifiche ai dati nel nodo master vengono replicate nei nodi slave in modo sincrono o asincrono.</span><span class="sxs-lookup"><span data-stu-id="2d785-116">Changes to the data on the master node are replicated to the slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="2d785-117">Questo articolo descrive come distribuire le macchine virtuali, configurare le macchine virtuali, installare il framework del cluster e installare e configurare la replica di sistema SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="2d785-117">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="2d785-118">Nelle configurazioni di esempio, nei comandi di installazione e così via vengono usati il numero di istanza 03 e l'ID di sistema HANA HDB.</span><span class="sxs-lookup"><span data-stu-id="2d785-118">In the example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="2d785-119">Leggere prima di tutto le note e i documenti seguenti relativi a SAP</span><span class="sxs-lookup"><span data-stu-id="2d785-119">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="2d785-120">Nota SAP [1928533], contenente:</span><span class="sxs-lookup"><span data-stu-id="2d785-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="2d785-121">Elenco delle dimensioni delle VM di Azure supportate per la distribuzione di software SAP</span><span class="sxs-lookup"><span data-stu-id="2d785-121">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="2d785-122">Importanti informazioni sulla capacità per le dimensioni delle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="2d785-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="2d785-123">Software SAP e combinazioni di sistemi operativi e database supportati</span><span class="sxs-lookup"><span data-stu-id="2d785-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="2d785-124">Versione del kernel SAP richiesta per Windows e Linux in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2d785-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="2d785-125">La nota SAP [2015553] elenca i prerequisiti per le distribuzioni di software SAP supportate da SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="2d785-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="2d785-126">La nota SAP [2205917] contiene le impostazioni consigliate del sistema operativo per SUSE Linux Enterprise Server for SAP Applications</span><span class="sxs-lookup"><span data-stu-id="2d785-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="2d785-127">La nota SAP [1944799] contiene linee guida per SAP HANA per SUSE Linux Enterprise Server for SAP Applications</span><span class="sxs-lookup"><span data-stu-id="2d785-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="2d785-128">La nota SAP [2178632] contiene informazioni dettagliate su tutte le metriche di monitoraggio segnalate per SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="2d785-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="2d785-129">La nota SAP [2191498] contiene la versione dell'agente host SAP per Linux necessaria in Azure.</span><span class="sxs-lookup"><span data-stu-id="2d785-129">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="2d785-130">La nota SAP [2243692] contiene informazioni sulle licenze SAP in Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="2d785-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="2d785-131">La nota SAP [1984787] contiene informazioni generali su SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="2d785-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="2d785-132">La nota SAP [1999351] contiene informazioni aggiuntive sulla risoluzione dei problemi per l'estensione di monitoraggio avanzato di Azure per SAP.</span><span class="sxs-lookup"><span data-stu-id="2d785-132">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="2d785-133">[Community WIKI SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene tutte le note su SAP necessarie per Linux.</span><span class="sxs-lookup"><span data-stu-id="2d785-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="2d785-134">[Pianificazione e implementazione di Macchine virtuali di Azure per SAP in Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="2d785-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="2d785-135">[Distribuzione di Macchine virtuali di Azure per SAP in Linux (questo articolo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="2d785-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="2d785-136">[Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="2d785-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="2d785-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] (Scenario ottimizzato per le prestazioni di SAP HANA SR) La guida contiene tutte le informazioni necessarie per configurare la replica di sistema SAP HANA in locale.</span><span class="sxs-lookup"><span data-stu-id="2d785-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="2d785-138">Usare la guida per le indicazioni di base.</span><span class="sxs-lookup"><span data-stu-id="2d785-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="2d785-139">Distribuzione di Linux</span><span class="sxs-lookup"><span data-stu-id="2d785-139">Deploying Linux</span></span>

<span data-ttu-id="2d785-140">L'agente delle risorse per SAP HANA è incluso in SUSE Linux Enterprise Server for SAP Applications.</span><span class="sxs-lookup"><span data-stu-id="2d785-140">The resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="2d785-141">Azure Marketplace contiene un'immagine per SUSE Linux Enterprise Server for SAP Applications 12 con BYOS (Bring Your Own Subscription) che è possibile usare per distribuire nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="2d785-141">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use to deploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="2d785-142">Distribuzione manuale</span><span class="sxs-lookup"><span data-stu-id="2d785-142">Manual Deployment</span></span>

1. <span data-ttu-id="2d785-143">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="2d785-143">Create a Resource Group</span></span>
1. <span data-ttu-id="2d785-144">Creare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="2d785-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="2d785-145">Creare due account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="2d785-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="2d785-146">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="2d785-146">Create an Availability Set</span></span>  
   <span data-ttu-id="2d785-147">Impostare il numero massimo di domini di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="2d785-147">Set max update domain</span></span>
1. <span data-ttu-id="2d785-148">Creare un servizio di bilanciamento del carico (interno)</span><span class="sxs-lookup"><span data-stu-id="2d785-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="2d785-149">Selezionare la rete virtuale del passaggio precedente</span><span class="sxs-lookup"><span data-stu-id="2d785-149">Select VNET of step above</span></span>
1. <span data-ttu-id="2d785-150">Creare la macchina virtuale 1</span><span class="sxs-lookup"><span data-stu-id="2d785-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="2d785-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="2d785-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="2d785-152">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="2d785-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="2d785-153">Selezionare l'account di archiviazione 1</span><span class="sxs-lookup"><span data-stu-id="2d785-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="2d785-154">Selezionare il set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="2d785-154">Select Availability Set</span></span>  
1. <span data-ttu-id="2d785-155">Creare la macchina virtuale 2</span><span class="sxs-lookup"><span data-stu-id="2d785-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="2d785-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="2d785-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="2d785-157">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="2d785-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="2d785-158">Selezionare l'account di archiviazione 2</span><span class="sxs-lookup"><span data-stu-id="2d785-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="2d785-159">Selezionare il set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="2d785-159">Select Availability Set</span></span>  
1. <span data-ttu-id="2d785-160">Aggiungere dischi dati</span><span class="sxs-lookup"><span data-stu-id="2d785-160">Add Data Disks</span></span>
1. <span data-ttu-id="2d785-161">Configurare il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="2d785-161">Configure the load balancer</span></span>
    1. <span data-ttu-id="2d785-162">Creare un pool di indirizzi IP front-end</span><span class="sxs-lookup"><span data-stu-id="2d785-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="2d785-163">Aprire il servizio di bilanciamento del carico, selezionare Pool di indirizzi IP front-end e fare clic su Aggiungi</span><span class="sxs-lookup"><span data-stu-id="2d785-163">Open the load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="2d785-164">Immettere il nome del nuovo pool di indirizzi IP front-end (ad esempio, hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="2d785-164">Enter the name of the new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="2d785-165">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="2d785-165">Click OK</span></span>
        1. <span data-ttu-id="2d785-166">Dopo aver creato il nuovo pool di indirizzi IP front-end, annotare il relativo indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="2d785-166">After the new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="2d785-167">Creare un pool back-end</span><span class="sxs-lookup"><span data-stu-id="2d785-167">Create a backend pool</span></span>
        1. <span data-ttu-id="2d785-168">Aprire il servizio di bilanciamento del carico, selezionare Pool back-end e fare clic su Aggiungi</span><span class="sxs-lookup"><span data-stu-id="2d785-168">Open the load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="2d785-169">Immettere il nome del nuovo pool back-end (ad esempio, hana-backend)</span><span class="sxs-lookup"><span data-stu-id="2d785-169">Enter the name of the new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="2d785-170">Fare clic su Aggiungi una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2d785-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="2d785-171">Selezionare il set di disponibilità creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="2d785-171">Select the Availability Set you created earlier</span></span>
        1. <span data-ttu-id="2d785-172">Selezionare le macchine virtuali del cluster SAP HANA</span><span class="sxs-lookup"><span data-stu-id="2d785-172">Select the virtual machines of the SAP HANA cluster</span></span>
        1. <span data-ttu-id="2d785-173">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="2d785-173">Click OK</span></span>
    1. <span data-ttu-id="2d785-174">Creare un probe di integrità</span><span class="sxs-lookup"><span data-stu-id="2d785-174">Create a health probe</span></span>
       1. <span data-ttu-id="2d785-175">Aprire il servizio di bilanciamento del carico, selezionare Probe integrità e fare clic su Aggiungi</span><span class="sxs-lookup"><span data-stu-id="2d785-175">Open the load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="2d785-176">Immettere il nome del nuovo probe integrità (ad esempio, hana-hp)</span><span class="sxs-lookup"><span data-stu-id="2d785-176">Enter the name of the new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="2d785-177">Selezionare TCP come protocollo, la porta 625**03**, mantenere 5 per Intervallo e impostare il valore di Soglia di non integrità su 2</span><span class="sxs-lookup"><span data-stu-id="2d785-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="2d785-178">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="2d785-178">Click OK</span></span>
    1. <span data-ttu-id="2d785-179">Creare le regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="2d785-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="2d785-180">Aprire il servizio di bilanciamento del carico, selezionare Regole di bilanciamento del carico e fare clic su Aggiungi</span><span class="sxs-lookup"><span data-stu-id="2d785-180">Open the load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="2d785-181">Immettere il nome della nuova regola di bilanciamento del carico (ad esempio, hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="2d785-181">Enter the name of the new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="2d785-182">Selezionare l'indirizzo IP front-end, il pool back-end e il probe integrità creati in precedenza (ad esempio, hana-frontend)</span><span class="sxs-lookup"><span data-stu-id="2d785-182">Select the frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="2d785-183">Mantenere il protocollo TCP, immettere la porta 3**03**15</span><span class="sxs-lookup"><span data-stu-id="2d785-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="2d785-184">Aumentare il timeout di inattività a 30 minuti</span><span class="sxs-lookup"><span data-stu-id="2d785-184">Increase idle timeout to 30 minutes</span></span>
       1. <span data-ttu-id="2d785-185">**Assicurarsi di abilitare l'indirizzo IP mobile**</span><span class="sxs-lookup"><span data-stu-id="2d785-185">**Make sure to enable Floating IP**</span></span>
        1. <span data-ttu-id="2d785-186">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="2d785-186">Click OK</span></span>
        1. <span data-ttu-id="2d785-187">Ripetere i passaggi precedenti per la porta 3**03**17</span><span class="sxs-lookup"><span data-stu-id="2d785-187">Repeat the steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="2d785-188">Eseguire la distribuzione con un modello</span><span class="sxs-lookup"><span data-stu-id="2d785-188">Deploy with template</span></span>
<span data-ttu-id="2d785-189">È possibile usare uno dei modelli di avvio rapido di GitHub per distribuire tutte le risorse necessarie.</span><span class="sxs-lookup"><span data-stu-id="2d785-189">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="2d785-190">Il modello consente di distribuire le macchine virtuali, il servizio di bilanciamento del carico, il set di disponibilità e così via. Per distribuire il modello, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="2d785-190">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="2d785-191">Aprire il [modello di database][template-multisid-db] o il [modello con convergenza][template-converged] nel portale di Azure. Il modello di database consente di creare solo le regole di bilanciamento del carico per un database, mentre il modello con convergenza crea anche le regole di bilanciamento del carico per un'istanza di ASCS/SCS ed ERS (solo Linux).</span><span class="sxs-lookup"><span data-stu-id="2d785-191">Open the [database template][template-multisid-db] or the [converged template][template-converged] on the Azure Portal The database template only creates the load-balancing rules for a database whereas the converged template also creates the load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="2d785-192">Se si prevede di installare un sistema basato su SAP NetWeaver e si vuole installare anche l'istanza di ASCS/SCS nelle stesse macchine, usare il [modello con convergenza][template-converged].</span><span class="sxs-lookup"><span data-stu-id="2d785-192">If you plan to install an SAP NetWeaver based system and you also want to install the ASCS/SCS instance on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="2d785-193">Immettere i parametri seguenti</span><span class="sxs-lookup"><span data-stu-id="2d785-193">Enter the following parameters</span></span>
    1. <span data-ttu-id="2d785-194">ID sistema SAP</span><span class="sxs-lookup"><span data-stu-id="2d785-194">Sap System Id</span></span>  
       <span data-ttu-id="2d785-195">Immettere l'ID del sistema SAP che si vuole installare.</span><span class="sxs-lookup"><span data-stu-id="2d785-195">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="2d785-196">L'ID verrà usato come prefisso per le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="2d785-196">The Id will be used as a prefix for the resources that are deployed.</span></span>
    1. <span data-ttu-id="2d785-197">Tipo di stack (applicabile solo se si usa il modello con convergenza)</span><span class="sxs-lookup"><span data-stu-id="2d785-197">Stack Type (only applicable if you use the converged template)</span></span>  
       <span data-ttu-id="2d785-198">Selezionare il tipo di stack SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="2d785-198">Select the SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="2d785-199">Tipo di sistema operativo</span><span class="sxs-lookup"><span data-stu-id="2d785-199">Os Type</span></span>  
       <span data-ttu-id="2d785-200">Selezionare una delle distribuzioni Linux.</span><span class="sxs-lookup"><span data-stu-id="2d785-200">Select one of the Linux distributions.</span></span> <span data-ttu-id="2d785-201">Per questo esempio, selezionare SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="2d785-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="2d785-202">Tipo di database</span><span class="sxs-lookup"><span data-stu-id="2d785-202">Db Type</span></span>  
       <span data-ttu-id="2d785-203">Selezionare HANA</span><span class="sxs-lookup"><span data-stu-id="2d785-203">Select HANA</span></span>
    1. <span data-ttu-id="2d785-204">Dimensioni del sistema SAP</span><span class="sxs-lookup"><span data-stu-id="2d785-204">Sap System Size</span></span>  
       <span data-ttu-id="2d785-205">Quantità di SAPS forniti dal nuovo sistema.</span><span class="sxs-lookup"><span data-stu-id="2d785-205">The amount of SAPS the new system will provide.</span></span> <span data-ttu-id="2d785-206">Se non si è certi del numero di SAPS necessari per il sistema, chiedere all'integratore di sistemi o al partner tecnologico SAP</span><span class="sxs-lookup"><span data-stu-id="2d785-206">If you are not sure how many SAPS the system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="2d785-207">Disponibilità del sistema</span><span class="sxs-lookup"><span data-stu-id="2d785-207">System Availability</span></span>  
       <span data-ttu-id="2d785-208">Selezionare la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="2d785-208">Select HA</span></span>
    1. <span data-ttu-id="2d785-209">Nome utente e password amministratore</span><span class="sxs-lookup"><span data-stu-id="2d785-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="2d785-210">Verrà creato un nuovo utente con cui è possibile accedere alla macchina</span><span class="sxs-lookup"><span data-stu-id="2d785-210">A new user is created that can be used to log on to the machine.</span></span>
    1. <span data-ttu-id="2d785-211">Subnet nuova o esistente</span><span class="sxs-lookup"><span data-stu-id="2d785-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="2d785-212">Determina se devono essere create una nuova rete virtuale e una nuova subnet o deve essere usata una subnet esistente.</span><span class="sxs-lookup"><span data-stu-id="2d785-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="2d785-213">Se è già presente una rete virtuale connessa alla rete locale, selezionare "existing".</span><span class="sxs-lookup"><span data-stu-id="2d785-213">If you already have a virtual network that is connected to your on-premises network, select existing.</span></span>
    1. <span data-ttu-id="2d785-214">ID subnet</span><span class="sxs-lookup"><span data-stu-id="2d785-214">Subnet Id</span></span>  
    <span data-ttu-id="2d785-215">ID della subnet a cui devono essere connesse le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="2d785-215">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="2d785-216">Selezionare la subnet della rete virtuale Express Route o VPN per connettere la macchina virtuale alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="2d785-216">Select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="2d785-217">L'ID si presenta in genere come segue: /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="2d785-217">The ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="2d785-218">Configurazione della disponibilità elevata di Linux</span><span class="sxs-lookup"><span data-stu-id="2d785-218">Setting up Linux HA</span></span>

<span data-ttu-id="2d785-219">Gli elementi seguenti sono preceduti dall'indicazione [A] - applicabile a tutti i nodi, [1] - applicabile solo al nodo 1 o [2] - applicabile solo al nodo 2.</span><span class="sxs-lookup"><span data-stu-id="2d785-219">The following items are prefixed with either [A] - applicable to all nodes, [1] - only applicable to node 1 or [2] - only applicable to node 2.</span></span>

1. <span data-ttu-id="2d785-220">[A] Solo SLES per SAP BYOS - Registrare SLES per poter usare i repository</span><span class="sxs-lookup"><span data-stu-id="2d785-220">[A] SLES for SAP BYOS only - Register SLES to be able to use the repositories</span></span>
1. <span data-ttu-id="2d785-221">[A] Solo SLES per SAP BYOS - Aggiungere il modulo cloud pubblico</span><span class="sxs-lookup"><span data-stu-id="2d785-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="2d785-222">[A] Aggiornare SLES</span><span class="sxs-lookup"><span data-stu-id="2d785-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="2d785-223">[1] Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="2d785-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="2d785-224">[2] Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="2d785-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert the public key you copied in the last step into the authorized keys file on the second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="2d785-225">[1] Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="2d785-225">[1] Enable ssh access</span></span>
    ```bash
    # insert the public key you copied in the last step into the authorized keys file on the first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="2d785-226">[A] Installare l'estensione per la disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="2d785-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="2d785-227">[A] Configurare il layout dei dischi</span><span class="sxs-lookup"><span data-stu-id="2d785-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="2d785-228">LVM</span><span class="sxs-lookup"><span data-stu-id="2d785-228">LVM</span></span>  
    <span data-ttu-id="2d785-229">In genere è consigliabile usare LVM per i volumi che archiviano i dati e file di log.</span><span class="sxs-lookup"><span data-stu-id="2d785-229">We generally recommend to use LVM for volumes that store data and log files.</span></span> <span data-ttu-id="2d785-230">L'esempio seguente presuppone che le macchine virtuali abbiano quattro dischi dati collegati che devono essere usati per creare due volumi.</span><span class="sxs-lookup"><span data-stu-id="2d785-230">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
        * <span data-ttu-id="2d785-231">Creare i volumi fisici per tutti i dischi da usare.</span><span class="sxs-lookup"><span data-stu-id="2d785-231">Create physical volumes for all disks that you want to use.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="2d785-232">Creare un gruppo di volumi per i file di dati, un gruppo di volumi per i file di log e uno per la directory condivisa di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="2d785-232">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="2d785-233">Creare i volumi logici</span><span class="sxs-lookup"><span data-stu-id="2d785-233">Create the logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="2d785-234">Creare le directory di montaggio e copiare l'UUID di tutti i volumi logici</span><span class="sxs-lookup"><span data-stu-id="2d785-234">Create the mount directories and copy the UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="2d785-235">Creare voci fstab per i tre volumi logici</span><span class="sxs-lookup"><span data-stu-id="2d785-235">Create fstab entries for the three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="2d785-236">Inserire questa riga in /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="2d785-236">Insert this line to /etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="2d785-237">Montare i nuovi volumi</span><span class="sxs-lookup"><span data-stu-id="2d785-237">Mount the new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="2d785-238">Dischi normali</span><span class="sxs-lookup"><span data-stu-id="2d785-238">Plain Disks</span></span>  
       <span data-ttu-id="2d785-239">Per sistemi demo o di piccole dimensioni, è possibile inserire i dati e i file di log HANA su un disco.</span><span class="sxs-lookup"><span data-stu-id="2d785-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="2d785-240">I comandi seguenti creano una partizione in /dev/sdc e la formattano con XFS.</span><span class="sxs-lookup"><span data-stu-id="2d785-240">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-the-id-of-devsdc1"></a><span data-ttu-id="2d785-241">Annotare l'ID di /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="2d785-241">write down the id of /dev/sdc1</span></span>
    <span data-ttu-id="2d785-242">sudo /sbin/blkid sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="2d785-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line to /etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create the target directory and mount the disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="2d785-243">[A] Configurare la risoluzione dei nomi host per tutti gli host</span><span class="sxs-lookup"><span data-stu-id="2d785-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="2d785-244">È possibile usare un server DNS o modificare /etc/hosts in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="2d785-244">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="2d785-245">Questo esempio mostra come usare il file /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="2d785-245">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="2d785-246">Sostituire l'indirizzo IP e il nome host nei comandi seguenti</span><span class="sxs-lookup"><span data-stu-id="2d785-246">Replace the IP address and the hostname in the following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="2d785-247">Inserire le righe seguenti in /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="2d785-247">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="2d785-248">Modificare l'indirizzo IP e il nome host in base all'ambiente</span><span class="sxs-lookup"><span data-stu-id="2d785-248">Change the IP address and hostname to match your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="2d785-249">[1] Installare il cluster</span><span class="sxs-lookup"><span data-stu-id="2d785-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want to continue anyway? [y/N] -> y
    # Network address to bind to (e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish to use SBD? [y/N] -> N
    # Do you wish to configure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="2d785-250">[2] Aggiungere un nodo al cluster</span><span class="sxs-lookup"><span data-stu-id="2d785-250">[2] Add node to cluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured to start at system boot.
    # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
    # Do you want to continue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="2d785-251">[A] Modificare la password hacluster in modo in modo da usare la stessa password</span><span class="sxs-lookup"><span data-stu-id="2d785-251">[A] Change hacluster password to the same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="2d785-252">[A] Configurare corosync per usare un altro trasporto e aggiungere nodelist.</span><span class="sxs-lookup"><span data-stu-id="2d785-252">[A] Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="2d785-253">In caso contrario, il cluster non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="2d785-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="2d785-254">Aggiungere il seguente contenuto in grassetto nel file.</span><span class="sxs-lookup"><span data-stu-id="2d785-254">Add the following bold content to the file.</span></span>
    
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

    <span data-ttu-id="2d785-255">Riavviare quindi il servizio corosync</span><span class="sxs-lookup"><span data-stu-id="2d785-255">Then restart the corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="2d785-256">[A] Installare pacchetti HANA a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="2d785-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="2d785-257">Installazione di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="2d785-257">Installing SAP HANA</span></span>

<span data-ttu-id="2d785-258">Seguire il capitolo 4 della guida [SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] (Scenario di ottimizzazione delle prestazioni di SAP HANA SR) per installare la replica di sistema di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="2d785-258">Follow chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span>

1. <span data-ttu-id="2d785-259">[A] Eseguire hdblcm dal DVD di HANA</span><span class="sxs-lookup"><span data-stu-id="2d785-259">[A] Run hdblcm from the HANA DVD</span></span>
    * <span data-ttu-id="2d785-260">Scegliere l'installazione -> 1</span><span class="sxs-lookup"><span data-stu-id="2d785-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="2d785-261">Selezionare i componenti aggiuntivi per l'installazione -> 1</span><span class="sxs-lookup"><span data-stu-id="2d785-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="2d785-262">Immettere il percorso di installazione [/hana/shared]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-263">Immettere il nome host locale [..]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-264">Aggiungere altri host al sistema?</span><span class="sxs-lookup"><span data-stu-id="2d785-264">Do you want to add additional hosts to the system?</span></span> <span data-ttu-id="2d785-265">(y/n) [n]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-266">Immettere l'ID di sistema SAP HANA: <SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="2d785-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="2d785-267">Immettere il numero di istanza [00]:</span><span class="sxs-lookup"><span data-stu-id="2d785-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="2d785-268">Numero di istanza di HANA.</span><span class="sxs-lookup"><span data-stu-id="2d785-268">HANA Instance number.</span></span> <span data-ttu-id="2d785-269">Usare 03 se è stato usato il modello di Azure o è stato seguito l'esempio precedente</span><span class="sxs-lookup"><span data-stu-id="2d785-269">Use 03 if you used the Azure Template or followed the example above</span></span>
    * <span data-ttu-id="2d785-270">Selezionare la modalità di database/immettere l'indice [1]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-271">Selezionare l'utilizzo del sistema/immettere l'indice [4]:</span><span class="sxs-lookup"><span data-stu-id="2d785-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="2d785-272">Selezionare l'utilizzo del sistema</span><span class="sxs-lookup"><span data-stu-id="2d785-272">Select the system Usage</span></span>
    * <span data-ttu-id="2d785-273">Immettere il percorso dei volumi di dati [/hana/data/HDB]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-274">Immettere il percorso dei volumi di log [/hana/log/HDB]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-275">Limitare l'allocazione massima della memoria?</span><span class="sxs-lookup"><span data-stu-id="2d785-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="2d785-276">[n]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-277">Immettere il nome host del certificato per l'host '...'</span><span class="sxs-lookup"><span data-stu-id="2d785-277">Enter Certificate Host Name For Host '...'</span></span> <span data-ttu-id="2d785-278">[...]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-278">[...]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-279">Immettere la password dell'utente agente host SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="2d785-279">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="2d785-280">Confermare la password dell'utente agente host SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="2d785-280">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="2d785-281">Immettere la password dell'amministratore di sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="2d785-281">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="2d785-282">Confermare la password dell'amministratore di sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="2d785-282">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="2d785-283">Immettere la home directory dell'amministratore di sistema [/usr/sap/HDB/home]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-283">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-284">Immettere la shell di accesso dell'amministratore di sistema [/bin/sh]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-284">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-285">Immettere l'ID utente dell'amministratore di sistema [1001]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-285">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-286">Immettere l'ID del gruppo di utenti (sapsys) [79]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-286">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-287">Immettere la password dell'utente del database (SYSTEM):</span><span class="sxs-lookup"><span data-stu-id="2d785-287">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="2d785-288">Confermare la password dell'utente del database (SYSTEM):</span><span class="sxs-lookup"><span data-stu-id="2d785-288">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="2d785-289">Riavviare il sistema dopo il riavvio della macchina?</span><span class="sxs-lookup"><span data-stu-id="2d785-289">Restart system after machine reboot?</span></span> <span data-ttu-id="2d785-290">[n]: -> INVIO</span><span class="sxs-lookup"><span data-stu-id="2d785-290">[n]: -> ENTER</span></span>
    * <span data-ttu-id="2d785-291">Continuare?</span><span class="sxs-lookup"><span data-stu-id="2d785-291">Do you want to continue?</span></span> <span data-ttu-id="2d785-292">(y/n):</span><span class="sxs-lookup"><span data-stu-id="2d785-292">(y/n):</span></span>  
  <span data-ttu-id="2d785-293">Convalidare il riepilogo e immettere y per continuare</span><span class="sxs-lookup"><span data-stu-id="2d785-293">Validate the summary and enter y to continue</span></span>
1. <span data-ttu-id="2d785-294">[A] Aggiornare l'agente host SAP</span><span class="sxs-lookup"><span data-stu-id="2d785-294">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="2d785-295">Scaricare l'archivio dell'agente host SAP più recente dal sito [SAP Softwarecenter] [sap-swcenter] ed eseguire il comando seguente per aggiornare l'agente.</span><span class="sxs-lookup"><span data-stu-id="2d785-295">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="2d785-296">Sostituire il percorso dell'archivio in modo da puntare al file scaricato.</span><span class="sxs-lookup"><span data-stu-id="2d785-296">Replace the path to the archive to point to the file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path to SAP Host Agent SAR>
    ```

1. <span data-ttu-id="2d785-297">[1] Creare la replica HANA (come radice)</span><span class="sxs-lookup"><span data-stu-id="2d785-297">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="2d785-298">Eseguire il comando indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2d785-298">Run the following command.</span></span> <span data-ttu-id="2d785-299">Assicurarsi di sostituire le stringhe in grassetto (ID di sistema HANA HDB e numero di istanza 03) con i valori dell'installazione di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="2d785-299">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="2d785-300">[A] Creare una voce di archivio chiavi (come radice)</span><span class="sxs-lookup"><span data-stu-id="2d785-300">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="2d785-301">[1] Eseguire il backup del database (come radice)</span><span class="sxs-lookup"><span data-stu-id="2d785-301">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="2d785-302">[1] Passare all'utente sapsid (ad esempio hdbadm) e creare il sito primario.</span><span class="sxs-lookup"><span data-stu-id="2d785-302">[1] Switch to the sapsid user (for example hdbadm) and create the primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="2d785-303">[2] Passare all'utente sapsid (ad esempio hdbadm) e creare il sito secondario.</span><span class="sxs-lookup"><span data-stu-id="2d785-303">[2] Switch to the sapsid user (for example hdbadm) and create the secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="2d785-304">Configurare il framework del cluster</span><span class="sxs-lookup"><span data-stu-id="2d785-304">Configure Cluster Framework</span></span>

<span data-ttu-id="2d785-305">Modificare le impostazioni predefinite</span><span class="sxs-lookup"><span data-stu-id="2d785-305">Change the default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter the following to crm-defaults.txt
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

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="2d785-306">Caricare ora il file nel cluster</span><span class="sxs-lookup"><span data-stu-id="2d785-306">now we load the file to the cluster</span></span>
<span data-ttu-id="2d785-307">sudo crm configure load update crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="2d785-307">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="2d785-308">Creare il dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="2d785-308">Create STONITH device</span></span>

<span data-ttu-id="2d785-309">Il dispositivo STONITH usa un'entità servizio per l'autorizzazione in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2d785-309">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="2d785-310">Per creare un'entità servizio, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="2d785-310">Please follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="2d785-311">Passare a <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="2d785-311">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="2d785-312">Aprire il pannello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d785-312">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="2d785-313">Passare a Proprietà e annotare l'ID directory.</span><span class="sxs-lookup"><span data-stu-id="2d785-313">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="2d785-314">Si tratta dell'**ID tenant**.</span><span class="sxs-lookup"><span data-stu-id="2d785-314">This is the **tenant id**.</span></span>
1. <span data-ttu-id="2d785-315">Fare clic su Registrazioni per l'app</span><span class="sxs-lookup"><span data-stu-id="2d785-315">Click App registrations</span></span>
1. <span data-ttu-id="2d785-316">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="2d785-316">Click Add</span></span>
1. <span data-ttu-id="2d785-317">Immettere un nome, selezionare il tipo di applicazione "App Web/API", immettere un URL di accesso (ad esempio http://localhost) e fare clic su Crea</span><span class="sxs-lookup"><span data-stu-id="2d785-317">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="2d785-318">L'URL di accesso non viene usato e può essere qualsiasi URL valido</span><span class="sxs-lookup"><span data-stu-id="2d785-318">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="2d785-319">Selezionare la nuova app e fare clic su Chiavi nella scheda Impostazioni</span><span class="sxs-lookup"><span data-stu-id="2d785-319">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="2d785-320">Immettere una descrizione per una nuova chiave, selezionare "Non scade mai" e fare clic su Salva</span><span class="sxs-lookup"><span data-stu-id="2d785-320">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="2d785-321">Annotare il valore.</span><span class="sxs-lookup"><span data-stu-id="2d785-321">Write down the Value.</span></span> <span data-ttu-id="2d785-322">Viene usato come **password** per l'entità servizio</span><span class="sxs-lookup"><span data-stu-id="2d785-322">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="2d785-323">Annotare l'ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d785-323">Write down the Application Id.</span></span> <span data-ttu-id="2d785-324">Viene usato come nome utente (**ID di accesso** nella procedura seguente) dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="2d785-324">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="2d785-325">L'entità servizio non ha le autorizzazioni per accedere alle risorse di Azure per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2d785-325">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="2d785-326">È necessario concedere all'entità servizio le autorizzazioni per avviare e arrestare (deallocare) tutte le macchine virtuali del cluster.</span><span class="sxs-lookup"><span data-stu-id="2d785-326">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="2d785-327">Passare a https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="2d785-327">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="2d785-328">Aprire il pannello Tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="2d785-328">Open the All resources blade</span></span>
1. <span data-ttu-id="2d785-329">Selezionare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2d785-329">Select the virtual machine</span></span>
1. <span data-ttu-id="2d785-330">Fare clic su Controllo di accesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="2d785-330">Click Access control (IAM)</span></span>
1. <span data-ttu-id="2d785-331">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="2d785-331">Click Add</span></span>
1. <span data-ttu-id="2d785-332">Selezionare il ruolo Proprietario</span><span class="sxs-lookup"><span data-stu-id="2d785-332">Select the role Owner</span></span>
1. <span data-ttu-id="2d785-333">Immettere il nome dell'applicazione creata in precedenza</span><span class="sxs-lookup"><span data-stu-id="2d785-333">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="2d785-334">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="2d785-334">Click OK</span></span>

<span data-ttu-id="2d785-335">Dopo aver modificato le autorizzazioni per le macchine virtuali, è possibile configurare i dispositivi STONITH nel cluster.</span><span class="sxs-lookup"><span data-stu-id="2d785-335">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter the following to crm-fencing.txt
# replace the bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="2d785-336">Caricare ora il file nel cluster</span><span class="sxs-lookup"><span data-stu-id="2d785-336">now we load the file to the cluster</span></span>
<span data-ttu-id="2d785-337">sudo crm configure load update crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="2d785-337">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="2d785-338">Creare risorse SAP HANA</span><span class="sxs-lookup"><span data-stu-id="2d785-338">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number and HANA system id
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

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="2d785-339">Caricare ora il file nel cluster</span><span class="sxs-lookup"><span data-stu-id="2d785-339">now we load the file to the cluster</span></span>
<span data-ttu-id="2d785-340">sudo crm configure load update crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="2d785-340">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
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

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="2d785-341">Caricare ora il file nel cluster</span><span class="sxs-lookup"><span data-stu-id="2d785-341">now we load the file to the cluster</span></span>
<span data-ttu-id="2d785-342">sudo crm configure load update crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="2d785-342">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="2d785-343">Testare la configurazione del cluster</span><span class="sxs-lookup"><span data-stu-id="2d785-343">Test cluster setup</span></span>
<span data-ttu-id="2d785-344">Il capitolo seguente descrive come testare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="2d785-344">The following chapter describe how you can test your setup.</span></span> <span data-ttu-id="2d785-345">Ogni test presuppone che ci si trovi nella radice e che il master SAP HANA sia in esecuzione nella macchina virtuale saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="2d785-345">Every test assumes that you are root and the SAP HANA master is running on the virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="2d785-346">Test di isolamento</span><span class="sxs-lookup"><span data-stu-id="2d785-346">Fencing Test</span></span>

<span data-ttu-id="2d785-347">È possibile testare la configurazione dell'agente di isolamento disabilitando l'interfaccia di rete nel nodo saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="2d785-347">You can test the setup of the fencing agent by disabling the network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="2d785-348">La macchina virtuale dovrebbe ora venire riavviata o arrestata, a seconda della configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="2d785-348">The virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="2d785-349">Se si imposta stonith-action su off, la macchina virtuale verrà arrestata e verrà eseguita la migrazione delle risorse alla macchina virtuale in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2d785-349">If you set the stonith-action to off, the virtual machine will be stopped and the resources are migrated to the running virtual machine.</span></span>

<span data-ttu-id="2d785-350">Una volta riavviata la macchina virtuale, la risorsa SAP HANA non verrà avviata come secondaria se si imposta AUTOMATED_REGISTER="false".</span><span class="sxs-lookup"><span data-stu-id="2d785-350">Once you start the virtual machine again, the SAP HANA resource will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="2d785-351">In questo caso, è necessario configurare l'istanza di HANA come secondaria eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2d785-351">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="2d785-352">Test di un failover manuale</span><span class="sxs-lookup"><span data-stu-id="2d785-352">Testing a manual failover</span></span>

<span data-ttu-id="2d785-353">È possibile testare un failover manuale arrestando il servizio pacemaker nel nodo saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="2d785-353">You can test a manual failover by stopping the pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="2d785-354">Dopo il failover, è possibile avviare nuovamente il servizio.</span><span class="sxs-lookup"><span data-stu-id="2d785-354">After the failover, you can start the service again.</span></span> <span data-ttu-id="2d785-355">La risorsa SAP HANA in saphanavm1 non verrà avviata come secondaria se si imposta AUTOMATED_REGISTER="false".</span><span class="sxs-lookup"><span data-stu-id="2d785-355">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="2d785-356">In questo caso, è necessario configurare l'istanza di HANA come secondaria eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2d785-356">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="2d785-357">Test di una migrazione</span><span class="sxs-lookup"><span data-stu-id="2d785-357">Testing a migration</span></span>

<span data-ttu-id="2d785-358">È possibile eseguire la migrazione del nodo master SAP HANA eseguendo il comando seguente</span><span class="sxs-lookup"><span data-stu-id="2d785-358">You can migrate the SAP HANA master node by executing the following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="2d785-359">In questo modo, dovrebbe venire eseguita la migrazione del nodo master SAP HANA e del gruppo che contiene l'indirizzo IP virtuale di saphanavm2.</span><span class="sxs-lookup"><span data-stu-id="2d785-359">This should migrate the SAP HANA master node and the group that contains the virtual IP address to saphanavm2.</span></span>
<span data-ttu-id="2d785-360">La risorsa SAP HANA in saphanavm1 non verrà avviata come secondaria se si imposta AUTOMATED_REGISTER="false".</span><span class="sxs-lookup"><span data-stu-id="2d785-360">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="2d785-361">In questo caso, è necessario configurare l'istanza di HANA come secondaria eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2d785-361">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="2d785-362">La migrazione crea vincoli di posizione che devono essere eliminati di nuovo.</span><span class="sxs-lookup"><span data-stu-id="2d785-362">The migration creates location contraints that need to be deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like the following contraint. You should have two contraints, one for the SAP HANA resource and one for the IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="2d785-363">È anche necessario eseguire la pulizia di stato della risorsa nodo secondario</span><span class="sxs-lookup"><span data-stu-id="2d785-363">You also need to cleanup the state of the secondary node resource</span></span>

<pre><code>
# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="2d785-364">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d785-364">Next steps</span></span>
* <span data-ttu-id="2d785-365">[Pianificazione e implementazione di Macchine virtuali di Azure per SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="2d785-365">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="2d785-366">[Distribuzione di Macchine virtuali di Azure per SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="2d785-366">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="2d785-367">[Distribuzione DBMS di Macchine virtuali di Azure per SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="2d785-367">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="2d785-368">Per informazioni su come stabilire la disponibilità elevata e pianificare il ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni), vedere [Disponibilità elevata e ripristino di emergenza di SAP HANA (istanze di grandi dimensioni) in Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="2d785-368">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
