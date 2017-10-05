---
title: Eseguire il monitoraggio delle app nel Servizio app di Azure | Documentazione Microsoft
description: Informazioni su come monitorare le app nel servizio app di Azure tramite il portale di Azure.
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 25d3776920d683fffedcd8ac6ed0e84dfe875974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="fa96d-103">Procedura: Eseguire il monitoraggio delle app nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="fa96d-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="fa96d-104">Il [servizio app](http://go.microsoft.com/fwlink/?LinkId=529714) offre la funzionalità di monitoraggio incorporata nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fa96d-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in the [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="fa96d-105">Consente, ad esempio, di esaminare **quote** e **metriche** di un'app e il relativo piano di servizio app, configurare**avvisi** e impostare il **ridimensionamento** automatico in base a tali metriche.</span><span class="sxs-lookup"><span data-stu-id="fa96d-105">This includes the ability to review **quotas** and **metrics** for an app as well as the App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="fa96d-106">Informazioni su quote e metriche</span><span class="sxs-lookup"><span data-stu-id="fa96d-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="fa96d-107">Quote</span><span class="sxs-lookup"><span data-stu-id="fa96d-107">Quotas</span></span>
<span data-ttu-id="fa96d-108">Le applicazioni ospitate nel servizio app di Azure sono soggette a determinati *limiti* in merito alle risorse che possono usare.</span><span class="sxs-lookup"><span data-stu-id="fa96d-108">Applications hosted in App Service are subject to certain *limits* on the resources they can use.</span></span> <span data-ttu-id="fa96d-109">I limiti sono definiti dal **piano di servizio app** associato all'app.</span><span class="sxs-lookup"><span data-stu-id="fa96d-109">The limits are defined by the **App Service plan** associated with the app.</span></span>

<span data-ttu-id="fa96d-110">Se l'applicazione è ospitata in un piano **gratuito** o **condiviso**, i limiti sulle risorse che l'app può usare sono definiti dalle **quote**.</span><span class="sxs-lookup"><span data-stu-id="fa96d-110">If the application is hosted in a **Free** or **Shared** plan, then the limits on the resources the app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="fa96d-111">Se l'applicazione è ospitata in un piano **Basic**, **Standard** o **Premium**, i limiti sulle risorse che può usare sono definiti dalle **dimensioni** (Small, Medium, Large) e dal **numero di istanze** (1, 2, 3...) del **piano di servizio app**.</span><span class="sxs-lookup"><span data-stu-id="fa96d-111">If the application is hosted in a **Basic**, **Standard** or **Premium** plan, then the limits on the resources they can use are set by the **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of the **App Service plan**.</span></span>

<span data-ttu-id="fa96d-112">Le **quote** per le app ospitate nel piano **gratuito** o **condiviso** sono:</span><span class="sxs-lookup"><span data-stu-id="fa96d-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="fa96d-113">**CPU (breve)**</span><span class="sxs-lookup"><span data-stu-id="fa96d-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="fa96d-114">Quantità di CPU consentita per l'applicazione in un intervallo di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="fa96d-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="fa96d-115">Questa quota viene reimpostata automaticamente ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="fa96d-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="fa96d-116">**CPU (giorno)**</span><span class="sxs-lookup"><span data-stu-id="fa96d-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="fa96d-117">Quantità totale di CPU consentita per l'applicazione in un giorno.</span><span class="sxs-lookup"><span data-stu-id="fa96d-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="fa96d-118">Questa quota viene reimpostata automaticamente ogni 24 ore a mezzanotte (ora UTC).</span><span class="sxs-lookup"><span data-stu-id="fa96d-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="fa96d-119">**Memoria**</span><span class="sxs-lookup"><span data-stu-id="fa96d-119">**Memory**</span></span>
  * <span data-ttu-id="fa96d-120">Quantità totale di memoria consentita per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa96d-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="fa96d-121">**Larghezza di banda**</span><span class="sxs-lookup"><span data-stu-id="fa96d-121">**Bandwidth**</span></span>
  * <span data-ttu-id="fa96d-122">Quantità totale di larghezza di banda in uscita consentita per l'applicazione in un giorno.</span><span class="sxs-lookup"><span data-stu-id="fa96d-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="fa96d-123">Questa quota viene reimpostata automaticamente ogni 24 ore a mezzanotte (ora UTC).</span><span class="sxs-lookup"><span data-stu-id="fa96d-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="fa96d-124">**File system**</span><span class="sxs-lookup"><span data-stu-id="fa96d-124">**Filesystem**</span></span>
  * <span data-ttu-id="fa96d-125">Quantità totale di spazio di archiviazione consentita.</span><span class="sxs-lookup"><span data-stu-id="fa96d-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="fa96d-126">L'unica quota applicabile alle app ospitate nei piani **Basic**, **Standard** e **Premium** è **File system**.</span><span class="sxs-lookup"><span data-stu-id="fa96d-126">The only quota applicable to apps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="fa96d-127">Per altre informazioni su quote, funzionalità e limiti specifici per i diversi SKU del piano di servizio app, vedere i [limiti del servizio della sottoscrizione di Azure](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="fa96d-127">More information about the specific quotas, limits and features available to the different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="fa96d-128">Imposizione della quota</span><span class="sxs-lookup"><span data-stu-id="fa96d-128">Quota Enforcement</span></span>
<span data-ttu-id="fa96d-129">Se l'uso di un'applicazione supera le quote per **CPU (breve)**, **CPU (giorno)** o **larghezza di banda**, l'applicazione verrà arrestata fino al momento in cui viene reimpostata la quota.</span><span class="sxs-lookup"><span data-stu-id="fa96d-129">If an application in its usage exceeds the **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then the application will be stopped until the quota re-sets.</span></span> <span data-ttu-id="fa96d-130">Durante questo periodo, per tutte le richieste in ingresso verrà restituito un errore di tipo **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="fa96d-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="fa96d-131">Se viene superata la quota di **memoria** , l'applicazione viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="fa96d-131">If the application **memory** quota is exceeded, then the application will be re-started.</span></span>

<span data-ttu-id="fa96d-132">Se viene superata la quota per il **file system** , tutte le operazioni di scrittura avranno esito negativo, incluse le operazioni di scrittura nei log.</span><span class="sxs-lookup"><span data-stu-id="fa96d-132">If the **Filesystem** quota is exceeded, then any write operation will fail, this includes writing to logs.</span></span>

<span data-ttu-id="fa96d-133">È possibile aumentare o rimuovere le quote dall'app aggiornando il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="fa96d-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="fa96d-134">Metrica</span><span class="sxs-lookup"><span data-stu-id="fa96d-134">Metrics</span></span>
<span data-ttu-id="fa96d-135">**Metrica** forniscono informazioni sull'app o sul comportamento del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="fa96d-135">**Metrics** provide information about the app, or App Service plan's behavior.</span></span>

<span data-ttu-id="fa96d-136">Per un' **applicazione**, le metriche disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="fa96d-136">For an **Application**, the available metrics are:</span></span>

* <span data-ttu-id="fa96d-137">**Tempo medio di risposta**</span><span class="sxs-lookup"><span data-stu-id="fa96d-137">**Average Response Time**</span></span>
  * <span data-ttu-id="fa96d-138">Tempo medio impiegato dall'app per gestire le richieste, in millisecondi.</span><span class="sxs-lookup"><span data-stu-id="fa96d-138">The average time taken for the app to serve requests in ms.</span></span>
* <span data-ttu-id="fa96d-139">**Working set della memoria medio**</span><span class="sxs-lookup"><span data-stu-id="fa96d-139">**Average memory working set**</span></span>
  * <span data-ttu-id="fa96d-140">Quantità media di memoria usata dall'app, in MiB.</span><span class="sxs-lookup"><span data-stu-id="fa96d-140">The average amount of memory in MiBs used by the app.</span></span>
* <span data-ttu-id="fa96d-141">**Tempo CPU**</span><span class="sxs-lookup"><span data-stu-id="fa96d-141">**CPU Time**</span></span>
  * <span data-ttu-id="fa96d-142">Quantità di CPU utilizzata dall'app, in secondi.</span><span class="sxs-lookup"><span data-stu-id="fa96d-142">The amount of CPU in seconds consumed by the app.</span></span> <span data-ttu-id="fa96d-143">Per altre informazioni su questa metrica, vedere [Tempo CPU e percentuale CPU](#cpu-time-vs-cpu-percentage)</span><span class="sxs-lookup"><span data-stu-id="fa96d-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="fa96d-144">**Dati in entrata**</span><span class="sxs-lookup"><span data-stu-id="fa96d-144">**Data In**</span></span>
  * <span data-ttu-id="fa96d-145">Quantità di larghezza di banda in entrata utilizzata dall'app, in MiB.</span><span class="sxs-lookup"><span data-stu-id="fa96d-145">The amount of incoming bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="fa96d-146">**Dati in uscita**</span><span class="sxs-lookup"><span data-stu-id="fa96d-146">**Data Out**</span></span>
  * <span data-ttu-id="fa96d-147">Quantità di larghezza di banda in uscita utilizzata dall'app, in MiB.</span><span class="sxs-lookup"><span data-stu-id="fa96d-147">The amount of outgoing bandwidth consumed by the app in MiBs.</span></span>
* <span data-ttu-id="fa96d-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="fa96d-148">**Http 2xx**</span></span>
  * <span data-ttu-id="fa96d-149">Numero di richieste che hanno restituito un codice di stato HTTP >= 200 e < 300.</span><span class="sxs-lookup"><span data-stu-id="fa96d-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="fa96d-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="fa96d-150">**Http 3xx**</span></span>
  * <span data-ttu-id="fa96d-151">Numero di richieste che hanno restituito un codice di stato HTTP >= 300 e < 400.</span><span class="sxs-lookup"><span data-stu-id="fa96d-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="fa96d-152">**Http 401**</span><span class="sxs-lookup"><span data-stu-id="fa96d-152">**Http 401**</span></span>
  * <span data-ttu-id="fa96d-153">Numero di richieste che hanno restituito un codice di stato HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="fa96d-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="fa96d-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="fa96d-154">**Http 403**</span></span>
  * <span data-ttu-id="fa96d-155">Numero di richieste che hanno restituito un codice di stato HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="fa96d-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="fa96d-156">**Http 404**</span><span class="sxs-lookup"><span data-stu-id="fa96d-156">**Http 404**</span></span>
  * <span data-ttu-id="fa96d-157">Numero di richieste che hanno restituito un codice di stato HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="fa96d-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="fa96d-158">**Http 406**</span><span class="sxs-lookup"><span data-stu-id="fa96d-158">**Http 406**</span></span>
  * <span data-ttu-id="fa96d-159">Numero di richieste che hanno restituito un codice di stato HTTP 406.</span><span class="sxs-lookup"><span data-stu-id="fa96d-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="fa96d-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="fa96d-160">**Http 4xx**</span></span>
  * <span data-ttu-id="fa96d-161">Numero di richieste che hanno restituito un codice di stato HTTP >= 400 e < 500.</span><span class="sxs-lookup"><span data-stu-id="fa96d-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="fa96d-162">**Errori server HTTP**</span><span class="sxs-lookup"><span data-stu-id="fa96d-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="fa96d-163">Numero di richieste che hanno restituito un codice di stato HTTP >= 500 e < 600.</span><span class="sxs-lookup"><span data-stu-id="fa96d-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="fa96d-164">**Working set della memoria**</span><span class="sxs-lookup"><span data-stu-id="fa96d-164">**Memory working set**</span></span>
  * <span data-ttu-id="fa96d-165">Quantità di memoria corrente usata dall'app, in MiB.</span><span class="sxs-lookup"><span data-stu-id="fa96d-165">Current amount of memory used by the app in MiBs.</span></span>
* <span data-ttu-id="fa96d-166">**Richieste**</span><span class="sxs-lookup"><span data-stu-id="fa96d-166">**Requests**</span></span>
  * <span data-ttu-id="fa96d-167">Numero totale di richieste, indipendentemente dal codice di stato HTTP restituito.</span><span class="sxs-lookup"><span data-stu-id="fa96d-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="fa96d-168">Per un **piano di servizio app**, le metriche disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="fa96d-168">For an **App Service plan**, the available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="fa96d-169">Le metriche del piano di servizio app sono disponibili solo per i piani nello SKU **Basic**, **Standard** e **Premium**.</span><span class="sxs-lookup"><span data-stu-id="fa96d-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="fa96d-170">**Percentuale di CPU**</span><span class="sxs-lookup"><span data-stu-id="fa96d-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="fa96d-171">CPU media usata tra tutte le istanze del piano.</span><span class="sxs-lookup"><span data-stu-id="fa96d-171">The average CPU used across all instances of the plan.</span></span>
* <span data-ttu-id="fa96d-172">**Percentuale memoria**</span><span class="sxs-lookup"><span data-stu-id="fa96d-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="fa96d-173">Memoria media usata tra tutte le istanze del piano.</span><span class="sxs-lookup"><span data-stu-id="fa96d-173">The average memory used across all instances of the plan.</span></span>
* <span data-ttu-id="fa96d-174">**Dati in entrata**</span><span class="sxs-lookup"><span data-stu-id="fa96d-174">**Data In**</span></span>
  * <span data-ttu-id="fa96d-175">Larghezza di banda in ingresso media usata tra tutte le istanze del piano.</span><span class="sxs-lookup"><span data-stu-id="fa96d-175">The average incoming bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="fa96d-176">**Dati in uscita**</span><span class="sxs-lookup"><span data-stu-id="fa96d-176">**Data Out**</span></span>
  * <span data-ttu-id="fa96d-177">Larghezza di banda in uscita media usata tra tutte le istanze del piano.</span><span class="sxs-lookup"><span data-stu-id="fa96d-177">The average outgoing bandwidth used across all instances of the plan.</span></span>
* <span data-ttu-id="fa96d-178">**Lunghezza coda disco**</span><span class="sxs-lookup"><span data-stu-id="fa96d-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="fa96d-179">Numero medio di richieste di lettura e scrittura accodate nella risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fa96d-179">The average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="fa96d-180">Una lunghezza coda disco elevata può indicare il rallentamento di un'applicazione a causa di operazioni di I/O su disco eccessive.</span><span class="sxs-lookup"><span data-stu-id="fa96d-180">A high disk queue length is an indication of an application that might be slowing down due to excessive disk I/O.</span></span>
* <span data-ttu-id="fa96d-181">**Lunghezza coda HTTP**</span><span class="sxs-lookup"><span data-stu-id="fa96d-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="fa96d-182">Numero medio di richieste HTTP che hanno dovuto attendere in coda prima di essere completate.</span><span class="sxs-lookup"><span data-stu-id="fa96d-182">The average number of HTTP requests that had to sit on the queue before being fulfilled.</span></span> <span data-ttu-id="fa96d-183">Una lunghezza coda HTTP elevata o in aumento indica che il piano si trova in condizioni di carico eccessivo.</span><span class="sxs-lookup"><span data-stu-id="fa96d-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="fa96d-184">Tempo CPU e percentuale CPU</span><span class="sxs-lookup"><span data-stu-id="fa96d-184">CPU time vs CPU percentage</span></span>
<!-- To do: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="fa96d-185">Le metriche che riflettono l'utilizzo della CPU sono due.</span><span class="sxs-lookup"><span data-stu-id="fa96d-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="fa96d-186">**Tempo CPU** e **Percentuale CPU**</span><span class="sxs-lookup"><span data-stu-id="fa96d-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="fa96d-187">**Tempo CPU** è utile per le app ospitate nei piani **gratuito** o **condiviso**, dal momento che una delle relative quote è definita in minuti di CPU usati dall'app.</span><span class="sxs-lookup"><span data-stu-id="fa96d-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by the app.</span></span>

<span data-ttu-id="fa96d-188">**Percentuale CPU** è invece utile per le app ospitate nei piani **Basic**, **Standard** e **Premium** dal momento che è possibile aumentarne il numero di istanze. Questa metrica è un ottimo indicatore dell'uso complessivo in tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="fa96d-188">**CPU percentage** on the other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of the overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="fa96d-189">Granularità delle metriche e criteri di conservazione</span><span class="sxs-lookup"><span data-stu-id="fa96d-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="fa96d-190">Le metriche per un'applicazione e un piano di servizio app vengono registrate e aggregate dal servizio con le granularità e i criteri di conservazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa96d-190">Metrics for an application and app service plan are logged and aggregated by the service with the following granularities and retention policies:</span></span>

* <span data-ttu-id="fa96d-191">Le metriche di granularità **minuto** vengono mantenute per **48 ore**</span><span class="sxs-lookup"><span data-stu-id="fa96d-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="fa96d-192">Le metriche di granularità **ora** vengono mantenute per **30 giorni**</span><span class="sxs-lookup"><span data-stu-id="fa96d-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="fa96d-193">Le metriche di granularità **giorno** vengono mantenute per **90 giorni**</span><span class="sxs-lookup"><span data-stu-id="fa96d-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-the-azure-portal"></a><span data-ttu-id="fa96d-194">Monitoraggio di quote e metriche nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fa96d-194">Monitoring Quotas and Metrics in the Azure Portal.</span></span>
<span data-ttu-id="fa96d-195">È possibile esaminare lo stato delle diverse **quote** e **metriche** che interessano un'applicazione nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fa96d-195">You can review the status of the different **quotas** and **metrics** affecting an application in the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="fa96d-196">Le ![][quotas]
**quote** sono disponibili in Impostazioni>**Quote**.</span><span class="sxs-lookup"><span data-stu-id="fa96d-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="fa96d-197">L'interfaccia utente consente di esaminare: (1) nomi delle quote, (2) intervallo di reimpostazione, (3) limiti correnti e (4) valore corrente.</span><span class="sxs-lookup"><span data-stu-id="fa96d-197">The UX allows you to review: (1) the quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="fa96d-198">Le ![][metrics]
**metriche** sono accessibili direttamente dal pannello delle risorse.</span><span class="sxs-lookup"><span data-stu-id="fa96d-198">![][metrics]
**Metrics** can be access directly from the resource blade.</span></span> <span data-ttu-id="fa96d-199">Per personalizzare il grafico: (1) **fare clic** su di esso e selezionare (2) **Modifica grafico**.</span><span class="sxs-lookup"><span data-stu-id="fa96d-199">You can also customize the chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="fa96d-200">Da qui è possibile modificare le opzioni relative a (3) **intervallo di tempo**, (4) **tipo di grafico** e (5) **metriche** da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="fa96d-200">From here you can change the (3) **time range**, (4) **chart type**, and (5) **metrics** to display.</span></span>  

<span data-ttu-id="fa96d-201">Per altre informazioni sulle metriche, vedere [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) (Monitorare le metriche del servizio).</span><span class="sxs-lookup"><span data-stu-id="fa96d-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="fa96d-202">Avvisi e scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="fa96d-202">Alerts and Autoscale</span></span>
<span data-ttu-id="fa96d-203">È possibile collegare le metriche per un'app o un piano di servizio app agli avvisi. Per altre informazioni, vedere [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) (Ricevere notifiche di avviso)</span><span class="sxs-lookup"><span data-stu-id="fa96d-203">Metrics for an App or App Service plan can be hooked up to alerts, to learn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="fa96d-204">Le app del servizio app ospitate nei piani di servizio app Basic, Standard e Premium supportano la **scalabilità automatica**.</span><span class="sxs-lookup"><span data-stu-id="fa96d-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="fa96d-205">È quindi possibile configurare regole per il monitoraggio delle metriche del piano di servizio app e aumentare o ridurre automaticamente il numero di istanze per fornire risorse aggiuntive quando necessario o per risparmiare denaro quando il provisioning dell'applicazione è eccessivo rispetto all'utilizzo effettivo.</span><span class="sxs-lookup"><span data-stu-id="fa96d-205">This allows you to configure rules that monitor the App Service plan metrics and can increase or decrease the instance count providing additional resources as needed, or saving money when the application is over-provision.</span></span> <span data-ttu-id="fa96d-206">Per altre informazioni sul ridimensionamento automatico, vedere [How to Scale](../monitoring-and-diagnostics/insights-how-to-scale.md) (Come ridimensionare) e [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md) (Procedure consigliate per il ridimensionamento automatico in Monitoraggio di Azure)</span><span class="sxs-lookup"><span data-stu-id="fa96d-206">You can learn more about auto scale here: [How to Scale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="fa96d-207">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="fa96d-207">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="fa96d-208">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="fa96d-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="fa96d-209">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="fa96d-209">What's changed</span></span>
* <span data-ttu-id="fa96d-210">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="fa96d-210">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
