---
title: aaaOverview del modello di programmazione affidabile servizio Fabric hello | Documenti Microsoft
description: Informazioni sul modello di programmazione Reliable Services di Service Fabric e su come sviluppare servizi personalizzati.
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek; mani-ramaswamy
ms.assetid: 0c88a533-73f8-4ae1-a939-67d17456ac06
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: masnider;
ms.openlocfilehash: 41d1826df902b1f1845c4702bf2567e6b9ca1f1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-overview"></a>Panoramica di Reliable Services
Azure Service Fabric semplifica la scrittura e la gestione di Reliable Services con e senza stato. In questo argomento viene trattato quanto segue:

* Hello servizi affidabili modello di programmazione per i servizi senza stato.
* Hello scelte disponibili toomake durante la scrittura di un servizio affidabile.
* Alcuni scenari ed esempi dei casi toouse affidabile Services e modalità di scrittura.

Servizi affidabili è uno dei modelli disponibili in Service Fabric di programmazione hello. altri Hello è hello Reliable Actor modello di programmazione, che fornisce un modello di programmazione Actor virtuale sul modello di servizi affidabili hello. Per ulteriori informazioni sul modello di programmazione Reliable Actors hello, vedere [tooService introduzione dell'infrastruttura Reliable Actors](service-fabric-reliable-actors-introduction.md).

Service Fabric gestisce la durata hello dei servizi, dal provisioning e la distribuzione tramite l'aggiornamento ed eliminazione, tramite [Gestione applicazioni di Service Fabric](service-fabric-deploy-remove-applications.md).

## <a name="what-are-reliable-services"></a>Informazioni su Reliable Services
Servizi affidabili offre un semplice, potente di livello principale express che cos'è importante tooyour applicazione toohelp di modello di programmazione. Con servizi affidabili hello modello di programmazione, sono disponibili:

* Rest toohello di accesso di hello le API di programmazione di Service Fabric. A differenza dei servizi di infrastruttura servizio modellata come [eseguibili Guest](service-fabric-deploy-existing-app.md), servizi affidabili ottenere rest hello toouse di hello API dei servizi dell'infrastruttura direttamente. Questo consente ai servizi di:
  * query sul sistema hello
  * segnalare l'integrità sulle entità presenti nel cluster hello
  * ricevere notifiche sulle modifiche alla configurazione e al codice
  * individuare e comunicare con altri servizi,
  * (facoltativo) utilizzare hello [raccolte affidabile](service-fabric-reliable-services-reliable-collections.md)
  * ... e in modo che possano accedere toomany ad altre funzionalità, tutti da un modello di programmazione di prima classe in diversi linguaggi di programmazione.
* Un modello semplice per l'esecuzione di codice personalizzato simile ai modelli di programmazione di uso comune. Il codice ha un punto di ingresso ben definito e un ciclo di vita facile da gestire.
* Un modello di comunicazione modulare. Utilizzare il trasporto hello di propria scelta, ad esempio HTTP con [API Web](service-fabric-reliable-services-communication-webapi.md), WebSockets, i protocolli TCP personalizzati o qualsiasi altro elemento. Reliable Services fornisce alcune interessanti opzioni predefinite, ma consente anche di usarne di personalizzate.
* Per i servizi con stati, hello servizi affidabili modello di programmazione consente tooconsistently e archiviare in modo affidabile lo stato direttamente all'interno del servizio tramite [raccolte affidabile](service-fabric-reliable-services-reliable-collections.md). Le raccolte affidabili sono una semplice serie di classi di raccolte di elevata disponibilità e affidabilità che sarà familiare tooanyone che ha utilizzato c# raccolte. In passato, per la gestione di uno stato affidabile i servizi dovevano contare su sistemi esterni. Con le raccolte affidabile, è possibile archiviare il calcolo tooyour avanti di stato con hello stesso elevata disponibilità e affidabilità aver tooexpect forniti dagli archivi esterni a disponibilità elevata. Questo modello migliora anche latenza perché si sono condivisione del percorso calcolo hello e lo stato deve toofunction.

Vedere questo video di Microsoft Virtual Academy per una panoramica di Reliable Services: <center>
<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=HhD9566yC_4106218965">
<img src="./media/service-fabric-reliable-services-introduction/ReliableServicesVid.png" WIDTH="360" HEIGHT="244" />
</a>
</center>

## <a name="what-makes-reliable-services-different"></a>Caratteristiche distintive di Reliable Services
Reliable Services in Service Fabric è diverso da eventuali servizi sviluppati in precedenza. Service Fabric offre affidabilità, disponibilità, coerenza e scalabilità.

* **Affidabilità** : il servizio rimane backup anche in ambienti non affidabili in cui le macchine esito negativo o riscontri problemi di rete, o nei casi in cui servizi hello verificheranno degli errori e arresto anomalo del sistema o non riuscire. Per i servizi con stati, lo stato viene mantenuto anche in presenza di hello di rete o altri errori.
* **Disponibilità**: il servizio è raggiungibile e reattivo. Service Fabric mantiene il numero desiderato di copie in esecuzione.
* **Scalabilità** - servizi vengono disaccoppiati da hardware specifico e che è possibile aumentare o diminuire in base alle esigenze tramite hello aggiunta o rimozione di hardware o altre risorse. I servizi sono tooensure facilmente partizionato (soprattutto in caso di informazioni sullo stato hello) che è possibile scalare il servizio hello e gestire gli errori parziali. I servizi possono essere creati ed eliminato in modo dinamico tramite codice, consentendo più toobe istanze riattivata, se necessario, ad esempio nelle richieste toocustomer di risposta. Infine, Service Fabric incoraggia lightweight toobe servizi. Service Fabric consente a migliaia di servizi toobe il provisioning in un unico processo, anziché richiedere o dedicare intere istanze del sistema operativo o i processi tooa singola istanza di un servizio.
* **Coerenza** -tutte le informazioni memorizzate in questo servizio possono essere garantite toobe coerente. Questo vale anche tra più raccolte Reliable in un servizio. È possibile apportare modifiche nelle raccolte all'interno di un servizio con transazioni atomiche.

## <a name="service-lifecycle"></a>Ciclo di vita del servizio
Reliable Services fornisce un ciclo di vita semplice che consente di attivare rapidamente il codice e iniziare a usarlo.  Sono disponibili solo uno o due metodi è necessario il servizio tooimplement tooget attivo e in esecuzione.

* **CreateServiceReplicaListeners/CreateServiceInstanceListeners** -questo metodo è in servizio hello è definito hello stack(s) di comunicazione che desideri toouse. Hello stack di comunicazione, ad esempio [API Web](service-fabric-reliable-services-communication-webapi.md), è ciò che definisce hello endpoint in ascolto o gli endpoint per hello servizio (come raggiungere i client del servizio hello). Definisce inoltre il modo in cui vengono visualizzati messaggi hello interagiscono rest hello hello del codice di servizio.
* **RunAsync** -questo metodo è in cui il servizio viene eseguita la logica di business e in cui si avviano qualsiasi attività in background che deve essere eseguito per la durata di hello del servizio hello. token di annullamento Hello fornito è un segnale per quando è necessario interrompere il lavoro. Ad esempio, se il servizio hello deve toopull messaggi dalla coda affidabile ed elaborarle, è in cui viene eseguita tale lavoro.

Se si riferisce servizi affidabili per hello prima volta, leggere in. Se si sta cercando una procedura dettagliata di hello del ciclo di vita di servizi affidabili, è possibile visitare troppo[questo articolo](service-fabric-reliable-services-lifecycle.md).

## <a name="example-services"></a>Servizi di esempio
La conoscenza di questo modello di programmazione, esaminiamo un rapido due diversi servizi toosee, come vengono assemblati questi pezzi.

### <a name="stateless-reliable-services"></a>Reliable Services senza stato
Un servizio senza stato è una posizione in cui vi è alcuno stato gestito all'interno del servizio hello durante le chiamate. Qualsiasi stato presente è interamente eliminabile e non richiede sincronizzazione, replica, persistenza o disponibilità elevata.

Si consideri ad esempio una calcolatrice che non ha memoria e riceve tutti tooperform termini e le operazioni in una sola volta.

In questo caso, hello `RunAsync()` (c#) o `runAsync()` (linguaggio) di hello servizio può essere vuoto, poiché non esiste alcun background attività elaborazione servizio hello deve toodo. Quando viene creato il servizio di calcolatrice hello, restituisce un `ICommunicationListener` (c#) o `CommunicationListener` (linguaggio) (ad esempio [API Web](service-fabric-reliable-services-communication-webapi.md)) che consente di aprire un endpoint in ascolto su una porta. Questo endpoint di ascolto Aggancia toohello differenti metodi di calcolo (esempio: "Add (n1, n2)") che definiscono l'API pubblica della calcolatrice hello.

Quando viene effettuata una chiamata da un client, hello appropriato viene richiamato il metodo e il servizio di calcolatrice hello hello operazioni eseguite su hello dati specificato e restituisce il risultato di hello. Il servizio Calculator esegue le operazioni sui dati forniti e restituisce il risultato, senza archiviare alcuno stato.

La mancata archiviazione di qualsiasi stato interno rende semplice il servizio Calculator di esempio. La maggior parte dei servizi non è però realmente senza stato. Invece, si Esternalizza toosome loro stato altro archivio. Ad esempio, un'app Web che mantiene lo stato delle sessioni in una cache o in un archivio di backup non è senza stato.

Un esempio comune di servizi come senza informazioni sullo stato vengono utilizzati in Service Fabric è come front-end che espone hello API pubblico per un'applicazione web. servizio front-end Hello comunica quindi toostateful servizi toocomplete una richiesta dell'utente. In questo caso, le chiamate da client sono diretto tooa noto porta, ad esempio 80, in cui è in ascolto servizio senza stato hello. Questo servizio senza stato riceve chiamata hello e determina se chiamata hello da una fonte attendibile e che servizio a cui è destinato.  Quindi, servizio senza stato hello inoltra partizione corretta hello chiamata toohello di servizio con stato hello e attende una risposta. Quando il servizio senza stato hello riceve una risposta, risponde toohello originale client. Un esempio di tale servizio è disponibile in [C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) / [Java](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Actors/VisualObjectActor/VisualObjectWebService). Questo è solo un esempio di questo modello negli esempi di hello, esistono altri in anche altri esempi.

### <a name="stateful-reliable-services"></a>Reliable Services con stato
Un servizio con stato è quello che deve avere una parte dello stato mantenuta coerente e presente affinché toofunction servizio hello. Si consideri, ad esempio, un servizio che deve calcolare costantemente la media mobile di alcuni valori in base agli aggiornamenti ricevuti. toodo, deve disporre di hello set corrente di richieste in ingresso deve tooprocess e hello Media attuale. Qualsiasi servizio che recupera, elabora e archivia informazioni in un archivio esterno, ad esempio un archivio tabelle o un BLOB di Azure, è un servizio con stato. Mantiene solo lo stato nell'archivio di stato esterno hello.

La maggior parte dei servizi archiviano oggi il proprio stato esternamente, poiché archivio esterno hello cosa offre affidabilità, disponibilità, scalabilità e la coerenza di tale stato. Nell'infrastruttura del servizio, di servizi non è necessari toostore stato esternamente. Service Fabric si occupa di questi requisiti per il codice di servizio hello e lo stato del servizio hello.

> [!NOTE]
> Il supporto per Reliable Services con stato non è ancora disponibile in Linux (per C# o Java).
>

Si supponga toowrite un servizio che elabora le immagini. toodo questo hello servizio accetta un'immagine e hello serie di conversioni tooperform su quell'immagine. Il servizio restituisce un listener di comunicazione (si supponga che sia un'API Web) che espone un'API come `ConvertImage(Image i, IList<Conversion> conversions)`. Quando riceve una richiesta, il servizio hello viene memorizzato in un `IReliableQueue`e restituisce alcuni client toohello id, quindi è possibile tenere traccia delle richiesta hello.

In questo servizio `RunAsync()` potrebbe essere più complesso. servizio Hello è presente un ciclo all'interno di relativo `RunAsync()` che effettua il pull delle richieste di `IReliableQueue` ed esegue le conversioni di hello richieste. risultati Hello ottengano archiviati in un `IReliableDictionary` in modo che quando il client hello torna possono ottenere le immagini convertite. tooensure che anche nel caso di errori immagine hello non vada perduto, questo servizio affidabile verrà pull dalla coda di hello, eseguire le conversioni di hello e memorizza il risultato di hello in una singola transazione. In questo caso, il messaggio hello viene rimosso dalla coda hello e risultati hello vengono archiviati nel dizionario di risultato hello solo quando vengono completate le conversioni di hello. In alternativa, servizio hello Impossibile estrarre immagine hello dalla coda hello e immediatamente archiviarlo in un archivio remoto. Questo riduce hello quantità del servizio di stato hello è toomanage, ma aumenta la complessità poiché servizio hello ha tookeep hello necessarie toomanage hello remoto metadati. Con entrambi gli approcci, se un elemento non è riuscito a hello hello intermedio richiesta rimane in hello coda in attesa toobe elaborati.

Una cosa toonote su questo servizio è può sembrare un normale servizio .NET. Hello unica differenza è che le strutture di dati hello in uso (`IReliableQueue` e `IReliableDictionary`) vengono forniti dall'infrastruttura di servizio e sono altamente affidabile, disponibili e coerente.

## <a name="when-toouse-reliable-services-apis"></a>Quando toouse API dei servizi affidabili
Se una delle seguenti operazioni hello caratterizzare le esigenze dell'applicazione del servizio, è necessario considerare affidabile API dei servizi:

* Si desidera che il codice del servizio (e facoltativamente) toobe elevata disponibilità e affidabilità
* Sono necessarie garanzie transazionali in più unità di stato multiple, ad esempio elementi di ordine e righe di ordine.
* Lo stato dell'applicazione può essere modellato naturalmente sotto forma di oggetti ReliableDictionary e ReliableQueue.
* Il codice delle applicazioni o lo stato deve toobe a disponibilità elevata con bassa latenza letture e scritture.
* L'applicazione deve toocontrol hello concorrenza o granularità di operazioni transazionali in uno o più raccolte affidabile.
* Si desiderano le comunicazioni hello toomanage o hello controllo combinazione per il servizio di partizionamento.
* Il codice necessita di un ambiente di runtime a thread libero.
* L'applicazione deve toodynamically creare o eliminare dizionari affidabile o le code o interi servizi in fase di esecuzione.
* È necessario tooprogrammatically fornito Service Fabric backup e ripristino di funzionalità di controllo per lo stato del servizio.
* L'applicazione richiede la cronologia delle modifiche toomaintain per unità di stato.
* Si desidera toodevelop o utilizzata il provider di stato sviluppato a terze parti e personalizzati.

## <a name="next-steps"></a>Passaggi successivi
* [Guida introduttiva a Reliable Services di Microsoft Azure Service Fabric](service-fabric-reliable-services-quick-start.md)
* [Uso avanzato del modello di programmazione Reliable Services](service-fabric-reliable-services-advanced-usage.md)
* [modello di programmazione di Hello Reliable Actors](service-fabric-reliable-actors-introduction.md)
