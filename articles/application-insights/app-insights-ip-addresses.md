---
title: Indirizzi IP usati da Application Insights e Log Analytics | Microsoft Docs
description: Eccezioni del firewall del server necessarie per Application Insights
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/13/2017
ms.author: mbullwin
ms.openlocfilehash: afdef7898ef68930ef702ddf67baaadae9360236
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/11/2018
---
# <a name="ip-addresses-used-by-application-insights-and-log-analytics"></a>Indirizzi IP usati da Application Insights e Log Analytics
Il servizio [Azure Application Insights](app-insights-overview.md) usa diversi indirizzi IP. Potrebbe essere necessario conoscere questi indirizzi se l'app che si sta monitorando è ospitata dietro un firewall.

> [!NOTE]
> Anche se questi indirizzi sono statici, a volte potrebbe essere necessari modificarli.
> 
> 

## <a name="outgoing-ports"></a>Porte in uscita
È necessario aprire alcune porte in uscita nel firewall del server per consentire ad Application Insights SDK e/o a Status Monitor di inviare dati al portale:

| Scopo | URL | IP | Porte |
| --- | --- | --- | --- |
| Telemetria |dc.services.visualstudio.com<br/>dc.applicationinsights.microsoft.com |40.114.241.141<br/>104.45.136.42<br/>40.84.189.107<br/>168.63.242.221<br/>52.167.221.184<br/>52.169.64.244 |443 |
| Flusso di metriche live |dc.services.visualstudio.com<br/>dc.applicationinsights.microsoft.com |23.96.28.38<br/>13.92.40.198 |443 |
| Telemetria interna |breeze.aimon.applicationinsights.io |52.161.11.71 |443 |

## <a name="status-monitor"></a>Monitoraggio stato
Configurazione di Status Monitor: necessaria solo quando si apportano modifiche.

| Scopo | URL | IP | Porte |
| --- | --- | --- | --- |
| Configurazione |`management.core.windows.net` | |`443` |
| Configurazione |`management.azure.com` | |`443` |
| Configurazione |`login.windows.net` | |`443` |
| Configurazione |`login.microsoftonline.com` | |`443` |
| Configurazione |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| Configurazione |`auth.gfx.ms` | |`443` |
| Configurazione |`login.live.com` | |`443` |
| Installazione |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a>HockeyApp
| Scopo | URL | IP | Porte |
| --- | --- | --- | --- |
| Dati sugli arresti anomali |gate.hockeyapp.net |104.45.136.42 |80, 443 |

## <a name="availability-tests"></a>Test della disponibilità
Questo è l'elenco di indirizzi da cui vengono eseguiti i [test Web della disponibilità](app-insights-monitor-web-app-availability.md) . Se si vogliono eseguire test Web sull'app, ma il server Web è limitato alla fornitura di servizi a client specifici, è necessario consentire il traffico in ingresso dai server di test della disponibilità.

Aprire le porte 80 (http) e 443 (https) per il traffico in ingresso da questi indirizzi (gli indirizzi IP sono raggruppati per posizione):

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
52.136.140.221
52.136.140.222
52.136.140.223
52.136.140.226
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
52.143.140.242 
52.143.140.246
52.143.140.247
52.143.140.249
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
51.140.79.229
51.140.84.172
51.140.87.211
51.140.105.74
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
GB : United Kingdom
51.141.25.219
51.141.32.101
51.141.35.167
51.141.54.177
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
52.165.130.58
52.173.142.229
52.173.147.190
52.173.17.41
52.173.204.247
52.173.244.190
52.173.36.222
52.176.1.226
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

## <a name="application-insights-api"></a>API Application Insights
| Scopo | URI | IP | Porte |
| --- | --- | --- | --- |
| API |api.applicationinsights.io<br/>api1.applicationinsights.io<br/>api2.applicationinsights.io<br/>api3.applicationinsights.io<br/>api4.applicationinsights.io<br/>api5.applicationinsights.io |13.82.26.252<br/>40.76.213.73 |80,443 |
| Documentazione API |dev.applicationinsights.io<br/>dev.applicationinsights.microsoft.com<br/>dev.aisvc.visualstudio.com<br/>www.applicationinsights.io<br/>www.applicationinsights.microsoft.com<br/>www.aisvc.visualstudio.com |13.82.24.149<br/>40.114.82.10 |80,443 |
| API interna |aigs.aisvc.visualstudio.com<br/>aigs1.aisvc.visualstudio.com<br/>aigs2.aisvc.visualstudio.com<br/>aigs3.aisvc.visualstudio.com<br/>aigs4.aisvc.visualstudio.com<br/>aigs5.aisvc.visualstudio.com<br/>aigs6.aisvc.visualstudio.com |dinamico|443 |

## <a name="log-analytics-api"></a>API di Log Analytics
| Scopo | URI | IP | Porte |
| --- | --- | --- | --- |
| API |api.loganalytics.io<br/>*.api.loganalytics.io |dinamico |80,443 |
| Documentazione API |dev.loganalytics.io<br/>docs.loganalytics.io<br/>www.loganalytics.io |dinamico |80,443 |

## <a name="application-insights-analytics"></a>Analytics in Application Insights

| Scopo | URI | IP | Porte |
| --- | --- | --- | --- |
| Portale di Analisi | analytics.applicationinsights.io | dinamico | 80,443 |
| RETE CDN | applicationanalytics.azureedge.net | dinamico | 80,443 |
| Contenuti multimediali e rete CDN | applicationanalyticsmedia.azureedge.net | dinamico | 80,443 |

Nota: il dominio *.applicationinsights.io è di proprietà del team Application Insights.

## <a name="log-analytics-portal"></a>Portale di Log Analytics

| Scopo | URI | IP | Porte |
| --- | --- | --- | --- |
| Portale | portal.loganalytics.io | dinamico | 80,443 |
| RETE CDN | applicationanalytics.azureedge.net | dinamico | 80,443 |

Nota: il dominio *.loganalytics.io è di proprietà del team di Log Analytics.

## <a name="application-insights-azure-portal-extension"></a>Estensione del portale di Azure Application Insights

| Scopo | URI | IP | Porte |
| --- | --- | --- | --- |
| Estensione Application Insights | stamp2.app.insightsportal.visualstudio.com | dinamico | 80,443 |
| Rete CDN estensione Application Insights | insightsportal-prod2-cdn.aisvc.visualstudio.com<br/>insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com<br/>insightsportal-cdn-aimon.applicationinsights.io | dinamico | 80,443 |

## <a name="application-insights-sdks"></a>Application Insights SDK

| Scopo | URI | IP | Porte |
| --- | --- | --- | --- |
| Rete CDN Application Insights JS SDK | az416426.vo.msecnd.net | dinamico | 80,443 |
| Application Insights Java SDK | aijavasdk.blob.core.windows.net | dinamico | 80,443 |

## <a name="profiler"></a>Profiler

| Scopo | URI | IP | Porte |
| --- | --- | --- | --- |
| Agente | agent.azureserviceprofiler.net<br/>*.agent.azureserviceprofiler.net | 51.143.96.206<br/>51.143.98.157<br/>52.161.8.88<br/>52.161.29.225<br/>52.178.149.106<br/>52.178.147.66<br/>40.68.32.221<br/>104.40.217.71 | 443
| Portale | gateway.azureserviceprofiler.net | dinamico | 443
| Archiviazione | *.core.windows.net | dinamico | 443

## <a name="snapshot-debugger"></a>Debugger di snapshot

| Scopo | URI | IP | Porte |
| --- | --- | --- | --- |
| Agente | ppe.azureserviceprofiler.net<br/>*.ppe.azureserviceprofiler.net | 23.101.68.84<br/>52.174.44.101<br/>52.250.121.195<br/>51.143.88.187<br/> | 443
| Portale | ppe.gateway.azureserviceprofiler.net | dinamico | 443
| Archiviazione | *.core.windows.net | dinamico | 443
