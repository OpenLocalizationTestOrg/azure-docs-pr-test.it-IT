---
title: Creare la prima applicazione di Service Fabric in C# | Microsoft Docs
description: "Introduzione alla creazione di un’applicazione dell’infrastruttura di servizi di Microsoft Azure con i servizi con e senza stato."
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
ms.openlocfilehash: 813021d6239ae3cf79bb84b78f77e39c9e0783f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-reliable-services"></a>Introduzione a Reliable Services
> [!div class="op_single_selector"]
> * [C# su Windows](service-fabric-reliable-services-quick-start.md)
> * [Java su Linux](service-fabric-reliable-services-quick-start-java.md)
> 
> 

Un'applicazione di Azure Service Fabric contiene uno o più servizi che consentono l'esecuzione del codice. Questa guida illustra come creare applicazioni di Service Fabric con e senza stato con i servizi [Reliable Services](service-fabric-reliable-services-introduction.md).  Questo video di Microsoft Virtual Academy illustra anche come creare un servizio Reliable Services senza stato: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>Concetti di base
Per iniziare a usare Reliable Services, è sufficiente comprendere solo alcuni concetti di base:

* **Tipo di servizio**: si tratta dell'implementazione del servizio. Viene definito dalla classe scritta che estende `StatelessService` e qualsiasi altro codice o dipendenze usate, insieme al nome e al numero della versione.
* **Istanza di servizio denominata**: per eseguire il servizio, si creano le istanze denominate del tipo di servizio, analogamente al modo in cui si creano le istanze di un oggetto di un tipo di classe. Il formato del nome di un'istanza del servizio è un URI che usa lo schema "fabric:/", ad esempio "fabric:/MyApp/MyService".
* **Host del servizio**: le istanze del servizio denominate che si creano devono essere eseguite in un processo host. L'host del servizio è semplicemente un processo in cui eseguire le istanze del servizio.
* **Registrazione del servizio**: la registrazione raccoglie tutti gli elementi. Il tipo di servizio deve essere registrato con il runtime di Service Fabric in un host del servizio per consentire a Service Fabric di creare istanze per l'esecuzione.  

## <a name="create-a-stateless-service"></a>Creare un servizio senza stato
Il servizio senza stato è il tipo di servizio di norma presente nelle applicazioni cloud. Viene considerato senza stato perché il servizio stesso non contiene dati che devono essere archiviati in modo affidabile o resi a disponibilità elevata. Se un'istanza di un servizio senza stato si arresta, il relativo stato interno viene perso. In questi tipi di servizio lo stato deve essere reso persistente mediante un archivio esterno, ad esempio tabelle di Azure o un database SQL, in modo da assicurare elevata disponibilità e affidabilità.

Avviare Visual Studio 2015 o Visual Studio 2017 come amministratore e creare un nuovo progetto di applicazione di Service Fabric denominato *HelloWorld*:

![Uso della finestra di dialogo New Project per creare una nuova applicazione di Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

Creare quindi un progetto di servizio senza stato denominato *HelloWorldStateless*:

![Nella seconda finestra di dialogo creare un progetto di servizio senza stato](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

La soluzione ora contiene due progetti:

* *HelloWorld*. Si tratta del progetto *applicazione* contenente i *servizi*. Il progetto contiene anche il manifesto dell'applicazione che descrive l'applicazione stessa, oltre ad alcuni script di PowerShell che consentono di distribuirla.
* *HelloWorldStateless*. Si tratta del progetto di servizio. Il progetto contiene l'implementazione del servizio senza stato.

## <a name="implement-the-service"></a>Implementare il servizio
Aprire il file **HelloWorldStateless.cs** nel progetto del servizio. In Service Fabric un servizio può eseguire qualsiasi tipo di logica di business. L'API del servizio fornisce due punti di ingresso per il codice:

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

Questa esercitazione si concentra sul metodo del punto di ingresso `RunAsync()` . In questo punto è possibile iniziare immediatamente a eseguire il codice.
Il modello di progetto include un esempio di implementazione di `RunAsync()` che gestisce un conteggio incrementale.

> [!NOTE]
> Per informazioni dettagliate sull'uso di uno stack di comunicazione, vedere [Introduzione ai servizi API Web di Microsoft Azure Service Fabric con self-hosting OWIN](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>RunAsync
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
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

La piattaforma chiama questo metodo quando si inserisce un'istanza di un servizio pronta per l'esecuzione. Per un servizio senza stato, la piattaforma chiama il metodo quando l'istanza del servizio viene aperta. Viene fornito un token di annullamento che determina quando è necessario chiudere l'istanza del servizio. In Service Fabric questo ciclo di apertura e chiusura di un'istanza del servizio può verificarsi più volte per tutta la durata del servizio nel suo complesso. Questa situazione può verificarsi per vari motivi, tra cui:

* Il sistema sposta le istanze del servizio per il bilanciamento delle risorse.
* Si verificano errori nel codice.
* Viene aggiornato il sistema o l'applicazione.
* Si verifica un'interruzione nell'hardware sottostante.

Questa orchestrazione viene gestita dal sistema per assicurare l'elevata disponibilità e il corretto bilanciamento del servizio.

`RunAsync()` non deve bloccarsi in modo sincrono. L'implementazione di RunAsync deve restituire un'attività o restare in attesa in caso di operazioni a esecuzione prolungata oppure bloccate, per consentire al runtime di continuare. Si noti che nel ciclo `while(true)` dell'esempio precedente viene usato `await Task.Delay()` per la restituzione di un'attività. Se il carico di lavoro si deve bloccare in modo sincrono, è opportuno pianificare una nuova Task con `Task.Run()` nell'implementazione `RunAsync`.

L'annullamento del carico di lavoro è un'operazione cooperativa coordinata dal token di annullamento fornito. Il sistema attende la fine dell'attività (per esito positivo, annullamento o errore) prima di continuare. È importante rispettare il token di annullamento, completare le operazioni e chiudere `RunAsync()` il più rapidamente possibile quando viene richiesto l'annullamento dal sistema.

In questo esempio di servizio senza stato il conteggio è archiviato in una variabile locale. Tuttavia, poiché si tratta di un servizio senza stato, il valore archiviato esiste soltanto per il ciclo di vita corrente dell'istanza del servizio. Quando si posta o si riavvia il servizio, il valore viene perso.

## <a name="create-a-stateful-service"></a>Creare un servizio con stato
Service Fabric introduce un nuovo tipo di servizio con stato. Un servizio con stato può mantenere lo stato affidabile all'interno del servizio stesso, con percorso condiviso con il codice che lo usa. L'elevata disponibilità dello stato è assicurata da Service Fabric, senza dover rendere persistente lo stato mediante un archivio esterno.

Per convertire un valore del contatore da senza stato a elevata disponibilità e persistenza anche quando il servizio viene spostato o riavviato, è necessario un servizio con stato.

Nella stessa applicazione *HelloWorld* aggiungere un nuovo servizio facendo clic con il pulsante destro del mouse sui riferimenti ai servizi nel progetto applicazione e selezionare **Aggiungi -> Nuovo servizio Service Fabric**.

![Aggiungere un servizio all'applicazione di Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

Selezionare **Stateful Service** e assegnare il nome *HelloWorldStateful*. Fare clic su **OK**.

![Uso della finestra di dialogo New Project per creare un nuovo servizio di Service Fabric con stato](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

A questo punto l'applicazione ha due servizi: il servizio senza stato *HelloWorldStateless* e il servizio con stato *HelloWorldStateful*.

Un servizio con stato ha gli stessi punti di ingresso di un servizio senza stato. La differenza principale è data dalla disponibilità di un *provider di stato* che può archiviare lo stato in modo affidabile. Service Fabric include un'implementazione del provider di stato denominata [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), che permette di creare strutture di dati replicate tramite Reliable State Manager. Un servizio Reliable Services con stato usa questo provider di stato per impostazione predefinita.

Aprire **HelloWorldStateful.cs** in *HelloWorldStateful*che contiene il metodo RunAsync seguente:

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
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

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>RunAsync
`RunAsync()` funziona in modo simile sia nei servizi con stato che nei servizi senza stato. In un servizio con stato la piattaforma esegue tuttavia operazioni aggiuntive per conto dell'utente prima di eseguire `RunAsync()`. Tali operazioni possono includere la verifica che Reliable State Manager e Reliable Collections siano pronti per l'uso.

### <a name="reliable-collections-and-the-reliable-state-manager"></a>Reliable Collections e Reliable State Manager
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) è un'implementazione di dizionario che permette di archiviare in modo affidabile lo stato nel servizio. Grazie a Service Fabric e alle raccolte Reliable Collections è possibile archiviare i dati direttamente nel servizio, senza la necessità di un archivio esterno persistente. Le raccolte Reliable Collections garantiscono la disponibilità elevata dei dati. A tale scopo, Service Fabric crea e gestisce automaticamente più *repliche* del servizio. Offre anche un'API che consente di evitare le complessità di gestione di tali repliche e delle relative transizioni di stato.

Le raccolte Reliable Collections possono archiviare qualsiasi tipo .NET, inclusi quelli personalizzati, con alcuni avvertimenti:

* Service Fabric garantisce la disponibilità elevata dello stato *replicando* lo stato nei nodi, mentre Reliable Collections archivia i dati nel disco locale a ogni replica. Questo significa che tutti gli elementi archiviati in Reliable Collections devono essere *serializzabili*. Per impostazione predefinita, le raccolte Reliable Collections usano [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) per la serializzazione. Quando si usa il serializzatore predefinito, è quindi importante assicurarsi che i tipi siano [supportati dal serializzatore dei contratti dati](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx).
* Quando si esegue il commit di transazioni nelle raccolte Reliable Collections, gli oggetti vengono replicati per assicurare disponibilità elevata. Gli oggetti archiviati nelle raccolte Reliable Collections vengono conservati nella memoria locale del servizio. Ciò significa che è presente un riferimento locale all'oggetto.
  
   È importante non apportare modifiche alle istanze locali degli oggetti senza prima eseguire un'operazione di aggiornamento sulla raccolta Reliable Collections in una transazione. Le modifiche apportate alle istanze locali di oggetti, infatti, non vengono replicate automaticamente. È necessario inserire nuovamente l'oggetto nel dizionario oppure usare uno dei metodi di *aggiornamento* nel dizionario.

Reliable State Manager gestisce automaticamente le raccolte Reliable Collections. In qualunque momento e in qualsiasi posizione del servizio è possibile chiedere a Reliable State Manager una raccolta Reliable Collections indicandone il nome. Reliable State Manager restituirà un riferimento. Non si consiglia di salvare riferimenti alle istanze di raccolte Reliable Collections in proprietà o variabili membri di classe. Prestare particolare attenzione per assicurarsi che il riferimento sia sempre impostato su un'istanza durante il ciclo di vita del servizio. Reliable State Manager gestisce queste operazioni automaticamente ed è ottimizzato per le visite ripetute.

### <a name="transactional-and-asynchronous-operations"></a>Operazioni transazionali e asincrone
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

Le raccolte Reliable Collections includono molte delle operazioni corrispondenti di `System.Collections.Generic` e `System.Collections.Concurrent`, tranne LINQ. Le operazioni sulle raccolte Reliable Collections sono asincrone. Questo avviene perché le operazioni di scrittura sulle raccolte Reliable Collections eseguono operazioni di I/O per replicare e rendere persistenti i dati su disco.

Le operazioni sulle raccolte Reliable Collections sono *transazionali*e consentono di mantenere lo stato coerente tra più raccolte Reliable Collections e operazioni. Ad esempio, è possibile rimuovere un elemento di lavoro da un oggetto ReliableQueue, eseguire un'operazione su tale elemento e salvare il risultato in un oggetto ReliableDictionary, il tutto all'interno di una singola transazione. Questa viene considerata come un'operazione atomica e garantisce la riuscita o il rollback dell'intera operazione. Se si verifica un errore dopo aver rimosso l'elemento dalla coda ma prima di aver salvato il risultato, viene eseguito il rollback dell'intera transazione e l'elemento rimane nella coda per l'elaborazione.

## <a name="run-the-application"></a>Eseguire l'applicazione
Tornare all'applicazione *HelloWorld* . È ora possibile compilare e distribuire i servizi. Quando si preme **F5**, l'applicazione viene compilata e distribuita nel cluster locale.

Dopo l'avvio dell'esecuzione dei servizi, è possibile visualizzare gli eventi generati di Event Tracing for Windows (ETW) in una finestra **Eventi di diagnostica** . Si noti che gli eventi visualizzati nell'applicazione provengono sia dal servizio senza stato sia dal servizio con stato. È possibile sospendere il flusso facendo clic sul pulsante **Pausa** . Espandendo un messaggio è possibile esaminarne i dettagli.

> [!NOTE]
> Prima di eseguire l'applicazione, assicurarsi di avere un cluster di sviluppo locale in esecuzione. Per informazioni sulla configurazione dell'ambiente locale, vedere la [guida introduttiva](service-fabric-get-started.md) .
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

