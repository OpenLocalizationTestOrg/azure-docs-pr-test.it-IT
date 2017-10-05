---
title: Sicurezza dei dati della soluzione Sicurezza e controllo di Operations Management Suite | Documentazione Microsoft
description: Questo documento illustra il modo in cui i dati vengono gestiti e protetti nella soluzione Sicurezza e controllo di Operations Management Suite.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 3b6327b1f5150f32afd71639f32c55d823f1d1f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="1e0ef-103">Sicurezza dei dati della soluzione Sicurezza e controllo di Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="1e0ef-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="1e0ef-104">Per aiutare i clienti a evitare, rilevare e rispondere alle minacce, la [Soluzione Sicurezza e controllo di Operations Management Suite (OMS)](operations-management-suite-overview.md) raccoglie ed elabora i dati sulle risorse, tra cui:</span><span class="sxs-lookup"><span data-stu-id="1e0ef-104">To help customers prevent, detect, and respond to threats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="1e0ef-105">Registri eventi sicurezza</span><span class="sxs-lookup"><span data-stu-id="1e0ef-105">Security event log</span></span>
* <span data-ttu-id="1e0ef-106">Tracciamento degli eventi di Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="1e0ef-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="1e0ef-107">Eventi di controllo AppLocker</span><span class="sxs-lookup"><span data-stu-id="1e0ef-107">AppLocker auditing events</span></span>
* <span data-ttu-id="1e0ef-108">Log di Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="1e0ef-108">Windows Firewall log</span></span>
* <span data-ttu-id="1e0ef-109">Eventi di Advanced Threat Analytics</span><span class="sxs-lookup"><span data-stu-id="1e0ef-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="1e0ef-110">Risultati della valutazione baseline</span><span class="sxs-lookup"><span data-stu-id="1e0ef-110">Results of baseline assessment</span></span>
* <span data-ttu-id="1e0ef-111">Risultati di Antimalware Assessment</span><span class="sxs-lookup"><span data-stu-id="1e0ef-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="1e0ef-112">Risultati della valutazione di aggiornamenti/patch</span><span class="sxs-lookup"><span data-stu-id="1e0ef-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="1e0ef-113">Flussi di Syslog abilitati esplicitamente nell'agente</span><span class="sxs-lookup"><span data-stu-id="1e0ef-113">Syslogs streams that are explicitly enabled on the agent</span></span>

<span data-ttu-id="1e0ef-114">Microsoft è fortemente impegnata nella protezione della privacy e della sicurezza dei dati.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-114">We make strong commitments to protect the privacy and security of this data.</span></span> <span data-ttu-id="1e0ef-115">Microsoft è conforme alle più rigorose linee guida sulla sicurezza e sulla conformità in tutte le fasi, dalla codifica all'esecuzione di un servizio.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-115">Microsoft adheres to strict compliance and security guidelines—from coding to operating a service.</span></span>
<span data-ttu-id="1e0ef-116">Questo articolo illustra il modo in cui i dati vengono gestiti e protetti nella soluzione Sicurezza e controllo di OMS.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="1e0ef-117">Origini dati</span><span class="sxs-lookup"><span data-stu-id="1e0ef-117">Data sources</span></span>
<span data-ttu-id="1e0ef-118">La soluzione Sicurezza e controllo di OMS analizza i dati provenienti dalle macchine virtuali e dai computer fisici in cui è installato l'agente OMS.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where the OMS Agent is installed.</span></span> <span data-ttu-id="1e0ef-119">La soluzione Sicurezza e controllo di OMS può raccogliere informazioni di configurazione sugli eventi di sicurezza, ad esempio gli eventi Windows, i log di controllo, i log di IIS e i messaggi syslog.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="1e0ef-120">Esempi di tali dati sono: tipo e versione del sistema operativo, processi in esecuzione, nome computer, indirizzi IP, utente connesso e ID tenant.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="1e0ef-121">Protezione dati</span><span class="sxs-lookup"><span data-stu-id="1e0ef-121">Data protection</span></span>
<span data-ttu-id="1e0ef-122">**Separazione dei dati:**i dati vengono mantenuti separati logicamente in ogni componente del servizio.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-122">**Data segregation**: Data is kept logically separate on each component throughout the service.</span></span> <span data-ttu-id="1e0ef-123">Tutti i dati vengono contrassegnati in base all'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-123">All data is tagged per organization.</span></span> <span data-ttu-id="1e0ef-124">Tale contrassegno persiste per tutto il ciclo di vita dei dati e viene applicato a ogni livello del servizio.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-124">This tagging persists throughout the data lifecycle, and it is enforced at each layer of the service.</span></span> 

<span data-ttu-id="1e0ef-125">**Accesso ai dati**: per fornire raccomandazioni sulla sicurezza e analizzare le potenziali minacce alla sicurezza, il personale Microsoft può accedere alle informazioni raccolte o analizzate dai servizi, inclusi i file di dump di arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-125">**Data access**: To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="1e0ef-126">Microsoft rispetta le [condizioni di Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) e l'[Informativa sulla privacy](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), in cui è specificato che Microsoft non userà i dati del cliente o ne ricaverà informazioni per scopi pubblicitari o commerciali simili.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-126">We adhere to the [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="1e0ef-127">Per fornire raccomandazioni sulla sicurezza e analizzare le potenziali minacce alla sicurezza, il personale Microsoft può accedere alle informazioni raccolte o analizzate dai servizi, inclusi i file di dump di arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-127">To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="1e0ef-128">Microsoft userà i dati dei clienti solo se necessari per fornire i servizi di Azure, incluse le finalità compatibili con la fornitura di tali servizi.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-128">We only use Customer Data as needed to provide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="1e0ef-129">L'utente mantiene tutti i diritti sui propri dati.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-129">You retain all rights to your own data.</span></span>

<span data-ttu-id="1e0ef-130">**Uso dei dati**: Microsoft usa modelli e intelligence per le minacce trovati in più tenant per migliorare le funzionalità di prevenzione e rilevamento, in base alle garanzie relative alla privacy descritte nell'[Informativa sulla privacy](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e0ef-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants to enhance our prevention and detection capabilities; we do so in accordance with the privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="1e0ef-131">La posizione dei dati viene configurata a livello di area di lavoro di OMS, durante la creazione dell'area di lavoro, che fa parte del processo di configurazione iniziale della soluzione Sicurezza e controllo di OMS.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-131">Data location is configured at the OMS workspace level, during the workspace creation, which is part of the initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="1e0ef-132">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1e0ef-132">See also</span></span>
<span data-ttu-id="1e0ef-133">Questo documento illustra in che modo vengono gestiti e protetti i dati in OMS.</span><span class="sxs-lookup"><span data-stu-id="1e0ef-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="1e0ef-134">Per altre informazioni sulla soluzione Sicurezza e controllo di OMS, vedere:</span><span class="sxs-lookup"><span data-stu-id="1e0ef-134">To learn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="1e0ef-135">Panoramica di Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="1e0ef-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="1e0ef-136">Monitoraggio e gestione degli avvisi di sicurezza nella soluzione Operations Management Suite per la sicurezza e il controllo</span><span class="sxs-lookup"><span data-stu-id="1e0ef-136">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="1e0ef-137">Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo</span><span class="sxs-lookup"><span data-stu-id="1e0ef-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

