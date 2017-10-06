---
title: aaaOverview di AMQP 1.0 in Azure Service Bus | Documenti Microsoft
description: Informazioni sull'uso di hello Advanced Message Queuing Protocol (AMQP) 1.0 in Azure.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0e8d19cc-de36-478e-84ae-e089bbc2d515
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: c35a20c50dd24845d9a4c7a0251e8240848a6f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-support-in-service-bus"></a>Supporto per il protocollo AMQP 1.0 nel bus di servizio
Entrambi hello in locale e servizio cloud di Azure Service Bus [Service Bus per Windows Server (Service Bus 1.1)](https://msdn.microsoft.com/library/dn282144.aspx) supporto hello Advanced Message Queuing Protocol (AMQP) 1.0. AMQP consente si toobuild multipiattaforma, di applicazioni ibride tramite un protocollo standard aperto. È possibile creare applicazioni usando componenti creati in linguaggi e framework diversi e in esecuzione su sistemi operativi diversi. Tutti questi componenti possono connettersi tooService Bus e facilmente scambiarsi messaggi aziendali strutturati in modo efficiente e alla massima fedeltà.

## <a name="introduction-what-is-amqp-10-and-why-is-it-important"></a>Introduzione: informazioni sul protocollo AMQP 1.0 e sulla sua rilevanza
I prodotti middleware orientati ai messaggi hanno tradizionalmente usato protocolli proprietari per le comunicazioni tra applicazioni client e broker. Ciò significa che dopo aver selezionato i broker di messaggistica un particolare fornitore, è necessario utilizzare tooconnect librerie del fornitore intermediario toothat di applicazioni client. Ciò consente di un livello di dipendenza dal fornitore, poiché il porting di un prodotto di applicazione tooa diverso richiede modifiche del codice in tutte le applicazioni hello connesso. 

La connessione di broker di messaggistica da fornitori diversi è inoltre complicata Questo in genere richiede messaggi toomove bridging a livello di applicazione da un sistema tooanother e tootranslate tra i formati di messaggio proprietario. Questo è un requisito comune; ad esempio, quando è necessario fornire un nuovo tooolder interfaccia unificata sistemi diversi o integrare i sistemi IT dopo una fusione tra società.

settore software Hello è un'azienda rapido. a un ritmo contribuito a volte vengono introdotti nuovi linguaggi di programmazione e altri framework applicazione. Analogamente, evolversi delle esigenze di hello dei sistemi IT nel corso del tempo e gli sviluppatori desiderino tootake sfruttare funzionalità più recenti della piattaforma hello. Tuttavia, talvolta hello fornitore messaggistica selezionato non supporta queste piattaforme. Poiché i protocolli di messaggistica sono proprietari, non è possibile per gli altri utenti tooprovide librerie per queste nuove piattaforme. Pertanto, è necessario utilizzare gli approcci, ad esempio la compilazione di gateway o bridge che consentono di toocontinue toouse hello messaggistica prodotto.

sviluppo di Hello di hello Advanced Message Queuing Protocol (AMQP) 1.0 è stato eseguito da tali problemi. presso JP Morgan Chase, che, come la maggior parte delle aziende del settore dei servizi finanziari, fa ampio uso di prodotti middleware orientati alla messaggistica. obiettivo Hello è semplice: un protocollo di messaggistica standard aperti che viene effettuata utilizzando i componenti compilati utilizzando diversi linguaggi, Framework e sistemi operativi, applicazioni basate su messaggi toobuild possibili toocreate tutte utilizzano i componenti di migliori da un intervallo di fornitori.

## <a name="amqp-10-technical-features"></a>Caratteristiche tecniche del protocollo AMQP 1.0
AMQP 1.0 è un protocollo di messaggistica efficiente, affidabile e a livello di rete che è possibile utilizzare toobuild multipiattaforma affidabile, applicazioni di messaggistica. protocollo Hello ha l'obiettivo semplice: meccanismi hello toodefine hello protetta, affidabile ed efficiente di trasferimento dei messaggi tra due parti. messaggi Hello stessi vengono codificati utilizzando una rappresentazione dati portatile che consente di eterogenei mittenti e ricevitori tooexchange strutturato messaggi di business alla massima fedeltà. di seguito Hello è un riepilogo delle funzionalità più importanti hello:

* **Efficiente**: AMQP 1.0 è un protocollo orientato alla connessione che usa una codifica per hello binaria istruzioni del protocollo e hello messaggi aziendali trasferiti su di esso. Incorpora un controllo di flusso sofisticati schemi toomaximize hello utilizzo delle rete hello e componenti hello connesso. Ciò premesso, hello è stato progettato toostrike un equilibrio tra efficienza, flessibilità e interoperabilità.
* **Affidabile**: hello protocollo AMQP 1.0 consente toobe di messaggi scambiati con un intervallo di garanzie di affidabilità, dal tooreliable fire-and-forget, esattamente-una volta riconosciuto recapito.
* **Flessibile**: AMQP 1.0 è un protocollo flessibile che può essere utilizzato toosupport diverse topologie. Hello stesso protocollo può essere utilizzato per le comunicazioni da client client-gestore e gestore-gestore.
* **Indipendenza dal modello di Broker**: hello protocollo AMQP 1.0 non impone requisiti relativi modello di messaggistica hello usato da un gestore. Ciò significa che è possibile tooeasily aggiungere tooexisting di supporto di AMQP 1.0 Broker di messaggistica.

## <a name="amqp-10-is-a-standard-with-a-capital-s"></a>AMQP 1.0 è uno standard affermato
AMQP 1.0 è uno standard internazionale approvato da ISO e IEC come ISO/IEC 19464:2014.

Lo sviluppo di AMQP 1.0 procede dal 2008 a opera di un gruppo fondamentale di oltre 20 società, di cui fanno parte fornitori di tecnologie e aziende utenti finali. Durante questo periodo, aziende utenti hanno comunicato i requisiti aziendali reali e i fornitori di tecnologie hello si sono evoluti hello protocollo toomeet tali requisiti. Durante il processo di hello, fornitori hanno partecipato workshop in cui essi hanno collaborato interoperabilità hello toovalidate tra le diverse implementazioni.

In ottobre 2011, il processo di sviluppo hello passata tooa comitato tecnico all'interno dell'organizzazione di hello per hello Advancement di Structured Information Standards (OASIS) e hello Standard OASIS AMQP 1.0 è stato rilasciato in ottobre 2012. Hello imprese seguenti hanno partecipato comitato tecnico hello durante lo sviluppo di hello di hello standard:

* **Fornitori di tecnologie**: Axway Software, Huawei Technologies, IIT Software, INETCO Systems, Kaazing, Microsoft, Mitre Corporation, Primeton Technologies, Progress Software, Red Hat, SITA, Software AG, Solace Systems, VMware, WSO2, Zenika.
* **Aziende utenti**: Bank of America, Credit Suisse, Deutsche Boerse, Goldman Sachs, JPMorgan Chase.

Di hello comunemente menzionate degli standard aperti seguenti vantaggi:

* Minore possibilità di blocco da parte del fornitore
* Interoperabilità
* Ampia disponibilità di librerie e strumenti
* Protezione dall'obsolescenza
* Disponibilità di personale competente
* Rischio ridotto e gestibile

## <a name="amqp-10-and-service-bus"></a>AMQP 1.0 e bus di servizio
Supporto di AMQP 1.0 in Azure Service Bus indica che è possibile sfruttare hello Bus di servizio di accodamento e di pubblicazione/sottoscrizione funzionalità di messaggistica negoziata da una vasta gamma di piattaforme usando un protocollo binario efficiente. Inoltre, è possibile creare applicazioni costituite da componenti creati con un insieme di linguaggi, framework e sistemi operativi.

Hello figura riportata di seguito viene illustrato un esempio di distribuzione in cui client Java in esecuzione in Linux, scritti con API Java Message Service (JMS) standard hello e client .NET in esecuzione su Windows scambiano messaggi tramite il Bus di servizio tramite AMQP 1.0.

![][0]

**Figura 1: Scenario di distribuzione di esempio, in cui per la messaggistica tra diverse piattaforme usa il bus di servizio e il protocollo AMQP 1.0**

In questo hello ora librerie client seguenti sono noti toowork con il Bus di servizio:

| Lingua | Libreria |
| --- | --- |
| Java |Client Apache Qpid Java Message Service (JMS)<br/>Client IIT Software SwiftMQ Java |
| C |Apache Qpid Proton-C |
| PHP |Apache Qpid Proton-PHP |
| Python |Apache Qpid Proton-Python |
| C# |AMQP .Net Lite |

**Figura 2: Tabella delle librerie client del protocollo AMQP 1.0**

## <a name="summary"></a>Riepilogo
* AMQP 1.0 è un protocollo di messaggistica affidabile, aprire che è possibile utilizzare applicazioni ibride di toobuild multipiattaforma. AMQP 1.0 è uno standard OASIS.
* Il supporto per il protocollo AMQP 1.0 è ora disponibile nel bus di servizio di Azure e nel bus di servizio per Windows Server (Service Bus 1.1). I prezzi sono hello che stesso hello protocolli esistenti.

## <a name="next-steps"></a>Passaggi successivi
Pronto più toolearn? Visitare hello seguenti collegamenti:

* [Uso del bus di servizio da .NET con AMQP]
* [Uso del bus di servizio da Java con AMQP]
* [Installazione di Apache Qpid Proton-C in una macchina virtuale Linux di Azure]
* [AMQP nel bus di servizio per Windows Server]

[0]: ./media/service-bus-amqp-overview/service-bus-amqp-1.png
[Uso del bus di servizio da .NET con AMQP]: service-bus-amqp-dotnet.md
[Uso del bus di servizio da Java con AMQP]: service-bus-amqp-java.md
[Installazione di Apache Qpid Proton-C in una macchina virtuale Linux di Azure]: service-bus-amqp-apache.md
[AMQP nel bus di servizio per Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
