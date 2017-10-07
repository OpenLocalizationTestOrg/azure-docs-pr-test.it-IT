---
title: soluzioni per i partner aaaManaging nel Centro protezione di Azure | Documenti Microsoft
description: "Questo documento illustra come Centro sicurezza di Azure consente di monitoraggio in uno stato di integrità hello panoramica delle soluzioni di partner integrato con la sottoscrizione di Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="4841c-103">Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="4841c-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="4841c-104">Questo documento illustra come toomonitor hello lo stato di integrità delle soluzioni di partner in Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="4841c-104">This document walks you through how toomonitor hello health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="4841c-105">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4841c-105">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="4841c-106">Questo argomento non costituisce una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="4841c-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="4841c-107">Monitoraggio delle soluzioni dei partner</span><span class="sxs-lookup"><span data-stu-id="4841c-107">Monitoring partner solutions</span></span>
<span data-ttu-id="4841c-108">Hello **soluzioni Partner** riquadro hello **Centro sicurezza PC** consente di blade monitorare in uno stato di integrità hello immediatamente partner delle soluzioni dell'utente che vengono integrati con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4841c-108">hello **Partner solutions** tile on hello **Security Center** blade lets you monitor at a glance hello health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Riquadro Soluzioni partner][1]

<span data-ttu-id="4841c-110">Hello **soluzioni Partner** riquadro Visualizza il numero di hello di soluzioni per i partner integrato con la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4841c-110">hello **Partner solutions** tile displays hello number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="4841c-111">Se non esistono soluzioni integrate, riquadro hello viene visualizzato il numero di hello zero.</span><span class="sxs-lookup"><span data-stu-id="4841c-111">If there are no solutions integrated, hello tile displays hello number zero.</span></span>

<span data-ttu-id="4841c-112">integrità di hello tooview partner delle soluzioni dell'utente:</span><span class="sxs-lookup"><span data-stu-id="4841c-112">tooview hello health of your partner solutions:</span></span>

1. <span data-ttu-id="4841c-113">Seleziona hello **soluzioni Partner** riquadro.</span><span class="sxs-lookup"><span data-stu-id="4841c-113">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="4841c-114">Hello **soluzioni Partner** apre blade che visualizza un elenco di partner delle soluzioni dell'utente connesso tooSecurity Center.</span><span class="sxs-lookup"><span data-stu-id="4841c-114">hello **Partner solutions** blade opens displaying a list of your partner solutions connected tooSecurity Center.</span></span>

   ![Soluzioni partner][3]

   <span data-ttu-id="4841c-116">può essere stato Hello di una soluzione di partner:</span><span class="sxs-lookup"><span data-stu-id="4841c-116">hello status of a partner solution can be:</span></span>

   * <span data-ttu-id="4841c-117">Protetto (verde): nessun problema di integrità.</span><span class="sxs-lookup"><span data-stu-id="4841c-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="4841c-118">Danneggiato (rosso): è presente un problema di integrità che richiede attenzione immediata.</span><span class="sxs-lookup"><span data-stu-id="4841c-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="4841c-119">Segnalazione arresto (arancione) - soluzione hello è stato arrestato reporting relativa integrità.</span><span class="sxs-lookup"><span data-stu-id="4841c-119">Stopped reporting (orange) - hello solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="4841c-120">Lo stato di protezione sconosciuto (arancione) - stato hello della soluzione hello è sconosciuto al momento a causa di processo tooa non riuscito di aggiungere una nuova soluzione esistente toohello di risorse.</span><span class="sxs-lookup"><span data-stu-id="4841c-120">Unknown protection status (orange) - hello health of hello solution is unknown at this time due tooa failed process of adding a new resource toohello existing solution.</span></span>
   * <span data-ttu-id="4841c-121">Non segnalato (grigio) - non è stato segnalato qualsiasi soluzione hello ancora, lo stato di una soluzione potrebbe essere segnalato se recentemente è stato connesso e viene effettuata la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4841c-121">Not reported (gray) - hello solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="4841c-122">Selezionare una soluzione dei partner.</span><span class="sxs-lookup"><span data-stu-id="4841c-122">Select a partner solution.</span></span> <span data-ttu-id="4841c-123">In questo esempio, consente di seleziona hello **Qualys** soluzione.</span><span class="sxs-lookup"><span data-stu-id="4841c-123">In this example, lets select hello **Qualys** solution.</span></span>  <span data-ttu-id="4841c-124">Un pannello apre visualizzando lo stato di hello della soluzione di partner hello e della soluzione hello le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="4841c-124">A blade opens showing you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="4841c-125">Selezionare **console soluzione** esperienza di gestione dei partner hello tooopen per questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="4841c-125">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

   ![Dettagli della soluzione di un partner][4]
3. <span data-ttu-id="4841c-127">Tornare indietro toohello **Qualys** pannello e selezionare **collegamento VM**.</span><span class="sxs-lookup"><span data-stu-id="4841c-127">Go back toohello **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="4841c-128">Hello **collegamento applicazioni** apre blade.</span><span class="sxs-lookup"><span data-stu-id="4841c-128">hello **Link Applications** blade opens.</span></span> <span data-ttu-id="4841c-129">Qui è possibile connettersi soluzione partner toohello di risorse.</span><span class="sxs-lookup"><span data-stu-id="4841c-129">Here you can connect resources toohello partner solution.</span></span>

   ![Collegamento risorse toopartner soluzione][5]

## <a name="next-steps"></a><span data-ttu-id="4841c-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4841c-131">Next steps</span></span>
<span data-ttu-id="4841c-132">In questo documento è stato introdotto toohello **soluzioni dei Partner** riquadro in Centro sicurezza PC.</span><span class="sxs-lookup"><span data-stu-id="4841c-132">In this document, you were introduced toohello **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="4841c-133">toolearn ulteriori informazioni su Centro di sicurezza, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="4841c-133">toolearn more about Security Center, see hello following articles:</span></span>

* <span data-ttu-id="4841c-134">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) , informazioni come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="4841c-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4841c-135">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni facilitano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4841c-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4841c-136">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4841c-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="4841c-137">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) , informazioni come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="4841c-137">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="4841c-138">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="4841c-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="4841c-139">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) , ottenere informazioni e notizie sicurezza di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4841c-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
