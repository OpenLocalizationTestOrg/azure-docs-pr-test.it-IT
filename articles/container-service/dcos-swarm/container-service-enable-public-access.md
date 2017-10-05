---
title: Consentire l'accesso all'app contenitore DC/OS di Azure | Documentazione Microsoft
description: Come abilitare l'accesso pubblico ai contenitori DC/OS in un servizio contenitore di Azure.
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, Contenitori, Micro-servizi, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c9ef5913859cf3a55a2de2107a9304f1d28a4829
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="enable-public-access-to-an-azure-container-service-application"></a><span data-ttu-id="6805a-104">Abilitare l'accesso pubblico a un'applicazione del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="6805a-104">Enable public access to an Azure Container Service application</span></span>
<span data-ttu-id="6805a-105">Qualsiasi contenitore DC/OS nel [pool di agenti pubblico](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) del servizio contenitore di Azure viene esposto automaticamente a Internet.</span><span class="sxs-lookup"><span data-stu-id="6805a-105">Any DC/OS container in the ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed to the internet.</span></span> <span data-ttu-id="6805a-106">Per impostazione predefinita, le porte **80**, **443**, **8080** sono aperte e qualsiasi contenitore (pubblico) in ascolto su queste porte è accessibile.</span><span class="sxs-lookup"><span data-stu-id="6805a-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="6805a-107">Questo articolo descrive come aprire altre porte per le applicazioni nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="6805a-107">This article shows you how to open more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="6805a-108">Aprire una porta (portale)</span><span class="sxs-lookup"><span data-stu-id="6805a-108">Open a port (portal)</span></span>
<span data-ttu-id="6805a-109">Prima di tutto è necessario aprire la porta desiderata.</span><span class="sxs-lookup"><span data-stu-id="6805a-109">First, we need to open the port we want.</span></span>

1. <span data-ttu-id="6805a-110">Accedere al portale.</span><span class="sxs-lookup"><span data-stu-id="6805a-110">Log in to the portal.</span></span>
2. <span data-ttu-id="6805a-111">Trovare il gruppo di risorse in cui è stato distribuito il servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="6805a-111">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="6805a-112">Selezionare il servizio di bilanciamento del carico dell'agente, che ha un nome simile a **XXXX-agent-lb-XXXX**.</span><span class="sxs-lookup"><span data-stu-id="6805a-112">Select the agent load balancer (which is named similar to **XXXX-agent-lb-XXXX**).</span></span>
   
    ![Servizio di bilanciamento del carico del servizio contenitore di Azure](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="6805a-114">Fare clic su **Probe** e quindi su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6805a-114">Click **Probes** and then **Add**.</span></span>
   
    ![Probe del servizio di bilanciamento del carico del servizio contenitore di Azure](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="6805a-116">Compilare il form dei probe e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6805a-116">Fill out the probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="6805a-117">Campo</span><span class="sxs-lookup"><span data-stu-id="6805a-117">Field</span></span> | <span data-ttu-id="6805a-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6805a-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="6805a-119">Nome</span><span class="sxs-lookup"><span data-stu-id="6805a-119">Name</span></span> |<span data-ttu-id="6805a-120">Nome descrittivo del probe.</span><span class="sxs-lookup"><span data-stu-id="6805a-120">A descriptive name of the probe.</span></span> |
   | <span data-ttu-id="6805a-121">Port</span><span class="sxs-lookup"><span data-stu-id="6805a-121">Port</span></span> |<span data-ttu-id="6805a-122">Porta del contenitore da testare.</span><span class="sxs-lookup"><span data-stu-id="6805a-122">The port of the container to test.</span></span> |
   | <span data-ttu-id="6805a-123">Path</span><span class="sxs-lookup"><span data-stu-id="6805a-123">Path</span></span> |<span data-ttu-id="6805a-124">(In modalità HTTP) Percorso relativo del sito Web su cui eseguire probe.</span><span class="sxs-lookup"><span data-stu-id="6805a-124">(When in HTTP mode) The relative website path to probe.</span></span> <span data-ttu-id="6805a-125">HTTPS non è supportato.</span><span class="sxs-lookup"><span data-stu-id="6805a-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="6805a-126">Interval</span><span class="sxs-lookup"><span data-stu-id="6805a-126">Interval</span></span> |<span data-ttu-id="6805a-127">Intervallo di tempo tra i tentativi del probe, in secondi.</span><span class="sxs-lookup"><span data-stu-id="6805a-127">The amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="6805a-128">Soglia non integra</span><span class="sxs-lookup"><span data-stu-id="6805a-128">Unhealthy threshold</span></span> |<span data-ttu-id="6805a-129">Numero di tentativi consecutivi del probe prima che il contenitore sia considerato non integro.</span><span class="sxs-lookup"><span data-stu-id="6805a-129">Number of consecutive probe attempts before considering the container unhealthy.</span></span> |
6. <span data-ttu-id="6805a-130">Tornare alle proprietà del servizio di bilanciamento del carico dell'agente, fare clic su **Regole di bilanciamento del carico** e quindi su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6805a-130">Back at the properties of the agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Regole del servizio di bilanciamento del carico del servizio contenitore di Azure](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="6805a-132">Compilare il modulo del servizio di bilanciamento del carico e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6805a-132">Fill out the load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="6805a-133">Campo</span><span class="sxs-lookup"><span data-stu-id="6805a-133">Field</span></span> | <span data-ttu-id="6805a-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6805a-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="6805a-135">Nome</span><span class="sxs-lookup"><span data-stu-id="6805a-135">Name</span></span> |<span data-ttu-id="6805a-136">Nome descrittivo del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="6805a-136">A descriptive name of the load balancer.</span></span> |
   | <span data-ttu-id="6805a-137">Port</span><span class="sxs-lookup"><span data-stu-id="6805a-137">Port</span></span> |<span data-ttu-id="6805a-138">Porta pubblica in ingresso.</span><span class="sxs-lookup"><span data-stu-id="6805a-138">The public incoming port.</span></span> |
   | <span data-ttu-id="6805a-139">Porta back-end</span><span class="sxs-lookup"><span data-stu-id="6805a-139">Backend port</span></span> |<span data-ttu-id="6805a-140">Porta pubblica interna del contenitore a cui instradare il traffico.</span><span class="sxs-lookup"><span data-stu-id="6805a-140">The internal-public port of the container to route traffic to.</span></span> |
   | <span data-ttu-id="6805a-141">Pool back-end</span><span class="sxs-lookup"><span data-stu-id="6805a-141">Backend pool</span></span> |<span data-ttu-id="6805a-142">I contenitori in questo pool saranno la destinazione per questo servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="6805a-142">The containers in this pool will be the target for this load balancer.</span></span> |
   | <span data-ttu-id="6805a-143">Probe</span><span class="sxs-lookup"><span data-stu-id="6805a-143">Probe</span></span> |<span data-ttu-id="6805a-144">Probe usato per determinare se una destinazione nel **Pool back-end** è integra.</span><span class="sxs-lookup"><span data-stu-id="6805a-144">The probe used to determine if a target in the **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="6805a-145">Persistenza della sessione</span><span class="sxs-lookup"><span data-stu-id="6805a-145">Session persistence</span></span> |<span data-ttu-id="6805a-146">Determina la modalità di gestione del traffico da un client per la durata della sessione.</span><span class="sxs-lookup"><span data-stu-id="6805a-146">Determines how traffic from a client should be handled for the duration of the session.</span></span><br><br><span data-ttu-id="6805a-147">**Nessuna**: le richieste successive provenienti dallo stesso client possono essere gestite da qualsiasi contenitore.</span><span class="sxs-lookup"><span data-stu-id="6805a-147">**None**: Successive requests from the same client can be handled by any container.</span></span><br><span data-ttu-id="6805a-148">**IP client**: le richieste successive provenienti dallo stesso indirizzo IP client vengono gestite dallo stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="6805a-148">**Client IP**: Successive requests from the same client IP are handled by the same container.</span></span><br><span data-ttu-id="6805a-149">**IP e protocollo client**: le richieste successive provenienti dalla stessa combinazione di indirizzo IP e protocollo client vengono gestite dallo stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="6805a-149">**Client IP and protocol**: Successive requests from the same client IP and protocol combination are handled by the same container.</span></span> |
   | <span data-ttu-id="6805a-150">Timeout di inattività</span><span class="sxs-lookup"><span data-stu-id="6805a-150">Idle timeout</span></span> |<span data-ttu-id="6805a-151">(Solo TCP) Tempo necessario, in minuti, per mantenere aperto un client TCP/HTTP aprire senza basarsi sui messaggi *keep-alive* .</span><span class="sxs-lookup"><span data-stu-id="6805a-151">(TCP only) In minutes, the time to keep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="6805a-152">Aggiungere una regola di sicurezza (portale)</span><span class="sxs-lookup"><span data-stu-id="6805a-152">Add a security rule (portal)</span></span>
<span data-ttu-id="6805a-153">Successivamente, è necessario aggiungere una regola di sicurezza che instradi il traffico dalla porta aperta tramite il firewall.</span><span class="sxs-lookup"><span data-stu-id="6805a-153">Next, we need to add a security rule that routes traffic from our opened port through the firewall.</span></span>

1. <span data-ttu-id="6805a-154">Accedere al portale.</span><span class="sxs-lookup"><span data-stu-id="6805a-154">Log in to the portal.</span></span>
2. <span data-ttu-id="6805a-155">Trovare il gruppo di risorse in cui è stato distribuito il servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="6805a-155">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="6805a-156">Selezionare il gruppo di sicurezza di rete dell'agente **pubblico**, che ha un nome simile a **XXXX-agent-public-nsg-XXXX**.</span><span class="sxs-lookup"><span data-stu-id="6805a-156">Select the **public** agent network security group (which is named similar to **XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Gruppo di sicurezza di rete del servizio contenitore di Azure](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="6805a-158">Selezionare **Regole di sicurezza in ingresso** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6805a-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Regole del gruppo di sicurezza di rete del servizio contenitore di Azure](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="6805a-160">Compilare la regola del firewall per consentire la porta pubblica e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6805a-160">Fill out the firewall rule to allow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="6805a-161">Campo</span><span class="sxs-lookup"><span data-stu-id="6805a-161">Field</span></span> | <span data-ttu-id="6805a-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6805a-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="6805a-163">Nome</span><span class="sxs-lookup"><span data-stu-id="6805a-163">Name</span></span> |<span data-ttu-id="6805a-164">Nome descrittivo della regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="6805a-164">A descriptive name of the firewall rule.</span></span> |
   | <span data-ttu-id="6805a-165">Priorità</span><span class="sxs-lookup"><span data-stu-id="6805a-165">Priority</span></span> |<span data-ttu-id="6805a-166">Classificazione di priorità per la regola.</span><span class="sxs-lookup"><span data-stu-id="6805a-166">Priority rank for the rule.</span></span> <span data-ttu-id="6805a-167">Più è basso il numero, maggiore sarà la priorità.</span><span class="sxs-lookup"><span data-stu-id="6805a-167">The lower the number the higher the priority.</span></span> |
   | <span data-ttu-id="6805a-168">Sorgente</span><span class="sxs-lookup"><span data-stu-id="6805a-168">Source</span></span> |<span data-ttu-id="6805a-169">Consente di limitare l'intervallo di indirizzi IP in ingresso che la regola dovrà consentire o negare.</span><span class="sxs-lookup"><span data-stu-id="6805a-169">Restrict the incoming IP address range to be allowed or denied by this rule.</span></span> <span data-ttu-id="6805a-170">Usare **Qualsiasi** per non specificare una restrizione.</span><span class="sxs-lookup"><span data-stu-id="6805a-170">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="6805a-171">Service</span><span class="sxs-lookup"><span data-stu-id="6805a-171">Service</span></span> |<span data-ttu-id="6805a-172">Selezionare un set di servizi predefiniti a cui è destinata questa regola di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="6805a-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="6805a-173">In caso contrario, usare **Personalizzato** per crearne di personalizzati.</span><span class="sxs-lookup"><span data-stu-id="6805a-173">Otherwise use **Custom** to create your own.</span></span> |
   | <span data-ttu-id="6805a-174">Protocol</span><span class="sxs-lookup"><span data-stu-id="6805a-174">Protocol</span></span> |<span data-ttu-id="6805a-175">Consente di limitare il traffico in base a **TCP** o **UDP**.</span><span class="sxs-lookup"><span data-stu-id="6805a-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="6805a-176">Usare **Qualsiasi** per non specificare una restrizione.</span><span class="sxs-lookup"><span data-stu-id="6805a-176">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="6805a-177">Intervallo di porte</span><span class="sxs-lookup"><span data-stu-id="6805a-177">Port range</span></span> |<span data-ttu-id="6805a-178">Quando **Servizio** è **Personalizzato**, specifica l'intervallo di porte interessato da questa regola.</span><span class="sxs-lookup"><span data-stu-id="6805a-178">When **Service** is **Custom**, specifies the range of ports that this rule affects.</span></span> <span data-ttu-id="6805a-179">È possibile usare una singola porta, ad esempio **80**, o un intervallo come **1024-1500**.</span><span class="sxs-lookup"><span data-stu-id="6805a-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="6805a-180">Azione</span><span class="sxs-lookup"><span data-stu-id="6805a-180">Action</span></span> |<span data-ttu-id="6805a-181">Consentire o negare il traffico che soddisfa i criteri.</span><span class="sxs-lookup"><span data-stu-id="6805a-181">Allow or deny traffic that meets the criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6805a-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6805a-182">Next steps</span></span>
<span data-ttu-id="6805a-183">Informazioni sulle differenze tra [agenti DC/OS pubblici e privati](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="6805a-183">Learn about the difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="6805a-184">Sono disponibili altre informazioni sulla [gestione dei contenitori DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="6805a-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

