---
title: App in Azure App Service aaaMonitor | Documenti Microsoft
description: Informazioni su come toomonitor App in Azure App Service tramite hello portale di Azure.
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
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="0c5a5-103">Procedura: Eseguire il monitoraggio delle app nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="0c5a5-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="0c5a5-104">[Servizio app](http://go.microsoft.com/fwlink/?LinkId=529714) fornisce funzionalità di monitoraggio incorporate hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c5a5-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in hello [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="0c5a5-105">Sono inclusi hello possibilità tooreview **quote** e **metriche** per un'app, nonché hello piano di servizio App, impostazione **avvisi** e anche **scalabilità** automaticamente in base queste metriche.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-105">This includes hello ability tooreview **quotas** and **metrics** for an app as well as hello App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="0c5a5-106">Informazioni su quote e metriche</span><span class="sxs-lookup"><span data-stu-id="0c5a5-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="0c5a5-107">Quote</span><span class="sxs-lookup"><span data-stu-id="0c5a5-107">Quotas</span></span>
<span data-ttu-id="0c5a5-108">Le applicazioni ospitate nel servizio App sono soggetto toocertain *limiti* sulle risorse possono utilizzare.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-108">Applications hosted in App Service are subject toocertain *limits* on the resources they can use.</span></span> <span data-ttu-id="0c5a5-109">Hello limiti sono definiti dai hello **piano di servizio App** associati hello app.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-109">hello limits are defined by hello **App Service plan** associated with hello app.</span></span>

<span data-ttu-id="0c5a5-110">Se un'applicazione hello è ospitata in un **libero** o **Shared** piano, quindi hello limiti sulle risorse hello app hello è possibile utilizzare sono definiti dai **quote**.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-110">If hello application is hosted in a **Free** or **Shared** plan, then hello limits on hello resources hello app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="0c5a5-111">Se un'applicazione hello è ospitata in un **base**, **Standard** o **Premium** piano, quindi i limiti di hello risorse hello possono utilizzare vengono impostati da hello **dimensioni** (Piccolo, medio, grande) e **numero** (1, 2, 3,...) di hello **piano di servizio App**.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-111">If hello application is hosted in a **Basic**, **Standard** or **Premium** plan, then hello limits on hello resources they can use are set by hello **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of hello **App Service plan**.</span></span>

<span data-ttu-id="0c5a5-112">Le **quote** per le app ospitate nel piano **gratuito** o **condiviso** sono:</span><span class="sxs-lookup"><span data-stu-id="0c5a5-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="0c5a5-113">**CPU (breve)**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="0c5a5-114">Quantità di CPU consentita per l'applicazione in un intervallo di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="0c5a5-115">Questa quota viene reimpostata automaticamente ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="0c5a5-116">**CPU (giorno)**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="0c5a5-117">Quantità totale di CPU consentita per l'applicazione in un giorno.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="0c5a5-118">Questa quota viene reimpostata automaticamente ogni 24 ore a mezzanotte (ora UTC).</span><span class="sxs-lookup"><span data-stu-id="0c5a5-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="0c5a5-119">**Memoria**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-119">**Memory**</span></span>
  * <span data-ttu-id="0c5a5-120">Quantità totale di memoria consentita per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="0c5a5-121">**Larghezza di banda**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-121">**Bandwidth**</span></span>
  * <span data-ttu-id="0c5a5-122">Quantità totale di larghezza di banda in uscita consentita per l'applicazione in un giorno.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="0c5a5-123">Questa quota viene reimpostata automaticamente ogni 24 ore a mezzanotte (ora UTC).</span><span class="sxs-lookup"><span data-stu-id="0c5a5-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="0c5a5-124">**File system**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-124">**Filesystem**</span></span>
  * <span data-ttu-id="0c5a5-125">Quantità totale di spazio di archiviazione consentita.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="0c5a5-126">Hello solo quota applicabile tooapps ospitato in **base**, **Standard** e **Premium** piani è **Filesystem**.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-126">hello only quota applicable tooapps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="0c5a5-127">Ulteriori informazioni sulle quote specifiche di hello, limiti e funzionalità disponibili per hello diverse SKU di servizio App è reperibile qui: [i limiti del servizio di sottoscrizione Azure](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="0c5a5-127">More information about hello specific quotas, limits and features available to hello different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="0c5a5-128">Imposizione della quota</span><span class="sxs-lookup"><span data-stu-id="0c5a5-128">Quota Enforcement</span></span>
<span data-ttu-id="0c5a5-129">Se un'applicazione nell'utilizzo supera hello **CPU (breve)**, **CPU (giorno)**, o **della larghezza di banda** quota quindi hello applicazione verrà arrestata fino a quando non imposta nuovamente quota hello.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-129">If an application in its usage exceeds hello **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then hello application will be stopped until hello quota re-sets.</span></span> <span data-ttu-id="0c5a5-130">Durante questo periodo, per tutte le richieste in ingresso verrà restituito un errore di tipo **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="0c5a5-131">Se hello applicazione **memoria** quota viene superata, quindi l'applicazione hello sarà riavviata.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-131">If hello application **memory** quota is exceeded, then hello application will be re-started.</span></span>

<span data-ttu-id="0c5a5-132">Se hello **Filesystem** quota viene superata, quindi qualsiasi operazione avrà esito negativo, incluso scrittura toologs di scrittura.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-132">If hello **Filesystem** quota is exceeded, then any write operation will fail, this includes writing toologs.</span></span>

<span data-ttu-id="0c5a5-133">È possibile aumentare o rimuovere le quote dall'app aggiornando il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="0c5a5-134">Metrica</span><span class="sxs-lookup"><span data-stu-id="0c5a5-134">Metrics</span></span>
<span data-ttu-id="0c5a5-135">**Metriche** forniscono informazioni sull'applicazione hello o il comportamento del piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-135">**Metrics** provide information about hello app, or App Service plan's behavior.</span></span>

<span data-ttu-id="0c5a5-136">Per un **applicazione**, hello disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="0c5a5-136">For an **Application**, hello available metrics are:</span></span>

* <span data-ttu-id="0c5a5-137">**Tempo medio di risposta**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-137">**Average Response Time**</span></span>
  * <span data-ttu-id="0c5a5-138">Hello tempo medio per le richieste di tooserve app hello in ms.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-138">hello average time taken for hello app tooserve requests in ms.</span></span>
* <span data-ttu-id="0c5a5-139">**Working set della memoria medio**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-139">**Average memory working set**</span></span>
  * <span data-ttu-id="0c5a5-140">quantità media di Hello di memoria usata dall'app hello MIB.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-140">hello average amount of memory in MiBs used by hello app.</span></span>
* <span data-ttu-id="0c5a5-141">**Tempo CPU**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-141">**CPU Time**</span></span>
  * <span data-ttu-id="0c5a5-142">quantità di Hello di CPU in secondi usati da app hello.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-142">hello amount of CPU in seconds consumed by hello app.</span></span> <span data-ttu-id="0c5a5-143">Per altre informazioni su questa metrica, vedere [Tempo CPU e percentuale CPU](#cpu-time-vs-cpu-percentage)</span><span class="sxs-lookup"><span data-stu-id="0c5a5-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="0c5a5-144">**Dati in entrata**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-144">**Data In**</span></span>
  * <span data-ttu-id="0c5a5-145">quantità di Hello di larghezza di banda in ingresso utilizzata dall'applicazione hello in MIB.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-145">hello amount of incoming bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="0c5a5-146">**Dati in uscita**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-146">**Data Out**</span></span>
  * <span data-ttu-id="0c5a5-147">quantità di Hello di larghezza di banda in uscita utilizzata dall'applicazione hello in MIB.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-147">hello amount of outgoing bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="0c5a5-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-148">**Http 2xx**</span></span>
  * <span data-ttu-id="0c5a5-149">Numero di richieste che hanno restituito un codice di stato HTTP >= 200 e < 300.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="0c5a5-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-150">**Http 3xx**</span></span>
  * <span data-ttu-id="0c5a5-151">Numero di richieste che hanno restituito un codice di stato HTTP >= 300 e < 400.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="0c5a5-152">**Http 401**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-152">**Http 401**</span></span>
  * <span data-ttu-id="0c5a5-153">Numero di richieste che hanno restituito un codice di stato HTTP 401.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="0c5a5-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-154">**Http 403**</span></span>
  * <span data-ttu-id="0c5a5-155">Numero di richieste che hanno restituito un codice di stato HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="0c5a5-156">**Http 404**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-156">**Http 404**</span></span>
  * <span data-ttu-id="0c5a5-157">Numero di richieste che hanno restituito un codice di stato HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="0c5a5-158">**Http 406**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-158">**Http 406**</span></span>
  * <span data-ttu-id="0c5a5-159">Numero di richieste che hanno restituito un codice di stato HTTP 406.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="0c5a5-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-160">**Http 4xx**</span></span>
  * <span data-ttu-id="0c5a5-161">Numero di richieste che hanno restituito un codice di stato HTTP >= 400 e < 500.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="0c5a5-162">**Errori server HTTP**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="0c5a5-163">Numero di richieste che hanno restituito un codice di stato HTTP >= 500 e < 600.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="0c5a5-164">**Working set della memoria**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-164">**Memory working set**</span></span>
  * <span data-ttu-id="0c5a5-165">Quantità corrente di memoria utilizzata dall'applicazione hello in MIB.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-165">Current amount of memory used by hello app in MiBs.</span></span>
* <span data-ttu-id="0c5a5-166">**Richieste**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-166">**Requests**</span></span>
  * <span data-ttu-id="0c5a5-167">Numero totale di richieste, indipendentemente dal codice di stato HTTP restituito.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="0c5a5-168">Per un **piano di servizio App**, hello disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="0c5a5-168">For an **App Service plan**, hello available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="0c5a5-169">Le metriche del piano di servizio app sono disponibili solo per i piani nello SKU **Basic**, **Standard** e **Premium**.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="0c5a5-170">**Percentuale di CPU**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="0c5a5-171">Hello utilizzo medio della CPU utilizzato da tutte le istanze del piano di hello.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-171">hello average CPU used across all instances of hello plan.</span></span>
* <span data-ttu-id="0c5a5-172">**Percentuale memoria**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="0c5a5-173">Hello Media della memoria utilizzata in tutte le istanze del piano di hello.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-173">hello average memory used across all instances of hello plan.</span></span>
* <span data-ttu-id="0c5a5-174">**Dati in entrata**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-174">**Data In**</span></span>
  * <span data-ttu-id="0c5a5-175">Hello in arrivo larghezza di banda media utilizzata in tutte le istanze del piano di hello.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-175">hello average incoming bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="0c5a5-176">**Dati in uscita**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-176">**Data Out**</span></span>
  * <span data-ttu-id="0c5a5-177">Media di Hello in uscita di larghezza di banda utilizzata in tutte le istanze del piano di hello.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-177">hello average outgoing bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="0c5a5-178">**Lunghezza coda disco**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="0c5a5-179">numero medio di Hello di lettura sia richieste messe in coda di scrittura nell'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-179">hello average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="0c5a5-180">Una coda del disco elevato è un'indicazione di un'applicazione che potrebbe rallentare a causa dei / o disco tooexcessive.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-180">A high disk queue length is an indication of an application that might be slowing down due tooexcessive disk I/O.</span></span>
* <span data-ttu-id="0c5a5-181">**Lunghezza coda HTTP**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="0c5a5-182">numero medio di Hello di richieste HTTP che ha toosit in coda hello prima sono soddisfatte.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-182">hello average number of HTTP requests that had toosit on hello queue before being fulfilled.</span></span> <span data-ttu-id="0c5a5-183">Una lunghezza coda HTTP elevata o in aumento indica che il piano si trova in condizioni di carico eccessivo.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="0c5a5-184">Tempo CPU e percentuale CPU</span><span class="sxs-lookup"><span data-stu-id="0c5a5-184">CPU time vs CPU percentage</span></span>
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="0c5a5-185">Le metriche che riflettono l'utilizzo della CPU sono due.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="0c5a5-186">**Tempo CPU** e **Percentuale CPU**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="0c5a5-187">**Tempo di CPU** è utile per le app ospitate in **libero** o **Shared** piani perché una delle rispettive quote è definita in minuti della CPU usati dall'app hello.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by hello app.</span></span>

<span data-ttu-id="0c5a5-188">**Percentuale CPU** su hello invece è utile per le app ospitate in **base**, **standard** e **premium** piani poiché può essere ampliati e questa metrica è una valida indicazione hello utilizzo complessivo per tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-188">**CPU percentage** on hello other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of hello overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="0c5a5-189">Granularità delle metriche e criteri di conservazione</span><span class="sxs-lookup"><span data-stu-id="0c5a5-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="0c5a5-190">Le metriche per un piano di servizio app e di applicazione sono registrate e aggregate da servizio hello con hello seguenti criteri di conservazione e granularità:</span><span class="sxs-lookup"><span data-stu-id="0c5a5-190">Metrics for an application and app service plan are logged and aggregated by hello service with hello following granularities and retention policies:</span></span>

* <span data-ttu-id="0c5a5-191">Le metriche di granularità **minuto** vengono mantenute per **48 ore**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="0c5a5-192">Le metriche di granularità **ora** vengono mantenute per **30 giorni**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="0c5a5-193">Le metriche di granularità **giorno** vengono mantenute per **90 giorni**</span><span class="sxs-lookup"><span data-stu-id="0c5a5-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a><span data-ttu-id="0c5a5-194">Monitoraggio delle quote e le metriche nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-194">Monitoring Quotas and Metrics in hello Azure Portal.</span></span>
<span data-ttu-id="0c5a5-195">È possibile esaminare lo stato di hello di hello diversi **quote** e **metriche** influire su un'applicazione hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c5a5-195">You can review hello status of hello different **quotas** and **metrics** affecting an application in hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="0c5a5-196">Le ![][quotas]
**quote** sono disponibili in Impostazioni>**Quote**.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="0c5a5-197">Hello UX consente di esaminare: nome quote hello (1), (2) l'intervallo di ripristino, (3) il limite corrente e valore (4) corrente.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-197">hello UX allows you to review: (1) hello quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="0c5a5-198">![][metrics]
**Metriche** è possibile accedere direttamente dal pannello della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-198">![][metrics]
**Metrics** can be access directly from hello resource blade.</span></span> <span data-ttu-id="0c5a5-199">È inoltre possibile personalizzare il grafico hello da: (1) **fare clic su** su di esso e (2) selezionare **Modifica grafico**.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-199">You can also customize hello chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="0c5a5-200">Da qui è possibile modificare hello (3) **intervallo di tempo**, (4) **tipo di grafico**e (5) **metriche** toodisplay.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-200">From here you can change hello (3) **time range**, (4) **chart type**, and (5) **metrics** toodisplay.</span></span>  

<span data-ttu-id="0c5a5-201">Per altre informazioni sulle metriche, vedere [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) (Monitorare le metriche del servizio).</span><span class="sxs-lookup"><span data-stu-id="0c5a5-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="0c5a5-202">Avvisi e scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="0c5a5-202">Alerts and Autoscale</span></span>
<span data-ttu-id="0c5a5-203">Le metriche per un piano di App o un servizio App può essere agganciato tooalerts, toolearn ulteriori informazioni, vedere [ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="0c5a5-203">Metrics for an App or App Service plan can be hooked up tooalerts, toolearn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="0c5a5-204">Le app del servizio app ospitate nei piani di servizio app Basic, Standard e Premium supportano la **scalabilità automatica**.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="0c5a5-205">In questo modo si tooconfigure regole che di monitorare le metriche del piano di servizio App e possono aumentare o diminuire il numero di istanze hello fornendo risorse aggiuntive in base alle esigenze o salvataggio money quando un'applicazione hello è effettuare il provisioning in eccesso.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-205">This allows you tooconfigure rules that monitor the App Service plan metrics and can increase or decrease hello instance count providing additional resources as needed, or saving money when hello application is over-provision.</span></span> <span data-ttu-id="0c5a5-206">È possibile approfondire qui scalabilità automatica: [come tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) e qui [procedure consigliate per la scalabilità automatica di monitoraggio di Azure](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="0c5a5-206">You can learn more about auto scale here: [How tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="0c5a5-207">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-207">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0c5a5-208">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="0c5a5-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="0c5a5-209">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="0c5a5-209">What's changed</span></span>
* <span data-ttu-id="0c5a5-210">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="0c5a5-210">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
