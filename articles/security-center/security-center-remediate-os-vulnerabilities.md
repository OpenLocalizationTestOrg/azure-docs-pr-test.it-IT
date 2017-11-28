---
title: "le vulnerabilità del sistema operativo aaaRemediate in Centro sicurezza di Azure | Documenti Microsoft"
description: "Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * OS correggere vulnerabilità * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="fdff0-103">Risolvere le vulnerabilità del sistema operativo in Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="fdff0-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="fdff0-104">Centro sicurezza di Azure ogni giorno analizza il sistema operativo di macchina virtuale (VM) (sistema operativo) per le configurazioni che è possibile apportare hello VM più vulnerabile tooattack ed è consigliabile utilizzare le modifiche di configurazione tooaddress queste vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="fdff0-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make hello VM more vulnerable tooattack and recommends configuration changes tooaddress these vulnerabilities.</span></span> <span data-ttu-id="fdff0-105">Centro sicurezza PC consiglia di risolvere le vulnerabilità quando configurazione del sistema operativo della macchina virtuale non corrisponde ad hello regole di configurazione consigliata.</span><span class="sxs-lookup"><span data-stu-id="fdff0-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match hello recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="fdff0-106">Per ulteriori informazioni sulle configurazioni di hello specifici da monitorare, vedere hello [elenco delle regole di configurazione consigliata](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="fdff0-106">For more information on hello specific configurations being monitored, see hello [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="fdff0-107">Implementare la raccomandazione hello</span><span class="sxs-lookup"><span data-stu-id="fdff0-107">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="fdff0-108">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fdff0-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="fdff0-109">Questo argomento non costituisce una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="fdff0-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="fdff0-110">In hello **indicazioni** pannello seleziona **vulnerabilità monitora e aggiorna sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="fdff0-110">In hello **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="fdff0-111">![Remediate OS vulnerabilities][1]</span><span class="sxs-lookup"><span data-stu-id="fdff0-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="fdff0-112">Hello **vulnerabilità monitora e aggiorna sistema operativo** pannello apre ed elenca le macchine virtuali con configurazioni del sistema operativo che non corrispondono a regole di configurazione consigliata hello.</span><span class="sxs-lookup"><span data-stu-id="fdff0-112">hello **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match hello recommended configuration rules.</span></span>  <span data-ttu-id="fdff0-113">Per ogni macchina virtuale, identifica pannello hello:</span><span class="sxs-lookup"><span data-stu-id="fdff0-113">For each VM, hello blade identifies:</span></span>

   * <span data-ttu-id="fdff0-114">**REGOLE non è stato** -numero hello di regole hello configurazione del sistema operativo della macchina virtuale non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="fdff0-114">**FAILED RULES** -- hello number of rules that hello VM's OS configuration failed.</span></span>
   * <span data-ttu-id="fdff0-115">**ORA dell'ultima analisi** - hello data e l'ora che il Centro sicurezza PC ultima verifica disponibilità aggiornamenti configurazione del sistema operativo della macchina virtuale di hello.</span><span class="sxs-lookup"><span data-stu-id="fdff0-115">**LAST SCAN TIME** -- hello date and time that Security Center last scanned hello VM’s OS configuration.</span></span>
   * <span data-ttu-id="fdff0-116">**STATO** -hello stato corrente della vulnerabilità hello:</span><span class="sxs-lookup"><span data-stu-id="fdff0-116">**STATE** -- hello current state of hello vulnerability:</span></span>

     * <span data-ttu-id="fdff0-117">Apri: vulnerabilità hello è non stata risolta ancora</span><span class="sxs-lookup"><span data-stu-id="fdff0-117">Open: hello vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="fdff0-118">In corso: Vulnerabilità hello attualmente applicato, è necessario alcun intervento da parte dell'utente</span><span class="sxs-lookup"><span data-stu-id="fdff0-118">In Progress: hello vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="fdff0-119">Risolto: vulnerabilità hello è stato già risolto (quando hello problema è stato risolto, la voce hello è grigio)</span><span class="sxs-lookup"><span data-stu-id="fdff0-119">Resolved: hello vulnerability was already addressed (when hello issue has been resolved, hello entry is grayed out)</span></span>
   * <span data-ttu-id="fdff0-120">**GRAVITÀ** -tutte le vulnerabilità sono impostate tooa gravità bassa, vale a dire una vulnerabilità deve essere risolti, ma non richiede attenzione immediata.</span><span class="sxs-lookup"><span data-stu-id="fdff0-120">**SEVERITY** -- All vulnerabilities are set tooa severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="fdff0-121">Selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fdff0-121">Select a VM.</span></span> <span data-ttu-id="fdff0-122">Un pannello per tale macchina virtuale viene aperto e le regole di hello che non sono stato.</span><span class="sxs-lookup"><span data-stu-id="fdff0-122">A blade for that VM opens and displays hello rules that have failed.</span></span>
   <span data-ttu-id="fdff0-123">![Regole di configurazione non riuscite][2]</span><span class="sxs-lookup"><span data-stu-id="fdff0-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="fdff0-124">Selezionare una regola.</span><span class="sxs-lookup"><span data-stu-id="fdff0-124">Select a rule.</span></span> <span data-ttu-id="fdff0-125">In questo esempio selezioniamo **Le password devono essere conformi ai requisiti di complessità**.</span><span class="sxs-lookup"><span data-stu-id="fdff0-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="fdff0-126">Un pannello apre hello non è stato possibile regola e hello impatto che descrive.</span><span class="sxs-lookup"><span data-stu-id="fdff0-126">A blade opens describing hello failed rule and hello impact.</span></span> <span data-ttu-id="fdff0-127">Esaminare i dettagli di hello e prendere in considerazione le modalità di applicazione delle configurazioni del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="fdff0-127">Review hello details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="fdff0-128">![Descrizione per la regola non riuscito di hello][3]</span><span class="sxs-lookup"><span data-stu-id="fdff0-128">![Description for hello failed rule][3]</span></span>

  <span data-ttu-id="fdff0-129">Centro sicurezza PC utilizza identificatori univoci tooassign di enumerazione di configurazione comuni (CCE) per le regole di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fdff0-129">Security Center uses Common Configuration Enumeration (CCE) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="fdff0-130">Hello le seguenti informazioni verrà fornita in questo pannello:</span><span class="sxs-lookup"><span data-stu-id="fdff0-130">hello following information is provided on this blade:</span></span>

  - <span data-ttu-id="fdff0-131">NOME: nome della regola</span><span class="sxs-lookup"><span data-stu-id="fdff0-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="fdff0-132">GRAVITÀ: valore della gravità di CCE a livello critico, importante o di avviso</span><span class="sxs-lookup"><span data-stu-id="fdff0-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="fdff0-133">CCIED - Identificatore univoco CCE per regola hello</span><span class="sxs-lookup"><span data-stu-id="fdff0-133">CCIED -- CCE unique identifier for hello rule</span></span>
  - <span data-ttu-id="fdff0-134">DESCRIZIONE: descrizione della regola</span><span class="sxs-lookup"><span data-stu-id="fdff0-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="fdff0-135">VULNERABILITÀ: spiegazione della vulnerabilità o del rischio in caso di mancata applicazione della regola</span><span class="sxs-lookup"><span data-stu-id="fdff0-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="fdff0-136">IMPATTO: impatto sull'azienda quando viene applicata la regola</span><span class="sxs-lookup"><span data-stu-id="fdff0-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="fdff0-137">VALORE previsto, ovvero Valore previsto quando il Centro sicurezza PC consente di analizzare la configurazione del sistema operativo VM rispetto regola hello</span><span class="sxs-lookup"><span data-stu-id="fdff0-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="fdff0-138">OPERAZIONE di regola - Regola operazione utilizzata dal centro di sicurezza durante l'analisi della configurazione del sistema operativo VM rispetto regola hello</span><span class="sxs-lookup"><span data-stu-id="fdff0-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="fdff0-139">Il valore effettivo: Valore restituito dopo l'analisi della configurazione del sistema operativo VM rispetto regola hello</span><span class="sxs-lookup"><span data-stu-id="fdff0-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="fdff0-140">RISULTATO DELLA VALUTAZIONE: risultati dell'analisi: riuscita, non riuscita</span><span class="sxs-lookup"><span data-stu-id="fdff0-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="fdff0-141">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="fdff0-141">See also</span></span>
<span data-ttu-id="fdff0-142">In questo articolo ha illustrato come tooimplement hello Centro sicurezza PC indicazione "del sistema operativo di correggere vulnerabilità."</span><span class="sxs-lookup"><span data-stu-id="fdff0-142">This article showed you how tooimplement hello Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="fdff0-143">È possibile esaminare i set di regole di configurazione di hello [qui](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="fdff0-143">You can review hello set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="fdff0-144">Centro sicurezza PC utilizza identificatori univoci di tooassign CCE (Common Configuration Enumeration) per le regole di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fdff0-144">Security Center uses CCE (Common Configuration Enumeration) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="fdff0-145">Visitare hello [CCE](https://nvd.nist.gov/cce/index.cfm) sito per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="fdff0-145">Visit hello [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="fdff0-146">toolearn ulteriori informazioni su Centro di sicurezza, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="fdff0-146">toolearn more about Security Center, see hello following resources:</span></span>

* <span data-ttu-id="fdff0-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) (Piattaforme supportate nel Centro sicurezza di Azure): contiene un elenco di macchine virtuali Windows e Linux supportate.</span><span class="sxs-lookup"><span data-stu-id="fdff0-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="fdff0-148">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="fdff0-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="fdff0-149">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdff0-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="fdff0-150">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdff0-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="fdff0-151">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="fdff0-151">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="fdff0-152">[Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="fdff0-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="fdff0-153">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="fdff0-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="fdff0-154">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdff0-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
