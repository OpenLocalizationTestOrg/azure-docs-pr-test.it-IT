---
title: aaaCreate il primo microservizio Azure basato su attori in c# | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello di creazione, il debug e distribuzione di un servizio basato su attori semplice usando Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Introduzione a Reliable Actors
> [!div class="op_single_selector"]
> * [C# su Windows](service-fabric-reliable-actors-get-started.md)
> * [Java su Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

In questo articolo vengono illustrati concetti fondamentali di hello di Azure Service Fabric Reliable Actors e viene illustrata la creazione, il debug e distribuzione di un'applicazione semplice Reliable Actor in Visual Studio.

## <a name="installation-and-setup"></a>Installazione e configurazione
Prima di iniziare, assicurarsi di disporre dell'ambiente di sviluppo di Service Fabric hello configurare nel computer.
Se è necessario tooset, configurarlo, vedere le istruzioni dettagliate sulla [come tooset hello ambiente di sviluppo](service-fabric-get-started.md).

## <a name="basic-concepts"></a>Concetti di base
tooget introduttiva Reliable Actors, è solo necessario toounderstand alcuni concetti di base:

* **Servizio attore**. Reliable Actors sono inclusi nei servizi affidabili che può essere distribuito nell'infrastruttura di Service Fabric hello. Le istanze di Actors vengono attivate in un'istanza del servizio denominata.
* **Registrazione attore**. Come con i servizi affidabili, un servizio Reliable Actor deve toobe registrato con il runtime di Service Fabric hello. Inoltre, è necessario toobe registrato con il runtime di attore hello tipo attore hello.
* **Interfaccia attore**. interfaccia attore Hello è toodefine utilizzata un'interfaccia pubblica fortemente tipizzata di un attore. Nella terminologia dei modelli Reliable Actor hello, interfaccia attore hello definisce hello tipi di messaggi hello attore possono comprendere ed elaborare. interfaccia attore Hello viene utilizzato da altri attori e le applicazioni client troppo "inviano" (in modo asincrono) attore toohello messaggi. Reliable Actors può implementare più interfacce.
* **Classe ActorProxy**. classe ActorProxy Hello viene utilizzato da client applicazioni tooinvoke hello metodi esposti tramite l'interfaccia di hello attore. classe ActorProxy Hello offre due funzionalità importanti:
  
  * Risoluzione dei nomi: è in grado di toolocate attore di hello cluster hello (Trova hello nodo del cluster di hello in cui è ospitato).
  * Gestione degli errori: può ripetere chiamate al metodo e risolvere nuovamente il percorso di attore hello dopo, ad esempio, un errore che richiede hello attore toobe rilocato tooanother nodo cluster hello.

Hello alle regole che riguardano le interfacce tooactor è utile citare:

* I metodi di interfaccia dell'attore non possono essere sottoposti a overload.
* I metodi di interfaccia dell'attore non accettano parametri facoltativi, out o ref.
* Non sono supportate interfacce generiche.

## <a name="create-a-new-project-in-visual-studio"></a>Creare un nuovo progetto in Visual Studio
Avviare Visual Studio 2015 o Visual Studio 2017 come amministratore e creare un nuovo progetto di applicazione di Service Fabric:

![Strumenti di Service Fabric per Visual Studio - nuovo progetto][1]

In hello successiva finestra di dialogo, è possibile scegliere il tipo di hello del progetto che si desidera toocreate.

![Modelli di progetto di Service Fabric][5]

Per il progetto HelloWorld hello, utilizziamo servizio Service Fabric Reliable Actors hello.

Dopo aver creato la soluzione hello, dovrebbe essere hello seguente struttura:

![Struttura del progetto di Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a>Blocchi predefiniti di base di Reliable Actors
Una tipica soluzione Reliable Actors è costituita da tre progetti:

* **progetto di applicazione Hello (MyActorApplication)**. Si tratta di progetto di hello che tutti i servizi di hello insieme per la distribuzione di pacchetti. Contiene hello *ApplicationManifest.xml* e script di PowerShell per la gestione di un'applicazione hello.
* **progetto di interfaccia Hello (MyActor.Interfaces)**. Si tratta hello progetto che contiene la definizione di interfaccia hello per attore hello. Nel progetto MyActor.Interfaces hello, è possibile definire le interfacce di hello che verranno utilizzate da attori hello nella soluzione hello. Le interfacce attore possono essere definite in qualsiasi progetto con un nome qualsiasi, tuttavia l'interfaccia hello definisce contratto attore hello condiviso da implementazione attore hello e i client hello chiamata attore hello, pertanto è in genere senso toodefine in un assembly separare dall'implementazione attore hello e può essere condiviso da più altri progetti.

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **progetto del servizio actor Hello (MyActor)**. Si tratta di hello progetto utilizzato toodefine hello Service Fabric servizio che corso toohost hello attore. Contiene l'implementazione hello dell'attore hello. Un'implementazione attore è una classe che deriva dal tipo di base hello `Actor` e implementa hello interfacce che sono definita nel progetto MyActor.Interfaces hello. Una classe attore deve anche implementare un costruttore che accetta un `ActorService` istanza e un `ActorId` e li passa toohello base `Actor` classe. Ciò consente l'inserimento della dipendenza costruttore delle dipendenze della piattaforma.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

servizio actor Hello deve essere registrato con un tipo di servizio nel runtime di Service Fabric hello. Per consentire hello servizio Actor toorun le istanze di attore, il tipo di attore inoltre deve essere registrato con hello servizio Actor. Hello `ActorRuntime` metodo di registrazione, questa operazione viene eseguita per attori.

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Se si parte da un nuovo progetto in Visual Studio e si dispone di una sola definizione attore, registrazione hello è incluso per impostazione predefinita nel codice hello generato da Visual Studio. Se si definiscono altri attori nel servizio di hello, è necessario registrazione attore di hello tooadd utilizzando:

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> Hello attori di infrastruttura servizio runtime genera alcuni [gli eventi e contatori di prestazioni correlati metodi tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). che sono utili per la diagnostica e il monitoraggio delle prestazioni.
> 
> 

## <a name="debugging"></a>Debug
strumenti di Hello Service Fabric per Visual Studio supportano il debug sul computer locale. È possibile avviare una sessione di debug da hello che colpisce tasto F5. Visual Studio esegue, se necessario, la compilazione dei pacchetti Inoltre, consente di distribuire un'applicazione hello nel cluster di Service Fabric locale hello e collega il debugger hello.

Durante il processo di distribuzione di hello, è possibile visualizzare lo stato di avanzamento hello in hello **Output** finestra.

![Finestra di output del debug di Service Fabric][3]

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni, vedere [utilizzo di piattaforma Service Fabric hello Reliable Actors](service-fabric-reliable-actors-platform.md).

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
