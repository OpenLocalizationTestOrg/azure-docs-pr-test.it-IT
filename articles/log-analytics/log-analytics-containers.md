---
title: soluzione di monitoraggio in Azure Log Analitica aaaContainer | Documenti Microsoft
description: soluzione di monitoraggio della contenitore nel Log Analitica Hello consente di visualizzare e gestire Docker e Windows host contenitore in un'unica posizione.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="22326-103">Soluzione Monitoraggio contenitori in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="22326-103">Container Monitoring solution in Log Analytics</span></span>

![Simbolo di Contenitori](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="22326-105">In questo articolo viene descritto come tooset backup e utilizzare hello contenitore monitoraggio soluzione Analitica di Log, che consente di visualizzare e gestire Docker e Windows host contenitore in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="22326-105">This article describes how tooset up and use hello Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="22326-106">Docker è un sistema di virtualizzazione software utilizzati contenitori toocreate che consentono di automatizzare la distribuzione di software tootheir IT dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="22326-106">Docker is a software virtualization system used toocreate containers that automate software deployment tootheir IT infrastructure.</span></span>

<span data-ttu-id="22326-107">soluzione Mostra contenitori in esecuzione, quali immagini contenitore vengono eseguiti, Hello e in cui vengono eseguiti i contenitori.</span><span class="sxs-lookup"><span data-stu-id="22326-107">hello solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="22326-108">È possibile visualizzare informazioni di controllo dettagliate che indicano i comandi usati con i contenitori.</span><span class="sxs-lookup"><span data-stu-id="22326-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="22326-109">E, è possibile risolvere i contenitori mediante la visualizzazione e la ricerca di log centralizzato senza visualizzazione tooremotely Docker o host di Windows.</span><span class="sxs-lookup"><span data-stu-id="22326-109">And, you can troubleshoot containers by viewing and searching centralized logs without having tooremotely view Docker or Windows hosts.</span></span> <span data-ttu-id="22326-110">È possibile trovare contenitori che consumano una quantità eccessiva di risorse in un host.</span><span class="sxs-lookup"><span data-stu-id="22326-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="22326-111">È anche possibile visualizzare informazioni centralizzate su utilizzo di CPU, memoria, archiviazione e rete e sulle prestazioni dei contenitori.</span><span class="sxs-lookup"><span data-stu-id="22326-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="22326-112">Nei computer che eseguono Windows, è possibile centralizzare e confrontare i log dai contenitori Windows Server, Hyper-V e Docker.</span><span class="sxs-lookup"><span data-stu-id="22326-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="22326-113">soluzione Hello supporta hello orchestrators contenitore seguente:</span><span class="sxs-lookup"><span data-stu-id="22326-113">hello solution supports hello following container orchestrators:</span></span>

- <span data-ttu-id="22326-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="22326-114">Docker Swarm</span></span>
- <span data-ttu-id="22326-115">Controller di dominio/sistema operativo</span><span class="sxs-lookup"><span data-stu-id="22326-115">DC/OS</span></span>
- <span data-ttu-id="22326-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="22326-116">Kubernetes</span></span>
- <span data-ttu-id="22326-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="22326-117">Service Fabric</span></span>
- <span data-ttu-id="22326-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="22326-118">Red Hat OpenShift</span></span>


<span data-ttu-id="22326-119">Hello diagramma seguente mostra le relazioni di hello tra vari host contenitore e di agenti con OMS.</span><span class="sxs-lookup"><span data-stu-id="22326-119">hello following diagram shows hello relationships between various container hosts and agents with OMS.</span></span>

![Diagramma dei contenitori](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="22326-121">Requisiti di sistema</span><span class="sxs-lookup"><span data-stu-id="22326-121">System requirements</span></span>

<span data-ttu-id="22326-122">Prima di iniziare, esaminare hello seguenti siano soddisfatti i prerequisiti di hello tooverify di dettagli.</span><span class="sxs-lookup"><span data-stu-id="22326-122">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="22326-123">Supporto della soluzione di monitoraggio del contenitore per l'orchestrazione di Docker e la piattaforma del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="22326-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="22326-124">Hello tabella seguente vengono illustrati hello orchestrazione Docker e supporto di inventario di contenitore, prestazioni e i registri con Analitica di Log di controllo del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="22326-124">hello following table outlines hello Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="22326-125">ACS</span><span class="sxs-lookup"><span data-stu-id="22326-125">ACS</span></span> | <span data-ttu-id="22326-126">Linux</span><span class="sxs-lookup"><span data-stu-id="22326-126">Linux</span></span> | <span data-ttu-id="22326-127">Windows</span><span class="sxs-lookup"><span data-stu-id="22326-127">Windows</span></span> | <span data-ttu-id="22326-128">Contenitore</span><span class="sxs-lookup"><span data-stu-id="22326-128">Container</span></span><br><span data-ttu-id="22326-129">Inventario</span><span class="sxs-lookup"><span data-stu-id="22326-129">Inventory</span></span> | <span data-ttu-id="22326-130">Image</span><span class="sxs-lookup"><span data-stu-id="22326-130">Image</span></span><br><span data-ttu-id="22326-131">Inventario</span><span class="sxs-lookup"><span data-stu-id="22326-131">Inventory</span></span> | <span data-ttu-id="22326-132">Nodo</span><span class="sxs-lookup"><span data-stu-id="22326-132">Node</span></span><br><span data-ttu-id="22326-133">Inventario</span><span class="sxs-lookup"><span data-stu-id="22326-133">Inventory</span></span> | <span data-ttu-id="22326-134">Contenitore</span><span class="sxs-lookup"><span data-stu-id="22326-134">Container</span></span><br><span data-ttu-id="22326-135">Prestazioni</span><span class="sxs-lookup"><span data-stu-id="22326-135">Performance</span></span> | <span data-ttu-id="22326-136">Contenitore</span><span class="sxs-lookup"><span data-stu-id="22326-136">Container</span></span><br><span data-ttu-id="22326-137">Evento</span><span class="sxs-lookup"><span data-stu-id="22326-137">Event</span></span> | <span data-ttu-id="22326-138">Evento</span><span class="sxs-lookup"><span data-stu-id="22326-138">Event</span></span><br><span data-ttu-id="22326-139">Log</span><span class="sxs-lookup"><span data-stu-id="22326-139">Log</span></span> | <span data-ttu-id="22326-140">Contenitore</span><span class="sxs-lookup"><span data-stu-id="22326-140">Container</span></span><br><span data-ttu-id="22326-141">Log</span><span class="sxs-lookup"><span data-stu-id="22326-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="22326-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="22326-142">Kubernetes</span></span> | <span data-ttu-id="22326-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-143">&#8226;</span></span> | <span data-ttu-id="22326-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-144">&#8226;</span></span> | | <span data-ttu-id="22326-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-145">&#8226;</span></span> | <span data-ttu-id="22326-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-146">&#8226;</span></span> | <span data-ttu-id="22326-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-147">&#8226;</span></span> | <span data-ttu-id="22326-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-148">&#8226;</span></span> | <span data-ttu-id="22326-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-149">&#8226;</span></span> | <span data-ttu-id="22326-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-150">&#8226;</span></span> | <span data-ttu-id="22326-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-151">&#8226;</span></span> |
| <span data-ttu-id="22326-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="22326-152">Mesosphere</span></span><br><span data-ttu-id="22326-153">Controller di dominio/sistema operativo</span><span class="sxs-lookup"><span data-stu-id="22326-153">DC/OS</span></span> | <span data-ttu-id="22326-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-154">&#8226;</span></span> | <span data-ttu-id="22326-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-155">&#8226;</span></span> | | <span data-ttu-id="22326-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-156">&#8226;</span></span> | <span data-ttu-id="22326-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-157">&#8226;</span></span> | <span data-ttu-id="22326-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-158">&#8226;</span></span> | <span data-ttu-id="22326-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-159">&#8226;</span></span>| <span data-ttu-id="22326-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-160">&#8226;</span></span> | <span data-ttu-id="22326-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-161">&#8226;</span></span> | <span data-ttu-id="22326-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-162">&#8226;</span></span> |
| <span data-ttu-id="22326-163">Docker</span><span class="sxs-lookup"><span data-stu-id="22326-163">Docker</span></span><br><span data-ttu-id="22326-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="22326-164">Swarm</span></span> | <span data-ttu-id="22326-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-165">&#8226;</span></span> | <span data-ttu-id="22326-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-166">&#8226;</span></span> | <span data-ttu-id="22326-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-167">&#8226;</span></span> | <span data-ttu-id="22326-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-168">&#8226;</span></span> | <span data-ttu-id="22326-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-169">&#8226;</span></span> | <span data-ttu-id="22326-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-170">&#8226;</span></span> | <span data-ttu-id="22326-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-171">&#8226;</span></span> | <span data-ttu-id="22326-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-172">&#8226;</span></span> | | <span data-ttu-id="22326-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-173">&#8226;</span></span> |
| <span data-ttu-id="22326-174">Service</span><span class="sxs-lookup"><span data-stu-id="22326-174">Service</span></span><br><span data-ttu-id="22326-175">Infrastruttura</span><span class="sxs-lookup"><span data-stu-id="22326-175">Fabric</span></span> | | | <span data-ttu-id="22326-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-176">&#8226;</span></span> | <span data-ttu-id="22326-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-177">&#8226;</span></span> | <span data-ttu-id="22326-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-178">&#8226;</span></span> | <span data-ttu-id="22326-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-179">&#8226;</span></span> | <span data-ttu-id="22326-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-180">&#8226;</span></span> | <span data-ttu-id="22326-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-181">&#8226;</span></span> | <span data-ttu-id="22326-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-182">&#8226;</span></span> | <span data-ttu-id="22326-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-183">&#8226;</span></span> |
| <span data-ttu-id="22326-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="22326-184">Red Hat Open</span></span><br><span data-ttu-id="22326-185">MAIUSC</span><span class="sxs-lookup"><span data-stu-id="22326-185">Shift</span></span> | | <span data-ttu-id="22326-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-186">&#8226;</span></span> | | <span data-ttu-id="22326-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-187">&#8226;</span></span> | <span data-ttu-id="22326-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-188">&#8226;</span></span>| <span data-ttu-id="22326-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-189">&#8226;</span></span> | <span data-ttu-id="22326-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-190">&#8226;</span></span> | <span data-ttu-id="22326-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-191">&#8226;</span></span> | | <span data-ttu-id="22326-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-192">&#8226;</span></span> |
| <span data-ttu-id="22326-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="22326-193">Windows Server</span></span><br><span data-ttu-id="22326-194">(autonomo)</span><span class="sxs-lookup"><span data-stu-id="22326-194">(standalone)</span></span> | | | <span data-ttu-id="22326-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-195">&#8226;</span></span> | <span data-ttu-id="22326-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-196">&#8226;</span></span> | <span data-ttu-id="22326-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-197">&#8226;</span></span> | <span data-ttu-id="22326-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-198">&#8226;</span></span> | <span data-ttu-id="22326-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-199">&#8226;</span></span> | <span data-ttu-id="22326-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-200">&#8226;</span></span> | | <span data-ttu-id="22326-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-201">&#8226;</span></span> |
| <span data-ttu-id="22326-202">Server Linux</span><span class="sxs-lookup"><span data-stu-id="22326-202">Linux Server</span></span><br><span data-ttu-id="22326-203">(autonomo)</span><span class="sxs-lookup"><span data-stu-id="22326-203">(standalone)</span></span> | | <span data-ttu-id="22326-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-204">&#8226;</span></span> | | <span data-ttu-id="22326-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-205">&#8226;</span></span> | <span data-ttu-id="22326-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-206">&#8226;</span></span> | <span data-ttu-id="22326-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-207">&#8226;</span></span> | <span data-ttu-id="22326-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-208">&#8226;</span></span> | <span data-ttu-id="22326-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-209">&#8226;</span></span> | | <span data-ttu-id="22326-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="22326-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="22326-211">Versioni di Docker supportate in Linux</span><span class="sxs-lookup"><span data-stu-id="22326-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="22326-212">Docker 1.11 too1.13</span><span class="sxs-lookup"><span data-stu-id="22326-212">Docker 1.11 too1.13</span></span>
- <span data-ttu-id="22326-213">Docker CE e EE v17.06</span><span class="sxs-lookup"><span data-stu-id="22326-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="22326-214">Distribuzioni Linux x64 supportate come host del contenitore</span><span class="sxs-lookup"><span data-stu-id="22326-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="22326-215">Ubuntu 14.04 LTS e 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="22326-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="22326-216">CoreOS (stable)</span><span class="sxs-lookup"><span data-stu-id="22326-216">CoreOS(stable)</span></span>
- <span data-ttu-id="22326-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="22326-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="22326-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="22326-218">openSUSE 13.2</span></span>
- <span data-ttu-id="22326-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="22326-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="22326-220">CentOS 7.2 e 7.3</span><span class="sxs-lookup"><span data-stu-id="22326-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="22326-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="22326-221">SLES 12</span></span>
- <span data-ttu-id="22326-222">RHEL 7.2 e 7.3</span><span class="sxs-lookup"><span data-stu-id="22326-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="22326-223">Red Hat OpenShift Container Platform (OCP) 3.4 e 3.5</span><span class="sxs-lookup"><span data-stu-id="22326-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="22326-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span><span class="sxs-lookup"><span data-stu-id="22326-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span></span>
- <span data-ttu-id="22326-225">ACS Kubernetes 1.4.5 too1.6</span><span class="sxs-lookup"><span data-stu-id="22326-225">ACS Kubernetes 1.4.5 too1.6</span></span>
- <span data-ttu-id="22326-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="22326-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="22326-227">Sistema operativo Windows supportato</span><span class="sxs-lookup"><span data-stu-id="22326-227">Supported Windows operating system</span></span>

- <span data-ttu-id="22326-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="22326-228">Windows Server 2016</span></span>
- <span data-ttu-id="22326-229">Versione di Windows per il 10° anniversario (professionale o aziendale)</span><span class="sxs-lookup"><span data-stu-id="22326-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="22326-230">Versioni di Docker supportate in Windows</span><span class="sxs-lookup"><span data-stu-id="22326-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="22326-231">Docker 1.12 e 1.13</span><span class="sxs-lookup"><span data-stu-id="22326-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="22326-232">Docker 17.03.0 e successive</span><span class="sxs-lookup"><span data-stu-id="22326-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="22326-233">Installazione e configurazione di soluzione hello</span><span class="sxs-lookup"><span data-stu-id="22326-233">Installing and configuring hello solution</span></span>
<span data-ttu-id="22326-234">Utilizzare hello tooinstall le informazioni seguenti e configurare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="22326-234">Use hello following information tooinstall and configure hello solution.</span></span>

1. <span data-ttu-id="22326-235">Aggiungere hello contenitore monitoraggio soluzione tooyour area di lavoro OMS da [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="22326-235">Add hello Container Monitoring solution tooyour OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="22326-236">Installare e usare Docker con un agente OMS.</span><span class="sxs-lookup"><span data-stu-id="22326-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="22326-237">In base al sistema operativo, è possibile scegliere tra hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="22326-237">Based on your operating system, you can choose from hello following methods:</span></span>

  * <span data-ttu-id="22326-238">Nei sistemi operativi Linux supportati, installare e l'esecuzione di Docker e quindi installare e configurare hello [agente OMS per Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="22326-238">On supported Linux operating systems, install and run Docker and then install and configure hello [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="22326-239">In CoreOS, è possibile eseguire hello agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="22326-239">On CoreOS, you cannot run hello OMS Agent for Linux.</span></span> <span data-ttu-id="22326-240">Eseguire invece una versione nei contenitori di hello agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="22326-240">Instead, you run a containerized version of hello OMS Agent for Linux.</span></span> <span data-ttu-id="22326-241">Vedere la sezione [Per tutti gli host del contenitore Linux inclusi CoreOS](#for-all-linux-container-hosts-including-coreos) o [Per tutti gli host del contenitore Linux Azure per enti pubblici incluso CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) se si usano contenitori nel cloud di Azure per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="22326-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="22326-242">In Windows Server 2016 e Windows 10, è possibile installare hello motore Docker e il client quindi connettersi informazioni toogather agente e inviarlo tooLog Analitica.</span><span class="sxs-lookup"><span data-stu-id="22326-242">On Windows Server 2016 and Windows 10, install hello Docker Engine and client then connect an agent toogather information and send it tooLog Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="22326-243">Servizi contenitore</span><span class="sxs-lookup"><span data-stu-id="22326-243">Container services</span></span>

- <span data-ttu-id="22326-244">Se si opera in un ambiente Red Hat OpenShift, vedere [Configurare un agente OMS per Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="22326-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="22326-245">Se si dispone di un cluster di Kubernetes utilizzando hello servizio contenitore di Azure, consultare [monitorare un cluster il servizio contenitore di Azure con Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="22326-245">If you have a Kubernetes cluster using hello Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="22326-246">Se si ha un cluster DC/OS del servizio contenitore di Azure, vedere [Monitorare un cluster DC/OS del servizio contenitore di Azure con Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="22326-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="22326-247">Se è presente un ambiente in modalità Docker Swarm, per altre informazioni vedere [Configurare un agente OMS per Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="22326-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="22326-248">Se si usano contenitori con Service Fabric, vedere [Panoramica di Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="22326-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="22326-249">Hello revisione [motore Docker in Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) articolo per ulteriori informazioni su come tooinstall e configurare i motori di Docker su computer che eseguono Windows.</span><span class="sxs-lookup"><span data-stu-id="22326-249">Review hello [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how tooinstall and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22326-250">Deve essere in esecuzione di docker **prima** installare hello [agente OMS per Linux](log-analytics-agent-linux.md) negli host contenitore.</span><span class="sxs-lookup"><span data-stu-id="22326-250">Docker must be running **before** you install hello [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="22326-251">Se è già stato installato l'agente di hello prima di installare Docker, è necessario tooreinstall hello agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="22326-251">If you've already installed hello agent before installing Docker, you need tooreinstall hello OMS Agent for Linux.</span></span> <span data-ttu-id="22326-252">Per ulteriori informazioni su Docker, vedere hello [sito Web di Docker](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="22326-252">For more information about Docker, see hello [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="22326-253">Host del contenitore Linux</span><span class="sxs-lookup"><span data-stu-id="22326-253">Linux container hosts</span></span>

<span data-ttu-id="22326-254">Dopo aver installato Docker, usare hello seguenti impostazioni per l'agente di hello tooconfigure host contenitore per l'utilizzo con Docker.</span><span class="sxs-lookup"><span data-stu-id="22326-254">After you've installed Docker, use hello following settings for your container host tooconfigure hello agent for use with Docker.</span></span> <span data-ttu-id="22326-255">È necessario l'ID area di lavoro OMS e la chiave, che è possibile trovare nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="22326-255">First you need your OMS workspace ID and key, which you can find in hello Azure portal.</span></span> <span data-ttu-id="22326-256">Nell'area di lavoro, fare clic su **avvio rapido** > **computer** tooview il **ID area di lavoro** e **chiave primaria**.</span><span class="sxs-lookup"><span data-stu-id="22326-256">In your workspace, click **Quick Start** > **Computers** tooview your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="22326-257">Copiare e incollare entrambi i valori nell'editor predefinito.</span><span class="sxs-lookup"><span data-stu-id="22326-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="22326-258">Per tutti gli host del contenitore Linux, ad eccezione di CoreOS</span><span class="sxs-lookup"><span data-stu-id="22326-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="22326-259">Per ulteriori informazioni e procedure su come tooinstall hello agente OMS per Linux, vedere [connettersi il tooOperations computer Linux Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="22326-259">For more information and steps on how tooinstall hello OMS Agent for Linux, see [Connect your Linux Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="22326-260">Per tutti gli host del contenitore Linux inclusi CoreOS</span><span class="sxs-lookup"><span data-stu-id="22326-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="22326-261">Avviare il contenitore OMS hello che si desidera toomonitor.</span><span class="sxs-lookup"><span data-stu-id="22326-261">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="22326-262">Modificare e usare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="22326-262">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="22326-263">Per tutti gli host del contenitore Linux Azure per enti pubblici incluso CoreOS</span><span class="sxs-lookup"><span data-stu-id="22326-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="22326-264">Avviare il contenitore OMS hello che si desidera toomonitor.</span><span class="sxs-lookup"><span data-stu-id="22326-264">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="22326-265">Modificare e usare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="22326-265">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a><span data-ttu-id="22326-266">Il passaggio da utilizzando un tooone di agente Linux installato in un contenitore</span><span class="sxs-lookup"><span data-stu-id="22326-266">Switching from using an installed Linux agent tooone in a container</span></span>
<span data-ttu-id="22326-267">Se si precedentemente utilizzato agente installato direttamente hello e si desidera utilizzare tooinstead un agente in esecuzione in un contenitore, è necessario innanzitutto rimuovere hello agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="22326-267">If you previously used hello directly-installed agent and want tooinstead use an agent running in a container, you must first remove hello OMS Agent for Linux.</span></span> <span data-ttu-id="22326-268">Vedere [hello il processo di disinstallazione agente OMS per Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand come toosuccessfully disinstallare hello agente.</span><span class="sxs-lookup"><span data-stu-id="22326-268">See [Uninstalling hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand how toosuccessfully uninstall hello agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="22326-269">Configurare un agente OMS per Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="22326-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="22326-270">È possibile eseguire hello agente OMS come servizio globale su Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="22326-270">You can run hello OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="22326-271">Utilizzare hello seguente informazioni toocreate un servizio dell'agente OMS.</span><span class="sxs-lookup"><span data-stu-id="22326-271">Use hello following information toocreate an OMS Agent service.</span></span> <span data-ttu-id="22326-272">È necessario tooinsert l'ID area di lavoro OMS e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="22326-272">You need tooinsert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="22326-273">Eseguire l'istruzione seguente hello su nodo principale hello.</span><span class="sxs-lookup"><span data-stu-id="22326-273">Run hello following on hello master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="22326-274">Configurare un agente OMS per Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="22326-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="22326-275">Esistono tre modi tooadd hello agente OMS tooRed Hat OpenShift toostart raccolta contenitore dati di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="22326-275">There are three ways tooadd hello OMS Agent tooRed Hat OpenShift toostart collecting container monitoring data.</span></span>

* <span data-ttu-id="22326-276">[Installare hello agente OMS per Linux](log-analytics-agent-linux.md) direttamente in ogni nodo OpenShift</span><span class="sxs-lookup"><span data-stu-id="22326-276">[Install hello OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="22326-277">[Abilitare l'estensione della macchina virtuale di Log Analytics](log-analytics-azure-vm-extension.md) in ogni nodo OpenShift che risiede in Azure</span><span class="sxs-lookup"><span data-stu-id="22326-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="22326-278">Installare l'agente OMS hello come un set di daemon OpenShift</span><span class="sxs-lookup"><span data-stu-id="22326-278">Install hello OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="22326-279">In questa sezione viene illustrata hello passaggi necessari tooinstall hello agente OMS come un set di daemon OpenShift.</span><span class="sxs-lookup"><span data-stu-id="22326-279">In this section we cover hello steps required tooinstall hello OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="22326-280">Accesso toohello OpenShift nodo e copia hello yaml file master [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) da GitHub tooyour master nodo e modificare il valore di hello con l'ID dell'area di lavoro OMS e con la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="22326-280">Sign on toohello OpenShift master node and copy hello yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub tooyour master node and modify hello value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="22326-281">Eseguire un progetto di hello toocreate i comandi seguenti per OMS e impostare l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="22326-281">Run hello following commands toocreate a project for OMS and set hello user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="22326-282">hello toodeploy set daemon, eseguire hello:</span><span class="sxs-lookup"><span data-stu-id="22326-282">toodeploy hello daemon-set, run hello following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="22326-283">tooverify è configurato e che funzioni correttamente, digitare il seguente di hello:</span><span class="sxs-lookup"><span data-stu-id="22326-283">tooverify it is configured and working correctly, type hello following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="22326-284">e l'output di hello dovrebbe essere simile:</span><span class="sxs-lookup"><span data-stu-id="22326-284">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

<span data-ttu-id="22326-285">Se si desidera toouse segreti toosecure l'ID area di lavoro OMS e la chiave primaria quando si utilizza hello agente OMS yaml daemon-set di file, eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="22326-285">If you want toouse secrets toosecure your OMS Workspace ID and Primary Key when using hello OMS Agent daemon-set yaml file, perform hello following steps.</span></span>

1. <span data-ttu-id="22326-286">Accesso toohello OpenShift nodo e copia hello yaml file master [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) e il segreto di generazione dello script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) da GitHub.</span><span class="sxs-lookup"><span data-stu-id="22326-286">Sign on toohello OpenShift master node and copy hello yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="22326-287">Lo script genererà hello segreti yaml file toosecure ID area di lavoro OMS e la chiave primaria il secrete informazioni.</span><span class="sxs-lookup"><span data-stu-id="22326-287">This script will generate hello secrets yaml file for OMS Workspace ID and Primary Key toosecure your secrete information.</span></span>  
2. <span data-ttu-id="22326-288">Eseguire un progetto di hello toocreate i comandi seguenti per OMS e impostare l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="22326-288">Run hello following commands toocreate a project for OMS and set hello user account.</span></span> <span data-ttu-id="22326-289">segreto Hello generazione dello script richiede l'ID dell'area di lavoro OMS <WSID> e la chiave primaria <KEY> e dopo il completamento, crea file ocp-secret.yaml hello.</span><span class="sxs-lookup"><span data-stu-id="22326-289">hello secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates hello ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="22326-290">Distribuire file segreto hello eseguendo hello:</span><span class="sxs-lookup"><span data-stu-id="22326-290">Deploy hello secret file by running hello following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="22326-291">Verificare la distribuzione eseguendo hello:</span><span class="sxs-lookup"><span data-stu-id="22326-291">Verify deployment by running hello following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="22326-292">e l'output di hello dovrebbe essere simile:</span><span class="sxs-lookup"><span data-stu-id="22326-292">and hello  output should resemble:</span></span>  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. <span data-ttu-id="22326-293">Distribuire file daemon set yaml di hello agente OMS eseguendo hello:</span><span class="sxs-lookup"><span data-stu-id="22326-293">Deploy hello OMS Agent daemon-set yaml file by running hello following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="22326-294">Verificare la distribuzione eseguendo hello:</span><span class="sxs-lookup"><span data-stu-id="22326-294">Verify deployment by running hello following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="22326-295">e l'output di hello dovrebbe essere simile:</span><span class="sxs-lookup"><span data-stu-id="22326-295">and hello output should resemble:</span></span>

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="22326-296">Proteggere le informazioni segrete per Docker Swarm e Kubernetes</span><span class="sxs-lookup"><span data-stu-id="22326-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="22326-297">È possibile proteggere l'ID segreto dell'area di lavoro OMS e le chiavi primarie segrete per i servizi contenitore Docker Swarm e Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="22326-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="22326-298">Proteggere i segreti per Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="22326-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="22326-299">Per Docker Swarm, una volta creato il segreto di hello per ID area di lavoro e la chiave primaria, è possibile eseguire hello creare il servizio Docker hello per OMSagent.</span><span class="sxs-lookup"><span data-stu-id="22326-299">For Docker Swarm, once hello secret for Workspace ID and Primary Key is created, you can run hello create hello Docker service for OMSagent.</span></span> <span data-ttu-id="22326-300">Utilizzare hello toocreate informazioni seguendo le informazioni segrete.</span><span class="sxs-lookup"><span data-stu-id="22326-300">Use hello following information toocreate your secret information.</span></span>

1. <span data-ttu-id="22326-301">Eseguire l'istruzione seguente hello su nodo principale hello.</span><span class="sxs-lookup"><span data-stu-id="22326-301">Run hello following on hello master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="22326-302">Verificare che i segreti siano stati creati correttamente.</span><span class="sxs-lookup"><span data-stu-id="22326-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="22326-303">Esecuzione hello successivo comando toomount hello segreti toohello contenitore agente OMS.</span><span class="sxs-lookup"><span data-stu-id="22326-303">Run hello following command toomount hello secrets toohello containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="22326-304">Proteggere i segreti per Kubernetes con file yaml</span><span class="sxs-lookup"><span data-stu-id="22326-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="22326-305">Per Kubernetes, utilizzare un file di script toogenerate hello segreti yaml per l'ID area di lavoro e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="22326-305">For Kubernetes, you use a script toogenerate hello secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="22326-306">In hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) pagina, sono disponibili i file che è possibile utilizzare con o senza le informazioni segrete.</span><span class="sxs-lookup"><span data-stu-id="22326-306">At hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="22326-307">Hello predefinito OMS Agent DaemonSet non dispone di informazioni segrete (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="22326-307">hello Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="22326-308">file yaml di Hello DaemonSet agente OMS Usa informazioni segrete (omsagent-ds-secrets.yaml) con file di generazione secret script toogenerate hello segreti yaml (omsagentsecret.yaml).</span><span class="sxs-lookup"><span data-stu-id="22326-308">hello OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts toogenerate hello secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="22326-309">È possibile scegliere toocreate omsagent DaemonSets con o senza i segreti.</span><span class="sxs-lookup"><span data-stu-id="22326-309">You can choose toocreate omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="22326-310">File DaemonSet con estensione yaml predefinito dell'agente OMS senza segreti</span><span class="sxs-lookup"><span data-stu-id="22326-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="22326-311">Per file yaml DaemonSet agente OMS di hello predefinito, sostituire hello `<WSID>` e `<KEY>` tooyour WSID e la chiave.</span><span class="sxs-lookup"><span data-stu-id="22326-311">For hello default OMS Agent DaemonSet yaml file, replace hello `<WSID>` and `<KEY>` tooyour WSID and KEY.</span></span> <span data-ttu-id="22326-312">Copiare nodo principale di hello file tooyour e seguenti hello esecuzione:</span><span class="sxs-lookup"><span data-stu-id="22326-312">Copy hello file tooyour master node and run hello following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="22326-313">File DaemonSet con estensione yaml predefinito dell'agente OMS con segreti</span><span class="sxs-lookup"><span data-stu-id="22326-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="22326-314">toouse DaemonSet agente OMS utilizzando le informazioni segrete, creare i segreti hello prima.</span><span class="sxs-lookup"><span data-stu-id="22326-314">toouse OMS Agent DaemonSet using secret information, create hello secrets first.</span></span>
    1. <span data-ttu-id="22326-315">Copiare script hello e file di modello segreta e verificare che siano presenti hello stessa directory.</span><span class="sxs-lookup"><span data-stu-id="22326-315">Copy hello script and secret template file and make sure they are on hello same directory.</span></span>
        - <span data-ttu-id="22326-316">Script per la generazione di segreti: secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="22326-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="22326-317">Modello di segreto: secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="22326-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="22326-318">Eseguire script hello, ad esempio hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="22326-318">Run hello script, like hello following example.</span></span> <span data-ttu-id="22326-319">script Hello chiede hello ID area di lavoro OMS e la chiave primaria e dopo l'immissione, script hello crea un file di secret yaml in modo da eseguire.</span><span class="sxs-lookup"><span data-stu-id="22326-319">hello script asks for hello OMS Workspace ID and Primary Key and after you enter them, hello script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="22326-320">Creare pod segreti hello eseguendo hello:</span><span class="sxs-lookup"><span data-stu-id="22326-320">Create hello secrets pod by running hello following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="22326-321">tooverify, eseguire hello seguente:</span><span class="sxs-lookup"><span data-stu-id="22326-321">tooverify, run hello following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="22326-322">L'output deve essere simile a:</span><span class="sxs-lookup"><span data-stu-id="22326-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="22326-323">L'output deve essere simile a:</span><span class="sxs-lookup"><span data-stu-id="22326-323">Output should resemble:</span></span>

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. <span data-ttu-id="22326-324">Creare il DaemonSet dell'agente OMS eseguendo l'istruzione ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="22326-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="22326-325">Verificare che hello che daemonset agente OMS è in esecuzione, simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="22326-325">Verify that hello OMS Agent DaemonSet is running, similar toohello following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="22326-326">Per Kubernetes, utilizzare un file di script toogenerate hello segreti yaml per ID area di lavoro e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="22326-326">For Kubernetes, use a script toogenerate hello secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="22326-327">Hello di utilizzare le seguenti informazioni di esempio con hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure le informazioni segrete.</span><span class="sxs-lookup"><span data-stu-id="22326-327">Use hello following example information with hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure your secret information.</span></span>

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a><span data-ttu-id="22326-328">Host del contenitore Windows</span><span class="sxs-lookup"><span data-stu-id="22326-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="22326-329">Preparazione prima dell'installazione degli agenti di Windows</span><span class="sxs-lookup"><span data-stu-id="22326-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="22326-330">Prima di installare gli agenti nei computer che eseguono Windows, è necessario servizio Docker di tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="22326-330">Before you install agents on computers running Windows, you need tooconfigure hello Docker service.</span></span> <span data-ttu-id="22326-331">configurazione di Hello consente hello Windows hello o agente di Log Analitica macchina virtuale estensione toouse hello del socket TCP Docker in modo che gli agenti di hello possono accedere in remoto i daemon Docker hello e toocapture dati per il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="22326-331">hello configuration allows hello Windows agent or hello Log Analytics virtual machine extension toouse hello Docker TCP socket so that hello agents can access hello Docker daemon remotely and toocapture data for monitoring.</span></span>

#### <a name="toostart-docker-and-verify-its-configuration"></a><span data-ttu-id="22326-332">toostart Docker e verificare la configurazione</span><span class="sxs-lookup"><span data-stu-id="22326-332">toostart Docker and verify its configuration</span></span>

<span data-ttu-id="22326-333">Esistono passaggi necessari tooset backup TCP, named pipe per Windows Server:</span><span class="sxs-lookup"><span data-stu-id="22326-333">There are steps needed tooset up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="22326-334">In Windows PowerShell, abilitare pipe TCP e named pipe.</span><span class="sxs-lookup"><span data-stu-id="22326-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="22326-335">Configurare Docker con il file di configurazione hello per pipe TCP e named pipe.</span><span class="sxs-lookup"><span data-stu-id="22326-335">Configure Docker with hello configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="22326-336">file di configurazione Hello è disponibile in c:\programdata\docker\config\daemon.JSON..</span><span class="sxs-lookup"><span data-stu-id="22326-336">hello configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="22326-337">Nel file daemon hello, sarà necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="22326-337">In hello daemon.json file, you will need hello following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="22326-338">Per ulteriori informazioni sulla configurazione del daemon Docker hello usato con i contenitori di Windows, vedere [motore Docker in Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="22326-338">For more information about hello Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="22326-339">Installare gli agenti Windows</span><span class="sxs-lookup"><span data-stu-id="22326-339">Install Windows agents</span></span>

<span data-ttu-id="22326-340">tooenable Windows e contenitore di Hyper-V di monitoraggio, installare Microsoft Monitoring Agent (MMA) hello nei computer Windows che sono host contenitore.</span><span class="sxs-lookup"><span data-stu-id="22326-340">tooenable Windows and Hyper-V container monitoring, install hello Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="22326-341">Per i computer che eseguono Windows nell'ambiente locale, vedere [tooLog computer Windows di connettersi Analitica](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="22326-341">For computers running Windows in your on-premises environment, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="22326-342">Per le macchine virtuali in esecuzione in Azure, connetterle tooLog Analitica utilizzando hello [estensione della macchina virtuale](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="22326-342">For virtual machines running in Azure, connect them tooLog Analytics using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="22326-343">È possibile monitorare i contenitori Windows in esecuzione in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="22326-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="22326-344">Solo le [macchine virtuali in esecuzione in Azure](log-analytics-azure-vm-extension.md) e i [computer che eseguono Windows nell'ambiente locale](log-analytics-windows-agents.md), tuttavia, sono attualmente supportati da Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="22326-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="22326-345">È possibile verificare che tale soluzione di monitoraggio contenitore hello sia impostato correttamente per Windows.</span><span class="sxs-lookup"><span data-stu-id="22326-345">You can verify that hello Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="22326-346">toocheck se hello management pack download non è correttamente, cercare *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="22326-346">toocheck whether hello management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="22326-347">file di Hello devono trovarsi nella cartella c:\Programmi\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs hello.</span><span class="sxs-lookup"><span data-stu-id="22326-347">hello files should be in hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="22326-348">Componenti della soluzione</span><span class="sxs-lookup"><span data-stu-id="22326-348">Solution components</span></span>

<span data-ttu-id="22326-349">Se si usano agenti di Windows, quindi hello seguenti management pack è installato in ogni computer con un agente quando si aggiunge questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="22326-349">If you are using Windows agents, then hello following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="22326-350">Non è necessaria per il management pack di hello alcuna configurazione o manutenzione.</span><span class="sxs-lookup"><span data-stu-id="22326-350">No configuration or maintenance is required for hello management pack.</span></span>

- <span data-ttu-id="22326-351">*ContainerManagement.xxx* installato in C:\Programmi\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span><span class="sxs-lookup"><span data-stu-id="22326-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="22326-352">Informazioni dettagliate sulla raccolta di dati dei contenitori</span><span class="sxs-lookup"><span data-stu-id="22326-352">Container data collection details</span></span>
<span data-ttu-id="22326-353">soluzione di monitoraggio contenitore Hello raccoglie diversi dati di log e le metriche delle prestazioni dall'host contenitore e i contenitori usano agenti che si attivano.</span><span class="sxs-lookup"><span data-stu-id="22326-353">hello Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="22326-354">Dati raccolti ogni tre minuti per hello seguenti tipi di agente.</span><span class="sxs-lookup"><span data-stu-id="22326-354">Data is collected every three minutes by hello following agent types.</span></span>

- [<span data-ttu-id="22326-355">Agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="22326-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="22326-356">Agente Windows</span><span class="sxs-lookup"><span data-stu-id="22326-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="22326-357">Estensione macchina virtuale di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="22326-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="22326-358">Record dei contenitori</span><span class="sxs-lookup"><span data-stu-id="22326-358">Container records</span></span>

<span data-ttu-id="22326-359">Hello nella tabella seguente vengono illustrati esempi di record raccolti dalla soluzione di monitoraggio di contenitore hello e hello i tipi di dati che vengono visualizzati nei risultati della ricerca log.</span><span class="sxs-lookup"><span data-stu-id="22326-359">hello following table shows examples of records collected by hello Container Monitoring solution and hello data types that appear in log search results.</span></span>

| <span data-ttu-id="22326-360">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="22326-360">Data type</span></span> | <span data-ttu-id="22326-361">Tipo di dati in Ricerca log</span><span class="sxs-lookup"><span data-stu-id="22326-361">Data type in Log Search</span></span> | <span data-ttu-id="22326-362">Fields</span><span class="sxs-lookup"><span data-stu-id="22326-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22326-363">Prestazioni per host e contenitori</span><span class="sxs-lookup"><span data-stu-id="22326-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="22326-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="22326-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="22326-365">Inventario contenitori</span><span class="sxs-lookup"><span data-stu-id="22326-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="22326-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="22326-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="22326-367">Inventario delle immagini dei contenitori</span><span class="sxs-lookup"><span data-stu-id="22326-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="22326-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="22326-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="22326-369">Log contenitori</span><span class="sxs-lookup"><span data-stu-id="22326-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="22326-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="22326-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="22326-371">Log servizio contenitori</span><span class="sxs-lookup"><span data-stu-id="22326-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="22326-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="22326-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="22326-373">Inventario di nodi contenitore</span><span class="sxs-lookup"><span data-stu-id="22326-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="22326-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="22326-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="22326-375">Inventario di Kubernetes</span><span class="sxs-lookup"><span data-stu-id="22326-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="22326-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="22326-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="22326-377">Processo contenitore</span><span class="sxs-lookup"><span data-stu-id="22326-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="22326-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="22326-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="22326-379">Eventi di Kubernetes</span><span class="sxs-lookup"><span data-stu-id="22326-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="22326-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span><span class="sxs-lookup"><span data-stu-id="22326-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="22326-381">Aggiunta di etichette troppo*PodLabel* etichette personalizzate sono di tipi di dati.</span><span class="sxs-lookup"><span data-stu-id="22326-381">Labels appended too*PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="22326-382">Hello aggiunte etichette PodLabel illustrate nella tabella hello sono esempi.</span><span class="sxs-lookup"><span data-stu-id="22326-382">hello appended PodLabel labels shown in hello table are examples.</span></span> <span data-ttu-id="22326-383">`PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` saranno quindi diverse nel set di dati dell'ambiente e in genere saranno simili a `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="22326-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="22326-384">Monitorare i contenitori</span><span class="sxs-lookup"><span data-stu-id="22326-384">Monitor containers</span></span>
<span data-ttu-id="22326-385">Dopo aver creato una soluzione di hello abilitata nel portale OMS hello, hello **contenitori** riquadro mostra le informazioni di riepilogo sull'host contenitore e i contenitori di hello in esecuzione negli host.</span><span class="sxs-lookup"><span data-stu-id="22326-385">After you have hello solution enabled in hello OMS portal, hello **Containers** tile shows summary information about your container hosts and hello containers running in hosts.</span></span>

![Riquadro Containers (Contenitori)](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="22326-387">riquadro Hello Mostra una panoramica dei contenitori di quanti sono in ambiente hello e se è impossibile, in esecuzione o arrestato.</span><span class="sxs-lookup"><span data-stu-id="22326-387">hello tile shows an overview of how many containers you have in hello environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-hello-containers-dashboard"></a><span data-ttu-id="22326-388">Tramite il dashboard di contenitori hello</span><span class="sxs-lookup"><span data-stu-id="22326-388">Using hello Containers dashboard</span></span>
<span data-ttu-id="22326-389">Fare clic su hello **contenitori** riquadro.</span><span class="sxs-lookup"><span data-stu-id="22326-389">Click hello **Containers** tile.</span></span> <span data-ttu-id="22326-390">Le visualizzazioni sono organizzate in base agli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="22326-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="22326-391">**Eventi del contenitore**: visualizza lo stato dei contenitori e i computer con contenitori non riusciti.</span><span class="sxs-lookup"><span data-stu-id="22326-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="22326-392">**Contenitore registri** -Visualizza un grafico dei file di log contenitore generati nel tempo e un elenco di computer con numero più alto di hello dei file di log.</span><span class="sxs-lookup"><span data-stu-id="22326-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with hello highest number of log files.</span></span>
- <span data-ttu-id="22326-393">**Eventi Kubernetes** -Mostra un grafico di eventi Kubernetes generati nel tempo e un elenco di motivi hello perché POD generati eventi hello.</span><span class="sxs-lookup"><span data-stu-id="22326-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of hello reasons why pods generated hello events.</span></span> <span data-ttu-id="22326-394">*Questo set di dati viene usato solo negli ambienti Linux.*</span><span class="sxs-lookup"><span data-stu-id="22326-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="22326-395">**Inventario Namespace Kubernetes** - Mostra il numero di hello di unità e spazi dei nomi e viene illustrata la gerarchia.</span><span class="sxs-lookup"><span data-stu-id="22326-395">**Kubernetes Namespace Inventory** - Shows hello number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="22326-396">*Questo set di dati viene usato solo negli ambienti Linux.*</span><span class="sxs-lookup"><span data-stu-id="22326-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="22326-397">**Inventario nodo contenitore** -Mostra il numero di hello dei tipi di orchestrazione utilizzati in nodi/host contenitore.</span><span class="sxs-lookup"><span data-stu-id="22326-397">**Container Node Inventory** - Shows hello number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="22326-398">Hello computer nodi/host sono elencati anche dal numero di hello di contenitori.</span><span class="sxs-lookup"><span data-stu-id="22326-398">hello computer nodes/hosts are also listed by hello number of containers.</span></span> <span data-ttu-id="22326-399">*Questo set di dati viene usato solo negli ambienti Linux.*</span><span class="sxs-lookup"><span data-stu-id="22326-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="22326-400">**Inventario delle immagini contenitore** -Mostra numero totale di hello di immagini contenitore utilizzato e numero di tipi di immagine.</span><span class="sxs-lookup"><span data-stu-id="22326-400">**Container Images Inventory** - Shows hello total number of container images used and number of image types.</span></span> <span data-ttu-id="22326-401">numero di Hello delle immagini è inoltre elencato dal tag di immagine hello.</span><span class="sxs-lookup"><span data-stu-id="22326-401">hello number of images are also listed by hello image tag.</span></span>
- <span data-ttu-id="22326-402">**Lo stato di contenitori** -Mostra il numero totale di hello del contenitore di computer o l'host di nodi che dispongono di contenitori in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="22326-402">**Containers Status** - Shows hello total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="22326-403">I computer sono elencati anche dal numero di hello dell'esecuzione di host.</span><span class="sxs-lookup"><span data-stu-id="22326-403">Computers are also listed by hello number of running hosts.</span></span>
- <span data-ttu-id="22326-404">**Processi del contenitore**: visualizza un grafico a linee dei processi del contenitore in esecuzione nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="22326-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="22326-405">I contenitori vengono anche indicati dal comando/processo in esecuzione nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="22326-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="22326-406">*Questo set di dati viene usato solo negli ambienti Linux.*</span><span class="sxs-lookup"><span data-stu-id="22326-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="22326-407">**Prestazioni CPU contenitore** -Mostra un grafico a linee dell'utilizzo medio della CPU hello nel corso del tempo per i nodi di computer o gli host.</span><span class="sxs-lookup"><span data-stu-id="22326-407">**Container CPU Performance** - Shows a line chart of hello average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="22326-408">Anche gli elenchi di hello computer nodi/ospita in base medio della CPU.</span><span class="sxs-lookup"><span data-stu-id="22326-408">Also lists hello computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="22326-409">**Prestazioni memoria contenitore**: visualizza un grafico a linee dell'utilizzo della memoria nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="22326-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="22326-410">Elenca anche l'utilizzo della memoria del computer in base al nome dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="22326-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="22326-411">**Prestazioni del computer** -Mostra i grafici a linee pari al % hello di prestazioni della CPU nel tempo, percentuale di utilizzo della memoria nel tempo e megabyte di spazio libero su disco nel tempo.</span><span class="sxs-lookup"><span data-stu-id="22326-411">**Computer Performance** - Shows line charts of hello percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="22326-412">È possibile passare il mouse su qualsiasi riga in un grafico di tooview ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="22326-412">You can hover over any line in a chart tooview more details.</span></span>


<span data-ttu-id="22326-413">Ogni area del dashboard hello è una rappresentazione visiva di una ricerca eseguita sui dati raccolti.</span><span class="sxs-lookup"><span data-stu-id="22326-413">Each area of hello dashboard is a visual representation of a search that is run on collected data.</span></span>

![Dashboard Containers (Contenitori)](./media/log-analytics-containers/containers-dash01.png)

![Dashboard Containers (Contenitori)](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="22326-416">In hello **stato contenitore** area, fare clic su area superiore hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="22326-416">In hello **Container Status** area, click hello top area, as shown below.</span></span>

![Stato dei contenitori](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="22326-418">Verrà visualizzata la finestra di ricerca nei log, visualizzazione di informazioni sullo stato di hello i contenitori.</span><span class="sxs-lookup"><span data-stu-id="22326-418">Log Search opens, displaying information about hello state of your containers.</span></span>

![Ricerca log per i contenitori](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="22326-420">Da qui è possibile modificare toomodify query di ricerca hello è informazioni specifiche hello toofind si è interessati.</span><span class="sxs-lookup"><span data-stu-id="22326-420">From here, you can edit hello search query toomodify it toofind hello specific information you're interested in.</span></span> <span data-ttu-id="22326-421">Per altre informazioni sulle ricerche log, vedere [Ricerche nei log in Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="22326-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="22326-422">Risolvere i problemi cercando un contenitore con errori</span><span class="sxs-lookup"><span data-stu-id="22326-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="22326-423">Log Analytics contrassegna un contenitore come **Non riuscito** se il contenitore è stato terminato con un codice di uscita diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="22326-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="22326-424">È possibile visualizzare una panoramica di hello errori e problemi nell'ambiente di hello in hello **Impossibile contenitori** area.</span><span class="sxs-lookup"><span data-stu-id="22326-424">You can see an overview of hello errors and failures in hello environment in hello **Failed Containers** area.</span></span>

### <a name="toofind-failed-containers"></a><span data-ttu-id="22326-425">contenitori toofind non riuscita</span><span class="sxs-lookup"><span data-stu-id="22326-425">toofind failed containers</span></span>
1. <span data-ttu-id="22326-426">Fare clic su hello **stato contenitore** area.</span><span class="sxs-lookup"><span data-stu-id="22326-426">Click hello **Container Status** area.</span></span>  
   <span data-ttu-id="22326-427">![Stato dei contenitori](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="22326-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="22326-428">Ricerca nei log aprirà e visualizzerà stato hello i contenitori, simile toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="22326-428">Log Search opens and displays hello state of your containers, similar toohello following.</span></span>  
   ![stato dei contenitori](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="22326-430">Successivamente, fare clic su valore hello aggregato di informazioni aggiuntive di tooview contenitori non riuscita.</span><span class="sxs-lookup"><span data-stu-id="22326-430">Next, click hello aggregated value of failed containers tooview additional information.</span></span> <span data-ttu-id="22326-431">Espandere **Mostra altre** tooview hello immagine ID</span><span class="sxs-lookup"><span data-stu-id="22326-431">Expand **show more** tooview hello image ID.</span></span>  
   <span data-ttu-id="22326-432">![contenitori non riusciti](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="22326-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="22326-433">Digitare quindi seguito hello nella query di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="22326-433">Next, type hello following in hello search query.</span></span> <span data-ttu-id="22326-434">`Type=ContainerInventory <ImageID>`toosee informazioni dettagliate sull'immagine di hello quali dimensioni dell'immagine e il numero di immagini arrestate e non riuscite.</span><span class="sxs-lookup"><span data-stu-id="22326-434">`Type=ContainerInventory <ImageID>` toosee details about hello image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="22326-435">![contenitori non riusciti](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="22326-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="22326-436">Ricerca dei dati dei contenitori nei log</span><span class="sxs-lookup"><span data-stu-id="22326-436">Search logs for container data</span></span>
<span data-ttu-id="22326-437">Quando si sta cercando di risolvere un errore specifico, può essere utile toosee in cui viene eseguito nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="22326-437">When you're troubleshooting a specific error, it can help toosee where it is occurring in your environment.</span></span> <span data-ttu-id="22326-438">Hello seguenti tipi di log consente di creare query informazioni hello tooreturn desiderate.</span><span class="sxs-lookup"><span data-stu-id="22326-438">hello following log types will help you create queries tooreturn hello information you want.</span></span>


- <span data-ttu-id="22326-439">**ContainerImageInventory** : usare questo tipo quando si cerca di informazioni sul toofind organizzate per immagine e tooview informazioni sulle immagini, ad esempio gli ID immagine o dimensioni.</span><span class="sxs-lookup"><span data-stu-id="22326-439">**ContainerImageInventory** – Use this type when you're trying toofind information organized by image and tooview image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="22326-440">**ContainerInventory**: usare questo tipo per ottenere informazioni sul percorso dei contenitori, i relativi nomi e le immagini che eseguono.</span><span class="sxs-lookup"><span data-stu-id="22326-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="22326-441">**ContainerLog** : usare questo tipo quando si desidera toofind informazioni nel registro errori specifici e le voci.</span><span class="sxs-lookup"><span data-stu-id="22326-441">**ContainerLog** – Use this type when you want toofind specific error log information and entries.</span></span>
- <span data-ttu-id="22326-442">**ContainerNodeInventory_CL** usare questo tipo di informazioni di hello/nodo host in cui sono presenti contenitori.</span><span class="sxs-lookup"><span data-stu-id="22326-442">**ContainerNodeInventory_CL**  Use this type when you want hello information about host/node where containers are residing.</span></span> <span data-ttu-id="22326-443">Fornisce informazioni su versione di Docker, tipo di orchestrazione, risorsa di archiviazione e rete.</span><span class="sxs-lookup"><span data-stu-id="22326-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="22326-444">**ContainerProcess_CL** tooquickly questo tipo di utilizzo visualizzare hello del processo in esecuzione all'interno del contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="22326-444">**ContainerProcess_CL** Use this type tooquickly see hello process running within hello container.</span></span>
- <span data-ttu-id="22326-445">**ContainerServiceLog** : usare questo tipo quando si cerca informazioni toofind audit trail per hello daemon Docker, ad esempio avvio, arresto, eliminare o comandi pull.</span><span class="sxs-lookup"><span data-stu-id="22326-445">**ContainerServiceLog** – Use this type when you're trying toofind audit trail information for hello Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="22326-446">**KubeEvents_CL** utilizzare gli eventi di Kubernetes questo tipo toosee hello.</span><span class="sxs-lookup"><span data-stu-id="22326-446">**KubeEvents_CL**  Use this type toosee hello Kubernetes events.</span></span>
- <span data-ttu-id="22326-447">**KubePodInventory_CL** utilizzare questo tipo quando si desiderano che le informazioni di gerarchia toounderstand hello cluster.</span><span class="sxs-lookup"><span data-stu-id="22326-447">**KubePodInventory_CL**  Use this type when you want toounderstand hello cluster hierarchy information.</span></span>


### <a name="toosearch-logs-for-container-data"></a><span data-ttu-id="22326-448">toosearch registri per i dati del contenitore</span><span class="sxs-lookup"><span data-stu-id="22326-448">toosearch logs for container data</span></span>
* <span data-ttu-id="22326-449">Scegliere un'immagine che si è certi recentemente si sono verificati e cercare i log degli errori di hello.</span><span class="sxs-lookup"><span data-stu-id="22326-449">Choose an image that you know has failed recently and find hello error logs for it.</span></span> <span data-ttu-id="22326-450">Iniziare cercando il nome di un contenitore che esegue l'immagine con una ricerca **ContainerInventory**.</span><span class="sxs-lookup"><span data-stu-id="22326-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="22326-451">Cercare ad esempio `Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="22326-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="22326-452">![Cercare contenitori Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="22326-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="22326-453">Hello nome del contenitore hello accanto troppo**nome**e cercare tali log.</span><span class="sxs-lookup"><span data-stu-id="22326-453">hello name of hello container next too**Name**, and search for those logs.</span></span> <span data-ttu-id="22326-454">In questo esempio si tratta di `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="22326-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="22326-455">**Visualizzare le informazioni sulle prestazioni**</span><span class="sxs-lookup"><span data-stu-id="22326-455">**View performance information**</span></span>

<span data-ttu-id="22326-456">Quando si sta iniziando tooconstruct query, può essere utile toosee ciò che è possibile innanzitutto.</span><span class="sxs-lookup"><span data-stu-id="22326-456">When you're beginning tooconstruct queries, it can help toosee what's possible first.</span></span> <span data-ttu-id="22326-457">Ad esempio, eseguire una query toosee ricerca di tutti i dati sulle prestazioni, provare una query ampia digitando hello seguente.</span><span class="sxs-lookup"><span data-stu-id="22326-457">For example, toosee all performance data, try a broad query by typing hello following search query.</span></span>

```
Type=Perf
```

![prestazioni dei contenitori](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="22326-459">È possibile definire l'ambito di dati sulle prestazioni hello risposta tooa specifico contenitore digitando il nome di hello di esso toohello a destra della query.</span><span class="sxs-lookup"><span data-stu-id="22326-459">You can scope hello performance data you're seeing tooa specific container by typing hello name of it toohello right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="22326-460">Che mostra l'elenco di hello delle metriche delle prestazioni raccolti per un singolo contenitore.</span><span class="sxs-lookup"><span data-stu-id="22326-460">That shows hello list of performance metrics that are collected for an individual container.</span></span>

![prestazioni dei contenitori](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="22326-462">Esempio di query di ricerca log</span><span class="sxs-lookup"><span data-stu-id="22326-462">Example log search queries</span></span>
<span data-ttu-id="22326-463">È spesso utile toobuild esegue una query a partire da un esempio o due e quindi modificandoli toofit l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="22326-463">It's often useful toobuild queries starting with an example or two and then modifying them toofit your environment.</span></span> <span data-ttu-id="22326-464">Come punto di partenza, è possibile sperimentare hello **query di esempio** toohelp area si compila una query più avanzate.</span><span class="sxs-lookup"><span data-stu-id="22326-464">As a starting point, you can experiment with hello **Sample Queries** area toohelp you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Query sui contenitori](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="22326-466">Salvataggio delle query di ricerca log</span><span class="sxs-lookup"><span data-stu-id="22326-466">Saving log search queries</span></span>
<span data-ttu-id="22326-467">Il salvataggio di query è una funzionalità standard di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="22326-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="22326-468">Le query salvate potranno essere riusate rapidamente in futuro.</span><span class="sxs-lookup"><span data-stu-id="22326-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="22326-469">Dopo aver creato una query che utile, salvarlo facendo **Preferiti** nella parte superiore di hello della pagina di ricerca nei Log hello.</span><span class="sxs-lookup"><span data-stu-id="22326-469">After you create a query that you find useful, save it by clicking **Favorites** at hello top of hello Log Search page.</span></span> <span data-ttu-id="22326-470">Quindi è possibile accedervi facilmente in un secondo momento da hello **My Dashboard** pagina.</span><span class="sxs-lookup"><span data-stu-id="22326-470">Then you can easily access it later from hello **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22326-471">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22326-471">Next steps</span></span>
* <span data-ttu-id="22326-472">[Ricerca dei registri](log-analytics-log-searches.md) tooview dettagliate record dei dati contenitore.</span><span class="sxs-lookup"><span data-stu-id="22326-472">[Search logs](log-analytics-log-searches.md) tooview detailed container data records.</span></span>
