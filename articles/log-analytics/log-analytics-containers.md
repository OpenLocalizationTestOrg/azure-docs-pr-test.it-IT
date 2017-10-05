---
title: Soluzione Monitoraggio contenitori in Log Analytics di Azure | Microsoft Docs
description: La soluzione Monitoraggio contenitori in Log Analytics consente di visualizzare e gestire gli host del contenitore Docker e Windows in un'unica posizione.
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
ms.openlocfilehash: b2e03531ee401f4552198e5dd50fbfe1d970f0e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="b2711-103">Soluzione Monitoraggio contenitori in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b2711-103">Container Monitoring solution in Log Analytics</span></span>

![Simbolo di Contenitori](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="b2711-105">Questo articolo descrive come configurare e usare la soluzione Monitoraggio contenitori in Log Analytics per visualizzare e gestire gli host del contenitore Docker e Windows in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="b2711-105">This article describes how to set up and use the Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="b2711-106">Docker è un sistema di virtualizzazione software usato per creare contenitori che consentono di automatizzare la distribuzione del software nell'infrastruttura IT.</span><span class="sxs-lookup"><span data-stu-id="b2711-106">Docker is a software virtualization system used to create containers that automate software deployment to their IT infrastructure.</span></span>

<span data-ttu-id="b2711-107">La soluzione indica quali contenitori sono in esecuzione, quale immagine del contenitore eseguono e dove vengono eseguiti i contenitori.</span><span class="sxs-lookup"><span data-stu-id="b2711-107">The solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="b2711-108">È possibile visualizzare informazioni di controllo dettagliate che indicano i comandi usati con i contenitori.</span><span class="sxs-lookup"><span data-stu-id="b2711-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="b2711-109">È anche possibile risolvere i problemi dei contenitori visualizzando i log centralizzati ed eseguendo ricerche al loro interno senza dover visualizzare gli host Docker o Windows in remoto.</span><span class="sxs-lookup"><span data-stu-id="b2711-109">And, you can troubleshoot containers by viewing and searching centralized logs without having to remotely view Docker or Windows hosts.</span></span> <span data-ttu-id="b2711-110">È possibile trovare contenitori che consumano una quantità eccessiva di risorse in un host.</span><span class="sxs-lookup"><span data-stu-id="b2711-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="b2711-111">È anche possibile visualizzare informazioni centralizzate su utilizzo di CPU, memoria, archiviazione e rete e sulle prestazioni dei contenitori.</span><span class="sxs-lookup"><span data-stu-id="b2711-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="b2711-112">Nei computer che eseguono Windows, è possibile centralizzare e confrontare i log dai contenitori Windows Server, Hyper-V e Docker.</span><span class="sxs-lookup"><span data-stu-id="b2711-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="b2711-113">La soluzione supporta gli agenti di orchestrazione dei contenitori seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2711-113">The solution supports the following container orchestrators:</span></span>

- <span data-ttu-id="b2711-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="b2711-114">Docker Swarm</span></span>
- <span data-ttu-id="b2711-115">Controller di dominio/sistema operativo</span><span class="sxs-lookup"><span data-stu-id="b2711-115">DC/OS</span></span>
- <span data-ttu-id="b2711-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="b2711-116">Kubernetes</span></span>
- <span data-ttu-id="b2711-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b2711-117">Service Fabric</span></span>
- <span data-ttu-id="b2711-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="b2711-118">Red Hat OpenShift</span></span>


<span data-ttu-id="b2711-119">Il diagramma seguente mostra le relazioni tra vari host del contenitore e agenti con OMS.</span><span class="sxs-lookup"><span data-stu-id="b2711-119">The following diagram shows the relationships between various container hosts and agents with OMS.</span></span>

![Diagramma dei contenitori](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="b2711-121">Requisiti di sistema</span><span class="sxs-lookup"><span data-stu-id="b2711-121">System requirements</span></span>

<span data-ttu-id="b2711-122">Prima di iniziare, esaminare i dettagli seguenti per verificare che i prerequisiti siano soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="b2711-122">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="b2711-123">Supporto della soluzione di monitoraggio del contenitore per l'orchestrazione di Docker e la piattaforma del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="b2711-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="b2711-124">La tabella seguente descrive il supporto del monitoraggio dell'orchestrazione di Docker e del sistema operativo per inventario, prestazioni e log del contenitore con Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b2711-124">The following table outlines the Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="b2711-125">ACS</span><span class="sxs-lookup"><span data-stu-id="b2711-125">ACS</span></span> | <span data-ttu-id="b2711-126">Linux</span><span class="sxs-lookup"><span data-stu-id="b2711-126">Linux</span></span> | <span data-ttu-id="b2711-127">Windows</span><span class="sxs-lookup"><span data-stu-id="b2711-127">Windows</span></span> | <span data-ttu-id="b2711-128">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b2711-128">Container</span></span><br><span data-ttu-id="b2711-129">Inventario</span><span class="sxs-lookup"><span data-stu-id="b2711-129">Inventory</span></span> | <span data-ttu-id="b2711-130">Image</span><span class="sxs-lookup"><span data-stu-id="b2711-130">Image</span></span><br><span data-ttu-id="b2711-131">Inventario</span><span class="sxs-lookup"><span data-stu-id="b2711-131">Inventory</span></span> | <span data-ttu-id="b2711-132">Nodo</span><span class="sxs-lookup"><span data-stu-id="b2711-132">Node</span></span><br><span data-ttu-id="b2711-133">Inventario</span><span class="sxs-lookup"><span data-stu-id="b2711-133">Inventory</span></span> | <span data-ttu-id="b2711-134">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b2711-134">Container</span></span><br><span data-ttu-id="b2711-135">Prestazioni</span><span class="sxs-lookup"><span data-stu-id="b2711-135">Performance</span></span> | <span data-ttu-id="b2711-136">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b2711-136">Container</span></span><br><span data-ttu-id="b2711-137">Evento</span><span class="sxs-lookup"><span data-stu-id="b2711-137">Event</span></span> | <span data-ttu-id="b2711-138">Evento</span><span class="sxs-lookup"><span data-stu-id="b2711-138">Event</span></span><br><span data-ttu-id="b2711-139">Log</span><span class="sxs-lookup"><span data-stu-id="b2711-139">Log</span></span> | <span data-ttu-id="b2711-140">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b2711-140">Container</span></span><br><span data-ttu-id="b2711-141">Log</span><span class="sxs-lookup"><span data-stu-id="b2711-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="b2711-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="b2711-142">Kubernetes</span></span> | <span data-ttu-id="b2711-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-143">&#8226;</span></span> | <span data-ttu-id="b2711-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-144">&#8226;</span></span> | | <span data-ttu-id="b2711-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-145">&#8226;</span></span> | <span data-ttu-id="b2711-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-146">&#8226;</span></span> | <span data-ttu-id="b2711-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-147">&#8226;</span></span> | <span data-ttu-id="b2711-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-148">&#8226;</span></span> | <span data-ttu-id="b2711-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-149">&#8226;</span></span> | <span data-ttu-id="b2711-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-150">&#8226;</span></span> | <span data-ttu-id="b2711-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-151">&#8226;</span></span> |
| <span data-ttu-id="b2711-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="b2711-152">Mesosphere</span></span><br><span data-ttu-id="b2711-153">Controller di dominio/sistema operativo</span><span class="sxs-lookup"><span data-stu-id="b2711-153">DC/OS</span></span> | <span data-ttu-id="b2711-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-154">&#8226;</span></span> | <span data-ttu-id="b2711-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-155">&#8226;</span></span> | | <span data-ttu-id="b2711-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-156">&#8226;</span></span> | <span data-ttu-id="b2711-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-157">&#8226;</span></span> | <span data-ttu-id="b2711-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-158">&#8226;</span></span> | <span data-ttu-id="b2711-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-159">&#8226;</span></span>| <span data-ttu-id="b2711-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-160">&#8226;</span></span> | <span data-ttu-id="b2711-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-161">&#8226;</span></span> | <span data-ttu-id="b2711-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-162">&#8226;</span></span> |
| <span data-ttu-id="b2711-163">Docker</span><span class="sxs-lookup"><span data-stu-id="b2711-163">Docker</span></span><br><span data-ttu-id="b2711-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="b2711-164">Swarm</span></span> | <span data-ttu-id="b2711-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-165">&#8226;</span></span> | <span data-ttu-id="b2711-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-166">&#8226;</span></span> | <span data-ttu-id="b2711-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-167">&#8226;</span></span> | <span data-ttu-id="b2711-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-168">&#8226;</span></span> | <span data-ttu-id="b2711-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-169">&#8226;</span></span> | <span data-ttu-id="b2711-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-170">&#8226;</span></span> | <span data-ttu-id="b2711-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-171">&#8226;</span></span> | <span data-ttu-id="b2711-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-172">&#8226;</span></span> | | <span data-ttu-id="b2711-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-173">&#8226;</span></span> |
| <span data-ttu-id="b2711-174">Service</span><span class="sxs-lookup"><span data-stu-id="b2711-174">Service</span></span><br><span data-ttu-id="b2711-175">Infrastruttura</span><span class="sxs-lookup"><span data-stu-id="b2711-175">Fabric</span></span> | | | <span data-ttu-id="b2711-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-176">&#8226;</span></span> | <span data-ttu-id="b2711-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-177">&#8226;</span></span> | <span data-ttu-id="b2711-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-178">&#8226;</span></span> | <span data-ttu-id="b2711-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-179">&#8226;</span></span> | <span data-ttu-id="b2711-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-180">&#8226;</span></span> | <span data-ttu-id="b2711-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-181">&#8226;</span></span> | <span data-ttu-id="b2711-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-182">&#8226;</span></span> | <span data-ttu-id="b2711-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-183">&#8226;</span></span> |
| <span data-ttu-id="b2711-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="b2711-184">Red Hat Open</span></span><br><span data-ttu-id="b2711-185">MAIUSC</span><span class="sxs-lookup"><span data-stu-id="b2711-185">Shift</span></span> | | <span data-ttu-id="b2711-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-186">&#8226;</span></span> | | <span data-ttu-id="b2711-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-187">&#8226;</span></span> | <span data-ttu-id="b2711-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-188">&#8226;</span></span>| <span data-ttu-id="b2711-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-189">&#8226;</span></span> | <span data-ttu-id="b2711-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-190">&#8226;</span></span> | <span data-ttu-id="b2711-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-191">&#8226;</span></span> | | <span data-ttu-id="b2711-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-192">&#8226;</span></span> |
| <span data-ttu-id="b2711-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="b2711-193">Windows Server</span></span><br><span data-ttu-id="b2711-194">(autonomo)</span><span class="sxs-lookup"><span data-stu-id="b2711-194">(standalone)</span></span> | | | <span data-ttu-id="b2711-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-195">&#8226;</span></span> | <span data-ttu-id="b2711-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-196">&#8226;</span></span> | <span data-ttu-id="b2711-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-197">&#8226;</span></span> | <span data-ttu-id="b2711-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-198">&#8226;</span></span> | <span data-ttu-id="b2711-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-199">&#8226;</span></span> | <span data-ttu-id="b2711-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-200">&#8226;</span></span> | | <span data-ttu-id="b2711-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-201">&#8226;</span></span> |
| <span data-ttu-id="b2711-202">Server Linux</span><span class="sxs-lookup"><span data-stu-id="b2711-202">Linux Server</span></span><br><span data-ttu-id="b2711-203">(autonomo)</span><span class="sxs-lookup"><span data-stu-id="b2711-203">(standalone)</span></span> | | <span data-ttu-id="b2711-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-204">&#8226;</span></span> | | <span data-ttu-id="b2711-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-205">&#8226;</span></span> | <span data-ttu-id="b2711-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-206">&#8226;</span></span> | <span data-ttu-id="b2711-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-207">&#8226;</span></span> | <span data-ttu-id="b2711-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-208">&#8226;</span></span> | <span data-ttu-id="b2711-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-209">&#8226;</span></span> | | <span data-ttu-id="b2711-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2711-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="b2711-211">Versioni di Docker supportate in Linux</span><span class="sxs-lookup"><span data-stu-id="b2711-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="b2711-212">Docker da 1.11 a 1.13</span><span class="sxs-lookup"><span data-stu-id="b2711-212">Docker 1.11 to 1.13</span></span>
- <span data-ttu-id="b2711-213">Docker CE e EE v17.06</span><span class="sxs-lookup"><span data-stu-id="b2711-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="b2711-214">Distribuzioni Linux x64 supportate come host del contenitore</span><span class="sxs-lookup"><span data-stu-id="b2711-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="b2711-215">Ubuntu 14.04 LTS e 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="b2711-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="b2711-216">CoreOS (stable)</span><span class="sxs-lookup"><span data-stu-id="b2711-216">CoreOS(stable)</span></span>
- <span data-ttu-id="b2711-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="b2711-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="b2711-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="b2711-218">openSUSE 13.2</span></span>
- <span data-ttu-id="b2711-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="b2711-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="b2711-220">CentOS 7.2 e 7.3</span><span class="sxs-lookup"><span data-stu-id="b2711-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="b2711-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="b2711-221">SLES 12</span></span>
- <span data-ttu-id="b2711-222">RHEL 7.2 e 7.3</span><span class="sxs-lookup"><span data-stu-id="b2711-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="b2711-223">Red Hat OpenShift Container Platform (OCP) 3.4 e 3.5</span><span class="sxs-lookup"><span data-stu-id="b2711-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="b2711-224">ACS Mesosphere DC/OS da 1.7.3 a 1.8.8</span><span class="sxs-lookup"><span data-stu-id="b2711-224">ACS Mesosphere DC/OS 1.7.3 to 1.8.8</span></span>
- <span data-ttu-id="b2711-225">ACS Kubernetes da 1.4.5 a 1.6</span><span class="sxs-lookup"><span data-stu-id="b2711-225">ACS Kubernetes 1.4.5 to 1.6</span></span>
- <span data-ttu-id="b2711-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="b2711-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="b2711-227">Sistema operativo Windows supportato</span><span class="sxs-lookup"><span data-stu-id="b2711-227">Supported Windows operating system</span></span>

- <span data-ttu-id="b2711-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b2711-228">Windows Server 2016</span></span>
- <span data-ttu-id="b2711-229">Versione di Windows per il 10° anniversario (professionale o aziendale)</span><span class="sxs-lookup"><span data-stu-id="b2711-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="b2711-230">Versioni di Docker supportate in Windows</span><span class="sxs-lookup"><span data-stu-id="b2711-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="b2711-231">Docker 1.12 e 1.13</span><span class="sxs-lookup"><span data-stu-id="b2711-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="b2711-232">Docker 17.03.0 e successive</span><span class="sxs-lookup"><span data-stu-id="b2711-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="b2711-233">Installazione e configurazione della soluzione</span><span class="sxs-lookup"><span data-stu-id="b2711-233">Installing and configuring the solution</span></span>
<span data-ttu-id="b2711-234">Usare le informazioni seguenti per installare e configurare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="b2711-234">Use the following information to install and configure the solution.</span></span>

1. <span data-ttu-id="b2711-235">Aggiungere la soluzione Monitoraggio contenitori all'area di lavoro OMS da [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) o seguendo la procedura illustrata in [Aggiungere soluzioni di Log Analytics dalla Raccolta soluzioni](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="b2711-235">Add the Container Monitoring solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="b2711-236">Installare e usare Docker con un agente OMS.</span><span class="sxs-lookup"><span data-stu-id="b2711-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="b2711-237">In base al sistema operativo, è possibile scegliere uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2711-237">Based on your operating system, you can choose from the following methods:</span></span>

  * <span data-ttu-id="b2711-238">Nei sistemi operativi Linux supportati installare ed eseguire Docker, quindi installare e configurare l'[agente OMS per Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b2711-238">On supported Linux operating systems, install and run Docker and then install and configure the [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="b2711-239">Non è possibile eseguire l'agente OMS per Linux in CoreOS.</span><span class="sxs-lookup"><span data-stu-id="b2711-239">On CoreOS, you cannot run the OMS Agent for Linux.</span></span> <span data-ttu-id="b2711-240">È invece necessario eseguire una versione di tale agente inserita in contenitori.</span><span class="sxs-lookup"><span data-stu-id="b2711-240">Instead, you run a containerized version of the OMS Agent for Linux.</span></span> <span data-ttu-id="b2711-241">Vedere la sezione [Per tutti gli host del contenitore Linux inclusi CoreOS](#for-all-linux-container-hosts-including-coreos) o [Per tutti gli host del contenitore Linux Azure per enti pubblici incluso CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) se si usano contenitori nel cloud di Azure per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="b2711-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="b2711-242">In Windows Server 2016 e Windows 10, installare il motore e il client Docker, quindi connettere un agente per raccogliere informazioni da inviare a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b2711-242">On Windows Server 2016 and Windows 10, install the Docker Engine and client then connect an agent to gather information and send it to Log Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="b2711-243">Servizi contenitore</span><span class="sxs-lookup"><span data-stu-id="b2711-243">Container services</span></span>

- <span data-ttu-id="b2711-244">Se si opera in un ambiente Red Hat OpenShift, vedere [Configurare un agente OMS per Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="b2711-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="b2711-245">Se si ha un cluster Kubernetes che usa il servizio contenitore di Azure, vedere [Monitorare un cluster del servizio contenitore di Azure con Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="b2711-245">If you have a Kubernetes cluster using the Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="b2711-246">Se si ha un cluster DC/OS del servizio contenitore di Azure, vedere [Monitorare un cluster DC/OS del servizio contenitore di Azure con Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="b2711-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="b2711-247">Se è presente un ambiente in modalità Docker Swarm, per altre informazioni vedere [Configurare un agente OMS per Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="b2711-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="b2711-248">Se si usano contenitori con Service Fabric, vedere [Panoramica di Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2711-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="b2711-249">Consultare l'articolo sul [motore Docker in Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) per altre informazioni su come installare e configurare i motori di Docker sui computer che eseguono Windows.</span><span class="sxs-lookup"><span data-stu-id="b2711-249">Review the [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how to install and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b2711-250">Docker deve essere in esecuzione **prima** di installare l'[agente OMS per Linux](log-analytics-agent-linux.md) negli host di contenitori.</span><span class="sxs-lookup"><span data-stu-id="b2711-250">Docker must be running **before** you install the [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="b2711-251">Se l'agente era già stato installato prima di installare Docker, è necessario reinstallare l'agente di OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="b2711-251">If you've already installed the agent before installing Docker, you need to reinstall the OMS Agent for Linux.</span></span> <span data-ttu-id="b2711-252">Per altre informazioni su Docker, vedere il [sito Web di Docker](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="b2711-252">For more information about Docker, see the [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="b2711-253">Host del contenitore Linux</span><span class="sxs-lookup"><span data-stu-id="b2711-253">Linux container hosts</span></span>

<span data-ttu-id="b2711-254">Dopo aver installato Docker, usare le impostazioni seguenti per l'host di contenitori per configurare l'agente per l'uso con Docker.</span><span class="sxs-lookup"><span data-stu-id="b2711-254">After you've installed Docker, use the following settings for your container host to configure the agent for use with Docker.</span></span> <span data-ttu-id="b2711-255">Saranno necessari l'ID e la chiave dell'area di lavoro OMS, che è possibile identificare nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2711-255">First you need your OMS workspace ID and key, which you can find in the Azure portal.</span></span> <span data-ttu-id="b2711-256">Nell'area di lavoro fare clic su **Avvio rapido** > **Computer** per visualizzare **ID area di lavoro** e **Chiave primaria**.</span><span class="sxs-lookup"><span data-stu-id="b2711-256">In your workspace, click **Quick Start** > **Computers** to view your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="b2711-257">Copiare e incollare entrambi i valori nell'editor predefinito.</span><span class="sxs-lookup"><span data-stu-id="b2711-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="b2711-258">Per tutti gli host del contenitore Linux, ad eccezione di CoreOS</span><span class="sxs-lookup"><span data-stu-id="b2711-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="b2711-259">Per altre informazioni e procedure su come installare l'agente OMS per Linux, vedere [Connettere i computer Linux a Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b2711-259">For more information and steps on how to install the OMS Agent for Linux, see [Connect your Linux Computers to Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="b2711-260">Per tutti gli host del contenitore Linux inclusi CoreOS</span><span class="sxs-lookup"><span data-stu-id="b2711-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="b2711-261">Avviare il contenitore OMS da monitorare.</span><span class="sxs-lookup"><span data-stu-id="b2711-261">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="b2711-262">Modificare e usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b2711-262">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="b2711-263">Per tutti gli host del contenitore Linux Azure per enti pubblici incluso CoreOS</span><span class="sxs-lookup"><span data-stu-id="b2711-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="b2711-264">Avviare il contenitore OMS da monitorare.</span><span class="sxs-lookup"><span data-stu-id="b2711-264">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="b2711-265">Modificare e usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b2711-265">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-to-one-in-a-container"></a><span data-ttu-id="b2711-266">Passaggio dall'uso di un agente Linux installato a un agente in un contenitore</span><span class="sxs-lookup"><span data-stu-id="b2711-266">Switching from using an installed Linux agent to one in a container</span></span>
<span data-ttu-id="b2711-267">Se in precedenza veniva usato l'agente installato direttamente e si vuole usare invece un agente in esecuzione in un contenitore, prima è necessario rimuovere l'agente OMS per Linux.</span><span class="sxs-lookup"><span data-stu-id="b2711-267">If you previously used the directly-installed agent and want to instead use an agent running in a container, you must first remove the OMS Agent for Linux.</span></span> <span data-ttu-id="b2711-268">Vedere [Disinstallazione dell'agente OMS per Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) per comprendere come disinstallare correttamente l'agente.</span><span class="sxs-lookup"><span data-stu-id="b2711-268">See [Uninstalling the OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) to understand how to successfully uninstall the agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="b2711-269">Configurare un agente OMS per Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="b2711-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="b2711-270">È possibile eseguire l'agente OMS come servizio globale in Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="b2711-270">You can run the OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="b2711-271">Usare le informazioni seguenti per creare un servizio agente OMS.</span><span class="sxs-lookup"><span data-stu-id="b2711-271">Use the following information to create an OMS Agent service.</span></span> <span data-ttu-id="b2711-272">È necessario inserire l'ID e la chiave primaria dell'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="b2711-272">You need to insert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="b2711-273">Eseguire quanto segue sul nodo principale.</span><span class="sxs-lookup"><span data-stu-id="b2711-273">Run the following on the master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="b2711-274">Configurare un agente OMS per Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="b2711-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="b2711-275">Esistono tre modi per aggiungere l'agente OMS a Red Hat OpenShift e avviare la raccolta dei dati di monitoraggio del contenitore.</span><span class="sxs-lookup"><span data-stu-id="b2711-275">There are three ways to add the OMS Agent to Red Hat OpenShift to start collecting container monitoring data.</span></span>

* <span data-ttu-id="b2711-276">[Installare l'agente OMS per Linux](log-analytics-agent-linux.md) direttamente in ogni nodo OpenShift</span><span class="sxs-lookup"><span data-stu-id="b2711-276">[Install the OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="b2711-277">[Abilitare l'estensione della macchina virtuale di Log Analytics](log-analytics-azure-vm-extension.md) in ogni nodo OpenShift che risiede in Azure</span><span class="sxs-lookup"><span data-stu-id="b2711-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="b2711-278">Installare l'agente OMS come DaemonSet OpenShift</span><span class="sxs-lookup"><span data-stu-id="b2711-278">Install the OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="b2711-279">In questa sezione viene illustrata la procedura necessaria per installare l'agente OMS come DaemonSet OpenShift.</span><span class="sxs-lookup"><span data-stu-id="b2711-279">In this section we cover the steps required to install the OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="b2711-280">Accedere al nodo principale OpenShift e copiare il file yaml [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) da GitHub nel nodo principale e modificare il valore con l'ID dell'area di lavoro OMS e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="b2711-280">Sign on to the OpenShift master node and copy the yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub to your master node and modify the value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="b2711-281">Eseguire i comandi seguenti per creare un progetto per OMS e configurare l'account utente.</span><span class="sxs-lookup"><span data-stu-id="b2711-281">Run the following commands to create a project for OMS and set the user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="b2711-282">Per distribuire DaemonSet, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b2711-282">To deploy the daemon-set, run the following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="b2711-283">Per verificare che sia configurato e funzioni correttamente, digitare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b2711-283">To verify it is configured and working correctly, type the following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="b2711-284">L'output deve essere simile a:</span><span class="sxs-lookup"><span data-stu-id="b2711-284">and the output should resemble:</span></span>

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

<span data-ttu-id="b2711-285">Se si vuole usare i segreti per proteggere l'ID e la chiave primaria dell'area di lavoro OMS quando si usa il file yaml DaemonSet dell'agente OMS, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="b2711-285">If you want to use secrets to secure your OMS Workspace ID and Primary Key when using the OMS Agent daemon-set yaml file, perform the following steps.</span></span>

1. <span data-ttu-id="b2711-286">Accedere al nodo principale OpenShift e copiare il file yaml [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) e il segreto che genera lo script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) da GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2711-286">Sign on to the OpenShift master node and copy the yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="b2711-287">Questo script genererà il file yaml dei segreti per l'ID e la chiave primaria dell'area di lavoro OMS per proteggere le informazioni segrete.</span><span class="sxs-lookup"><span data-stu-id="b2711-287">This script will generate the secrets yaml file for OMS Workspace ID and Primary Key to secure your secrete information.</span></span>  
2. <span data-ttu-id="b2711-288">Eseguire i comandi seguenti per creare un progetto per OMS e configurare l'account utente.</span><span class="sxs-lookup"><span data-stu-id="b2711-288">Run the following commands to create a project for OMS and set the user account.</span></span> <span data-ttu-id="b2711-289">Il segreto che genera lo script chiede di specificare l'ID <WSID> e la chiave primaria <KEY> dell'area di lavoro OMS e, al completamento, crea il file ocp-secret.yaml.</span><span class="sxs-lookup"><span data-stu-id="b2711-289">The secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates the ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="b2711-290">Distribuire il file del segreto eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b2711-290">Deploy the secret file by running the following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="b2711-291">Verificare la distribuzione eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b2711-291">Verify deployment by running the following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="b2711-292">L'output deve essere simile a:</span><span class="sxs-lookup"><span data-stu-id="b2711-292">and the  output should resemble:</span></span>  

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

6. <span data-ttu-id="b2711-293">Distribuire il file yaml DaemonSet dell'agente OMS eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b2711-293">Deploy the OMS Agent daemon-set yaml file by running the following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="b2711-294">Verificare la distribuzione eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b2711-294">Verify deployment by running the following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="b2711-295">L'output deve essere simile a:</span><span class="sxs-lookup"><span data-stu-id="b2711-295">and the output should resemble:</span></span>

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

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="b2711-296">Proteggere le informazioni segrete per Docker Swarm e Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b2711-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="b2711-297">È possibile proteggere l'ID segreto dell'area di lavoro OMS e le chiavi primarie segrete per i servizi contenitore Docker Swarm e Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b2711-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="b2711-298">Proteggere i segreti per Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="b2711-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="b2711-299">In Docker Swarm, una volta creato il segreto per l'ID area di lavoro e la chiave primaria è possibile creare il servizio Docker per OMSagent.</span><span class="sxs-lookup"><span data-stu-id="b2711-299">For Docker Swarm, once the secret for Workspace ID and Primary Key is created, you can run the create the Docker service for OMSagent.</span></span> <span data-ttu-id="b2711-300">Usare le informazioni seguenti per creare i segreti.</span><span class="sxs-lookup"><span data-stu-id="b2711-300">Use the following information to create your secret information.</span></span>

1. <span data-ttu-id="b2711-301">Eseguire quanto segue sul nodo principale.</span><span class="sxs-lookup"><span data-stu-id="b2711-301">Run the following on the master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="b2711-302">Verificare che i segreti siano stati creati correttamente.</span><span class="sxs-lookup"><span data-stu-id="b2711-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="b2711-303">Eseguire il comando seguente per impostare i segreti per l'agente OMS nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="b2711-303">Run the following command to mount the secrets to the containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="b2711-304">Proteggere i segreti per Kubernetes con file yaml</span><span class="sxs-lookup"><span data-stu-id="b2711-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="b2711-305">Per Kubernetes è possibile usare uno script per generare il file yaml dei segreti per l'ID area di lavoro e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="b2711-305">For Kubernetes, you use a script to generate the secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="b2711-306">Nella pagina [OMS Docker/Kubernetes di GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) sono disponibili file usabili con o senza informazioni segrete.</span><span class="sxs-lookup"><span data-stu-id="b2711-306">At the [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="b2711-307">Il file DaemonSet predefinito dell'agente OMS non include informazioni segrete (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="b2711-307">The Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="b2711-308">Il file yaml DaemonSet dell'agente OMS usa le informazioni segrete (omsagent-ds-secrets.yaml) con script per la generazione di segreti per generare il file yaml dei segreti (omsagentsecret.yaml).</span><span class="sxs-lookup"><span data-stu-id="b2711-308">The OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts to generate the secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="b2711-309">È possibile scegliere di creare DaemonSet dell'agente OMS con o senza segreti.</span><span class="sxs-lookup"><span data-stu-id="b2711-309">You can choose to create omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="b2711-310">File DaemonSet con estensione yaml predefinito dell'agente OMS senza segreti</span><span class="sxs-lookup"><span data-stu-id="b2711-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="b2711-311">Per il file DaemonSet con estensione yaml predefinito dell'agente OMS, sostituire `<WSID>` e `<KEY>` a WSID e KEY.</span><span class="sxs-lookup"><span data-stu-id="b2711-311">For the default OMS Agent DaemonSet yaml file, replace the `<WSID>` and `<KEY>` to your WSID and KEY.</span></span> <span data-ttu-id="b2711-312">Copiare il file nel nodo principale ed eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2711-312">Copy the file to your master node and run the following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="b2711-313">File DaemonSet con estensione yaml predefinito dell'agente OMS con segreti</span><span class="sxs-lookup"><span data-stu-id="b2711-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="b2711-314">Per usare il DaemonSet dell'agente OMS con informazioni segrete, in primo luogo creare i segreti.</span><span class="sxs-lookup"><span data-stu-id="b2711-314">To use OMS Agent DaemonSet using secret information, create the secrets first.</span></span>
    1. <span data-ttu-id="b2711-315">Copiare lo script e il file modello dei segreti e assicurarsi che siano nella stessa directory.</span><span class="sxs-lookup"><span data-stu-id="b2711-315">Copy the script and secret template file and make sure they are on the same directory.</span></span>
        - <span data-ttu-id="b2711-316">Script per la generazione di segreti: secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="b2711-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="b2711-317">Modello di segreto: secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="b2711-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="b2711-318">Eseguire lo script come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="b2711-318">Run the script, like the following example.</span></span> <span data-ttu-id="b2711-319">Lo script richiede l'ID e la chiave primaria dell'area di lavoro OMS. Dopo aver specificato queste credenziali, lo script crea un file yaml dei segreti che può essere eseguito.</span><span class="sxs-lookup"><span data-stu-id="b2711-319">The script asks for the OMS Workspace ID and Primary Key and after you enter them, the script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="b2711-320">Creare il pod dei segreti eseguendo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2711-320">Create the secrets pod by running the following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="b2711-321">Per la verifica eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2711-321">To verify, run the following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="b2711-322">L'output deve essere simile a:</span><span class="sxs-lookup"><span data-stu-id="b2711-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="b2711-323">L'output deve essere simile a:</span><span class="sxs-lookup"><span data-stu-id="b2711-323">Output should resemble:</span></span>

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

    5. <span data-ttu-id="b2711-324">Creare il DaemonSet dell'agente OMS eseguendo l'istruzione ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="b2711-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="b2711-325">Verificare che il DaemonSet dell'agente OMS sia in esecuzione, con un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b2711-325">Verify that the OMS Agent DaemonSet is running, similar to the following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="b2711-326">Per Kubernetes usare uno script per generare il file dei segreti con estensione yaml per l'ID area di lavoro e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="b2711-326">For Kubernetes, use a script to generate the secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="b2711-327">Usare le informazioni di esempio seguenti con il [file yaml dell'agente OMS](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) per proteggere le informazioni segrete.</span><span class="sxs-lookup"><span data-stu-id="b2711-327">Use the following example information with the [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) to secure your secret information.</span></span>

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

## <a name="windows-container-hosts"></a><span data-ttu-id="b2711-328">Host del contenitore Windows</span><span class="sxs-lookup"><span data-stu-id="b2711-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="b2711-329">Preparazione prima dell'installazione degli agenti di Windows</span><span class="sxs-lookup"><span data-stu-id="b2711-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="b2711-330">Prima di installare gli agenti nei computer che eseguono Windows, è necessario configurare il servizio Docker.</span><span class="sxs-lookup"><span data-stu-id="b2711-330">Before you install agents on computers running Windows, you need to configure the Docker service.</span></span> <span data-ttu-id="b2711-331">La configurazione consente all'agente di Windows o all'estensione macchina virtuale Log Analytics di usare il socket TCP di Docker in modo che gli agenti possano accedere in remoto al daemon Docker e acquisire i dati per il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="b2711-331">The configuration allows the Windows agent or the Log Analytics virtual machine extension to use the Docker TCP socket so that the agents can access the Docker daemon remotely and to capture data for monitoring.</span></span>

#### <a name="to-start-docker-and-verify-its-configuration"></a><span data-ttu-id="b2711-332">Per avviare Docker e verificare la configurazione</span><span class="sxs-lookup"><span data-stu-id="b2711-332">To start Docker and verify its configuration</span></span>

<span data-ttu-id="b2711-333">Per configurare pipe TCP e named pipe per Windows Server, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="b2711-333">There are steps needed to set up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="b2711-334">In Windows PowerShell, abilitare pipe TCP e named pipe.</span><span class="sxs-lookup"><span data-stu-id="b2711-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="b2711-335">Configurare Docker con il file di configurazione per pipe TCP e named pipe.</span><span class="sxs-lookup"><span data-stu-id="b2711-335">Configure Docker with the configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="b2711-336">Il file di configurazione è disponibile in C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="b2711-336">The configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="b2711-337">Nel file daemon.json, è necessario specificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b2711-337">In the daemon.json file, you will need the following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="b2711-338">Per altre informazioni sulla configurazione del daemon Docker usata con contenitori Windows, vedere [Motore Docker in Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="b2711-338">For more information about the Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="b2711-339">Installare gli agenti Windows</span><span class="sxs-lookup"><span data-stu-id="b2711-339">Install Windows agents</span></span>

<span data-ttu-id="b2711-340">Per abilitare il monitoraggio dei contenitori Windows e Hyper-V, installare Microsoft Monitoring Agent (MMA) nei computer Windows che sono host del contenitore.</span><span class="sxs-lookup"><span data-stu-id="b2711-340">To enable Windows and Hyper-V container monitoring, install the Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="b2711-341">Per i computer che eseguono Windows nell'ambiente locale, vedere [Collegare i computer di Windows a Log Analytics](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="b2711-341">For computers running Windows in your on-premises environment, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="b2711-342">Per le macchine virtuali eseguite in Azure, collegarle a Log Analytics usando l'[estensione macchina virtuale](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b2711-342">For virtual machines running in Azure, connect them to Log Analytics using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="b2711-343">È possibile monitorare i contenitori Windows in esecuzione in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b2711-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="b2711-344">Solo le [macchine virtuali in esecuzione in Azure](log-analytics-azure-vm-extension.md) e i [computer che eseguono Windows nell'ambiente locale](log-analytics-windows-agents.md), tuttavia, sono attualmente supportati da Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b2711-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="b2711-345">È possibile verificare che la soluzione Monitoraggio contenitori sia impostata correttamente per Windows.</span><span class="sxs-lookup"><span data-stu-id="b2711-345">You can verify that the Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="b2711-346">Per verificare che il Management Pack sia stato scaricato correttamente, cercare *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="b2711-346">To check whether the management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="b2711-347">Il file dovrebbe trovarsi nella cartella C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span><span class="sxs-lookup"><span data-stu-id="b2711-347">The files should be in the C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="b2711-348">Componenti della soluzione</span><span class="sxs-lookup"><span data-stu-id="b2711-348">Solution components</span></span>

<span data-ttu-id="b2711-349">Se si usano agenti Windows, il Management Pack seguente viene installato in ogni computer con un agente quando si aggiunge questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="b2711-349">If you are using Windows agents, then the following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="b2711-350">Per il Management Pack non è richiesta alcuna configurazione o manutenzione.</span><span class="sxs-lookup"><span data-stu-id="b2711-350">No configuration or maintenance is required for the management pack.</span></span>

- <span data-ttu-id="b2711-351">*ContainerManagement.xxx* installato in C:\Programmi\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span><span class="sxs-lookup"><span data-stu-id="b2711-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="b2711-352">Informazioni dettagliate sulla raccolta di dati dei contenitori</span><span class="sxs-lookup"><span data-stu-id="b2711-352">Container data collection details</span></span>
<span data-ttu-id="b2711-353">La soluzione Monitoraggio contenitori raccoglie le varie metriche delle prestazioni e i vari dati di log da host del contenitore e contenitori usando gli agenti abilitati.</span><span class="sxs-lookup"><span data-stu-id="b2711-353">The Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="b2711-354">I dati vengono raccolti ogni tre minuti dai tipi di agenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="b2711-354">Data is collected every three minutes by the following agent types.</span></span>

- [<span data-ttu-id="b2711-355">Agente OMS per Linux</span><span class="sxs-lookup"><span data-stu-id="b2711-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="b2711-356">Agente Windows</span><span class="sxs-lookup"><span data-stu-id="b2711-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="b2711-357">Estensione macchina virtuale di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b2711-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="b2711-358">Record dei contenitori</span><span class="sxs-lookup"><span data-stu-id="b2711-358">Container records</span></span>

<span data-ttu-id="b2711-359">La tabella seguente mostra esempi di record raccolti dalla soluzione Monitoraggio contenitori e i tipi di dati visualizzati nei risultati della ricerca log.</span><span class="sxs-lookup"><span data-stu-id="b2711-359">The following table shows examples of records collected by the Container Monitoring solution and the data types that appear in log search results.</span></span>

| <span data-ttu-id="b2711-360">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="b2711-360">Data type</span></span> | <span data-ttu-id="b2711-361">Tipo di dati in Ricerca log</span><span class="sxs-lookup"><span data-stu-id="b2711-361">Data type in Log Search</span></span> | <span data-ttu-id="b2711-362">Fields</span><span class="sxs-lookup"><span data-stu-id="b2711-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2711-363">Prestazioni per host e contenitori</span><span class="sxs-lookup"><span data-stu-id="b2711-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="b2711-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="b2711-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="b2711-365">Inventario contenitori</span><span class="sxs-lookup"><span data-stu-id="b2711-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="b2711-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="b2711-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="b2711-367">Inventario delle immagini dei contenitori</span><span class="sxs-lookup"><span data-stu-id="b2711-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="b2711-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="b2711-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="b2711-369">Log contenitori</span><span class="sxs-lookup"><span data-stu-id="b2711-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="b2711-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="b2711-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="b2711-371">Log servizio contenitori</span><span class="sxs-lookup"><span data-stu-id="b2711-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="b2711-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="b2711-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="b2711-373">Inventario di nodi contenitore</span><span class="sxs-lookup"><span data-stu-id="b2711-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="b2711-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="b2711-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="b2711-375">Inventario di Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b2711-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="b2711-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="b2711-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="b2711-377">Processo contenitore</span><span class="sxs-lookup"><span data-stu-id="b2711-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="b2711-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="b2711-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="b2711-379">Eventi di Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b2711-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="b2711-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span><span class="sxs-lookup"><span data-stu-id="b2711-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="b2711-381">Le etichette aggiunte ai tipi di dati *PodLabel* sono etichette personalizzate.</span><span class="sxs-lookup"><span data-stu-id="b2711-381">Labels appended to *PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="b2711-382">Le etichette PodLabel aggiunte indicate nella tabella sono esempi.</span><span class="sxs-lookup"><span data-stu-id="b2711-382">The appended PodLabel labels shown in the table are examples.</span></span> <span data-ttu-id="b2711-383">`PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` saranno quindi diverse nel set di dati dell'ambiente e in genere saranno simili a `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="b2711-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="b2711-384">Monitorare i contenitori</span><span class="sxs-lookup"><span data-stu-id="b2711-384">Monitor containers</span></span>
<span data-ttu-id="b2711-385">Dopo avere abilitato la soluzione nel portale di OMS, il riquadro **Contenitori** mostra le informazioni di riepilogo sugli host di contenitori e i contenitori in esecuzione negli host.</span><span class="sxs-lookup"><span data-stu-id="b2711-385">After you have the solution enabled in the OMS portal, the **Containers** tile shows summary information about your container hosts and the containers running in hosts.</span></span>

![Riquadro Containers (Contenitori)](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="b2711-387">Il riquadro visualizza una panoramica del numero di contenitori nell'ambiente e indica se i contenitori presentano errori, sono in esecuzione oppure sono stati arrestati.</span><span class="sxs-lookup"><span data-stu-id="b2711-387">The tile shows an overview of how many containers you have in the environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-the-containers-dashboard"></a><span data-ttu-id="b2711-388">Uso del dashboard Containers (Contenitori)</span><span class="sxs-lookup"><span data-stu-id="b2711-388">Using the Containers dashboard</span></span>
<span data-ttu-id="b2711-389">Fare clic sul riquadro **Containers** (Contenitori).</span><span class="sxs-lookup"><span data-stu-id="b2711-389">Click the **Containers** tile.</span></span> <span data-ttu-id="b2711-390">Le visualizzazioni sono organizzate in base agli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2711-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="b2711-391">**Eventi del contenitore**: visualizza lo stato dei contenitori e i computer con contenitori non riusciti.</span><span class="sxs-lookup"><span data-stu-id="b2711-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="b2711-392">**Log contenitori**: visualizza un grafico dei file di log dei contenitori generati nel corso del tempo e un elenco di computer con il numero più elevato di file di log.</span><span class="sxs-lookup"><span data-stu-id="b2711-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with the highest number of log files.</span></span>
- <span data-ttu-id="b2711-393">**Eventi Kubernetes**: visualizza un grafico degli eventi di Kubernetes generati nel corso del tempo e un elenco dei motivi per cui i pod hanno generato gli eventi.</span><span class="sxs-lookup"><span data-stu-id="b2711-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of the reasons why pods generated the events.</span></span> <span data-ttu-id="b2711-394">*Questo set di dati viene usato solo negli ambienti Linux.*</span><span class="sxs-lookup"><span data-stu-id="b2711-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="b2711-395">**Inventario degli spazi dei nomi Kubernetes**: visualizza il numero di spazi dei nomi e di pod e la gerarchia.</span><span class="sxs-lookup"><span data-stu-id="b2711-395">**Kubernetes Namespace Inventory** - Shows the number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="b2711-396">*Questo set di dati viene usato solo negli ambienti Linux.*</span><span class="sxs-lookup"><span data-stu-id="b2711-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="b2711-397">**Inventario nodi del contenitore**: visualizza il numero di tipi di orchestrazioni usati nei nodi/host del contenitore.</span><span class="sxs-lookup"><span data-stu-id="b2711-397">**Container Node Inventory** - Shows the number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="b2711-398">I nodi/host del computer vengono anche indicati dal numero di contenitori.</span><span class="sxs-lookup"><span data-stu-id="b2711-398">The computer nodes/hosts are also listed by the number of containers.</span></span> <span data-ttu-id="b2711-399">*Questo set di dati viene usato solo negli ambienti Linux.*</span><span class="sxs-lookup"><span data-stu-id="b2711-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="b2711-400">**Inventario immagini contenitore**: visualizza il numero totale di immagini del contenitore usate e il numero di tipi di immagini.</span><span class="sxs-lookup"><span data-stu-id="b2711-400">**Container Images Inventory** - Shows the total number of container images used and number of image types.</span></span> <span data-ttu-id="b2711-401">Il numero delle immagini è indicato anche dal tag immagine.</span><span class="sxs-lookup"><span data-stu-id="b2711-401">The number of images are also listed by the image tag.</span></span>
- <span data-ttu-id="b2711-402">**Stato dei contenitori**: visualizza il numero totale di nodi contenitore/computer host con contenitori in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b2711-402">**Containers Status** - Shows the total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="b2711-403">I computer vengono anche indicati dal numero di host in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b2711-403">Computers are also listed by the number of running hosts.</span></span>
- <span data-ttu-id="b2711-404">**Processi del contenitore**: visualizza un grafico a linee dei processi del contenitore in esecuzione nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="b2711-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="b2711-405">I contenitori vengono anche indicati dal comando/processo in esecuzione nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="b2711-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="b2711-406">*Questo set di dati viene usato solo negli ambienti Linux.*</span><span class="sxs-lookup"><span data-stu-id="b2711-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="b2711-407">**Prestazioni CPU contenitore**: visualizza un grafico a linee dell'utilizzo medio della CPU nel corso del tempo per i nodi/host del computer.</span><span class="sxs-lookup"><span data-stu-id="b2711-407">**Container CPU Performance** - Shows a line chart of the average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="b2711-408">Elenca anche i nodi/host del computer in base all'utilizzo medio della CPU.</span><span class="sxs-lookup"><span data-stu-id="b2711-408">Also lists the computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="b2711-409">**Prestazioni memoria contenitore**: visualizza un grafico a linee dell'utilizzo della memoria nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="b2711-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="b2711-410">Elenca anche l'utilizzo della memoria del computer in base al nome dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="b2711-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="b2711-411">**Prestazioni computer**: visualizza i grafici a linee di percentuale di prestazioni della CPU nel corso del tempo, percentuale di utilizzo della memoria nel corso del tempo e megabyte di spazio su disco nel corso del tempo.</span><span class="sxs-lookup"><span data-stu-id="b2711-411">**Computer Performance** - Shows line charts of the percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="b2711-412">È possibile passare il puntatore su una linea di un grafico per visualizzare altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="b2711-412">You can hover over any line in a chart to view more details.</span></span>


<span data-ttu-id="b2711-413">Ogni area del dashboard è una rappresentazione visiva di una ricerca eseguita sui dati raccolti.</span><span class="sxs-lookup"><span data-stu-id="b2711-413">Each area of the dashboard is a visual representation of a search that is run on collected data.</span></span>

![Dashboard Containers (Contenitori)](./media/log-analytics-containers/containers-dash01.png)

![Dashboard Containers (Contenitori)](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="b2711-416">Nel pannello **Stato del contenitore** fare clic sull'area superiore come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b2711-416">In the **Container Status** area, click the top area, as shown below.</span></span>

![Stato dei contenitori](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="b2711-418">Si aprirà Ricerca log con informazioni sugli host e sullo stato del contenitore.</span><span class="sxs-lookup"><span data-stu-id="b2711-418">Log Search opens, displaying information about the state of your containers.</span></span>

![Ricerca log per i contenitori](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="b2711-420">A questo punto è possibile modificare la query di ricerca per trovare specifiche informazioni di interesse.</span><span class="sxs-lookup"><span data-stu-id="b2711-420">From here, you can edit the search query to modify it to find the specific information you're interested in.</span></span> <span data-ttu-id="b2711-421">Per altre informazioni sulle ricerche log, vedere [Ricerche nei log in Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="b2711-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="b2711-422">Risolvere i problemi cercando un contenitore con errori</span><span class="sxs-lookup"><span data-stu-id="b2711-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="b2711-423">Log Analytics contrassegna un contenitore come **Non riuscito** se il contenitore è stato terminato con un codice di uscita diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="b2711-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="b2711-424">È possibile visualizzare una panoramica degli errori nell'ambiente nell'area **Contenitori non riusciti**.</span><span class="sxs-lookup"><span data-stu-id="b2711-424">You can see an overview of the errors and failures in the environment in the **Failed Containers** area.</span></span>

### <a name="to-find-failed-containers"></a><span data-ttu-id="b2711-425">Per trovare i contenitori non riusciti</span><span class="sxs-lookup"><span data-stu-id="b2711-425">To find failed containers</span></span>
1. <span data-ttu-id="b2711-426">Fare clic sull'area **Stato del contenitore**.</span><span class="sxs-lookup"><span data-stu-id="b2711-426">Click the **Container Status** area.</span></span>  
   <span data-ttu-id="b2711-427">![Stato dei contenitori](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="b2711-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="b2711-428">Si aprirà Ricerca log e verrà visualizzato lo stato dei contenitori. Vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="b2711-428">Log Search opens and displays the state of your containers, similar to the following.</span></span>  
   ![stato dei contenitori](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="b2711-430">Fare quindi clic sul valore aggregato dei contenitori non riusciti per visualizzare altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="b2711-430">Next, click the aggregated value of failed containers to view additional information.</span></span> <span data-ttu-id="b2711-431">Espandere **mostra dettagli** per visualizzare l'ID immagine.</span><span class="sxs-lookup"><span data-stu-id="b2711-431">Expand **show more** to view the image ID.</span></span>  
   <span data-ttu-id="b2711-432">![contenitori non riusciti](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="b2711-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="b2711-433">Digitare quindi il codice seguente nella query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="b2711-433">Next, type the following in the search query.</span></span> <span data-ttu-id="b2711-434">`Type=ContainerInventory <ImageID>` visualizza i dettagli dell'immagine, ad esempio dimensioni e numero di immagini arrestate e non riuscite.</span><span class="sxs-lookup"><span data-stu-id="b2711-434">`Type=ContainerInventory <ImageID>` to see details about the image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="b2711-435">![contenitori non riusciti](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="b2711-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="b2711-436">Ricerca dei dati dei contenitori nei log</span><span class="sxs-lookup"><span data-stu-id="b2711-436">Search logs for container data</span></span>
<span data-ttu-id="b2711-437">Nella risoluzione di un errore specifico può essere utile vedere dove l'errore si verifica nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="b2711-437">When you're troubleshooting a specific error, it can help to see where it is occurring in your environment.</span></span> <span data-ttu-id="b2711-438">I tipi di log seguenti consentono di creare query per ottenere le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="b2711-438">The following log types will help you create queries to return the information you want.</span></span>


- <span data-ttu-id="b2711-439">**ContainerImageInventory**: usare questo tipo per trovare informazioni organizzate per immagine e visualizzare le informazioni sulle immagini, ad esempio ID o dimensioni.</span><span class="sxs-lookup"><span data-stu-id="b2711-439">**ContainerImageInventory** – Use this type when you're trying to find information organized by image and to view image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="b2711-440">**ContainerInventory**: usare questo tipo per ottenere informazioni sul percorso dei contenitori, i relativi nomi e le immagini che eseguono.</span><span class="sxs-lookup"><span data-stu-id="b2711-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="b2711-441">**ContainerLog**: usare questo tipo per trovare informazioni e voci specifiche del registro errori.</span><span class="sxs-lookup"><span data-stu-id="b2711-441">**ContainerLog** – Use this type when you want to find specific error log information and entries.</span></span>
- <span data-ttu-id="b2711-442">**ContainerNodeInventory_CL** Usare questo tipo quando sono necessarie le informazioni sull'host o sul nodo in cui si trovano i contenitori.</span><span class="sxs-lookup"><span data-stu-id="b2711-442">**ContainerNodeInventory_CL**  Use this type when you want the information about host/node where containers are residing.</span></span> <span data-ttu-id="b2711-443">Fornisce informazioni su versione di Docker, tipo di orchestrazione, risorsa di archiviazione e rete.</span><span class="sxs-lookup"><span data-stu-id="b2711-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="b2711-444">**ContainerProcess_CL** Usare questo tipo per visualizzare velocemente il processo in esecuzione nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="b2711-444">**ContainerProcess_CL** Use this type to quickly see the process running within the container.</span></span>
- <span data-ttu-id="b2711-445">**ContainerServiceLog**: usare questo tipo per trovare informazioni di audit trail per il daemon Docker, ad esempio comandi di avvio, arresto, eliminazione o pull.</span><span class="sxs-lookup"><span data-stu-id="b2711-445">**ContainerServiceLog** – Use this type when you're trying to find audit trail information for the Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="b2711-446">**KubeEvents_CL** Usare questo tipo per visualizzare gli eventi di Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b2711-446">**KubeEvents_CL**  Use this type to see the Kubernetes events.</span></span>
- <span data-ttu-id="b2711-447">**KubePodInventory_CL** Usare questo tipo quando sono necessarie le informazioni sulla gerarchia dei cluster.</span><span class="sxs-lookup"><span data-stu-id="b2711-447">**KubePodInventory_CL**  Use this type when you want to understand the cluster hierarchy information.</span></span>


### <a name="to-search-logs-for-container-data"></a><span data-ttu-id="b2711-448">Per cercare i dati dei contenitori nei log</span><span class="sxs-lookup"><span data-stu-id="b2711-448">To search logs for container data</span></span>
* <span data-ttu-id="b2711-449">Scegliere un'immagine non riuscita di recente e trovare i relativi registri degli errori.</span><span class="sxs-lookup"><span data-stu-id="b2711-449">Choose an image that you know has failed recently and find the error logs for it.</span></span> <span data-ttu-id="b2711-450">Iniziare cercando il nome di un contenitore che esegue l'immagine con una ricerca **ContainerInventory**.</span><span class="sxs-lookup"><span data-stu-id="b2711-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="b2711-451">Cercare ad esempio `Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="b2711-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="b2711-452">![Cercare contenitori Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="b2711-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="b2711-453">Prendere nota del nome del contenitore accanto a **Name** e cercare questi log.</span><span class="sxs-lookup"><span data-stu-id="b2711-453">The name of the container next to **Name**, and search for those logs.</span></span> <span data-ttu-id="b2711-454">In questo esempio si tratta di `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="b2711-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="b2711-455">**Visualizzare le informazioni sulle prestazioni**</span><span class="sxs-lookup"><span data-stu-id="b2711-455">**View performance information**</span></span>

<span data-ttu-id="b2711-456">Quando si inizia a creare query, può essere utile comprendere prima le operazioni possibili.</span><span class="sxs-lookup"><span data-stu-id="b2711-456">When you're beginning to construct queries, it can help to see what's possible first.</span></span> <span data-ttu-id="b2711-457">Per visualizzare ad esempio tutti i dati sulle prestazioni, provare con una query generica digitando la query di ricerca seguente.</span><span class="sxs-lookup"><span data-stu-id="b2711-457">For example, to see all performance data, try a broad query by typing the following search query.</span></span>

```
Type=Perf
```

![prestazioni dei contenitori](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="b2711-459">È possibile limitare i dati sulle prestazioni visualizzati a un contenitore specifico digitando il relativo nome a destra della query.</span><span class="sxs-lookup"><span data-stu-id="b2711-459">You can scope the performance data you're seeing to a specific container by typing the name of it to the right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="b2711-460">Verrà visualizzato l'elenco delle metriche delle prestazioni raccolte per un singolo contenitore.</span><span class="sxs-lookup"><span data-stu-id="b2711-460">That shows the list of performance metrics that are collected for an individual container.</span></span>

![prestazioni dei contenitori](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="b2711-462">Esempio di query di ricerca log</span><span class="sxs-lookup"><span data-stu-id="b2711-462">Example log search queries</span></span>
<span data-ttu-id="b2711-463">Spesso è utile compilare query iniziando con qualche esempio da modificare in funzione dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="b2711-463">It's often useful to build queries starting with an example or two and then modifying them to fit your environment.</span></span> <span data-ttu-id="b2711-464">Come punto di partenza è possibile provare a usare l'area **Query di esempio** per compilare query più avanzate.</span><span class="sxs-lookup"><span data-stu-id="b2711-464">As a starting point, you can experiment with the **Sample Queries** area to help you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Query sui contenitori](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="b2711-466">Salvataggio delle query di ricerca log</span><span class="sxs-lookup"><span data-stu-id="b2711-466">Saving log search queries</span></span>
<span data-ttu-id="b2711-467">Il salvataggio di query è una funzionalità standard di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b2711-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="b2711-468">Le query salvate potranno essere riusate rapidamente in futuro.</span><span class="sxs-lookup"><span data-stu-id="b2711-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="b2711-469">Dopo aver creato una query che si ritiene utile, salvarla facendo clic su **Preferiti** nella parte superiore della pagina Ricerca log.</span><span class="sxs-lookup"><span data-stu-id="b2711-469">After you create a query that you find useful, save it by clicking **Favorites** at the top of the Log Search page.</span></span> <span data-ttu-id="b2711-470">Sarà possibile accedere facilmente alla query in seguito dalla pagina **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b2711-470">Then you can easily access it later from the **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2711-471">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b2711-471">Next steps</span></span>
* <span data-ttu-id="b2711-472">[Eseguire ricerche nei log](log-analytics-log-searches.md) per visualizzare i record di dati dettagliati per i contenitori.</span><span class="sxs-lookup"><span data-stu-id="b2711-472">[Search logs](log-analytics-log-searches.md) to view detailed container data records.</span></span>
