---
title: i dati personali aaaProtect con Centro sicurezza di Azure | Documenti Microsoft
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
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="b7309-103">Proteggere i dati personali da violazioni e attacchi: Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="b7309-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="b7309-104">In questo articolo consentirà di comprendere la modalità di upera toouse Centro sicurezza di Azure tooprotect dati personali e attacchi.</span><span class="sxs-lookup"><span data-stu-id="b7309-104">This article will help you understand how toouse Azure Security Center tooprotect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="b7309-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="b7309-105">Scenario</span></span> 

<span data-ttu-id="b7309-106">Una società crociera di grandi dimensioni, sede hello negli Stati Uniti, all'espansione relativo itinerari toooffer operazioni Mediterraneo, hello e mare Baltico, nonché hello isole britannico.</span><span class="sxs-lookup"><span data-stu-id="b7309-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="b7309-107">toohelp in tali attività, che è stato acquisito più righe crociera inferiori basate in Italia, Germania, Danimarca e hello Regno Unito</span><span class="sxs-lookup"><span data-stu-id="b7309-107">toohelp in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="b7309-108">la società Hello utilizza i dati aziendali di Microsoft Azure toostore nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="b7309-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="b7309-109">Questi includono informazioni personali come nomi, indirizzi, numeri di telefono e dati delle carte di credito,</span><span class="sxs-lookup"><span data-stu-id="b7309-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="b7309-110">oltre a informazioni relative alle risorse umane quali:</span><span class="sxs-lookup"><span data-stu-id="b7309-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="b7309-111">Indirizzi</span><span class="sxs-lookup"><span data-stu-id="b7309-111">Addresses</span></span>
- <span data-ttu-id="b7309-112">Numeri di telefono</span><span class="sxs-lookup"><span data-stu-id="b7309-112">Phone numbers</span></span>
- <span data-ttu-id="b7309-113">Codici fiscali</span><span class="sxs-lookup"><span data-stu-id="b7309-113">Tax identification numbers</span></span>
- <span data-ttu-id="b7309-114">Informazioni sanitarie</span><span class="sxs-lookup"><span data-stu-id="b7309-114">Medical information</span></span>

<span data-ttu-id="b7309-115">riga crociera Hello gestisce anche un database di grandi dimensioni di benefici e la fedeltà dei membri del programma.</span><span class="sxs-lookup"><span data-stu-id="b7309-115">hello cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="b7309-116">Rete con i dipendenti aziendali accesso hello da sedi remote e agenzie di viaggio hello aziendali presenti in ogni HelloWorld hanno accesso alle risorse aziendali toosome.</span><span class="sxs-lookup"><span data-stu-id="b7309-116">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>
<span data-ttu-id="b7309-117">Dati personali viaggiano attraverso la rete hello tra questi percorsi e i data center Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="b7309-117">Personal data travels across hello network between these locations and hello Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="b7309-118">Presentazione del problema</span><span class="sxs-lookup"><span data-stu-id="b7309-118">Problem statement</span></span>

<span data-ttu-id="b7309-119">la società Hello è interessata sulla minaccia hello di attacchi nelle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7309-119">hello company is concerned about hello threat of attacks on their Azure resources.</span></span> <span data-ttu-id="b7309-120">Desiderano tooprevent esposizione delle persone di toounauthorized dati personali dei dipendenti e clienti.</span><span class="sxs-lookup"><span data-stu-id="b7309-120">They want tooprevent exposure of customers’ and employees’ personal data toounauthorized persons.</span></span> <span data-ttu-id="b7309-121">Informazioni aggiuntive su sia prevenzione e risposta/monitoraggio e aggiornamento, nonché un modo efficace toomonitor hello in corso la sicurezza delle risorse cloud desiderati.</span><span class="sxs-lookup"><span data-stu-id="b7309-121">They want guidance on both prevention and response/remediation, as well as an effective way toomonitor hello ongoing security of their cloud resources.</span></span>
<span data-ttu-id="b7309-122">È necessaria una solida linea di difesa dagli attuali utenti malintenzionati, particolarmente sofisticati e organizzati.</span><span class="sxs-lookup"><span data-stu-id="b7309-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="b7309-123">Obiettivo dell'azienda</span><span class="sxs-lookup"><span data-stu-id="b7309-123">Company goal</span></span>

<span data-ttu-id="b7309-124">Uno degli obiettivi dell'azienda hello è privacy hello tooensure dei dati personali dei dipendenti e clienti per proteggerlo da eventuali minacce.</span><span class="sxs-lookup"><span data-stu-id="b7309-124">One of hello company’s goals is tooensure hello privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="b7309-125">Uno degli obiettivi è toorespond immediatamente toosigns di violazione toomitigate hello impatto.</span><span class="sxs-lookup"><span data-stu-id="b7309-125">One of their goals is toorespond immediately toosigns of breach toomitigate hello impact.</span></span> <span data-ttu-id="b7309-126">Richiede un modo tooassess hello stato corrente di sicurezza, identificare le configurazioni vulnerabile e aggiornarli.</span><span class="sxs-lookup"><span data-stu-id="b7309-126">It requires a way tooassess hello current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="b7309-127">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="b7309-127">Solutions</span></span>

<span data-ttu-id="b7309-128">Il Centro sicurezza di Microsoft Azure offre una soluzione integrata di monitoraggio della sicurezza e gestione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="b7309-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="b7309-129">Offre funzionalità efficaci e facili da usare per la prevenzione e il rilevamento delle minacce e la relativa risposta.</span><span class="sxs-lookup"><span data-stu-id="b7309-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="b7309-130">Prevenzione</span><span class="sxs-lookup"><span data-stu-id="b7309-130">Prevention</span></span>

<span data-ttu-id="b7309-131">ASC consente di impedire violazioni della sicurezza grazie alla possibilità di criteri di sicurezza tooset, fornire l'accesso a just-in-time e implementare i suggerimenti relativi alla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b7309-131">ASC helps you prevent breaches by enabling you tooset security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="b7309-132">Un criterio di sicurezza definisce il set di hello dei controlli consigliati per le risorse all'interno di hello specificato sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b7309-132">A security policy defines hello set of controls recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="b7309-133">Solo in fase di accesso può essere utilizzato toolock verso il basso il traffico in entrata tooyour macchine virtuali di Azure, riducendo l'esposizione tooattacks.</span><span class="sxs-lookup"><span data-stu-id="b7309-133">Just in time access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks.</span></span> <span data-ttu-id="b7309-134">Consigli relativi alla sicurezza vengono creati da ASC al termine dell'analisi dello stato di sicurezza hello delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7309-134">Security recommendations are created by ASC after analyzing hello security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="b7309-135">Come impostare i criteri di sicurezza nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="b7309-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="b7309-136">È possibile configurare criteri di sicurezza per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b7309-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="b7309-137">toomodify un criterio di sicurezza, è necessario essere un proprietario o collaboratore della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b7309-137">toomodify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="b7309-138">Nel portale di Azure hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7309-138">In hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="b7309-139">Selezionare **criteri** nel dashboard di hello ASC.</span><span class="sxs-lookup"><span data-stu-id="b7309-139">Select **Policy** in hello ASC dashboard.</span></span>

2. <span data-ttu-id="b7309-140">Selezionare la sottoscrizione di hello in cui si desidera che i criteri di hello tooenable.</span><span class="sxs-lookup"><span data-stu-id="b7309-140">Select hello subscription on which you want tooenable hello policy.</span></span>

3. <span data-ttu-id="b7309-141">Scegliere **criteri di prevenzione** tooconfigure criteri per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b7309-141">Choose **Prevention policy** tooconfigure policies per subscription.</span></span> <span data-ttu-id="b7309-142">**Raccogliere i dati dalle macchine virtuali** deve essere impostato troppo**in.**</span><span class="sxs-lookup"><span data-stu-id="b7309-142">**Collect data from virtual machines** should be set too**On.**</span></span>

4. <span data-ttu-id="b7309-143">In hello **criteri di prevenzione** opzioni, selezionare **su** tooenable hello consigli relativi alla sicurezza riguardano per la sottoscrizione di hello.</span><span class="sxs-lookup"><span data-stu-id="b7309-143">In hello **Prevention policy** options, select **On** tooenable hello security recommendations that are relevant for hello subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="b7309-144">Per ulteriori istruzioni e una spiegazione di ognuna delle indicazioni di hello criteri che possono essere abilitate, vedere [impostare criteri di sicurezza nel Centro protezione Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="b7309-144">For more detailed instructions and an explanation of each of hello policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="b7309-145">Come configurare l'accesso Just-in-Time</span><span class="sxs-lookup"><span data-stu-id="b7309-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="b7309-146">Quando JIT è abilitato, il Centro sicurezza PC protegge il traffico in entrata tooyour macchine virtuali di Azure creando una regola di gruppo.</span><span class="sxs-lookup"><span data-stu-id="b7309-146">When JIT is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="b7309-147">Selezionare le porte hello in hello VM toowhich verrà bloccato il traffico in ingresso verso il basso.</span><span class="sxs-lookup"><span data-stu-id="b7309-147">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="b7309-148">toouse JIT accedere, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7309-148">toouse JIT access, do hello following:</span></span>

1. <span data-ttu-id="b7309-149">Seleziona hello **immediatamente nel riquadro di accesso VM ora** nel pannello ASC hello.</span><span class="sxs-lookup"><span data-stu-id="b7309-149">Select hello **Just in time VM access tile** on hello ASC blade.</span></span>

2. <span data-ttu-id="b7309-150">Seleziona hello **consigliato** scheda.</span><span class="sxs-lookup"><span data-stu-id="b7309-150">Select hello **Recommended** tab.</span></span>

3. <span data-ttu-id="b7309-151">In **macchine virtuali**, selezionare le macchine virtuali hello che si desidera tooenable.</span><span class="sxs-lookup"><span data-stu-id="b7309-151">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="b7309-152">In questo modo un tooa Avanti VM di segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="b7309-152">This puts a checkmark next tooa VM.</span></span> 
4. <span data-ttu-id="b7309-153">Selezionare **Abilita JIT** in VM.</span><span class="sxs-lookup"><span data-stu-id="b7309-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="b7309-154">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b7309-154">Select **Save**.</span></span>

<span data-ttu-id="b7309-155">È quindi possibile visualizzare porte predefinite hello che ASC consiglia l'abilitazione per JIT.</span><span class="sxs-lookup"><span data-stu-id="b7309-155">Then you can see hello default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="b7309-156">È anche possibile aggiungere e configurare una nuova porta su cui si desidera hello tooenable solo nella soluzione di tempo.</span><span class="sxs-lookup"><span data-stu-id="b7309-156">You can also add and configure a new port on which you want tooenable hello just in time solution.</span></span> <span data-ttu-id="b7309-157">Hello **immediatamente nell'accesso in fase di VM** riquadro nel Centro sicurezza PC hello Mostra il numero di hello di macchine virtuali configurate per l'accesso JIT.</span><span class="sxs-lookup"><span data-stu-id="b7309-157">hello **Just in time VM access** tile in hello Security Center shows hello number of VMs configured for JIT access.</span></span> <span data-ttu-id="b7309-158">Viene inoltre illustrato il numero di hello delle richieste di accesso approvato effettuate in hello ultima settimana.</span><span class="sxs-lookup"><span data-stu-id="b7309-158">It also shows hello number of approved access requests made in hello last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="b7309-159">Per istruzioni su come toodo, e ulteriori informazioni sulla immediatamente accesso ora, vedere [gestire l'accesso alla macchina virtuale con in-time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="b7309-159">For instructions on how toodo this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="b7309-160">Come implementare le raccomandazioni sulla sicurezza del Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="b7309-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="b7309-161">Quando identifica potenziali vulnerabilità della sicurezza, crea raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="b7309-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="b7309-162">indicazioni Hello semplificato il processo di hello di configurazione dei controlli di hello necessita.</span><span class="sxs-lookup"><span data-stu-id="b7309-162">hello recommendations guide you through hello process of configuring hello needed controls.</span></span> 
1. <span data-ttu-id="b7309-163">Seleziona hello **indicazioni** riquadro nel dashboard di hello ASC.</span><span class="sxs-lookup"><span data-stu-id="b7309-163">Select hello **Recommendations** tile on hello ASC dashboard.</span></span>

2. <span data-ttu-id="b7309-164">Visualizzare le raccomandazioni hello, che vengono visualizzati in un formato di tabella in cui ogni riga rappresenta una raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="b7309-164">View hello recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="b7309-165">Selezionare toofilter indicazioni, **filtro** e selezionare i valori di gravità e lo stato hello desiderato toosee.</span><span class="sxs-lookup"><span data-stu-id="b7309-165">toofilter recommendations, select **Filter** and select hello severity and state values you wish toosee.</span></span>

4. <span data-ttu-id="b7309-166">toodismiss un'indicazione che non è applicabile, è possibile fare clic destro e selezionare **Elimina.**</span><span class="sxs-lookup"><span data-stu-id="b7309-166">toodismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="b7309-167">Valutare la raccomandazione da applicare per prima.</span><span class="sxs-lookup"><span data-stu-id="b7309-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="b7309-168">Applica indicazioni hello in ordine di priorità.</span><span class="sxs-lookup"><span data-stu-id="b7309-168">Apply hello recommendations in order of priority.</span></span>

<span data-ttu-id="b7309-169">Per un elenco di possibili indicazioni e procedure su come tooapply ogni, vedere [gestione consigli sulla sicurezza in Centro sicurezza di Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="b7309-169">For a list of possible recommendations and walk-throughs on how tooapply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="b7309-170">Rilevamento e risposta</span><span class="sxs-lookup"><span data-stu-id="b7309-170">Detection and Response</span></span>

<span data-ttu-id="b7309-171">Rilevamento e la risposta andare insieme, come si desidera toorespond al più presto dopo che viene rilevata una minaccia.</span><span class="sxs-lookup"><span data-stu-id="b7309-171">Detection and response go together, as you want toorespond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="b7309-172">Rilevamento minacce ASC funziona automaticamente la raccolta di informazioni di sicurezza da risorse di Azure, rete hello e soluzioni partner connesso.</span><span class="sxs-lookup"><span data-stu-id="b7309-172">ASC threat detection works by automatically collecting security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="b7309-173">Il Centro sicurezza di Azure può aggiornare rapidamente gli algoritmi di rilevamento a fronte del rilascio di exploit nuovi e sofisticati da parte di utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="b7309-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="b7309-174">Per altre informazioni sul funzionamento del rilevamento delle minacce nel Centro sicurezza di Azure, vedere [Funzionalità di rilevamento del Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="b7309-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a><span data-ttu-id="b7309-175">Come gestire e rispondere toosecurity avvisi?</span><span class="sxs-lookup"><span data-stu-id="b7309-175">How do I manage and respond toosecurity alerts?</span></span>

<span data-ttu-id="b7309-176">Viene visualizzato un elenco di avvisi di sicurezza in ordine di priorità del Centro sicurezza PC insieme hello informazioni necessarie tooquickly esaminare il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="b7309-176">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem.</span></span> <span data-ttu-id="b7309-177">Centro sicurezza PC include inoltre indicazioni sul tooremediate un attacco.</span><span class="sxs-lookup"><span data-stu-id="b7309-177">Security Center also includes recommendations for how tooremediate an attack.</span></span> <span data-ttu-id="b7309-178">toomanage la sicurezza degli avvisi, eseguire hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7309-178">toomanage your security alerts, do hello following:</span></span>

1. <span data-ttu-id="b7309-179">Seleziona hello **degli avvisi di sicurezza** riquadro nel dashboard di hello ASC.</span><span class="sxs-lookup"><span data-stu-id="b7309-179">Select hello **Security alerts** tile in hello ASC dashboard.</span></span> <span data-ttu-id="b7309-180">Verranno visualizzati i dettagli di ogni avviso.</span><span class="sxs-lookup"><span data-stu-id="b7309-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="b7309-181">Selezionare gli avvisi toofilter basati sulla data, stato e alla gravità, **filtro** e quindi selezionare i valori hello da toosee.</span><span class="sxs-lookup"><span data-stu-id="b7309-181">toofilter alerts based on date, state, and severity, select **Filter** and then select hello values you want toosee.</span></span>

3. <span data-ttu-id="b7309-182">toorespond tooan avviso, selezionarlo e verificare informazioni hello, quindi selezionare hello risorsa che è stato attaccato.</span><span class="sxs-lookup"><span data-stu-id="b7309-182">toorespond tooan alert, select it and review hello information, then select hello resource that was attacked.</span></span>

4. <span data-ttu-id="b7309-183">In hello **descrizione** campo, si noterà informazioni dettagliate, tra cui monitoraggio e aggiornamento consigliato.</span><span class="sxs-lookup"><span data-stu-id="b7309-183">In hello **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="b7309-184">Per informazioni dettagliate sul risponde toosecurity avvisi, vedere [toosecurity risponda e gestire gli avvisi in Centro sicurezza di Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="b7309-184">For more detailed instructions on responding toosecurity alerts, see [Managing and responding toosecurity alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="b7309-185">Per ulteriori informazioni sull'analisi degli avvisi di sicurezza, società hello possibile integrare avvisi ASC con le relative soluzioni SIEM, utilizzando [integrazione di Azure Log](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="b7309-185">For further help in investigating security alerts, hello company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="b7309-186">Come gestire gli eventi imprevisti per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="b7309-186">How do I manage security incidents?</span></span>

<span data-ttu-id="b7309-187">In Centro sicurezza di Azure, un evento imprevisto per la sicurezza è un'aggregazione di tutti gli avvisi relativi a una risorsa corrispondenti a modelli di catena di attacco.</span><span class="sxs-lookup"><span data-stu-id="b7309-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="b7309-188">Un evento imprevisto riveleranno hello elenco avvisi correlati, che consente di tooobtain ulteriori informazioni su ogni occorrenza.</span><span class="sxs-lookup"><span data-stu-id="b7309-188">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span> <span data-ttu-id="b7309-189">Gli eventi imprevisti vengono visualizzati in hello riquadro avvisi di sicurezza e blade.</span><span class="sxs-lookup"><span data-stu-id="b7309-189">Incidents appear in hello Security Alerts tile and blade.</span></span>

<span data-ttu-id="b7309-190">tooreview e gestire eventi di sicurezza, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7309-190">tooreview and manage security incidents, do hello following:</span></span>

1. <span data-ttu-id="b7309-191">Seleziona hello **degli avvisi di sicurezza** riquadro.</span><span class="sxs-lookup"><span data-stu-id="b7309-191">Select hello **Security alerts** tile.</span></span> <span data-ttu-id="b7309-192">Se viene rilevato un problema di sicurezza, viene visualizzato nel grafico gli avvisi di sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="b7309-192">if a security incident is detected, it will appear under hello security alerts graph.</span></span> <span data-ttu-id="b7309-193">con un'icona diversa da quella degli altri avvisi.</span><span class="sxs-lookup"><span data-stu-id="b7309-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="b7309-194">Selezionare toosee degli eventi imprevisti hello ulteriori dettagli sull'evento imprevisto di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b7309-194">Select hello incident toosee more details about this security incident.</span></span> <span data-ttu-id="b7309-195">Dettagli aggiuntivi includono la descrizione completa, la gravità, il relativo stato corrente, hello attaccata di risorse, i passaggi correttivi hello per evento imprevisto di hello e hello avvisi che sono stati inclusi nell'evento imprevisto.</span><span class="sxs-lookup"><span data-stu-id="b7309-195">Additional details include its full description, its severity, its current state, hello attacked resource, hello remediation steps for hello incident, and hello alerts that were included in this incident.</span></span>

<span data-ttu-id="b7309-196">È possibile filtrare toosee **solo gli eventi imprevisti**, **avvisi solo**, o **entrambi**.</span><span class="sxs-lookup"><span data-stu-id="b7309-196">You can filter toosee **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a><span data-ttu-id="b7309-197">La modalità di accesso di hello Report sullo stato della minaccia</span><span class="sxs-lookup"><span data-stu-id="b7309-197">How do I access hello Threat Intelligence Report?</span></span>

<span data-ttu-id="b7309-198">ASC analizza le informazioni da eventuali minacce tooidentify di più origini.</span><span class="sxs-lookup"><span data-stu-id="b7309-198">ASC analyzes information from multiple sources tooidentify threats.</span></span> <span data-ttu-id="b7309-199">i team di risposta agli eventi imprevisti tooassist ricerca e correzione delle minacce, centro di sicurezza include un report sullo stato della minaccia che contiene informazioni sulla minaccia hello che è stato rilevato.</span><span class="sxs-lookup"><span data-stu-id="b7309-199">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected.</span></span>

<span data-ttu-id="b7309-200">Il Centro sicurezza rende disponibili tre tipi di report per le minacce, che possono variare a seconda dell'attacco.</span><span class="sxs-lookup"><span data-stu-id="b7309-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="b7309-201">report di Hello disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="b7309-201">hello reports available are:</span></span>

- <span data-ttu-id="b7309-202">Report sui gruppi di attività: fornisce approfondimenti sugli utenti malintenzionati e relativi obiettivi e strategie.</span><span class="sxs-lookup"><span data-stu-id="b7309-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="b7309-203">Report sulle campagne: si concentra sui dettagli di specifiche campagne di attacco.</span><span class="sxs-lookup"><span data-stu-id="b7309-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="b7309-204">Report di riepilogo minaccia: copre tutti gli elementi di due report hello precedente.</span><span class="sxs-lookup"><span data-stu-id="b7309-204">Threat Summary Report: covers all items in hello previous two reports.</span></span>

<span data-ttu-id="b7309-205">Questo tipo di informazioni è molto utile durante il processo di risposta agli eventi imprevisti hello, in cui è presente un'origine di hello toounderstand analisi in corso di attacco hello, hello motivazioni dell'autore dell'attacco e quali toomitigate toodo questo problema nelle versioni successive.</span><span class="sxs-lookup"><span data-stu-id="b7309-205">This type of information is very useful during hello incident response process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

1. <span data-ttu-id="b7309-206">tooaccess hello minacce di report, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7309-206">tooaccess hello threat intelligence report, do hello following:</span></span>

2. <span data-ttu-id="b7309-207">Seleziona hello **degli avvisi di sicurezza** riquadro nel dashboard di hello ASC.</span><span class="sxs-lookup"><span data-stu-id="b7309-207">Select hello **Security alerts** tile on hello ASC dashboard.</span></span>

3. <span data-ttu-id="b7309-208">Selezionare l'avviso di sicurezza hello per cui si desidera tooobtain ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="b7309-208">Select hello security alert for which you want tooobtain more information.</span></span>

4. <span data-ttu-id="b7309-209">In hello **report** campo, fare clic su report sullo stato della minaccia di hello collegamento toohello.</span><span class="sxs-lookup"><span data-stu-id="b7309-209">In hello **Reports** field, click hello link toohello threat intelligence report.</span></span>

5. <span data-ttu-id="b7309-210">Verrà aperto il file PDF hello, che è possibile scaricare.</span><span class="sxs-lookup"><span data-stu-id="b7309-210">This will open hello PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="b7309-211">Per ulteriori informazioni su hello report sullo stato della minaccia ASC, vedere [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="b7309-211">For additional information about hello ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="b7309-212">Valutazione</span><span class="sxs-lookup"><span data-stu-id="b7309-212">Assessment</span></span>

<span data-ttu-id="b7309-213">toohelp con test e valutare le condizioni di sicurezza, ASC fornisce per la valutazione delle vulnerabilità integrata con Qualys agenti cloud, come parte del componente indicazioni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b7309-213">toohelp with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="b7309-214">agente Qualys Hello report vulnerabilità dati toohello Qualys piattaforma di gestione, che quindi invia la vulnerabilità e dei dati di monitoraggio dell'integrità, eseguire il backup tooASC.</span><span class="sxs-lookup"><span data-stu-id="b7309-214">hello Qualys agent reports vulnerability data toohello Qualys management platform, which then sends vulnerability and health monitoring data back tooASC.</span></span> <span data-ttu-id="b7309-215">Hello tooadd indicazione viene visualizzata una soluzione per la valutazione delle vulnerabilità in hello **indicazioni** pannello nel dashboard di hello ASC.</span><span class="sxs-lookup"><span data-stu-id="b7309-215">hello recommendation tooadd a vulnerability assessment solution is displayed in hello **Recommendations** blade on hello ASC dashboard.</span></span>

<span data-ttu-id="b7309-216">Dopo l'installazione di soluzioni di valutazione delle vulnerabilità hello destinazione hello VM, analisi di Centro sicurezza PC hello toodetect VM e identificano le vulnerabilità di sistema e dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b7309-216">After hello vulnerability assessment solution is installed on hello target VM, Security Center scans hello VM toodetect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="b7309-217">Rilevati problemi vengono visualizzati sotto hello **indicazioni di macchine virtuali** opzione.</span><span class="sxs-lookup"><span data-stu-id="b7309-217">Detected issues are shown under hello **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="b7309-218">Come implementare una soluzione di valutazione della vulnerabilità</span><span class="sxs-lookup"><span data-stu-id="b7309-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="b7309-219">Se in una macchina virtuale non è già distribuita una soluzione di valutazione della vulnerabilità, il Centro sicurezza ne raccomanda l'installazione.</span><span class="sxs-lookup"><span data-stu-id="b7309-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="b7309-220">Nel dashboard ASC hello in hello **indicazioni** pannello seleziona **aggiungere una soluzione per la valutazione delle vulnerabilità.**</span><span class="sxs-lookup"><span data-stu-id="b7309-220">In hello ASC dashboard, on hello **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="b7309-221">Selezionare le macchine virtuali hello in cui si desidera soluzione per la valutazione delle vulnerabilità tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="b7309-221">Select hello VMs where you want tooinstall hello vulnerability assessment solution.</span></span>

3. <span data-ttu-id="b7309-222">Fare clic su **Installa su [numero di] VM.**</span><span class="sxs-lookup"><span data-stu-id="b7309-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="b7309-223">Selezionare una soluzione di partner in hello Azure Marketplace o under **usare una soluzione esistente,** selezionare **Qualys.**</span><span class="sxs-lookup"><span data-stu-id="b7309-223">Select a partner solution in hello Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="b7309-224">È possibile attivare le impostazioni di aggiornamento automatico hello o disattivare in hello **soluzioni dei Partner** blade.</span><span class="sxs-lookup"><span data-stu-id="b7309-224">You can turn hello auto update settings on or off in hello **Partner Solutions** blade.</span></span>

<span data-ttu-id="b7309-225">Per ulteriori informazioni su come tooimplement una soluzione per la valutazione delle vulnerabilità, vedere [valutazione delle vulnerabilità nel Centro protezione di Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="b7309-225">For further instructions on how tooimplement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7309-226">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b7309-226">Next steps</span></span>

- [<span data-ttu-id="b7309-227">Guida introduttiva per il Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="b7309-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="b7309-228">Introduzione tooAzure Centro sicurezza</span><span class="sxs-lookup"><span data-stu-id="b7309-228">Introduction tooAzure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="b7309-229">Integrazione degli avvisi del Centro sicurezza di Azure con l'integrazione dei log di Azure</span><span class="sxs-lookup"><span data-stu-id="b7309-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="b7309-230">Ottimizzare il Centro sicurezza di Azure con la valutazione integrata della vulnerabilità</span><span class="sxs-lookup"><span data-stu-id="b7309-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
