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
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a>Modalità toouse hello tootrace API controllo chiama in Gestione API di Azure
Gestione API fornisce un controllo API toohelp strumento il debug e le API di risoluzione dei problemi. Hello API controllo può essere utilizzato a livello di codice e può anche essere utilizzato direttamente dal portale per sviluppatori hello. 

Inoltre operations tootracing, API di controllo anche tracce [espressione di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx) valutazioni. Per una dimostrazione, vedere [Cloud coprire episodio 177: più le funzionalità di gestione API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too21:00.

Questa guida contiene una procedura dettagliata sull'uso di Controllo API.

> [!NOTE]
> API controllo tracce solo generate e resi disponibili per le richieste contenenti le chiavi di sottoscrizione che appartengono toohello [amministratore](api-management-howto-create-groups.md) account.
> 
> 

## <a name="trace-call"></a> Tootrace utilizzare API controllo una chiamata
toouse API di controllo, aggiungere un **ocp-ruoli-trace: true** intestazione tooyour operazione chiamata, per una richiesta, quindi scaricare e controllare traccia hello utilizzando URL hello indicato da hello **ocp-ruoli traccia location** intestazione della risposta. Questo può essere eseguito a livello di codice e può anche essere eseguito direttamente dal portale per sviluppatori hello.

Questa esercitazione viene illustrato come le operazioni tootrace controllo hello API toouse utilizzando hello API Calculator base configurato in hello [gestione API prima](api-management-get-started.md) esercitazione introduttiva. Se non ancora completate tale esercitazione bastano pochi istanti tooimport hello API Calculator base oppure è possibile utilizzare un'altra API di propria scelta, ad esempio hello Echo API. Ogni istanza del servizio Gestione API preconfigurata con un'API Echo che possono essere tooexperiment utilizzati con e acquisire informazioni su gestione API. Hello Echo API restituisce nuovamente tooit viene inviato da qualsiasi input. toouse, è possibile richiamare qualsiasi verbo HTTP e valore restituito di hello semplicemente è ciò che è stata inviata. 

tooget avviato, fare clic su **portale per sviluppatori** in hello portale di Azure per il servizio Gestione API. Operazioni possono essere chiamate direttamente dal portale per sviluppatori hello che fornisce un modo pratico di tooview e testare il funzionamento di hello di un'API.

> Se è ancora stata creata un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.
> 
> 

![Portale per sviluppatori di Gestione API][api-management-developer-portal-menu]

Fare clic su **API** dal menu superiore hello e quindi fare clic su **Calcolatrice di base**.

![API Echo][api-management-api]

Fare clic su **provarla** tootry hello **aggiungere due numeri interi** operazione.

![Prova][api-management-open-console]

Mantenere i valori di parametro predefiniti hello e chiave di sottoscrizione selezionare hello per prodotto hello desiderato toouse da hello **chiave di sottoscrizione** elenco a discesa.

Per impostazione predefinita in hello portale per sviluppatori di hello **Ocp-ruoli-traccia** intestazione è già impostata troppo**true**. Questa intestazione indica se viene o meno generata una traccia.

![Invio][api-management-http-get]

Fare clic su **inviare** operazione hello tooinvoke.

![Invio][api-management-send-results]

In risposta hello intestazioni sarà un **ocp-ruoli traccia location** con un toohello simile valore esempio seguente.

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

traccia Hello può essere scaricato dal percorso specificato ed esaminato come illustrato nel passaggio successivo hello di hello. Si noti che solo hello ultimo 100 voci di log vengono archiviate e percorsi dei log vengono riutilizzati nella rotazione. Pertanto, se si effettuano chiamate più di 100 con traccia attivata infine avviare sovrascrivendo le tracce prima hello sul posto.

## <a name="inspect-trace"></a>Controllare traccia hello
i valori hello tooreview in traccia hello, scaricare il file di traccia hello da hello **ocp-ruoli traccia location** URL. È un file di testo in formato JSON e contiene le voci toohello simile esempio seguente.

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

## <a name="next-steps"></a>Passaggi successivi
* Per una demo sulla traccia delle espressioni di criteri, vedere il video [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/). Demo di hello toosee too21:00 fast forward-only.

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




