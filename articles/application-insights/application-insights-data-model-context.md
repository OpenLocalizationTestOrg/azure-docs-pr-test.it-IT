---
title: Modello di dati di Azure Application Insights Telemetry - Contesto dei dati di telemetria | Microsoft Docs
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
ms.openlocfilehash: d6a0cad8bda6ca68aa691867e84f540c5ac9f6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="3eb7a-103">Contesto dei dati di telemetria: modello di dati di Application Insights</span><span class="sxs-lookup"><span data-stu-id="3eb7a-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="3eb7a-104">Ogni elemento di telemetria può contenere campi di contesto fortemente tipizzati.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="3eb7a-105">Ogni campo consente uno specifico scenario di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="3eb7a-106">Usare la raccolta di proprietà personalizzate per archiviare informazioni contestuali personalizzate o specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-106">Use the custom properties collection to store custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="3eb7a-107">Versione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="3eb7a-107">Application version</span></span>

<span data-ttu-id="3eb7a-108">Le informazioni contenute nei campi di contesto dell'applicazione si riferiscono sempre all'applicazione che invia i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-108">Information in the application context fields is always about the application that is sending the telemetry.</span></span> <span data-ttu-id="3eb7a-109">La versione dell'applicazione viene usata per analizzare i cambiamenti nei trend di comportamento dell'applicazione e la correlazione con le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-109">Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.</span></span>

<span data-ttu-id="3eb7a-110">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="3eb7a-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="3eb7a-111">Indirizzo IP client</span><span class="sxs-lookup"><span data-stu-id="3eb7a-111">Client IP address</span></span>

<span data-ttu-id="3eb7a-112">L'indirizzo IP del dispositivo client.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-112">The IP address of the client device.</span></span> <span data-ttu-id="3eb7a-113">Sono supportati sia IPv4 che IPv6.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="3eb7a-114">Quando i dati di telemetria vengono inviati da un servizio, il contesto della posizione si riferisce all'utente che ha avviato l'operazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-114">When telemetry is sent from a service, the location context is about the user that initiated the operation in the service.</span></span> <span data-ttu-id="3eb7a-115">Application Insights estrae i dati di geolocalizzazione dall'IP client, per poi troncarli.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-115">Application Insights extract the geo-location information from the client IP and then truncate it.</span></span> <span data-ttu-id="3eb7a-116">L'IP client da solo non può quindi essere usato come informazione personale dell'utente finale.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="3eb7a-117">Lunghezza massima: 46</span><span class="sxs-lookup"><span data-stu-id="3eb7a-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="3eb7a-118">Tipo di dispositivo</span><span class="sxs-lookup"><span data-stu-id="3eb7a-118">Device type</span></span>

<span data-ttu-id="3eb7a-119">In origine questo campo serviva a indicare il tipo di dispositivo usato dall'utente finale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-119">Originally this field was used to indicate the type of the device the end user of the application is using.</span></span> <span data-ttu-id="3eb7a-120">Oggi viene usato principalmente per distinguere i dati di telemetria JavaScript con tipo di dispositivo "Browser" dai dati di telemetria lato server con tipo di dispositivo "PC".</span><span class="sxs-lookup"><span data-stu-id="3eb7a-120">Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.</span></span>

<span data-ttu-id="3eb7a-121">Lunghezza massima: 64</span><span class="sxs-lookup"><span data-stu-id="3eb7a-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="3eb7a-122">ID operazione</span><span class="sxs-lookup"><span data-stu-id="3eb7a-122">Operation id</span></span>

<span data-ttu-id="3eb7a-123">Un identificatore univoco dell'operazione di root.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-123">A unique identifier of the root operation.</span></span> <span data-ttu-id="3eb7a-124">Questo identificatore univoco consente di raggruppare i dati di telemetria tra componenti multipli.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-124">This identifier allows to group telemetry across multiple components.</span></span> <span data-ttu-id="3eb7a-125">Per informazioni dettagliate, vedere [Correlazione di dati di telemetria](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="3eb7a-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="3eb7a-126">L'ID operazione viene creato da una richiesta o da una visualizzazione pagina.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-126">The operation id is created by either a request or a page view.</span></span> <span data-ttu-id="3eb7a-127">Tutti gli altri dati di telemetria impostano questo campo sul valore per la richiesta o la visualizzazione pagina che lo contiene.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-127">All other telemetry sets this field to the value for the containing request or page view.</span></span> 

<span data-ttu-id="3eb7a-128">Lunghezza massima: 128</span><span class="sxs-lookup"><span data-stu-id="3eb7a-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="3eb7a-129">ID operazione padre</span><span class="sxs-lookup"><span data-stu-id="3eb7a-129">Parent operation ID</span></span>

<span data-ttu-id="3eb7a-130">L'identificatore univoco dell'elemento padre diretto dell'elemento di telemetria.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-130">The unique identifier of the telemetry item's immediate parent.</span></span> <span data-ttu-id="3eb7a-131">Per informazioni dettagliate, vedere [Correlazione di dati di telemetria](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="3eb7a-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="3eb7a-132">Lunghezza massima: 128</span><span class="sxs-lookup"><span data-stu-id="3eb7a-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="3eb7a-133">Nome operazione</span><span class="sxs-lookup"><span data-stu-id="3eb7a-133">Operation name</span></span>

<span data-ttu-id="3eb7a-134">Il nome (gruppo) dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-134">The name (group) of the operation.</span></span> <span data-ttu-id="3eb7a-135">Il nome dell'operazione viene creato da una richiesta o da una visualizzazione pagina.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-135">The operation name is created by either a request or a page view.</span></span> <span data-ttu-id="3eb7a-136">Tutti gli altri elementi di telemetria impostano questo campo sul valore della richiesta o dalla visualizzazione pagina che lo contiene.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-136">All other telemetry items set this field to the value for the containing request or page view.</span></span> <span data-ttu-id="3eb7a-137">Il nome dell'operazione è usato per individuare tutti gli elementi di telemetria per un gruppo di operazioni (ad esempio "GET Home/Index").</span><span class="sxs-lookup"><span data-stu-id="3eb7a-137">Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="3eb7a-138">Questa proprietà di contesto viene usata per rispondere a domande come "Quali sono le eccezioni tipiche generate in questa pagina?".</span><span class="sxs-lookup"><span data-stu-id="3eb7a-138">This context property is used to answer questions like "what are the typical exceptions thrown on this page."</span></span>

<span data-ttu-id="3eb7a-139">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="3eb7a-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-the-operation"></a><span data-ttu-id="3eb7a-140">Origine sintetica dell'operazione</span><span class="sxs-lookup"><span data-stu-id="3eb7a-140">Synthetic source of the operation</span></span>

<span data-ttu-id="3eb7a-141">Il nome dell'origine sintetica.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-141">Name of synthetic source.</span></span> <span data-ttu-id="3eb7a-142">Alcuni dati di telemetria generati dall'applicazione possono rappresentare traffico sintetico.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-142">Some telemetry from the application may represent synthetic traffic.</span></span> <span data-ttu-id="3eb7a-143">Potrebbe trattarsi di agenti di ricerca Web che indicizzano il sito Web, test di disponibilità del sito o tracce di librerie di diagnostica come Application Insights SDK stesso.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-143">It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="3eb7a-144">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="3eb7a-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="3eb7a-145">ID sessione</span><span class="sxs-lookup"><span data-stu-id="3eb7a-145">Session id</span></span>

<span data-ttu-id="3eb7a-146">L'ID sessione, cioè l'istanza di interazione dell'utente con l'app.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-146">Session ID - the instance of the user's interaction with the app.</span></span> <span data-ttu-id="3eb7a-147">Le informazioni contenute nei campi di contesto della sessione si riferiscono sempre all'utente finale.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-147">Information in the session context fields is always about the end user.</span></span> <span data-ttu-id="3eb7a-148">Quando i dati di telemetria vengono inviati da un servizio, il contesto di sessione si riferisce all'utente che ha avviato l'operazione nel servizio.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-148">When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="3eb7a-149">Lunghezza massima: 64</span><span class="sxs-lookup"><span data-stu-id="3eb7a-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="3eb7a-150">ID utente anonimo</span><span class="sxs-lookup"><span data-stu-id="3eb7a-150">Anonymous user id</span></span>

<span data-ttu-id="3eb7a-151">L'ID utente anonimo.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-151">Anonymous user id.</span></span> <span data-ttu-id="3eb7a-152">Rappresenta l'utente finale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-152">Represents the end user of the application.</span></span> <span data-ttu-id="3eb7a-153">Quando i dati di telemetria vengono inviati da un servizio, il contesto utente si riferisce all'utente che ha avviato l'operazione nel servizio.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-153">When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="3eb7a-154">Il [campionamento](app-insights-sampling.md) è una delle tecniche usate per ridurre al minimo la quantità di dati di telemetria raccolti.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-154">[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry.</span></span> <span data-ttu-id="3eb7a-155">L'algoritmo di campionamento tenta di sondare tutti i dati di telemetria correlati in ingresso o in uscita.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-155">Sampling algorithm attempts to either sample in or out all the correlated telemetry.</span></span> <span data-ttu-id="3eb7a-156">L'ID utente anonimo viene usato per generare un punteggio di campionamento.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-156">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="3eb7a-157">L'ID utente anonimo deve essere quindi un valore sufficientemente casuale.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-157">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="3eb7a-158">L'uso di un ID utente anonimo per archiviare il nome utente rappresenta un uso improprio del campo.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-158">Using anonymous user id to store user name is a misuse of the field.</span></span> <span data-ttu-id="3eb7a-159">Usare un ID utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-159">Use Authenticated user id.</span></span>

<span data-ttu-id="3eb7a-160">Lunghezza massima: 128</span><span class="sxs-lookup"><span data-stu-id="3eb7a-160">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="3eb7a-161">ID utente autenticato</span><span class="sxs-lookup"><span data-stu-id="3eb7a-161">Authenticated user id</span></span>

<span data-ttu-id="3eb7a-162">L'ID utente autenticato.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-162">Authenticated user id.</span></span> <span data-ttu-id="3eb7a-163">Al contrario dell'ID utente anonimo, questo campo rappresenta l'utente con un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-163">The opposite of anonymous user id, this field represents the user with a friendly name.</span></span> <span data-ttu-id="3eb7a-164">Le sue informazioni personali non vengono infatti raccolte per impostazione predefinita dalla maggior parte degli SDK.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-164">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="3eb7a-165">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="3eb7a-165">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="3eb7a-166">ID account</span><span class="sxs-lookup"><span data-stu-id="3eb7a-166">Account id</span></span>

<span data-ttu-id="3eb7a-167">In applicazioni multi-tenant, rappresenta l'ID o il nome dell'account con cui l'utente opera.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-167">In multi-tenant applications this is the account ID or name, which the user is acting with.</span></span> <span data-ttu-id="3eb7a-168">Esempi possono essere gli ID sottoscrizione al portale di Azure, il nome del blog o la piattaforma di blogging.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-168">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="3eb7a-169">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="3eb7a-169">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="3eb7a-170">Ruolo del cloud</span><span class="sxs-lookup"><span data-stu-id="3eb7a-170">Cloud role</span></span>

<span data-ttu-id="3eb7a-171">Il nome del ruolo di cui l'applicazione fa parte.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-171">Name of the role the application is a part of.</span></span> <span data-ttu-id="3eb7a-172">Esegue direttamente il mapping al nome del ruolo in Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-172">Maps directly to the role name in azure.</span></span> <span data-ttu-id="3eb7a-173">Consente anche di distinguere i micro servizi che fanno parte di una singola applicazione.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-173">Can also be used to distinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="3eb7a-174">Lunghezza massima: 256</span><span class="sxs-lookup"><span data-stu-id="3eb7a-174">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="3eb7a-175">Istanza del ruolo del cloud</span><span class="sxs-lookup"><span data-stu-id="3eb7a-175">Cloud role instance</span></span>

<span data-ttu-id="3eb7a-176">Il nome dell'istanza in cui l'applicazione è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-176">Name of the instance where the application is running.</span></span> <span data-ttu-id="3eb7a-177">Il nome computer in locale, il nome dell'istanza in Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-177">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="3eb7a-178">Lunghezza massima: 256</span><span class="sxs-lookup"><span data-stu-id="3eb7a-178">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="3eb7a-179">Informazione interna: versione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="3eb7a-179">Internal: SDK version</span></span>

<span data-ttu-id="3eb7a-180">La versione dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-180">SDK version.</span></span> <span data-ttu-id="3eb7a-181">Per informazioni, vedere https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-181">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="3eb7a-182">Lunghezza massima: 64</span><span class="sxs-lookup"><span data-stu-id="3eb7a-182">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="3eb7a-183">Informazione interna: nome del nodo</span><span class="sxs-lookup"><span data-stu-id="3eb7a-183">Internal: Node name</span></span>

<span data-ttu-id="3eb7a-184">Questo campo rappresenta il nome del nodo usato a scopi di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-184">This field represents the node name used for billing purposes.</span></span> <span data-ttu-id="3eb7a-185">È possibile usarlo per eseguire l'override del rilevamento standard dei nodi.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-185">Use it to override the standard detection of nodes.</span></span>

<span data-ttu-id="3eb7a-186">Lunghezza massima: 256</span><span class="sxs-lookup"><span data-stu-id="3eb7a-186">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="3eb7a-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3eb7a-187">Next steps</span></span>

- <span data-ttu-id="3eb7a-188">Informazioni su come [estendere e filtrare i dati di telemetria](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="3eb7a-188">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="3eb7a-189">Per informazioni sul modello di dati e sui tipi di Application Insights, vedere il [modello di dati](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="3eb7a-189">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="3eb7a-190">Estrarre la [configurazione](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) di una raccolta di proprietà di contesto standard.</span><span class="sxs-lookup"><span data-stu-id="3eb7a-190">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
