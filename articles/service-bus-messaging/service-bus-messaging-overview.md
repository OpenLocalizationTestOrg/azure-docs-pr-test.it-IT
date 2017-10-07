---
title: Cenni preliminari sulla messaggistica di Service Bus aaaAzure | Documenti Microsoft
description: Descrizione della messaggistica del bus di servizio e dell'inoltro di Azure
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f99766cb-8f4b-4baf-b061-4b1e2ae570e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: ede2904e11544d8f9428a2d657dcc77dacd95ac4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-flexible-data-delivery-in-hello-cloud"></a>Bus di servizio di messaggistica: recapito dei dati flessibile nel cloud hello
Il bus di servizio di Microsoft Azure è un servizio di recapito di informazioni affidabile. scopo di Hello di questo servizio è più facile la comunicazione toomake. Quando due o più parti tooexchange utili, è necessario un coordinatore di comunicazione. Il bus di servizio è un meccanismo di comunicazione negoziato o di terze parti. Ciò è simile servizio postale tooa HelloWorld fisico. Servizi postali renderlo toosend molto semplice diversi tipi di pacchetti con una serie di garanzie di recapito e le lettere in un punto qualsiasi in HelloWorld.

Il servizio postale toohello simile lettere, Bus di servizio di recapito è recapito flessibile informazioni dal mittente hello e destinatario hello. Hello servizio di messaggistica garantisce che le informazioni di hello sono recapitate anche se le parti hello due mai entrambi online hello stesso tempo, o se non sono disponibili in hello esatta stesso tempo. In questo modo, messaggistica è simile toosending una lettera, mentre la comunicazione non negoziata è simile tooplacing una telefonata (o utilizzo di una chiamata telefonica toobe - prima dell'attesa e chiamante ID chiamata, che sono molto più simile alla messaggistica negoziata).

mittente del messaggio Hello è inoltre possibile richiedere un'ampia gamma di caratteristiche del recapito tra cui transazioni, il rilevamento dei duplicati, basati sull'ora di scadenza e l'invio in batch. Anche questi modelli presentano analogie con il servizio postale: consegna ripetuta, firma obbligatoria, modifica dell'indirizzo o richiamo.

Il bus di servizio supporta due modelli di messaggistica distinti: *inoltro di Azure* e *messaggistica del bus di servizio*.

## <a name="azure-relay"></a>Servizio di inoltro di Azure
Hello [inoltro WCF](../service-bus-relay/relay-what-is-it.md) componente di inoltro di Azure è un servizio centralizzato (con elevato bilanciamento del carico) che supporta un'ampia gamma di protocolli di trasporto differenti e servizi Web standard. tra cui SOAP, WS-* e anche REST. Hello [servizio di inoltro](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md) offre un'ampia gamma di opzioni di connettività di inoltro diversi e consentono di negoziare le connessioni dirette peer-to-peer, quando possibile. Bus di servizio è ottimizzato per gli sviluppatori di .NET che utilizzano Windows Communication Foundation (WCF), entrambi con tooperformance considerare che l'usabilità, hello e fornisce accesso completo tooits servizio di inoltro tramite interfacce SOAP e REST. Questo rende possibile per qualsiasi programmazione SOAP o REST toointegrate ambiente con il Bus di servizio.

il servizio di inoltro Hello supporta la messaggistica unidirezionale tradizionale, messaggistica di richiesta/risposta e la messaggistica peer-to-peer. Supporta anche la distribuzione di eventi nell'ambito di Internet tooenable pubblicazione-sottoscrizione scenari e comunicazione tramite socket bidirezionale per migliorare l'efficienza Point to Point maggiore. Nel modello di messaggistica inoltrata hello, un servizio locale si connette il servizio di inoltro toohello tramite una porta in uscita e crea un socket bidirezionale per indirizzo rendezvous specifico tooa di comunicazione associato. client di Hello può quindi comunicare con il servizio locale hello inviando messaggi del servizio di inoltro toohello Assegnazione indirizzo rendezvous hello. il servizio di inoltro Hello verrà quindi "servizio di inoltro" messaggi toohello locale attraverso il socket bidirezionale hello già in uso. Hello client non è necessario un servizio locale di toohello connessione diretta e non è necessario it tooknow in cui risiede il servizio hello e servizio locale hello non necessita di porte in ingresso aperte nel firewall hello.

Si avvia connessione hello tra il servizio locale e servizio di inoltro hello, utilizzando una suite di "inoltro" associazioni di WCF. Background hello, binding di inoltro hello mappa tootransport associazione elementi progettati toocreate canale componenti WCF che si integrano con il Bus di servizio nel cloud hello.

Inoltro WCF offre numerosi vantaggi, ma richiede hello server e client tooboth essere online all'indirizzo hello stesso periodo di tempo in ordine toosend e ricevere messaggi. Questo comportamento non è ottimale per la comunicazione di tipo HTTP, in cui hello richieste potrebbero non essere in genere di lunga durate, né per i client che si connettono solo occasionalmente, ad esempio i browser, applicazioni per dispositivi mobili e così via. La messaggistica negoziata supporta la comunicazione disaccoppiata e presenta dei vantaggi; i client e server possono connettersi quando necessario ed eseguire le operazioni in modo asincrono.

## <a name="brokered-messaging"></a>Messaggistica negoziata
Al contrario di inoltro di schema, Bus di servizio di messaggistica, toohello o [messaggistica negoziata](service-bus-queues-topics-subscriptions.md) può essere considerata come asincrona o "temporaneamente disaccoppiata". Producer e consumer (ricevitori) non è in linea toobe in hello contemporaneamente. infrastruttura di messaggistica Hello archivia in modo affidabile i messaggi in un "gestore" (ad esempio una coda) hello finché consumer non è pronto tooreceive li. In questo modo i componenti di hello di toobe applicazione hello distribuita disconnesso, ovvero volontariamente; ad esempio, per la manutenzione o a causa di arresto anomalo del componente tooa, senza influire sull'intero sistema hello. Inoltre, un'applicazione ricevente hello può avere toocome online in certi orari del giorno hello, ad esempio un sistema di gestione inventario che è solo necessario toorun alla fine giornata lavorativa hello hello.

componenti di base Hello dell'infrastruttura di messaggistica negoziata di hello Bus di servizio sono code, argomenti e sottoscrizioni.  Hello principale differenza è che gli argomenti supportano le funzionalità di pubblicazione/sottoscrizione che possono essere utilizzate per basato sul contenuto routing e al recapito logica sofisticata, tra cui l'invio di toomultiple destinatari. Questi componenti consentono nuovi scenari di messaggistica asincrona, ad esempio disaccoppiamento temporale, pubblicazione/sottoscrizione e bilanciamento del carico. Per altre informazioni sulle entità di messaggistica, vedere [Code, argomenti e sottoscrizioni del bus di servizio](service-bus-queues-topics-subscriptions.md).

Come con l'infrastruttura di inoltro WCF hello, hello messaggistica negoziata funzionalità disponibile per i programmatori di .NET Framework e WCF, nonché tramite REST.

## <a name="next-steps"></a>Passaggi successivi
toolearn più sulla messaggistica del Bus di servizio, vedere hello seguenti argomenti.

* [Dati fondamentali del bus di servizio](service-bus-fundamentals-hybrid-solutions.md)
* [Code, argomenti e sottoscrizioni del bus di servizio](service-bus-queues-topics-subscriptions.md)
* [Come le code del Bus di servizio toouse](service-bus-dotnet-get-started-with-queues.md)
* [Il Bus di servizio toouse argomenti e sottoscrizioni](service-bus-dotnet-how-to-use-topics-subscriptions.md)

