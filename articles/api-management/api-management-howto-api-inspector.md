---
title: Tenere traccia delle chiamate con Controllo API in Gestione API di Azure | Documentazione Microsoft
description: Informazioni su come tenere traccia delle chiamate usando Controllo API in Gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 4b222327-c8a4-4f33-9a06-adff2a9834d9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a9d4d3be7f046af975f6dc25670070204848588c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-api-inspector-to-trace-calls-in-azure-api-management"></a><span data-ttu-id="857d4-103">Come usare Controllo API per tenere traccia delle chiamate in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="857d4-103">How to use the API Inspector to trace calls in Azure API Management</span></span>
<span data-ttu-id="857d4-104">Gestione API fornisce uno strumento per il controllo delle API per aiutare gli sviluppatori ad eseguire il debug e la risoluzione dei problemi correlati alle API.</span><span class="sxs-lookup"><span data-stu-id="857d4-104">API Management provides an API Inspector tool to help you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="857d4-105">È possibile usare Controllo API sia a livello di codice sia direttamente dal portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="857d4-105">The API Inspector can be used programmatically and can also be used directly from the developer portal.</span></span> 

<span data-ttu-id="857d4-106">Oltre alle operazioni di analisi, Controllo API consente anche di tenere traccia delle valutazioni delle [espressioni di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx) .</span><span class="sxs-lookup"><span data-stu-id="857d4-106">In addition to tracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="857d4-107">Per una dimostrazione, vedere il video [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e avanzare rapidamente al minuto 21:00.</span><span class="sxs-lookup"><span data-stu-id="857d4-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 21:00.</span></span>

<span data-ttu-id="857d4-108">Questa guida contiene una procedura dettagliata sull'uso di Controllo API.</span><span class="sxs-lookup"><span data-stu-id="857d4-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="857d4-109">Le tracce di Controllo API sono generate e rese disponibili solo per le richieste contenenti chiavi di sottoscrizione che appartengono all'account [amministratore](api-management-howto-create-groups.md) .</span><span class="sxs-lookup"><span data-stu-id="857d4-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong to the [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="857d4-110"><a name="trace-call"> </a> Usare Controllo API per tenere traccia di una chiamata</span><span class="sxs-lookup"><span data-stu-id="857d4-110"><a name="trace-call"> </a> Use API Inspector to trace a call</span></span>
<span data-ttu-id="857d4-111">Per usare Controllo API, aggiungere un'intestazione di richiesta **ocp-apim-trace: true** alla chiamata di operazioni, quindi scaricare ed esaminare la traccia usando l'URL indicato dall'intestazione di risposta **ocp-apim-trace-location**.</span><span class="sxs-lookup"><span data-stu-id="857d4-111">To use API Inspector, add an **ocp-apim-trace: true** request header to your operation call, and then download and inspect the trace using the URL indicated by the **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="857d4-112">Questa operazione può essere eseguita sia a livello di codice che direttamente dal portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="857d4-112">This can be done programatically, and can also be done directly from the developer portal.</span></span>

<span data-ttu-id="857d4-113">Questa esercitazione illustra come usare Controllo API per tenere traccia delle operazioni tramite l'API Basic Calculator configurata nell'esercitazione introduttiva [Gestire la prima API](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="857d4-113">This tutorial shows how to use the API Inspector to trace operations using the Basic Calculator API that is configured in the [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="857d4-114">Se tale esercitazione non è stata completata, sono sufficienti pochi minuti per importare l'API Basic Calculator oppure è possibile usare un'altra API a scelta, ad esempio l'API Echo.</span><span class="sxs-lookup"><span data-stu-id="857d4-114">If you haven't completed that tutorial it only takes a few moments to import the Basic Calculator API, or you can use another API of your choosing such as the Echo API.</span></span> <span data-ttu-id="857d4-115">Ogni istanza del servizio Gestione API è preconfigurata con un'API Echo utilizzabile per sperimentare e ottenere altre informazioni su Gestione API.</span><span class="sxs-lookup"><span data-stu-id="857d4-115">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="857d4-116">L'API Echo restituisce qualunque input gli venga inviato.</span><span class="sxs-lookup"><span data-stu-id="857d4-116">The Echo API returns back whatever input is sent to it.</span></span> <span data-ttu-id="857d4-117">Per usarla, è possibile richiamare un qualsiasi verbo HTTP. Il valore restituito sarà semplicemente ciò che si è inviato.</span><span class="sxs-lookup"><span data-stu-id="857d4-117">To use it, you can invoke any HTTP verb, and the return value will simply be what you sent.</span></span> 

<span data-ttu-id="857d4-118">Per iniziare, fare clic su **Portale per sviluppatori** nel portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="857d4-118">To get started, click **Developer portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="857d4-119">È possibile chiamare le operazioni direttamente dal portale per sviluppatori, che consente di visualizzare e testare le operazioni di un'API in tutta comodità.</span><span class="sxs-lookup"><span data-stu-id="857d4-119">Operations can be called directly from the developer portal which provides a convenient way to view and test the operations of an API.</span></span>

> <span data-ttu-id="857d4-120">Se non è stata ancora creata un'istanza del servizio Gestione API, vedere [Creare un'istanza del servizio Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="857d4-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![Portale per sviluppatori di Gestione API][api-management-developer-portal-menu]

<span data-ttu-id="857d4-122">Fare clic su **API** nel menu superiore, quindi su **Basic Calculator** (Calcolatrice di base).</span><span class="sxs-lookup"><span data-stu-id="857d4-122">Click **APIs** from the top menu, and then click **Basic Calculator**.</span></span>

![API Echo][api-management-api]

<span data-ttu-id="857d4-124">Fare clic su **Prova** per provare a eseguire l'operazione **Aggiungere due Integer**.</span><span class="sxs-lookup"><span data-stu-id="857d4-124">Click **Try it** to try the **Add two integers** operation.</span></span>

![Prova][api-management-open-console]

<span data-ttu-id="857d4-126">Mantenere i valori predefiniti dei parametri e selezionare la chiave di sottoscrizione per il prodotto da usare nell'elenco a discesa **subscription-key** .</span><span class="sxs-lookup"><span data-stu-id="857d4-126">Keep the default parameter values, and select the subscription key for the product you want to use from the **subscription-key** drop-down.</span></span>

<span data-ttu-id="857d4-127">Per impostazione predefinita, nel portale per sviluppatori l'intestazione **Ocp-Apim-Trace** è già impostata su **true**.</span><span class="sxs-lookup"><span data-stu-id="857d4-127">By default in the developer portal the **Ocp-Apim-Trace** header is already set to **true**.</span></span> <span data-ttu-id="857d4-128">Questa intestazione indica se viene o meno generata una traccia.</span><span class="sxs-lookup"><span data-stu-id="857d4-128">This header configures whether or not a trace is generated.</span></span>

![Send][api-management-http-get]

<span data-ttu-id="857d4-130">Fare clic su **Send** per richiamare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="857d4-130">Click **Send** to invoke the operation.</span></span>

![Send][api-management-send-results]

<span data-ttu-id="857d4-132">Le intestazioni di risposta conterranno un elemento **ocp-apim-trace-location** con un valore simile a quello dell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="857d4-132">In the response headers will be an **ocp-apim-trace-location** with a value similar to the following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="857d4-133">È possibile scaricare la traccia dal percorso specificato e quindi analizzarla, come illustrato nel passaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="857d4-133">The trace can be downloaded from the specified location and reviewed as demonstrated in the next step.</span></span> <span data-ttu-id="857d4-134">Si noti che vengono archiviate solo le ultime 100 voci di log e i percorsi del log vengono riutilizzati a rotazione.</span><span class="sxs-lookup"><span data-stu-id="857d4-134">Note that only the last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="857d4-135">Pertanto se si eseguono più di 100 chiamate con la traccia attivata, si finirà per sovrascrivere le prime tracce.</span><span class="sxs-lookup"><span data-stu-id="857d4-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting the first traces in place.</span></span>

## <span data-ttu-id="857d4-136"><a name="inspect-trace"> </a>Esaminare la traccia</span><span class="sxs-lookup"><span data-stu-id="857d4-136"><a name="inspect-trace"> </a>Inspect the trace</span></span>
<span data-ttu-id="857d4-137">Per rivedere i valori nella traccia, scaricare il file di traccia dell'URL **ocp-apim-trace-location** .</span><span class="sxs-lookup"><span data-stu-id="857d4-137">To review the values in the trace, download the trace file from the **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="857d4-138">Si tratta di un file di testo in formato JSON, contenente voci simili a quelle illustrate nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="857d4-138">It is a text file in JSON format, and contains entries similar to the following example.</span></span>

```json
{
    "traceId": "abcd8ea63d134c1fabe6371566c7cbea",
    "traceEntries": {
        "inbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0725926",
                "data": {
                    "request": {
                        "method": "GET",
                        "url": "https://contoso5.azure-api.net/calc/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "Connection",
                                "value": "Keep-Alive"
                            },
                            {
                                "name": "Host",
                                "value": "contoso5.azure-api.net"
                            }
                        ]
                    }
                }
            },
            {
                "source": "mapper",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0726213",
                "data": {
                    "configuration": {
                        "api": {
                            "from": "/calc",
                            "to": {
                                "scheme": "http",
                                "host": "calcapi.cloudapp.net",
                                "port": 80,
                                "path": "/api",
                                "queryString": "",
                                "query": {},
                                "isDefaultPort": true
                            }
                        },
                        "operation": {
                            "method": "GET",
                            "uriTemplate": "/add?a={a}&b={b}"
                        },
                        "user": {
                            "id": 1,
                            "groups": [
                                "Administrators",
                                "Developers"
                            ]
                        },
                        "product": {
                            "id": 1
                        }
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0727522",
                "data": {
                    "message": "Request is being forwarded to the backend service.",
                    "request": {
                        "method": "GET",
                        "url": "http://calcapi.cloudapp.net/api/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "X-Forwarded-For",
                                "value": "33.52.215.35"
                            }
                        ]
                    }
                }
            }
        ],
        "outbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1960601",
                "data": {
                    "response": {
                        "status": {
                            "code": 200,
                            "reason": "OK"
                        },
                        "headers": [
                            {
                                "name": "Pragma",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Length",
                                "value": "124"
                            },
                            {
                                "name": "Cache-Control",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Type",
                                "value": "application/xml; charset=utf-8"
                            },
                            {
                                "name": "Date",
                                "value": "Tue, 23 Jun 2015 19:51:35 GMT"
                            },
                            {
                                "name": "Expires",
                                "value": "-1"
                            },
                            {
                                "name": "Server",
                                "value": "Microsoft-IIS/8.5"
                            },
                            {
                                "name": "X-AspNet-Version",
                                "value": "4.0.30319"
                            },
                            {
                                "name": "X-Powered-By",
                                "value": "ASP.NET"
                            }
                        ]
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1961112",
                "data": {
                    "message": "Response headers have been sent to the caller. Starting to stream the response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming to the caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="857d4-139"><a name="next-steps"> </a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="857d4-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="857d4-140">Per una demo sulla traccia delle espressioni di criteri, vedere il video [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="857d4-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="857d4-141">Avanzare rapidamente al minuto 21:00 per vedere la demo.</span><span class="sxs-lookup"><span data-stu-id="857d4-141">Fast-forward to 21:00 to see the demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector to trace a call]: #trace-call
[Inspect the trace]: #inspect-trace
[Next steps]: #next-steps

[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Azure Classic Portal]: https://manage.windowsazure.com/


[api-management-developer-portal-menu]: ./media/api-management-howto-api-inspector/api-management-developer-portal-menu.png
[api-management-api]: ./media/api-management-howto-api-inspector/api-management-api.png
[api-management-echo-api-get]: ./media/api-management-howto-api-inspector/api-management-echo-api-get.png
[api-management-developer-key]: ./media/api-management-howto-api-inspector/api-management-developer-key.png
[api-management-open-console]: ./media/api-management-howto-api-inspector/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-api-inspector/api-management-http-get.png
[api-management-send-results]: ./media/api-management-howto-api-inspector/api-management-send-results.png




