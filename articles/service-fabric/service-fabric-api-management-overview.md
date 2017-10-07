---
title: aaaAzure Service Fabric con panoramica di gestione API | Documenti Microsoft
description: "Questo articolo è un toousing introduzione gestione API di Azure come applicazioni di Service Fabric tooyour gateway."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: vturecek
ms.openlocfilehash: f01dc570a11e68cd4a2d878abbe6019e209e2f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a>Panoramica di Service Fabric con Gestione API di Azure

Le applicazioni cloud in genere necessitano tooprovide un gateway front-end un singolo punto di ingresso per gli utenti, dispositivi o altre applicazioni. In Service Fabric un gateway può essere qualsiasi servizio senza stato, ad esempio un'[applicazione ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), o un altro servizio progettati per l'ingresso del traffico, ad esempio [Hub eventi](https://docs.microsoft.com/azure/event-hubs/), [Hub IoT](https://docs.microsoft.com/azure/iot-hub/) o [Gestione API di Azure](https://docs.microsoft.com/azure/api-management/).

Questo articolo è un toousing introduzione gestione API di Azure come applicazioni di Service Fabric tooyour gateway. API di gestione si integra direttamente con Service Fabric, consentendo toopublish API con una vasta gamma di servizi di routing regole tooyour back-end dell'infrastruttura di servizio. 

## <a name="architecture"></a>Architettura
Un'architettura di Service Fabric comune utilizza un'applicazione di una pagina web che effettua chiamate HTTP servizi tooback-end che espongono APIs HTTP. Hello [applicazione di esempio della Guida introduttiva di Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) Mostra un esempio di questa architettura.

In questo scenario, un servizio web senza stato funge da gateway hello in hello applicazione di Service Fabric. Questo approccio richiede si toowrite un servizio web che può essere proxy HTTP richiede servizi tooback-end, come illustrato nel seguente diagramma hello:

![Panoramica di Service Fabric con topologia di Gestione API di Azure][sf-web-app-stateless-gateway]

Le applicazioni con l'aumentare della complessità, in modo hello gateway che deve presentare un'API davanti innumerevoli servizi back-end. Gestione API di Azure è progettato toohandle API complesse con regole di routing, controllo dell'accesso, la limitazione della velocità, monitoraggio, la registrazione degli eventi e la memorizzazione nella cache di risposta con il minimo da parte dell'utente. Gestione API di Azure supporta l'individuazione del servizio Service Fabric, la risoluzione della partizione, e route di replica selezione toointelligently richiede direttamente servizi tooback-end nell'infrastruttura del servizio, non vi è toowrite gateway API senza stato. 

In questo scenario, hello web che dell'interfaccia utente anche tramite un servizio web, mentre le chiamate API HTTP vengono gestite e instradate tramite Gestione API di Azure, come illustrato nel seguente diagramma hello:

![Panoramica di Service Fabric con topologia di Gestione API di Azure][sf-apim-web-app]

## <a name="application-scenarios"></a>Scenari applicativi

I servizi in Service Fabric possono essere con stato o senza stato ed essere partizionati usando uno di tre schemi: singleton, Int64 range e named. La risoluzione degli endpoint di servizio richiede l'identificazione di una specifica partizione di una determinata istanza del servizio. Durante la risoluzione di un endpoint di un servizio, entrambi hello nome dell'istanza del servizio (ad esempio, `fabric:/myapp/myservice`), nonché specificare partizione specifica di hello del servizio di hello, tranne nel caso di hello di partizione singleton.

Gestione API di Azure può essere usato con qualsiasi combinazione di servizi senza stato e con stato o qualsiasi schema di partizionamento.

## <a name="send-traffic-tooa-stateless-service"></a>Servizio senza stato tooa del traffico di trasmissione

Nel caso più semplice di hello, il traffico viene inoltrato l'istanza del servizio senza stato tooa. tooachieve, un'operazione di gestione API contiene un criterio dell'elaborazione in ingresso con un back-end di Service Fabric associato all'istanza di specifica del servizio senza stato tooa in hello Service Fabric back-end. Le richieste inviate toothat servizio vengono inviate tooa replica casuale dell'istanza di servizio senza stato hello.

#### <a name="example"></a>Esempio
Nel seguente scenario di hello, un'applicazione di Service Fabric contiene un servizio senza stato denominato `fabric:/app/fooservice`, che espone un'API HTTP interna. nome dell'istanza del servizio Hello è ben noto e possa essere hard-coded direttamente in hello criteri di gestione API di elaborazione in ingresso. 

![Panoramica di Service Fabric con topologia di Gestione API di Azure][sf-apim-static-stateless]

## <a name="send-traffic-tooa-stateful-service"></a>Servizio con stato tooa di traffico di trasmissione

Scenario di servizio senza stato toohello simile, il traffico può essere inoltrato tooa istanza di servizio con stato. In questo caso, un'operazione di gestione API contiene un criterio dell'elaborazione in ingresso con un back-end di Service Fabric che esegue il mapping di una partizione specifica tooa di richiesta di uno specifico *stateful* istanza del servizio. Hello partizione toomap toois ogni richiesta calcolata mediante un metodo di espressione lambda con alcuni input hello richiesta in ingresso HTTP, ad esempio un valore in hello percorso URL. Hello criterio potrebbe essere configurato toosend richieste toohello replica primaria solo, o tooa casuale per le operazioni di lettura.

#### <a name="example"></a>Esempio

In hello seguente scenario, un'applicazione di Service Fabric contiene un servizio con stato partizionato denominato `fabric:/app/userservice` che espone un'API HTTP interna. nome dell'istanza del servizio Hello è ben noto e possa essere hard-coded direttamente in hello criteri di gestione API di elaborazione in ingresso.  

Hello servizio è partizionato usando lo schema di partizione hello Int64 con due partizioni e un intervallo di chiavi che si estende su `Int64.MinValue` troppo`Int64.MaxValue`. criteri di back-end Hello calcola una chiave di partizione all'interno dell'intervallo convertendo hello `id` valore fornito in hello URL richiesta percorso tooa integer a 64 bit, anche se qualsiasi algoritmo può essere una chiave di partizione hello toocompute qui utilizzato. 

![Panoramica di Service Fabric con topologia di Gestione API di Azure][sf-apim-static-stateful]

## <a name="send-traffic-toomultiple-stateless-services"></a>Invia il traffico di servizi senza stato toomultiple

Negli scenari più avanzati, è possibile definire un'operazione di gestione API che esegue il mapping delle richieste toomore di istanza di un servizio. In questo caso, ogni operazione contiene un criterio che mappa le richieste istanza specifica del servizio tooa in base ai valori hello richiesta in ingresso HTTP, ad esempio di stringa di percorso o la query di URL hello e nel caso di hello di servizi con stato, una partizione nell'istanza di servizio hello . 

tooachieve questa gestione API di un'operazione contiene un criterio dell'elaborazione in ingresso con un back-end di Service Fabric associato all'istanza di servizio senza stato tooa in hello Service Fabric back-end in base ai valori recuperati da una richiesta HTTP in ingresso hello. Istanza del servizio tooa le richieste vengono inviate tooa replica casuale hello di istanze del servizio.

#### <a name="example"></a>Esempio

In questo esempio, una nuova istanza di servizio senza stato è creata per ogni utente di un'applicazione con un nome generato dinamicamente utilizzando hello formula seguente:
 
 - `fabric:/app/users/<username>`

 Ogni servizio dispone di un nome univoco, ma i nomi di hello non sono noti come iniziale perché hello servizi vengono creati nella risposta toouser o amministratore di input e pertanto non può essere codificato in Criteri di ruoli o le regole di routing. Al contrario, nome hello di hello servizio toowhich toosend una richiesta viene generato nella definizione di criteri di back-end hello da hello `name` valore fornito nel percorso di richiesta URL hello. ad esempio:

  - Oggetto richiesta troppo`/api/users/foo` è indirizzato tooservice istanza`fabric:/app/users/foo`
  - Oggetto richiesta troppo`/api/users/bar` è indirizzato tooservice istanza`fabric:/app/users/bar`

![Panoramica di Service Fabric con topologia di Gestione API di Azure][sf-apim-dynamic-stateless]

## <a name="send-traffic-toomultiple-stateful-services"></a>Invia il traffico di servizi con stato toomultiple

Le richieste di gestione API di un'operazione possibile eseguire il mapping di esempio di servizio senza stato toohello simile, toomore rispetto a uno **stateful** istanza del servizio, nel qual caso è anche necessario tooperform risoluzione di partizione per ogni servizio con stato istanza.

tooachieve questa gestione API di un'operazione contiene un criterio dell'elaborazione in ingresso con un back-end di Service Fabric associato all'istanza di servizio con stato tooa in hello Service Fabric back-end in base ai valori recuperati da una richiesta HTTP in ingresso hello. Inoltre i toomapping richiesta toospecific istanza del servizio richiesta hello può anche essere mappate tooa partizione specifica all'interno di istanza del servizio hello e, facoltativamente, replica primaria di hello tooeither o una replica secondaria casuale all'interno della partizione hello.

#### <a name="example"></a>Esempio

In questo esempio, una nuova istanza di servizio con stato è creata per ogni utente dell'applicazione hello con un nome generato dinamicamente utilizzando hello formula seguente:
 
 - `fabric:/app/users/<username>`

 Ogni servizio dispone di un nome univoco, ma i nomi di hello non sono noti come iniziale perché hello servizi vengono creati nella risposta toouser o amministratore di input e pertanto non può essere codificato in Criteri di ruoli o le regole di routing. Al contrario, nome hello di hello servizio toowhich toosend una richiesta viene generato nella definizione di criteri di back-end hello da hello `name` percorso della richiesta URL hello valore fornito. ad esempio:

  - Oggetto richiesta troppo`/api/users/foo` è indirizzato tooservice istanza`fabric:/app/users/foo`
  - Oggetto richiesta troppo`/api/users/bar` è indirizzato tooservice istanza`fabric:/app/users/bar`

Ogni istanza del servizio è partizionato anche utilizzando lo schema di partizione hello Int64 con due partizioni e un intervallo di chiavi che si estende su `Int64.MinValue` troppo`Int64.MaxValue`. criteri di back-end Hello calcola una chiave di partizione all'interno dell'intervallo convertendo hello `id` valore fornito in hello URL richiesta percorso tooa integer a 64 bit, anche se qualsiasi algoritmo può essere una chiave di partizione hello toocompute qui utilizzato. 

![Panoramica di Service Fabric con topologia di Gestione API di Azure][sf-apim-dynamic-stateful]

## <a name="next-steps"></a>Passaggi successivi

Seguire hello [Guida introduttiva](service-fabric-api-management-quick-start.md) tooset di infrastruttura del servizio prima del cluster con le richieste API di gestione e il flusso tramite servizi di gestione API tooyour.

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png