---
title: "disponibilità elevata macchine virtuali per SAP NetWeaver in SUSE Linux Enterprise Server per le applicazioni SAP aaaAzure | Documenti Microsoft"
description: "Guida alla disponibilità elevata per SAP NetWeaver su SUSE Linux Enterprise Server per SAP applications"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="fbbfe-103">Disponibilità elevata per SAP NetWeaver su macchina virtuali di Azure in SUSE Linux Enterprise Server for SAP applications</span><span class="sxs-lookup"><span data-stu-id="fbbfe-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

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
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="fbbfe-113">In questo articolo viene descritto come macchine virtuali di toodeploy hello, configurare le macchine virtuali di hello, installare il framework di cluster hello e installare un sistema SAP NetWeaver 7,50 a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-113">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="fbbfe-114">Nelle configurazioni di esempio hello, i comandi di installazione e così via. vengono usati il numero di istanza ASCS 00, il numero di istanza ERS 02 e l'ID del sistema SAP NWS.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-114">In hello example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="fbbfe-115">Hello i nomi delle risorse di hello (ad esempio macchine virtuali, reti virtuali) nell'esempio hello si supponga di aver utilizzato hello [convergente modello] [ template-converged] con risorse di hello toocreate NWS ID sistema SAP.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-115">hello names of hello resources (for example virtual machines, virtual networks) in hello example assume that you have used hello [converged template][template-converged] with SAP system ID NWS toocreate hello resources.</span></span>

<span data-ttu-id="fbbfe-116">Leggere hello seguenti prima di note su SAP e documenti</span><span class="sxs-lookup"><span data-stu-id="fbbfe-116">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="fbbfe-117">Nota SAP [1928533], contenente:</span><span class="sxs-lookup"><span data-stu-id="fbbfe-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="fbbfe-118">Elenco di dimensioni di macchina virtuale di Azure sono supportati per la distribuzione del software SAP hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-118">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="fbbfe-119">Importanti informazioni sulla capacità per le dimensioni delle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="fbbfe-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="fbbfe-120">Software SAP e combinazioni di sistemi operativi e database supportati</span><span class="sxs-lookup"><span data-stu-id="fbbfe-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="fbbfe-121">Versione del kernel SAP richiesta per Windows e Linux in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fbbfe-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="fbbfe-122">La nota SAP [2015553] elenca i prerequisiti per le distribuzioni di software SAP supportate da SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="fbbfe-123">La nota SAP [2205917] contiene le impostazioni consigliate del sistema operativo per SUSE Linux Enterprise Server for SAP Applications</span><span class="sxs-lookup"><span data-stu-id="fbbfe-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="fbbfe-124">La nota SAP [1944799] contiene linee guida per SAP HANA per SUSE Linux Enterprise Server for SAP Applications</span><span class="sxs-lookup"><span data-stu-id="fbbfe-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="fbbfe-125">La nota SAP [2178632] contiene informazioni dettagliate su tutte le metriche di monitoraggio segnalate per SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="fbbfe-126">Nota SAP [2191498] hello necessario versione dell'agente Host SAP per Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-126">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="fbbfe-127">La nota SAP [2243692] contiene informazioni sulle licenze SAP in Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="fbbfe-128">La nota SAP [1984787] contiene informazioni generali su SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="fbbfe-129">Nota SAP [1999351] contiene altre informazioni sulla risoluzione dei problemi per hello Azure Enhanced Monitoring Extension per SAP.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-129">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="fbbfe-130">[Community WIKI SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene tutte le note su SAP necessarie per Linux.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="fbbfe-131">[Pianificazione e implementazione di Macchine virtuali di Azure per SAP in Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="fbbfe-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="fbbfe-132">[Distribuzione di Macchine virtuali di Azure per SAP in Linux (questo articolo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="fbbfe-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="fbbfe-133">[Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="fbbfe-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="fbbfe-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] (Scenario di ottimizzazione delle prestazioni di SAP HANA SR)</span><span class="sxs-lookup"><span data-stu-id="fbbfe-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="fbbfe-135">Guida di Hello contiene tutte le informazioni necessarie tooset di SAP HANA sistema replica locale.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-135">hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="fbbfe-136">Usare la guida per le indicazioni di base.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="fbbfe-137">[Elevata NFS spazio di archiviazione disponibile con DRBD e Pacemaker] [ suse-drbd-guide] Guida hello contiene tutte le informazioni necessarie tooset di un server NFS a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] hello guide contains all required information tooset up a highly available NFS server.</span></span> <span data-ttu-id="fbbfe-138">Usare la guida per le indicazioni di base.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="fbbfe-139">Panoramica</span><span class="sxs-lookup"><span data-stu-id="fbbfe-139">Overview</span></span>

<span data-ttu-id="fbbfe-140">disponibilità elevata di tooachieve, SAP NetWeaver richiede un server NFS.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-140">tooachieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="fbbfe-141">server NFS Hello è configurato in un cluster separato e può essere utilizzato da più sistemi SAP.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-141">hello NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![Panoramica della disponibilità elevata di SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="fbbfe-143">Hello del server NFS, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver Hiamanti e database SAP HANA hello utilizzare nome host virtuale e gli indirizzi IP virtuali.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-143">hello NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and hello SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="fbbfe-144">In Azure, un bilanciamento del carico è necessario toouse un indirizzo IP virtuale.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-144">On Azure, a load balancer is required toouse a virtual IP address.</span></span> <span data-ttu-id="fbbfe-145">Hello elenco riportato di seguito viene illustrata hello configurazione di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-145">hello following list shows hello configuration of hello load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="fbbfe-146">Server NFS</span><span class="sxs-lookup"><span data-stu-id="fbbfe-146">NFS Server</span></span>
* <span data-ttu-id="fbbfe-147">Configurazione front-end</span><span class="sxs-lookup"><span data-stu-id="fbbfe-147">Frontend configuration</span></span>
  * <span data-ttu-id="fbbfe-148">Indirizzo IP 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="fbbfe-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="fbbfe-149">Configurazione back-end</span><span class="sxs-lookup"><span data-stu-id="fbbfe-149">Backend configuration</span></span>
  * <span data-ttu-id="fbbfe-150">Interfacce di rete tooprimary di tutte le macchine virtuali che devono far parte del cluster NFS hello connesso</span><span class="sxs-lookup"><span data-stu-id="fbbfe-150">Connected tooprimary network interfaces of all virtual machines that should be part of hello NFS cluster</span></span>
* <span data-ttu-id="fbbfe-151">Porta probe</span><span class="sxs-lookup"><span data-stu-id="fbbfe-151">Probe Port</span></span>
  * <span data-ttu-id="fbbfe-152">Porta 61000</span><span class="sxs-lookup"><span data-stu-id="fbbfe-152">Port 61000</span></span>
* <span data-ttu-id="fbbfe-153">Regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fbbfe-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="fbbfe-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-154">2049 TCP</span></span> 
  * <span data-ttu-id="fbbfe-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="fbbfe-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="fbbfe-156">(A)SCS</span></span>
* <span data-ttu-id="fbbfe-157">Configurazione front-end</span><span class="sxs-lookup"><span data-stu-id="fbbfe-157">Frontend configuration</span></span>
  * <span data-ttu-id="fbbfe-158">Indirizzo IP 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="fbbfe-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="fbbfe-159">Configurazione back-end</span><span class="sxs-lookup"><span data-stu-id="fbbfe-159">Backend configuration</span></span>
  * <span data-ttu-id="fbbfe-160">Interfacce di rete connessa tooprimary di tutte le macchine virtuali che devono far parte del cluster di hello (A) SCS/Hiamanti</span><span class="sxs-lookup"><span data-stu-id="fbbfe-160">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="fbbfe-161">Porta probe</span><span class="sxs-lookup"><span data-stu-id="fbbfe-161">Probe Port</span></span>
  * <span data-ttu-id="fbbfe-162">Porta 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="fbbfe-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="fbbfe-163">Regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fbbfe-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="fbbfe-164">32**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="fbbfe-165">36**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="fbbfe-166">39**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="fbbfe-167">81**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="fbbfe-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="fbbfe-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="fbbfe-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="fbbfe-171">ERS</span><span class="sxs-lookup"><span data-stu-id="fbbfe-171">ERS</span></span>
* <span data-ttu-id="fbbfe-172">Configurazione front-end</span><span class="sxs-lookup"><span data-stu-id="fbbfe-172">Frontend configuration</span></span>
  * <span data-ttu-id="fbbfe-173">Indirizzo IP 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="fbbfe-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="fbbfe-174">Configurazione back-end</span><span class="sxs-lookup"><span data-stu-id="fbbfe-174">Backend configuration</span></span>
  * <span data-ttu-id="fbbfe-175">Interfacce di rete connessa tooprimary di tutte le macchine virtuali che devono far parte del cluster di hello (A) SCS/Hiamanti</span><span class="sxs-lookup"><span data-stu-id="fbbfe-175">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="fbbfe-176">Porta probe</span><span class="sxs-lookup"><span data-stu-id="fbbfe-176">Probe Port</span></span>
  * <span data-ttu-id="fbbfe-177">Porta 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="fbbfe-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="fbbfe-178">Regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fbbfe-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="fbbfe-179">33**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="fbbfe-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="fbbfe-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="fbbfe-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="fbbfe-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="fbbfe-183">SAP HANA</span></span>
* <span data-ttu-id="fbbfe-184">Configurazione front-end</span><span class="sxs-lookup"><span data-stu-id="fbbfe-184">Frontend configuration</span></span>
  * <span data-ttu-id="fbbfe-185">Indirizzo IP 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="fbbfe-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="fbbfe-186">Configurazione back-end</span><span class="sxs-lookup"><span data-stu-id="fbbfe-186">Backend configuration</span></span>
  * <span data-ttu-id="fbbfe-187">Interfacce di rete tooprimary di tutte le macchine virtuali che devono far parte del cluster HANA hello connesso</span><span class="sxs-lookup"><span data-stu-id="fbbfe-187">Connected tooprimary network interfaces of all virtual machines that should be part of hello HANA cluster</span></span>
* <span data-ttu-id="fbbfe-188">Porta probe</span><span class="sxs-lookup"><span data-stu-id="fbbfe-188">Probe Port</span></span>
  * <span data-ttu-id="fbbfe-189">Porta 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="fbbfe-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="fbbfe-190">Regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fbbfe-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="fbbfe-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="fbbfe-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="fbbfe-193">Configurazione di un server NFS a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="fbbfe-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="fbbfe-194">Distribuzione di Linux</span><span class="sxs-lookup"><span data-stu-id="fbbfe-194">Deploying Linux</span></span>

<span data-ttu-id="fbbfe-195">Hello Azure Marketplace contiene un'immagine per SUSE Linux Enterprise Server per SAP 12 di applicazioni che è possibile utilizzare toodeploy nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-195">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span>
<span data-ttu-id="fbbfe-196">È possibile utilizzare uno dei modelli di avvio rapido hello in github toodeploy tutte le risorse necessarie.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-196">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="fbbfe-197">Consente di distribuire il modello di Hello hello le macchine virtuali, bilanciamento del carico hello, disponibilità, set e così via. Seguire questi modelli di hello toodeploy passaggi:</span><span class="sxs-lookup"><span data-stu-id="fbbfe-197">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="fbbfe-198">Aprire hello [modello di file server di SAP] [ template-file-server] in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fbbfe-198">Open hello [SAP file server template][template-file-server] in hello Azure portal</span></span>   
1. <span data-ttu-id="fbbfe-199">Immettere i seguenti parametri hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-199">Enter hello following parameters</span></span>
   1. <span data-ttu-id="fbbfe-200">Prefisso della risorsa</span><span class="sxs-lookup"><span data-stu-id="fbbfe-200">Resource Prefix</span></span>  
      <span data-ttu-id="fbbfe-201">Immettere il prefisso di hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-201">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="fbbfe-202">il valore di Hello viene utilizzato come prefisso per le risorse di hello che vengono distribuite.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-202">hello value is used as a prefix for hello resources that are deployed.</span></span>
   2. <span data-ttu-id="fbbfe-203">Tipo di sistema operativo</span><span class="sxs-lookup"><span data-stu-id="fbbfe-203">Os Type</span></span>  
      <span data-ttu-id="fbbfe-204">Selezionare una delle distribuzioni di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-204">Select one of hello Linux distributions.</span></span> <span data-ttu-id="fbbfe-205">Per questo esempio, selezionare SLES 12</span><span class="sxs-lookup"><span data-stu-id="fbbfe-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="fbbfe-206">Nome utente e password amministratore</span><span class="sxs-lookup"><span data-stu-id="fbbfe-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="fbbfe-207">Viene creato un nuovo utente che può essere utilizzato toolog toohello computer.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-207">A new user is created that can be used toolog on toohello machine.</span></span>
   4. <span data-ttu-id="fbbfe-208">ID subnet</span><span class="sxs-lookup"><span data-stu-id="fbbfe-208">Subnet Id</span></span>  
      <span data-ttu-id="fbbfe-209">ID Hello delle macchine virtuali di hello subnet toowhich hello deve essere connessa a.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-209">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="fbbfe-210">Lasciare vuoto se si desidera toocreate una nuova rete virtuale o selezionare hello subnet della rete VPN o Express Route rete virtuale tooconnect hello macchina virtuale tooyour locale rete.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-210">Leave empty if you want toocreate a new virtual network or select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="fbbfe-211">ID Hello in genere è simile /Subscriptions/<ID**&lt;id sottoscrizione&gt;**/ResourceGroups /**&lt;nome gruppo di risorse&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nome di rete virtuale&gt;**/subnets/**&lt;nome subnet&gt;**</span><span class="sxs-lookup"><span data-stu-id="fbbfe-211">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="fbbfe-212">Installazione</span><span class="sxs-lookup"><span data-stu-id="fbbfe-212">Installation</span></span>

<span data-ttu-id="fbbfe-213">Hello seguenti elementi sono preceduti da una **[A]** -nodi tooall applicabile, **[1]** -solo applicabile toonode 1 o **[2]** -solo applicabile toonode 2.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-213">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="fbbfe-214">**[A]** Aggiornare SLES</span><span class="sxs-lookup"><span data-stu-id="fbbfe-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="fbbfe-215">**[1]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="fbbfe-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="fbbfe-216">**[2]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="fbbfe-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="fbbfe-217">**[1]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="fbbfe-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="fbbfe-218">**[A]** Installare l'estensione per la disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="fbbfe-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="fbbfe-219">**[A]** Configurare la risoluzione dei nomi host</span><span class="sxs-lookup"><span data-stu-id="fbbfe-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="fbbfe-220">È possibile usare un server DNS o modificare /etc/hosts hello in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-220">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="fbbfe-221">Questo esempio mostra come toouse hello file /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-221">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="fbbfe-222">Sostituire l'indirizzo IP hello e nome host hello in hello seguenti comandi</span><span class="sxs-lookup"><span data-stu-id="fbbfe-222">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="fbbfe-223">Inserire hello seguenti righe troppo/ecc/host.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-223">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="fbbfe-224">Modificare l'ambiente di hello IP indirizzo e nome host toomatch</span><span class="sxs-lookup"><span data-stu-id="fbbfe-224">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="fbbfe-225">**[1]** Installare il cluster</span><span class="sxs-lookup"><span data-stu-id="fbbfe-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="fbbfe-226">**[2]**  Aggiungi nodo toocluster</span><span class="sxs-lookup"><span data-stu-id="fbbfe-226">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="fbbfe-227">**[A]**  Modifica hacluster password toohello stessa password</span><span class="sxs-lookup"><span data-stu-id="fbbfe-227">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="fbbfe-228">**[A]**  Configurare corosync toouse altro trasporto e aggiungere nodelist.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-228">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="fbbfe-229">In caso contrario, il cluster non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="fbbfe-230">Aggiungere i seguenti file grassetto toohello contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-230">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="fbbfe-231">Riavviare il servizio di corosync hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-231">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="fbbfe-232">**[A]** Installare i componenti drbd</span><span class="sxs-lookup"><span data-stu-id="fbbfe-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="fbbfe-233">**[A]**  Creare una partizione per il dispositivo drbd hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-233">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="fbbfe-234">**[A]** Creare le configurazioni LVM</span><span class="sxs-lookup"><span data-stu-id="fbbfe-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="fbbfe-235">**[A]**  Dispositivo drbd di crea hello NFS</span><span class="sxs-lookup"><span data-stu-id="fbbfe-235">**[A]** Create hello NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="fbbfe-236">Inserisci configurazione hello per il nuovo dispositivo di drbd hello e uscita</span><span class="sxs-lookup"><span data-stu-id="fbbfe-236">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="fbbfe-237">Creare un dispositivo drbd hello e avviarla</span><span class="sxs-lookup"><span data-stu-id="fbbfe-237">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="fbbfe-238">**[1]** Saltare la sincronizzazione iniziale</span><span class="sxs-lookup"><span data-stu-id="fbbfe-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="fbbfe-239">**[1]**  Nodo primario del set hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-239">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="fbbfe-240">**[1]**  Attendere finché non vengono sincronizzati i nuovi dispositivi drbd hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-240">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="fbbfe-241">**[1]**  Creare sistemi di file in hello drbd dispositivi</span><span class="sxs-lookup"><span data-stu-id="fbbfe-241">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="fbbfe-242">Configurare il framework del cluster</span><span class="sxs-lookup"><span data-stu-id="fbbfe-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="fbbfe-243">**[1]**  Modificare le impostazioni predefinite di hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-243">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="fbbfe-244">**[1]**  Configurazione cluster Aggiungi hello NFS drbd dispositivo toohello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-244">**[1]** Add hello NFS drbd device toohello cluster configuration</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="fbbfe-245">**[1]**  Del server NFS hello crea</span><span class="sxs-lookup"><span data-stu-id="fbbfe-245">**[1]** Create hello NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="fbbfe-246">**[1]**  Creare risorse di File System NFS hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-246">**[1]** Create hello NFS File System resources</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="fbbfe-247">**[1]**  Creare esportazioni NFS hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-247">**[1]** Create hello NFS exports</span></span>

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="fbbfe-248">**[1]**  Creare un probe di integrità servizio di bilanciamento del carico interno hello e una risorsa IP virtuale</span><span class="sxs-lookup"><span data-stu-id="fbbfe-248">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="fbbfe-249">Creare il dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="fbbfe-249">Create STONITH device</span></span>

<span data-ttu-id="fbbfe-250">dispositivo STONITH Hello utilizza un tooauthorize dell'entità servizio in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-250">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="fbbfe-251">Seguire questi toocreate passaggi un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-251">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="fbbfe-252">Andare troppo<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="fbbfe-252">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="fbbfe-253">Pannello di Azure Active Directory aprire hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-253">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="fbbfe-254">Passare tooProperties e annotare hello ID di Directory. Si tratta di hello **id tenant**.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-254">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="fbbfe-255">Fare clic su Registrazioni per l'app</span><span class="sxs-lookup"><span data-stu-id="fbbfe-255">Click App registrations</span></span>
1. <span data-ttu-id="fbbfe-256">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-256">Click Add</span></span>
1. <span data-ttu-id="fbbfe-257">Immettere un nome, selezionare il tipo di applicazione "App Web/API", immettere un URL di accesso (ad esempio http://localhost) e fare clic su Crea</span><span class="sxs-lookup"><span data-stu-id="fbbfe-257">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="fbbfe-258">URL Hello-sign-on non viene utilizzato e può essere un URL valido</span><span class="sxs-lookup"><span data-stu-id="fbbfe-258">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="fbbfe-259">Selezionare hello nuova App e fare clic su chiavi nella scheda Impostazioni hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-259">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="fbbfe-260">Immettere una descrizione per una nuova chiave, selezionare "Non scade mai" e fare clic su Salva</span><span class="sxs-lookup"><span data-stu-id="fbbfe-260">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="fbbfe-261">Annotare hello valore.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-261">Write down hello Value.</span></span> <span data-ttu-id="fbbfe-262">Viene utilizzato come hello **password** per hello dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="fbbfe-262">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="fbbfe-263">Annotare hello ID dell'applicazione. Viene utilizzato come nome utente di hello (**id di accesso** in seguito hello) di hello dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="fbbfe-263">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="fbbfe-264">Hello dell'entità servizio non dispone delle autorizzazioni tooaccess le risorse di Azure per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-264">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="fbbfe-265">È necessario toogive hello dell'entità servizio autorizzazioni toostart e l'arresto (deallocazione) tutte le macchine virtuali del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-265">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="fbbfe-266">Passare toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="fbbfe-266">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="fbbfe-267">Apri hello tutti pannello risorse</span><span class="sxs-lookup"><span data-stu-id="fbbfe-267">Open hello All resources blade</span></span>
1. <span data-ttu-id="fbbfe-268">Selezionare la macchina virtuale di hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-268">Select hello virtual machine</span></span>
1. <span data-ttu-id="fbbfe-269">Fare clic su Controllo di accesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="fbbfe-269">Click Access control (IAM)</span></span>
1. <span data-ttu-id="fbbfe-270">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-270">Click Add</span></span>
1. <span data-ttu-id="fbbfe-271">Selezionare il ruolo di hello proprietario</span><span class="sxs-lookup"><span data-stu-id="fbbfe-271">Select hello role Owner</span></span>
1. <span data-ttu-id="fbbfe-272">Immettere il nome di hello dell'applicazione hello creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="fbbfe-272">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="fbbfe-273">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-273">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="fbbfe-274">**[1]**  Creare hello STONITH dispositivi</span><span class="sxs-lookup"><span data-stu-id="fbbfe-274">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="fbbfe-275">Dopo le autorizzazioni di hello per le macchine virtuali hello modificato, è possibile configurare i dispositivi STONITH hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-275">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="fbbfe-276">**[1]**  Abilitare hello utilizzo di un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="fbbfe-276">**[1]** Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="fbbfe-277">Configurazione di (A)SCS</span><span class="sxs-lookup"><span data-stu-id="fbbfe-277">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="fbbfe-278">Distribuzione di Linux</span><span class="sxs-lookup"><span data-stu-id="fbbfe-278">Deploying Linux</span></span>

<span data-ttu-id="fbbfe-279">Hello Azure Marketplace contiene un'immagine per SUSE Linux Enterprise Server per SAP 12 di applicazioni che è possibile utilizzare toodeploy nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-279">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span> <span data-ttu-id="fbbfe-280">immagine del marketplace Hello contiene l'agente di risorsa hello per SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-280">hello marketplace image contains hello resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="fbbfe-281">È possibile utilizzare uno dei modelli di avvio rapido hello in github toodeploy tutte le risorse necessarie.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-281">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="fbbfe-282">Consente di distribuire il modello di Hello hello le macchine virtuali, bilanciamento del carico hello, disponibilità, set e così via. Seguire questi modelli di hello toodeploy passaggi:</span><span class="sxs-lookup"><span data-stu-id="fbbfe-282">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="fbbfe-283">Aprire hello [modello ASCS/SCS più SID] [ template-multisid-xscs] o hello [convergente modello] [ template-converged] sul modello solo di hello hello portale Azure ASCS/SCS Crea regole di bilanciamento del carico di hello per le istanze di Hiamanti (solo Linux) e SAP NetWeaver ASCS/SCS hello mentre hello convergente modello crea anche le regole di bilanciamento del carico di hello per un database (ad esempio Microsoft SQL Server o SAP HANA).</span><span class="sxs-lookup"><span data-stu-id="fbbfe-283">Open hello [ASCS/SCS Multi SID template][template-multisid-xscs] or hello [converged template][template-converged] on hello Azure portal hello ASCS/SCS template only creates hello load-balancing rules for hello SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas hello converged template also creates hello load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="fbbfe-284">Se si prevede di tooinstall un sistema basate su SAP NetWeaver e si desidera anche database hello tooinstall in hello stesse macchine, utilizzare hello [convergente modello][template-converged].</span><span class="sxs-lookup"><span data-stu-id="fbbfe-284">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello database on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="fbbfe-285">Immettere i seguenti parametri hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-285">Enter hello following parameters</span></span>
   1. <span data-ttu-id="fbbfe-286">Prefisso di risorsa (solo modello ASCS/SCS a più SID)</span><span class="sxs-lookup"><span data-stu-id="fbbfe-286">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="fbbfe-287">Immettere il prefisso di hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-287">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="fbbfe-288">il valore di Hello viene utilizzato come prefisso per le risorse di hello che vengono distribuite.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-288">hello value is used as a prefix for hello resources that are deployed.</span></span>
   3. <span data-ttu-id="fbbfe-289">ID del sistema SAP (solo modello convergente)</span><span class="sxs-lookup"><span data-stu-id="fbbfe-289">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="fbbfe-290">Immettere il sistema SAP hello Id di sistema SAP si desidera tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-290">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="fbbfe-291">Hello Id viene utilizzato come prefisso per le risorse di hello che vengono distribuite.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-291">hello Id is used as a prefix for hello resources that are deployed.</span></span>
   4. <span data-ttu-id="fbbfe-292">Tipo di stack</span><span class="sxs-lookup"><span data-stu-id="fbbfe-292">Stack Type</span></span>  
      <span data-ttu-id="fbbfe-293">Selezionare tipo di stack hello SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="fbbfe-293">Select hello SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="fbbfe-294">Tipo di sistema operativo</span><span class="sxs-lookup"><span data-stu-id="fbbfe-294">Os Type</span></span>  
      <span data-ttu-id="fbbfe-295">Selezionare una delle distribuzioni di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-295">Select one of hello Linux distributions.</span></span> <span data-ttu-id="fbbfe-296">Per questo esempio, selezionare SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="fbbfe-296">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="fbbfe-297">Tipo di database</span><span class="sxs-lookup"><span data-stu-id="fbbfe-297">Db Type</span></span>  
      <span data-ttu-id="fbbfe-298">Selezionare HANA</span><span class="sxs-lookup"><span data-stu-id="fbbfe-298">Select HANA</span></span>
   7. <span data-ttu-id="fbbfe-299">Dimensioni del sistema SAP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-299">Sap System Size</span></span>  
      <span data-ttu-id="fbbfe-300">quantità di Hello del nuovo sistema SAP hello fornisce.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-300">hello amount of SAPS hello new system provides.</span></span> <span data-ttu-id="fbbfe-301">Se non si conoscono quanti valori SAPS hello sistema richiede, chiedere il Partner di tecnologia di SAP o l'integratore</span><span class="sxs-lookup"><span data-stu-id="fbbfe-301">If you are not sure how many SAPS hello system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="fbbfe-302">Disponibilità del sistema</span><span class="sxs-lookup"><span data-stu-id="fbbfe-302">System Availability</span></span>  
      <span data-ttu-id="fbbfe-303">Selezionare la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-303">Select HA</span></span>
   9. <span data-ttu-id="fbbfe-304">Nome utente e password amministratore</span><span class="sxs-lookup"><span data-stu-id="fbbfe-304">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="fbbfe-305">Viene creato un nuovo utente che può essere utilizzato toolog toohello computer.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-305">A new user is created that can be used toolog on toohello machine.</span></span>
   10. <span data-ttu-id="fbbfe-306">ID subnet</span><span class="sxs-lookup"><span data-stu-id="fbbfe-306">Subnet Id</span></span>  
   <span data-ttu-id="fbbfe-307">ID Hello delle macchine virtuali di hello subnet toowhich hello deve essere connessa a.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-307">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span>  <span data-ttu-id="fbbfe-308">Lasciare vuoto se si desidera toocreate una nuova rete virtuale o selezionare hello stessa subnet utilizzata o creato come parte della distribuzione del server NFS hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-308">Leave empty if you want toocreate a new virtual network or select hello same subnet that you used or created as part of hello NFS server deployment.</span></span> <span data-ttu-id="fbbfe-309">ID Hello in genere è simile /Subscriptions/<ID**&lt;id sottoscrizione&gt;**/ResourceGroups /**&lt;nome gruppo di risorse&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nome di rete virtuale&gt;**/subnets/**&lt;nome subnet&gt;**</span><span class="sxs-lookup"><span data-stu-id="fbbfe-309">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="fbbfe-310">Installazione</span><span class="sxs-lookup"><span data-stu-id="fbbfe-310">Installation</span></span>

<span data-ttu-id="fbbfe-311">Hello seguenti elementi sono preceduti da una **[A]** -nodi tooall applicabile, **[1]** -solo applicabile toonode 1 o **[2]** -solo applicabile toonode 2.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-311">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="fbbfe-312">**[A]** Aggiornare SLES</span><span class="sxs-lookup"><span data-stu-id="fbbfe-312">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="fbbfe-313">**[1]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="fbbfe-313">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="fbbfe-314">**[2]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="fbbfe-314">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="fbbfe-315">**[1]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="fbbfe-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="fbbfe-316">**[A]** Installare l'estensione per la disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="fbbfe-316">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="fbbfe-317">**[A]**  Aggiornare gli agenti delle risorse SAP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-317">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="fbbfe-318">Una patch per il pacchetto di risorse agenti hello è obbligatorio toouse hello nuova configurazione descritta in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-318">A patch for hello resource-agents package is required toouse hello new configuration, that is described in this article.</span></span> <span data-ttu-id="fbbfe-319">È possibile controllare se patch hello è già installato con hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="fbbfe-319">You can check, if hello patch is already installed with hello following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="fbbfe-320">output di Hello dovrebbe essere simile a</span><span class="sxs-lookup"><span data-stu-id="fbbfe-320">hello output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="fbbfe-321">Se il comando grep hello non viene trovato il parametro IS_ERS hello, è necessario patch hello tooinstall elencato in [hello SUSE pagina di download](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="fbbfe-321">If hello grep command does not find hello IS_ERS parameter, you need tooinstall hello patch listed on [hello SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="fbbfe-322">**[A]** Configurare la risoluzione dei nomi host</span><span class="sxs-lookup"><span data-stu-id="fbbfe-322">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="fbbfe-323">È possibile usare un server DNS o modificare /etc/hosts hello in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-323">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="fbbfe-324">Questo esempio mostra come toouse hello file /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-324">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="fbbfe-325">Sostituire l'indirizzo IP hello e nome host hello in hello seguenti comandi</span><span class="sxs-lookup"><span data-stu-id="fbbfe-325">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="fbbfe-326">Inserire hello seguenti righe troppo/ecc/host.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-326">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="fbbfe-327">Modificare l'ambiente di hello IP indirizzo e nome host toomatch</span><span class="sxs-lookup"><span data-stu-id="fbbfe-327">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="fbbfe-328">**[1]** Installare il cluster</span><span class="sxs-lookup"><span data-stu-id="fbbfe-328">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="fbbfe-329">**[2]**  Aggiungi nodo toocluster</span><span class="sxs-lookup"><span data-stu-id="fbbfe-329">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="fbbfe-330">**[A]**  Modifica hacluster password toohello stessa password</span><span class="sxs-lookup"><span data-stu-id="fbbfe-330">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="fbbfe-331">**[A]**  Configurare corosync toouse altro trasporto e aggiungere nodelist.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-331">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="fbbfe-332">In caso contrario, il cluster non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-332">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="fbbfe-333">Aggiungere i seguenti file grassetto toohello contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-333">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="fbbfe-334">Riavviare il servizio di corosync hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-334">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="fbbfe-335">**[A]** Installare i componenti drbd</span><span class="sxs-lookup"><span data-stu-id="fbbfe-335">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="fbbfe-336">**[A]**  Creare una partizione per il dispositivo drbd hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-336">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="fbbfe-337">**[A]** Creare le configurazioni LVM</span><span class="sxs-lookup"><span data-stu-id="fbbfe-337">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="fbbfe-338">**[A]**  Dispositivo drbd SCS hello di creazione</span><span class="sxs-lookup"><span data-stu-id="fbbfe-338">**[A]** Create hello SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="fbbfe-339">Inserisci configurazione hello per il nuovo dispositivo di drbd hello e uscita</span><span class="sxs-lookup"><span data-stu-id="fbbfe-339">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="fbbfe-340">Creare un dispositivo drbd hello e avviarla</span><span class="sxs-lookup"><span data-stu-id="fbbfe-340">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="fbbfe-341">**[A]**  Dispositivo drbd Hiamanti hello di creazione</span><span class="sxs-lookup"><span data-stu-id="fbbfe-341">**[A]** Create hello ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="fbbfe-342">Inserisci configurazione hello per il nuovo dispositivo di drbd hello e uscita</span><span class="sxs-lookup"><span data-stu-id="fbbfe-342">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="fbbfe-343">Creare un dispositivo drbd hello e avviarla</span><span class="sxs-lookup"><span data-stu-id="fbbfe-343">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="fbbfe-344">**[1]** Saltare la sincronizzazione iniziale</span><span class="sxs-lookup"><span data-stu-id="fbbfe-344">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="fbbfe-345">**[1]**  Nodo primario del set hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-345">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="fbbfe-346">**[1]**  Attendere finché non vengono sincronizzati i nuovi dispositivi drbd hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-346">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="fbbfe-347">**[1]**  Creare sistemi di file in hello drbd dispositivi</span><span class="sxs-lookup"><span data-stu-id="fbbfe-347">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="fbbfe-348">Configurare il framework del cluster</span><span class="sxs-lookup"><span data-stu-id="fbbfe-348">Configure Cluster Framework</span></span>

<span data-ttu-id="fbbfe-349">**[1]**  Modificare le impostazioni predefinite di hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-349">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="fbbfe-350">Prepararsi per l'installazione di SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="fbbfe-350">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="fbbfe-351">**[A]**  Hello Crea directory condivise</span><span class="sxs-lookup"><span data-stu-id="fbbfe-351">**[A]** Create hello shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="fbbfe-352">**[A]** Configurare autofs</span><span class="sxs-lookup"><span data-stu-id="fbbfe-352">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="fbbfe-353">Creare un file con</span><span class="sxs-lookup"><span data-stu-id="fbbfe-353">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="fbbfe-354">Riavviare autofs toomount hello nuovi volumi o condivisioni</span><span class="sxs-lookup"><span data-stu-id="fbbfe-354">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="fbbfe-355">**[A]**  Configurare il file SWAP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-355">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="fbbfe-356">La modifica di hello hello agente tooactivate</span><span class="sxs-lookup"><span data-stu-id="fbbfe-356">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="fbbfe-357">Installazione di SAP NetWeaver ASCS/ERS</span><span class="sxs-lookup"><span data-stu-id="fbbfe-357">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="fbbfe-358">**[1]**  Creare un probe di integrità servizio di bilanciamento del carico interno hello e una risorsa IP virtuale</span><span class="sxs-lookup"><span data-stu-id="fbbfe-358">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="fbbfe-359">Assicurarsi che lo stato del cluster hello è accettabile e che tutte le risorse siano avviate.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-359">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="fbbfe-360">Non è importante in quali risorse hello nodo sono in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-360">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. <span data-ttu-id="fbbfe-361">**[1]** Installare SAP NetWeaver ASCS</span><span class="sxs-lookup"><span data-stu-id="fbbfe-361">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="fbbfe-362">Installazione di SAP NetWeaver ASCS come radice nel primo nodo hello utilizzando un nome host virtuale che esegue il mapping, ad esempio l'indirizzo IP toohello del configurazione front-end di bilanciamento del carico hello per hello ASCS <b>nws ascs</b>, <b>10.0.0.10</b>e numero di istanza hello utilizzato per il probe hello di bilanciamento del carico hello, ad esempio <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-362">Install SAP NetWeaver ASCS as root on hello first node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and hello instance number that you used for hello probe of hello load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="fbbfe-363">È possibile utilizzare hello sapinst parametro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst di tooconnect un utente non root.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-363">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="fbbfe-364">**[1]**  Creare un probe di integrità servizio di bilanciamento del carico interno hello e una risorsa IP virtuale</span><span class="sxs-lookup"><span data-stu-id="fbbfe-364">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="fbbfe-365">Assicurarsi che lo stato del cluster hello è accettabile e che tutte le risorse siano avviate.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-365">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="fbbfe-366">Non è importante in quali risorse hello nodo sono in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-366">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="fbbfe-367">**[2]** Installare SAP NetWeaver ERS</span><span class="sxs-lookup"><span data-stu-id="fbbfe-367">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="fbbfe-368">Installazione di SAP NetWeaver Hiamanti come radice nel secondo nodo hello utilizzando un nome host virtuale che esegue il mapping, ad esempio l'indirizzo IP toohello del configurazione front-end di bilanciamento del carico hello per hello Hiamanti <b>nws hiamanti</b>, <b>10.0.0.11</b> numero di istanza hello utilizzato per il probe hello di bilanciamento del carico hello, ad esempio e <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-368">Install SAP NetWeaver ERS as root on hello second node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and hello instance number that you used for hello probe of hello load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="fbbfe-369">È possibile utilizzare hello sapinst parametro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst di tooconnect un utente non root.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-369">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="fbbfe-370">Usare SWPM SP 20 PL 05 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-370">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="fbbfe-371">Le versioni precedenti non è impostato correttamente le autorizzazioni di hello e hello installazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-371">Lower versions do not set hello permissions correctly and hello installation will fail.</span></span>
   > 

1. <span data-ttu-id="fbbfe-372">**[1]**  Adattare i profili di istanza ASCS/SCS e Hiamanti hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-372">**[1]** Adapt hello ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="fbbfe-373">Profilo ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="fbbfe-373">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="fbbfe-374">Profilo ERS</span><span class="sxs-lookup"><span data-stu-id="fbbfe-374">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="fbbfe-375">**[A]**  Configurare keep-alive</span><span class="sxs-lookup"><span data-stu-id="fbbfe-375">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="fbbfe-376">la comunicazione tra il server applicazioni SAP NetWeaver hello e hello ASCS/SCS Hello viene instradata tramite un bilanciamento del carico software.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-376">hello communication between hello SAP NetWeaver application server and hello ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="fbbfe-377">servizio di bilanciamento del carico Hello disconnette le connessioni inattive dopo un timeout configurabile.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-377">hello load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="fbbfe-378">tooprevent questo è necessario un parametro nel profilo di SAP NetWeaver ASCS/SCS hello tooset e modificare le impostazioni di sistema di hello Linux.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-378">tooprevent this you need tooset a parameter in hello SAP NetWeaver ASCS/SCS profile and change hello Linux system settings.</span></span> <span data-ttu-id="fbbfe-379">Per altre informazioni, leggere la [nota SAP 1410736][1410736].</span><span class="sxs-lookup"><span data-stu-id="fbbfe-379">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="fbbfe-380">Hello ASCS/SCS profilo accodare parametro/encni/set_so_keepalive è stato già aggiunto nell'ultimo passaggio hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-380">hello ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in hello last step.</span></span>

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="fbbfe-381">**[A]**  Configurare utenti SAP hello dopo l'installazione di hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-381">**[A]** Configure hello SAP users after hello installation</span></span>
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="fbbfe-382">**[1]**  Aggiungi hello ASCS e SAP Hiamanti toohello sapservice file services</span><span class="sxs-lookup"><span data-stu-id="fbbfe-382">**[1]** Add hello ASCS and ERS SAP services toohello sapservice file</span></span>

   <span data-ttu-id="fbbfe-383">Aggiungere hello ASCS servizio voce toohello secondo nodo e copia hello Hiamanti voce toohello primo nodo del servizio.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-383">Add hello ASCS service entry toohello second node and copy hello ERS service entry toohello first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="fbbfe-384">**[1]**  Creare risorse del cluster di hello SAP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-384">**[1]** Create hello SAP cluster resources</span></span>

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   <span data-ttu-id="fbbfe-385">Assicurarsi che lo stato del cluster hello è accettabile e che tutte le risorse siano avviate.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-385">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="fbbfe-386">Non è importante in quali risorse hello nodo sono in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-386">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="fbbfe-387">Creare il dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="fbbfe-387">Create STONITH device</span></span>

<span data-ttu-id="fbbfe-388">dispositivo STONITH Hello utilizza un tooauthorize dell'entità servizio in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-388">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="fbbfe-389">Seguire questi toocreate passaggi un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-389">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="fbbfe-390">Andare troppo<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="fbbfe-390">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="fbbfe-391">Pannello di Azure Active Directory aprire hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-391">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="fbbfe-392">Passare tooProperties e annotare hello ID di Directory. Si tratta di hello **id tenant**.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-392">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="fbbfe-393">Fare clic su Registrazioni per l'app</span><span class="sxs-lookup"><span data-stu-id="fbbfe-393">Click App registrations</span></span>
1. <span data-ttu-id="fbbfe-394">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-394">Click Add</span></span>
1. <span data-ttu-id="fbbfe-395">Immettere un nome, selezionare il tipo di applicazione "App Web/API", immettere un URL di accesso (ad esempio http://localhost) e fare clic su Crea</span><span class="sxs-lookup"><span data-stu-id="fbbfe-395">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="fbbfe-396">URL Hello-sign-on non viene utilizzato e può essere un URL valido</span><span class="sxs-lookup"><span data-stu-id="fbbfe-396">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="fbbfe-397">Selezionare hello nuova App e fare clic su chiavi nella scheda Impostazioni hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-397">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="fbbfe-398">Immettere una descrizione per una nuova chiave, selezionare "Non scade mai" e fare clic su Salva</span><span class="sxs-lookup"><span data-stu-id="fbbfe-398">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="fbbfe-399">Annotare hello valore.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-399">Write down hello Value.</span></span> <span data-ttu-id="fbbfe-400">Viene utilizzato come hello **password** per hello dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="fbbfe-400">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="fbbfe-401">Annotare hello ID dell'applicazione. Viene utilizzato come nome utente di hello (**id di accesso** in seguito hello) di hello dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="fbbfe-401">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="fbbfe-402">Hello dell'entità servizio non dispone delle autorizzazioni tooaccess le risorse di Azure per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-402">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="fbbfe-403">È necessario toogive hello dell'entità servizio autorizzazioni toostart e l'arresto (deallocazione) tutte le macchine virtuali del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-403">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="fbbfe-404">Passare toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="fbbfe-404">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="fbbfe-405">Apri hello tutti pannello risorse</span><span class="sxs-lookup"><span data-stu-id="fbbfe-405">Open hello All resources blade</span></span>
1. <span data-ttu-id="fbbfe-406">Selezionare la macchina virtuale di hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-406">Select hello virtual machine</span></span>
1. <span data-ttu-id="fbbfe-407">Fare clic su Controllo di accesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="fbbfe-407">Click Access control (IAM)</span></span>
1. <span data-ttu-id="fbbfe-408">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-408">Click Add</span></span>
1. <span data-ttu-id="fbbfe-409">Selezionare il ruolo di hello proprietario</span><span class="sxs-lookup"><span data-stu-id="fbbfe-409">Select hello role Owner</span></span>
1. <span data-ttu-id="fbbfe-410">Immettere il nome di hello dell'applicazione hello creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="fbbfe-410">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="fbbfe-411">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-411">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="fbbfe-412">**[1]**  Creare hello STONITH dispositivi</span><span class="sxs-lookup"><span data-stu-id="fbbfe-412">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="fbbfe-413">Dopo le autorizzazioni di hello per le macchine virtuali hello modificato, è possibile configurare i dispositivi STONITH hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-413">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="fbbfe-414">**[1]**  Abilitare hello utilizzo di un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="fbbfe-414">**[1]** Enable hello use of a STONITH device</span></span>

<span data-ttu-id="fbbfe-415">Abilitare l'utilizzo di hello di un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="fbbfe-415">Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="fbbfe-416">Installare il database</span><span class="sxs-lookup"><span data-stu-id="fbbfe-416">Install database</span></span>

<span data-ttu-id="fbbfe-417">In questo esempio viene installata e configurata una replica di sistema di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-417">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="fbbfe-418">SAP HANA verrà eseguito in hello stesso cluster come hello ASCS/SCS di SAP NetWeaver e Hiamanti.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-418">SAP HANA will run in hello same cluster as hello SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="fbbfe-419">È anche possibile installare SAP HANA in un cluster dedicato.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-419">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="fbbfe-420">Per altre informazioni, vedere [Disponibilità elevata di SAP HANA in macchine virtuali di Azure (VM)][sap-hana-ha].</span><span class="sxs-lookup"><span data-stu-id="fbbfe-420">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="fbbfe-421">Prepararsi per l'installazione di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="fbbfe-421">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="fbbfe-422">È in genere consigliabile usare LVM per i volumi che archiviano i dati e file di log.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-422">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="fbbfe-423">A scopo di test, è anche possibile scegliere toostore hello dati e log file direttamente su un disco normale.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-423">For testing purposes, you can also choose toostore hello data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="fbbfe-424">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="fbbfe-424">**[A]** LVM</span></span>  
   <span data-ttu-id="fbbfe-425">esempio Hello riportato di seguito presuppone che le macchine virtuali hello disponga di quattro dischi dati collegati che devono essere utilizzati toocreate due volumi.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-425">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
   
   <span data-ttu-id="fbbfe-426">Creare volumi fisici per tutti i dischi che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-426">Create physical volumes for all disks that you want toouse.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="fbbfe-427">Creare un gruppo di volumi per il file di dati di hello, un gruppo di volumi per il file di log hello e una directory condivisa hello SAP HANA</span><span class="sxs-lookup"><span data-stu-id="fbbfe-427">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="fbbfe-428">Creare hello volumi logici</span><span class="sxs-lookup"><span data-stu-id="fbbfe-428">Create hello logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="fbbfe-429">Creare le directory di montaggio hello e copiare hello UUID di tutti i volumi logici</span><span class="sxs-lookup"><span data-stu-id="fbbfe-429">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="fbbfe-430">Creare le voci di autofs per hello tre volumi logici</span><span class="sxs-lookup"><span data-stu-id="fbbfe-430">Create autofs entries for hello three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="fbbfe-431">Inserire la riga toosudo vi /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="fbbfe-431">Insert this line toosudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="fbbfe-432">Montare i volumi di nuovo hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-432">Mount hello new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="fbbfe-433">**[A]** Dischi normali</span><span class="sxs-lookup"><span data-stu-id="fbbfe-433">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="fbbfe-434">Per sistemi demo o di piccole dimensioni, è possibile inserire i dati e i file di log HANA su un disco.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-434">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="fbbfe-435">Hello seguenti comandi creare una partizione su /dev/sdc e formattarla con xfs.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-435">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="fbbfe-436">Inserire questo too/etc/auto.direct riga</span><span class="sxs-lookup"><span data-stu-id="fbbfe-436">Insert this line too/etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="fbbfe-437">Creare la directory di destinazione hello e montare il disco di hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-437">Create hello target directory and mount hello disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="fbbfe-438">Installazione di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="fbbfe-438">Installing SAP HANA</span></span>

<span data-ttu-id="fbbfe-439">Hello passaggi seguenti si basano capitolo 4 di hello [SAP HANA SR prestazioni ottimizzate Scenario guide] [ suse-hana-ha-guide] tooinstall SAP HANA sistema di replica.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-439">hello following steps are based on chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span> <span data-ttu-id="fbbfe-440">Leggerlo prima di continuare l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-440">Please read it before you continue hello installation.</span></span>

1. <span data-ttu-id="fbbfe-441">**[A]**  Eseguire hdblcm da hello HANA DVD</span><span class="sxs-lookup"><span data-stu-id="fbbfe-441">**[A]** Run hdblcm from hello HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="fbbfe-442">**[A]** Aggiornare l'agente host SAP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-442">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="fbbfe-443">Scaricare l'archivio agente Host SAP più recente hello da hello [SAP Softwarecenter] [ sap-swcenter] ed eseguiti hello seguenti comando tooupgrade hello agente.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-443">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="fbbfe-444">Sostituire hello percorso toohello archivio toopoint toohello file scaricato.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-444">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="fbbfe-445">**[1]** Creare la replica HANA (come root)</span><span class="sxs-lookup"><span data-stu-id="fbbfe-445">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="fbbfe-446">Eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-446">Run hello following command.</span></span> <span data-ttu-id="fbbfe-447">Verificare che tooreplace grassetto stringhe (HANA sistema ID HDB e numero di istanza 03) con valori di hello dell'installazione di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-447">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="fbbfe-448">**[A]** Creare una voce di archivio chiavi (come root)</span><span class="sxs-lookup"><span data-stu-id="fbbfe-448">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="fbbfe-449">**[1]** Eseguire il backup del database (come root)</span><span class="sxs-lookup"><span data-stu-id="fbbfe-449">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="fbbfe-450">**[1]**  Cambiare toohello HANA sapsid utente e creare il sito primario di hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-450">**[1]** Switch toohello HANA sapsid user and create hello primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="fbbfe-451">**[2]**  Cambiare toohello HANA sapsid utente e creare il sito secondario di hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-451">**[2]** Switch toohello HANA sapsid user and create hello secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="fbbfe-452">**[1]** Creare le risorse del cluster SAP HANA</span><span class="sxs-lookup"><span data-stu-id="fbbfe-452">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="fbbfe-453">Innanzitutto, creare una topologia di hello.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-453">First, create hello topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   <span data-ttu-id="fbbfe-454">Successivamente, creare risorse HANA hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-454">Next, create hello HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="fbbfe-455">Assicurarsi che lo stato del cluster hello è accettabile e che tutte le risorse siano avviate.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-455">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="fbbfe-456">Non è importante in quali risorse hello nodo sono in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-456">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="fbbfe-457">**[1]**  Istanza del database SAP NetWeaver hello installazione</span><span class="sxs-lookup"><span data-stu-id="fbbfe-457">**[1]** Install hello SAP NetWeaver database instance</span></span>

   <span data-ttu-id="fbbfe-458">Istanza del database SAP NetWeaver hello installa come radice utilizzando un nome host virtuale che esegue il mapping, ad esempio l'indirizzo IP toohello del configurazione front-end di bilanciamento del carico hello per database hello <b>nws db</b> e <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-458">Install hello SAP NetWeaver database instance as root using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="fbbfe-459">È possibile utilizzare hello sapinst parametro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst di tooconnect un utente non root.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-459">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="fbbfe-460">Installazione del server applicazioni di SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="fbbfe-460">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="fbbfe-461">Seguire questi tooinstall passaggi un server applicazioni SAP.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-461">Follow these steps tooinstall an SAP application server.</span></span> <span data-ttu-id="fbbfe-462">Hello i passaggi seguenti presuppongono che si installa il server applicazioni di hello in un server diverso da hello ASCS/SCS e i server HANA.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-462">hello steps bellow assume that you install hello application server on a server different from hello ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="fbbfe-463">In caso contrario alcuni dei passaggi di hello sotto (ad esempio la configurazione di risoluzione del nome host) non sono necessarie.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-463">Otherwise some of hello steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="fbbfe-464">Configurare la risoluzione dei nomi host</span><span class="sxs-lookup"><span data-stu-id="fbbfe-464">Setup host name resolution</span></span>    
   <span data-ttu-id="fbbfe-465">È possibile usare un server DNS o modificare /etc/hosts hello in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-465">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="fbbfe-466">Questo esempio mostra come toouse hello file /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-466">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="fbbfe-467">Sostituire l'indirizzo IP hello e nome host hello in hello seguenti comandi</span><span class="sxs-lookup"><span data-stu-id="fbbfe-467">Replace hello IP address and hello hostname in hello following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="fbbfe-468">Inserire hello seguenti righe troppo/ecc/host.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-468">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="fbbfe-469">Modificare l'ambiente di hello IP indirizzo e nome host toomatch</span><span class="sxs-lookup"><span data-stu-id="fbbfe-469">Change hello IP address and hostname toomatch your environment</span></span>    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="fbbfe-470">Creare la directory sapmnt hello</span><span class="sxs-lookup"><span data-stu-id="fbbfe-470">Create hello sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="fbbfe-471">Configurare autofs</span><span class="sxs-lookup"><span data-stu-id="fbbfe-471">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="fbbfe-472">Creare un nuovo file con</span><span class="sxs-lookup"><span data-stu-id="fbbfe-472">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="fbbfe-473">Riavviare autofs toomount hello nuovi volumi o condivisioni</span><span class="sxs-lookup"><span data-stu-id="fbbfe-473">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="fbbfe-474">Configurare il file SWAP</span><span class="sxs-lookup"><span data-stu-id="fbbfe-474">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="fbbfe-475">La modifica di hello hello agente tooactivate</span><span class="sxs-lookup"><span data-stu-id="fbbfe-475">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="fbbfe-476">Installare il server applicazioni di SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="fbbfe-476">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="fbbfe-477">Installare un server applicazioni di SAP NetWeaver primario o aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-477">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="fbbfe-478">È possibile utilizzare hello sapinst parametro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst di tooconnect un utente non root.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-478">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="fbbfe-479">Aggiornare l'archivio sicuro di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="fbbfe-479">Update SAP HANA secure store</span></span>

   <span data-ttu-id="fbbfe-480">Nome virtuale di toohello toopoint del programma di installazione di SAP HANA sistema replica hello dell'archivio hello aggiornamento SAP HANA sicura.</span><span class="sxs-lookup"><span data-stu-id="fbbfe-480">Update hello SAP HANA secure store toopoint toohello virtual name of hello SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="fbbfe-481">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fbbfe-481">Next steps</span></span>
* <span data-ttu-id="fbbfe-482">[Pianificazione e implementazione di Macchine virtuali di Azure per SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="fbbfe-482">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="fbbfe-483">[Distribuzione di Macchine virtuali di Azure per SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="fbbfe-483">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="fbbfe-484">[Distribuzione DBMS di Macchine virtuali di Azure per SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="fbbfe-484">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="fbbfe-485">toolearn tooestablish la disponibilità elevata e piano di ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni), vedere [SAP HANA (istanze di grandi dimensioni) ad alto disponibilità e ripristino di emergenza in Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="fbbfe-485">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="fbbfe-486">toolearn tooestablish la disponibilità elevata e piano di ripristino di emergenza di SAP HANA in macchine virtuali di Azure, vedere [disponibilità elevata di SAP HANA in macchine virtuali di Azure (VM)][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="fbbfe-486">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>
