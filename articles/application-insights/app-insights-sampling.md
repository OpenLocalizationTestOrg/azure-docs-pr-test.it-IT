---
title: campionamento aaaTelemetry in Azure Application Insights | Documenti Microsoft
description: Tookeep hello come volume di dati di telemetria nel controllo.
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="32174-103">Campionamento in Application Insights</span><span class="sxs-lookup"><span data-stu-id="32174-103">Sampling in Application Insights</span></span>


<span data-ttu-id="32174-104">Il campionamento è una funzionalità di [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32174-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="32174-105">È il traffico dati di telemetria in senso tooreduce e archiviazione, hello consigliati mantenendo una corretta analisi dei dati dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="32174-105">It is hello recommended way tooreduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="32174-106">filtro Hello seleziona gli elementi correlati, in modo che è possibile spostarsi tra gli elementi quando si esegue l'analisi diagnostica.</span><span class="sxs-lookup"><span data-stu-id="32174-106">hello filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="32174-107">Quando i conteggi di metrica vengono presentati tooyou nel portale di hello, essi vengono rinormalizzati account tootake di campionamento, toominimize qualsiasi effetto sulle statistiche di hello hello.</span><span class="sxs-lookup"><span data-stu-id="32174-107">When metric counts are presented tooyou in hello portal, they are renormalized tootake account of hello sampling, toominimize any effect on hello statistics.</span></span>

<span data-ttu-id="32174-108">Il campionamento riduce i costi del traffico e dei dati e consente di evitare la limitazione.</span><span class="sxs-lookup"><span data-stu-id="32174-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="32174-109">In breve:</span><span class="sxs-lookup"><span data-stu-id="32174-109">In brief:</span></span>
* <span data-ttu-id="32174-110">Campionamento mantiene 1 in  *n*  registra ed Elimina rest hello.</span><span class="sxs-lookup"><span data-stu-id="32174-110">Sampling retains 1 in *n* records and discards hello rest.</span></span> <span data-ttu-id="32174-111">Ad esempio, potrebbe mantenere 1 un evento su 5, corrispondente a una frequenza di campionamento del 20%.</span><span class="sxs-lookup"><span data-stu-id="32174-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="32174-112">Nelle app server Web ASP.NET, il campionamento viene eseguito automaticamente se l'applicazione invia molti dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="32174-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="32174-113">È inoltre possibile impostare manualmente, campionamento entrambi hello in portale su hello dei prezzi di pagina. oppure in hello SDK ASP.NET nel file config hello, tooalso ridurre il traffico di rete hello.</span><span class="sxs-lookup"><span data-stu-id="32174-113">You can also set sampling manually, either in hello portal on hello pricing page; or in hello ASP.NET SDK in hello .config file, tooalso reduce hello network traffic.</span></span>
* <span data-ttu-id="32174-114">Se si accede a eventi personalizzati e si desidera toomake assicurarsi che un set di eventi viene mantenuto o eliminato insieme, assicurarsi che essi hanno hello stesso valore di ID operazione.</span><span class="sxs-lookup"><span data-stu-id="32174-114">If you log custom events and you want toomake sure that a set of events is either retained or discarded together, make sure that they have hello same OperationId value.</span></span>
* <span data-ttu-id="32174-115">divisore di campionamento Hello  *n*  viene segnalato in ogni record nella proprietà hello `itemCount`, che nella ricerca viene visualizzata sotto hello nome descrittivo "numero di richieste" o "conteggio eventi".</span><span class="sxs-lookup"><span data-stu-id="32174-115">hello sampling divisor *n* is reported in each record in hello property `itemCount`, which in Search appears under hello friendly name "request count" or "event count".</span></span> <span data-ttu-id="32174-116">Quando il campionamento non è in esecuzione, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="32174-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="32174-117">Se si scrivono query di Dati di analisi, è necessario [tener conto del campionamento](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="32174-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="32174-118">In particolare, anziché eseguire semplicemente il conteggio dei record, è necessario usare `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="32174-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="32174-119">Tipi di campionamento</span><span class="sxs-lookup"><span data-stu-id="32174-119">Types of sampling</span></span>
<span data-ttu-id="32174-120">Esistono tre diversi metodi di campionamento:</span><span class="sxs-lookup"><span data-stu-id="32174-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="32174-121">**Campionamento adattivo** regola automaticamente il volume di hello di telemetria inviato da hello SDK nell'applicazione ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="32174-121">**Adaptive sampling** automatically adjusts hello volume of telemetry sent from hello SDK in your ASP.NET app.</span></span> <span data-ttu-id="32174-122">Si tratta di un'opzione predefinita dell'SDK versione 2.0.0-beta3.</span><span class="sxs-lookup"><span data-stu-id="32174-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="32174-123">Attualmente disponibile solo per la telemetria lato server di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="32174-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="32174-124">**Campionamento tasso fisso** ridurre hello volume di dati di telemetria inviati da entrambi i server ASP.NET e i browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="32174-124">**Fixed-rate sampling** reduces hello volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="32174-125">Impostare la frequenza di hello.</span><span class="sxs-lookup"><span data-stu-id="32174-125">You set hello rate.</span></span> <span data-ttu-id="32174-126">Hello client e server eseguirà la sincronizzazione loro campionamento in modo che, nella ricerca, è possibile spostarsi tra le visualizzazioni pagina correlati e richieste.</span><span class="sxs-lookup"><span data-stu-id="32174-126">hello client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="32174-127">**Campionamento inserimento** funziona in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="32174-127">**Ingestion sampling** works in hello Azure portal.</span></span> <span data-ttu-id="32174-128">Vengono rimossi alcuni dei dati di telemetria hello in arrivo dall'app, a una velocità è impostata.</span><span class="sxs-lookup"><span data-stu-id="32174-128">It discards some of hello telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="32174-129">Non riduce il traffico di telemetria, ma consente all'utente di rispettare la quota mensile.</span><span class="sxs-lookup"><span data-stu-id="32174-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="32174-130">Hello grande vantaggio offerto dal campionamento di inserimento è che è possibile impostarlo senza ridistribuire l'applicazione e funziona in modo uniforme per tutti i server e client.</span><span class="sxs-lookup"><span data-stu-id="32174-130">hello big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="32174-131">Se è in esecuzione il campionamento adattivo o a frequenza fissa, il campionamento per inserimento è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="32174-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="32174-132">Campionamento per inserimento</span><span class="sxs-lookup"><span data-stu-id="32174-132">Ingestion sampling</span></span>
<span data-ttu-id="32174-133">Questo modulo di campionamento opera a punto hello in dati di telemetria hello dal server web, browser e dispositivi raggiunge l'endpoint del servizio Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="32174-133">This form of sampling operates at hello point where hello telemetry from your web server, browsers, and devices reaches hello Application Insights service endpoint.</span></span> <span data-ttu-id="32174-134">Anche se non ridurre il traffico di dati di telemetria hello inviato dall'app, riduce la quantità hello elaborati e mantenuti (e addebitato) da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="32174-134">Although it doesn't reduce hello telemetry traffic sent from your app, it does reduce hello amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="32174-135">Se l'app passa spesso superamento della quota mensile e non è necessario scegliere hello di utilizzare uno dei tipi di base SDK hello di campionamento, utilizzare questo tipo di campionamento.</span><span class="sxs-lookup"><span data-stu-id="32174-135">Use this type of sampling if your app often goes over its monthly quota and you don't have hello option of using either of hello SDK-based types of sampling.</span></span> 

<span data-ttu-id="32174-136">Impostare la frequenza di campionamento hello in hello quote e prezzi pannello:</span><span class="sxs-lookup"><span data-stu-id="32174-136">Set hello sampling rate in hello Quotas and Pricing blade:</span></span>

![Dal pannello della panoramica applicazione hello, fare clic su impostazioni di Quota, esempi, quindi selezionare una frequenza di campionamento e fare clic su Aggiorna.](./media/app-insights-sampling/04.png)

<span data-ttu-id="32174-138">Gli altri tipi di campionamento di algoritmo hello mantiene gli elementi di dati di telemetria correlati.</span><span class="sxs-lookup"><span data-stu-id="32174-138">Like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="32174-139">Ad esempio, quando si sta controllando telemetria hello nella ricerca, sarà possibile richiesta hello toofind correlati tooa particolare eccezione.</span><span class="sxs-lookup"><span data-stu-id="32174-139">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> <span data-ttu-id="32174-140">I conteggi di metrica, ad esempio la frequenza delle richieste e delle eccezioni, vengono mantenuti correttamente.</span><span class="sxs-lookup"><span data-stu-id="32174-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="32174-141">I punti dati che vengono rimossi dal campionamento non sono disponibili in alcuna funzionalità di Application Insights, ad esempio nell' [esportazione continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="32174-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="32174-142">Il campionamento per inserimento non funziona mentre è attivo il campionamento a frequenza fissa o adattivo basato sull'SDK.</span><span class="sxs-lookup"><span data-stu-id="32174-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="32174-143">Se la frequenza di campionamento hello in hello SDK è inferiore al 100%, quindi hello frequenza di campionamento inserimento impostate viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="32174-143">If hello sampling rate at hello SDK is less than 100%, then hello ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="32174-144">valore Hello visualizzato sul riquadro hello indica i valori hello impostati per il campionamento di inserimento.</span><span class="sxs-lookup"><span data-stu-id="32174-144">hello value shown on hello tile indicates hello value that you set for ingestion sampling.</span></span> <span data-ttu-id="32174-145">Non ha una frequenza di campionamento effettivo hello se campionamento SDK è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="32174-145">It doesn't represent hello actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="32174-146">Campionamento adattivo nel server Web</span><span class="sxs-lookup"><span data-stu-id="32174-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="32174-147">Campionamento adattivo è disponibile per hello Application Insights SDK per ASP.NET v 2.0.0-beta3 e versioni successive ed è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="32174-147">Adaptive sampling is available for hello Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="32174-148">Campionamento adattivo influisce sul volume hello di telemetria inviato da toohello di app del server web del servizio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="32174-148">Adaptive sampling affects hello volume of telemetry sent from your web server app toohello Application Insights service.</span></span> <span data-ttu-id="32174-149">Hello volume viene regolato automaticamente tookeep all'interno di una frequenza massima specificata del traffico.</span><span class="sxs-lookup"><span data-stu-id="32174-149">hello volume is adjusted automatically tookeep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="32174-150">Non opera a bassi volumi di dati di telemetria, pertanto un'app per eseguire il debug o un sito Web con un basso utilizzo non saranno interessate.</span><span class="sxs-lookup"><span data-stu-id="32174-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="32174-151">volume di destinazione hello tooachieve, alcuni dei dati di telemetria hello generato viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="32174-151">tooachieve hello target volume, some of hello telemetry generated is discarded.</span></span> <span data-ttu-id="32174-152">Ma gli altri tipi di campionamento di algoritmo hello mantiene gli elementi di dati di telemetria correlati.</span><span class="sxs-lookup"><span data-stu-id="32174-152">But like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="32174-153">Ad esempio, quando si sta controllando telemetria hello nella ricerca, sarà possibile richiesta hello toofind correlati tooa particolare eccezione.</span><span class="sxs-lookup"><span data-stu-id="32174-153">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> 

<span data-ttu-id="32174-154">Consente di contare metrica, ad esempio tasso di richiesta e il tasso di eccezione sono toocompensate adattata per hello, frequenza di campionamento in modo che siano visualizzati valori circa corretti in Esplora metriche.</span><span class="sxs-lookup"><span data-stu-id="32174-154">Metric counts such as request rate and exception rate are adjusted toocompensate for hello sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="32174-155">**Aggiornamento NuGet del progetto** pacchetti toohello più recente *pre-release* versione di Application Insights: fare clic sul progetto hello in Esplora soluzioni, scegliere Gestisci pacchetti NuGet controllare **inclusione versione non definitiva** e cercare Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="32174-155">**Update your project's NuGet** packages toohello latest *pre-release* version of Application Insights: Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="32174-156">In [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), è possibile modificare vari parametri in hello `AdaptiveSamplingTelemetryProcessor` nodo.</span><span class="sxs-lookup"><span data-stu-id="32174-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in hello `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="32174-157">cifre Hello indicate sono valori predefiniti di hello:</span><span class="sxs-lookup"><span data-stu-id="32174-157">hello figures shown are hello default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="32174-158">Hello velocità di destinazione che hello algoritmo adattivo ha come obiettivo **in ogni host server**.</span><span class="sxs-lookup"><span data-stu-id="32174-158">hello target rate that hello adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="32174-159">Se l'app web viene eseguito il numero di host, è possibile ridurre in modo da tooremain entro la frequenza di destinazione del traffico nel portale Application Insights hello questo valore.</span><span class="sxs-lookup"><span data-stu-id="32174-159">If your web app runs on many hosts, reduce this value so as tooremain within your target rate of traffic at hello Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="32174-160">intervallo di Hello in cui hello viene rivalutato quantità attuale di telemetria.</span><span class="sxs-lookup"><span data-stu-id="32174-160">hello interval at which hello current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="32174-161">La valutazione viene eseguita come media mobile.</span><span class="sxs-lookup"><span data-stu-id="32174-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="32174-162">È possibile tooshorten questo intervallo se i dati di telemetria è ritenuta toosudden picchi.</span><span class="sxs-lookup"><span data-stu-id="32174-162">You might want tooshorten this interval if your telemetry is liable toosudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="32174-163">Quando le modifiche valore percentuale di campionamento, dopo quanto tempo dopo che sono è consentito il campionamento percentuale nuovamente toolower toocapture meno dati.</span><span class="sxs-lookup"><span data-stu-id="32174-163">When sampling percentage value changes, how soon after are we allowed toolower sampling percentage again toocapture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="32174-164">Quando le modifiche valore percentuale di campionamento, dopo quanto tempo dopo che sono è consentito il campionamento percentuale nuovamente tooincrease toocapture più dati.</span><span class="sxs-lookup"><span data-stu-id="32174-164">When sampling percentage value changes, how soon after are we allowed tooincrease sampling percentage again toocapture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="32174-165">Campionamento percentuale in base alla variazione, che cos'è il valore minimo di hello ci stiamo consentiti tooset.</span><span class="sxs-lookup"><span data-stu-id="32174-165">As sampling percentage varies, what is hello minimum value we're allowed tooset.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="32174-166">Campionamento percentuale in base alla variazione, che cos'è il valore massimo di hello ci stiamo consentiti tooset.</span><span class="sxs-lookup"><span data-stu-id="32174-166">As sampling percentage varies, what is hello maximum value we're allowed tooset.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="32174-167">Nel calcolo della media mobile hello hello peso hello assegnato toohello il valore più recente.</span><span class="sxs-lookup"><span data-stu-id="32174-167">In hello calculation of hello moving average, hello weight assigned toohello most recent value.</span></span> <span data-ttu-id="32174-168">Utilizzare un tooor uguale valore minore di 1.</span><span class="sxs-lookup"><span data-stu-id="32174-168">Use a value equal tooor less than 1.</span></span> <span data-ttu-id="32174-169">I valori minori modificare algoritmo hello meno reattivi toosudden.</span><span class="sxs-lookup"><span data-stu-id="32174-169">Smaller values make hello algorithm less reactive toosudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="32174-170">valore di Hello assegnato quando l'applicazione hello ha iniziato.</span><span class="sxs-lookup"><span data-stu-id="32174-170">hello value assigned when hello app has just started.</span></span> <span data-ttu-id="32174-171">Non ridurlo durante il debug.</span><span class="sxs-lookup"><span data-stu-id="32174-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="32174-172">Elenco di tipi che non si desidera toobe campionate delimitate da un punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="32174-172">A semi-colon delimited list of types that you do not want toobe sampled.</span></span> <span data-ttu-id="32174-173">I tipi riconosciuti sono: dipendenza, evento, eccezione, pageview, richiesta, traccia.</span><span class="sxs-lookup"><span data-stu-id="32174-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="32174-174">Tutte le istanze di hello specificato vengono trasmessi tipi; tipi di Hello non specificati vengono campionati.</span><span class="sxs-lookup"><span data-stu-id="32174-174">All instances of hello specified types are transmitted; hello types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="32174-175">Elenco di tipi che si desidera toobe campionate delimitate da un punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="32174-175">A semi-colon delimited list of types that you want toobe sampled.</span></span> <span data-ttu-id="32174-176">I tipi riconosciuti sono: dipendenza, evento, eccezione, pageview, richiesta, traccia.</span><span class="sxs-lookup"><span data-stu-id="32174-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="32174-177">Hello specificato vengono campionati tipi; tutte le istanze di hello sempre da trasmettere altri tipi.</span><span class="sxs-lookup"><span data-stu-id="32174-177">hello specified types are sampled; all instances of hello other types will always be transmitted.</span></span>


<span data-ttu-id="32174-178">**tooswitch off** campionamento adattivo, Rimuovi hello AdaptiveSamplingTelemetryProcessor nodo dalla configurazione di applicationinsights.</span><span class="sxs-lookup"><span data-stu-id="32174-178">**tooswitch off** adaptive sampling, remove hello AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="32174-179">Alternativa: configurare il campionamento adattivo nel codice</span><span class="sxs-lookup"><span data-stu-id="32174-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="32174-180">Anziché regolare campionamento nel file hello. config, è possibile utilizzare codice.</span><span class="sxs-lookup"><span data-stu-id="32174-180">Instead of adjusting sampling in hello .config file, you can use code.</span></span> <span data-ttu-id="32174-181">In questo modo è una funzione di callback che viene richiamata ogni volta che la frequenza di campionamento hello viene rivalutata toospecify.</span><span class="sxs-lookup"><span data-stu-id="32174-181">This allows you toospecify a callback function that is invoked whenever hello sampling rate is re-evaluated.</span></span> <span data-ttu-id="32174-182">Si può usare, ad esempio, viene utilizzato toofind out la frequenza di campionamento.</span><span class="sxs-lookup"><span data-stu-id="32174-182">You could use this, for example, toofind out what sampling rate is being used.</span></span>

<span data-ttu-id="32174-183">Rimuovere hello `AdaptiveSamplingTelemetryProcessor` nodo da file hello. config.</span><span class="sxs-lookup"><span data-stu-id="32174-183">Remove hello `AdaptiveSamplingTelemetryProcessor` node from hello .config file.</span></span>

<span data-ttu-id="32174-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="32174-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="32174-185">([Informazioni sui processori di telemetria](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="32174-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="32174-186">Campionamento per pagine Web con JavaScript</span><span class="sxs-lookup"><span data-stu-id="32174-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="32174-187">È possibile configurare le pagine Web per il campionamento a frequenza fissa da qualsiasi server.</span><span class="sxs-lookup"><span data-stu-id="32174-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="32174-188">Quando si [configurare le pagine web hello per Application Insights](app-insights-javascript.md), modificare il frammento hello che vengono recuperate dal portale Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="32174-188">When you [configure hello web pages for Application Insights](app-insights-javascript.md), modify hello snippet that you get from hello Application Insights portal.</span></span> <span data-ttu-id="32174-189">(In applicazioni ASP.NET, frammento di codice hello in genere viene inserito in layout. cshtml.)  Inserire una riga simile `samplingPercentage: 10,` prima chiave di strumentazione hello:</span><span class="sxs-lookup"><span data-stu-id="32174-189">(In ASP.NET apps, hello snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before hello instrumentation key:</span></span>

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

<span data-ttu-id="32174-190">Per percentuale di campionamento hello, scegliere una percentuale Chiudi too100/N dove N è un numero intero.</span><span class="sxs-lookup"><span data-stu-id="32174-190">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="32174-191">Il campionamento attualmente non supporta altri valori.</span><span class="sxs-lookup"><span data-stu-id="32174-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="32174-192">È inoltre possibile abilitare il campionamento tasso fisso nel server di hello, server e client hello verranno sincronizzate in modo che, nella ricerca, è possibile spostarsi tra le visualizzazioni pagina correlati e richieste.</span><span class="sxs-lookup"><span data-stu-id="32174-192">If you also enable fixed-rate sampling at hello server, hello clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="32174-193">Campionamento a frequenza fissa per siti Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="32174-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="32174-194">Tasso fisso campionamento riduce il traffico di hello inviato dal server web e i browser web.</span><span class="sxs-lookup"><span data-stu-id="32174-194">Fixed rate sampling reduces hello traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="32174-195">A differenza del campionamento adattivo, riduce i dati di telemetria a una frequenza fissa definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="32174-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="32174-196">Sincronizza inoltre hello client e il campionamento di server in modo che vengono mantenuti gli elementi correlati, ad esempio, in modo che se si esamina una visualizzazione di pagina nella ricerca, è possibile trovare la richiesta correlata.</span><span class="sxs-lookup"><span data-stu-id="32174-196">It also synchronizes hello client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="32174-197">algoritmo di campionamento Hello mantiene gli elementi correlati.</span><span class="sxs-lookup"><span data-stu-id="32174-197">hello sampling algorithm retains related items.</span></span> <span data-ttu-id="32174-198">Per ciascun evento di richiesta HTTP, l'algoritmo e gli eventi correlati vengono eliminati o trasmessi.</span><span class="sxs-lookup"><span data-stu-id="32174-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="32174-199">In Esplora metriche, velocità, ad esempio conteggi di richiesta e l'eccezione sono moltiplicato per toocompensate un fattore per la frequenza di campionamento di hello, in modo che siano circa corretti.</span><span class="sxs-lookup"><span data-stu-id="32174-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor toocompensate for hello sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="32174-200">**Aggiornare i pacchetti NuGet del progetto** toohello più recente *definitive* versione di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="32174-200">**Update your project's NuGet packages** toohello latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="32174-201">Fare clic sul progetto hello in Esplora soluzioni, scegliere Gestisci pacchetti NuGet, controllare **Includi versione preliminare** e cercare Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="32174-201">Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="32174-202">**Disabilitare il campionamento adattivo**: In [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), rimuovere o impostare come commento hello `AdaptiveSamplingTelemetryProcessor` nodo.</span><span class="sxs-lookup"><span data-stu-id="32174-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out hello `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="32174-203">**Abilita il modulo di campionamento tasso fisso hello.**</span><span class="sxs-lookup"><span data-stu-id="32174-203">**Enable hello fixed-rate sampling module.**</span></span> <span data-ttu-id="32174-204">Aggiungere questo frammento troppo[Applicationinsights](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="32174-204">Add this snippet too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="32174-205">Per percentuale di campionamento hello, scegliere una percentuale Chiudi too100/N dove N è un numero intero.</span><span class="sxs-lookup"><span data-stu-id="32174-205">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="32174-206">Il campionamento attualmente non supporta altri valori.</span><span class="sxs-lookup"><span data-stu-id="32174-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="32174-207">Alternativa: abilitare il campionamento a frequenza fissa nel codice del server locale</span><span class="sxs-lookup"><span data-stu-id="32174-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="32174-208">Anziché impostare il parametro di campionamento hello nel file hello. config, è possibile utilizzare codice.</span><span class="sxs-lookup"><span data-stu-id="32174-208">Instead of setting hello sampling parameter in hello .config file, you can use code.</span></span> 

<span data-ttu-id="32174-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="32174-209">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="32174-210">([Informazioni sui processori di telemetria](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="32174-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-toouse-sampling"></a><span data-ttu-id="32174-211">Quando il campionamento toouse?</span><span class="sxs-lookup"><span data-stu-id="32174-211">When toouse sampling?</span></span>
<span data-ttu-id="32174-212">Campionamento adattivo è abilitato automaticamente se si utilizza hello 2.0.0-beta3 versione ASP.NET SDK o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="32174-212">Adaptive sampling is automatically enabled if you use hello ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="32174-213">Nel server Microsoft è possibile usare il campionamento per inserimento indipendentemente dalla versione dell'SDK in uso.</span><span class="sxs-lookup"><span data-stu-id="32174-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="32174-214">Per la maggior parte delle applicazioni di piccole e medie dimensioni, il campionamento non è necessario.</span><span class="sxs-lookup"><span data-stu-id="32174-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="32174-215">raccogliendo i dati in tutte le attività utente si ottengono informazioni di diagnostica utili Hello e statistiche più accurate.</span><span class="sxs-lookup"><span data-stu-id="32174-215">hello most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="32174-216">vantaggi principali di Hello di campionamento sono:</span><span class="sxs-lookup"><span data-stu-id="32174-216">hello main advantages of sampling are:</span></span>

* <span data-ttu-id="32174-217">Il servizio Application Insights rimuove ("limita") i punti dati quando l'app invia una frequenza di telemetria molto elevata in un breve intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="32174-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="32174-218">tookeep all'interno di hello [quota](app-insights-pricing.md) di punti dati per il piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="32174-218">tookeep within hello [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="32174-219">traffico di rete tooreduce dalla raccolta hello di telemetria.</span><span class="sxs-lookup"><span data-stu-id="32174-219">tooreduce network traffic from hello collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="32174-220">Quale tipo di campionamento è opportuno usare?</span><span class="sxs-lookup"><span data-stu-id="32174-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="32174-221">**Usare il campionamento per inserimento se:**</span><span class="sxs-lookup"><span data-stu-id="32174-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="32174-222">Si supera spesso la quota mensile dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="32174-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="32174-223">Si utilizza una versione di hello SDK che non supporta il campionamento - ad esempio, hello SDK per Java o nelle versioni ASP.NET precedenti a 2.</span><span class="sxs-lookup"><span data-stu-id="32174-223">You're using a version of hello SDK that doesn't support sampling - for example, hello Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="32174-224">Si ricevono grandi quantità di dati di telemetria dal Web browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="32174-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="32174-225">**Usare il campionamento a frequenza fissa se:**</span><span class="sxs-lookup"><span data-stu-id="32174-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="32174-226">Si usa hello Application Insights SDK per la versione di servizi web ASP.NET 2.0.0 o versioni successive, e</span><span class="sxs-lookup"><span data-stu-id="32174-226">You're using hello Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="32174-227">Si desidera campionamento sincronizzato tra client e server, in modo che, quando si sta verificando gli eventi in [ricerca](app-insights-diagnostic-search.md), è possibile spostarsi tra gli eventi correlati nel client hello e server, ad esempio le visualizzazioni di pagina e le richieste http.</span><span class="sxs-lookup"><span data-stu-id="32174-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on hello client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="32174-228">Si è certi della percentuale di hello campionamento appropriato per l'app.</span><span class="sxs-lookup"><span data-stu-id="32174-228">You are confident of hello appropriate sampling percentage for your app.</span></span> <span data-ttu-id="32174-229">Deve essere sufficientemente alto tooget metriche precise, ma di seguito hello frequenza che supera la quota di determinazione dei prezzi e hello limitazioni.</span><span class="sxs-lookup"><span data-stu-id="32174-229">It should be high enough tooget accurate metrics, but below hello rate that exceeds your pricing quota and hello throttling limits.</span></span> 

<span data-ttu-id="32174-230">**Usare il campionamento adattivo:**</span><span class="sxs-lookup"><span data-stu-id="32174-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="32174-231">In caso contrario, è consigliabile il campionamento adattivo.</span><span class="sxs-lookup"><span data-stu-id="32174-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="32174-232">Questa opzione è abilitata per impostazione predefinita nel server ASP.NET hello SDK, versione 2.0.0-beta3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="32174-232">This is enabled by default in hello ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="32174-233">Non riduce il traffico fino a una determinata frequenza minima, in modo da non avere effetto su un sito poco usato.</span><span class="sxs-lookup"><span data-stu-id="32174-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="32174-234">Come è possibile sapere se il campionamento è in esecuzione?</span><span class="sxs-lookup"><span data-stu-id="32174-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="32174-235">hello toodiscover effettivo campionamento frequenza indipendentemente da dove è stato applicato, usare un [query Analitica](app-insights-analytics.md) simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="32174-235">toodiscover hello actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="32174-236">In ogni mantenuti record, `itemCount` indica il numero di hello di record originali che esso rappresenta, too1 uguale + il numero di hello di record scartati precedente.</span><span class="sxs-lookup"><span data-stu-id="32174-236">In each retained record, `itemCount` indicates hello number of original records that it represents, equal too1 + hello number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="32174-237">Come funziona il campionamento?</span><span class="sxs-lookup"><span data-stu-id="32174-237">How does sampling work?</span></span>
<span data-ttu-id="32174-238">Tasso fisso e campionamento adattivo sono una funzionalità di hello SDK nelle versioni ASP.NET da partire 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="32174-238">Fixed-rate and adaptive sampling are a feature of hello SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="32174-239">Campionamento di inserimento è una funzionalità del servizio di Application Insights hello e può essere attivo se hello SDK non sta eseguendo il campionamento.</span><span class="sxs-lookup"><span data-stu-id="32174-239">Ingestion sampling is a feature of hello Application Insights service, and can be in operation if hello SDK is not performing sampling.</span></span> 

<span data-ttu-id="32174-240">algoritmo di campionamento Hello decide quali toodrop di elementi di dati di telemetria e quali tookeep quelli (se è in hello SDK o nel servizio di Application Insights hello).</span><span class="sxs-lookup"><span data-stu-id="32174-240">hello sampling algorithm decides which telemetry items toodrop, and which ones tookeep (whether it's in hello SDK or in hello Application Insights service).</span></span> <span data-ttu-id="32174-241">decisione di campionamento Hello è basata su diverse regole finalizzate toopreserve tutti i punti dati correlati tra loro intatto, gestione di un'esperienza di diagnostica in Application Insights affidabile anche con un set di dati ridotto e utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="32174-241">hello sampling decision is based on several rules that aim toopreserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="32174-242">Se, ad esempio, per una richiesta non riuscita l'app invia elementi di telemetria aggiuntivi (come eccezioni e tracce registrate da questa richiesta), il campionamento non dividerà la richiesta e il resto della telemetria,</span><span class="sxs-lookup"><span data-stu-id="32174-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="32174-243">ma conserverà o rimuoverà gli elementi tutti insieme.</span><span class="sxs-lookup"><span data-stu-id="32174-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="32174-244">Di conseguenza, quando si esamina i dettagli della richiesta hello in Application Insights, è possibile visualizzare sempre richiesta hello insieme ai relativi elementi di telemetria associati.</span><span class="sxs-lookup"><span data-stu-id="32174-244">As a result, when you look at hello request details in Application Insights, you can always see hello request along with its associated telemetry items.</span></span> 

<span data-ttu-id="32174-245">Per le applicazioni che definiscono "user" (ovvero, applicazioni web più comuni), decisione di campionamento hello è basata su hash hello dell'id utente di hello, che significa che tutti i dati di telemetria per un determinato utente è mantenuta o eliminata.</span><span class="sxs-lookup"><span data-stu-id="32174-245">For applications that define "user" (that is, most typical web applications), hello sampling decision is based on hello hash of hello user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="32174-246">Per i tipi di applicazioni che non definiscono gli utenti (ad esempio servizi web) hello decisione di campionamento hello è basata su id operazione hello della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="32174-246">For hello types of applications that don't define users (such as web services) hello sampling decision is based on hello operation id of hello request.</span></span> <span data-ttu-id="32174-247">Infine, per gli elementi di dati di telemetria hello che non dispongono di id utente né operazione impostato (ad esempio elementi di dati di telemetria segnalati dal thread asincroni senza alcun contesto http) campionamento acquisisce semplicemente una percentuale di elementi di dati di telemetria di ogni tipo.</span><span class="sxs-lookup"><span data-stu-id="32174-247">Finally, for hello telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="32174-248">Per la presentazione di dati di telemetria indietro tooyou hello Application Insights servizio regola metriche hello da hello stessa percentuale di campionamento che è stato utilizzato in fase di hello della raccolta, toocompensate per hello punti dati mancanti.</span><span class="sxs-lookup"><span data-stu-id="32174-248">When presenting telemetry back tooyou, hello Application Insights service adjusts hello metrics by hello same sampling percentage that was used at hello time of collection, toocompensate for hello missing data points.</span></span> <span data-ttu-id="32174-249">Di conseguenza, quando si esaminano i dati di telemetria hello in Application Insights, gli utenti di hello sono quelli statisticamente corretto delle approssimazioni di numeri reali toohello molto simile.</span><span class="sxs-lookup"><span data-stu-id="32174-249">Hence, when looking at hello telemetry in Application Insights, hello users are seeing statistically correct approximations that are very close toohello real numbers.</span></span>

<span data-ttu-id="32174-250">accuratezza Hello di approssimazione hello dipende in larga misura dalla percentuale di campionamento hello configurato.</span><span class="sxs-lookup"><span data-stu-id="32174-250">hello accuracy of hello approximation largely depends on hello configured sampling percentage.</span></span> <span data-ttu-id="32174-251">Inoltre, l'accuratezza di hello aumenta per le applicazioni che gestiscono un volume elevato di richieste simili in genere da un numero elevato di utenti.</span><span class="sxs-lookup"><span data-stu-id="32174-251">Also, hello accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="32174-252">In hello invece, per le applicazioni che non funzionano con un carico significativo, campionamento non è necessaria perché queste applicazioni possono inviare in genere tutti i relativi dati di telemetria rimanendo entro la quota di hello, senza perdita di dati dalla limitazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="32174-252">On hello other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within hello quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="32174-253">Si noti che Application Insights non di esempio i tipi di dati di telemetria metriche e le sessioni, poiché per questi tipi di riduzione della precisione hello può risultare estremamente indesiderata.</span><span class="sxs-lookup"><span data-stu-id="32174-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in hello precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="32174-254">Campionamento adattivo</span><span class="sxs-lookup"><span data-stu-id="32174-254">Adaptive sampling</span></span>
<span data-ttu-id="32174-255">Campionamento adattivo aggiunge un componente di tale monitor hello velocità di trasmissione corrente dal hello SDK e modifica hello campionamento percentuale tootry toostay all'interno di velocità massima di hello destinazione.</span><span class="sxs-lookup"><span data-stu-id="32174-255">Adaptive sampling adds a component that monitors hello current rate of transmission from hello SDK, and adjusts hello sampling percentage tootry toostay within hello target maximum rate.</span></span> <span data-ttu-id="32174-256">regolazione Hello viene ricalcolata a intervalli regolari e si basa su una media mobile di hello velocità di trasmissione in uscita.</span><span class="sxs-lookup"><span data-stu-id="32174-256">hello adjustment is recalculated at regular intervals, and is based on a moving average of hello outgoing transmission rate.</span></span>

## <a name="sampling-and-hello-javascript-sdk"></a><span data-ttu-id="32174-257">Campionamento e hello SDK per JavaScript</span><span class="sxs-lookup"><span data-stu-id="32174-257">Sampling and hello JavaScript SDK</span></span>
<span data-ttu-id="32174-258">Hello sul lato client (JavaScript) SDK fa parte di campionamento tasso fisso in combinazione con hello sul lato server SDK.</span><span class="sxs-lookup"><span data-stu-id="32174-258">hello client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with hello server-side SDK.</span></span> <span data-ttu-id="32174-259">pagine Hello instrumentato invierà telemetria sul lato client da hello agli stessi utenti per la quale hello sul lato server effettuata decisione troppo "di esempio in."</span><span class="sxs-lookup"><span data-stu-id="32174-259">hello instrumented pages will only send client-side telemetry from hello same users for which hello server-side made its decision too"sample in."</span></span> <span data-ttu-id="32174-260">Questa logica è progettato toomaintain integrità della sessione utente tra lato client e server.</span><span class="sxs-lookup"><span data-stu-id="32174-260">This logic is designed toomaintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="32174-261">Di conseguenza, da un particolare elemento della telemetria in Application Insights è possibile trovare tutti gli altri elementi della telemetria per questa sessione utente.</span><span class="sxs-lookup"><span data-stu-id="32174-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="32174-262">*La telemetria lato e client e server non mostra i campioni coordinati, come descritto sopra.*</span><span class="sxs-lookup"><span data-stu-id="32174-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="32174-263">Verificare di avere abilitato il campionamento a frequenza fissa sia sul server che sul client.</span><span class="sxs-lookup"><span data-stu-id="32174-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="32174-264">Assicurarsi che la versione SDK hello è 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="32174-264">Make sure that hello SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="32174-265">Verificare che si imposta hello stesso campionamento percentuale in hello client e server.</span><span class="sxs-lookup"><span data-stu-id="32174-265">Check that you set hello same sampling percentage in both hello client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="32174-266">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="32174-266">Frequently Asked Questions</span></span>
<span data-ttu-id="32174-267">*Perché il campionamento non è una semplice "raccolta di percentuale X di ogni tipo di telemetria"?*</span><span class="sxs-lookup"><span data-stu-id="32174-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="32174-268">Durante questo metodo di campionamento fornisce con una precisione molto elevata in approssimazioni metrica, causa l'interruzione dati di diagnostica toocorrelate possibilità per utente, sessione e la richiesta, è fondamentale per la diagnostica.</span><span class="sxs-lookup"><span data-stu-id="32174-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability toocorrelate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="32174-269">Il campionamento quindi funziona meglio come logica di "raccolta di tutti gli elementi della telemetria per una percentuale X di utenti dell'app" o di "raccolta di tutta la telemetria per una percentuale X di richieste app".</span><span class="sxs-lookup"><span data-stu-id="32174-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="32174-270">Per gli elementi di dati di telemetria hello non associati alle richieste di hello (ad esempio, l'elaborazione asincrona in background), hello rientrano il backup è troppo "collect X % di tutti gli elementi per ogni tipo di dati di telemetria."</span><span class="sxs-lookup"><span data-stu-id="32174-270">For hello telemetry items not associated with hello requests (such as background asynchronous processing), hello fall back is too"collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="32174-271">*Percentuale di campionamento hello può cambiare nel tempo?*</span><span class="sxs-lookup"><span data-stu-id="32174-271">*Can hello sampling percentage change over time?*</span></span>

* <span data-ttu-id="32174-272">Sì, adattivo campionando gradualmente la percentuale di campionamento di hello, in base a hello attualmente osservata volume di dati di telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="32174-272">Yes, adaptive sampling gradually changes hello sampling percentage, based on hello currently observed volume of hello telemetry.</span></span>

<span data-ttu-id="32174-273">*Se si utilizza il campionamento tasso fisso, come si capisce quali campionamento percentuale funzionerà hello migliore per la mia applicazione?*</span><span class="sxs-lookup"><span data-stu-id="32174-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work hello best for my app?*</span></span>

* <span data-ttu-id="32174-274">È toostart con campionamento adattivo, scoprire cosa valutarlo liquida in (vedere hello sopra domanda), e quindi commutatore toofixed-velocità di campionamento con tale tasso.</span><span class="sxs-lookup"><span data-stu-id="32174-274">One way is toostart with adaptive sampling, find out what rate it settles on (see hello above question), and then switch toofixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="32174-275">In caso contrario, è necessario tooguess.</span><span class="sxs-lookup"><span data-stu-id="32174-275">Otherwise, you have tooguess.</span></span> <span data-ttu-id="32174-276">Analizzare l'utilizzo di dati di telemetria corrente nel AI, osservare qualsiasi limitazione delle richieste che è in corso e stima hello volume di dati di telemetria raccolti hello.</span><span class="sxs-lookup"><span data-stu-id="32174-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate hello volume of hello collected telemetry.</span></span> <span data-ttu-id="32174-277">Questi tre input, nonché il piano tariffario selezionato, è consigliabile quanto desiderato volume hello tooreduce di telemetria raccolti hello.</span><span class="sxs-lookup"><span data-stu-id="32174-277">These three inputs, together with your selected pricing tier, suggest how much you might want tooreduce hello volume of hello collected telemetry.</span></span> <span data-ttu-id="32174-278">Tuttavia, un aumento nel numero hello degli utenti o alcuni altri MAIUSC volume hello di telemetria potrebbe invalidare la stima.</span><span class="sxs-lookup"><span data-stu-id="32174-278">However, an increase in hello number of your users or some other shift in hello volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="32174-279">*Cosa accade se si configura una percentuale di campionamento troppo bassa?*</span><span class="sxs-lookup"><span data-stu-id="32174-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="32174-280">Percentuale di campionamento eccessivamente basso (campionamento over-aggressive) riduce accuratezza hello delle approssimazioni di hello, quando si tenta di Application Insights visualizzazione hello toocompensate dei dati di hello per riduce il volume di dati hello.</span><span class="sxs-lookup"><span data-stu-id="32174-280">Excessively low sampling percentage (over-aggressive sampling) reduces hello accuracy of hello approximations, when Application Insights attempts toocompensate hello visualization of hello data for hello data volume reduction.</span></span> <span data-ttu-id="32174-281">Inoltre, diagnostica esperienza potrebbe influire negativamente, come alcuni dei hello raramente errori o richieste lente possono essere campionate.</span><span class="sxs-lookup"><span data-stu-id="32174-281">Also, diagnostic experience might be negatively impacted, as some of hello infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="32174-282">*Cosa accade se si configura una percentuale di campionamento troppo alta?*</span><span class="sxs-lookup"><span data-stu-id="32174-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="32174-283">Configurazione troppo elevato di campionamento percentuale (non aggressiva sufficientemente) comporta una riduzione insufficiente nel volume di hello di hello raccolti dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="32174-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in hello volume of hello collected telemetry.</span></span> <span data-ttu-id="32174-284">Possono comunque verificarsi telemetria perdita di dati correlati potrebbe essere superiore è pianificato a causa delle spese toooverage toothrottling e hello costo dell'utilizzo di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="32174-284">You may still experience telemetry data loss related toothrottling, and hello cost of using Application Insights might be higher than you planned due toooverage charges.</span></span>

<span data-ttu-id="32174-285">*Su quali piattaforme è possibile usare il campionamento?*</span><span class="sxs-lookup"><span data-stu-id="32174-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="32174-286">Campionamento di inserimento può avvenire automaticamente per qualsiasi telemetria di sopra di un determinato volume, se non sta eseguendo il campionamento hello SDK.</span><span class="sxs-lookup"><span data-stu-id="32174-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if hello SDK is not performing sampling.</span></span> <span data-ttu-id="32174-287">Questo funzionerà, ad esempio, se l'app Usa un server Java o se si utilizza una versione precedente di hello SDK di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="32174-287">This would work, for example, if your app uses a Java server, or if you are using an older version of hello ASP.NET SDK.</span></span>
* <span data-ttu-id="32174-288">Se si sta utilizzando versioni SDK ASP.NET 2.0.0 e versioni successive (ospitato in Azure o nel proprio server), si ottiene adattivo di campionamento per impostazione predefinita, ma è possibile passare toofixed velocità, come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="32174-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch toofixed-rate as described above.</span></span> <span data-ttu-id="32174-289">Campionamento tasso fisso, il browser hello SDK consente di sincronizzare automaticamente toosample eventi correlati.</span><span class="sxs-lookup"><span data-stu-id="32174-289">With fixed-rate sampling, hello browser SDK automatically synchronizes toosample related events.</span></span> 

<span data-ttu-id="32174-290">*Esistono alcuni eventi rari voglio sempre toosee. Come è possibile ottenere tali oltre il modulo di campionamento hello?*</span><span class="sxs-lookup"><span data-stu-id="32174-290">*There are certain rare events I always want toosee. How can I get them past hello sampling module?*</span></span>

* <span data-ttu-id="32174-291">Inizializza un'istanza separata di TelemetryClient con un nuovo TelemetryConfiguration (non hello Active quello predefinito).</span><span class="sxs-lookup"><span data-stu-id="32174-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not hello default Active one).</span></span> <span data-ttu-id="32174-292">Utilizzare tale toosend gli eventi rari.</span><span class="sxs-lookup"><span data-stu-id="32174-292">Use that toosend your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32174-293">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32174-293">Next steps</span></span>
* <span data-ttu-id="32174-294">[applicazione di filtri](app-insights-api-filtering-sampling.md) può garantire un controllo più rigoroso sui dati inviati dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="32174-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

