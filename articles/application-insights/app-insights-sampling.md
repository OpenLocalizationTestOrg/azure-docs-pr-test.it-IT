---
title: Campionamento della telemetria in Azure Application Insights | Documentazione Microsoft
description: Come tenere sotto controllo il volume della telemetria.
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
ms.openlocfilehash: ceaeced414c9c302fba335b4578bcdcbfaef0410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="d83c7-103">Campionamento in Application Insights</span><span class="sxs-lookup"><span data-stu-id="d83c7-103">Sampling in Application Insights</span></span>


<span data-ttu-id="d83c7-104">Il campionamento è una funzionalità di [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d83c7-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="d83c7-105">È l'approccio consigliato per ridurre il traffico e l'archiviazione della telemetria mantenendo però un'analisi statisticamente corretta dei dati dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d83c7-105">It is the recommended way to reduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="d83c7-106">Il filtro seleziona gli elementi correlati per poter passare dall'uno all'altro nel corso delle indagini diagnostiche.</span><span class="sxs-lookup"><span data-stu-id="d83c7-106">The filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="d83c7-107">Quando i conteggi delle metriche vengono presentati nel portale, vengono nuovamente normalizzati tenendo in considerazione il campionamento, per ridurre al minimo gli effetti sulle statistiche.</span><span class="sxs-lookup"><span data-stu-id="d83c7-107">When metric counts are presented to you in the portal, they are renormalized to take account of the sampling, to minimize any effect on the statistics.</span></span>

<span data-ttu-id="d83c7-108">Il campionamento riduce i costi del traffico e dei dati e consente di evitare la limitazione.</span><span class="sxs-lookup"><span data-stu-id="d83c7-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="d83c7-109">In breve:</span><span class="sxs-lookup"><span data-stu-id="d83c7-109">In brief:</span></span>
* <span data-ttu-id="d83c7-110">Campionamento mantiene 1 in  *n*  registra e ignora il resto.</span><span class="sxs-lookup"><span data-stu-id="d83c7-110">Sampling retains 1 in *n* records and discards the rest.</span></span> <span data-ttu-id="d83c7-111">Ad esempio, potrebbe mantenere 1 un evento su 5, corrispondente a una frequenza di campionamento del 20%.</span><span class="sxs-lookup"><span data-stu-id="d83c7-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="d83c7-112">Nelle app server Web ASP.NET, il campionamento viene eseguito automaticamente se l'applicazione invia molti dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="d83c7-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="d83c7-113">È anche possibile impostare il campionamento manualmente, nella pagina del portale relativa ai prezzi oppure nel file con estensione config di ASP.NET SDK, per ridurre anche il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="d83c7-113">You can also set sampling manually, either in the portal on the pricing page; or in the ASP.NET SDK in the .config file, to also reduce the network traffic.</span></span>
* <span data-ttu-id="d83c7-114">Se si registrano eventi personalizzati e ci si vuole assicurare che gli eventi di un set vengano mantenuti o rimossi insieme, verificare che abbiano lo stesso valore OperationId.</span><span class="sxs-lookup"><span data-stu-id="d83c7-114">If you log custom events and you want to make sure that a set of events is either retained or discarded together, make sure that they have the same OperationId value.</span></span>
* <span data-ttu-id="d83c7-115">Il divisore di campionamento  *n*  viene segnalato in ogni record nella proprietà `itemCount`, che nella ricerca viene visualizzata sotto il nome descrittivo "numero di richieste" o "conteggio eventi".</span><span class="sxs-lookup"><span data-stu-id="d83c7-115">The sampling divisor *n* is reported in each record in the property `itemCount`, which in Search appears under the friendly name "request count" or "event count".</span></span> <span data-ttu-id="d83c7-116">Quando il campionamento non è in esecuzione, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="d83c7-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="d83c7-117">Se si scrivono query di Dati di analisi, è necessario [tener conto del campionamento](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="d83c7-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="d83c7-118">In particolare, anziché eseguire semplicemente il conteggio dei record, è necessario usare `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="d83c7-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="d83c7-119">Tipi di campionamento</span><span class="sxs-lookup"><span data-stu-id="d83c7-119">Types of sampling</span></span>
<span data-ttu-id="d83c7-120">Esistono tre diversi metodi di campionamento:</span><span class="sxs-lookup"><span data-stu-id="d83c7-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="d83c7-121">**Campionamento adattivo** , che regola automaticamente il volume dei dati di telemetria inviati dall'SDK nell'app ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d83c7-121">**Adaptive sampling** automatically adjusts the volume of telemetry sent from the SDK in your ASP.NET app.</span></span> <span data-ttu-id="d83c7-122">Si tratta di un'opzione predefinita dell'SDK versione 2.0.0-beta3.</span><span class="sxs-lookup"><span data-stu-id="d83c7-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="d83c7-123">Attualmente disponibile solo per la telemetria lato server di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d83c7-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="d83c7-124">**Campionamento a frequenza fissa** , che riduce il volume dei dati di telemetria inviati sia dal server ASP.NET che dai browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="d83c7-124">**Fixed-rate sampling** reduces the volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="d83c7-125">È necessario impostare la frequenza.</span><span class="sxs-lookup"><span data-stu-id="d83c7-125">You set the rate.</span></span> <span data-ttu-id="d83c7-126">Il client e il server sincronizzeranno il rispettivo campionamento in modo che nella ricerca sia possibile spostarsi tra le visualizzazioni pagina e le richieste correlate.</span><span class="sxs-lookup"><span data-stu-id="d83c7-126">The client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="d83c7-127">**Campionamento per inserimento** funziona nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d83c7-127">**Ingestion sampling** works in the Azure portal.</span></span> <span data-ttu-id="d83c7-128">Rimuove alcuni dati di telemetria provenienti dall'app, a una velocità impostata.</span><span class="sxs-lookup"><span data-stu-id="d83c7-128">It discards some of the telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="d83c7-129">Non riduce il traffico di telemetria, ma consente all'utente di rispettare la quota mensile.</span><span class="sxs-lookup"><span data-stu-id="d83c7-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="d83c7-130">Il grande vantaggio del campionamento per inserimento consiste nella possibilità di impostarlo senza ridistribuire l'applicazione, oltre al fatto di funzionare in modo uniforme per tutti i server e i client.</span><span class="sxs-lookup"><span data-stu-id="d83c7-130">The big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="d83c7-131">Se è in esecuzione il campionamento adattivo o a frequenza fissa, il campionamento per inserimento è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="d83c7-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="d83c7-132">Campionamento per inserimento</span><span class="sxs-lookup"><span data-stu-id="d83c7-132">Ingestion sampling</span></span>
<span data-ttu-id="d83c7-133">Questa forma di campionamento opera nel punto in cui i dati di telemetria di server Web, browser e dispositivi raggiungono l'endpoint di servizio di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d83c7-133">This form of sampling operates at the point where the telemetry from your web server, browsers, and devices reaches the Application Insights service endpoint.</span></span> <span data-ttu-id="d83c7-134">Anche se non riduce il traffico dei dati di telemetria inviato dall'app, riduce la quantità di dati elaborati, conservati e addebitati da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d83c7-134">Although it doesn't reduce the telemetry traffic sent from your app, it does reduce the amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="d83c7-135">Usare questo tipo di campionamento se l'app spesso supera la quota mensile e non si ha la possibilità di usare uno dei tipi di campionamento basati sull'SDK.</span><span class="sxs-lookup"><span data-stu-id="d83c7-135">Use this type of sampling if your app often goes over its monthly quota and you don't have the option of using either of the SDK-based types of sampling.</span></span> 

<span data-ttu-id="d83c7-136">Impostare la frequenza di campionamento nel pannello Quota + prezzi:</span><span class="sxs-lookup"><span data-stu-id="d83c7-136">Set the sampling rate in the Quotas and Pricing blade:</span></span>

![Nel pannello Panoramica sull'applicazione fare clic su Impostazioni, Quota, Esempi e quindi selezionare una frequenza di campionamento e fare clic su Aggiorna.](./media/app-insights-sampling/04.png)

<span data-ttu-id="d83c7-138">Come in altri tipi di campionamento, l'algoritmo consente di mantenere gli elementi di telemetria correlati.</span><span class="sxs-lookup"><span data-stu-id="d83c7-138">Like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="d83c7-139">Ad esempio, quando si controllano i dati di telemetria nella ricerca, sarà possibile trovare la richiesta correlata a una particolare eccezione.</span><span class="sxs-lookup"><span data-stu-id="d83c7-139">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> <span data-ttu-id="d83c7-140">I conteggi di metrica, ad esempio la frequenza delle richieste e delle eccezioni, vengono mantenuti correttamente.</span><span class="sxs-lookup"><span data-stu-id="d83c7-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="d83c7-141">I punti dati che vengono rimossi dal campionamento non sono disponibili in alcuna funzionalità di Application Insights, ad esempio nell' [esportazione continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="d83c7-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="d83c7-142">Il campionamento per inserimento non funziona mentre è attivo il campionamento a frequenza fissa o adattivo basato sull'SDK.</span><span class="sxs-lookup"><span data-stu-id="d83c7-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="d83c7-143">Se la frequenza di campionamento nell'SDK è inferiore al 100%, la frequenza di campionamento di inserimento impostata viene ignorata.</span><span class="sxs-lookup"><span data-stu-id="d83c7-143">If the sampling rate at the SDK is less than 100%, then the ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="d83c7-144">Il valore visualizzato nel riquadro indica il valore impostato per il campionamento per inserimento.</span><span class="sxs-lookup"><span data-stu-id="d83c7-144">The value shown on the tile indicates the value that you set for ingestion sampling.</span></span> <span data-ttu-id="d83c7-145">Non rappresenta la frequenza di campionamento effettiva se il campionamento dell'SDK è in funzione.</span><span class="sxs-lookup"><span data-stu-id="d83c7-145">It doesn't represent the actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="d83c7-146">Campionamento adattivo nel server Web</span><span class="sxs-lookup"><span data-stu-id="d83c7-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="d83c7-147">Il campionamento adattivo è abilitato per impostazione predefinita ed è disponibile in Application Insights SDK per ASP.NET, versione 2.0.0-beta3 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d83c7-147">Adaptive sampling is available for the Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="d83c7-148">Il campionamento adattivo riguarda il volume dei dati di telemetria inviati dall'app del server Web al servizio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d83c7-148">Adaptive sampling affects the volume of telemetry sent from your web server app to the Application Insights service.</span></span> <span data-ttu-id="d83c7-149">Il volume viene regolato automaticamente affinché rimanga in una frequenza massima specificata del traffico.</span><span class="sxs-lookup"><span data-stu-id="d83c7-149">The volume is adjusted automatically to keep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="d83c7-150">Non opera a bassi volumi di dati di telemetria, pertanto un'app per eseguire il debug o un sito Web con un basso utilizzo non saranno interessate.</span><span class="sxs-lookup"><span data-stu-id="d83c7-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="d83c7-151">Per ottenere il volume di destinazione, alcuni dei dati di telemetria generati vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="d83c7-151">To achieve the target volume, some of the telemetry generated is discarded.</span></span> <span data-ttu-id="d83c7-152">Tuttavia, come in altri tipi di campionamento, l'algoritmo consente di mantenere gli elementi di telemetria correlati.</span><span class="sxs-lookup"><span data-stu-id="d83c7-152">But like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="d83c7-153">Ad esempio, quando si controllano i dati di telemetria nella ricerca, sarà possibile trovare la richiesta correlata a una particolare eccezione.</span><span class="sxs-lookup"><span data-stu-id="d83c7-153">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> 

<span data-ttu-id="d83c7-154">I conteggi di metrica, ad esempio la frequenza delle richieste e delle eccezioni, vengono adattati per compensare la frequenza di campionamento, in modo che mostrino i valori corretti in Esplora metriche.</span><span class="sxs-lookup"><span data-stu-id="d83c7-154">Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="d83c7-155">**Aggiornare i pacchetti del progetto NuGet** all'ultima versione *preliminare* di Application Insights: fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere Gestisci pacchetti NuGet, selezionare **Includi versione preliminare** e cercare Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="d83c7-155">**Update your project's NuGet** packages to the latest *pre-release* version of Application Insights: Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="d83c7-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) è possibile regolare diversi parametri nel nodo `AdaptiveSamplingTelemetryProcessor`.</span><span class="sxs-lookup"><span data-stu-id="d83c7-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in the `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="d83c7-157">Le cifre indicate sono i valori predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d83c7-157">The figures shown are the default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="d83c7-158">Frequenza di destinazione che l'algoritmo adattivo deve raggiungere **su ogni host server**.</span><span class="sxs-lookup"><span data-stu-id="d83c7-158">The target rate that the adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="d83c7-159">Se l'app Web viene eseguita su più host, ridurre questo valore per non superare la frequenza di destinazione del traffico nel portale di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d83c7-159">If your web app runs on many hosts, reduce this value so as to remain within your target rate of traffic at the Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="d83c7-160">Intervallo in base al quale la frequenza corrente della telemetria viene rivalutata.</span><span class="sxs-lookup"><span data-stu-id="d83c7-160">The interval at which the current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="d83c7-161">La valutazione viene eseguita come media mobile.</span><span class="sxs-lookup"><span data-stu-id="d83c7-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="d83c7-162">Potrebbe essere necessario ridurre questo intervallo se la telemetria è responsabile di burst improvvisi.</span><span class="sxs-lookup"><span data-stu-id="d83c7-162">You might want to shorten this interval if your telemetry is liable to sudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="d83c7-163">Quando il valore della percentuale di campionamento cambia, periodo di tempo dopo il quale è consentito ridurre nuovamente la percentuale di campionamento per acquisire meno dati.</span><span class="sxs-lookup"><span data-stu-id="d83c7-163">When sampling percentage value changes, how soon after are we allowed to lower sampling percentage again to capture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="d83c7-164">Quando il valore della percentuale di campionamento cambia, periodo di tempo dopo il quale è consentito aumentare nuovamente la percentuale di campionamento per acquisire più dati.</span><span class="sxs-lookup"><span data-stu-id="d83c7-164">When sampling percentage value changes, how soon after are we allowed to increase sampling percentage again to capture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="d83c7-165">Quando la percentuale di campionamento varia, valore minimo che è consentito impostare.</span><span class="sxs-lookup"><span data-stu-id="d83c7-165">As sampling percentage varies, what is the minimum value we're allowed to set.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="d83c7-166">Quando la percentuale di campionamento varia, valore massimo che è consentito impostare.</span><span class="sxs-lookup"><span data-stu-id="d83c7-166">As sampling percentage varies, what is the maximum value we're allowed to set.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="d83c7-167">Nel calcolo della media mobile, peso assegnato al valore più recente.</span><span class="sxs-lookup"><span data-stu-id="d83c7-167">In the calculation of the moving average, the weight assigned to the most recent value.</span></span> <span data-ttu-id="d83c7-168">Usare un valore uguale o inferiore a 1.</span><span class="sxs-lookup"><span data-stu-id="d83c7-168">Use a value equal to or less than 1.</span></span> <span data-ttu-id="d83c7-169">I valori più bassi rendono l'algoritmo meno reattivo alle modifiche improvvise.</span><span class="sxs-lookup"><span data-stu-id="d83c7-169">Smaller values make the algorithm less reactive to sudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="d83c7-170">Valore assegnato quando l'app è appena stata avviata.</span><span class="sxs-lookup"><span data-stu-id="d83c7-170">The value assigned when the app has just started.</span></span> <span data-ttu-id="d83c7-171">Non ridurlo durante il debug.</span><span class="sxs-lookup"><span data-stu-id="d83c7-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="d83c7-172">Elenco dei tipi da non campionare delimitato dal punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="d83c7-172">A semi-colon delimited list of types that you do not want to be sampled.</span></span> <span data-ttu-id="d83c7-173">I tipi riconosciuti sono: dipendenza, evento, eccezione, pageview, richiesta, traccia.</span><span class="sxs-lookup"><span data-stu-id="d83c7-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="d83c7-174">Tutte le istanze dei tipi specificati vengono trasmesse; i tipi non specificati vengono campionati.</span><span class="sxs-lookup"><span data-stu-id="d83c7-174">All instances of the specified types are transmitted; the types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="d83c7-175">Elenco dei tipi da campionare delimitato dal punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="d83c7-175">A semi-colon delimited list of types that you want to be sampled.</span></span> <span data-ttu-id="d83c7-176">I tipi riconosciuti sono: dipendenza, evento, eccezione, pageview, richiesta, traccia.</span><span class="sxs-lookup"><span data-stu-id="d83c7-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="d83c7-177">I tipi specificati vengono campionati; tutte le istanze degli altri tipi vengono sempre trasmesse.</span><span class="sxs-lookup"><span data-stu-id="d83c7-177">The specified types are sampled; all instances of the other types will always be transmitted.</span></span>


<span data-ttu-id="d83c7-178">**Per disattivare** il campionamento adattivo, rimuovere il nodo AdaptiveSamplingTelemetryProcessor da applicationinsights-config.</span><span class="sxs-lookup"><span data-stu-id="d83c7-178">**To switch off** adaptive sampling, remove the AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="d83c7-179">Alternativa: configurare il campionamento adattivo nel codice</span><span class="sxs-lookup"><span data-stu-id="d83c7-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="d83c7-180">Invece di regolare il campionamento nel file .config, è possibile utilizzare il codice.</span><span class="sxs-lookup"><span data-stu-id="d83c7-180">Instead of adjusting sampling in the .config file, you can use code.</span></span> <span data-ttu-id="d83c7-181">Ciò consente di specificare una funzione di callback che viene richiamata ogni volta che si valuta nuovamente la frequenza di campionamento.</span><span class="sxs-lookup"><span data-stu-id="d83c7-181">This allows you to specify a callback function that is invoked whenever the sampling rate is re-evaluated.</span></span> <span data-ttu-id="d83c7-182">È possibile utilizzarlo, ad esempio, per scoprire quale frequenza di campionamento si sta utilizzando.</span><span class="sxs-lookup"><span data-stu-id="d83c7-182">You could use this, for example, to find out what sampling rate is being used.</span></span>

<span data-ttu-id="d83c7-183">Rimuovere il nodo `AdaptiveSamplingTelemetryProcessor` dal file .config.</span><span class="sxs-lookup"><span data-stu-id="d83c7-183">Remove the `AdaptiveSamplingTelemetryProcessor` node from the .config file.</span></span>

<span data-ttu-id="d83c7-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="d83c7-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust the settings from their defaults.

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
             // Report the sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="d83c7-185">([Informazioni sui processori di telemetria](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="d83c7-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="d83c7-186">Campionamento per pagine Web con JavaScript</span><span class="sxs-lookup"><span data-stu-id="d83c7-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="d83c7-187">È possibile configurare le pagine Web per il campionamento a frequenza fissa da qualsiasi server.</span><span class="sxs-lookup"><span data-stu-id="d83c7-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="d83c7-188">Quando si [configurano le pagine Web per Application Insights](app-insights-javascript.md), modificare il frammento ottenuto dal portale di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d83c7-188">When you [configure the web pages for Application Insights](app-insights-javascript.md), modify the snippet that you get from the Application Insights portal.</span></span> <span data-ttu-id="d83c7-189">Nelle app ASP.NET il frammento viene in genere salvato in _Layout.cshtml.  Inserire una riga simile a `samplingPercentage: 10,` prima della chiave di strumentazione:</span><span class="sxs-lookup"><span data-stu-id="d83c7-189">(In ASP.NET apps, the snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before the instrumentation key:</span></span>

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

<span data-ttu-id="d83c7-190">Come percentuale di campionamento, sceglierne una vicina a 100/N dove N è un numero intero.</span><span class="sxs-lookup"><span data-stu-id="d83c7-190">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="d83c7-191">Il campionamento attualmente non supporta altri valori.</span><span class="sxs-lookup"><span data-stu-id="d83c7-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="d83c7-192">Se si abilita il campionamento a frequenza fissa nel server, i client e il server si sincronizzeranno in modo che nella ricerca sia possibile spostarsi tra le visualizzazioni pagina e le richieste correlate.</span><span class="sxs-lookup"><span data-stu-id="d83c7-192">If you also enable fixed-rate sampling at the server, the clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="d83c7-193">Campionamento a frequenza fissa per siti Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d83c7-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="d83c7-194">Il campionamento a frequenza fissa riduce il traffico inviato dal server e dai Web browser.</span><span class="sxs-lookup"><span data-stu-id="d83c7-194">Fixed rate sampling reduces the traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="d83c7-195">A differenza del campionamento adattivo, riduce i dati di telemetria a una frequenza fissa definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="d83c7-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="d83c7-196">Sincronizza inoltre il campionamento del client e del server in modo che gli elementi correlati vengano mantenuti, ad esempio in modo che se si esamina una pagina di ricerca, è possibile trovare la richiesta correlata.</span><span class="sxs-lookup"><span data-stu-id="d83c7-196">It also synchronizes the client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="d83c7-197">L'algoritmo di campionamento mantiene gli elementi correlati.</span><span class="sxs-lookup"><span data-stu-id="d83c7-197">The sampling algorithm retains related items.</span></span> <span data-ttu-id="d83c7-198">Per ciascun evento di richiesta HTTP, l'algoritmo e gli eventi correlati vengono eliminati o trasmessi.</span><span class="sxs-lookup"><span data-stu-id="d83c7-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="d83c7-199">In Esplora metriche, frequenze quali il numero di richieste ed eccezioni vengono moltiplicate per un fattore in modo da compensare la frequenza di campionamento ed essere quindi corretti.</span><span class="sxs-lookup"><span data-stu-id="d83c7-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor to compensate for the sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="d83c7-200">**Aggiornare i pacchetti NuGet del progetto** all'ultima versione *preliminare* di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d83c7-200">**Update your project's NuGet packages** to the latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="d83c7-201">Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere Gestisci pacchetti NuGet, selezionare **Includi versione preliminare** e cercare Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="d83c7-201">Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="d83c7-202">**Disabilitare il campionamento adattivo**: in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) rimuovere o impostare come commento il nodo `AdaptiveSamplingTelemetryProcessor`.</span><span class="sxs-lookup"><span data-stu-id="d83c7-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out the `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="d83c7-203">**Abilitare il modulo di campionamento a frequenza fissa.**</span><span class="sxs-lookup"><span data-stu-id="d83c7-203">**Enable the fixed-rate sampling module.**</span></span> <span data-ttu-id="d83c7-204">Aggiungere questo frammento ad [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="d83c7-204">Add this snippet to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="d83c7-205">Come percentuale di campionamento, sceglierne una vicina a 100/N dove N è un numero intero.</span><span class="sxs-lookup"><span data-stu-id="d83c7-205">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="d83c7-206">Il campionamento attualmente non supporta altri valori.</span><span class="sxs-lookup"><span data-stu-id="d83c7-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="d83c7-207">Alternativa: abilitare il campionamento a frequenza fissa nel codice del server locale</span><span class="sxs-lookup"><span data-stu-id="d83c7-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="d83c7-208">Invece di impostare il parametro di campionamento nel file .config, è possibile utilizzare il codice.</span><span class="sxs-lookup"><span data-stu-id="d83c7-208">Instead of setting the sampling parameter in the .config file, you can use code.</span></span> 

<span data-ttu-id="d83c7-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="d83c7-209">*C#*</span></span>

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

<span data-ttu-id="d83c7-210">([Informazioni sui processori di telemetria](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="d83c7-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-to-use-sampling"></a><span data-ttu-id="d83c7-211">Quando usare il campionamento?</span><span class="sxs-lookup"><span data-stu-id="d83c7-211">When to use sampling?</span></span>
<span data-ttu-id="d83c7-212">Il campionamento adattivo viene automaticamente abilitato se si usa ASP.NET SDK versione 2.0.0-beta3 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d83c7-212">Adaptive sampling is automatically enabled if you use the ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="d83c7-213">Nel server Microsoft è possibile usare il campionamento per inserimento indipendentemente dalla versione dell'SDK in uso.</span><span class="sxs-lookup"><span data-stu-id="d83c7-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="d83c7-214">Per la maggior parte delle applicazioni di piccole e medie dimensioni, il campionamento non è necessario.</span><span class="sxs-lookup"><span data-stu-id="d83c7-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="d83c7-215">Le informazioni di diagnostica più utili e le statistiche più accurate si ottengono raccogliendo dati su tutte le attività utente.</span><span class="sxs-lookup"><span data-stu-id="d83c7-215">The most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="d83c7-216">I vantaggi principali del campionamento sono:</span><span class="sxs-lookup"><span data-stu-id="d83c7-216">The main advantages of sampling are:</span></span>

* <span data-ttu-id="d83c7-217">Il servizio Application Insights rimuove ("limita") i punti dati quando l'app invia una frequenza di telemetria molto elevata in un breve intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="d83c7-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="d83c7-218">Non superare la [quota](app-insights-pricing.md) di punti dati per il proprio piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="d83c7-218">To keep within the [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="d83c7-219">Ridurre il traffico di rete dalla raccolta di telemetria.</span><span class="sxs-lookup"><span data-stu-id="d83c7-219">To reduce network traffic from the collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="d83c7-220">Quale tipo di campionamento è opportuno usare?</span><span class="sxs-lookup"><span data-stu-id="d83c7-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="d83c7-221">**Usare il campionamento per inserimento se:**</span><span class="sxs-lookup"><span data-stu-id="d83c7-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="d83c7-222">Si supera spesso la quota mensile dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="d83c7-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="d83c7-223">Si usa una versione dell'SDK che non supporta il campionamento, ad esempio Java SDK o versioni di ASP.NET precedenti alla 2.</span><span class="sxs-lookup"><span data-stu-id="d83c7-223">You're using a version of the SDK that doesn't support sampling - for example, the Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="d83c7-224">Si ricevono grandi quantità di dati di telemetria dal Web browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="d83c7-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="d83c7-225">**Usare il campionamento a frequenza fissa se:**</span><span class="sxs-lookup"><span data-stu-id="d83c7-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="d83c7-226">Si usa Application Insights SDK per i servizi Web ASP.NET versione 2.0.0 o successiva e</span><span class="sxs-lookup"><span data-stu-id="d83c7-226">You're using the Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="d83c7-227">È necessario il campionamento sincronizzato tra client e server, in modo che, quando si esaminano gli eventi in [Cerca](app-insights-diagnostic-search.md), sia possibile spostarsi tra gli eventi correlati nel client e nel server, ad esempio visualizzazioni pagina e richieste http.</span><span class="sxs-lookup"><span data-stu-id="d83c7-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on the client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="d83c7-228">Se è certi della percentuale di campionamento appropriata per l'app.</span><span class="sxs-lookup"><span data-stu-id="d83c7-228">You are confident of the appropriate sampling percentage for your app.</span></span> <span data-ttu-id="d83c7-229">Deve essere abbastanza elevata da ottenere metriche accurate, ma al di sotto della frequenza che fa superare la quota di prezzo e le soglie di limitazione.</span><span class="sxs-lookup"><span data-stu-id="d83c7-229">It should be high enough to get accurate metrics, but below the rate that exceeds your pricing quota and the throttling limits.</span></span> 

<span data-ttu-id="d83c7-230">**Usare il campionamento adattivo:**</span><span class="sxs-lookup"><span data-stu-id="d83c7-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="d83c7-231">In caso contrario, è consigliabile il campionamento adattivo.</span><span class="sxs-lookup"><span data-stu-id="d83c7-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="d83c7-232">Questo tipo di campionamento è abilitato per impostazione predefinita nell'SDK del server ASP.NET versione 2.0.0-beta3.</span><span class="sxs-lookup"><span data-stu-id="d83c7-232">This is enabled by default in the ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="d83c7-233">Non riduce il traffico fino a una determinata frequenza minima, in modo da non avere effetto su un sito poco usato.</span><span class="sxs-lookup"><span data-stu-id="d83c7-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="d83c7-234">Come è possibile sapere se il campionamento è in esecuzione?</span><span class="sxs-lookup"><span data-stu-id="d83c7-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="d83c7-235">Per individuare la frequenza di campionamento effettiva indipendentemente dal punto in cui è stata applicata, usare una [query di Analisi](app-insights-analytics.md) simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="d83c7-235">To discover the actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="d83c7-236">In ogni record conservato, `itemCount` indica il numero di record originali che rappresenta, uguale a 1 + il numero di record precedenti scartati.</span><span class="sxs-lookup"><span data-stu-id="d83c7-236">In each retained record, `itemCount` indicates the number of original records that it represents, equal to 1 + the number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="d83c7-237">Come funziona il campionamento?</span><span class="sxs-lookup"><span data-stu-id="d83c7-237">How does sampling work?</span></span>
<span data-ttu-id="d83c7-238">Il campionamento a frequenza fissa e il campionamento adattivo sono funzionalità dell'SDK nella versione ASP.NET 2.0.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d83c7-238">Fixed-rate and adaptive sampling are a feature of the SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="d83c7-239">Il campionamento per inserimento è una funzionalità del servizio Application Insights ed è operativo se l'SDK non sta eseguendo un altro campionamento.</span><span class="sxs-lookup"><span data-stu-id="d83c7-239">Ingestion sampling is a feature of the Application Insights service, and can be in operation if the SDK is not performing sampling.</span></span> 

<span data-ttu-id="d83c7-240">L'algoritmo di campionamento decide quali elementi di telemetria eliminare e quali mantenere, sia che venga eseguito nell'SDK o nel servizio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d83c7-240">The sampling algorithm decides which telemetry items to drop, and which ones to keep (whether it's in the SDK or in the Application Insights service).</span></span> <span data-ttu-id="d83c7-241">La decisione sul campionamento si basa su alcune regole che hanno lo scopo di lasciare intatti tutti i punti dati correlati, mantenendo in Application Insights un'esperienza di diagnostica sfruttabile e affidabile anche con un set di dati ridotto.</span><span class="sxs-lookup"><span data-stu-id="d83c7-241">The sampling decision is based on several rules that aim to preserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="d83c7-242">Se, ad esempio, per una richiesta non riuscita l'app invia elementi di telemetria aggiuntivi (come eccezioni e tracce registrate da questa richiesta), il campionamento non dividerà la richiesta e il resto della telemetria,</span><span class="sxs-lookup"><span data-stu-id="d83c7-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="d83c7-243">ma conserverà o rimuoverà gli elementi tutti insieme.</span><span class="sxs-lookup"><span data-stu-id="d83c7-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="d83c7-244">Di conseguenza, quando si osservano i dettagli della richiesta in Application Insights, è sempre possibile visualizzare la richiesta con gli elementi di telemetria associati.</span><span class="sxs-lookup"><span data-stu-id="d83c7-244">As a result, when you look at the request details in Application Insights, you can always see the request along with its associated telemetry items.</span></span> 

<span data-ttu-id="d83c7-245">Per le applicazioni che definiscono "user" (la maggior parte delle normali applicazioni Web), la decisione sul campionamento si basa sull'hash dell'ID utente, vale a dire che tutta la telemetria associata a un particolare utente viene conservata o rimossa.</span><span class="sxs-lookup"><span data-stu-id="d83c7-245">For applications that define "user" (that is, most typical web applications), the sampling decision is based on the hash of the user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="d83c7-246">Per i tipi di applicazioni che non definiscono gli utenti (ad esempio, i servizi Web), la decisione sul campionamento si basa sull'ID operazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d83c7-246">For the types of applications that don't define users (such as web services) the sampling decision is based on the operation id of the request.</span></span> <span data-ttu-id="d83c7-247">Infine, per gli elementi della telemetria per cui non è impostato né l'ID utente né l'ID operazione (ad esempio, gli elementi della telemetria segnalati da thread asincroni senza contesto http), il campionamento si limita ad acquisire una percentuale degli elementi della telemetria di ogni tipo.</span><span class="sxs-lookup"><span data-stu-id="d83c7-247">Finally, for the telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="d83c7-248">Quando la telemetria viene ripresentata all'utente, il servizio Application Insights modifica le metriche in base alla stessa percentuale di campionamento usata in fase di raccolta, per compensare i punti dati mancanti.</span><span class="sxs-lookup"><span data-stu-id="d83c7-248">When presenting telemetry back to you, the Application Insights service adjusts the metrics by the same sampling percentage that was used at the time of collection, to compensate for the missing data points.</span></span> <span data-ttu-id="d83c7-249">Quindi, quando osservano la telemetria in Application Insights, gli utenti visualizzano approssimazioni statisticamente corrette molto vicine ai numeri reali.</span><span class="sxs-lookup"><span data-stu-id="d83c7-249">Hence, when looking at the telemetry in Application Insights, the users are seeing statistically correct approximations that are very close to the real numbers.</span></span>

<span data-ttu-id="d83c7-250">La precisione dell'approssimazione dipende in gran parte dalla percentuale di campionamento configurata.</span><span class="sxs-lookup"><span data-stu-id="d83c7-250">The accuracy of the approximation largely depends on the configured sampling percentage.</span></span> <span data-ttu-id="d83c7-251">La precisione è anche maggiore per le applicazioni che gestiscono un volume elevato di richieste generalmente simili da una grande quantità di utenti.</span><span class="sxs-lookup"><span data-stu-id="d83c7-251">Also, the accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="d83c7-252">Per le applicazioni che non gestiscono un carico di lavoro significativo, invece, il campionamento non è necessario perché queste applicazioni in genere riescono a inviare tutti i dati di telemetria senza superare la quota e senza causare perdite di dati dovute alla limitazione.</span><span class="sxs-lookup"><span data-stu-id="d83c7-252">On the other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within the quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="d83c7-253">Si noti che Application Insights non campiona i tipi di telemetria relativi a metrica e sessioni, perché la riduzione della precisione per questi tipi non è consigliabile.</span><span class="sxs-lookup"><span data-stu-id="d83c7-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in the precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="d83c7-254">Campionamento adattivo</span><span class="sxs-lookup"><span data-stu-id="d83c7-254">Adaptive sampling</span></span>
<span data-ttu-id="d83c7-255">Il campionamento adattivo aggiunge un componente che monitora la frequenza corrente di trasmissione dall'SDK e regola la percentuale di campionamento per cercare di rimanere entro la frequenza massima di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d83c7-255">Adaptive sampling adds a component that monitors the current rate of transmission from the SDK, and adjusts the sampling percentage to try to stay within the target maximum rate.</span></span> <span data-ttu-id="d83c7-256">La rettifica viene ricalcolata a intervalli regolari e si basa su una media mobile della frequenza di trasmissione in uscita.</span><span class="sxs-lookup"><span data-stu-id="d83c7-256">The adjustment is recalculated at regular intervals, and is based on a moving average of the outgoing transmission rate.</span></span>

## <a name="sampling-and-the-javascript-sdk"></a><span data-ttu-id="d83c7-257">Campionamento e JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="d83c7-257">Sampling and the JavaScript SDK</span></span>
<span data-ttu-id="d83c7-258">L'SDK lato client (JavaScript) partecipa al campionamento a frequenza fissa insieme all'SDK lato server.</span><span class="sxs-lookup"><span data-stu-id="d83c7-258">The client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with the server-side SDK.</span></span> <span data-ttu-id="d83c7-259">Le pagine instrumentate invieranno solo la telemetria lato client dagli stessi utenti per cui il lato server ha preso la decisione di "eseguire il campionamento internamente".</span><span class="sxs-lookup"><span data-stu-id="d83c7-259">The instrumented pages will only send client-side telemetry from the same users for which the server-side made its decision to "sample in."</span></span> <span data-ttu-id="d83c7-260">Questa logica è concepita per mantenere l'integrità della sessione utente sui lati client e server.</span><span class="sxs-lookup"><span data-stu-id="d83c7-260">This logic is designed to maintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="d83c7-261">Di conseguenza, da un particolare elemento della telemetria in Application Insights è possibile trovare tutti gli altri elementi della telemetria per questa sessione utente.</span><span class="sxs-lookup"><span data-stu-id="d83c7-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="d83c7-262">*La telemetria lato e client e server non mostra i campioni coordinati, come descritto sopra.*</span><span class="sxs-lookup"><span data-stu-id="d83c7-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="d83c7-263">Verificare di avere abilitato il campionamento a frequenza fissa sia sul server che sul client.</span><span class="sxs-lookup"><span data-stu-id="d83c7-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="d83c7-264">Assicurarsi che la versione dell'SDK sia 2.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d83c7-264">Make sure that the SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="d83c7-265">Controllare di avere impostato la stessa percentuale di campionamento sia nel client che nel server.</span><span class="sxs-lookup"><span data-stu-id="d83c7-265">Check that you set the same sampling percentage in both the client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="d83c7-266">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="d83c7-266">Frequently Asked Questions</span></span>
<span data-ttu-id="d83c7-267">*Perché il campionamento non è una semplice "raccolta di percentuale X di ogni tipo di telemetria"?*</span><span class="sxs-lookup"><span data-stu-id="d83c7-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="d83c7-268">Anche se questo approccio al campionamento offre una precisione davvero elevata nelle approssimazioni delle metriche, tuttavia non permette di correlare i dati diagnostici per utente, sessione e richiesta, come è indispensabile per la diagnostica.</span><span class="sxs-lookup"><span data-stu-id="d83c7-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability to correlate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="d83c7-269">Il campionamento quindi funziona meglio come logica di "raccolta di tutti gli elementi della telemetria per una percentuale X di utenti dell'app" o di "raccolta di tutta la telemetria per una percentuale X di richieste app".</span><span class="sxs-lookup"><span data-stu-id="d83c7-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="d83c7-270">Per gli elementi della telemetria non associati alle richieste, ad esempio l'elaborazione asincrona in background, il fallback prevede la "raccolta di una percentuale X di tutti gli elementi per ogni tipo di telemetria".</span><span class="sxs-lookup"><span data-stu-id="d83c7-270">For the telemetry items not associated with the requests (such as background asynchronous processing), the fall back is to "collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="d83c7-271">*La percentuale di campionamento può variare nel tempo?*</span><span class="sxs-lookup"><span data-stu-id="d83c7-271">*Can the sampling percentage change over time?*</span></span>

* <span data-ttu-id="d83c7-272">Sì, il campionamento adattivo modifica gradualmente la percentuale di campionamento, in base al volume attualmente osservato della telemetria.</span><span class="sxs-lookup"><span data-stu-id="d83c7-272">Yes, adaptive sampling gradually changes the sampling percentage, based on the currently observed volume of the telemetry.</span></span>

<span data-ttu-id="d83c7-273">*Se si usa il campionamento a frequenza fissa, come stabilire quale sarà la percentuale di campionamento ideale per l'app?*</span><span class="sxs-lookup"><span data-stu-id="d83c7-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work the best for my app?*</span></span>

* <span data-ttu-id="d83c7-274">Una modalità è quella di iniziare con il campionamento adattivo, scoprire quale frequenza è impostata (vedere la domanda precedente) e quindi cambiarla a campionamento a frequenza fissa usando quella frequenza.</span><span class="sxs-lookup"><span data-stu-id="d83c7-274">One way is to start with adaptive sampling, find out what rate it settles on (see the above question), and then switch to fixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="d83c7-275">In caso contrario, è necessario usare l'intuito.</span><span class="sxs-lookup"><span data-stu-id="d83c7-275">Otherwise, you have to guess.</span></span> <span data-ttu-id="d83c7-276">Analizzare l'utilizzo della telemetria corrente in AI, osservare le possibili limitazioni in corso e stimare il volume della telemetria raccolta.</span><span class="sxs-lookup"><span data-stu-id="d83c7-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate the volume of the collected telemetry.</span></span> <span data-ttu-id="d83c7-277">Questi tre input, insieme al piano tariffario selezionato, suggeriscono di quanto ridurre il volume dei dati di telemetria raccolti.</span><span class="sxs-lookup"><span data-stu-id="d83c7-277">These three inputs, together with your selected pricing tier, suggest how much you might want to reduce the volume of the collected telemetry.</span></span> <span data-ttu-id="d83c7-278">Tuttavia, un aumento nel numero degli utenti o qualsiasi altra migrazione nel volume di telemetria potrebbe invalidare la stima.</span><span class="sxs-lookup"><span data-stu-id="d83c7-278">However, an increase in the number of your users or some other shift in the volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="d83c7-279">*Cosa accade se si configura una percentuale di campionamento troppo bassa?*</span><span class="sxs-lookup"><span data-stu-id="d83c7-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="d83c7-280">Una percentuale di campionamento troppo bassa (campionamento eccessivamente aggressivo) ridurrà la precisione delle approssimazioni, quando Application Insights tenterà di compensare la visualizzazione dei dati per la riduzione del volume dei dati.</span><span class="sxs-lookup"><span data-stu-id="d83c7-280">Excessively low sampling percentage (over-aggressive sampling) reduces the accuracy of the approximations, when Application Insights attempts to compensate the visualization of the data for the data volume reduction.</span></span> <span data-ttu-id="d83c7-281">Anche l'esperienza di diagnostica potrebbe risultare compromessa, perché potrebbero venire campionate alcune richieste lente o non riuscite.</span><span class="sxs-lookup"><span data-stu-id="d83c7-281">Also, diagnostic experience might be negatively impacted, as some of the infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="d83c7-282">*Cosa accade se si configura una percentuale di campionamento troppo alta?*</span><span class="sxs-lookup"><span data-stu-id="d83c7-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="d83c7-283">Configurando una percentuale di campionamento troppo elevata (non abbastanza aggressiva), si otterrà una riduzione insufficiente del volume dei dati di telemetria raccolti.</span><span class="sxs-lookup"><span data-stu-id="d83c7-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in the volume of the collected telemetry.</span></span> <span data-ttu-id="d83c7-284">Potrebbe tuttavia verificarsi una perdita dei dati di telemetria correlata alla limitazione e il costo per l'uso di Application Insights potrebbe essere superiore al previsto per l'applicazione di tariffe aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="d83c7-284">You may still experience telemetry data loss related to throttling, and the cost of using Application Insights might be higher than you planned due to overage charges.</span></span>

<span data-ttu-id="d83c7-285">*Su quali piattaforme è possibile usare il campionamento?*</span><span class="sxs-lookup"><span data-stu-id="d83c7-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="d83c7-286">Se nell'SDK non è impostato il campionamento, si verifica automaticamente il campionamento per inserimento per i dati di telemetria superiori a un determinato volume.</span><span class="sxs-lookup"><span data-stu-id="d83c7-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if the SDK is not performing sampling.</span></span> <span data-ttu-id="d83c7-287">Si verifica, ad esempio, se l'app usa un server Java o se si esegue una versione precedente dell'SDK ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d83c7-287">This would work, for example, if your app uses a Java server, or if you are using an older version of the ASP.NET SDK.</span></span>
* <span data-ttu-id="d83c7-288">Se si usa l'SDK ASP.NET versione 2.0.0 o successiva, ospitato in Azure o sul server in uso, per impostazione predefinita viene eseguito il campionamento adattivo, ma è comunque possibile passare al campionamento a frequenza fissa, come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d83c7-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch to fixed-rate as described above.</span></span> <span data-ttu-id="d83c7-289">Con il campionamento a frequenza fissa, l'SDK del browser si sincronizza automaticamente con gli eventi correlati al campione.</span><span class="sxs-lookup"><span data-stu-id="d83c7-289">With fixed-rate sampling, the browser SDK automatically synchronizes to sample related events.</span></span> 

<span data-ttu-id="d83c7-290">*Esistono alcuni eventi rari che si vuole visualizzare sempre. Come è possibile passarli al modulo di campionamento?*</span><span class="sxs-lookup"><span data-stu-id="d83c7-290">*There are certain rare events I always want to see. How can I get them past the sampling module?*</span></span>

* <span data-ttu-id="d83c7-291">Inizializzare un'istanza separata di TelemetryClient con una nuova TelemetryConfiguration (non con quello predefinito attivo).</span><span class="sxs-lookup"><span data-stu-id="d83c7-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not the default Active one).</span></span> <span data-ttu-id="d83c7-292">Usarla per inviare gli eventi rari.</span><span class="sxs-lookup"><span data-stu-id="d83c7-292">Use that to send your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d83c7-293">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d83c7-293">Next steps</span></span>
* <span data-ttu-id="d83c7-294">[applicazione di filtri](app-insights-api-filtering-sampling.md) può garantire un controllo più rigoroso sui dati inviati dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="d83c7-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

