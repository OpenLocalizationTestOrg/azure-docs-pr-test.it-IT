---
title: aaaCreate la prima applicazione di Service Fabric in c# | Documenti Microsoft
description: Introduzione toocreating un'applicazione di Microsoft Azure Service Fabric con servizi senza stato.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Introduzione a Reliable Services
> [!div class="op_single_selector"]
> * [C# su Windows](service-fabric-reliable-services-quick-start.md)
> * [Java su Linux](service-fabric-reliable-services-quick-start-java.md)
> 
> 

Un'applicazione di Azure Service Fabric contiene uno o più servizi che consentono l'esecuzione del codice. Questa guida illustra come toocreate state e senza applicazioni di Service Fabric con [servizi affidabili](service-fabric-reliable-services-introduction.md).  In questo video Microsoft Virtual Academy illustra anche come un servizio Reliable senza stato toocreate:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>Concetti di base
tooget avviato con servizi affidabili, è solo necessario toounderstand alcuni concetti di base:

* **Tipo di servizio**: si tratta dell'implementazione del servizio. È definito dalla classe hello è scrivere che estende `StatelessService` e qualsiasi altro codice o dipendenze al suo interno, utilizzate insieme a un nome e un numero di versione.
* **Istanza di servizio denominata**: toorun il servizio, si creano le istanze denominate del tipo di servizio, molto come si creano istanze di un oggetto di un tipo classe. Un'istanza del servizio ha un nome in formato hello di un URI usando hello "fabric: /" dello schema, ad esempio "fabric: / MyApp/MyService".
* **Host del servizio**: hello denominata è necessario toorun all'interno di un processo host di creare istanze del servizio. host del servizio Hello è semplicemente un processo in cui è possono eseguire le istanze del servizio.
* **Registrazione del servizio**: la registrazione raccoglie tutti gli elementi. Hello tipo di servizio deve essere registrato con hello Service Fabric runtime in un servizio host tooallow Service Fabric toocreate istanze toorun.  

## <a name="create-a-stateless-service"></a>Creare un servizio senza stato
Un servizio senza stato è un tipo di servizio che è attualmente norm hello nelle applicazioni cloud. Viene considerato senza stato servizio hello stesso contiene dati che devono essere toobe archiviati in modo affidabile o reso a disponibilità elevata. Se un'istanza di un servizio senza stato si arresta, il relativo stato interno viene perso. In questo tipo di servizio, lo stato deve essere archivio esterno tooan persistente, ad esempio le tabelle di Azure o un database SQL, per tale toobe apportate a elevata disponibilità e affidabilità.

Avviare Visual Studio 2015 o Visual Studio 2017 come amministratore e creare un nuovo progetto di applicazione di Service Fabric denominato *HelloWorld*:

![Utilizzare toocreate finestra di dialogo Nuovo progetto hello una nuova applicazione di Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

Creare quindi un progetto di servizio senza stato denominato *HelloWorldStateless*:

![Nella finestra di dialogo hello secondo creare un progetto di servizio senza stato](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

La soluzione ora contiene due progetti:

* *HelloWorld*. Si tratta di hello *applicazione* progetto che contiene il *servizi*. Contiene inoltre il manifesto dell'applicazione hello che descrive l'applicazione hello, nonché un numero di script di PowerShell che consentono di toodeploy l'applicazione.
* *HelloWorldStateless*. Questo è il progetto di servizio hello. Contiene l'implementazione del servizio senza stato hello.

## <a name="implement-hello-service"></a>Implementare il servizio hello
Aprire hello **HelloWorldStateless.cs** file nel progetto di servizio hello. In Service Fabric un servizio può eseguire qualsiasi tipo di logica di business. API del servizio Hello fornisce due punti di ingresso per il codice:

* Un metodo del punto di ingresso aperto denominato *RunAsync*, che consente di iniziare a eseguire qualsiasi carico di lavoro, inclusi carichi di lavoro di calcolo con esecuzione prolungata.

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* Un punto di ingresso di comunicazione a cui è possibile collegare lo stack di comunicazione desiderato, come ASP.NET Core. In questo punto è possibile iniziare a ricevere richieste da utenti e da altri servizi.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

In questa esercitazione, esamineremo hello `RunAsync()` metodo punto di ingresso. In questo punto è possibile iniziare immediatamente a eseguire il codice.
il modello di progetto di Hello include un esempio di implementazione di `RunAsync()` che incrementa il numero di sequenza.

> [!NOTE]
> Per informazioni dettagliate su come toowork con una comunicazione stack, vedere [servizi API Web dell'infrastruttura del servizio con self-hosting OWIN](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>RunAsync
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

piattaforma Hello chiama questo metodo quando un'istanza di un servizio è tooexecute posizionato ed è pronto. Per un servizio senza stato, che indica semplicemente quando viene aperto l'istanza del servizio hello. Un token di annullamento viene fornito toocoordinate quando l'istanza del servizio deve toobe chiuso. In Service Fabric, questo ciclo di apertura o chiusura di un'istanza del servizio può verificarsi più volte nel ciclo di vita di hello del servizio hello nel suo complesso. Questa situazione può verificarsi per vari motivi, tra cui:

* sistema di Hello sposta le istanze del servizio di bilanciamento delle risorse.
* Si verificano errori nel codice.
* un'applicazione Hello o sistema viene aggiornato.
* hardware sottostante Hello di cui si verifichi un'interruzione del servizio.

Questa orchestrazione è gestita da hello sistema tookeep il servizio a disponibilità elevata e bilanciato in modo corretto.

`RunAsync()` non deve bloccarsi in modo sincrono. L'implementazione di RunAsync deve restituire un'attività o await in qualsiasi runtime toocontinue di operazioni a esecuzione prolungata o blocco tooallow hello. Nota in hello `while(true)` ciclo nell'esempio precedente hello, restituzione attività `await Task.Delay()` viene utilizzato. Se il carico di lavoro si deve bloccare in modo sincrono, è opportuno pianificare una nuova Task con `Task.Run()` nell'implementazione `RunAsync`.

Annullamento del carico di lavoro è un lavoro cooperativo orchestrato da hello fornito token di annullamento. sistema Hello attenderà per l'attività tooend (per il completamento, annullamento o errore) prima di spostare. È importante toohonor hello annullamento token, termina qualsiasi lavoro e chiudere `RunAsync()` più rapidamente possibile quando il sistema hello richiede l'annullamento.

In questo esempio di servizio senza stato, il conteggio di hello è archiviato in una variabile locale. Ma, poiché si tratta di un servizio senza stato, il valore hello archiviato esiste solo per hello corrente del ciclo di vita dell'istanza del servizio. Quando il servizio hello viene spostato o viene riavviato, il valore di hello viene perso.

## <a name="create-a-stateful-service"></a>Creare un servizio con stato
Service Fabric introduce un nuovo tipo di servizio con stato. Un servizio con stato consente di mantenere lo stato in modo affidabile all'interno del servizio di hello, posizionato insieme ad codice hello in uso è. Lo stato è a disponibilità elevata grazie Service Fabric senza hello necessità toopersist tooan esterna l'archivio dello stato.

tooconvert un valore del contatore da toohighly senza stato persistente e disponibile, anche quando il servizio hello viene spostato o viene riavviato, è necessario un servizio con stato.

In hello stesso *HelloWorld* applicazione, è possibile aggiungere un nuovo servizio facendo clic su riferimenti a servizi di hello in progetto di applicazione hello e selezionando **Aggiungi -> nuovo servizio Service Fabric**.

![Aggiungere un tooyour servizio applicazione di Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

Selezionare **Stateful Service** e assegnare il nome *HelloWorldStateful*. Fare clic su **OK**.

![Utilizzare toocreate casella di dialogo Nuovo progetto hello un nuovo servizio con stato di Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

A questo punto l'applicazione deve disporre di due servizi: hello servizio senza stato *HelloWorldStateless* e il servizio con stato hello *HelloWorldStateful*.

Hello dispone di un servizio con stato punti di ingresso stesso come un servizio senza stato. la differenza principale Hello è hello di disponibilità di un *provider di stato* che possono archiviare lo stato in modo affidabile. Infrastruttura del servizio viene fornito con un'implementazione del provider di stata chiamata [raccolte affidabile](service-fabric-reliable-services-reliable-collections.md), che consente di creare strutture dei dati replicati tramite hello affidabile di gestione dello stato. Un servizio Reliable Services con stato usa questo provider di stato per impostazione predefinita.

Aprire **HelloWorldStateful.cs** in *HelloWorldStateful*, che contiene hello RunAsync al metodo:

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>RunAsync
`RunAsync()` funziona in modo simile sia nei servizi con stato che nei servizi senza stato. Tuttavia, in un servizio con stato, la piattaforma hello esegue ulteriori operazioni per conto dell'utente prima di eseguire `RunAsync()`. Questa operazione può includere assicurandosi che hello affidabile di gestione dello stato e affidabile le raccolte sono toouse pronto.

### <a name="reliable-collections-and-hello-reliable-state-manager"></a>Affidabile raccolte e hello affidabile di gestione dello stato
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) è un'implementazione di dizionario, che è possibile utilizzare tooreliably archiviare lo stato del servizio hello. Con Service Fabric e raccolte affidabile, è possibile archiviare i dati direttamente nel servizio senza necessità di hello di un archivio permanente esterno. Le raccolte Reliable Collections garantiscono la disponibilità elevata dei dati. A tale scopo, Service Fabric crea e gestisce automaticamente più *repliche* del servizio. Fornisce inoltre un'API che astrae complessità di stoccaggio hello della gestione di tali repliche e le transizioni di stato.

Le raccolte Reliable Collections possono archiviare qualsiasi tipo .NET, inclusi quelli personalizzati, con alcuni avvertimenti:

* Service Fabric rende lo stato a disponibilità elevata *replica* stato tra nodi e le raccolte affidabile archiviare disco toolocal dati in ogni replica. Questo significa che tutti gli elementi archiviati in Reliable Collections devono essere *serializzabili*. Per impostazione predefinita, utilizzare le raccolte affidabile [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) per la serializzazione, è importante toomake assicurarsi che i tipi siano [supportati dal serializzatore dei contratti dati hello](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) quando si utilizza l'impostazione predefinita hello serializzatore.
* Quando si esegue il commit di transazioni nelle raccolte Reliable Collections, gli oggetti vengono replicati per assicurare disponibilità elevata. Gli oggetti archiviati nelle raccolte Reliable Collections vengono conservati nella memoria locale del servizio. Ciò significa che si disponga di un oggetto toohello riferimento locale.
  
   È importante non modificare le istanze locali di tali oggetti senza eseguire un'operazione di aggiornamento nella raccolta affidabile di hello in una transazione. Questo avviene perché le modifiche toolocal istanze di oggetti non verranno replicate automaticamente. È necessario inserire nuovamente oggetto hello nel dizionario di hello o utilizzare uno dei hello *aggiornare* metodi nel dizionario di hello.

Hello affidabile di gestione dello stato gestisce raccolte affidabile per l'utente. È possibile semplicemente chiedere hello affidabile di gestione dello stato per un insieme affidabile in base al nome in qualsiasi momento e in qualsiasi punto del servizio. Hello affidabile di gestione dello stato consente di ottenere un riferimento nuovamente. Non è consigliabile salvare i riferimenti tooreliable raccolta istanze nelle variabili di membro di classe o proprietà. È necessario prestare particolare attenzione tooensure impostato riferimento hello tooan istanza sempre hello del ciclo di vita del servizio. Hello affidabile di gestione dello stato gestisce questo lavoro per l'utente ed è ottimizzato per tornino.

### <a name="transactional-and-asynchronous-operations"></a>Operazioni transazionali e asincrone
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

Raccolte affidabile hanno molte hello stesse operazioni che i relativi `System.Collections.Generic` e `System.Collections.Concurrent` corrispondenti, ad eccezione di LINQ. Le operazioni sulle raccolte Reliable Collections sono asincrone. In questo modo le operazioni di scrittura con le raccolte affidabile eseguono tooreplicate di operazioni dei / o e mantenere i dati toodisk.

Le operazioni sulle raccolte Reliable Collections sono *transazionali*e consentono di mantenere lo stato coerente tra più raccolte Reliable Collections e operazioni. Ad esempio, è possibile rimuovere dalla coda un elemento di lavoro da una coda affidabile, eseguire un'operazione su di esso e salvare hello risultato in un dizionario affidabile, tutti in un'unica transazione. Viene considerato come operazione atomica e garantisce che verrà completata l'intera operazione hello o verrà eseguito il rollback dell'intera operazione hello. Se si verifica un errore dopo che di rimozione dalla coda elemento hello ma prima di salvare i risultati di hello, viene eseguito il rollback dell'intera transazione hello e hello elemento rimane nella coda di hello per l'elaborazione.

## <a name="run-hello-application"></a>Eseguire un'applicazione hello
È ora restituire toohello *HelloWorld* dell'applicazione. È ora possibile compilare e distribuire i servizi. Quando si preme **F5**, l'applicazione sarà cluster locale tooyour compilato e distribuito.

Dopo l'esecuzione dei servizi hello, è possibile visualizzare gli eventi Event Tracing for Windows (ETW) hello generato in un **gli eventi di diagnostica** finestra. Si noti che gli eventi di hello visualizzati dal servizio senza stato hello sia il servizio con stato di hello in un'applicazione hello. È possibile sospendere un flusso di hello facendo hello **sospendere** pulsante. È quindi possibile esaminare i dettagli di hello di un messaggio espandendo tale messaggio.

> [!NOTE]
> Prima di eseguire un'applicazione hello, assicurarsi di disporre di un cluster di sviluppo locale che esegue. Estrarre hello [Guida introduttiva](service-fabric-get-started.md) per informazioni su come configurare l'ambiente locale.
> 
> 

![Visualizzare gli eventi di diagnostica in Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a>Passaggi successivi
[Debug dell'applicazione di Service Fabric in Visual Studio](service-fabric-debugging-your-application.md)

[Introduzione ai servizi API Web di Service Fabric con self-hosting OWIN](service-fabric-reliable-services-communication-webapi.md)

[Reliable Collections](service-fabric-reliable-services-reliable-collections.md)

[Distribuire un'applicazione](service-fabric-deploy-remove-applications.md)

[Aggiornamento dell'applicazione](service-fabric-application-upgrade.md)

[Guida di riferimento per gli sviluppatori per Reliable Services](https://msdn.microsoft.com/library/azure/dn706529.aspx)

