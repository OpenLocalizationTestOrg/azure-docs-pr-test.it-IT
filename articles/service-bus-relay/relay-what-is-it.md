---
title: "aaaWhat è l'inoltro di Azure e perché usarlo Panoramica | Documenti Microsoft"
description: Panoramica del servizio di inoltro di Azure
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1e3e971d-2a24-4f96-a88a-ce3ea2b1a1cd
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 4cfd77048210a435c446b908b7896737cad0edbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-relay"></a>Che cos'è il servizio di inoltro di Azure?

Hello Azure inoltro servizio facilita ibrida applicazioni abilitando toosecurely si espongono i servizi che risiedono all'interno di un'organizzazione aziendale rete toohello pubblica cloud senza una connessione di firewall, tooopen o richiedono intrusivo cambia tooa infrastruttura della rete aziendale. Il servizio di inoltro supporta un'ampia gamma di protocolli di trasporto e standard dei servizi Web.

il servizio di inoltro Hello supporta richiesta/risposta, unidirezionale tradizionale e il traffico peer-to-peer. Supporta inoltre la distribuzione di eventi in scenari di pubblicazione/sottoscrizione tooenable ambito internet e comunicazione tramite socket bidirezionale per migliorare l'efficienza Point to Point maggiore. 

Nel modello di trasferimento di hello inoltro dei dati, un servizio locale si connette il servizio di inoltro toohello tramite una porta in uscita e crea un socket bidirezionale per indirizzo rendezvous specifico tooa di comunicazione associato. client di Hello può quindi comunicare con il servizio locale hello inviando servizio inoltro del traffico toohello Assegnazione indirizzo rendezvous hello. il servizio di inoltro Hello quindi "Inoltra" servizio locale toohello di dati tramite un client dedicato tooeach socket bidirezionale. Hello client non necessita di un servizio locale di toohello connessione diretta, non è necessario tooknow in cui risiede il servizio hello e servizio locale hello non necessita di porte in ingresso aperte nel firewall hello.

gli elementi chiave funzionalità Hello forniti da inoltro sono bidirezionali, non memorizzato nel buffer di comunicazione attraverso i limiti di rete con la limitazione delle richieste di tipo TCP, individuazione di endpoint, lo stato della connettività e sovrapposti di sicurezza degli endpoint. funzionalità di inoltro Hello diverse tecnologie di integrazione a livello di rete, ad esempio VPN, in tale inoltro può essere tooa con ambito applicazione singolo endpoint in un unico computer, mentre la tecnologia VPN è molto più intrusiva quanto si basa sulla modifica di ambiente di rete hello .

Il servizio di inoltro di Azure include due funzionalità.

1. [Le connessioni ibride](#hybrid-connections) - utilizza hello aprire standard WebSocket abilitazione di scenari con più piattaforme.
2. [Gli inoltri WCF](#wcf-relays) -chiamate di procedura remota tooenable utilizza Windows Communication Foundation (WCF). Inoltro di WCF è inoltro legacy di hello offerta che molti clienti usano già con i relativi modelli di programmazione WCF.

Connessioni ibride e inoltri WCF consentono una connessione sicura tooassets esistenti all'interno di una rete aziendale dell'organizzazione. Uso di uno su altri hello è dipendente alle esigenze specifiche, come descritto in hello nella tabella seguente:

|  | Inoltro WCF | Connessioni ibride |
| --- |:---:|:---:|
| **WCF** |x | |
| **.NET Core** | |x |
| **.NET Framework** |x |x |
| **JavaScript/NodeJS** | |x |
| **Protocollo aperto basato su standard** | |x |
| **Più modelli di programmazione RPC** | |x |

## <a name="hybrid-connections"></a>connessioni ibride

Hello [connessioni ibride di inoltro Azure](relay-hybrid-connections-protocol.md) funzionalità è un'evoluzione protetta, aprire protocollo di hello esistente le funzionalità di inoltro che possono essere implementate in qualsiasi piattaforma e in qualsiasi linguaggio che è una funzionalità di base WebSocket, che include in modo esplicito hello WebSocket API nel browser. La funzionalità Connessioni ibride è basata su HTTP e WebSocket.

### <a name="service-history"></a>Storia del servizio

Le connessioni ibride sostituisce ex hello, denominato in modo simile funzionalità "BizTalk Services" che è stato creato il hello inoltro WCF di Azure Service Bus. nuova funzionalità di connessioni ibride Hello si integra con funzionalità di inoltro WCF esistente hello e queste funzionalità di due servizio esistono side-by-side nel servizio di inoltro di Azure hello. Condividono un gateway comune, ma costituiscono per il resto implementazioni diverse.

## <a name="wcf-relays"></a>Inoltri WCF

funzionamento di inoltro WCF Hello per hello completo .NET Framework (NETFX) e per WCF. Avviare connessione hello tra il servizio locale e servizio di inoltro hello mediante un gruppo di associazioni di WCF "inoltro". Background hello, binding di inoltro hello mappa toonew trasporto associazione elementi progettati toocreate canale componenti WCF che si integrano con il Bus di servizio nel cloud hello.

## <a name="architecture-processing-of-incoming-relay-requests"></a>Architettura: elaborazione delle richieste di inoltro in ingresso
Quando un client invia una richiesta toohello [inoltro Azure](/azure/service-bus-relay/) service, servizio di bilanciamento del carico di Azure hello lo indirizza tooany dei nodi gateway hello. Se la richiesta hello è in ascolto, nodo gateway hello crea un nuovo relay. Se la richiesta hello un inoltro specifico di connessione richiesta tooa, nodo gateway hello inoltra hello connessione richiesta toohello gateway nodo proprietario inoltro hello. nodo di gateway Hello proprietario inoltro hello invia un rendezvous richiesta toohello ascolto client, che richiede di un nodo di gateway toohello canale temporaneo che ha ricevuto la richiesta di connessione hello toocreate listener hello.

Quando viene stabilita connessione relay hello, i client hello possono scambiare messaggi tramite nodo gateway hello che viene utilizzato per rendezvous hello.

![Elaborazione delle richieste di inoltro Web application firewa in ingresso](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a>Passaggi successivi

* [Domande frequenti sull'inoltro](relay-faq.md)
* [Creare uno spazio dei nomi](relay-create-namespace-portal.md)
* [Introduzione a .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introduzione a Node](relay-hybrid-connections-node-get-started.md)

