---
title: aaaIntroduction tooAzure Centro sicurezza PC | Documenti Microsoft
description: "Informazioni sul Centro sicurezza di Azure, le funzionalità principali e il funzionamento."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a><span data-ttu-id="590ae-103">Introduzione tooAzure Centro sicurezza</span><span class="sxs-lookup"><span data-stu-id="590ae-103">Introduction tooAzure Security Center</span></span>
<span data-ttu-id="590ae-104">Informazioni sul Centro sicurezza di Azure, le funzionalità principali e il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="590ae-104">Learn about Azure Security Center, its key capabilities, and how it works.</span></span>

> [!NOTE]
> <span data-ttu-id="590ae-105">A partire da anticipata giugno 2017, centro di sicurezza verrà utilizzata toocollect Microsoft Monitoring Agent hello e archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="590ae-105">Beginning in early June 2017, Security Center will use hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="590ae-106">Vedere [migrazione della piattaforma Azure sicurezza Center](security-center-platform-migration.md) toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="590ae-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) toolearn more.</span></span> <span data-ttu-id="590ae-107">informazioni di Hello in questo articolo rappresentano funzionalità Centro sicurezza dopo la transizione toohello Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="590ae-107">hello information in this article represents Security Center functionality after transition toohello Microsoft Monitoring Agent.</span></span>
>
>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="590ae-108">Che cos'è il Centro sicurezza di Azure?</span><span class="sxs-lookup"><span data-stu-id="590ae-108">What is Azure Security Center?</span></span>
 <span data-ttu-id="590ae-109">Centro sicurezza PC consente di impedire, rilevare e rispondere toothreats con una maggiore visibilità e controllo sulla protezione hello delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="590ae-109">Security Center helps you prevent, detect, and respond toothreats with increased visibility into and control over hello security of your Azure resources.</span></span> <span data-ttu-id="590ae-110">Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="590ae-110">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="590ae-111">Funzionalità principali</span><span class="sxs-lookup"><span data-stu-id="590ae-111">Key capabilities</span></span>
 <span data-ttu-id="590ae-112">Centro sicurezza PC offre minaccia di semplice utilizzo ed efficace funzionalità di prevenzione, rilevamento e risposta che vengono compilate in tooAzure.</span><span class="sxs-lookup"><span data-stu-id="590ae-112">Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in tooAzure.</span></span> <span data-ttu-id="590ae-113">Funzionalità principali:</span><span class="sxs-lookup"><span data-stu-id="590ae-113">Key capabilities are:</span></span>

| <span data-ttu-id="590ae-114">Fase</span><span class="sxs-lookup"><span data-stu-id="590ae-114">Stage</span></span> | <span data-ttu-id="590ae-115">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="590ae-115">Capability</span></span> |
| --- | --- |
| <span data-ttu-id="590ae-116">Prevenzione</span><span class="sxs-lookup"><span data-stu-id="590ae-116">Prevent</span></span> |<span data-ttu-id="590ae-117">Monitoraggi hello lo stato di protezione delle risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="590ae-117">Monitors hello security state of your Azure resources</span></span> |
| <span data-ttu-id="590ae-118">Prevenzione</span><span class="sxs-lookup"><span data-stu-id="590ae-118">Prevent</span></span> | <span data-ttu-id="590ae-119">Definisce i criteri per le sottoscrizioni di Azure in base ai requisiti di sicurezza dell'azienda, tipi di hello di applicazioni che utilizzano e hello riservatezza dei dati</span><span class="sxs-lookup"><span data-stu-id="590ae-119">Defines policies for your Azure subscriptions based on your company’s security requirements, hello types of applications that you use, and hello sensitivity of your data</span></span> |
| <span data-ttu-id="590ae-120">Prevenzione</span><span class="sxs-lookup"><span data-stu-id="590ae-120">Prevent</span></span> | <span data-ttu-id="590ae-121">Usa basate sui criteri di sicurezza indicazioni tooguide i proprietari tramite il processo di hello di implementazione necessari controlli</span><span class="sxs-lookup"><span data-stu-id="590ae-121">Uses policy-driven security recommendations tooguide service owners through hello process of implementing needed controls</span></span> |
| <span data-ttu-id="590ae-122">Prevenzione</span><span class="sxs-lookup"><span data-stu-id="590ae-122">Prevent</span></span> | <span data-ttu-id="590ae-123">Distribuisce rapidamente i servizi di sicurezza e i dispositivi di Microsoft e dei partner</span><span class="sxs-lookup"><span data-stu-id="590ae-123">Rapidly deploys security services and appliances from Microsoft and partners</span></span> |
| <span data-ttu-id="590ae-124">Rilevamento</span><span class="sxs-lookup"><span data-stu-id="590ae-124">Detect</span></span> |<span data-ttu-id="590ae-125">Raccoglie e analizza i dati di sicurezza di risorse di Azure, rete hello e soluzioni partner come programmi antimalware e i firewall automaticamente</span><span class="sxs-lookup"><span data-stu-id="590ae-125">Automatically collects and analyzes security data from your Azure resources, hello network, and partner solutions like antimalware programs and firewalls</span></span> |
| <span data-ttu-id="590ae-126">Rilevamento</span><span class="sxs-lookup"><span data-stu-id="590ae-126">Detect</span></span> | <span data-ttu-id="590ae-127">Usa globale minaccia intelligence da Microsoft hello di prodotti e servizi, hello Microsoft Digital Crimes Unit (DCU), Microsoft Security Response Center (MSRC) e un feed esterno</span><span class="sxs-lookup"><span data-stu-id="590ae-127">Uses global threat intelligence from Microsoft products and services, hello Microsoft Digital Crimes Unit (DCU), hello Microsoft Security Response Center (MSRC), and external feeds</span></span> |
| <span data-ttu-id="590ae-128">Rilevamento</span><span class="sxs-lookup"><span data-stu-id="590ae-128">Detect</span></span> | <span data-ttu-id="590ae-129">Applica analisi avanzate, tra cui analisi del comportamento e di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="590ae-129">Applies advanced analytics, including machine learning and behavioral analysis</span></span> |
| <span data-ttu-id="590ae-130">Risposta</span><span class="sxs-lookup"><span data-stu-id="590ae-130">Respond</span></span> |<span data-ttu-id="590ae-131">Fornisce eventi imprevisti o avvisi di sicurezza con priorità</span><span class="sxs-lookup"><span data-stu-id="590ae-131">Provides prioritized security incidents/alerts</span></span> |
| <span data-ttu-id="590ae-132">Risposta</span><span class="sxs-lookup"><span data-stu-id="590ae-132">Respond</span></span> | <span data-ttu-id="590ae-133">Offre informazioni dettagliate sui origine hello di attacco hello e risorse interessate</span><span class="sxs-lookup"><span data-stu-id="590ae-133">Offers insights into hello source of hello attack and impacted resources</span></span> |
| <span data-ttu-id="590ae-134">Risposta</span><span class="sxs-lookup"><span data-stu-id="590ae-134">Respond</span></span> | <span data-ttu-id="590ae-135">Vengono suggerite alcune modalità toostop hello attacco corrente e impedire attacchi futuri</span><span class="sxs-lookup"><span data-stu-id="590ae-135">Suggests ways toostop hello current attack and help prevent future attacks</span></span> |

## <a name="introductory-walkthrough"></a><span data-ttu-id="590ae-136">Procedura dettagliata introduttiva</span><span class="sxs-lookup"><span data-stu-id="590ae-136">Introductory walkthrough</span></span>

> [!NOTE]
> <span data-ttu-id="590ae-137">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="590ae-137">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="590ae-138">Questo argomento non costituisce una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="590ae-138">This document is not a step-by-step guide.</span></span>
>
>

 <span data-ttu-id="590ae-139">Tramite il Centro sicurezza PC hello [portale di Azure](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="590ae-139">You access Security Center from hello [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="590ae-140">[Accedi al portale toohello](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="590ae-140">[Sign in toohello portal](https://portal.azure.com).</span></span> <span data-ttu-id="590ae-141">Nel menu del portale principale hello, scorrere toohello **Centro sicurezza PC** opzione o seleziona hello **Centro sicurezza PC** riquadro che è stato aggiunto in precedenza toohello dashboard del portale.</span><span class="sxs-lookup"><span data-stu-id="590ae-141">Under hello main portal menu, scroll toohello **Security Center** option or select hello **Security Center** tile that you previously pinned toohello portal dashboard.</span></span>

![Riquadro Sicurezza nel portale di Azure][1]

<span data-ttu-id="590ae-143">Nel Centro sicurezza è possibile impostare i criteri di sicurezza, monitorare le configurazioni di sicurezza e visualizzare gli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="590ae-143">From Security Center, you can set security policies, monitor security configurations, and view security alerts.</span></span>

### <a name="security-policies"></a><span data-ttu-id="590ae-144">Criteri di sicurezza</span><span class="sxs-lookup"><span data-stu-id="590ae-144">Security policies</span></span>
<span data-ttu-id="590ae-145">È possibile definire i criteri per le sottoscrizioni di Azure in base a requisiti di sicurezza della società tooyour.</span><span class="sxs-lookup"><span data-stu-id="590ae-145">You can define policies for your Azure subscriptions according tooyour company's security requirements.</span></span> <span data-ttu-id="590ae-146">È inoltre possibile personalizzare tali toohello tipi di applicazioni in uso o toohello riservatezza dei dati hello in ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="590ae-146">You can also tailor them toohello types of applications you're using or toohello sensitivity of hello data in each subscription.</span></span> <span data-ttu-id="590ae-147">Ad esempio, le risorse usate per lo sviluppo o il test possono avere requisiti di sicurezza diversi da quelli delle applicazioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="590ae-147">For example, resources used for development or testing may have different security requirements than those used for production applications.</span></span> <span data-ttu-id="590ae-148">Allo stesso modo, le applicazioni con dati regolamentati, come le informazioni personali, possono richiedere un livello di sicurezza più elevato.</span><span class="sxs-lookup"><span data-stu-id="590ae-148">Likewise, applications with regulated data like PII may require a higher level of security.</span></span>

> [!NOTE]
> <span data-ttu-id="590ae-149">toomodify un criterio di sicurezza, è necessario essere di un'amministratore della sicurezza hello sottoscrizione o proprietario o collaboratore.</span><span class="sxs-lookup"><span data-stu-id="590ae-149">toomodify a security policy, you must be a Security Administrator or hello subscription's Owner or Contributor.</span></span> <span data-ttu-id="590ae-150">toolearn ulteriori informazioni sui ruoli e le operazioni consentite in Centro sicurezza PC, vedere [autorizzazioni nel Centro protezione Azure](security-center-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="590ae-150">toolearn more about roles and allowed actions in Security Center, see [Permissions in Azure Security Center](security-center-permissions.md).</span></span>
>
>

<span data-ttu-id="590ae-151">In hello **Centro sicurezza PC** blade, seleziona hello **criteri** riquadro per un elenco delle sottoscrizioni e dei gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="590ae-151">On hello **Security Center** blade, select hello **Policy** tile for a list of your subscriptions and resource groups.</span></span>   

![Pannello Centro sicurezza][2]

<span data-ttu-id="590ae-153">In hello **criteri di sicurezza** pannello selezionare un criterio dettagli di sottoscrizione tooview hello.</span><span class="sxs-lookup"><span data-stu-id="590ae-153">On hello **Security policy** blade, select a subscription tooview hello policy details.</span></span>

<span data-ttu-id="590ae-154">**Raccolta dati** abilita la raccolta dei dati per i criteri di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="590ae-154">**Data collection** enables data collection for a security policy.</span></span> <span data-ttu-id="590ae-155">L'abilitazione fornisce:</span><span class="sxs-lookup"><span data-stu-id="590ae-155">Enabling provides:</span></span>

* <span data-ttu-id="590ae-156">Analisi giornaliera di tutte le macchine virtuali (VM) supportate per il monitoraggio della sicurezza e le raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="590ae-156">Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.</span></span>
* <span data-ttu-id="590ae-157">Raccolta di eventi di sicurezza per l'analisi e il rilevamento delle minacce.</span><span class="sxs-lookup"><span data-stu-id="590ae-157">Collection of security events for analysis and threat detection.</span></span>

> [!NOTE]
> <span data-ttu-id="590ae-158">Raccolta dei dati è configurata a livello di sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="590ae-158">Data collection is configured at hello subscription level.</span></span>
>
>

<span data-ttu-id="590ae-159">Selezionare **criteri di prevenzione** tooopen hello **criteri di prevenzione** blade.</span><span class="sxs-lookup"><span data-stu-id="590ae-159">Select **Prevention policy** tooopen hello **Prevention policy** blade.</span></span> <span data-ttu-id="590ae-160">**Mostra i consigli per** consente di scegliere i controlli di sicurezza hello che si desidera toomonitor e hello raccomandazioni che si desidera toosee in base alle esigenze di sicurezza hello di risorse hello sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="590ae-160">**Show recommendations for** lets you choose hello security controls that you want toomonitor and hello recommendations that you want toosee based on hello security needs of hello resources within hello subscription.</span></span>

### <a name="security-recommendations"></a><span data-ttu-id="590ae-161">Suggerimenti per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="590ae-161">Security recommendations</span></span>
 <span data-ttu-id="590ae-162">Centro sicurezza PC analizza lo stato di sicurezza hello le risorse di Azure tooidentify potenziali vulnerabilità della protezione.</span><span class="sxs-lookup"><span data-stu-id="590ae-162">Security Center analyzes hello security state of your Azure resources tooidentify potential security vulnerabilities.</span></span> <span data-ttu-id="590ae-163">Un elenco di suggerimenti in modo semplificato il processo di hello di configurazione di controlli necessari.</span><span class="sxs-lookup"><span data-stu-id="590ae-163">A list of recommendations guides you through hello process of configuring needed controls.</span></span> <span data-ttu-id="590ae-164">Tra gli esempi sono inclusi:</span><span class="sxs-lookup"><span data-stu-id="590ae-164">Examples include:</span></span>

* <span data-ttu-id="590ae-165">Provisioning antimalware toohelp identificare e rimuovere il software dannoso</span><span class="sxs-lookup"><span data-stu-id="590ae-165">Provisioning antimalware toohelp identify and remove malicious software</span></span>
* <span data-ttu-id="590ae-166">Configurazione di rete sicurezza e gruppi di regole toocontrol traffico tooVMs</span><span class="sxs-lookup"><span data-stu-id="590ae-166">Configuring network security groups and rules toocontrol traffic tooVMs</span></span>
* <span data-ttu-id="590ae-167">Il provisioning dei firewall applicazione web toohelp difendersi da attacchi che le applicazioni web di destinazione</span><span class="sxs-lookup"><span data-stu-id="590ae-167">Provisioning of web application firewalls toohelp defend against attacks that target your web applications</span></span>
* <span data-ttu-id="590ae-168">Distribuzione degli aggiornamenti di sistema mancanti</span><span class="sxs-lookup"><span data-stu-id="590ae-168">Deploying missing system updates</span></span>
* <span data-ttu-id="590ae-169">Indirizzamento delle configurazioni del sistema operativo che non corrispondono a hello consiglia le linee di base</span><span class="sxs-lookup"><span data-stu-id="590ae-169">Addressing OS configurations that do not match hello recommended baselines</span></span>

<span data-ttu-id="590ae-170">Fare clic su hello **indicazioni** riquadro per un elenco di indicazioni.</span><span class="sxs-lookup"><span data-stu-id="590ae-170">Click hello **Recommendations** tile for a list of recommendations.</span></span> <span data-ttu-id="590ae-171">Fare clic su ogni raccomandazione tooview ulteriori informazioni o un problema di hello tootake azione tooresolve.</span><span class="sxs-lookup"><span data-stu-id="590ae-171">Click each recommendation tooview additional information or tootake action tooresolve hello issue.</span></span>

![Raccomandazioni di sicurezza nel Centro sicurezza di Azure][5]

### <a name="security-state-of-azure-resources"></a><span data-ttu-id="590ae-173">Stato di sicurezza delle risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="590ae-173">Security state of Azure resources</span></span>
<span data-ttu-id="590ae-174">Hello **prevenzione** sezione dashboard hello Mostra hello generali di sicurezza dell'ambiente hello dal tipo di risorsa, tra cui le macchine virtuali, applicazioni web e altre risorse.</span><span class="sxs-lookup"><span data-stu-id="590ae-174">hello **Prevention** section of hello dashboard shows hello overall security posture of hello environment by resource type, including VMs, web applications, and other resources.</span></span>   

<span data-ttu-id="590ae-175">Selezionare un tipo di risorsa in **prevenzione** tooview ulteriori informazioni, incluso un elenco di qualsiasi potenziali vulnerabilità di sicurezza che sono stati identificati.</span><span class="sxs-lookup"><span data-stu-id="590ae-175">Select a resource type under **Prevention** tooview more information, including a list of any potential security vulnerabilities that have been identified.</span></span> <span data-ttu-id="590ae-176">(**Calcolo** sia selezionata nel seguente esempio hello.)</span><span class="sxs-lookup"><span data-stu-id="590ae-176">(**Compute** is selected in hello example below.)</span></span>

![Riquadro Integrità delle risorse][6]

### <a name="security-alerts"></a><span data-ttu-id="590ae-178">Avvisi di sicurezza</span><span class="sxs-lookup"><span data-stu-id="590ae-178">Security alerts</span></span>
 <span data-ttu-id="590ae-179">Centro sicurezza PC automaticamente raccoglie, analizza e consente di integrare dati di log da risorse di Azure, rete hello e soluzioni partner come programmi antimalware e firewall.</span><span class="sxs-lookup"><span data-stu-id="590ae-179">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and partner solutions like antimalware programs and firewalls.</span></span> <span data-ttu-id="590ae-180">Quando vengono rilevate minacce, viene creato un avviso di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="590ae-180">When threats are detected, a security alert is created.</span></span> <span data-ttu-id="590ae-181">Ad esempio, è compreso il rilevamento di:</span><span class="sxs-lookup"><span data-stu-id="590ae-181">Examples include detection of:</span></span>

* <span data-ttu-id="590ae-182">VM compromesse in comunicazione con indirizzi IP dannosi noti</span><span class="sxs-lookup"><span data-stu-id="590ae-182">Compromised VMs communicating with known malicious IP addresses</span></span>
* <span data-ttu-id="590ae-183">Malware avanzato rilevato tramite Segnalazione errori Windows</span><span class="sxs-lookup"><span data-stu-id="590ae-183">Advanced malware detected by using Windows error reporting</span></span>
* <span data-ttu-id="590ae-184">Attacchi di forza bruta alle VM</span><span class="sxs-lookup"><span data-stu-id="590ae-184">Brute force attacks against VMs</span></span>
* <span data-ttu-id="590ae-185">Avvisi di sicurezza da programmi antimalware e firewall integrati</span><span class="sxs-lookup"><span data-stu-id="590ae-185">Security alerts from integrated antimalware programs and firewalls</span></span>

<span data-ttu-id="590ae-186">Facendo clic su hello **degli avvisi di sicurezza** riquadro Visualizza un elenco di avvisi con priorità.</span><span class="sxs-lookup"><span data-stu-id="590ae-186">Clicking hello **Security alerts** tile displays a list of prioritized alerts.</span></span>

![Avvisi di sicurezza][7]

<span data-ttu-id="590ae-188">Selezionare un avviso per visualizzare ulteriori informazioni su attacco hello e i suggerimenti su come tooremediate è.</span><span class="sxs-lookup"><span data-stu-id="590ae-188">Selecting an alert shows more information about hello attack and suggestions for how tooremediate it.</span></span>

![Dettagli dell'avviso di sicurezza][8]

### <a name="partner-solutions"></a><span data-ttu-id="590ae-190">Soluzioni partner</span><span class="sxs-lookup"><span data-stu-id="590ae-190">Partner solutions</span></span>
<span data-ttu-id="590ae-191">Hello **soluzioni Partner** riquadro consente di monitorare in uno stato di sicurezza immediatamente hello partner delle soluzioni dell'utente è integrato con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="590ae-191">hello **Partner solutions** tile lets you monitor at a glance hello security state of your partner solutions integrated with your Azure subscription.</span></span> <span data-ttu-id="590ae-192">Centro sicurezza PC consente di visualizzare gli avvisi provenienti da soluzioni hello.</span><span class="sxs-lookup"><span data-stu-id="590ae-192">Security Center displays alerts coming from hello solutions.</span></span>

<span data-ttu-id="590ae-193">Seleziona hello **soluzioni Partner** riquadro.</span><span class="sxs-lookup"><span data-stu-id="590ae-193">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="590ae-194">Viene visualizzato un pannello contenente un elenco di tutte le soluzioni dei partner connessi.</span><span class="sxs-lookup"><span data-stu-id="590ae-194">A blade opens displaying a list of all connected partner solutions.</span></span>

![Soluzioni partner][9]

## <a name="get-started"></a><span data-ttu-id="590ae-196">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="590ae-196">Get started</span></span>
<span data-ttu-id="590ae-197">tooget avviato con il Centro sicurezza PC, è necessario tooMicrosoft una sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="590ae-197">tooget started with Security Center, you need a subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="590ae-198">Il Centro sicurezza viene abilitato con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="590ae-198">Security Center is enabled with your Azure subscription.</span></span> <span data-ttu-id="590ae-199">Se non si ha una sottoscrizione, è possibile iscriversi per una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="590ae-199">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

 <span data-ttu-id="590ae-200">Tramite il Centro sicurezza PC hello [portale di Azure](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="590ae-200">You access Security Center from hello [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="590ae-201">Vedere hello [documentazione portale](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="590ae-201">See hello [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn more.</span></span>

<span data-ttu-id="590ae-202">[Introduzione a Centro sicurezza di Azure](security-center-get-started.md) rapidamente in modo semplificato i componenti di monitoraggio della protezione e gestione dei criteri di hello del Centro sicurezza PC.</span><span class="sxs-lookup"><span data-stu-id="590ae-202">[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through hello security-monitoring and policy-management components of Security Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="590ae-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="590ae-203">Next steps</span></span>
<span data-ttu-id="590ae-204">In questo documento, sono state introdotte tooSecurity Center, le funzionalità chiave e la modalità di avvio tooget.</span><span class="sxs-lookup"><span data-stu-id="590ae-204">In this document, you were introduced tooSecurity Center, its key capabilities, and how tooget started.</span></span> <span data-ttu-id="590ae-205">toolearn informazioni, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="590ae-205">toolearn more, see hello following resources:</span></span>

* <span data-ttu-id="590ae-206">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) , informazioni come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="590ae-206">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="590ae-207">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni facilitano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="590ae-207">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="590ae-208">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="590ae-208">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="590ae-209">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) , informazioni come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="590ae-209">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="590ae-210">[Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="590ae-210">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="590ae-211">[Sicurezza dei dati nel Centro sicurezza di Azure](security-center-data-security.md): informazioni sulla gestione e la protezione dei dati nel Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="590ae-211">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="590ae-212">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="590ae-212">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="590ae-213">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) , ottenere informazioni e notizie sicurezza di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="590ae-213">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
