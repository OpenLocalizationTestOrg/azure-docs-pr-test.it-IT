---
title: "Correggere le vulnerabilità del sistema operativo nel Centro sicurezza di Azure | Microsoft Docs"
description: "Questo documento illustra come implementare la raccomandazione **Remediate OS vulnerabilities (Risolvi vulnerabilità del sistema operativo)** del Centro sicurezza di Azure."
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
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="ee301-103">Risolvere le vulnerabilità del sistema operativo in Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="ee301-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="ee301-104">Il Centro sicurezza di Azure analizza ogni giorno le configurazioni del sistema operativo delle macchine virtuali (VM) che potrebbero rendere la VM più vulnerabile agli attacchi e suggerisce le modifiche di configurazione per risolvere tali problemi.</span><span class="sxs-lookup"><span data-stu-id="ee301-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make the VM more vulnerable to attack and recommends configuration changes to address these vulnerabilities.</span></span> <span data-ttu-id="ee301-105">Il Centro sicurezza consiglia di risolvere le vulnerabilità quando la configurazione del sistema operativo della VM non corrisponde alle regole di configurazione consigliate.</span><span class="sxs-lookup"><span data-stu-id="ee301-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match the recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="ee301-106">Per altre informazioni sulle configurazioni specifiche monitorate, vedere l'[elenco delle regole di configurazione consigliate](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="ee301-106">For more information on the specific configurations being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="ee301-107">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="ee301-107">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="ee301-108">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="ee301-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="ee301-109">Questo argomento non costituisce una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="ee301-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="ee301-110">Nel pannello **Indicazioni** selezionare **Correggi le vulnerabilità del sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="ee301-110">In the **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="ee301-111">![Remediate OS vulnerabilities (Risolvi vulnerabilità del sistema operativo)][1]</span><span class="sxs-lookup"><span data-stu-id="ee301-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="ee301-112">Viene aperto il pannello **Correggi le vulnerabilità del sistema operativo**, in cui sono elencate le VM con configurazioni del sistema operativo che non corrispondono alle regole di configurazione consigliate.</span><span class="sxs-lookup"><span data-stu-id="ee301-112">The **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match the recommended configuration rules.</span></span>  <span data-ttu-id="ee301-113">Per ogni VM, il pannello identifica:</span><span class="sxs-lookup"><span data-stu-id="ee301-113">For each VM, the blade identifies:</span></span>

   * <span data-ttu-id="ee301-114">**REGOLE NON RIUSCITE** : il numero di regole non riuscite nella configurazione del sistema operativo della VM.</span><span class="sxs-lookup"><span data-stu-id="ee301-114">**FAILED RULES** -- The number of rules that the VM's OS configuration failed.</span></span>
   * <span data-ttu-id="ee301-115">**ORA DELL'ULTIMA ANALISI** : data e ora dell'ultima volta in cui il Centro sicurezza ha verificato la configurazione del sistema operativo della VM.</span><span class="sxs-lookup"><span data-stu-id="ee301-115">**LAST SCAN TIME** -- The date and time that Security Center last scanned the VM’s OS configuration.</span></span>
   * <span data-ttu-id="ee301-116">**STATO** : stato corrente della vulnerabilità:</span><span class="sxs-lookup"><span data-stu-id="ee301-116">**STATE** -- The current state of the vulnerability:</span></span>

     * <span data-ttu-id="ee301-117">Aperta: la vulnerabilità non è ancora stata applicata</span><span class="sxs-lookup"><span data-stu-id="ee301-117">Open: The vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="ee301-118">In corso: l'applicazione della vulnerabilità in corso e non è richiesta alcuna azione da parte dell'utente</span><span class="sxs-lookup"><span data-stu-id="ee301-118">In Progress: The vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="ee301-119">Risolta: la vulnerabilità è già stata risolta. Dopo che il problema è stato risolto, la voce viene visualizzata in grigio</span><span class="sxs-lookup"><span data-stu-id="ee301-119">Resolved: The vulnerability was already addressed (when the issue has been resolved, the entry is grayed out)</span></span>
   * <span data-ttu-id="ee301-120">**GRAVITÀ** : tutte le vulnerabilità sono impostate su un livello di gravità bassa, vale a dire che è necessario gestire una vulnerabilità ma non è necessaria un'attenzione immediata.</span><span class="sxs-lookup"><span data-stu-id="ee301-120">**SEVERITY** -- All vulnerabilities are set to a severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="ee301-121">Selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ee301-121">Select a VM.</span></span> <span data-ttu-id="ee301-122">Si apre un pannello per la VM, in cui sono visualizzate le regole non riuscite.</span><span class="sxs-lookup"><span data-stu-id="ee301-122">A blade for that VM opens and displays the rules that have failed.</span></span>
   <span data-ttu-id="ee301-123">![Regole di configurazione non riuscite][2]</span><span class="sxs-lookup"><span data-stu-id="ee301-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="ee301-124">Selezionare una regola.</span><span class="sxs-lookup"><span data-stu-id="ee301-124">Select a rule.</span></span> <span data-ttu-id="ee301-125">In questo esempio selezioniamo **Le password devono essere conformi ai requisiti di complessità**.</span><span class="sxs-lookup"><span data-stu-id="ee301-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="ee301-126">Verrà visualizzato un pannello che descrive la regola non riuscita e l'impatto.</span><span class="sxs-lookup"><span data-stu-id="ee301-126">A blade opens describing the failed rule and the impact.</span></span> <span data-ttu-id="ee301-127">Esaminare i dettagli e valutare come verranno applicate le configurazioni del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ee301-127">Review the details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="ee301-128">![Descrizione della regola non riuscita][3]</span><span class="sxs-lookup"><span data-stu-id="ee301-128">![Description for the failed rule][3]</span></span>

  <span data-ttu-id="ee301-129">Il Centro sicurezza usa l'enumerazione di configurazione comune (CCE) per assegnare identificatori univoci per le regole di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ee301-129">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="ee301-130">In questo pannello sono disponibili le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ee301-130">The following information is provided on this blade:</span></span>

  - <span data-ttu-id="ee301-131">NOME: nome della regola</span><span class="sxs-lookup"><span data-stu-id="ee301-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="ee301-132">GRAVITÀ: valore della gravità di CCE a livello critico, importante o di avviso</span><span class="sxs-lookup"><span data-stu-id="ee301-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="ee301-133">CCIED: identificatore univoco di CCE per la regola</span><span class="sxs-lookup"><span data-stu-id="ee301-133">CCIED -- CCE unique identifier for the rule</span></span>
  - <span data-ttu-id="ee301-134">DESCRIZIONE: descrizione della regola</span><span class="sxs-lookup"><span data-stu-id="ee301-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="ee301-135">VULNERABILITÀ: spiegazione della vulnerabilità o del rischio in caso di mancata applicazione della regola</span><span class="sxs-lookup"><span data-stu-id="ee301-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="ee301-136">IMPATTO: impatto sull'azienda quando viene applicata la regola</span><span class="sxs-lookup"><span data-stu-id="ee301-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="ee301-137">VALORE PREVISTO: valore previsto quando il Centro sicurezza analizza la configurazione del sistema operativo della VM rispetto alla regola</span><span class="sxs-lookup"><span data-stu-id="ee301-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="ee301-138">OPERAZIONE DI REGOLA: operazione di regola usata dal Centro sicurezza durante l'analisi della configurazione del sistema operativo della VM rispetto alla regola</span><span class="sxs-lookup"><span data-stu-id="ee301-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="ee301-139">VALORE EFFETTIVO: valore restituito dopo l'analisi della configurazione del sistema operativo della VM rispetto alla regola</span><span class="sxs-lookup"><span data-stu-id="ee301-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="ee301-140">RISULTATO DELLA VALUTAZIONE: risultati dell'analisi: riuscita, non riuscita</span><span class="sxs-lookup"><span data-stu-id="ee301-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="ee301-141">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ee301-141">See also</span></span>
<span data-ttu-id="ee301-142">Questo documento illustra come implementare la raccomandazione "Remediate OS vulnerabilities" (Risolvi vulnerabilità del sistema operativo) del Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="ee301-142">This article showed you how to implement the Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="ee301-143">È possibile esaminare il set di regole di configurazione [qui](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="ee301-143">You can review the set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="ee301-144">Il Centro sicurezza usa l'enumerazione di configurazione comune (CCE) per assegnare identificatori univoci per le regole di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ee301-144">Security Center uses CCE (Common Configuration Enumeration) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="ee301-145">Per altre informazioni, vedere la pagina relativa alla enumerazione [CCE](https://nvd.nist.gov/cce/index.cfm) .</span><span class="sxs-lookup"><span data-stu-id="ee301-145">Visit the [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="ee301-146">Per altre informazioni sul Centro sicurezza, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="ee301-146">To learn more about Security Center, see the following resources:</span></span>

* <span data-ttu-id="ee301-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) (Piattaforme supportate nel Centro sicurezza di Azure): contiene un elenco di macchine virtuali Windows e Linux supportate.</span><span class="sxs-lookup"><span data-stu-id="ee301-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="ee301-148">[Impostare i criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee301-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ee301-149">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee301-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ee301-150">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md) : informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee301-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="ee301-151">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="ee301-151">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="ee301-152">[Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come monitorare l'integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="ee301-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="ee301-153">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="ee301-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="ee301-154">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee301-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
