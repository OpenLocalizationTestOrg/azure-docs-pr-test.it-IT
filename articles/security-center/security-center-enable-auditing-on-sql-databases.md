---
title: rilevamento di controllo e minacce aaaEnable in SQL database in Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * abilitare il rilevamento di minaccia e di controllo nel database SQL * *.
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
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="90079-103">Abilitare il controllo e il rilevamento delle minacce sui database SQL nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="90079-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="90079-104">Il Centro sicurezza di Azure consiglia di attivare il controllo e il rilevamento delle minacce per tutti i database SQL, se queste funzionalità non sono già abilitate.</span><span class="sxs-lookup"><span data-stu-id="90079-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="90079-105">Il controllo e il rilevamento delle minacce possono agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare problemi aziendali o sospette violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="90079-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="90079-106">Dopo aver attivato il controllo è possibile configurare funzionalità di rilevamento minacce impostazioni e i messaggi di posta elettronica tooreceive degli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="90079-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="90079-107">Rilevamento minacce consente attività di database anomale che possono indicare potenziali database toohello rischi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="90079-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="90079-108">Questo permette toodetect e risposta toopotential minacce che si verificano.</span><span class="sxs-lookup"><span data-stu-id="90079-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="90079-109">Questa indicazione si applica toohello solo servizio di SQL Azure non include SQL in esecuzione nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="90079-109">This recommendation applies toohello Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="90079-110">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="90079-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="90079-111">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="90079-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="90079-112">Implementare la raccomandazione hello</span><span class="sxs-lookup"><span data-stu-id="90079-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="90079-113">In hello **indicazioni** pannello seleziona **Attiva controllo & minaccia rilevamento nel database SQL**.</span><span class="sxs-lookup"><span data-stu-id="90079-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="90079-114">Verrà visualizzata hello **Attiva controllo & minaccia rilevamento nel database SQL** blade.</span><span class="sxs-lookup"><span data-stu-id="90079-114">This opens hello **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Abilitare il controllo sui database SQL][1]
2. <span data-ttu-id="90079-116">Selezionare un tooenable controllo del database SQL in.</span><span class="sxs-lookup"><span data-stu-id="90079-116">Select a SQL database tooenable auditing on.</span></span> <span data-ttu-id="90079-117">Verrà visualizzata hello **controllo e rilevamento minacce** blade.</span><span class="sxs-lookup"><span data-stu-id="90079-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="90079-118">In hello **controllo e rilevamento minacce** pannello seleziona **ON** in **controllo**.</span><span class="sxs-lookup"><span data-stu-id="90079-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Attivare il controllo e rilevamento minacce][2]
4. <span data-ttu-id="90079-120">Seguire i passaggi di hello in [rilevamento minacce del Database SQL nel portale di Azure hello](../sql-database/sql-database-threat-detection-portal.md) tooturn in e configurare il rilevamento di minaccia ed elenco hello tooconfigure di messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di attività anomale.</span><span class="sxs-lookup"><span data-stu-id="90079-120">Follow hello steps in [SQL Database Threat Detection in hello Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="90079-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="90079-121">See also</span></span>
<span data-ttu-id="90079-122">In questo articolo ha illustrato come tooimplement hello Centro sicurezza PC indicazione "Abilita controllo & minaccia rilevamento nel database SQL".</span><span class="sxs-lookup"><span data-stu-id="90079-122">This article showed you how tooimplement hello Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="90079-123">toolearn più sulla protezione dei database SQL, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="90079-123">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="90079-124">Protezione del Database SQL</span><span class="sxs-lookup"><span data-stu-id="90079-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="90079-125">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="90079-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="90079-126">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="90079-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="90079-127">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="90079-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="90079-128">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="90079-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="90079-129">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="90079-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="90079-130">[Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="90079-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="90079-131">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="90079-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="90079-132">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) -ottenere informazioni e notizie sicurezza di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="90079-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
