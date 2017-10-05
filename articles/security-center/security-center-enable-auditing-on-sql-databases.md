---
title: Abilitare il controllo e il rilevamento delle minacce sui database SQL nel Centro sicurezza di Azure | Microsoft Docs
description: Questo documento viene illustrato come implementare la raccomandazione del Centro sicurezza di Azure * * abilitare il rilevamento di minaccia e di controllo nel database SQL * *.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 8f4febdaa4497fee0dc690b59cd6eaa415c5e5cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="49680-103">Abilitare il controllo e il rilevamento delle minacce sui database SQL nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="49680-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="49680-104">Il Centro sicurezza di Azure consiglia di attivare il controllo e il rilevamento delle minacce per tutti i database SQL, se queste funzionalità non sono già abilitate.</span><span class="sxs-lookup"><span data-stu-id="49680-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="49680-105">Il controllo e il rilevamento delle minacce possono agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare problemi aziendali o sospette violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="49680-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="49680-106">Dopo aver attivato il controllo è possibile configurare le impostazioni di rilevamento delle minacce e gli indirizzi di posta elettronica per ricevere gli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="49680-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="49680-107">La funzionalità di rilevamento delle minacce individua le attività di database che indicano la presenza di potenziali minacce alla sicurezza nel database.</span><span class="sxs-lookup"><span data-stu-id="49680-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="49680-108">Essa consente di rilevare e rispondere a potenziali rischi appena si verificano.</span><span class="sxs-lookup"><span data-stu-id="49680-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="49680-109">Questa raccomandazione si applica esclusivamente al servizio SQL di Azure e non include SQL in esecuzione sulle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="49680-109">This recommendation applies to the Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="49680-110">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="49680-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="49680-111">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="49680-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="49680-112">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="49680-112">Implement the recommendation</span></span>
1. <span data-ttu-id="49680-113">Nel pannello **Raccomandazioni** selezionare **Enable Auditing & Threat detection on SQL databases** (Abilita il controllo e il rilevamento delle minacce sui database SQL).</span><span class="sxs-lookup"><span data-stu-id="49680-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="49680-114">Verrà visualizzato il pannello **Enable Auditing & Threat detection on SQL databases** (Abilita il controllo e il rilevamento delle minacce sui database SQL).</span><span class="sxs-lookup"><span data-stu-id="49680-114">This opens the **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Abilitare il controllo sui database SQL][1]
2. <span data-ttu-id="49680-116">Selezionare un database SQL su cui abilitare il controllo.</span><span class="sxs-lookup"><span data-stu-id="49680-116">Select a SQL database to enable auditing on.</span></span> <span data-ttu-id="49680-117">Verrà visualizzato il pannello **Controllo e rilevamento minacce**.</span><span class="sxs-lookup"><span data-stu-id="49680-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="49680-118">Nel pannello **Controllo e rilevamento minacce** selezionare **ON** in **Controllo**.</span><span class="sxs-lookup"><span data-stu-id="49680-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Attivare il controllo e rilevamento minacce][2]
4. <span data-ttu-id="49680-120">Seguire i passaggi in [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) (Rilevamento di minacce del database SQL nel portale di Azure) per attivare e configurare il rilevamento di minacce e per configurare l'elenco dei messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di anomalie dell'attività.</span><span class="sxs-lookup"><span data-stu-id="49680-120">Follow the steps in [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="49680-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="49680-121">See also</span></span>
<span data-ttu-id="49680-122">Questo articolo illustra come implementare la raccomandazione "Abilitare il controllo e il rilevamento delle minacce sui database SQL" del Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="49680-122">This article showed you how to implement the Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="49680-123">Per altre informazioni su come proteggere il database SQL, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="49680-123">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="49680-124">Protezione del Database SQL</span><span class="sxs-lookup"><span data-stu-id="49680-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="49680-125">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="49680-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="49680-126">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="49680-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="49680-127">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="49680-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="49680-128">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md) : informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="49680-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="49680-129">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="49680-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="49680-130">[Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come monitorare lo stato integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="49680-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="49680-131">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="49680-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="49680-132">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : informazioni e notizie aggiornate sulla sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="49680-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
