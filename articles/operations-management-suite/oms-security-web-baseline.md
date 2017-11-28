---
title: aaaOperations gestione gruppo di sicurezza e controllo soluzione Web Baseline | Documenti Microsoft
description: "Questo documento viene illustrato come toouse OMS Security and Audit soluzione tooperform una valutazione della linea di base di web di tutti i server web monitorati a scopo di conformità e sicurezza."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="6e253-103">Valutazione baseline Web nella soluzione Sicurezza e controllo di Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6e253-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="6e253-104">Questo documento consente di toouse [soluzione di controllo e protezione di Operations Management Suite (OMS)](operations-management-suite-overview.md) web valutazione della linea di base tooaccess funzionalità hello stato sicuro le risorse monitorati.</span><span class="sxs-lookup"><span data-stu-id="6e253-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="6e253-105">Informazioni sulla valutazione baseline Web</span><span class="sxs-lookup"><span data-stu-id="6e253-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="6e253-106">OMS Security offre attualmente la possibilità di eseguire una valutazione baseline della sicurezza dei sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="6e253-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="6e253-107">Analizza impostazioni del sistema operativo dei server hello ogni 24 ore e fornisce una visualizzazione a impostazioni potenzialmente vulnerabile.</span><span class="sxs-lookup"><span data-stu-id="6e253-107">It scans hello operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="6e253-108">Per altre informazioni sull'argomento, vedere [Valutazione baseline nella soluzione Sicurezza e controllo di Operations Management Suite](oms-security-baseline.md).</span><span class="sxs-lookup"><span data-stu-id="6e253-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="6e253-109">obiettivo di Hello di valutazione di riferimento web hello è toofind impostazioni del server web potenzialmente vulnerabile.</span><span class="sxs-lookup"><span data-stu-id="6e253-109">hello goal of hello web baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="6e253-110">Hello tre origini primarie per le configurazioni di base di hello web sono: configurazione di IIS, ASP.NET e .NET.</span><span class="sxs-lookup"><span data-stu-id="6e253-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="6e253-111">Solo come hello valutazione della linea di base di sistema operativo, sicurezza OMS verrà tooscan il server web ogni 24 ore e forniscono una visualizzazione in stato di sicurezza di essi.</span><span class="sxs-lookup"><span data-stu-id="6e253-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="6e253-112">In Internet Information Service (IIS), le configurazioni sono altamente personalizzabili, che consente di vari toobe livelli di applicazione e del sito sottoposto a override.</span><span class="sxs-lookup"><span data-stu-id="6e253-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="6e253-113">scanner Hello controlla le impostazioni di hello a ogni livello di applicazione/sito di livello radice di addizione toohello predefinito.</span><span class="sxs-lookup"><span data-stu-id="6e253-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="6e253-114">Ciò consente di posizione delle impostazioni di vulnerabilità potenziale tooidentify e correggere rapidamente.</span><span class="sxs-lookup"><span data-stu-id="6e253-114">This helps you tooidentify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="6e253-115">Valutazione baseline della sicurezza Web</span><span class="sxs-lookup"><span data-stu-id="6e253-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="6e253-116">Per questa versione di anteprima questa funzionalità è in corso toobe accedere utilizzando l'opzione di ricerca OMS hello.</span><span class="sxs-lookup"><span data-stu-id="6e253-116">For this preview this feature is going toobe accessed using hello OMS Search option.</span></span> <span data-ttu-id="6e253-117">Seguire i passaggi di hello di sotto di tooperform hello attualmente utilizzato riferimento ad:</span><span class="sxs-lookup"><span data-stu-id="6e253-117">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="6e253-118">In hello **Microsoft Operations Management Suite** fare clic su dashboard principale **Security and Audit** riquadro.</span><span class="sxs-lookup"><span data-stu-id="6e253-118">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="6e253-119">In hello **Security and Audit** dashboard, fare clic su **ricerca nei Log** pulsante.</span><span class="sxs-lookup"><span data-stu-id="6e253-119">In hello **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="6e253-120">Hello prima query che è possibile utilizzare è hello **riepilogo di valutazione della linea di base Web**.</span><span class="sxs-lookup"><span data-stu-id="6e253-120">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="6e253-121">In hello **Cerca qui** , digitare la query: tipo*= SecurityBaselineSummary BaselineType = web*.</span><span class="sxs-lookup"><span data-stu-id="6e253-121">In hello **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="6e253-122">Hello schermata seguente è un esempio di output:</span><span class="sxs-lookup"><span data-stu-id="6e253-122">hello following screen has an output sample:</span></span>

![Riepilogo valutazione baseline Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="6e253-124">In questa query ogni record indica il riepilogo della valutazione in un singolo server.</span><span class="sxs-lookup"><span data-stu-id="6e253-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="6e253-125">Una volta nel hello **Log Search**, è possibile digitare ulteriori informazioni sulla valutazione della linea di base web hello tooobtain query diverse.</span><span class="sxs-lookup"><span data-stu-id="6e253-125">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="6e253-126">Inoltre toohello query precedente, è possibile inoltre utilizzare hello dopo quelli appartenenti a questa versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="6e253-126">In addition toohello previous query, you can also use hello following ones in this preview.</span></span>

<span data-ttu-id="6e253-127">**Web Baseline Rule Assessment** (Valutazione regola baseline Web): ogni record rappresenta una singola valutazione della regola baseline Web in un server singolo.</span><span class="sxs-lookup"><span data-stu-id="6e253-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="6e253-128">Include tutti i dati per regola hello, percorso, il risultato previsto hello e risultato effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="6e253-128">It includes all data for hello rule, location, hello expected result, and hello actual result.</span></span>

<span data-ttu-id="6e253-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="6e253-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Valutazione regola baseline Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="6e253-131">**Mostra tutti i risultati per un server specifico**: questa query Mostra la vista dei risultati toosee di un server specifico.</span><span class="sxs-lookup"><span data-stu-id="6e253-131">**Show all results for a specific server**: This query shows how toosee results of a specific server.</span></span>

<span data-ttu-id="6e253-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="6e253-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Tutti i risultati](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="6e253-134">Inoltre, è possibile utilizzare questi toocreate record/query dashboard, report o avvisi.</span><span class="sxs-lookup"><span data-stu-id="6e253-134">You can also use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="6e253-135">schermata di Hello riportata di seguito è un esempio di controllo dell'interfaccia utente che è possibile aggiungere tooyour dashboard.</span><span class="sxs-lookup"><span data-stu-id="6e253-135">hello screen below has a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="6e253-136">È possibile ottenere informazioni come toovisualize i dati mediante Progettazione vista OMS [qui](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="6e253-136">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="6e253-137">schermata di Hello riportata di seguito è riportato un esempio di come hello affiancato avrà un aspetto simile dopo aver effettuato la personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="6e253-137">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![Interfaccia utente di esempio](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="6e253-139">Se si desidera che le impostazioni di hello tooknow selezionati per la valutazione della linea di base hello, è possibile scaricare [questo foglio di calcolo di Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) che contiene queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="6e253-139">If you would like tooknow hello settings that are checked for hello baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="6e253-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="6e253-140">See also</span></span>
<span data-ttu-id="6e253-141">In questo documento sono state fornite informazioni sulla valutazione baseline Web di Sicurezza e controllo di OMS.</span><span class="sxs-lookup"><span data-stu-id="6e253-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="6e253-142">toolearn più sulla sicurezza di OMS, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="6e253-142">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="6e253-143">Panoramica di Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="6e253-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="6e253-144">Monitoraggio e risposta tooSecurity avvisi nella soluzione di controllo e protezione di Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6e253-144">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="6e253-145">Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo</span><span class="sxs-lookup"><span data-stu-id="6e253-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

