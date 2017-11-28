---
title: aaaOperations gestione gruppo di sicurezza e protezione dei dati di controllo soluzione | Documenti Microsoft
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
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="f1a55-103">Sicurezza dei dati della soluzione Sicurezza e controllo di Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="f1a55-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="f1a55-104">i clienti toohelp impedire, rilevare e rispondere toothreats, [soluzione di controllo e protezione di Operations Management Suite (OMS)](operations-management-suite-overview.md) raccoglie ed elabora i dati sulle risorse, che includono:</span><span class="sxs-lookup"><span data-stu-id="f1a55-104">toohelp customers prevent, detect, and respond toothreats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="f1a55-105">Registri eventi sicurezza</span><span class="sxs-lookup"><span data-stu-id="f1a55-105">Security event log</span></span>
* <span data-ttu-id="f1a55-106">Tracciamento degli eventi di Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="f1a55-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="f1a55-107">Eventi di controllo AppLocker</span><span class="sxs-lookup"><span data-stu-id="f1a55-107">AppLocker auditing events</span></span>
* <span data-ttu-id="f1a55-108">Log di Windows Firewall</span><span class="sxs-lookup"><span data-stu-id="f1a55-108">Windows Firewall log</span></span>
* <span data-ttu-id="f1a55-109">Eventi di Advanced Threat Analytics</span><span class="sxs-lookup"><span data-stu-id="f1a55-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="f1a55-110">Risultati della valutazione baseline</span><span class="sxs-lookup"><span data-stu-id="f1a55-110">Results of baseline assessment</span></span>
* <span data-ttu-id="f1a55-111">Risultati di Antimalware Assessment</span><span class="sxs-lookup"><span data-stu-id="f1a55-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="f1a55-112">Risultati della valutazione di aggiornamenti/patch</span><span class="sxs-lookup"><span data-stu-id="f1a55-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="f1a55-113">Flussi i registri di sistema che sono abilitati in modo esplicito sull'agente hello</span><span class="sxs-lookup"><span data-stu-id="f1a55-113">Syslogs streams that are explicitly enabled on hello agent</span></span>

<span data-ttu-id="f1a55-114">Rendiamo impegni sicuro tooprotect hello privacy e protezione dei dati.</span><span class="sxs-lookup"><span data-stu-id="f1a55-114">We make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="f1a55-115">Microsoft aderisce toostrict linee guida di conformità e sicurezza, dalla codifica toooperating un servizio.</span><span class="sxs-lookup"><span data-stu-id="f1a55-115">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span>
<span data-ttu-id="f1a55-116">Questo articolo illustra il modo in cui i dati vengono gestiti e protetti nella soluzione Sicurezza e controllo di OMS.</span><span class="sxs-lookup"><span data-stu-id="f1a55-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="f1a55-117">Origini dati</span><span class="sxs-lookup"><span data-stu-id="f1a55-117">Data sources</span></span>
<span data-ttu-id="f1a55-118">Soluzione di controllo e sicurezza OMS analizzare i dati dalle macchine virtuali e i computer fisici in cui è installato l'agente OMS hello.</span><span class="sxs-lookup"><span data-stu-id="f1a55-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where hello OMS Agent is installed.</span></span> <span data-ttu-id="f1a55-119">La soluzione Sicurezza e controllo di OMS può raccogliere informazioni di configurazione sugli eventi di sicurezza, ad esempio gli eventi Windows, i log di controllo, i log di IIS e i messaggi syslog.</span><span class="sxs-lookup"><span data-stu-id="f1a55-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="f1a55-120">Esempi di tali dati sono: tipo e versione del sistema operativo, processi in esecuzione, nome computer, indirizzi IP, utente connesso e ID tenant.</span><span class="sxs-lookup"><span data-stu-id="f1a55-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="f1a55-121">Protezione dati</span><span class="sxs-lookup"><span data-stu-id="f1a55-121">Data protection</span></span>
<span data-ttu-id="f1a55-122">**La separazione dei dati**: dati vengono mantenuti separati logicamente in ogni componente servizio hello.</span><span class="sxs-lookup"><span data-stu-id="f1a55-122">**Data segregation**: Data is kept logically separate on each component throughout hello service.</span></span> <span data-ttu-id="f1a55-123">Tutti i dati vengono contrassegnati in base all'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="f1a55-123">All data is tagged per organization.</span></span> <span data-ttu-id="f1a55-124">Tale contrassegno persiste per tutto hello del ciclo di vita dei dati e viene applicato a ogni livello del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="f1a55-124">This tagging persists throughout hello data lifecycle, and it is enforced at each layer of hello service.</span></span> 

<span data-ttu-id="f1a55-125">**Accesso ai dati**: tooprovide consigli relativi alla sicurezza e provare a potenziali minacce alla sicurezza, personale Microsoft potrebbero accedere a informazioni raccolte o analizzati dai servizi.</span><span class="sxs-lookup"><span data-stu-id="f1a55-125">**Data access**: tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="f1a55-126">È conforme toohello [condizioni per i servizi Online Microsoft](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) e [informativa sulla Privacy](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), quale stato che Microsoft non utilizza i dati dei clienti o derivare da esso per annunci o simili a scopo commerciale.</span><span class="sxs-lookup"><span data-stu-id="f1a55-126">We adhere toohello [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="f1a55-127">consigli sulla sicurezza tooprovide e analizzare potenziali minacce alla sicurezza, il personale di Microsoft possono accedere a informazioni raccolte o analizzati dai servizi.</span><span class="sxs-lookup"><span data-stu-id="f1a55-127">tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="f1a55-128">Utilizziamo solo i dati dei clienti come tooprovide necessari con Azure servizi, inclusi motivi compatibile con tali servizi.</span><span class="sxs-lookup"><span data-stu-id="f1a55-128">We only use Customer Data as needed tooprovide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="f1a55-129">Mantenere tutti i dati personalizzati tooyour diritti.</span><span class="sxs-lookup"><span data-stu-id="f1a55-129">You retain all rights tooyour own data.</span></span>

<span data-ttu-id="f1a55-130">**Utilizzo di dati**: Microsoft utilizza i modelli e sulle minacce visualizzata in più tenant tooenhance la funzionalità di rilevamento e prevenzione; avviene in conformità con impegni di privacy hello descritto in questo [sulla Privacy Istruzione](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1a55-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants tooenhance our prevention and detection capabilities; we do so in accordance with hello privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="f1a55-131">Percorso dei dati è configurata a livello di area di lavoro OMS hello, durante la creazione dell'area di lavoro hello, che fa parte del processo configurazione OMS Security and Audit iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="f1a55-131">Data location is configured at hello OMS workspace level, during hello workspace creation, which is part of hello initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="f1a55-132">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f1a55-132">See also</span></span>
<span data-ttu-id="f1a55-133">Questo documento illustra in che modo vengono gestiti e protetti i dati in OMS.</span><span class="sxs-lookup"><span data-stu-id="f1a55-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="f1a55-134">toolearn ulteriori informazioni su sicurezza OMS e la soluzione di controllo, vedere:</span><span class="sxs-lookup"><span data-stu-id="f1a55-134">toolearn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="f1a55-135">Panoramica di Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="f1a55-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="f1a55-136">Monitoraggio e risposta tooSecurity avvisi nella soluzione di controllo e protezione di Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="f1a55-136">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="f1a55-137">Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo</span><span class="sxs-lookup"><span data-stu-id="f1a55-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

