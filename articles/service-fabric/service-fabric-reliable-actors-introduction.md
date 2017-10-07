---
title: aaaService infrastruttura affidabile attori Panoramica | Documenti Microsoft
description: Introduzione toohello Service Fabric Reliable Actors modello di programmazione.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 7fdad07f-f2d6-4c74-804d-e0d56131f060
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab010cbf936c6cf723b3d453ef95a9bf51f76c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-reliable-actors"></a>Introduzione tooService infrastruttura Reliable Actors
Reliable Actors è un framework di applicazione di Service Fabric in base a hello [Actor virtuale](http://research.microsoft.com/en-us/projects/orleans/) modello. Hello affidabile attori API fornisce un modello di programmazione a thread singolo compilato in hello scalabilità e affidabilità garanzie fornite dall'infrastruttura del servizio.

## <a name="what-are-actors"></a>Che cosa sono gli attori?
Un attore è un'unità isolata e indipendente di calcolo e di stato con esecuzione a thread singolo. Hello [modello attore](https://en.wikipedia.org/wiki/Actor_model) è un modello di calcolo per i sistemi simultanei o distribuiti che un numero elevato di questi operatori possono essere eseguite simultaneamente in modo indipendente. Gli attori possono comunicare tra loro e possono creare altri attori.

### <a name="when-toouse-reliable-actors"></a>Quando toouse Reliable Actors
Servizio Fabric Reliable Actors è un'implementazione del modello di progettazione di hello attore. Come con qualsiasi modello di progettazione del software, decisione hello se toouse un pattern specifico viene eseguito in base a o meno un software per progettare problema soddisfa il criterio di hello.

Sebbene l'attore hello progettazione modello può essere che ideale tooa numerosi problemi di sistemi distribuiti e gli scenari, un'attenta considerazione dei vincoli di hello del criterio di hello e framework hello implementarlo deve essere eseguita. Come indicazione generale, prendere in considerazione hello attore modello toomodel il problema o scenario se:

* Il problema riguarda un gran numero (migliaia o più) di piccole unità indipendenti e isolate di stato e logica.
* Si desidera toowork con oggetti a thread singolo che non richiedono una notevole interazione da componenti esterni, incluse l'esecuzione di query dello stato in un set di attori.
* Le istanze degli attori non bloccano i chiamanti con ritardi imprevedibili eseguendo operazioni I/O.

## <a name="actors-in-service-fabric"></a>Attori in Service Fabric
In Service Fabric, attori vengono implementati in framework Reliable Actors hello: un framework di applicazione basato su attori modello compilato in cima [affidabili servizi dell'infrastruttura](service-fabric-reliable-services-introduction.md). Ogni servizio di tipo Reliable Actor che viene scritto è di fatto un servizio Reliable partizionato con stato.

Ogni attore è definito come un'istanza di un tipo attore, identici toohello modo un oggetto .NET è un'istanza di un tipo .NET. Potrebbe esserci più attori di quel tipo distribuiti su vari nodi in un cluster, ad esempio, potrebbe esserci un tipo actor che implementa la funzionalità di hello di una calcolatrice. Ciascuno di questi attori è identificato in modo univoco da un ID.

### <a name="actor-lifetime"></a>Durata attore
Gli attori di Service Fabric sono virtuali, che significa che la durata non rappresentazione in memoria vincolata tootheir. Di conseguenza, non è necessario toobe creato o eliminato in modo esplicito. runtime Reliable Actors Hello attiva automaticamente hello un attore prima volta che riceve una richiesta per tale ID attore. Se un attore non viene utilizzato per un periodo di tempo, hello Reliable Actors runtime garbage-raccoglie oggetti in memoria hello. Anche manterrà conoscenza dell'esistenza dell'attore hello dovrebbe essere necessario toobe riattivati in un secondo momento. Per altre informazioni, vedere [Ciclo di vita degli attori e Garbage Collection](service-fabric-reliable-actors-lifecycle.md).

Questa astrazione durata actor virtuale esegue alcune raccomandazioni come risultato modello actor virtuale hello e in realtà hello implementazione Reliable Actors devia orari da questo modello.

* Un attore viene attivato automaticamente (causando un attore toobe oggetto costruito) hello prima volta che un messaggio viene inviato ID attore tooits Dopo un certo periodo di tempo, l'oggetto attore hello è sottoposto a garbage collection. In hello futuro, utilizzando di nuovo ID attore hello provoca un attore nuovo toobe oggetto costruito. Stato di un attore sia maggiore di quella durata dell'oggetto hello quando archiviata nel gestore degli stati hello.
* La chiamata di un qualsiasi metodo di attore per l'ID attore attiva l'attore. Per questo motivo, attore hanno il relativo costruttore chiamato in modo implicito dal runtime di hello. Pertanto, il codice client non è possibile passare al costruttore del tipo di parametri toohello attore, anche se i parametri possono essere passati costruttore toohello actor dal servizio hello stesso. il risultato di Hello è che gli attori possono essere costruiti in uno stato parzialmente inizializzata da altri metodi vengono chiamati su di esso, tempo di hello se attore hello richiede parametri di inizializzazione da client hello. Non è presente alcun singolo punto di ingresso per l'attivazione di un attore da client hello hello.
* Sebbene Reliable Actors creare in modo implicito oggetti attore. è hello possibilità tooexplicitly eliminare un attore e il relativo stato.

### <a name="distribution-and-failover"></a>Distribuzione e failover
tooprovide scalabilità e affidabilità, Service Fabric distribuisce gli attori in tutto il cluster hello e automaticamente consente di migrare da nodi con errori toohealthy quelli come richiesto. Questa è un'astrazione su un [Reliable Service partizionato con stato](service-fabric-concepts-partitioning.md). Distribuzione, la scalabilità, affidabilità e il failover automatico vengono forniti in virtù dei fatti hello attori in esecuzione all'interno di un servizio affidabile con stato chiamato hello *servizio Actor*.

Le partizioni siano distribuite in nodi hello in un cluster di Service Fabric attori vengono distribuiti tra partizioni hello di hello servizio Actor. Ogni partizione del servizio contiene un set di attori. Service Fabric gestisce la distribuzione e il failover delle partizioni servizio hello.

Ad esempio, un servizio actor con nove partizioni distribuiti vengono distribuiti i nodi utilizzando il posizionamento di partizione hello predefinito attore thusly toothree:

![Distribuzione di Reliable Actors][2]

Hello attore Framework gestisce le impostazioni di intervallo dello schema e la chiave di partizione per l'utente. In tal modo la scelta è più semplice, ma occorre tenere presente alcune considerazioni:

* Servizi affidabili consente toochoose uno schema di partizionamento, l'intervallo di chiavi (quando si usa un intervallo di schema di partizionamento) e il numero di partizione. Reliable Actors è schema di partizionamento toohello limitato intervallo (schema Int64 uniforme hello) e richiede l'utilizzo di hello completo Int64 intervalli di chiavi.
* Per impostazione predefinita, gli attori vengono posizionati in modo casuale nelle partizioni, in modo che la distribuzione risulti uniforme.
* Poiché gli attori vengono posizionati in modo casuale, è prevedibile che le operazioni dell'attore richiedano sempre la comunicazione di rete, incluse la serializzazione e deserializzazione dei dati di chiamata del metodo, la latenza riscontrata e il sovraccarico.
* In scenari avanzati, è la selezione di partizione attore toocontrol possibili con attore Int64 ID che eseguono il mapping delle partizioni toospecific. Questo metodo può tuttavia comportare una distribuzione sbilanciata degli attori tra le partizioni.

Per ulteriori informazioni sulla modalità di partizionamento servizi actor di, vedere troppo[partizionamento concetti per attori](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

### <a name="actor-communication"></a>Comunicazione tra attori
Interazioni attore sono definite in un'interfaccia che viene condiviso da attore hello che implementa l'interfaccia hello e hello client che consente di ottenere un proxy attore tooan tramite hello stessa interfaccia. Poiché questa interfaccia è utilizzata tooinvoke attore metodi in modo asincrono, ogni metodo nell'interfaccia hello deve essere restituzione di attività.

Chiamate ai metodi e le relative risposte implicano, in richieste di rete tra cluster hello, argomenti hello in tal caso e tipi di risultati hello delle attività hello che restituiscono deve essere serializzabile dalla piattaforma hello. In particolare, devono essere [contratto dati serializzabili](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

#### <a name="hello-actor-proxy"></a>proxy attore Hello
API client di Reliable Actors Hello fornisce la comunicazione tra un'istanza di attore e un client attore. toocommunicate con un attore, un client crea un oggetto proxy attore che implementa l'interfaccia di hello attore. client Hello interagisce con attore hello per richiamare metodi su oggetti proxy hello. proxy attore Hello è utilizzabile per la comunicazione client-a-attore e attore-a-attore.

```csharp
// Create a randomly distributed actor ID
ActorId actorId = ActorId.CreateRandom();

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
IMyActor myActor = ActorProxy.Create<IMyActor>(actorId, new Uri("fabric:/MyApp/MyActorService"));

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
await myActor.DoWorkAsync();
```

```java
// Create actor ID with some name
ActorId actorId = new ActorId("Actor1");

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
MyActor myActor = ActorProxyBase.create(actorId, new URI("fabric:/MyApp/MyActorService"), MyActor.class);

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
myActor.DoWorkAsync().get();
```


Si noti che i tipi di informazioni hello due utilizzato oggetto proxy attore di hello toocreate sono hello attore ID e nome dell'applicazione hello. ID attore Hello identifica in modo univoco l'attore hello, mentre il nome dell'applicazione hello identifica hello [applicazione di Service Fabric](service-fabric-reliable-actors-platform.md#application-model) in cui è distribuito attore hello.

Hello `ActorProxy`(c#) o `ActorProxyBase`classe (linguaggio) sul lato client hello esegue attore di hello risoluzione necessarie toolocate hello dall'ID e aprire un canale di comunicazione con esso. Effettua inoltre attore hello toolocate nei casi di hello di errori di comunicazione e di failover. Di conseguenza, il recapito dei messaggi è hello seguenti caratteristiche:

* Il recapito del messaggio è il massimo sforzo.
* Gli attori possono ricevere messaggi duplicati da hello client stesso.

### <a name="concurrency"></a>Concorrenza
Hello Reliable Actors runtime fornisce un modello di accesso basato su semplice per accedere ai metodi attore. Ciò significa che, in qualsiasi momento, all'interno del codice oggetto dell'attore non può essere attivo più di un thread. L'accesso a turno semplifica notevolmente i sistemi simultanei, poiché non occorrono meccanismi di sincronizzazione per l'accesso ai dati. Significa anche i sistemi devono essere progettati con considerazioni relative alla natura a thread singolo accesso hello di ogni istanza attore.

* Un'istanza di un solo attore non può elaborare più di una richiesta alla volta. Un'istanza di attore può causare un collo di bottiglia della velocità effettiva in caso di richieste simultanee toohandle previsto.
* Gli attori possono causare un deadlock tra loro se esiste una richiesta circolare tra due attori durante una richiesta esterna è tooone degli attori hello contemporaneamente. Hello attore runtime verrà automaticamente una volta sulla attore chiama e generare un toointerrupt chiamante di eccezione toohello situazione di blocco critico.

![Comunicazioni di Reliable Actors][3]

#### <a name="turn-based-access"></a>Accesso basato su turni
Una volta è costituito da hello esecuzione completa di un metodo attore nella richiesta tooa risposta da un client o altri attori o completare l'esecuzione hello di un [timer/promemoria](service-fabric-reliable-actors-timers-reminders.md) callback. Anche se questi metodi e i callback asincroni, il runtime di attori hello non interleave. Un turno deve essere interamente completato prima che sia consentito un nuovo turno. In altre parole, un callback di metodo o timer/promemoria attore attualmente in esecuzione deve essere completamente terminato prima di un nuovo metodo di chiamata tooa o callback è consentito. Un metodo o il callback viene considerato toohave completata se l'esecuzione di hello ha restituito dal metodo hello o di completamento dell'attività di callback e hello restituito dal metodo hello o un callback. È opportuno sottolineare che la concorrenza basata su turni viene rispettata anche su metodi, timer e callback diversi.

runtime attori Hello impone concorrenza basato su acquisendo un blocco actor all'inizio di hello di una volta e attivare il rilascio blocco hello alla fine hello hello. Pertanto, la concorrenza basata su turni viene applicata a livello di singolo attore e non per più attori. I metodi e i callback di timer/promemoria degli attori possono essere eseguiti simultaneamente per conto di diversi attori.

Hello di esempio seguente viene illustrato hello sopra i concetti. Si consideri un tipo di attore che implementa due metodi asincroni, ad esempio *Method1* e *Method2*, un timer e un promemoria. diagramma di Hello seguente viene illustrato un esempio di una sequenza temporale per l'esecuzione di hello di questi metodi e i callback per conto di due attori (*ActorId1* e *ActorId2*) che appartengono toothis attore tipo.

![Accesso e concorrenza basata su turni del runtime di Reliable Actors][1]

Il diagramma adotta queste convenzioni:

* Ogni linea verticale mostra il flusso logico hello dell'esecuzione di un metodo o un callback per conto dell'attore un particolare.
* gli eventi di Hello contrassegnati su ogni linea verticale si verificano in ordine cronologico, con gli eventi più recenti che si verificano di sotto di quelle meno recenti.
* Vengono utilizzati colori diversi per le sequenze temporali corrispondenti toodifferent attori.
* Evidenziazione è durata hello tooindicate utilizzato per la quale hello actor blocco per conto di un metodo o un callback.

Tooconsider alcuni punti importanti:

* Mentre *Method1* è in esecuzione per conto di *ActorId2* nella richiesta di risposta tooclient *xyz789*, un'altra richiesta del client (*abc123*) arriva che richiede inoltre *Method1* toobe eseguito da *ActorId2*. Tuttavia, hello seconda esecuzione di *Method1* non viene avviato finché termina l'esecuzione precedente hello. Analogamente, un promemoria registrata da *ActorId2* generato durante *Method1* viene eseguito nella richiesta di risposta tooclient *xyz789*. Hello callback promemoria viene eseguita solo dopo che entrambe le esecuzioni di *Method1* sono state completate. Tutte queste operazioni a causa della concorrenza basata su tooturn viene applicata per *ActorId2*.
* Analogamente, basato su concorrenza viene anche applicata per *ActorId1*, come illustrato dall'esecuzione hello *Method1*, *Method2*, e hello callback del timer per conto di *ActorId1* il problema in modo seriale.
* L'esecuzione di *Method1* per conto di *ActorId1* si sovrappone all'esecuzione per conto di *ActorId2*. Questo accade perché la concorrenza basata su turni viene applicata solo all'interno di un attore e non tra più attori.
* In alcune delle esecuzioni di metodo/callback hello, hello `Task`(c#) o `CompletableFuture`(linguaggio) restituito da hello metodo/callback termina una volta completato il metodo hello. In alcuni altri, operazione asincrona di hello è già terminata dal tempo hello hello metodo/callback restituisce. In entrambi i casi, hello actor viene sbloccata solo dopo che entrambi hello metodo/callback restituisce e completamento dell'operazione asincrona di hello.

#### <a name="reentrancy"></a>Rientranza
il runtime di attori Hello consente reentrancy per impostazione predefinita. Questo significa che se un metodo attore *attore A* chiama un metodo su *attore B*, che a sua volta chiama un altro metodo in *attore A*, che metodo è consentito toorun. Infatti, fa parte di hello stesso contesto logico della catena di chiamate. Tutte le chiamate timer e promemoria iniziano con il nuovo contesto di chiamata logico hello. Vedere hello [reentrancy Reliable Actors](service-fabric-reliable-actors-reentrancy.md) per altri dettagli.

#### <a name="scope-of-concurrency-guarantees"></a>Ambito delle garanzie di concorrenza
il runtime di attori Hello fornisce le garanzie di concorrenza in situazioni in cui tale vincolo controlla chiamata hello di questi metodi. Ad esempio, fornisce le garanzie hello nelle chiamate ai metodi che viene eseguite nella richiesta client tooa di risposta, nonché per i callback del timer e promemoria. Tuttavia, se codice attore hello richiama direttamente questi metodi di fuori di meccanismi di hello forniti dal runtime di attori hello, hello runtime non fornisce alcuna garanzia di concorrenza. Ad esempio, se il metodo hello viene richiamato nel contesto di hello di alcune attività che non sia associata con attività hello restituiti dai metodi attore hello, hello runtime non fornisce garanzie di concorrenza. Se il metodo hello viene richiamato da un thread in tale attore hello crea autonomamente, quindi hello runtime non può anche fornire le garanzie di concorrenza. Pertanto, le operazioni in background tooperform, attori devono utilizzare [timer attore e i promemoria attore](service-fabric-reliable-actors-timers-reminders.md) che rispettano concorrenza basata su attiva.

## <a name="next-steps"></a>Passaggi successivi
* Per iniziare, creare il primo servizio Reliable Actors:
   * [Introduzione a Reliable Actors in .NET](service-fabric-reliable-actors-get-started.md)
   * [Introduzione a Reliable Actors in Java](service-fabric-reliable-actors-get-started-java.md)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-introduction/concurrency.png
[2]: ./media/service-fabric-reliable-actors-introduction/distribution.png
[3]: ./media/service-fabric-reliable-actors-introduction/actor-communication.png
