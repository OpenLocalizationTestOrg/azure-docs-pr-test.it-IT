---
title: Proteggere i dati personali con il Centro sicurezza di Azure| Microsoft Docs
description: Proteggere i dati personali con il Centro sicurezza di Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3a941389713a4d3dbffbbfe8a717409927d85c6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="7595c-103">Proteggere i dati personali da violazioni e attacchi: Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="7595c-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="7595c-104">Questo articolo illustra come usare il Centro sicurezza di Azure per proteggere i dati personali da violazioni e attacchi.</span><span class="sxs-lookup"><span data-stu-id="7595c-104">This article will help you understand how to use Azure Security Center to protect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="7595c-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="7595c-105">Scenario</span></span> 

<span data-ttu-id="7595c-106">Un'importante compagnia di viaggi in crociera, con sede negli Stati Uniti, sta espandendo le proprie operazioni per offrire itinerari nel Mar Mediterraneo e nel Mar Baltico, nonché nelle isole britanniche.</span><span class="sxs-lookup"><span data-stu-id="7595c-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="7595c-107">Per supportare tale iniziativa, ha acquistato diverse linee minori con sede in Italia, Germania, Danimarca e Regno Unito.</span><span class="sxs-lookup"><span data-stu-id="7595c-107">To help in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="7595c-108">La società usa Microsoft Azure per archiviare i dati aziendali nel cloud.</span><span class="sxs-lookup"><span data-stu-id="7595c-108">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="7595c-109">Questi includono informazioni personali come nomi, indirizzi, numeri di telefono e dati delle carte di credito,</span><span class="sxs-lookup"><span data-stu-id="7595c-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="7595c-110">oltre a informazioni relative alle risorse umane quali:</span><span class="sxs-lookup"><span data-stu-id="7595c-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="7595c-111">Indirizzi</span><span class="sxs-lookup"><span data-stu-id="7595c-111">Addresses</span></span>
- <span data-ttu-id="7595c-112">Numeri di telefono</span><span class="sxs-lookup"><span data-stu-id="7595c-112">Phone numbers</span></span>
- <span data-ttu-id="7595c-113">Codici fiscali</span><span class="sxs-lookup"><span data-stu-id="7595c-113">Tax identification numbers</span></span>
- <span data-ttu-id="7595c-114">Informazioni sanitarie</span><span class="sxs-lookup"><span data-stu-id="7595c-114">Medical information</span></span>

<span data-ttu-id="7595c-115">La compagnia di viaggi in crociera gestisce anche un ampio database di clienti che partecipano al programma fedeltà.</span><span class="sxs-lookup"><span data-stu-id="7595c-115">The cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="7595c-116">I dipendenti aziendali accedono alla rete dagli uffici remoti della società, mentre agenti di viaggio in tutto il mondo hanno accesso ad alcune risorse aziendali.</span><span class="sxs-lookup"><span data-stu-id="7595c-116">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>
<span data-ttu-id="7595c-117">I dati personali viaggiano attraverso la rete tra queste posizioni e il data center di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7595c-117">Personal data travels across the network between these locations and the Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="7595c-118">Presentazione del problema</span><span class="sxs-lookup"><span data-stu-id="7595c-118">Problem statement</span></span>

<span data-ttu-id="7595c-119">La società teme eventuali attacchi alle risorse di Azure e</span><span class="sxs-lookup"><span data-stu-id="7595c-119">The company is concerned about the threat of attacks on their Azure resources.</span></span> <span data-ttu-id="7595c-120">intende impedire l'esposizione dei dati personali di clienti e dipendenti a persone non autorizzate.</span><span class="sxs-lookup"><span data-stu-id="7595c-120">They want to prevent exposure of customers’ and employees’ personal data to unauthorized persons.</span></span> <span data-ttu-id="7595c-121">Vuole ottenere informazioni sulla prevenzione e sulla risposta/correzione per questi eventi, oltre a un modo efficace per monitorare costantemente la sicurezza delle risorse cloud.</span><span class="sxs-lookup"><span data-stu-id="7595c-121">They want guidance on both prevention and response/remediation, as well as an effective way to monitor the ongoing security of their cloud resources.</span></span>
<span data-ttu-id="7595c-122">È necessaria una solida linea di difesa dagli attuali utenti malintenzionati, particolarmente sofisticati e organizzati.</span><span class="sxs-lookup"><span data-stu-id="7595c-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="7595c-123">Obiettivo dell'azienda</span><span class="sxs-lookup"><span data-stu-id="7595c-123">Company goal</span></span>

<span data-ttu-id="7595c-124">Uno degli obiettivi dell'azienda è garantire la privacy dei dati personali di dipendenti e clienti, proteggendo tali dati dalle minacce.</span><span class="sxs-lookup"><span data-stu-id="7595c-124">One of the company’s goals is to ensure the privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="7595c-125">Uno degli obiettivi dell'azienda è rispondere immediatamente a eventuali segnali di violazione per ridurre l'impatto.</span><span class="sxs-lookup"><span data-stu-id="7595c-125">One of their goals is to respond immediately to signs of breach to mitigate the impact.</span></span> <span data-ttu-id="7595c-126">È necessario un modo per valutare lo stato corrente della sicurezza e identificare le configurazioni vulnerabili per adottare misure correttive.</span><span class="sxs-lookup"><span data-stu-id="7595c-126">It requires a way to assess the current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="7595c-127">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="7595c-127">Solutions</span></span>

<span data-ttu-id="7595c-128">Il Centro sicurezza di Microsoft Azure offre una soluzione integrata di monitoraggio della sicurezza e gestione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="7595c-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="7595c-129">Offre funzionalità efficaci e facili da usare per la prevenzione e il rilevamento delle minacce e la relativa risposta.</span><span class="sxs-lookup"><span data-stu-id="7595c-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="7595c-130">Prevenzione</span><span class="sxs-lookup"><span data-stu-id="7595c-130">Prevention</span></span>

<span data-ttu-id="7595c-131">Il Centro sicurezza di Azure consente di impedire le violazioni tramite l'impostazione di criteri di sicurezza, l'accesso Just-in-Time e l'implementazione delle raccomandazioni sulla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="7595c-131">ASC helps you prevent breaches by enabling you to set security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="7595c-132">I criteri di sicurezza definiscono il set di controlli consigliati per le risorse all'interno della sottoscrizione specificata.</span><span class="sxs-lookup"><span data-stu-id="7595c-132">A security policy defines the set of controls recommended for resources within the specified subscription.</span></span> <span data-ttu-id="7595c-133">L'accesso Just-in-Time può essere usato per bloccare il traffico in ingresso nelle macchine virtuali di Azure, riducendo l'esposizione agli attacchi.</span><span class="sxs-lookup"><span data-stu-id="7595c-133">Just in time access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks.</span></span> <span data-ttu-id="7595c-134">Le raccomandazioni sulla sicurezza vengono create dal Centro sicurezza di Azure dopo l'analisi dello stato di sicurezza delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="7595c-134">Security recommendations are created by ASC after analyzing the security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="7595c-135">Come impostare i criteri di sicurezza nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="7595c-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="7595c-136">È possibile configurare criteri di sicurezza per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7595c-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="7595c-137">Per modificare i criteri di sicurezza, è necessario essere proprietario o collaboratore di tale sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7595c-137">To modify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="7595c-138">Nel portale di Azure eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7595c-138">In the Azure portal, do the following:</span></span>

1. <span data-ttu-id="7595c-139">Selezionare **Criteri** nel dashboard del Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="7595c-139">Select **Policy** in the ASC dashboard.</span></span>

2. <span data-ttu-id="7595c-140">Selezionare la sottoscrizione in cui abilitare i criteri.</span><span class="sxs-lookup"><span data-stu-id="7595c-140">Select the subscription on which you want to enable the policy.</span></span>

3. <span data-ttu-id="7595c-141">Scegliere **Criteri di prevenzione** per configurare criteri per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7595c-141">Choose **Prevention policy** to configure policies per subscription.</span></span> <span data-ttu-id="7595c-142">Impostare **Raccogli dati dalle macchine virtuali** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="7595c-142">**Collect data from virtual machines** should be set to **On.**</span></span>

4. <span data-ttu-id="7595c-143">Nelle opzioni **Criteri di prevenzione** selezionare **Sì** per abilitare le raccomandazioni sulla sicurezza da usare per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7595c-143">In the **Prevention policy** options, select **On** to enable the security recommendations that are relevant for the subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="7595c-144">Per altre istruzioni dettagliate e la spiegazione di ogni raccomandazione che può essere abilitata, vedere [Impostare i criteri di sicurezza nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="7595c-144">For more detailed instructions and an explanation of each of the policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="7595c-145">Come configurare l'accesso Just-in-Time</span><span class="sxs-lookup"><span data-stu-id="7595c-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="7595c-146">Quando è abilitata la funzionalità Just-in-Time, il Centro sicurezza protegge il traffico in ingresso alle macchine virtuali di Azure creando una regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="7595c-146">When JIT is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="7595c-147">Selezionare le porte nella macchina virtuale per cui proteggere il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="7595c-147">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="7595c-148">Per usare l'accesso Just-in-Time seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7595c-148">To use JIT access, do the following:</span></span>

1. <span data-ttu-id="7595c-149">Nel pannello del Centro sicurezza di Azure selezionare il **riquadro Accesso Just-In-Time alla VM**.</span><span class="sxs-lookup"><span data-stu-id="7595c-149">Select the **Just in time VM access tile** on the ASC blade.</span></span>

2. <span data-ttu-id="7595c-150">Selezionare la scheda **Consigliati**.</span><span class="sxs-lookup"><span data-stu-id="7595c-150">Select the **Recommended** tab.</span></span>

3. <span data-ttu-id="7595c-151">In **Macchine virtuali** selezionare le macchine virtuali da abilitare.</span><span class="sxs-lookup"><span data-stu-id="7595c-151">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="7595c-152">Verrà visualizzato un segno di spunta accanto a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7595c-152">This puts a checkmark next to a VM.</span></span> 
4. <span data-ttu-id="7595c-153">Selezionare **Abilita JIT** in VM.</span><span class="sxs-lookup"><span data-stu-id="7595c-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="7595c-154">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="7595c-154">Select **Save**.</span></span>

<span data-ttu-id="7595c-155">Verranno quindi visualizzate le porte predefinite che il Centro sicurezza di Azure consiglia di abilitare per la funzionalità Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="7595c-155">Then you can see the default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="7595c-156">È anche possibile aggiungere e configurare una nuova porta per cui abilitare la soluzione Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="7595c-156">You can also add and configure a new port on which you want to enable the just in time solution.</span></span> <span data-ttu-id="7595c-157">Il riquadro **Accesso Just-In-Time alla VM** nel Centro sicurezza visualizza il numero di macchine virtuali configurate per l'accesso Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="7595c-157">The **Just in time VM access** tile in the Security Center shows the number of VMs configured for JIT access.</span></span> <span data-ttu-id="7595c-158">Visualizza anche il numero di richieste di accesso approvate eseguite nell'ultima settimana.</span><span class="sxs-lookup"><span data-stu-id="7595c-158">It also shows the number of approved access requests made in the last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="7595c-159">Per istruzioni su questa operazione e altre informazioni sull'accesso Just-In-Time, vedere [Gestire l'accesso alle macchine virtuali con la funzionalità JIT (Just-in-Time)](https://docs.microsoft.com/azure/security-center/security-center-just-in-time).</span><span class="sxs-lookup"><span data-stu-id="7595c-159">For instructions on how to do this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="7595c-160">Come implementare le raccomandazioni sulla sicurezza del Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="7595c-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="7595c-161">Quando identifica potenziali vulnerabilità della sicurezza, crea raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="7595c-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="7595c-162">Queste raccomandazioni illustrano in dettaglio il processo di configurazione dei controlli necessari.</span><span class="sxs-lookup"><span data-stu-id="7595c-162">The recommendations guide you through the process of configuring the needed controls.</span></span> 
1. <span data-ttu-id="7595c-163">Selezionare il riquadro **Raccomandazioni** nel pannello del Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="7595c-163">Select the **Recommendations** tile on the ASC dashboard.</span></span>

2. <span data-ttu-id="7595c-164">Le raccomandazioni vengono visualizzate sotto forma di tabella, in cui ogni riga rappresenta una raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="7595c-164">View the recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="7595c-165">Per filtrare le raccomandazioni, selezionare **Filtro** e selezionare i valori di gravità e stato da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="7595c-165">To filter recommendations, select **Filter** and select the severity and state values you wish to see.</span></span>

4. <span data-ttu-id="7595c-166">Per ignorare una raccomandazione non applicabile, fare clic e selezionare **Ignora**.</span><span class="sxs-lookup"><span data-stu-id="7595c-166">To dismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="7595c-167">Valutare la raccomandazione da applicare per prima.</span><span class="sxs-lookup"><span data-stu-id="7595c-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="7595c-168">Applicare le raccomandazioni in ordine di priorità.</span><span class="sxs-lookup"><span data-stu-id="7595c-168">Apply the recommendations in order of priority.</span></span>

<span data-ttu-id="7595c-169">Per un elenco delle possibili raccomandazioni e le procedure dettagliate per l'applicazione di ognuna di esse, vedere [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-recommendations).</span><span class="sxs-lookup"><span data-stu-id="7595c-169">For a list of possible recommendations and walk-throughs on how to apply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="7595c-170">Rilevamento e risposta</span><span class="sxs-lookup"><span data-stu-id="7595c-170">Detection and Response</span></span>

<span data-ttu-id="7595c-171">Il rilevamento e la risposta vanno di pari passo perché si vuole ovviamente rispondere nel minor tempo possibile dopo aver rilevato una minaccia.</span><span class="sxs-lookup"><span data-stu-id="7595c-171">Detection and response go together, as you want to respond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="7595c-172">Il sistema di rilevamento delle minacce del Centro sicurezza di Azure funziona tramite la raccolta automatica di informazioni sulla sicurezza dalle risorse di Azure, dalla rete e dalle soluzioni dei partner connessi.</span><span class="sxs-lookup"><span data-stu-id="7595c-172">ASC threat detection works by automatically collecting security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="7595c-173">Il Centro sicurezza di Azure può aggiornare rapidamente gli algoritmi di rilevamento a fronte del rilascio di exploit nuovi e sofisticati da parte di utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="7595c-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="7595c-174">Per altre informazioni sul funzionamento del rilevamento delle minacce nel Centro sicurezza di Azure, vedere [Funzionalità di rilevamento del Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="7595c-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-to-security-alerts"></a><span data-ttu-id="7595c-175">Come gestire e rispondere agli avvisi di sicurezza</span><span class="sxs-lookup"><span data-stu-id="7595c-175">How do I manage and respond to security alerts?</span></span>

<span data-ttu-id="7595c-176">Il Centro sicurezza visualizza un elenco degli avvisi di sicurezza in ordine di priorità, oltre alle informazioni necessarie per analizzare rapidamente il problema</span><span class="sxs-lookup"><span data-stu-id="7595c-176">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem.</span></span> <span data-ttu-id="7595c-177">e indicazioni per risolvere un attacco.</span><span class="sxs-lookup"><span data-stu-id="7595c-177">Security Center also includes recommendations for how to remediate an attack.</span></span> <span data-ttu-id="7595c-178">Per gestire gli avvisi di sicurezza, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7595c-178">To manage your security alerts, do the following:</span></span>

1. <span data-ttu-id="7595c-179">Selezionare il riquadro **Avvisi di sicurezza** nel dashboard del Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="7595c-179">Select the **Security alerts** tile in the ASC dashboard.</span></span> <span data-ttu-id="7595c-180">Verranno visualizzati i dettagli di ogni avviso.</span><span class="sxs-lookup"><span data-stu-id="7595c-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="7595c-181">Per filtrare gli avvisi in base alla data, allo stato e alla gravità, selezionare **Filtro** e quindi i valori da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="7595c-181">To filter alerts based on date, state, and severity, select **Filter** and then select the values you want to see.</span></span>

3. <span data-ttu-id="7595c-182">Per rispondere a un avviso selezionarlo, verificare le informazioni e quindi selezionare la risorsa che ha subito l'attacco.</span><span class="sxs-lookup"><span data-stu-id="7595c-182">To respond to an alert, select it and review the information, then select the resource that was attacked.</span></span>

4. <span data-ttu-id="7595c-183">Nel campo **Descrizione** verranno visualizzate informazioni dettagliate, tra cui la correzione consigliata.</span><span class="sxs-lookup"><span data-stu-id="7595c-183">In the **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="7595c-184">Per altre informazioni dettagliate sulla risposta agli avvisi di sicurezza, vedere [Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="7595c-184">For more detailed instructions on responding to security alerts, see [Managing and responding to security alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="7595c-185">Per agevolare l'analisi degli avvisi di sicurezza, l'azienda può integrare gli avvisi del Centro sicurezza di Azure con la propria soluzione SIEM, usando l'[integrazione dei log di Azure](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="7595c-185">For further help in investigating security alerts, the company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="7595c-186">Come gestire gli eventi imprevisti per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="7595c-186">How do I manage security incidents?</span></span>

<span data-ttu-id="7595c-187">In Centro sicurezza di Azure, un evento imprevisto per la sicurezza è un'aggregazione di tutti gli avvisi relativi a una risorsa corrispondenti a modelli di catena di attacco.</span><span class="sxs-lookup"><span data-stu-id="7595c-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="7595c-188">Un evento imprevisto riporta un elenco degli avvisi correlati, che consente di ottenere altre informazioni su ogni occorrenza.</span><span class="sxs-lookup"><span data-stu-id="7595c-188">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span> <span data-ttu-id="7595c-189">Gli eventi imprevisti vengono visualizzati nel riquadro e nel pannello Avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="7595c-189">Incidents appear in the Security Alerts tile and blade.</span></span>

<span data-ttu-id="7595c-190">Per esaminare e gestire gli eventi imprevisti per la sicurezza, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7595c-190">To review and manage security incidents, do the following:</span></span>

1. <span data-ttu-id="7595c-191">Selezionare il riquadro **Avvisi di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="7595c-191">Select the **Security alerts** tile.</span></span> <span data-ttu-id="7595c-192">In caso di rilevamento, l'evento imprevisto per la sicurezza verrà visualizzato nel grafico degli avvisi di sicurezza,</span><span class="sxs-lookup"><span data-stu-id="7595c-192">if a security incident is detected, it will appear under the security alerts graph.</span></span> <span data-ttu-id="7595c-193">con un'icona diversa da quella degli altri avvisi.</span><span class="sxs-lookup"><span data-stu-id="7595c-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="7595c-194">Selezionare l'evento imprevisto per la sicurezza per visualizzare altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="7595c-194">Select the incident to see more details about this security incident.</span></span> <span data-ttu-id="7595c-195">Le altre informazioni includono descrizione completa, gravità, stato corrente, risorsa che ha subito l'attacco e misure correttive per l'evento imprevisto, oltre agli avvisi inclusi nell'evento.</span><span class="sxs-lookup"><span data-stu-id="7595c-195">Additional details include its full description, its severity, its current state, the attacked resource, the remediation steps for the incident, and the alerts that were included in this incident.</span></span>

<span data-ttu-id="7595c-196">È possibile filtrare per visualizzare **solo gli eventi imprevisti**, **solo gli avvisi** o **entrambi**.</span><span class="sxs-lookup"><span data-stu-id="7595c-196">You can filter to see **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-the-threat-intelligence-report"></a><span data-ttu-id="7595c-197">Come accedere al report di intelligence per le minacce</span><span class="sxs-lookup"><span data-stu-id="7595c-197">How do I access the Threat Intelligence Report?</span></span>

<span data-ttu-id="7595c-198">Per identificare le minacce, il Centro sicurezza di Azure analizza informazioni raccolte da più origini.</span><span class="sxs-lookup"><span data-stu-id="7595c-198">ASC analyzes information from multiple sources to identify threats.</span></span> <span data-ttu-id="7595c-199">Per consentire ai team che gestiscono la risposta agli eventi imprevisti di analizzare e correggere le minacce, il Centro sicurezza include un report di intelligence per le minacce contenente informazioni sulla minaccia rilevata.</span><span class="sxs-lookup"><span data-stu-id="7595c-199">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected.</span></span>

<span data-ttu-id="7595c-200">Il Centro sicurezza rende disponibili tre tipi di report per le minacce, che possono variare a seconda dell'attacco.</span><span class="sxs-lookup"><span data-stu-id="7595c-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="7595c-201">I report disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="7595c-201">The reports available are:</span></span>

- <span data-ttu-id="7595c-202">Report sui gruppi di attività: fornisce approfondimenti sugli utenti malintenzionati e relativi obiettivi e strategie.</span><span class="sxs-lookup"><span data-stu-id="7595c-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="7595c-203">Report sulle campagne: si concentra sui dettagli di specifiche campagne di attacco.</span><span class="sxs-lookup"><span data-stu-id="7595c-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="7595c-204">Report riepilogativo delle minacce: tratta tutti gli elementi presenti nei due report precedenti.</span><span class="sxs-lookup"><span data-stu-id="7595c-204">Threat Summary Report: covers all items in the previous two reports.</span></span>

<span data-ttu-id="7595c-205">Questo tipo di informazioni è molto utile nel corso del processo di risposta agli eventi imprevisti, in cui è in corso un'analisi per identificare l'origine dell'attacco, le motivazioni dell'utente malintenzionato e le azioni da eseguire per attenuare il problema in futuro.</span><span class="sxs-lookup"><span data-stu-id="7595c-205">This type of information is very useful during the incident response process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

1. <span data-ttu-id="7595c-206">Per accedere al report di intelligence per le minacce, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7595c-206">To access the threat intelligence report, do the following:</span></span>

2. <span data-ttu-id="7595c-207">Selezionare il riquadro **Avvisi di sicurezza** nel dashboard del Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="7595c-207">Select the **Security alerts** tile on the ASC dashboard.</span></span>

3. <span data-ttu-id="7595c-208">Selezionare l'avviso di sicurezza per il quale si vogliono ottenere altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="7595c-208">Select the security alert for which you want to obtain more information.</span></span>

4. <span data-ttu-id="7595c-209">Nel campo **Report** fare clic sul collegamento al report di intelligence per le minacce.</span><span class="sxs-lookup"><span data-stu-id="7595c-209">In the **Reports** field, click the link to the threat intelligence report.</span></span>

5. <span data-ttu-id="7595c-210">Si aprirà un file PDF che è possibile scaricare.</span><span class="sxs-lookup"><span data-stu-id="7595c-210">This will open the PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="7595c-211">Per altre informazioni sul report di intelligence per le minacce del Centro sicurezza di Azure, vedere [Report di intelligence per le minacce generato dal Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-threat-report).</span><span class="sxs-lookup"><span data-stu-id="7595c-211">For additional information about the ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="7595c-212">Valutazione</span><span class="sxs-lookup"><span data-stu-id="7595c-212">Assessment</span></span>

<span data-ttu-id="7595c-213">Per semplificare la verifica e la valutazione del comportamento di sicurezza, il Centro sicurezza di Azure mette a disposizione la valutazione integrata della vulnerabilità con agenti cloud Qualys nell'ambito del componente delle raccomandazioni per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="7595c-213">To help with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="7595c-214">L'agente Qualys invia i dati di vulnerabilità alla piattaforma di gestione Qualys che, a sua volta, ritrasmette i dati di vulnerabilità e monitoraggio dello stato al Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="7595c-214">The Qualys agent reports vulnerability data to the Qualys management platform, which then sends vulnerability and health monitoring data back to ASC.</span></span> <span data-ttu-id="7595c-215">La raccomandazione relativa all'aggiunta di una soluzione di valutazione della vulnerabilità viene visualizzata nel pannello **Raccomandazioni** del dashboard del Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="7595c-215">The recommendation to add a vulnerability assessment solution is displayed in the **Recommendations** blade on the ASC dashboard.</span></span>

<span data-ttu-id="7595c-216">Dopo l'installazione della soluzione di valutazione della vulnerabilità nella VM di destinazione, il Centro sicurezza analizza la VM per rilevare e identificare le vulnerabilità del sistema e delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7595c-216">After the vulnerability assessment solution is installed on the target VM, Security Center scans the VM to detect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="7595c-217">I problemi rilevati vengono visualizzati nell'opzione **Raccomandazioni sulle macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="7595c-217">Detected issues are shown under the **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="7595c-218">Come implementare una soluzione di valutazione della vulnerabilità</span><span class="sxs-lookup"><span data-stu-id="7595c-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="7595c-219">Se in una macchina virtuale non è già distribuita una soluzione di valutazione della vulnerabilità, il Centro sicurezza ne raccomanda l'installazione.</span><span class="sxs-lookup"><span data-stu-id="7595c-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="7595c-220">Nel pannello **Raccomandazioni** del dashboard del Centro sicurezza di Azure selezionare **Aggiungi una soluzione di valutazione della vulnerabilità**.</span><span class="sxs-lookup"><span data-stu-id="7595c-220">In the ASC dashboard, on the **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="7595c-221">Selezionare le VM in cui si vuole installare la soluzione di valutazione della vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="7595c-221">Select the VMs where you want to install the vulnerability assessment solution.</span></span>

3. <span data-ttu-id="7595c-222">Fare clic su **Installa su [numero di] VM.**</span><span class="sxs-lookup"><span data-stu-id="7595c-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="7595c-223">Selezionare una soluzione partner in Azure Marketplace oppure selezionare **Qualys** in **Usa la soluzione esistente**.</span><span class="sxs-lookup"><span data-stu-id="7595c-223">Select a partner solution in the Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="7595c-224">È possibile attivare o disattivare le impostazioni di aggiornamento automatico nel pannello **Soluzioni partner**.</span><span class="sxs-lookup"><span data-stu-id="7595c-224">You can turn the auto update settings on or off in the **Partner Solutions** blade.</span></span>

<span data-ttu-id="7595c-225">Per altre informazioni su come implementare una soluzione di valutazione della vulnerabilità, vedere [Valutazione della vulnerabilità nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations).</span><span class="sxs-lookup"><span data-stu-id="7595c-225">For further instructions on how to implement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7595c-226">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7595c-226">Next steps</span></span>

- [<span data-ttu-id="7595c-227">Guida introduttiva per il Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="7595c-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="7595c-228">Introduzione al Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="7595c-228">Introduction to Azure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="7595c-229">Integrazione degli avvisi del Centro sicurezza di Azure con l'integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="7595c-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="7595c-230">Ottimizzare il Centro sicurezza di Azure con la valutazione integrata della vulnerabilità</span><span class="sxs-lookup"><span data-stu-id="7595c-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
