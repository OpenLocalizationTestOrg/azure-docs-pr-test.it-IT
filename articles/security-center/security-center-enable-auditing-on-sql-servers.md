---
title: Abilitare il controllo e il rilevamento delle minacce sui server SQL nel Centro sicurezza di Azure | Microsoft Docs
description: Questo documento viene illustrato come implementare la raccomandazione del Centro sicurezza di Azure * * il rilevamento di abilitare il controllo & minaccia in SQL Server * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 660b537aef8d175a478ff93d60b8391d55fc92ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="f0a75-103">Abilitare il controllo e il rilevamento delle minacce sui server SQL nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="f0a75-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="f0a75-104">Il Centro sicurezza di Azure consiglia di attivare il controllo e il rilevamento delle minacce per tutti i database nei server SQL di Azure, se queste funzionalità non sono già abilitate.</span><span class="sxs-lookup"><span data-stu-id="f0a75-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="f0a75-105">Il controllo e il rilevamento delle minacce possono agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare problemi aziendali o sospette violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f0a75-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="f0a75-106">Dopo aver attivato il controllo è possibile configurare le impostazioni di rilevamento delle minacce e gli indirizzi di posta elettronica per ricevere gli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f0a75-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="f0a75-107">La funzionalità di rilevamento delle minacce individua le attività di database che indicano la presenza di potenziali minacce alla sicurezza nel database.</span><span class="sxs-lookup"><span data-stu-id="f0a75-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="f0a75-108">Essa consente di rilevare e rispondere a potenziali rischi appena si verificano.</span><span class="sxs-lookup"><span data-stu-id="f0a75-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="f0a75-109">Questa indicazione si applica esclusivamente al servizio SQL di Azure e non include i server SQL in esecuzione sulle macchine virtuali all'interno dei servizi di infrastruttura di Azure (Azure IaaS).</span><span class="sxs-lookup"><span data-stu-id="f0a75-109">This recommendation applies to the Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="f0a75-110">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="f0a75-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="f0a75-111">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="f0a75-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="f0a75-112">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="f0a75-112">Implement the recommendation</span></span>
1. <span data-ttu-id="f0a75-113">Nel pannello **Raccomandazioni** selezionare **Enable Auditing & Threat detection on SQL servers** (Abilita il controllo e il rilevamento delle minacce sui server SQL).</span><span class="sxs-lookup"><span data-stu-id="f0a75-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="f0a75-114">Verrà visualizzato il pannello **Enable Auditing & Threat detection on SQL servers** (Abilita il controllo e il rilevamento delle minacce sui server SQL).</span><span class="sxs-lookup"><span data-stu-id="f0a75-114">This opens the **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Abilitare il controllo sui server SQL][1]
2. <span data-ttu-id="f0a75-116">Selezionare il server SQL su cui abilitare il controllo e il rilevamento delle minacce.</span><span class="sxs-lookup"><span data-stu-id="f0a75-116">Select a SQL server to enable auditing and threat detection on.</span></span> <span data-ttu-id="f0a75-117">Verrà visualizzato il pannello **Controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="f0a75-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="f0a75-118">Nel pannello **Controllo e rilevamento minacce** selezionare **ON** in **Controllo**.</span><span class="sxs-lookup"><span data-stu-id="f0a75-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Attivare le impostazioni del servizio di controllo][2]
4. <span data-ttu-id="f0a75-120">Seguire la procedura in [SQL database auditing in the Azure portal](../sql-database/sql-database-auditing-portal.md) (Controllo del database SQL nel portale di Azure) per configurare l'archiviazione in cui verranno archiviati i log di controllo.</span><span class="sxs-lookup"><span data-stu-id="f0a75-120">Follow the steps in [SQL database auditing in the Azure portal](../sql-database/sql-database-auditing-portal.md) to configure storage where your audit logs will be stored.</span></span> <span data-ttu-id="f0a75-121">L'account di archiviazione della sottoscrizione per la raccolta dei dati è l'account di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="f0a75-121">The subscription's storage account for data collection is the default storage account.</span></span>
5. <span data-ttu-id="f0a75-122">Seguire i passaggi in [Introduzione individuazione Database SQL](../sql-database/sql-database-threat-detection.md) per attivare e configurare il rilevamento di minacce e per configurare l'elenco dei messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di anomalie dell'attività.</span><span class="sxs-lookup"><span data-stu-id="f0a75-122">Follow the steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="f0a75-123">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f0a75-123">See also</span></span>
<span data-ttu-id="f0a75-124">Questo articolo illustra come implementare la raccomandazione "Abilitare il controllo e il rilevamento delle minacce sui server SQL" del Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f0a75-124">This article showed you how to implement the Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="f0a75-125">Per altre informazioni su come proteggere il database SQL, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0a75-125">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="f0a75-126">Protezione del Database SQL</span><span class="sxs-lookup"><span data-stu-id="f0a75-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="f0a75-127">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0a75-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="f0a75-128">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0a75-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f0a75-129">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0a75-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f0a75-130">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md) : informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0a75-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="f0a75-131">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f0a75-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="f0a75-132">[Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come monitorare lo stato integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="f0a75-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="f0a75-133">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0a75-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="f0a75-134">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : informazioni e notizie aggiornate sulla sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0a75-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
