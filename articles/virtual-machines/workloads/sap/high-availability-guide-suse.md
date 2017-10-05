---
title: "Disponibilità elevata in macchine virtuali di Azure per SAP NetWeaver su SUSE Linux Enterprise Server for SAP applications | Microsoft Docs"
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
ms.openlocfilehash: 16e09797926f29bc18cb05671c986c74f9c2d4f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="94a58-103">Disponibilità elevata per SAP NetWeaver su macchina virtuali di Azure in SUSE Linux Enterprise Server for SAP applications</span><span class="sxs-lookup"><span data-stu-id="94a58-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="94a58-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="94a58-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="94a58-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="94a58-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="94a58-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="94a58-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="94a58-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="94a58-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="94a58-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="94a58-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="94a58-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="94a58-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="94a58-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="94a58-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="94a58-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="94a58-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="94a58-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="94a58-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="94a58-113">Questo articolo descrive come distribuire le macchine virtuali, configurare le macchine virtuali, installare il framework del cluster e installare un sistema SAP NetWeaver 7.50 a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="94a58-113">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="94a58-114">Nelle configurazioni di esempio, nei comandi di installazione e così via vengono usati il numero di istanza ASCS 00, il numero di istanza ERS 02 e l'ID del sistema SAP NWS.</span><span class="sxs-lookup"><span data-stu-id="94a58-114">In the example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="94a58-115">I nomi delle risorse (ad esempio macchine virtuali e reti virtuali) nell'esempio presuppongono che sia stato usato il [modello convergente][template-converged] con l'ID del sistema SAP NWS per creare le risorse.</span><span class="sxs-lookup"><span data-stu-id="94a58-115">The names of the resources (for example virtual machines, virtual networks) in the example assume that you have used the [converged template][template-converged] with SAP system ID NWS to create the resources.</span></span>

<span data-ttu-id="94a58-116">Leggere prima di tutto le note e i documenti seguenti relativi a SAP</span><span class="sxs-lookup"><span data-stu-id="94a58-116">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="94a58-117">Nota SAP [1928533], contenente:</span><span class="sxs-lookup"><span data-stu-id="94a58-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="94a58-118">Elenco delle dimensioni delle VM di Azure supportate per la distribuzione di software SAP</span><span class="sxs-lookup"><span data-stu-id="94a58-118">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="94a58-119">Importanti informazioni sulla capacità per le dimensioni delle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="94a58-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="94a58-120">Software SAP e combinazioni di sistemi operativi e database supportati</span><span class="sxs-lookup"><span data-stu-id="94a58-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="94a58-121">Versione del kernel SAP richiesta per Windows e Linux in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="94a58-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="94a58-122">La nota SAP [2015553] elenca i prerequisiti per le distribuzioni di software SAP supportate da SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="94a58-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="94a58-123">La nota SAP [2205917] contiene le impostazioni consigliate del sistema operativo per SUSE Linux Enterprise Server for SAP Applications</span><span class="sxs-lookup"><span data-stu-id="94a58-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="94a58-124">La nota SAP [1944799] contiene linee guida per SAP HANA per SUSE Linux Enterprise Server for SAP Applications</span><span class="sxs-lookup"><span data-stu-id="94a58-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="94a58-125">La nota SAP [2178632] contiene informazioni dettagliate su tutte le metriche di monitoraggio segnalate per SAP in Azure.</span><span class="sxs-lookup"><span data-stu-id="94a58-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="94a58-126">La nota SAP [2191498] contiene la versione dell'agente host SAP per Linux necessaria in Azure.</span><span class="sxs-lookup"><span data-stu-id="94a58-126">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="94a58-127">La nota SAP [2243692] contiene informazioni sulle licenze SAP in Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="94a58-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="94a58-128">La nota SAP [1984787] contiene informazioni generali su SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="94a58-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="94a58-129">La nota SAP [1999351] contiene informazioni aggiuntive sulla risoluzione dei problemi per l'estensione di monitoraggio avanzato di Azure per SAP.</span><span class="sxs-lookup"><span data-stu-id="94a58-129">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="94a58-130">[Community WIKI SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene tutte le note su SAP necessarie per Linux.</span><span class="sxs-lookup"><span data-stu-id="94a58-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="94a58-131">[Pianificazione e implementazione di Macchine virtuali di Azure per SAP in Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="94a58-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="94a58-132">[Distribuzione di Macchine virtuali di Azure per SAP in Linux (questo articolo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="94a58-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="94a58-133">[Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="94a58-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="94a58-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] (Scenario di ottimizzazione delle prestazioni di SAP HANA SR)</span><span class="sxs-lookup"><span data-stu-id="94a58-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="94a58-135">La guida contiene tutte le informazioni necessarie per configurare la replica di sistema SAP HANA in locale.</span><span class="sxs-lookup"><span data-stu-id="94a58-135">The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="94a58-136">Usare la guida per le indicazioni di base.</span><span class="sxs-lookup"><span data-stu-id="94a58-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="94a58-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] (Archiviazione NFS a disponibilità elevata con DRBD e Pacemaker) La guida contiene tutte le informazioni necessarie per configurare un server NFS a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="94a58-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] The guide contains all required information to set up a highly available NFS server.</span></span> <span data-ttu-id="94a58-138">Usare la guida per le indicazioni di base.</span><span class="sxs-lookup"><span data-stu-id="94a58-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="94a58-139">Panoramica</span><span class="sxs-lookup"><span data-stu-id="94a58-139">Overview</span></span>

<span data-ttu-id="94a58-140">Per ottenere la disponibilità elevata, SAP NetWeaver richiede un server NFS.</span><span class="sxs-lookup"><span data-stu-id="94a58-140">To achieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="94a58-141">Il server NFS viene configurato in un cluster separato e può essere usato da più sistemi SAP.</span><span class="sxs-lookup"><span data-stu-id="94a58-141">The NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![Panoramica della disponibilità elevata di SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="94a58-143">Il server NFS, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS e il database SAP HANA usano un nome host virtuale e indirizzi IP virtuali.</span><span class="sxs-lookup"><span data-stu-id="94a58-143">The NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and the SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="94a58-144">Per usare un indirizzo IP virtuale in Azure, occorre il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="94a58-144">On Azure, a load balancer is required to use a virtual IP address.</span></span> <span data-ttu-id="94a58-145">L'elenco seguente mostra la configurazione del bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="94a58-145">The following list shows the configuration of the load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="94a58-146">Server NFS</span><span class="sxs-lookup"><span data-stu-id="94a58-146">NFS Server</span></span>
* <span data-ttu-id="94a58-147">Configurazione front-end</span><span class="sxs-lookup"><span data-stu-id="94a58-147">Frontend configuration</span></span>
  * <span data-ttu-id="94a58-148">Indirizzo IP 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="94a58-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="94a58-149">Configurazione back-end</span><span class="sxs-lookup"><span data-stu-id="94a58-149">Backend configuration</span></span>
  * <span data-ttu-id="94a58-150">Connessione alle interfacce di rete primarie di tutte le macchine virtuali che devono far parte del cluster NFS</span><span class="sxs-lookup"><span data-stu-id="94a58-150">Connected to primary network interfaces of all virtual machines that should be part of the NFS cluster</span></span>
* <span data-ttu-id="94a58-151">Porta probe</span><span class="sxs-lookup"><span data-stu-id="94a58-151">Probe Port</span></span>
  * <span data-ttu-id="94a58-152">Porta 61000</span><span class="sxs-lookup"><span data-stu-id="94a58-152">Port 61000</span></span>
* <span data-ttu-id="94a58-153">Regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="94a58-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="94a58-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-154">2049 TCP</span></span> 
  * <span data-ttu-id="94a58-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="94a58-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="94a58-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="94a58-156">(A)SCS</span></span>
* <span data-ttu-id="94a58-157">Configurazione front-end</span><span class="sxs-lookup"><span data-stu-id="94a58-157">Frontend configuration</span></span>
  * <span data-ttu-id="94a58-158">Indirizzo IP 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="94a58-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="94a58-159">Configurazione back-end</span><span class="sxs-lookup"><span data-stu-id="94a58-159">Backend configuration</span></span>
  * <span data-ttu-id="94a58-160">Connessione alle interfacce di rete primarie di tutte le macchine virtuali che devono far parte del cluster (A)SCS/ERS</span><span class="sxs-lookup"><span data-stu-id="94a58-160">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="94a58-161">Porta probe</span><span class="sxs-lookup"><span data-stu-id="94a58-161">Probe Port</span></span>
  * <span data-ttu-id="94a58-162">Porta 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="94a58-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="94a58-163">Regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="94a58-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="94a58-164">32**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="94a58-165">36**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="94a58-166">39**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="94a58-167">81**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="94a58-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="94a58-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="94a58-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="94a58-171">ERS</span><span class="sxs-lookup"><span data-stu-id="94a58-171">ERS</span></span>
* <span data-ttu-id="94a58-172">Configurazione front-end</span><span class="sxs-lookup"><span data-stu-id="94a58-172">Frontend configuration</span></span>
  * <span data-ttu-id="94a58-173">Indirizzo IP 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="94a58-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="94a58-174">Configurazione back-end</span><span class="sxs-lookup"><span data-stu-id="94a58-174">Backend configuration</span></span>
  * <span data-ttu-id="94a58-175">Connessione alle interfacce di rete primarie di tutte le macchine virtuali che devono far parte del cluster (A)SCS/ERS</span><span class="sxs-lookup"><span data-stu-id="94a58-175">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="94a58-176">Porta probe</span><span class="sxs-lookup"><span data-stu-id="94a58-176">Probe Port</span></span>
  * <span data-ttu-id="94a58-177">Porta 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="94a58-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="94a58-178">Regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="94a58-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="94a58-179">33**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="94a58-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="94a58-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="94a58-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="94a58-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="94a58-183">SAP HANA</span></span>
* <span data-ttu-id="94a58-184">Configurazione front-end</span><span class="sxs-lookup"><span data-stu-id="94a58-184">Frontend configuration</span></span>
  * <span data-ttu-id="94a58-185">Indirizzo IP 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="94a58-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="94a58-186">Configurazione back-end</span><span class="sxs-lookup"><span data-stu-id="94a58-186">Backend configuration</span></span>
  * <span data-ttu-id="94a58-187">Connessione alle interfacce di rete primarie di tutte le macchine virtuali che devono far parte del cluster HANA</span><span class="sxs-lookup"><span data-stu-id="94a58-187">Connected to primary network interfaces of all virtual machines that should be part of the HANA cluster</span></span>
* <span data-ttu-id="94a58-188">Porta probe</span><span class="sxs-lookup"><span data-stu-id="94a58-188">Probe Port</span></span>
  * <span data-ttu-id="94a58-189">Porta 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="94a58-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="94a58-190">Regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="94a58-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="94a58-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="94a58-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="94a58-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="94a58-193">Configurazione di un server NFS a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="94a58-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="94a58-194">Distribuzione di Linux</span><span class="sxs-lookup"><span data-stu-id="94a58-194">Deploying Linux</span></span>

<span data-ttu-id="94a58-195">Azure Marketplace contiene un'immagine per SUSE Linux Enterprise Server for SAP Applications 12 che è possibile usare per distribuire nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="94a58-195">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span>
<span data-ttu-id="94a58-196">È possibile usare uno dei modelli di avvio rapido di GitHub per distribuire tutte le risorse necessarie.</span><span class="sxs-lookup"><span data-stu-id="94a58-196">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="94a58-197">Il modello consente di distribuire le macchine virtuali, il servizio di bilanciamento del carico, il set di disponibilità e così via. Per distribuire il modello, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="94a58-197">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="94a58-198">Aprire il [modello di file server di SAP][template-file-server] nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="94a58-198">Open the [SAP file server template][template-file-server] in the Azure portal</span></span>   
1. <span data-ttu-id="94a58-199">Immettere i parametri seguenti</span><span class="sxs-lookup"><span data-stu-id="94a58-199">Enter the following parameters</span></span>
   1. <span data-ttu-id="94a58-200">Prefisso della risorsa</span><span class="sxs-lookup"><span data-stu-id="94a58-200">Resource Prefix</span></span>  
      <span data-ttu-id="94a58-201">Immettere il prefisso che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="94a58-201">Enter the prefix you want to use.</span></span> <span data-ttu-id="94a58-202">Il valore viene usato come prefisso per le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="94a58-202">The value is used as a prefix for the resources that are deployed.</span></span>
   2. <span data-ttu-id="94a58-203">Tipo di sistema operativo</span><span class="sxs-lookup"><span data-stu-id="94a58-203">Os Type</span></span>  
      <span data-ttu-id="94a58-204">Selezionare una delle distribuzioni Linux.</span><span class="sxs-lookup"><span data-stu-id="94a58-204">Select one of the Linux distributions.</span></span> <span data-ttu-id="94a58-205">Per questo esempio, selezionare SLES 12</span><span class="sxs-lookup"><span data-stu-id="94a58-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="94a58-206">Nome utente e password amministratore</span><span class="sxs-lookup"><span data-stu-id="94a58-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="94a58-207">Verrà creato un nuovo utente con cui è possibile accedere alla macchina</span><span class="sxs-lookup"><span data-stu-id="94a58-207">A new user is created that can be used to log on to the machine.</span></span>
   4. <span data-ttu-id="94a58-208">ID subnet</span><span class="sxs-lookup"><span data-stu-id="94a58-208">Subnet Id</span></span>  
      <span data-ttu-id="94a58-209">ID della subnet a cui devono essere connesse le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="94a58-209">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="94a58-210">Lasciare vuoto se si vuole creare una nuova rete virtuale o selezionare la subnet della rete virtuale Express Route o VPN per connettere la macchina virtuale alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="94a58-210">Leave empty if you want to create a new virtual network or select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="94a58-211">L'ID in genere è simile al seguente: /subscriptions/**&lt;ID sottoscrizione&gt;**/resourceGroups/**&lt;nome gruppo risorse&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;nome rete virtuale&gt;**/subnets/**&lt;nome subnet&gt;**</span><span class="sxs-lookup"><span data-stu-id="94a58-211">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="94a58-212">Installazione</span><span class="sxs-lookup"><span data-stu-id="94a58-212">Installation</span></span>

<span data-ttu-id="94a58-213">Gli elementi seguenti sono preceduti dall'indicazione **[A]** - applicabile a tutti i nodi, **[1]** - applicabile solo al nodo 1 o **[2]** - applicabile solo al nodo 2.</span><span class="sxs-lookup"><span data-stu-id="94a58-213">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="94a58-214">**[A]** Aggiornare SLES</span><span class="sxs-lookup"><span data-stu-id="94a58-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="94a58-215">**[1]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="94a58-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="94a58-216">**[2]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="94a58-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="94a58-217">**[1]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="94a58-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="94a58-218">**[A]** Installare l'estensione per la disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="94a58-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="94a58-219">**[A]** Configurare la risoluzione dei nomi host</span><span class="sxs-lookup"><span data-stu-id="94a58-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="94a58-220">È possibile usare un server DNS o modificare /etc/hosts in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="94a58-220">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="94a58-221">Questo esempio mostra come usare il file /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="94a58-221">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="94a58-222">Sostituire l'indirizzo IP e il nome host nei comandi seguenti</span><span class="sxs-lookup"><span data-stu-id="94a58-222">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="94a58-223">Inserire le righe seguenti in /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="94a58-223">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="94a58-224">Modificare l'indirizzo IP e il nome host in base all'ambiente</span><span class="sxs-lookup"><span data-stu-id="94a58-224">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="94a58-225">**[1]** Installare il cluster</span><span class="sxs-lookup"><span data-stu-id="94a58-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="94a58-226">**[2]** Aggiungere un nodo al cluster</span><span class="sxs-lookup"><span data-stu-id="94a58-226">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="94a58-227">**[A]** Modificare la password hacluster in modo da usare la stessa password</span><span class="sxs-lookup"><span data-stu-id="94a58-227">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="94a58-228">**[A]** Configurare corosync per usare un altro trasporto e aggiungere nodelist</span><span class="sxs-lookup"><span data-stu-id="94a58-228">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="94a58-229">In caso contrario, il cluster non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="94a58-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="94a58-230">Aggiungere il seguente contenuto in grassetto nel file.</span><span class="sxs-lookup"><span data-stu-id="94a58-230">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="94a58-231">Riavviare quindi il servizio corosync</span><span class="sxs-lookup"><span data-stu-id="94a58-231">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="94a58-232">**[A]** Installare i componenti drbd</span><span class="sxs-lookup"><span data-stu-id="94a58-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="94a58-233">**[A]** Creare una partizione per il dispositivo drbd</span><span class="sxs-lookup"><span data-stu-id="94a58-233">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="94a58-234">**[A]** Creare le configurazioni LVM</span><span class="sxs-lookup"><span data-stu-id="94a58-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="94a58-235">**[A]** Creare il dispositivo drbd NFS</span><span class="sxs-lookup"><span data-stu-id="94a58-235">**[A]** Create the NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="94a58-236">Inserire la configurazione per il nuovo dispositivo drbd e uscire</span><span class="sxs-lookup"><span data-stu-id="94a58-236">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="94a58-237">Creare il dispositivo drbd e avviarlo</span><span class="sxs-lookup"><span data-stu-id="94a58-237">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="94a58-238">**[1]** Saltare la sincronizzazione iniziale</span><span class="sxs-lookup"><span data-stu-id="94a58-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="94a58-239">**[1]** Impostare il nodo primario</span><span class="sxs-lookup"><span data-stu-id="94a58-239">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="94a58-240">**[1]**  Attendere il completamento della sincronizzazione dei nuovi dispositivi drbd</span><span class="sxs-lookup"><span data-stu-id="94a58-240">**[1]** Wait until the new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="94a58-241">**[1]**  Creare i file system nei dispositivi drbd</span><span class="sxs-lookup"><span data-stu-id="94a58-241">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="94a58-242">Configurare il framework del cluster</span><span class="sxs-lookup"><span data-stu-id="94a58-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="94a58-243">**[1]** Modificare le impostazioni predefinite</span><span class="sxs-lookup"><span data-stu-id="94a58-243">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="94a58-244">**[1]**  Aggiungere il dispositivo drbd NFS alla configurazione del cluster</span><span class="sxs-lookup"><span data-stu-id="94a58-244">**[1]** Add the NFS drbd device to the cluster configuration</span></span>

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

1. <span data-ttu-id="94a58-245">**[1]** Creare il server NFS</span><span class="sxs-lookup"><span data-stu-id="94a58-245">**[1]** Create the NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="94a58-246">**[1]**  Creare le risorse del file system NFS</span><span class="sxs-lookup"><span data-stu-id="94a58-246">**[1]** Create the NFS File System resources</span></span>

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

1. <span data-ttu-id="94a58-247">**[1]** Creare le esportazioni NFS</span><span class="sxs-lookup"><span data-stu-id="94a58-247">**[1]** Create the NFS exports</span></span>

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

1. <span data-ttu-id="94a58-248">**[1]**  Creare una risorsa IP virtuale e un probe di integrità per il bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="94a58-248">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="94a58-249">Creare il dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="94a58-249">Create STONITH device</span></span>

<span data-ttu-id="94a58-250">Il dispositivo STONITH usa un'entità servizio per l'autorizzazione in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="94a58-250">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="94a58-251">Per creare un'entità servizio, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="94a58-251">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="94a58-252">Passare a <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="94a58-252">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="94a58-253">Aprire il pannello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94a58-253">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="94a58-254">Passare a Proprietà e annotare l'ID directory.</span><span class="sxs-lookup"><span data-stu-id="94a58-254">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="94a58-255">Si tratta dell'**ID tenant**.</span><span class="sxs-lookup"><span data-stu-id="94a58-255">This is the **tenant id**.</span></span>
1. <span data-ttu-id="94a58-256">Fare clic su Registrazioni per l'app</span><span class="sxs-lookup"><span data-stu-id="94a58-256">Click App registrations</span></span>
1. <span data-ttu-id="94a58-257">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="94a58-257">Click Add</span></span>
1. <span data-ttu-id="94a58-258">Immettere un nome, selezionare il tipo di applicazione "App Web/API", immettere un URL di accesso (ad esempio http://localhost) e fare clic su Crea</span><span class="sxs-lookup"><span data-stu-id="94a58-258">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="94a58-259">L'URL di accesso non viene usato e può essere qualsiasi URL valido</span><span class="sxs-lookup"><span data-stu-id="94a58-259">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="94a58-260">Selezionare la nuova app e fare clic su Chiavi nella scheda Impostazioni</span><span class="sxs-lookup"><span data-stu-id="94a58-260">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="94a58-261">Immettere una descrizione per una nuova chiave, selezionare "Non scade mai" e fare clic su Salva</span><span class="sxs-lookup"><span data-stu-id="94a58-261">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="94a58-262">Annotare il valore.</span><span class="sxs-lookup"><span data-stu-id="94a58-262">Write down the Value.</span></span> <span data-ttu-id="94a58-263">Viene usato come **password** per l'entità servizio</span><span class="sxs-lookup"><span data-stu-id="94a58-263">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="94a58-264">Annotare l'ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="94a58-264">Write down the Application Id.</span></span> <span data-ttu-id="94a58-265">Viene usato come nome utente (**ID di accesso** nella procedura seguente) dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="94a58-265">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="94a58-266">L'entità servizio non ha le autorizzazioni per accedere alle risorse di Azure per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="94a58-266">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="94a58-267">È necessario concedere all'entità servizio le autorizzazioni per avviare e arrestare (deallocare) tutte le macchine virtuali del cluster.</span><span class="sxs-lookup"><span data-stu-id="94a58-267">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="94a58-268">Passare a https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="94a58-268">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="94a58-269">Aprire il pannello Tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="94a58-269">Open the All resources blade</span></span>
1. <span data-ttu-id="94a58-270">Selezionare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="94a58-270">Select the virtual machine</span></span>
1. <span data-ttu-id="94a58-271">Fare clic su Controllo di accesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="94a58-271">Click Access control (IAM)</span></span>
1. <span data-ttu-id="94a58-272">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="94a58-272">Click Add</span></span>
1. <span data-ttu-id="94a58-273">Selezionare il ruolo Proprietario</span><span class="sxs-lookup"><span data-stu-id="94a58-273">Select the role Owner</span></span>
1. <span data-ttu-id="94a58-274">Immettere il nome dell'applicazione creata in precedenza</span><span class="sxs-lookup"><span data-stu-id="94a58-274">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="94a58-275">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="94a58-275">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="94a58-276">**[1]** Creare il dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="94a58-276">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="94a58-277">Dopo aver modificato le autorizzazioni per le macchine virtuali, è possibile configurare i dispositivi STONITH nel cluster.</span><span class="sxs-lookup"><span data-stu-id="94a58-277">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="94a58-278">**[1]** Abilitare l'uso di un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="94a58-278">**[1]** Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="94a58-279">Configurazione di (A)SCS</span><span class="sxs-lookup"><span data-stu-id="94a58-279">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="94a58-280">Distribuzione di Linux</span><span class="sxs-lookup"><span data-stu-id="94a58-280">Deploying Linux</span></span>

<span data-ttu-id="94a58-281">Azure Marketplace contiene un'immagine per SUSE Linux Enterprise Server for SAP Applications 12 che è possibile usare per distribuire nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="94a58-281">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span> <span data-ttu-id="94a58-282">L'immagine del marketplace contiene l'agente delle risorse per SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="94a58-282">The marketplace image contains the resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="94a58-283">È possibile usare uno dei modelli di avvio rapido di GitHub per distribuire tutte le risorse necessarie.</span><span class="sxs-lookup"><span data-stu-id="94a58-283">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="94a58-284">Il modello consente di distribuire le macchine virtuali, il servizio di bilanciamento del carico, il set di disponibilità e così via. Per distribuire il modello, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="94a58-284">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="94a58-285">Aprire il [modello ASCS/SCS a più SID][template-multisid-xscs] o il [modello convergente][template-converged] nel portale di Azure. Il modello ASCS/SCS consente di creare solo le regole di bilanciamento del carico per le istanze ASCS/SCS e ERS di SAP NetWeaver (solo Linux), mentre il modello convergente crea anche le regole di bilanciamento del carico per un database, ad esempio Microsoft SQL Server o SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94a58-285">Open the [ASCS/SCS Multi SID template][template-multisid-xscs] or the [converged template][template-converged] on the Azure portal The ASCS/SCS template only creates the load-balancing rules for the SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas the converged template also creates the load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="94a58-286">Se si prevede di installare un sistema basato su SAP NetWeaver e si vuole installare anche il database nelle stesse macchine, usare il [modello convergente][template-converged].</span><span class="sxs-lookup"><span data-stu-id="94a58-286">If you plan to install an SAP NetWeaver based system and you also want to install the database on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="94a58-287">Immettere i parametri seguenti</span><span class="sxs-lookup"><span data-stu-id="94a58-287">Enter the following parameters</span></span>
   1. <span data-ttu-id="94a58-288">Prefisso di risorsa (solo modello ASCS/SCS a più SID)</span><span class="sxs-lookup"><span data-stu-id="94a58-288">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="94a58-289">Immettere il prefisso che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="94a58-289">Enter the prefix you want to use.</span></span> <span data-ttu-id="94a58-290">Il valore viene usato come prefisso per le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="94a58-290">The value is used as a prefix for the resources that are deployed.</span></span>
   3. <span data-ttu-id="94a58-291">ID del sistema SAP (solo modello convergente)</span><span class="sxs-lookup"><span data-stu-id="94a58-291">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="94a58-292">Immettere l'ID del sistema SAP che si vuole installare.</span><span class="sxs-lookup"><span data-stu-id="94a58-292">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="94a58-293">L'ID viene usato come prefisso per le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="94a58-293">The Id is used as a prefix for the resources that are deployed.</span></span>
   4. <span data-ttu-id="94a58-294">Tipo di stack</span><span class="sxs-lookup"><span data-stu-id="94a58-294">Stack Type</span></span>  
      <span data-ttu-id="94a58-295">Selezionare il tipo di stack SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="94a58-295">Select the SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="94a58-296">Tipo di sistema operativo</span><span class="sxs-lookup"><span data-stu-id="94a58-296">Os Type</span></span>  
      <span data-ttu-id="94a58-297">Selezionare una delle distribuzioni Linux.</span><span class="sxs-lookup"><span data-stu-id="94a58-297">Select one of the Linux distributions.</span></span> <span data-ttu-id="94a58-298">Per questo esempio, selezionare SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="94a58-298">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="94a58-299">Tipo di database</span><span class="sxs-lookup"><span data-stu-id="94a58-299">Db Type</span></span>  
      <span data-ttu-id="94a58-300">Selezionare HANA</span><span class="sxs-lookup"><span data-stu-id="94a58-300">Select HANA</span></span>
   7. <span data-ttu-id="94a58-301">Dimensioni del sistema SAP</span><span class="sxs-lookup"><span data-stu-id="94a58-301">Sap System Size</span></span>  
      <span data-ttu-id="94a58-302">Quantità di SAPS forniti dal nuovo sistema.</span><span class="sxs-lookup"><span data-stu-id="94a58-302">The amount of SAPS the new system provides.</span></span> <span data-ttu-id="94a58-303">Se non si è certi del numero di SAPS necessari per il sistema, chiedere all'integratore di sistemi o al partner tecnologico SAP.</span><span class="sxs-lookup"><span data-stu-id="94a58-303">If you are not sure how many SAPS the system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="94a58-304">Disponibilità del sistema</span><span class="sxs-lookup"><span data-stu-id="94a58-304">System Availability</span></span>  
      <span data-ttu-id="94a58-305">Selezionare la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="94a58-305">Select HA</span></span>
   9. <span data-ttu-id="94a58-306">Nome utente e password amministratore</span><span class="sxs-lookup"><span data-stu-id="94a58-306">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="94a58-307">Verrà creato un nuovo utente con cui è possibile accedere alla macchina</span><span class="sxs-lookup"><span data-stu-id="94a58-307">A new user is created that can be used to log on to the machine.</span></span>
   10. <span data-ttu-id="94a58-308">ID subnet</span><span class="sxs-lookup"><span data-stu-id="94a58-308">Subnet Id</span></span>  
   <span data-ttu-id="94a58-309">ID della subnet a cui devono essere connesse le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="94a58-309">The ID of the subnet to which the virtual machines should be connected to.</span></span>  <span data-ttu-id="94a58-310">Lasciare vuoto se si vuole creare una nuova rete virtuale o selezionare la stessa subnet usata o creata come parte della distribuzione del server NFS.</span><span class="sxs-lookup"><span data-stu-id="94a58-310">Leave empty if you want to create a new virtual network or select the same subnet that you used or created as part of the NFS server deployment.</span></span> <span data-ttu-id="94a58-311">L'ID in genere è simile al seguente: /subscriptions/**&lt;ID sottoscrizione&gt;**/resourceGroups/**&lt;nome gruppo risorse&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;nome rete virtuale&gt;**/subnets/**&lt;nome subnet&gt;**</span><span class="sxs-lookup"><span data-stu-id="94a58-311">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="94a58-312">Installazione</span><span class="sxs-lookup"><span data-stu-id="94a58-312">Installation</span></span>

<span data-ttu-id="94a58-313">Gli elementi seguenti sono preceduti dall'indicazione **[A]** - applicabile a tutti i nodi, **[1]** - applicabile solo al nodo 1 o **[2]** - applicabile solo al nodo 2.</span><span class="sxs-lookup"><span data-stu-id="94a58-313">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="94a58-314">**[A]** Aggiornare SLES</span><span class="sxs-lookup"><span data-stu-id="94a58-314">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="94a58-315">**[1]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="94a58-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="94a58-316">**[2]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="94a58-316">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="94a58-317">**[1]** Abilitare l'accesso SSH</span><span class="sxs-lookup"><span data-stu-id="94a58-317">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="94a58-318">**[A]** Installare l'estensione per la disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="94a58-318">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="94a58-319">**[A]**  Aggiornare gli agenti delle risorse SAP</span><span class="sxs-lookup"><span data-stu-id="94a58-319">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="94a58-320">È necessaria una patch per il pacchetto degli agenti delle risorse per usare la nuova configurazione descritta in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="94a58-320">A patch for the resource-agents package is required to use the new configuration, that is described in this article.</span></span> <span data-ttu-id="94a58-321">È possibile verificare se la patch è già installata con il comando seguente</span><span class="sxs-lookup"><span data-stu-id="94a58-321">You can check, if the patch is already installed with the following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="94a58-322">L'output dovrebbe essere simile al seguente</span><span class="sxs-lookup"><span data-stu-id="94a58-322">The output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="94a58-323">Se il comando grep non trova il parametro IS_ERS, è necessario installare la patch indicata nella [pagina di download di SUSE](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="94a58-323">If the grep command does not find the IS_ERS parameter, you need to install the patch listed on [the SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="94a58-324">**[A]** Configurare la risoluzione dei nomi host</span><span class="sxs-lookup"><span data-stu-id="94a58-324">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="94a58-325">È possibile usare un server DNS o modificare /etc/hosts in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="94a58-325">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="94a58-326">Questo esempio mostra come usare il file /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="94a58-326">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="94a58-327">Sostituire l'indirizzo IP e il nome host nei comandi seguenti</span><span class="sxs-lookup"><span data-stu-id="94a58-327">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="94a58-328">Inserire le righe seguenti in /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="94a58-328">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="94a58-329">Modificare l'indirizzo IP e il nome host in base all'ambiente</span><span class="sxs-lookup"><span data-stu-id="94a58-329">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="94a58-330">**[1]** Installare il cluster</span><span class="sxs-lookup"><span data-stu-id="94a58-330">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="94a58-331">**[2]** Aggiungere un nodo al cluster</span><span class="sxs-lookup"><span data-stu-id="94a58-331">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="94a58-332">**[A]** Modificare la password hacluster in modo da usare la stessa password</span><span class="sxs-lookup"><span data-stu-id="94a58-332">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="94a58-333">**[A]** Configurare corosync per usare un altro trasporto e aggiungere nodelist</span><span class="sxs-lookup"><span data-stu-id="94a58-333">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="94a58-334">In caso contrario, il cluster non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="94a58-334">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="94a58-335">Aggiungere il seguente contenuto in grassetto nel file.</span><span class="sxs-lookup"><span data-stu-id="94a58-335">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="94a58-336">Riavviare quindi il servizio corosync</span><span class="sxs-lookup"><span data-stu-id="94a58-336">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="94a58-337">**[A]** Installare i componenti drbd</span><span class="sxs-lookup"><span data-stu-id="94a58-337">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="94a58-338">**[A]** Creare una partizione per il dispositivo drbd</span><span class="sxs-lookup"><span data-stu-id="94a58-338">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="94a58-339">**[A]** Creare le configurazioni LVM</span><span class="sxs-lookup"><span data-stu-id="94a58-339">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="94a58-340">**[A]** Creare il dispositivo drbd SCS</span><span class="sxs-lookup"><span data-stu-id="94a58-340">**[A]** Create the SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="94a58-341">Inserire la configurazione per il nuovo dispositivo drbd e uscire</span><span class="sxs-lookup"><span data-stu-id="94a58-341">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="94a58-342">Creare il dispositivo drbd e avviarlo</span><span class="sxs-lookup"><span data-stu-id="94a58-342">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="94a58-343">**[A]** Creare il dispositivo drbd ERS</span><span class="sxs-lookup"><span data-stu-id="94a58-343">**[A]** Create the ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="94a58-344">Inserire la configurazione per il nuovo dispositivo drbd e uscire</span><span class="sxs-lookup"><span data-stu-id="94a58-344">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="94a58-345">Creare il dispositivo drbd e avviarlo</span><span class="sxs-lookup"><span data-stu-id="94a58-345">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="94a58-346">**[1]** Saltare la sincronizzazione iniziale</span><span class="sxs-lookup"><span data-stu-id="94a58-346">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="94a58-347">**[1]** Impostare il nodo primario</span><span class="sxs-lookup"><span data-stu-id="94a58-347">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="94a58-348">**[1]**  Attendere il completamento della sincronizzazione dei nuovi dispositivi drbd</span><span class="sxs-lookup"><span data-stu-id="94a58-348">**[1]** Wait until the new drbd devices are synchronized</span></span>

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

1. <span data-ttu-id="94a58-349">**[1]**  Creare i file system nei dispositivi drbd</span><span class="sxs-lookup"><span data-stu-id="94a58-349">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="94a58-350">Configurare il framework del cluster</span><span class="sxs-lookup"><span data-stu-id="94a58-350">Configure Cluster Framework</span></span>

<span data-ttu-id="94a58-351">**[1]** Modificare le impostazioni predefinite</span><span class="sxs-lookup"><span data-stu-id="94a58-351">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="94a58-352">Prepararsi per l'installazione di SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="94a58-352">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="94a58-353">**[A]** Creare le directory condivise</span><span class="sxs-lookup"><span data-stu-id="94a58-353">**[A]** Create the shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="94a58-354">**[A]** Configurare autofs</span><span class="sxs-lookup"><span data-stu-id="94a58-354">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="94a58-355">Creare un file con</span><span class="sxs-lookup"><span data-stu-id="94a58-355">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="94a58-356">Riavviare autofs per montare le nuove condivisioni</span><span class="sxs-lookup"><span data-stu-id="94a58-356">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="94a58-357">**[A]**  Configurare il file SWAP</span><span class="sxs-lookup"><span data-stu-id="94a58-357">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="94a58-358">Riavviare l'agente per attivare la modifica</span><span class="sxs-lookup"><span data-stu-id="94a58-358">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="94a58-359">Installazione di SAP NetWeaver ASCS/ERS</span><span class="sxs-lookup"><span data-stu-id="94a58-359">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="94a58-360">**[1]**  Creare una risorsa IP virtuale e un probe di integrità per il bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="94a58-360">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

   <span data-ttu-id="94a58-361">Assicurarsi che lo stato del cluster sia corretto e che tutte le risorse siano avviate.</span><span class="sxs-lookup"><span data-stu-id="94a58-361">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="94a58-362">Non è importante il nodo su cui sono in esecuzione le risorse.</span><span class="sxs-lookup"><span data-stu-id="94a58-362">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="94a58-363">**[1]** Installare SAP NetWeaver ASCS</span><span class="sxs-lookup"><span data-stu-id="94a58-363">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="94a58-364">Installare SAP NetWeaver ASCS come root nel primo nodo usando un nome host virtuale mappato all'indirizzo IP della configurazione front-end di bilanciamento del carico per l'istanza ASCS, ad esempio <b>nws ascs</b>, <b>10.0.0.10</b> e il numero di istanza usato per il probe del bilanciamento del carico, ad esempio <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="94a58-364">Install SAP NetWeaver ASCS as root on the first node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and the instance number that you used for the probe of the load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="94a58-365">È possibile usare il parametro sapinst SAPINST_REMOTE_ACCESS_USER per consentire a un utente non ROOT di connettersi a sapinst.</span><span class="sxs-lookup"><span data-stu-id="94a58-365">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="94a58-366">**[1]**  Creare una risorsa IP virtuale e un probe di integrità per il bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="94a58-366">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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
   # Do you still want to commit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="94a58-367">Assicurarsi che lo stato del cluster sia corretto e che tutte le risorse siano avviate.</span><span class="sxs-lookup"><span data-stu-id="94a58-367">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="94a58-368">Non è importante il nodo su cui sono in esecuzione le risorse.</span><span class="sxs-lookup"><span data-stu-id="94a58-368">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="94a58-369">**[2]** Installare SAP NetWeaver ERS</span><span class="sxs-lookup"><span data-stu-id="94a58-369">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="94a58-370">Installare SAP NetWeaver ERS come root nel secondo nodo usando un nome host virtuale mappato all'indirizzo IP della configurazione front-end di bilanciamento del carico per ERS, ad esempio <b>nws-ers</b>, <b>10.0.0.11</b> e il numero di istanza usato per il probe del bilanciamento del carico, ad esempio <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="94a58-370">Install SAP NetWeaver ERS as root on the second node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and the instance number that you used for the probe of the load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="94a58-371">È possibile usare il parametro sapinst SAPINST_REMOTE_ACCESS_USER per consentire a un utente non ROOT di connettersi a sapinst.</span><span class="sxs-lookup"><span data-stu-id="94a58-371">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="94a58-372">Usare SWPM SP 20 PL 05 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="94a58-372">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="94a58-373">Le versioni precedenti non impostano correttamente le autorizzazioni e l'installazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="94a58-373">Lower versions do not set the permissions correctly and the installation will fail.</span></span>
   > 

1. <span data-ttu-id="94a58-374">**[1]**  Adattare i profili di istanza ASCS/SCS e ERS</span><span class="sxs-lookup"><span data-stu-id="94a58-374">**[1]** Adapt the ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="94a58-375">Profilo ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="94a58-375">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change the restart command to a start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add the keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="94a58-376">Profilo ERS</span><span class="sxs-lookup"><span data-stu-id="94a58-376">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="94a58-377">**[A]**  Configurare keep-alive</span><span class="sxs-lookup"><span data-stu-id="94a58-377">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="94a58-378">Le comunicazioni tra il server applicazioni SAP NetWeaver e ASCS/SCS vengono instradate tramite un servizio di bilanciamento del carico software.</span><span class="sxs-lookup"><span data-stu-id="94a58-378">The communication between the SAP NetWeaver application server and the ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="94a58-379">Il servizio di bilanciamento del carico disconnette le connessioni inattive dopo un timeout configurabile.</span><span class="sxs-lookup"><span data-stu-id="94a58-379">The load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="94a58-380">Per evitare questo comportamento, è necessario impostare un parametro nel profilo ASCS/SCS di SAP NetWeaver e modificare le impostazioni di sistema di Linux.</span><span class="sxs-lookup"><span data-stu-id="94a58-380">To prevent this you need to set a parameter in the SAP NetWeaver ASCS/SCS profile and change the Linux system settings.</span></span> <span data-ttu-id="94a58-381">Per altre informazioni, leggere la [nota SAP 1410736][1410736].</span><span class="sxs-lookup"><span data-stu-id="94a58-381">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="94a58-382">Il parametro del profilo ASCS/SCS enque/encni/set_so_keepalive è già stato aggiunto nell'ultimo passaggio.</span><span class="sxs-lookup"><span data-stu-id="94a58-382">The ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in the last step.</span></span>

   <pre><code> 
   # Change the Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="94a58-383">**[A]** Configurare gli utenti SAP dopo l'installazione</span><span class="sxs-lookup"><span data-stu-id="94a58-383">**[A]** Configure the SAP users after the installation</span></span>
 
   <pre><code>
   # Add sidadm to the haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="94a58-384">**[1]**  Aggiungere i servizi SAP ASCS e ERS al file sapservice</span><span class="sxs-lookup"><span data-stu-id="94a58-384">**[1]** Add the ASCS and ERS SAP services to the sapservice file</span></span>

   <span data-ttu-id="94a58-385">Aggiungere la voce del servizio ASCS al secondo nodo e copiare la voce del servizio ERS nel primo nodo.</span><span class="sxs-lookup"><span data-stu-id="94a58-385">Add the ASCS service entry to the second node and copy the ERS service entry to the first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="94a58-386">**[1]** Creare le risorse del cluster SAP</span><span class="sxs-lookup"><span data-stu-id="94a58-386">**[1]** Create the SAP cluster resources</span></span>

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

   <span data-ttu-id="94a58-387">Assicurarsi che lo stato del cluster sia corretto e che tutte le risorse siano avviate.</span><span class="sxs-lookup"><span data-stu-id="94a58-387">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="94a58-388">Non è importante il nodo su cui sono in esecuzione le risorse.</span><span class="sxs-lookup"><span data-stu-id="94a58-388">It is not important on which node the resources are running.</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="94a58-389">Creare il dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="94a58-389">Create STONITH device</span></span>

<span data-ttu-id="94a58-390">Il dispositivo STONITH usa un'entità servizio per l'autorizzazione in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="94a58-390">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="94a58-391">Per creare un'entità servizio, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="94a58-391">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="94a58-392">Passare a <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="94a58-392">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="94a58-393">Aprire il pannello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94a58-393">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="94a58-394">Passare a Proprietà e annotare l'ID directory.</span><span class="sxs-lookup"><span data-stu-id="94a58-394">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="94a58-395">Si tratta dell'**ID tenant**.</span><span class="sxs-lookup"><span data-stu-id="94a58-395">This is the **tenant id**.</span></span>
1. <span data-ttu-id="94a58-396">Fare clic su Registrazioni per l'app</span><span class="sxs-lookup"><span data-stu-id="94a58-396">Click App registrations</span></span>
1. <span data-ttu-id="94a58-397">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="94a58-397">Click Add</span></span>
1. <span data-ttu-id="94a58-398">Immettere un nome, selezionare il tipo di applicazione "App Web/API", immettere un URL di accesso (ad esempio http://localhost) e fare clic su Crea</span><span class="sxs-lookup"><span data-stu-id="94a58-398">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="94a58-399">L'URL di accesso non viene usato e può essere qualsiasi URL valido</span><span class="sxs-lookup"><span data-stu-id="94a58-399">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="94a58-400">Selezionare la nuova app e fare clic su Chiavi nella scheda Impostazioni</span><span class="sxs-lookup"><span data-stu-id="94a58-400">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="94a58-401">Immettere una descrizione per una nuova chiave, selezionare "Non scade mai" e fare clic su Salva</span><span class="sxs-lookup"><span data-stu-id="94a58-401">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="94a58-402">Annotare il valore.</span><span class="sxs-lookup"><span data-stu-id="94a58-402">Write down the Value.</span></span> <span data-ttu-id="94a58-403">Viene usato come **password** per l'entità servizio</span><span class="sxs-lookup"><span data-stu-id="94a58-403">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="94a58-404">Annotare l'ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="94a58-404">Write down the Application Id.</span></span> <span data-ttu-id="94a58-405">Viene usato come nome utente (**ID di accesso** nella procedura seguente) dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="94a58-405">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="94a58-406">L'entità servizio non ha le autorizzazioni per accedere alle risorse di Azure per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="94a58-406">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="94a58-407">È necessario concedere all'entità servizio le autorizzazioni per avviare e arrestare (deallocare) tutte le macchine virtuali del cluster.</span><span class="sxs-lookup"><span data-stu-id="94a58-407">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="94a58-408">Passare a https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="94a58-408">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="94a58-409">Aprire il pannello Tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="94a58-409">Open the All resources blade</span></span>
1. <span data-ttu-id="94a58-410">Selezionare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="94a58-410">Select the virtual machine</span></span>
1. <span data-ttu-id="94a58-411">Fare clic su Controllo di accesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="94a58-411">Click Access control (IAM)</span></span>
1. <span data-ttu-id="94a58-412">Fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="94a58-412">Click Add</span></span>
1. <span data-ttu-id="94a58-413">Selezionare il ruolo Proprietario</span><span class="sxs-lookup"><span data-stu-id="94a58-413">Select the role Owner</span></span>
1. <span data-ttu-id="94a58-414">Immettere il nome dell'applicazione creata in precedenza</span><span class="sxs-lookup"><span data-stu-id="94a58-414">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="94a58-415">Fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="94a58-415">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="94a58-416">**[1]** Creare il dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="94a58-416">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="94a58-417">Dopo aver modificato le autorizzazioni per le macchine virtuali, è possibile configurare i dispositivi STONITH nel cluster.</span><span class="sxs-lookup"><span data-stu-id="94a58-417">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="94a58-418">**[1]** Abilitare l'uso di un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="94a58-418">**[1]** Enable the use of a STONITH device</span></span>

<span data-ttu-id="94a58-419">Abilitare l'uso di un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="94a58-419">Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="94a58-420">Installare il database</span><span class="sxs-lookup"><span data-stu-id="94a58-420">Install database</span></span>

<span data-ttu-id="94a58-421">In questo esempio viene installata e configurata una replica di sistema di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94a58-421">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="94a58-422">SAP HANA verrà eseguito nello stesso cluster di SAP NetWeaver ASCS/SCS ed ERS.</span><span class="sxs-lookup"><span data-stu-id="94a58-422">SAP HANA will run in the same cluster as the SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="94a58-423">È anche possibile installare SAP HANA in un cluster dedicato.</span><span class="sxs-lookup"><span data-stu-id="94a58-423">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="94a58-424">Per altre informazioni, vedere [Disponibilità elevata di SAP HANA in macchine virtuali di Azure (VM)][sap-hana-ha].</span><span class="sxs-lookup"><span data-stu-id="94a58-424">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="94a58-425">Prepararsi per l'installazione di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="94a58-425">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="94a58-426">È in genere consigliabile usare LVM per i volumi che archiviano i dati e file di log.</span><span class="sxs-lookup"><span data-stu-id="94a58-426">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="94a58-427">A scopo di test, è anche possibile scegliere di archiviare i dati e i file di log direttamente in un disco normale.</span><span class="sxs-lookup"><span data-stu-id="94a58-427">For testing purposes, you can also choose to store the data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="94a58-428">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="94a58-428">**[A]** LVM</span></span>  
   <span data-ttu-id="94a58-429">L'esempio seguente presuppone che le macchine virtuali abbiano quattro dischi dati collegati che devono essere usati per creare due volumi.</span><span class="sxs-lookup"><span data-stu-id="94a58-429">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
   
   <span data-ttu-id="94a58-430">Creare i volumi fisici per tutti i dischi da usare.</span><span class="sxs-lookup"><span data-stu-id="94a58-430">Create physical volumes for all disks that you want to use.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="94a58-431">Creare un gruppo di volumi per i file di dati, un gruppo di volumi per i file di log e uno per la directory condivisa di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="94a58-431">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="94a58-432">Creare i volumi logici</span><span class="sxs-lookup"><span data-stu-id="94a58-432">Create the logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="94a58-433">Creare le directory di montaggio e copiare l'UUID di tutti i volumi logici</span><span class="sxs-lookup"><span data-stu-id="94a58-433">Create the mount directories and copy the UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="94a58-434">Creare voci autofs per i tre volumi logici</span><span class="sxs-lookup"><span data-stu-id="94a58-434">Create autofs entries for the three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="94a58-435">Inserire questa riga in sudo vi /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="94a58-435">Insert this line to sudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="94a58-436">Montare i nuovi volumi</span><span class="sxs-lookup"><span data-stu-id="94a58-436">Mount the new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="94a58-437">**[A]** Dischi normali</span><span class="sxs-lookup"><span data-stu-id="94a58-437">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="94a58-438">Per sistemi demo o di piccole dimensioni, è possibile inserire i dati e i file di log HANA su un disco.</span><span class="sxs-lookup"><span data-stu-id="94a58-438">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="94a58-439">I comandi seguenti creano una partizione in /dev/sdc e la formattano con XFS.</span><span class="sxs-lookup"><span data-stu-id="94a58-439">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down the id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="94a58-440">Inserire questa riga in /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="94a58-440">Insert this line to /etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="94a58-441">Creare la directory di destinazione e montare il disco.</span><span class="sxs-lookup"><span data-stu-id="94a58-441">Create the target directory and mount the disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="94a58-442">Installazione di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="94a58-442">Installing SAP HANA</span></span>

<span data-ttu-id="94a58-443">I passaggi seguenti sono basati sul capitolo 4 della guida [SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] (Scenario di ottimizzazione delle prestazioni di SAP HANA SR) per installare la replica di sistema di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94a58-443">The following steps are based on chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span> <span data-ttu-id="94a58-444">È consigliabile leggerlo prima di continuare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="94a58-444">Please read it before you continue the installation.</span></span>

1. <span data-ttu-id="94a58-445">**[A]** Eseguire hdblcm dal DVD di HANA</span><span class="sxs-lookup"><span data-stu-id="94a58-445">**[A]** Run hdblcm from the HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="94a58-446">**[A]** Aggiornare l'agente host SAP</span><span class="sxs-lookup"><span data-stu-id="94a58-446">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="94a58-447">Scaricare l'archivio dell'agente host SAP più recente dal sito [SAP Softwarecenter] [sap-swcenter] ed eseguire il comando seguente per aggiornare l'agente.</span><span class="sxs-lookup"><span data-stu-id="94a58-447">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="94a58-448">Sostituire il percorso dell'archivio in modo da puntare al file scaricato.</span><span class="sxs-lookup"><span data-stu-id="94a58-448">Replace the path to the archive to point to the file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path to SAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="94a58-449">**[1]** Creare la replica HANA (come root)</span><span class="sxs-lookup"><span data-stu-id="94a58-449">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="94a58-450">Eseguire il comando indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="94a58-450">Run the following command.</span></span> <span data-ttu-id="94a58-451">Assicurarsi di sostituire le stringhe in grassetto (ID di sistema HANA HDB e numero di istanza 03) con i valori dell'installazione di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94a58-451">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="94a58-452">**[A]** Creare una voce di archivio chiavi (come root)</span><span class="sxs-lookup"><span data-stu-id="94a58-452">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="94a58-453">**[1]** Eseguire il backup del database (come root)</span><span class="sxs-lookup"><span data-stu-id="94a58-453">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="94a58-454">**[1]** Passare all'utente sapsid HANA e creare il sito primario.</span><span class="sxs-lookup"><span data-stu-id="94a58-454">**[1]** Switch to the HANA sapsid user and create the primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="94a58-455">**[2]** Passare all'utente sapsid HANA e creare il sito secondario.</span><span class="sxs-lookup"><span data-stu-id="94a58-455">**[2]** Switch to the HANA sapsid user and create the secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="94a58-456">**[1]** Creare le risorse del cluster SAP HANA</span><span class="sxs-lookup"><span data-stu-id="94a58-456">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="94a58-457">Prima di tutto, creare la topologia.</span><span class="sxs-lookup"><span data-stu-id="94a58-457">First, create the topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number and HANA system id
   
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
   
   <span data-ttu-id="94a58-458">Creare poi le risorse SAP HANA</span><span class="sxs-lookup"><span data-stu-id="94a58-458">Next, create the HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
    
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

   <span data-ttu-id="94a58-459">Assicurarsi che lo stato del cluster sia corretto e che tutte le risorse siano avviate.</span><span class="sxs-lookup"><span data-stu-id="94a58-459">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="94a58-460">Non è importante il nodo su cui sono in esecuzione le risorse.</span><span class="sxs-lookup"><span data-stu-id="94a58-460">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="94a58-461">**[1]** Installare l'istanza del database di SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="94a58-461">**[1]** Install the SAP NetWeaver database instance</span></span>

   <span data-ttu-id="94a58-462">Installare l'istanza del database di SAP NetWeaver come root usando un nome host virtuale mappato all'indirizzo IP della configurazione front-end di bilanciamento del carico per il database, ad esempio <b>nws-db</b> e <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="94a58-462">Install the SAP NetWeaver database instance as root using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="94a58-463">È possibile usare il parametro sapinst SAPINST_REMOTE_ACCESS_USER per consentire a un utente non ROOT di connettersi a sapinst.</span><span class="sxs-lookup"><span data-stu-id="94a58-463">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="94a58-464">Installazione del server applicazioni di SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="94a58-464">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="94a58-465">Per installare il server applicazioni SAP, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="94a58-465">Follow these steps to install an SAP application server.</span></span> <span data-ttu-id="94a58-466">I passaggi seguenti presuppongono che il server applicazioni venga installato in un server diverso dai server ASCS/SCS e HANA.</span><span class="sxs-lookup"><span data-stu-id="94a58-466">The steps bellow assume that you install the application server on a server different from the ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="94a58-467">Diversamente, alcuni dei passaggi seguenti non sono necessari, ad esempio la configurazione della risoluzione dei nomi host.</span><span class="sxs-lookup"><span data-stu-id="94a58-467">Otherwise some of the steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="94a58-468">Configurare la risoluzione dei nomi host</span><span class="sxs-lookup"><span data-stu-id="94a58-468">Setup host name resolution</span></span>    
   <span data-ttu-id="94a58-469">È possibile usare un server DNS o modificare /etc/hosts in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="94a58-469">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="94a58-470">Questo esempio mostra come usare il file /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="94a58-470">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="94a58-471">Sostituire l'indirizzo IP e il nome host nei comandi seguenti</span><span class="sxs-lookup"><span data-stu-id="94a58-471">Replace the IP address and the hostname in the following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="94a58-472">Inserire le righe seguenti in /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="94a58-472">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="94a58-473">Modificare l'indirizzo IP e il nome host in base all'ambiente</span><span class="sxs-lookup"><span data-stu-id="94a58-473">Change the IP address and hostname to match your environment</span></span>    
    
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of the application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="94a58-474">Creare la directory sapmnt</span><span class="sxs-lookup"><span data-stu-id="94a58-474">Create the sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="94a58-475">Configurare autofs</span><span class="sxs-lookup"><span data-stu-id="94a58-475">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="94a58-476">Creare un nuovo file con</span><span class="sxs-lookup"><span data-stu-id="94a58-476">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="94a58-477">Riavviare autofs per montare le nuove condivisioni</span><span class="sxs-lookup"><span data-stu-id="94a58-477">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="94a58-478">Configurare il file SWAP</span><span class="sxs-lookup"><span data-stu-id="94a58-478">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="94a58-479">Riavviare l'agente per attivare la modifica</span><span class="sxs-lookup"><span data-stu-id="94a58-479">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="94a58-480">Installare il server applicazioni di SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="94a58-480">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="94a58-481">Installare un server applicazioni di SAP NetWeaver primario o aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="94a58-481">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="94a58-482">È possibile usare il parametro sapinst SAPINST_REMOTE_ACCESS_USER per consentire a un utente non ROOT di connettersi a sapinst.</span><span class="sxs-lookup"><span data-stu-id="94a58-482">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="94a58-483">Aggiornare l'archivio sicuro di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="94a58-483">Update SAP HANA secure store</span></span>

   <span data-ttu-id="94a58-484">Aggiornare l'archivio sicuro di SAP HANA in modo che punti al nome virtuale della configurazione della replica di sistema di SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="94a58-484">Update the SAP HANA secure store to point to the virtual name of the SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="94a58-485">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94a58-485">Next steps</span></span>
* <span data-ttu-id="94a58-486">[Pianificazione e implementazione di Macchine virtuali di Azure per SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="94a58-486">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="94a58-487">[Distribuzione di Macchine virtuali di Azure per SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="94a58-487">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="94a58-488">[Distribuzione DBMS di Macchine virtuali di Azure per SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="94a58-488">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="94a58-489">Per informazioni su come stabilire la disponibilità elevata e pianificare il ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni), vedere [Disponibilità elevata e ripristino di emergenza di SAP HANA (istanze di grandi dimensioni) in Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="94a58-489">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="94a58-490">Per informazioni su come ottenere la disponibilità elevata e un piano di ripristino di emergenza di SAP HANA nelle macchine virtuali di Azure, vedere [Disponibilità elevata di SAP HANA nelle macchine virtuali di Azure (VM)][sap-hana-ha].</span><span class="sxs-lookup"><span data-stu-id="94a58-490">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>