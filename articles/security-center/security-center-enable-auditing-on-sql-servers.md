---
title: rilevamento di controllo e minacce aaaEnable in SQL Server nel Centro protezione di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * il rilevamento di abilitare il controllo & minaccia in SQL Server * *.
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
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="2c94e-103">Abilitare il controllo e il rilevamento delle minacce sui server SQL nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="2c94e-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="2c94e-104">Il Centro sicurezza di Azure consiglia di attivare il controllo e il rilevamento delle minacce per tutti i database nei server SQL di Azure, se queste funzionalità non sono già abilitate.</span><span class="sxs-lookup"><span data-stu-id="2c94e-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="2c94e-105">Il controllo e il rilevamento delle minacce possono agevolare la conformità alle normative, comprendere le attività del database e ottenere informazioni su eventuali discrepanze e anomalie che potrebbero indicare problemi aziendali o sospette violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2c94e-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="2c94e-106">Dopo aver attivato il controllo è possibile configurare funzionalità di rilevamento minacce impostazioni e i messaggi di posta elettronica tooreceive degli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2c94e-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="2c94e-107">Rilevamento minacce consente attività di database anomale che possono indicare potenziali database toohello rischi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2c94e-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="2c94e-108">Questo permette toodetect e risposta toopotential minacce che si verificano.</span><span class="sxs-lookup"><span data-stu-id="2c94e-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="2c94e-109">Questa indicazione si applica toohello solo servizio di SQL Azure non include SQL Server in esecuzione nelle macchine virtuali in servizi di infrastruttura di Azure (IaaS di Azure).</span><span class="sxs-lookup"><span data-stu-id="2c94e-109">This recommendation applies toohello Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="2c94e-110">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2c94e-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="2c94e-111">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="2c94e-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="2c94e-112">Implementare la raccomandazione hello</span><span class="sxs-lookup"><span data-stu-id="2c94e-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="2c94e-113">In hello **indicazioni** pannello seleziona **rilevamento Attiva controllo & minaccia nei server SQL**.</span><span class="sxs-lookup"><span data-stu-id="2c94e-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="2c94e-114">Verrà visualizzata hello **rilevamento Attiva controllo & minaccia nei server SQL** blade.</span><span class="sxs-lookup"><span data-stu-id="2c94e-114">This opens hello **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Abilitare il controllo sui server SQL][1]
2. <span data-ttu-id="2c94e-116">Scegliere un SQL server tooenable controllo e minaccia il rilevamento.</span><span class="sxs-lookup"><span data-stu-id="2c94e-116">Select a SQL server tooenable auditing and threat detection on.</span></span> <span data-ttu-id="2c94e-117">Verrà visualizzata hello **controllo e rilevamento minacce** blade.</span><span class="sxs-lookup"><span data-stu-id="2c94e-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="2c94e-118">In hello **controllo e rilevamento minacce** pannello seleziona **ON** in **controllo**.</span><span class="sxs-lookup"><span data-stu-id="2c94e-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Attivare le impostazioni del servizio di controllo][2]
4. <span data-ttu-id="2c94e-120">Seguire i passaggi di hello in [controllo del database SQL nel portale di Azure di hello](../sql-database/sql-database-auditing-portal.md) tooconfigure archiviazione in cui verranno archiviati i log di controllo.</span><span class="sxs-lookup"><span data-stu-id="2c94e-120">Follow hello steps in [SQL database auditing in hello Azure portal](../sql-database/sql-database-auditing-portal.md) tooconfigure storage where your audit logs will be stored.</span></span> <span data-ttu-id="2c94e-121">Hello account di archiviazione della sottoscrizione per la raccolta dati è hello account di archiviazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="2c94e-121">hello subscription's storage account for data collection is hello default storage account.</span></span>
5. <span data-ttu-id="2c94e-122">Seguire i passaggi di hello in [introduzione rilevamento minacce del Database SQL](../sql-database/sql-database-threat-detection.md) tooturn in e configurare il rilevamento di minaccia ed elenco hello tooconfigure di messaggi di posta elettronica che riceveranno gli avvisi di sicurezza al rilevamento di attività anomale.</span><span class="sxs-lookup"><span data-stu-id="2c94e-122">Follow hello steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="2c94e-123">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2c94e-123">See also</span></span>
<span data-ttu-id="2c94e-124">In questo articolo ha illustrato come tooimplement hello raccomandazione Centro sicurezza PC "Abilitare il controllo e delle minacce rilevamento sul server SQL Server".</span><span class="sxs-lookup"><span data-stu-id="2c94e-124">This article showed you how tooimplement hello Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="2c94e-125">toolearn più sulla protezione dei database SQL, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="2c94e-125">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="2c94e-126">Protezione del Database SQL</span><span class="sxs-lookup"><span data-stu-id="2c94e-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="2c94e-127">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="2c94e-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="2c94e-128">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="2c94e-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="2c94e-129">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c94e-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="2c94e-130">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c94e-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="2c94e-131">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="2c94e-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="2c94e-132">[Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="2c94e-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="2c94e-133">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="2c94e-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="2c94e-134">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) -ottenere informazioni e notizie sicurezza di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2c94e-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
