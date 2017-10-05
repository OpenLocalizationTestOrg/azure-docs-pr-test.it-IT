---
title: Convalida degli avvisi nel Centro sicurezza di Azure | Microsoft Docs
description: Questo documento illustra come convalidare gli avvisi di sicurezza nel Centro sicurezza di Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 121b5d8f023a9b663d0e7af26dce8f81db27672c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="009a7-103">Convalida degli avvisi nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="009a7-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="009a7-104">Questo documento illustra come verificare che il sistema sia configurato correttamente per gli avvisi del Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="009a7-104">This document helps you learn how to verify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="009a7-105">Informazioni sugli avvisi di sicurezza</span><span class="sxs-lookup"><span data-stu-id="009a7-105">What are security alerts?</span></span>
<span data-ttu-id="009a7-106">Il Centro sicurezza raccoglie, analizza e integra automaticamente i dati di log delle risorse di Azure, della rete e delle soluzioni partner connesse, ad esempio soluzioni di protezione endpoint e firewall, per rilevare e segnalare all'utente le minacce.</span><span class="sxs-lookup"><span data-stu-id="009a7-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect and alert you to threats.</span></span> <span data-ttu-id="009a7-107">Vedere [Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) per altre informazioni sugli avvisi di sicurezza e [Informazioni sugli avvisi di sicurezza nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) per altre informazioni sui diversi tipi di avvisi.</span><span class="sxs-lookup"><span data-stu-id="009a7-107">Read [Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) to learn more about the different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="009a7-108">Convalida degli avvisi</span><span class="sxs-lookup"><span data-stu-id="009a7-108">Alert validation</span></span>
<span data-ttu-id="009a7-109">Dopo aver installato l'agente del Centro sicurezza nel computer, seguire questa procedura nel computer in cui si vuole essere avvisati delle risorse che hanno subito attacchi:</span><span class="sxs-lookup"><span data-stu-id="009a7-109">After Security Center agent is installed on your computer, follow the steps below from the computer where you want to be the attacked resource of the alert:</span></span>

1. <span data-ttu-id="009a7-110">Copiare un file eseguibile (ad esempio, calc.exe) sul desktop del computer o in un'altra directory per motivi di praticità.</span><span class="sxs-lookup"><span data-stu-id="009a7-110">Copy an executable (for example calc.exe) to the computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="009a7-111">Rinominare il file **ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="009a7-111">Rename this file to **ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="009a7-112">Aprire il prompt dei comandi ed eseguire il file con un argomento (un semplice nome di argomento fittizio), ad esempio: *ASC_AlertTest_662jfi039N.exe -foo*</span><span class="sxs-lookup"><span data-stu-id="009a7-112">Open the command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="009a7-113">Attendere da 5 a 10 minuti e aprire gli avvisi del Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="009a7-113">Wait 5 to 10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="009a7-114">Dovrebbe essere visualizzato un avviso simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="009a7-114">There you should find an alert similar to following one:</span></span>

    ![Convalida degli avvisi](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="009a7-116">Esaminando questo avviso, verificare che il campo Arguments Auditing Enabled (Controllo argomenti abilitato) sia impostato su "vero".</span><span class="sxs-lookup"><span data-stu-id="009a7-116">When reviewing this alert, make sure the field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="009a7-117">Se l'impostazione visualizzata è "falso", è necessario abilitare il controllo degli argomenti della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="009a7-117">If it shows false, you need to enable command-line arguments auditing.</span></span> <span data-ttu-id="009a7-118">È possibile abilitare questa opzione con la riga di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="009a7-118">You can enable this option using the following command line:</span></span>

<span data-ttu-id="009a7-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="009a7-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="009a7-120">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="009a7-120">See also</span></span>
<span data-ttu-id="009a7-121">Questo articolo ha presentato il processo di convalida degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="009a7-121">This article introduced you to the alerts validation process.</span></span> <span data-ttu-id="009a7-122">Dopo aver acquisito familiarità con tale convalida, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="009a7-122">Now that you're familiar with this validation, try the following articles:</span></span>

* <span data-ttu-id="009a7-123">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="009a7-123">[Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="009a7-124">Informazioni su come gestire gli avvisi e rispondere agli eventi imprevisti di sicurezza nel Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="009a7-124">Learn how to manage alerts, and respond to security incidents in Security Center.</span></span>
* <span data-ttu-id="009a7-125">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="009a7-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="009a7-126">Informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="009a7-126">Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="009a7-127">[Informazioni sugli avvisi di sicurezza nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="009a7-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="009a7-128">Informazioni sui diversi tipi di avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="009a7-128">Learn about the different types of security alerts.</span></span>
* <span data-ttu-id="009a7-129">[Guida alla risoluzione dei problemi del Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="009a7-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="009a7-130">Informazioni su come risolvere i problemi comuni nel Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="009a7-130">Learn how to troubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="009a7-131">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="009a7-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="009a7-132">Domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="009a7-132">Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="009a7-133">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="009a7-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="009a7-134">Post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="009a7-134">Find blog posts about Azure security and compliance.</span></span>

