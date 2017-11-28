---
title: Convalida in Centro sicurezza di Azure aaaAlerts | Documenti Microsoft
description: Questo documento consente di avvisi di sicurezza toovalidate hello in Centro sicurezza di Azure.
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
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="a73a8-103">Convalida degli avvisi nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="a73a8-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="a73a8-104">Questo documento vengono illustrate come tooverify se il sistema è configurato correttamente per gli avvisi del Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="a73a8-104">This document helps you learn how tooverify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="a73a8-105">Informazioni sugli avvisi di sicurezza</span><span class="sxs-lookup"><span data-stu-id="a73a8-105">What are security alerts?</span></span>
<span data-ttu-id="a73a8-106">Centro sicurezza PC automaticamente raccoglie, analizza e consente di integrare dati di log da risorse di Azure, rete hello e soluzioni partner connessi, come soluzioni di protezione firewall ed endpoint, toodetect e avvisi è toothreats.</span><span class="sxs-lookup"><span data-stu-id="a73a8-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect and alert you toothreats.</span></span> <span data-ttu-id="a73a8-107">Lettura [toosecurity risponda e gestire gli avvisi in Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) per ulteriori informazioni su avvisi di sicurezza e lettura [informazioni sugli avvisi di sicurezza nel Centro protezione Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn più hello diversi tipi di avvisi.</span><span class="sxs-lookup"><span data-stu-id="a73a8-107">Read [Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn more about hello different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="a73a8-108">Convalida degli avvisi</span><span class="sxs-lookup"><span data-stu-id="a73a8-108">Alert validation</span></span>
<span data-ttu-id="a73a8-109">Dopo che l'agente protezione Center è installato nel computer in uso, eseguire operazioni di hello seguenti dal computer hello in cui si desidera toobe hello attaccata di risorse di avviso hello:</span><span class="sxs-lookup"><span data-stu-id="a73a8-109">After Security Center agent is installed on your computer, follow hello steps below from hello computer where you want toobe hello attacked resource of hello alert:</span></span>

1. <span data-ttu-id="a73a8-110">Copiare un file eseguibile (per esempio calc.exe) toohello del PC o altra directory di praticità.</span><span class="sxs-lookup"><span data-stu-id="a73a8-110">Copy an executable (for example calc.exe) toohello computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="a73a8-111">Rinominare il file troppo**ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="a73a8-111">Rename this file too**ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="a73a8-112">Aprire il prompt dei comandi di hello ed eseguire il file con un argomento (un solo argomento fittizio nome), ad esempio: *ASC_AlertTest_662jfi039N.exe - foo*</span><span class="sxs-lookup"><span data-stu-id="a73a8-112">Open hello command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="a73a8-113">Attendere 5 minuti too10 e aprire gli avvisi del Centro protezione.</span><span class="sxs-lookup"><span data-stu-id="a73a8-113">Wait 5 too10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="a73a8-114">Sono disponibili un avviso toofollowing simili uno:</span><span class="sxs-lookup"><span data-stu-id="a73a8-114">There you should find an alert similar toofollowing one:</span></span>

    ![Convalida degli avvisi](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="a73a8-116">Quando si rivede questo avviso, assicurarsi che il campo di hello argomenti attivato il controllo viene visualizzato come true.</span><span class="sxs-lookup"><span data-stu-id="a73a8-116">When reviewing this alert, make sure hello field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="a73a8-117">Se viene visualizzato false, è necessario tooenable di argomenti della riga di comando di controllo.</span><span class="sxs-lookup"><span data-stu-id="a73a8-117">If it shows false, you need tooenable command-line arguments auditing.</span></span> <span data-ttu-id="a73a8-118">È possibile abilitare questa opzione utilizzando hello seguente riga di comando:</span><span class="sxs-lookup"><span data-stu-id="a73a8-118">You can enable this option using hello following command line:</span></span>

<span data-ttu-id="a73a8-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="a73a8-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="a73a8-120">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a73a8-120">See also</span></span>
<span data-ttu-id="a73a8-121">In questo articolo ha introdotto toohello processo di convalida di avvisi.</span><span class="sxs-lookup"><span data-stu-id="a73a8-121">This article introduced you toohello alerts validation process.</span></span> <span data-ttu-id="a73a8-122">Ora che si ha familiarità con la convalida, provare a hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="a73a8-122">Now that you're familiar with this validation, try hello following articles:</span></span>

* <span data-ttu-id="a73a8-123">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="a73a8-123">[Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="a73a8-124">Informazioni su come toomanage avvisi e gli eventi imprevisti toosecurity rispondono in Centro sicurezza PC.</span><span class="sxs-lookup"><span data-stu-id="a73a8-124">Learn how toomanage alerts, and respond toosecurity incidents in Security Center.</span></span>
* <span data-ttu-id="a73a8-125">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="a73a8-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="a73a8-126">Informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="a73a8-126">Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="a73a8-127">[Informazioni sugli avvisi di sicurezza nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="a73a8-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="a73a8-128">Informazioni sui tipi diversi di hello degli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a73a8-128">Learn about hello different types of security alerts.</span></span>
* <span data-ttu-id="a73a8-129">[Guida alla risoluzione dei problemi del Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="a73a8-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="a73a8-130">Informazioni su come tootroubleshoot comuni problemi nel Centro protezione.</span><span class="sxs-lookup"><span data-stu-id="a73a8-130">Learn how tootroubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="a73a8-131">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a73a8-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="a73a8-132">Trovare le domande frequenti sull'utilizzo del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a73a8-132">Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="a73a8-133">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="a73a8-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="a73a8-134">Post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="a73a8-134">Find blog posts about Azure security and compliance.</span></span>

