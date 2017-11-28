---
title: aaaAzure modello dati di telemetria Insights di applicazione - contesto dati di telemetria | Documenti Microsoft
description: Modello di contesto dei dati di telemetria di Application Insights
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="bed07-103">Contesto dei dati di telemetria: modello di dati di Application Insights</span><span class="sxs-lookup"><span data-stu-id="bed07-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="bed07-104">Ogni elemento di telemetria può contenere campi di contesto fortemente tipizzati.</span><span class="sxs-lookup"><span data-stu-id="bed07-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="bed07-105">Ogni campo consente uno specifico scenario di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="bed07-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="bed07-106">Utilizzare hello proprietà personalizzate della raccolta toostore personalizzati o specifici dell'applicazione le informazioni contestuali.</span><span class="sxs-lookup"><span data-stu-id="bed07-106">Use hello custom properties collection toostore custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="bed07-107">Versione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="bed07-107">Application version</span></span>

<span data-ttu-id="bed07-108">Le informazioni nei campi di contesto dell'applicazione hello sono sempre sull'applicazione hello che invia i dati di telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-108">Information in hello application context fields is always about hello application that is sending hello telemetry.</span></span> <span data-ttu-id="bed07-109">Versione dell'applicazione è utilizzata tooanalyze tendenza modifiche nel comportamento dell'applicazione hello e le relative distribuzioni toohello correlazione.</span><span class="sxs-lookup"><span data-stu-id="bed07-109">Application version is used tooanalyze trend changes in hello application behavior and its correlation toohello deployments.</span></span>

<span data-ttu-id="bed07-110">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="bed07-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="bed07-111">Indirizzo IP client</span><span class="sxs-lookup"><span data-stu-id="bed07-111">Client IP address</span></span>

<span data-ttu-id="bed07-112">indirizzo IP di Hello del dispositivo client hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-112">hello IP address of hello client device.</span></span> <span data-ttu-id="bed07-113">Sono supportati sia IPv4 che IPv6.</span><span class="sxs-lookup"><span data-stu-id="bed07-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="bed07-114">Quando i dati di telemetria viene inviato da un servizio, il contesto di percorso hello è sull'utente hello che ha avviato l'operazione di hello in servizio hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-114">When telemetry is sent from a service, hello location context is about hello user that initiated hello operation in hello service.</span></span> <span data-ttu-id="bed07-115">Application Insights estrarre le informazioni di posizione geografica hello da indirizzo IP del client hello e quindi troncarlo.</span><span class="sxs-lookup"><span data-stu-id="bed07-115">Application Insights extract hello geo-location information from hello client IP and then truncate it.</span></span> <span data-ttu-id="bed07-116">L'IP client da solo non può quindi essere usato come informazione personale dell'utente finale.</span><span class="sxs-lookup"><span data-stu-id="bed07-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="bed07-117">Lunghezza massima: 46</span><span class="sxs-lookup"><span data-stu-id="bed07-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="bed07-118">Tipo di dispositivo</span><span class="sxs-lookup"><span data-stu-id="bed07-118">Device type</span></span>

<span data-ttu-id="bed07-119">Originariamente questo campo è stato utilizzato il tipo di hello tooindicate hello hello finale dell'utente di dispositivo di un'applicazione hello utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bed07-119">Originally this field was used tooindicate hello type of hello device hello end user of hello application is using.</span></span> <span data-ttu-id="bed07-120">Oggi utilizzato principalmente toodistinguish JavaScript telemetria con hello tipo di dispositivo 'Browser' dalla telemetria sul lato server con il tipo di dispositivo hello 'Computer'.</span><span class="sxs-lookup"><span data-stu-id="bed07-120">Today used primarily toodistinguish JavaScript telemetry with hello device type 'Browser' from server-side telemetry with hello device type 'PC'.</span></span>

<span data-ttu-id="bed07-121">Lunghezza massima: 64</span><span class="sxs-lookup"><span data-stu-id="bed07-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="bed07-122">ID operazione</span><span class="sxs-lookup"><span data-stu-id="bed07-122">Operation id</span></span>

<span data-ttu-id="bed07-123">Identificatore univoco dell'operazione di hello radice.</span><span class="sxs-lookup"><span data-stu-id="bed07-123">A unique identifier of hello root operation.</span></span> <span data-ttu-id="bed07-124">Questo identificatore consente telemetria toogroup tra più componenti.</span><span class="sxs-lookup"><span data-stu-id="bed07-124">This identifier allows toogroup telemetry across multiple components.</span></span> <span data-ttu-id="bed07-125">Per informazioni dettagliate, vedere [Correlazione di dati di telemetria](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="bed07-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="bed07-126">id operazione Hello viene creato da una richiesta o una visualizzazione di pagina.</span><span class="sxs-lookup"><span data-stu-id="bed07-126">hello operation id is created by either a request or a page view.</span></span> <span data-ttu-id="bed07-127">Tutti gli altri dati di telemetria imposta questo valore del campo toohello per hello contenente la vista richiesta o della pagina.</span><span class="sxs-lookup"><span data-stu-id="bed07-127">All other telemetry sets this field toohello value for hello containing request or page view.</span></span> 

<span data-ttu-id="bed07-128">Lunghezza massima: 128</span><span class="sxs-lookup"><span data-stu-id="bed07-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="bed07-129">ID operazione padre</span><span class="sxs-lookup"><span data-stu-id="bed07-129">Parent operation ID</span></span>

<span data-ttu-id="bed07-130">Identificatore univoco del padre dell'elemento di dati di telemetria hello di Hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-130">hello unique identifier of hello telemetry item's immediate parent.</span></span> <span data-ttu-id="bed07-131">Per informazioni dettagliate, vedere [Correlazione di dati di telemetria](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="bed07-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="bed07-132">Lunghezza massima: 128</span><span class="sxs-lookup"><span data-stu-id="bed07-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="bed07-133">Nome operazione</span><span class="sxs-lookup"><span data-stu-id="bed07-133">Operation name</span></span>

<span data-ttu-id="bed07-134">nome di Hello (gruppo) dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-134">hello name (group) of hello operation.</span></span> <span data-ttu-id="bed07-135">nome dell'operazione Hello viene creato da una richiesta o una visualizzazione di pagina.</span><span class="sxs-lookup"><span data-stu-id="bed07-135">hello operation name is created by either a request or a page view.</span></span> <span data-ttu-id="bed07-136">Tutti gli altri elementi di dati di telemetria impostare questo valore del campo toohello per hello contenente la vista richiesta o della pagina.</span><span class="sxs-lookup"><span data-stu-id="bed07-136">All other telemetry items set this field toohello value for hello containing request or page view.</span></span> <span data-ttu-id="bed07-137">Nome dell'operazione viene utilizzato per la ricerca di tutti gli elementi di dati di telemetria hello per un gruppo di operazioni (ad esempio ' GET Home/Index').</span><span class="sxs-lookup"><span data-stu-id="bed07-137">Operation name is used for finding all hello telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="bed07-138">Questa proprietà di contesto viene utilizzato tooanswer domande quali "quali sono hello tipico eccezioni in questa pagina."</span><span class="sxs-lookup"><span data-stu-id="bed07-138">This context property is used tooanswer questions like "what are hello typical exceptions thrown on this page."</span></span>

<span data-ttu-id="bed07-139">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="bed07-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-hello-operation"></a><span data-ttu-id="bed07-140">Sintetica origine dell'operazione di hello</span><span class="sxs-lookup"><span data-stu-id="bed07-140">Synthetic source of hello operation</span></span>

<span data-ttu-id="bed07-141">Il nome dell'origine sintetica.</span><span class="sxs-lookup"><span data-stu-id="bed07-141">Name of synthetic source.</span></span> <span data-ttu-id="bed07-142">Alcuni dati di telemetria da un'applicazione hello può rappresentare traffico sintetico.</span><span class="sxs-lookup"><span data-stu-id="bed07-142">Some telemetry from hello application may represent synthetic traffic.</span></span> <span data-ttu-id="bed07-143">È possibile crawler indicizzazione hello web sito, il test di disponibilità del sito o le tracce da librerie di diagnostica come Application Insights SDK se stesso.</span><span class="sxs-lookup"><span data-stu-id="bed07-143">It may be web crawler indexing hello web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="bed07-144">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="bed07-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="bed07-145">ID sessione</span><span class="sxs-lookup"><span data-stu-id="bed07-145">Session id</span></span>

<span data-ttu-id="bed07-146">ID di sessione - istanza hello di interazione dell'utente di hello con app hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-146">Session ID - hello instance of hello user's interaction with hello app.</span></span> <span data-ttu-id="bed07-147">Le informazioni nei campi di contesto di sessione hello sono sempre sull'utente finale di hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-147">Information in hello session context fields is always about hello end user.</span></span> <span data-ttu-id="bed07-148">Quando i dati di telemetria viene inviato da un servizio, il contesto della sessione hello è sull'utente hello che ha avviato l'operazione di hello in servizio hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-148">When telemetry is sent from a service, hello session context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="bed07-149">Lunghezza massima: 64</span><span class="sxs-lookup"><span data-stu-id="bed07-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="bed07-150">ID utente anonimo</span><span class="sxs-lookup"><span data-stu-id="bed07-150">Anonymous user id</span></span>

<span data-ttu-id="bed07-151">L'ID utente anonimo. Rappresenta l'utente finale di hello di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-151">Anonymous user id. Represents hello end user of hello application.</span></span> <span data-ttu-id="bed07-152">Quando i dati di telemetria viene inviato da un servizio, contesto utente hello è sull'utente hello che ha avviato l'operazione di hello in servizio hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-152">When telemetry is sent from a service, hello user context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="bed07-153">[Campionamento](app-insights-sampling.md) è uno della quantità di hello tecniche toominimize hello di telemetria raccolto.</span><span class="sxs-lookup"><span data-stu-id="bed07-153">[Sampling](app-insights-sampling.md) is one of hello techniques toominimize hello amount of collected telemetry.</span></span> <span data-ttu-id="bed07-154">Campionamento algoritmo tentativi tooeither esempio in o out hello tutti correlati telemetria.</span><span class="sxs-lookup"><span data-stu-id="bed07-154">Sampling algorithm attempts tooeither sample in or out all hello correlated telemetry.</span></span> <span data-ttu-id="bed07-155">L'ID utente anonimo viene usato per generare un punteggio di campionamento.</span><span class="sxs-lookup"><span data-stu-id="bed07-155">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="bed07-156">L'ID utente anonimo deve essere quindi un valore sufficientemente casuale.</span><span class="sxs-lookup"><span data-stu-id="bed07-156">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="bed07-157">L'utilizzo di nome utente toostore di id utente anonimo è un utilizzo improprio del campo hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-157">Using anonymous user id toostore user name is a misuse of hello field.</span></span> <span data-ttu-id="bed07-158">Usare un ID utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="bed07-158">Use Authenticated user id.</span></span>

<span data-ttu-id="bed07-159">Lunghezza massima: 128</span><span class="sxs-lookup"><span data-stu-id="bed07-159">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="bed07-160">ID utente autenticato</span><span class="sxs-lookup"><span data-stu-id="bed07-160">Authenticated user id</span></span>

<span data-ttu-id="bed07-161">Id utente autenticato. Hello opposto dell'id utente anonimo, questo campo rappresenta utente hello con un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="bed07-161">Authenticated user id. hello opposite of anonymous user id, this field represents hello user with a friendly name.</span></span> <span data-ttu-id="bed07-162">Le sue informazioni personali non vengono infatti raccolte per impostazione predefinita dalla maggior parte degli SDK.</span><span class="sxs-lookup"><span data-stu-id="bed07-162">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="bed07-163">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="bed07-163">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="bed07-164">ID account</span><span class="sxs-lookup"><span data-stu-id="bed07-164">Account id</span></span>

<span data-ttu-id="bed07-165">Nelle applicazioni multi-tenant, si tratta hello account ID o nome, l'utente che ha hello opera con.</span><span class="sxs-lookup"><span data-stu-id="bed07-165">In multi-tenant applications this is hello account ID or name, which hello user is acting with.</span></span> <span data-ttu-id="bed07-166">Esempi possono essere gli ID sottoscrizione al portale di Azure, il nome del blog o la piattaforma di blogging.</span><span class="sxs-lookup"><span data-stu-id="bed07-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="bed07-167">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="bed07-167">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="bed07-168">Ruolo del cloud</span><span class="sxs-lookup"><span data-stu-id="bed07-168">Cloud role</span></span>

<span data-ttu-id="bed07-169">Nome di un'applicazione hello hello ruolo è una parte.</span><span class="sxs-lookup"><span data-stu-id="bed07-169">Name of hello role hello application is a part of.</span></span> <span data-ttu-id="bed07-170">Esegue il mapping direttamente il nome del ruolo toohello in azure.</span><span class="sxs-lookup"><span data-stu-id="bed07-170">Maps directly toohello role name in azure.</span></span> <span data-ttu-id="bed07-171">Può inoltre essere utilizzati toodistinguish micro servizi, che fanno parte di una singola applicazione.</span><span class="sxs-lookup"><span data-stu-id="bed07-171">Can also be used toodistinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="bed07-172">Lunghezza massima: 256</span><span class="sxs-lookup"><span data-stu-id="bed07-172">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="bed07-173">Istanza del ruolo del cloud</span><span class="sxs-lookup"><span data-stu-id="bed07-173">Cloud role instance</span></span>

<span data-ttu-id="bed07-174">Nome dell'istanza di hello in cui è in esecuzione un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bed07-174">Name of hello instance where hello application is running.</span></span> <span data-ttu-id="bed07-175">Il nome computer in locale, il nome dell'istanza in Azure.</span><span class="sxs-lookup"><span data-stu-id="bed07-175">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="bed07-176">Lunghezza massima: 256</span><span class="sxs-lookup"><span data-stu-id="bed07-176">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="bed07-177">Informazione interna: versione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="bed07-177">Internal: SDK version</span></span>

<span data-ttu-id="bed07-178">La versione dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="bed07-178">SDK version.</span></span> <span data-ttu-id="bed07-179">Per informazioni, vedere https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification.</span><span class="sxs-lookup"><span data-stu-id="bed07-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="bed07-180">Lunghezza massima: 64</span><span class="sxs-lookup"><span data-stu-id="bed07-180">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="bed07-181">Informazione interna: nome del nodo</span><span class="sxs-lookup"><span data-stu-id="bed07-181">Internal: Node name</span></span>

<span data-ttu-id="bed07-182">Questo campo rappresenta il nome di nodo hello utilizzato per la fatturazione.</span><span class="sxs-lookup"><span data-stu-id="bed07-182">This field represents hello node name used for billing purposes.</span></span> <span data-ttu-id="bed07-183">Utilizzare la toooverride hello il rilevamento standard dei nodi.</span><span class="sxs-lookup"><span data-stu-id="bed07-183">Use it toooverride hello standard detection of nodes.</span></span>

<span data-ttu-id="bed07-184">Lunghezza massima: 256</span><span class="sxs-lookup"><span data-stu-id="bed07-184">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="bed07-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bed07-185">Next steps</span></span>

- <span data-ttu-id="bed07-186">Informazioni su come troppo[estendere e filtrare i dati di telemetria](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="bed07-186">Learn how too[extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="bed07-187">Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="bed07-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="bed07-188">Estrarre la [configurazione](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) di una raccolta di proprietà di contesto standard.</span><span class="sxs-lookup"><span data-stu-id="bed07-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
