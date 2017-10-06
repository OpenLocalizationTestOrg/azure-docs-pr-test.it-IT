---
title: "architettura di connettività di Database SQL aaaAzure | Documenti Microsoft"
description: "Questo documento illustra hello Azure SQLDB connettività architettura da Azure o da all'esterno di Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="312ea-103">Architettura della connettività del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="312ea-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="312ea-104">In questo articolo illustra l'architettura di connettività di Database SQL di Azure hello e viene spiegato come diversi componenti hello funzionano toodirect traffico tooyour istanza Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="312ea-104">This article explains hello Azure SQL Database connectivity architecture and explains how hello different components function toodirect traffic tooyour instance of Azure SQL Database.</span></span> <span data-ttu-id="312ea-105">Questi componenti di connettività di Database SQL di Azure di funzione toohello il traffico di rete toodirect il database di Azure con i client che si connettono da all'interno di Azure e con i client che si connettono dall'esterno di Azure.</span><span class="sxs-lookup"><span data-stu-id="312ea-105">These Azure SQL Database connectivity components function toodirect network traffic toohello Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="312ea-106">In questo articolo fornisce anche toochange esempi di script come si verifica la connettività e considerazioni hello relative impostazioni di connettività toochanging hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="312ea-106">This article also provides script samples toochange how connectivity occurs, and hello considerations related toochanging hello default connectivity settings.</span></span> <span data-ttu-id="312ea-107">Se dopo aver letto questo articolo sorgono domande, contattare Dhruv all'indirizzo dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="312ea-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="312ea-108">Architettura della connettività</span><span class="sxs-lookup"><span data-stu-id="312ea-108">Connectivity architecture</span></span>

<span data-ttu-id="312ea-109">Hello seguente diagramma fornisce una panoramica generale di hello architettura di connettività di Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="312ea-109">hello following diagram provides a high-level overview of hello Azure SQL Database connectivity architecture.</span></span> 

![panoramica dell'architettura](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="312ea-111">Hello passaggi seguenti descrivono come una connessione viene stabilita tooan database SQL di Azure tramite hello Database SQL di Azure software carico-bilanciamento e il gateway di Database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="312ea-111">hello following steps describe how a connection is established tooan Azure SQL database through hello Azure SQL Database software load-balancer (SLB) and hello Azure SQL Database gateway.</span></span>

- <span data-ttu-id="312ea-112">I client all'interno di Azure o all'esterno di Azure connettersi toohello SLB, che ha un indirizzo IP pubblico e in ascolto sulla porta 1433.</span><span class="sxs-lookup"><span data-stu-id="312ea-112">Clients within Azure or outside of Azure connect toohello SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="312ea-113">Hello SLB indirizza il gateway di traffico toohello Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="312ea-113">hello SLB directs traffic toohello Azure SQL Database gateway.</span></span>
- <span data-ttu-id="312ea-114">gateway Hello reindirizza hello traffico toohello proxy corretto middleware.</span><span class="sxs-lookup"><span data-stu-id="312ea-114">hello gateway redirects hello traffic toohello correct proxy middleware.</span></span>
- <span data-ttu-id="312ea-115">middleware proxy Hello reindirizza il database SQL di Azure appropriato di hello traffico toohello.</span><span class="sxs-lookup"><span data-stu-id="312ea-115">hello proxy middleware redirects hello traffic toohello appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="312ea-116">Ognuno di questi componenti è distribuiti di tipo denial of protection service (DDoS) incorporato in rete hello e il livello di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="312ea-116">Each of these components has distributed denial of service (DDoS) protection built-in at hello network and hello app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="312ea-117">Connettività dall'interno di Azure</span><span class="sxs-lookup"><span data-stu-id="312ea-117">Connectivity from within Azure</span></span>

<span data-ttu-id="312ea-118">Se ci si connette dall'interno di Azure, il criterio di connessione predefinito per le connessioni è **reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="312ea-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="312ea-119">Un criterio di **reindirizzare** significa che le connessioni al termine della sessione TCP hello database SQL di Azure toohello stabilita, sessione client hello è quindi reindirizzati toohello proxy middleware con un IP virtuale di destinazione toohello modifica da che di hello Azure SQL Database gateway toothat di hello proxy middleware.</span><span class="sxs-lookup"><span data-stu-id="312ea-119">A policy of **Redirect** means that connections after hello TCP session is established toohello Azure SQL database, hello client session is then redirected toohello proxy middleware with a change toohello destination virtual IP from that of hello Azure SQL Database gateway toothat of hello proxy middleware.</span></span> <span data-ttu-id="312ea-120">Successivamente, tutti i pacchetti successivi del flusso direttamente tramite il middleware proxy hello, ignorando il gateway di Database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="312ea-120">Thereafter, all subsequent packets flow directly via hello proxy middleware, bypassing hello Azure SQL Database gateway.</span></span> <span data-ttu-id="312ea-121">Hello seguente diagramma illustra il flusso del traffico.</span><span class="sxs-lookup"><span data-stu-id="312ea-121">hello following diagram illustrates this traffic flow.</span></span>

![panoramica dell'architettura](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="312ea-123">Connettività dall'esterno di Azure</span><span class="sxs-lookup"><span data-stu-id="312ea-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="312ea-124">Se ci si connette dall'esterno di Azure, le connessioni usano un criterio di connessione **proxy** per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="312ea-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="312ea-125">Un criterio di **Proxy** significa che sessione TCP hello viene stabilita tramite il gateway di Database SQL di Azure hello e tutti i pacchetti successivi flusso tramite hello gateway.</span><span class="sxs-lookup"><span data-stu-id="312ea-125">A policy of **Proxy** means that hello TCP session is established via hello Azure SQL Database gateway and all subsequent packets flow via hello gateway.</span></span> <span data-ttu-id="312ea-126">Hello seguente diagramma illustra il flusso del traffico.</span><span class="sxs-lookup"><span data-stu-id="312ea-126">hello following diagram illustrates this traffic flow.</span></span>

![panoramica dell'architettura](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="312ea-128">Indirizzi IP del gateway del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="312ea-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="312ea-129">database di SQL Azure tooconnect tooan da risorse locali, è necessario gateway di Database SQL di Azure toohello di traffico di tooallow rete in uscita per l'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="312ea-129">tooconnect tooan Azure SQL database from on-premises resources, you need tooallow outbound network traffic toohello Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="312ea-130">Le connessioni passano solo tramite il gateway di hello quando ci si connette in modalità Proxy, che è l'impostazione predefinita di hello durante la connessione da risorse locali.</span><span class="sxs-lookup"><span data-stu-id="312ea-130">Your connections only go via hello gateway when connecting in Proxy mode, which is hello default when connecting from on-premises resources.</span></span>

<span data-ttu-id="312ea-131">Nella seguente sono elencati nella tabella Hello hello IP primario e secondario del gateway di Database SQL di Azure hello per tutte le aree dati.</span><span class="sxs-lookup"><span data-stu-id="312ea-131">hello following table lists hello primary and secondary IPs of hello Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="312ea-132">Per alcune aree sono disponibili due indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="312ea-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="312ea-133">In queste aree, indirizzo IP primario hello è l'indirizzo IP corrente hello del gateway hello e secondo indirizzo IP di hello è un indirizzo IP di failover.</span><span class="sxs-lookup"><span data-stu-id="312ea-133">In these regions, hello primary IP address is hello current IP address of hello gateway and hello second IP address is a failover IP address.</span></span> <span data-ttu-id="312ea-134">indirizzo failover Hello è toowhich indirizzo hello è possibile spostare l'elevata disponibilità server tookeep hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="312ea-134">hello failover address is hello address toowhich we might move your server tookeep hello service availability high.</span></span> <span data-ttu-id="312ea-135">Per queste aree, è consigliabile consentire tooboth in uscita gli indirizzi IP hello.</span><span class="sxs-lookup"><span data-stu-id="312ea-135">For these regions, we recommend that you allow outbound tooboth hello IP addresses.</span></span> <span data-ttu-id="312ea-136">secondo indirizzo IP di Hello è di proprietà di Microsoft e non è in ascolto su alcun servizio fino a quando non viene attivato da connessioni tooaccept Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="312ea-136">hello second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database tooaccept connections.</span></span>

| <span data-ttu-id="312ea-137">Nome area</span><span class="sxs-lookup"><span data-stu-id="312ea-137">Region Name</span></span> | <span data-ttu-id="312ea-138">Indirizzo IP primario</span><span class="sxs-lookup"><span data-stu-id="312ea-138">Primary IP address</span></span> | <span data-ttu-id="312ea-139">Indirizzo IP secondario</span><span class="sxs-lookup"><span data-stu-id="312ea-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="312ea-140">Australia orientale</span><span class="sxs-lookup"><span data-stu-id="312ea-140">Australia East</span></span> | <span data-ttu-id="312ea-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="312ea-141">191.238.66.109</span></span> | <span data-ttu-id="312ea-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="312ea-142">13.75.149.87</span></span> |
| <span data-ttu-id="312ea-143">Australia sud-orientale</span><span class="sxs-lookup"><span data-stu-id="312ea-143">Australia South East</span></span> | <span data-ttu-id="312ea-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="312ea-144">191.239.192.109</span></span> | <span data-ttu-id="312ea-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="312ea-145">13.73.109.251</span></span> |
| <span data-ttu-id="312ea-146">Brasile meridionale</span><span class="sxs-lookup"><span data-stu-id="312ea-146">Brazil South</span></span> | <span data-ttu-id="312ea-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="312ea-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="312ea-148">Canada centrale</span><span class="sxs-lookup"><span data-stu-id="312ea-148">Canada Central</span></span> | <span data-ttu-id="312ea-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="312ea-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="312ea-150">Canada orientale</span><span class="sxs-lookup"><span data-stu-id="312ea-150">Canada East</span></span> | <span data-ttu-id="312ea-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="312ea-151">40.86.226.166</span></span> | |
| <span data-ttu-id="312ea-152">Stati Uniti centrali</span><span class="sxs-lookup"><span data-stu-id="312ea-152">Central US</span></span> | <span data-ttu-id="312ea-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="312ea-153">23.99.160.139</span></span> | <span data-ttu-id="312ea-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="312ea-154">13.67.215.62</span></span> |
| <span data-ttu-id="312ea-155">Asia orientale</span><span class="sxs-lookup"><span data-stu-id="312ea-155">East Asia</span></span> | <span data-ttu-id="312ea-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="312ea-156">191.234.2.139</span></span> | <span data-ttu-id="312ea-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="312ea-157">52.175.33.150</span></span> |
| <span data-ttu-id="312ea-158">Stati Uniti orientali 1</span><span class="sxs-lookup"><span data-stu-id="312ea-158">East US 1</span></span> | <span data-ttu-id="312ea-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="312ea-159">191.238.6.43</span></span> | <span data-ttu-id="312ea-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="312ea-160">40.121.158.30</span></span> |
| <span data-ttu-id="312ea-161">Stati Uniti orientali 2</span><span class="sxs-lookup"><span data-stu-id="312ea-161">East US 2</span></span> | <span data-ttu-id="312ea-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="312ea-162">191.239.224.107</span></span> | <span data-ttu-id="312ea-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="312ea-163">40.79.84.180</span></span> |
| <span data-ttu-id="312ea-164">India centrale</span><span class="sxs-lookup"><span data-stu-id="312ea-164">India Central</span></span> | <span data-ttu-id="312ea-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="312ea-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="312ea-166">India meridionale</span><span class="sxs-lookup"><span data-stu-id="312ea-166">India South</span></span> | <span data-ttu-id="312ea-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="312ea-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="312ea-168">India occidentale</span><span class="sxs-lookup"><span data-stu-id="312ea-168">India West</span></span> | <span data-ttu-id="312ea-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="312ea-169">104.211.160.80</span></span> | |
| <span data-ttu-id="312ea-170">Giappone orientale</span><span class="sxs-lookup"><span data-stu-id="312ea-170">Japan East</span></span> | <span data-ttu-id="312ea-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="312ea-171">191.237.240.43</span></span> | <span data-ttu-id="312ea-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="312ea-172">13.78.61.196</span></span> |
| <span data-ttu-id="312ea-173">Giappone occidentale</span><span class="sxs-lookup"><span data-stu-id="312ea-173">Japan West</span></span> | <span data-ttu-id="312ea-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="312ea-174">191.238.68.11</span></span> | <span data-ttu-id="312ea-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="312ea-175">104.214.148.156</span></span> |
| <span data-ttu-id="312ea-176">Corea centrale</span><span class="sxs-lookup"><span data-stu-id="312ea-176">Korea Central</span></span> | <span data-ttu-id="312ea-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="312ea-177">52.231.32.42</span></span> | |
| <span data-ttu-id="312ea-178">Corea meridionale</span><span class="sxs-lookup"><span data-stu-id="312ea-178">Korea South</span></span> | <span data-ttu-id="312ea-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="312ea-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="312ea-180">Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="312ea-180">North Central US</span></span> | <span data-ttu-id="312ea-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="312ea-181">23.98.55.75</span></span> | <span data-ttu-id="312ea-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="312ea-182">23.96.178.199</span></span> |
| <span data-ttu-id="312ea-183">Europa settentrionale</span><span class="sxs-lookup"><span data-stu-id="312ea-183">North Europe</span></span> | <span data-ttu-id="312ea-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="312ea-184">191.235.193.75</span></span> | <span data-ttu-id="312ea-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="312ea-185">40.113.93.91</span></span> |
| <span data-ttu-id="312ea-186">Stati Uniti centro-meridionali</span><span class="sxs-lookup"><span data-stu-id="312ea-186">South Central US</span></span> | <span data-ttu-id="312ea-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="312ea-187">23.98.162.75</span></span> | <span data-ttu-id="312ea-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="312ea-188">13.66.62.124</span></span> |
| <span data-ttu-id="312ea-189">Asia sudorientale</span><span class="sxs-lookup"><span data-stu-id="312ea-189">South East Asia</span></span> | <span data-ttu-id="312ea-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="312ea-190">23.100.117.95</span></span> | <span data-ttu-id="312ea-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="312ea-191">104.43.15.0</span></span> |
| <span data-ttu-id="312ea-192">Regno Unito settentrionale</span><span class="sxs-lookup"><span data-stu-id="312ea-192">UK North</span></span> | <span data-ttu-id="312ea-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="312ea-193">13.87.97.210</span></span> | |
| <span data-ttu-id="312ea-194">Regno Unito meridionale 1</span><span class="sxs-lookup"><span data-stu-id="312ea-194">UK South 1</span></span> | <span data-ttu-id="312ea-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="312ea-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="312ea-196">Regno Unito meridionale 2</span><span class="sxs-lookup"><span data-stu-id="312ea-196">UK South 2</span></span> | <span data-ttu-id="312ea-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="312ea-197">13.87.34.7</span></span> | |
| <span data-ttu-id="312ea-198">Regno Unito occidentale</span><span class="sxs-lookup"><span data-stu-id="312ea-198">UK West</span></span> | <span data-ttu-id="312ea-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="312ea-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="312ea-200">Stati Uniti centro-occidentali</span><span class="sxs-lookup"><span data-stu-id="312ea-200">West Central US</span></span> | <span data-ttu-id="312ea-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="312ea-201">13.78.145.25</span></span> | |
| <span data-ttu-id="312ea-202">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="312ea-202">West Europe</span></span> | <span data-ttu-id="312ea-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="312ea-203">191.237.232.75</span></span> | <span data-ttu-id="312ea-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="312ea-204">40.68.37.158</span></span> |
| <span data-ttu-id="312ea-205">Stati Uniti occidentali 1</span><span class="sxs-lookup"><span data-stu-id="312ea-205">West US 1</span></span> | <span data-ttu-id="312ea-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="312ea-206">23.99.34.75</span></span> | <span data-ttu-id="312ea-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="312ea-207">104.42.238.205</span></span> |
| <span data-ttu-id="312ea-208">Stati Uniti occidentali 2</span><span class="sxs-lookup"><span data-stu-id="312ea-208">West US 2</span></span> | <span data-ttu-id="312ea-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="312ea-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="312ea-210">Modificare il criterio di connessione del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="312ea-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="312ea-211">hello toochange criteri di connessione di Database SQL di Azure per un server di Database SQL di Azure, utilizzare hello [API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="312ea-211">toochange hello Azure SQL Database connection policy for an Azure SQL Database server, use hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="312ea-212">Se il criterio di connessione è stato impostato troppo**Proxy**, tutto il flusso dei pacchetti tramite il gateway di Database SQL di Azure hello di rete.</span><span class="sxs-lookup"><span data-stu-id="312ea-212">If your connection policy is set too**Proxy**, all network packets flow via hello Azure SQL Database gateway.</span></span> <span data-ttu-id="312ea-213">Per questa impostazione, è necessario IP del gateway tooallow tooonly in uscita hello Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="312ea-213">For this setting, you need tooallow outbound tooonly hello Azure SQL Database gateway IP.</span></span> <span data-ttu-id="312ea-214">L'uso dell'impostazione **proxy** ha una latenza maggiore rispetto all'impostazione **reindirizzamento**.</span><span class="sxs-lookup"><span data-stu-id="312ea-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="312ea-215">Se i criteri di connessione sono l'impostazione **reindirizzare**, tutti i pacchetti di rete direttamente flusso toohello middleware proxy.</span><span class="sxs-lookup"><span data-stu-id="312ea-215">If your connection policy is setting **Redirect**, all network packets flow directly toohello middleware proxy.</span></span> <span data-ttu-id="312ea-216">Per questa impostazione, è necessario tooallow in uscita toomultiple gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="312ea-216">For this setting, you need tooallow outbound toomultiple IPs.</span></span> 

## <a name="script-toochange-connection-settings"></a><span data-ttu-id="312ea-217">Impostazioni di connessione toochange script</span><span class="sxs-lookup"><span data-stu-id="312ea-217">Script toochange connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="312ea-218">Questo script richiede hello [modulo Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="312ea-218">This script requires hello [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="312ea-219">Hello lo script di PowerShell seguente viene illustrato come toochange hello criteri di connessione.</span><span class="sxs-lookup"><span data-stu-id="312ea-219">hello following PowerShell script shows how toochange hello connection policy.</span></span>

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="312ea-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="312ea-220">Next steps</span></span>

- <span data-ttu-id="312ea-221">Per informazioni su come toochange hello criteri di connessione di Database SQL di Azure per un server di Database SQL di Azure, vedere [Create o criteri di connessione Server di aggiornamento tramite API REST di hello](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="312ea-221">For information on how toochange hello Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="312ea-222">Per informazioni sul comportamento della connessione al database SQL di Azure per i client che usano ADO.NET 4.5 o versione successiva, vedere [Porte successive alla 1433 per ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="312ea-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="312ea-223">Per una panoramica generale sullo sviluppo di applicazioni, vedere [Panoramica dello sviluppo di applicazioni del database SQL](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="312ea-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
