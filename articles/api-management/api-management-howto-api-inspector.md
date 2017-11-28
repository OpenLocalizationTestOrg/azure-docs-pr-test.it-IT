---
title: chiamate aaaTrace con API di controllo - Gestione API di Azure | Documenti Microsoft
description: Informazioni su come chiamate tootrace mediante hello controllo API in Gestione API di Azure.
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
ms.openlocfilehash: b0c401caa8da1b789f6cfe5edf97a5f118d78f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a><span data-ttu-id="cb8e3-103">Modalità toouse hello tootrace API controllo chiama in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="cb8e3-103">How toouse hello API Inspector tootrace calls in Azure API Management</span></span>
<span data-ttu-id="cb8e3-104">Gestione API fornisce un controllo API toohelp strumento il debug e le API di risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-104">API Management provides an API Inspector tool toohelp you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="cb8e3-105">Hello API controllo può essere utilizzato a livello di codice e può anche essere utilizzato direttamente dal portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-105">hello API Inspector can be used programmatically and can also be used directly from hello developer portal.</span></span> 

<span data-ttu-id="cb8e3-106">Inoltre operations tootracing, API di controllo anche tracce [espressione di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx) valutazioni.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-106">In addition tootracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="cb8e3-107">Per una dimostrazione, vedere [Cloud coprire episodio 177: più le funzionalità di gestione API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too21:00.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too21:00.</span></span>

<span data-ttu-id="cb8e3-108">Questa guida contiene una procedura dettagliata sull'uso di Controllo API.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="cb8e3-109">API controllo tracce solo generate e resi disponibili per le richieste contenenti le chiavi di sottoscrizione che appartengono toohello [amministratore](api-management-howto-create-groups.md) account.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong toohello [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="cb8e3-110"><a name="trace-call"></a> Tootrace utilizzare API controllo una chiamata</span><span class="sxs-lookup"><span data-stu-id="cb8e3-110"><a name="trace-call"> </a> Use API Inspector tootrace a call</span></span>
<span data-ttu-id="cb8e3-111">toouse API di controllo, aggiungere un **ocp-ruoli-trace: true** intestazione tooyour operazione chiamata, per una richiesta, quindi scaricare e controllare traccia hello utilizzando URL hello indicato da hello **ocp-ruoli traccia location** intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-111">toouse API Inspector, add an **ocp-apim-trace: true** request header tooyour operation call, and then download and inspect hello trace using hello URL indicated by hello **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="cb8e3-112">Questo può essere eseguito a livello di codice e può anche essere eseguito direttamente dal portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-112">This can be done programatically, and can also be done directly from hello developer portal.</span></span>

<span data-ttu-id="cb8e3-113">Questa esercitazione viene illustrato come le operazioni tootrace controllo hello API toouse utilizzando hello API Calculator base configurato in hello [gestione API prima](api-management-get-started.md) esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-113">This tutorial shows how toouse hello API Inspector tootrace operations using hello Basic Calculator API that is configured in hello [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="cb8e3-114">Se non ancora completate tale esercitazione bastano pochi istanti tooimport hello API Calculator base oppure è possibile utilizzare un'altra API di propria scelta, ad esempio hello Echo API.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-114">If you haven't completed that tutorial it only takes a few moments tooimport hello Basic Calculator API, or you can use another API of your choosing such as hello Echo API.</span></span> <span data-ttu-id="cb8e3-115">Ogni istanza del servizio Gestione API preconfigurata con un'API Echo che possono essere tooexperiment utilizzati con e acquisire informazioni su gestione API.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-115">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="cb8e3-116">Hello Echo API restituisce nuovamente tooit viene inviato da qualsiasi input.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-116">hello Echo API returns back whatever input is sent tooit.</span></span> <span data-ttu-id="cb8e3-117">toouse, è possibile richiamare qualsiasi verbo HTTP e valore restituito di hello semplicemente è ciò che è stata inviata.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-117">toouse it, you can invoke any HTTP verb, and hello return value will simply be what you sent.</span></span> 

<span data-ttu-id="cb8e3-118">tooget avviato, fare clic su **portale per sviluppatori** in hello portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-118">tooget started, click **Developer portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="cb8e3-119">Operazioni possono essere chiamate direttamente dal portale per sviluppatori hello che fornisce un modo pratico di tooview e testare il funzionamento di hello di un'API.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-119">Operations can be called directly from hello developer portal which provides a convenient way tooview and test hello operations of an API.</span></span>

> <span data-ttu-id="cb8e3-120">Se è ancora stata creata un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![Portale per sviluppatori di Gestione API][api-management-developer-portal-menu]

<span data-ttu-id="cb8e3-122">Fare clic su **API** dal menu superiore hello e quindi fare clic su **Calcolatrice di base**.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-122">Click **APIs** from hello top menu, and then click **Basic Calculator**.</span></span>

![API Echo][api-management-api]

<span data-ttu-id="cb8e3-124">Fare clic su **provarla** tootry hello **aggiungere due numeri interi** operazione.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-124">Click **Try it** tootry hello **Add two integers** operation.</span></span>

![Prova][api-management-open-console]

<span data-ttu-id="cb8e3-126">Mantenere i valori di parametro predefiniti hello e chiave di sottoscrizione selezionare hello per prodotto hello desiderato toouse da hello **chiave di sottoscrizione** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-126">Keep hello default parameter values, and select hello subscription key for hello product you want toouse from hello **subscription-key** drop-down.</span></span>

<span data-ttu-id="cb8e3-127">Per impostazione predefinita in hello portale per sviluppatori di hello **Ocp-ruoli-traccia** intestazione è già impostata troppo**true**.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-127">By default in hello developer portal hello **Ocp-Apim-Trace** header is already set too**true**.</span></span> <span data-ttu-id="cb8e3-128">Questa intestazione indica se viene o meno generata una traccia.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-128">This header configures whether or not a trace is generated.</span></span>

![Invio][api-management-http-get]

<span data-ttu-id="cb8e3-130">Fare clic su **inviare** operazione hello tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-130">Click **Send** tooinvoke hello operation.</span></span>

![Invio][api-management-send-results]

<span data-ttu-id="cb8e3-132">In risposta hello intestazioni sarà un **ocp-ruoli traccia location** con un toohello simile valore esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-132">In hello response headers will be an **ocp-apim-trace-location** with a value similar toohello following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="cb8e3-133">traccia Hello può essere scaricato dal percorso specificato ed esaminato come illustrato nel passaggio successivo hello di hello.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-133">hello trace can be downloaded from hello specified location and reviewed as demonstrated in hello next step.</span></span> <span data-ttu-id="cb8e3-134">Si noti che solo hello ultimo 100 voci di log vengono archiviate e percorsi dei log vengono riutilizzati nella rotazione.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-134">Note that only hello last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="cb8e3-135">Pertanto, se si effettuano chiamate più di 100 con traccia attivata infine avviare sovrascrivendo le tracce prima hello sul posto.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting hello first traces in place.</span></span>

## <span data-ttu-id="cb8e3-136"><a name="inspect-trace"></a>Controllare traccia hello</span><span class="sxs-lookup"><span data-stu-id="cb8e3-136"><a name="inspect-trace"> </a>Inspect hello trace</span></span>
<span data-ttu-id="cb8e3-137">i valori hello tooreview in traccia hello, scaricare il file di traccia hello da hello **ocp-ruoli traccia location** URL.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-137">tooreview hello values in hello trace, download hello trace file from hello **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="cb8e3-138">È un file di testo in formato JSON e contiene le voci toohello simile esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-138">It is a text file in JSON format, and contains entries similar toohello following example.</span></span>

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
                    "message": "Request is being forwarded toohello backend service.",
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
                    "message": "Response headers have been sent toohello caller. Starting toostream hello response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming toohello caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="cb8e3-139"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cb8e3-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="cb8e3-140">Per una demo sulla traccia delle espressioni di criteri, vedere il video [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="cb8e3-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="cb8e3-141">Demo di hello toosee too21:00 fast forward-only.</span><span class="sxs-lookup"><span data-stu-id="cb8e3-141">Fast-forward too21:00 toosee hello demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector tootrace a call]: #trace-call
[Inspect hello trace]: #inspect-trace
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




