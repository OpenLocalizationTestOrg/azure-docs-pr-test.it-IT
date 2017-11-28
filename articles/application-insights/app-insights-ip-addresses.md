---
title: indirizzi aaaIP utilizzati da Application Insights | Documenti Microsoft
description: Eccezioni del firewall del server necessarie per Application Insights
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 8/11/2017
ms.author: bwren
ms.openlocfilehash: 2c101b8da2ba9594fbff607f4f7551cda80c3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="2f180-103">Indirizzi IP usati da Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f180-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="2f180-104">Hello [Azure Application Insights](app-insights-overview.md) servizio utilizza un numero di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="2f180-104">hello [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="2f180-105">Potrebbe essere necessario tooknow questi indirizzi se hello app che si esegue il monitoraggio si trova dietro un firewall.</span><span class="sxs-lookup"><span data-stu-id="2f180-105">You might need tooknow these addresses if hello app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="2f180-106">Sebbene questi indirizzi sono statici, è possibile che sarà necessario toochange di tootime ora.</span><span class="sxs-lookup"><span data-stu-id="2f180-106">Although these addresses are static, it's possible that we will need toochange them from time tootime.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="2f180-107">Porte in uscita</span><span class="sxs-lookup"><span data-stu-id="2f180-107">Outgoing ports</span></span>
<span data-ttu-id="2f180-108">È necessario tooopen alcune porte in uscita in hello tooallow tramite firewall del server Application Insights SDK e/o il portale di monitoraggio stato toosend dati toohello:</span><span class="sxs-lookup"><span data-stu-id="2f180-108">You need tooopen some outgoing ports in your server's firewall tooallow hello Application Insights SDK and/or Status Monitor toosend data toohello portal:</span></span>

| <span data-ttu-id="2f180-109">Scopo</span><span class="sxs-lookup"><span data-stu-id="2f180-109">Purpose</span></span> | <span data-ttu-id="2f180-110">URL</span><span class="sxs-lookup"><span data-stu-id="2f180-110">URL</span></span> | <span data-ttu-id="2f180-111">IP</span><span class="sxs-lookup"><span data-stu-id="2f180-111">IP</span></span> | <span data-ttu-id="2f180-112">Porte</span><span class="sxs-lookup"><span data-stu-id="2f180-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f180-113">Telemetria</span><span class="sxs-lookup"><span data-stu-id="2f180-113">Telemetry</span></span> |<span data-ttu-id="2f180-114">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="2f180-115">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="2f180-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="2f180-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="2f180-116">40.114.241.141</span></span><br/><span data-ttu-id="2f180-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="2f180-117">104.45.136.42</span></span><br/><span data-ttu-id="2f180-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="2f180-118">40.84.189.107</span></span><br/><span data-ttu-id="2f180-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="2f180-119">168.63.242.221</span></span><br/><span data-ttu-id="2f180-120">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="2f180-120">52.167.221.184</span></span><br/><span data-ttu-id="2f180-121">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="2f180-121">52.169.64.244</span></span> |<span data-ttu-id="2f180-122">443</span><span class="sxs-lookup"><span data-stu-id="2f180-122">443</span></span> |
| <span data-ttu-id="2f180-123">Flusso di metriche live</span><span class="sxs-lookup"><span data-stu-id="2f180-123">Live Metrics Stream</span></span> |<span data-ttu-id="2f180-124">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-124">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="2f180-125">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="2f180-125">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="2f180-126">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="2f180-126">23.96.28.38</span></span><br/><span data-ttu-id="2f180-127">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="2f180-127">13.92.40.198</span></span> |<span data-ttu-id="2f180-128">443</span><span class="sxs-lookup"><span data-stu-id="2f180-128">443</span></span> |
| <span data-ttu-id="2f180-129">Telemetria interna</span><span class="sxs-lookup"><span data-stu-id="2f180-129">Internal Telemetry</span></span> |<span data-ttu-id="2f180-130">breeze.aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="2f180-130">breeze.aimon.applicationinsights.io</span></span> |<span data-ttu-id="2f180-131">52.161.11.71</span><span class="sxs-lookup"><span data-stu-id="2f180-131">52.161.11.71</span></span> |<span data-ttu-id="2f180-132">443</span><span class="sxs-lookup"><span data-stu-id="2f180-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="2f180-133">Monitoraggio stato</span><span class="sxs-lookup"><span data-stu-id="2f180-133">Status Monitor</span></span>
<span data-ttu-id="2f180-134">Configurazione di Status Monitor: necessaria solo quando si apportano modifiche.</span><span class="sxs-lookup"><span data-stu-id="2f180-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="2f180-135">Scopo</span><span class="sxs-lookup"><span data-stu-id="2f180-135">Purpose</span></span> | <span data-ttu-id="2f180-136">URL</span><span class="sxs-lookup"><span data-stu-id="2f180-136">URL</span></span> | <span data-ttu-id="2f180-137">IP</span><span class="sxs-lookup"><span data-stu-id="2f180-137">IP</span></span> | <span data-ttu-id="2f180-138">Porte</span><span class="sxs-lookup"><span data-stu-id="2f180-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f180-139">Configurazione</span><span class="sxs-lookup"><span data-stu-id="2f180-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="2f180-140">Configurazione</span><span class="sxs-lookup"><span data-stu-id="2f180-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="2f180-141">Configurazione</span><span class="sxs-lookup"><span data-stu-id="2f180-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="2f180-142">Configurazione</span><span class="sxs-lookup"><span data-stu-id="2f180-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="2f180-143">Configurazione</span><span class="sxs-lookup"><span data-stu-id="2f180-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="2f180-144">Configurazione</span><span class="sxs-lookup"><span data-stu-id="2f180-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="2f180-145">Configurazione</span><span class="sxs-lookup"><span data-stu-id="2f180-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="2f180-146">Installare</span><span class="sxs-lookup"><span data-stu-id="2f180-146">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="2f180-147">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="2f180-147">HockeyApp</span></span>
| <span data-ttu-id="2f180-148">Scopo</span><span class="sxs-lookup"><span data-stu-id="2f180-148">Purpose</span></span> | <span data-ttu-id="2f180-149">URL</span><span class="sxs-lookup"><span data-stu-id="2f180-149">URL</span></span> | <span data-ttu-id="2f180-150">IP</span><span class="sxs-lookup"><span data-stu-id="2f180-150">IP</span></span> | <span data-ttu-id="2f180-151">Porte</span><span class="sxs-lookup"><span data-stu-id="2f180-151">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f180-152">Dati sugli arresti anomali</span><span class="sxs-lookup"><span data-stu-id="2f180-152">Crash data</span></span> |<span data-ttu-id="2f180-153">gate.hockeyapp.net</span><span class="sxs-lookup"><span data-stu-id="2f180-153">gate.hockeyapp.net</span></span> |<span data-ttu-id="2f180-154">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="2f180-154">104.45.136.42</span></span> |<span data-ttu-id="2f180-155">80, 443</span><span class="sxs-lookup"><span data-stu-id="2f180-155">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="2f180-156">Test della disponibilità</span><span class="sxs-lookup"><span data-stu-id="2f180-156">Availability tests</span></span>
<span data-ttu-id="2f180-157">Si tratta di hello elenco di indirizzi da cui [test web disponibilità](app-insights-monitor-web-app-availability.md) vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="2f180-157">This is hello list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="2f180-158">Se si desidera test web toorun nella tua app, ma il server web è limitato tooserving client specifici, sarà necessario toopermit il traffico in ingresso dai nostri server di test di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="2f180-158">If you want toorun web tests on your app, but your web server is restricted tooserving specific clients, then you will have toopermit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="2f180-159">Aprire le porte 80 (http) e 443 (https) per il traffico in ingresso da questi indirizzi (gli indirizzi IP sono raggruppati per posizione):</span><span class="sxs-lookup"><span data-stu-id="2f180-159">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a><span data-ttu-id="2f180-160">API di accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="2f180-160">Data access API</span></span>
| <span data-ttu-id="2f180-161">Scopo</span><span class="sxs-lookup"><span data-stu-id="2f180-161">Purpose</span></span> | <span data-ttu-id="2f180-162">URI</span><span class="sxs-lookup"><span data-stu-id="2f180-162">URI</span></span> | <span data-ttu-id="2f180-163">IP</span><span class="sxs-lookup"><span data-stu-id="2f180-163">IP</span></span> | <span data-ttu-id="2f180-164">Porte</span><span class="sxs-lookup"><span data-stu-id="2f180-164">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f180-165">API</span><span class="sxs-lookup"><span data-stu-id="2f180-165">API</span></span> |<span data-ttu-id="2f180-166">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="2f180-166">api.applicationinsights.io</span></span><br/><span data-ttu-id="2f180-167">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="2f180-167">api1.applicationinsights.io</span></span><br/><span data-ttu-id="2f180-168">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="2f180-168">api2.applicationinsights.io</span></span><br/><span data-ttu-id="2f180-169">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="2f180-169">api3.applicationinsights.io</span></span><br/><span data-ttu-id="2f180-170">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="2f180-170">api4.applicationinsights.io</span></span><br/><span data-ttu-id="2f180-171">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="2f180-171">api5.applicationinsights.io</span></span> |<span data-ttu-id="2f180-172">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="2f180-172">13.82.26.252</span></span><br/><span data-ttu-id="2f180-173">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="2f180-173">40.76.213.73</span></span> |<span data-ttu-id="2f180-174">80,443</span><span class="sxs-lookup"><span data-stu-id="2f180-174">80,443</span></span> |
| <span data-ttu-id="2f180-175">Documentazione API</span><span class="sxs-lookup"><span data-stu-id="2f180-175">API docs</span></span> |<span data-ttu-id="2f180-176">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="2f180-176">dev.applicationinsights.io</span></span><br/><span data-ttu-id="2f180-177">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="2f180-177">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="2f180-178">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-178">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="2f180-179">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="2f180-179">www.applicationinsights.io</span></span><br/><span data-ttu-id="2f180-180">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="2f180-180">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="2f180-181">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-181">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="2f180-182">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="2f180-182">13.82.24.149</span></span><br/><span data-ttu-id="2f180-183">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="2f180-183">40.114.82.10</span></span> |<span data-ttu-id="2f180-184">80,443</span><span class="sxs-lookup"><span data-stu-id="2f180-184">80,443</span></span> |
| <span data-ttu-id="2f180-185">API interna</span><span class="sxs-lookup"><span data-stu-id="2f180-185">Internal API</span></span> |<span data-ttu-id="2f180-186">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-186">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="2f180-187">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-187">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="2f180-188">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-188">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="2f180-189">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-189">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="2f180-190">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-190">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="2f180-191">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-191">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="2f180-192">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-192">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="2f180-193">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-193">dynamic</span></span>|<span data-ttu-id="2f180-194">443</span><span class="sxs-lookup"><span data-stu-id="2f180-194">443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="2f180-195">Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f180-195">Application Insights Analytics</span></span>

| <span data-ttu-id="2f180-196">Scopo</span><span class="sxs-lookup"><span data-stu-id="2f180-196">Purpose</span></span> | <span data-ttu-id="2f180-197">URI</span><span class="sxs-lookup"><span data-stu-id="2f180-197">URI</span></span> | <span data-ttu-id="2f180-198">IP</span><span class="sxs-lookup"><span data-stu-id="2f180-198">IP</span></span> | <span data-ttu-id="2f180-199">Porte</span><span class="sxs-lookup"><span data-stu-id="2f180-199">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f180-200">Portale di Analisi</span><span class="sxs-lookup"><span data-stu-id="2f180-200">Analytics Portal</span></span> | <span data-ttu-id="2f180-201">analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="2f180-201">analytics.applicationinsights.io</span></span> | <span data-ttu-id="2f180-202">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-202">dynamic</span></span> | <span data-ttu-id="2f180-203">80,443</span><span class="sxs-lookup"><span data-stu-id="2f180-203">80,443</span></span> |
| <span data-ttu-id="2f180-204">RETE CDN</span><span class="sxs-lookup"><span data-stu-id="2f180-204">CDN</span></span> | <span data-ttu-id="2f180-205">applicationanalytics.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="2f180-205">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="2f180-206">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-206">dynamic</span></span> | <span data-ttu-id="2f180-207">80,443</span><span class="sxs-lookup"><span data-stu-id="2f180-207">80,443</span></span> |
| <span data-ttu-id="2f180-208">Contenuti multimediali e rete CDN</span><span class="sxs-lookup"><span data-stu-id="2f180-208">Media CDN</span></span> | <span data-ttu-id="2f180-209">applicationanalyticsmedia.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="2f180-209">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="2f180-210">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-210">dynamic</span></span> | <span data-ttu-id="2f180-211">80,443</span><span class="sxs-lookup"><span data-stu-id="2f180-211">80,443</span></span> |

<span data-ttu-id="2f180-212">Nota: il dominio *.applicationinsights.io è di proprietà del team Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2f180-212">Note: *.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="2f180-213">Estensione del portale di Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f180-213">Application Insights Azure Portal Extension</span></span>

| <span data-ttu-id="2f180-214">Scopo</span><span class="sxs-lookup"><span data-stu-id="2f180-214">Purpose</span></span> | <span data-ttu-id="2f180-215">URI</span><span class="sxs-lookup"><span data-stu-id="2f180-215">URI</span></span> | <span data-ttu-id="2f180-216">IP</span><span class="sxs-lookup"><span data-stu-id="2f180-216">IP</span></span> | <span data-ttu-id="2f180-217">Porte</span><span class="sxs-lookup"><span data-stu-id="2f180-217">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f180-218">Estensione Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f180-218">Application Insights Extension</span></span> | <span data-ttu-id="2f180-219">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-219">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="2f180-220">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-220">dynamic</span></span> | <span data-ttu-id="2f180-221">80,443</span><span class="sxs-lookup"><span data-stu-id="2f180-221">80,443</span></span> |
| <span data-ttu-id="2f180-222">Rete CDN estensione Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f180-222">Application Insights Extension CDN</span></span> | <span data-ttu-id="2f180-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-223">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="2f180-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="2f180-224">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="2f180-225">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="2f180-225">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="2f180-226">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-226">dynamic</span></span> | <span data-ttu-id="2f180-227">80,443</span><span class="sxs-lookup"><span data-stu-id="2f180-227">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="2f180-228">Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="2f180-228">Application Insights SDKs</span></span>

| <span data-ttu-id="2f180-229">Scopo</span><span class="sxs-lookup"><span data-stu-id="2f180-229">Purpose</span></span> | <span data-ttu-id="2f180-230">URI</span><span class="sxs-lookup"><span data-stu-id="2f180-230">URI</span></span> | <span data-ttu-id="2f180-231">IP</span><span class="sxs-lookup"><span data-stu-id="2f180-231">IP</span></span> | <span data-ttu-id="2f180-232">Porte</span><span class="sxs-lookup"><span data-stu-id="2f180-232">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f180-233">Rete CDN Application Insights JS SDK</span><span class="sxs-lookup"><span data-stu-id="2f180-233">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="2f180-234">az416426.vo.msecnd.net</span><span class="sxs-lookup"><span data-stu-id="2f180-234">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="2f180-235">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-235">dynamic</span></span> | <span data-ttu-id="2f180-236">80,443</span><span class="sxs-lookup"><span data-stu-id="2f180-236">80,443</span></span> |
| <span data-ttu-id="2f180-237">Application Insights Java SDK</span><span class="sxs-lookup"><span data-stu-id="2f180-237">Application Insights Java SDK</span></span> | <span data-ttu-id="2f180-238">aijavasdk.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="2f180-238">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="2f180-239">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-239">dynamic</span></span> | <span data-ttu-id="2f180-240">80,443</span><span class="sxs-lookup"><span data-stu-id="2f180-240">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="2f180-241">Profiler</span><span class="sxs-lookup"><span data-stu-id="2f180-241">Profiler</span></span>

| <span data-ttu-id="2f180-242">Scopo</span><span class="sxs-lookup"><span data-stu-id="2f180-242">Purpose</span></span> | <span data-ttu-id="2f180-243">URI</span><span class="sxs-lookup"><span data-stu-id="2f180-243">URI</span></span> | <span data-ttu-id="2f180-244">IP</span><span class="sxs-lookup"><span data-stu-id="2f180-244">IP</span></span> | <span data-ttu-id="2f180-245">Porte</span><span class="sxs-lookup"><span data-stu-id="2f180-245">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f180-246">Agente</span><span class="sxs-lookup"><span data-stu-id="2f180-246">Agent</span></span> | <span data-ttu-id="2f180-247">agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="2f180-247">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="2f180-248">*.agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="2f180-248">*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="2f180-249">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-249">dynamic</span></span> | <span data-ttu-id="2f180-250">443</span><span class="sxs-lookup"><span data-stu-id="2f180-250">443</span></span>
| <span data-ttu-id="2f180-251">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2f180-251">Portal</span></span> | <span data-ttu-id="2f180-252">gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="2f180-252">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="2f180-253">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-253">dynamic</span></span> | <span data-ttu-id="2f180-254">443</span><span class="sxs-lookup"><span data-stu-id="2f180-254">443</span></span>
| <span data-ttu-id="2f180-255">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="2f180-255">Storage</span></span> | <span data-ttu-id="2f180-256">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="2f180-256">*.core.windows.net</span></span> | <span data-ttu-id="2f180-257">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-257">dynamic</span></span> | <span data-ttu-id="2f180-258">443</span><span class="sxs-lookup"><span data-stu-id="2f180-258">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="2f180-259">Debugger di snapshot</span><span class="sxs-lookup"><span data-stu-id="2f180-259">Snapshot Debugger</span></span>

| <span data-ttu-id="2f180-260">Scopo</span><span class="sxs-lookup"><span data-stu-id="2f180-260">Purpose</span></span> | <span data-ttu-id="2f180-261">URI</span><span class="sxs-lookup"><span data-stu-id="2f180-261">URI</span></span> | <span data-ttu-id="2f180-262">IP</span><span class="sxs-lookup"><span data-stu-id="2f180-262">IP</span></span> | <span data-ttu-id="2f180-263">Porte</span><span class="sxs-lookup"><span data-stu-id="2f180-263">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f180-264">Agente</span><span class="sxs-lookup"><span data-stu-id="2f180-264">Agent</span></span> | <span data-ttu-id="2f180-265">ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="2f180-265">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="2f180-266">*.ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="2f180-266">*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="2f180-267">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-267">dynamic</span></span> | <span data-ttu-id="2f180-268">443</span><span class="sxs-lookup"><span data-stu-id="2f180-268">443</span></span>
| <span data-ttu-id="2f180-269">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2f180-269">Portal</span></span> | <span data-ttu-id="2f180-270">ppe.gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="2f180-270">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="2f180-271">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-271">dynamic</span></span> | <span data-ttu-id="2f180-272">443</span><span class="sxs-lookup"><span data-stu-id="2f180-272">443</span></span>
| <span data-ttu-id="2f180-273">Archiviazione</span><span class="sxs-lookup"><span data-stu-id="2f180-273">Storage</span></span> | <span data-ttu-id="2f180-274">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="2f180-274">*.core.windows.net</span></span> | <span data-ttu-id="2f180-275">dinamico</span><span class="sxs-lookup"><span data-stu-id="2f180-275">dynamic</span></span> | <span data-ttu-id="2f180-276">443</span><span class="sxs-lookup"><span data-stu-id="2f180-276">443</span></span>
