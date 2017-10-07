---
title: front-end web per l'app di Azure Service Fabric usando ASP.NET Core aaaCreate | Documenti Microsoft
description: Esporre web Service Fabric applicazione toohello utilizzando un progetto ASP.NET Core e la comunicazione tra i servizi tramite comunicazione remota del servizio.
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
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a>Compilare un front-end di servizio Web per l'applicazione tramite ASP.NET Core
Per impostazione predefinita, i servizi di Azure Service Fabric non forniscono un web toohello interfaccia pubblica. tooexpose client tooHTTP di funzionalità dell'applicazione, si dispone di toocreate web tooact come punto di ingresso del progetto e quindi comunicare da tooyour sono singoli servizi.

In questa esercitazione è prelevare in cui è stata interrotta in hello [creazione di un'applicazione in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) esercitazione e aggiungere un servizio web ASP.NET Core davanti servizio con stato contatore hello. Se non è già stato fatto, è necessario tornare indietro ed eseguire prima quella esercitazione.

## <a name="set-up-your-environment-for-aspnet-core"></a>Configurare l'ambiente per ASP.NET Core

È necessario Visual Studio 2017 toofollow insieme a questa esercitazione. Qualsiasi edizione è adeguata. 

 - [Installare Visual Studio 2017](https://www.visualstudio.com/)

applicazioni ASP.NET Core Service Fabric toodevelop, è necessario avere hello installati i carichi di lavoro seguente:
 - **Sviluppo di Azure** (in *Web e cloud*)
 - **Sviluppo ASP.NET e Web** (in *Web e cloud*)
 - **Sviluppo multipiattaforma .NET Core** (in *Altri set di strumenti*)

>[!Note] 
>Hello strumenti di .NET Core per Visual Studio 2015 non è più corso l'aggiornamento, tuttavia se si utilizza ancora Visual Studio 2015, è necessario toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installato.

## <a name="add-an-aspnet-core-service-tooyour-application"></a>Aggiungere un'applicazione di tooyour servizio ASP.NET Core
ASP.NET Core è un framework di sviluppo web lightweight e multipiattaforma che è possibile utilizzare l'interfaccia utente web moderna toocreate e le API web. 

Aggiungere un'applicazione esistente di progetto tooour ASP.NET Web API.

1. In Esplora soluzioni fare doppio clic su **servizi** interno hello progetto di applicazione e scegliere **Aggiungi > nuovo servizio Service Fabric**.
   
    ![Aggiunta di una nuova applicazione esistente tooan di servizio][vs-add-new-service]
2. In hello **creare un servizio** pagina, scegliere **ASP.NET Core** e assegnargli un nome.
   
    ![Scelta di servizi web ASP.NET nella finestra di dialogo di hello nuovo servizio][vs-new-service-dialog]

3. la pagina successiva di Hello fornisce un set di ASP.NET Core modelli di progetto. Si noti che questi sono hello stesso scelte che si otterrebbe se è stato creato un progetto ASP.NET Core all'esterno di un'applicazione di Service Fabric, con una piccola quantità di codice aggiuntivo tooregister hello servizio con il runtime di Service Fabric hello. Per questa esercitazione si sceglierà **API Web**, Tuttavia, è possibile applicare hello stessi concetti toobuilding un'applicazione web completa.
   
    ![Scelta di un tipo di progetto ASP.NET][vs-new-aspnet-project-dialog]
   
    Dopo la creazione del progetto API Web l'applicazione includerà due servizi. Mentre si continua a toobuild l'applicazione, è possibile aggiungere più servizi in hello esattamente allo stesso modo. Per ogni servizio, sarà possibile eseguire in modo indipendente il controllo della versione e l'aggiornamento.

## <a name="run-hello-application"></a>Eseguire un'applicazione hello
tooget un'idea di cosa i professionisti IT, si distribuire nuova applicazione hello e intraprendere fornisce un'occhiata al comportamento predefinito di hello che hello modello API Web di ASP.NET Core.

1. Premere F5 in Visual Studio toodebug hello app.
2. Una volta completata la distribuzione, Visual Studio avvia una radice di toohello browser di hello servizio ASP.NET Web API. modello API Web di ASP.NET Core Hello non fornisce il comportamento predefinito per la radice di hello, pertanto viene visualizzato un errore 404 nel browser hello.
3. Aggiungere `/api/values` toohello posizione nel browser hello. Viene richiamato hello `Get` metodo hello ValuesController nel modello di hello API Web. Restituisce una risposta predefinita hello fornito dal modello hello: una matrice JSON contenente due stringhe:
   
    ![Valori predefiniti restituiti dal modello API Web ASP.NET Core][browser-aspnet-template-values]
   
    Fine hello di esercitazione hello, questa pagina mostrerà hello contatore il valore più recente dal servizio informazioni sullo stato anziché hello stringhe predefinite.

## <a name="connect-hello-services"></a>Connessione dei servizi di hello
L'infrastruttura di servizi offre la massima flessibilità nella comunicazione con Reliable Services. In una singola applicazione possono coesistere servizi accessibili tramite TCP, altri tramite un'API REST HTTP e altri ancora tramite Web Socket. Per informazioni sulle opzioni di hello disponibili e gli svantaggi di hello relativi, vedere [comunicazione con i servizi](service-fabric-connect-and-communicate-with-services.md). In questa esercitazione, si usa [comunicazione remota del servizio Service Fabric](service-fabric-reliable-services-communication-remoting.md), fornito in hello SDK.

In hello approccio di comunicazione remota del servizio (basato su RPC o di chiamate di procedura remota), viene definito un tooact interfaccia come contratto pubblico di hello per servizio hello. È quindi possibile utilizzare tale toogenerate interfaccia, una classe proxy per l'interazione con il servizio di hello.

### <a name="create-hello-remoting-interface"></a>Creare l'interfaccia di comunicazione remota di hello
Iniziamo creando hello interfaccia tooact come contratto hello tra servizio con stato hello e altri servizi, in questo caso hello progetto web ASP.NET Core. Questa interfaccia deve essere condiviso da tutti i servizi che utilizzano le chiamate RPC toomake, pertanto si creerà il proprio progetto libreria di classi.

1. In Esplora soluzioni fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Aggiungere** > **Nuovo progetto**.

2. Scegliere hello **Visual c#** voce nel riquadro di spostamento e quindi seleziona hello a sinistra hello **libreria di classi** modello. Verificare che tale versione di .NET Framework hello sia impostato troppo**4.5.2**.
   
    ![Creazione di un progetto interfaccia per il servizio con stato][vs-add-class-library-project]

3. Installare hello **Microsoft.ServiceFabric.Services.Remoting** pacchetto NuGet. Cercare **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager e installarlo per tutti i progetti nella soluzione hello utilizzano Assistenza remota, tra cui:
   - progetto libreria di classi Hello che contiene l'interfaccia del servizio hello
   - progetto di servizio con stato Hello
   - progetto di servizio web ASP.NET Core Hello
   
    ![Aggiunta del pacchetto NuGet Services hello][vs-services-nuget-package]

4. Nella libreria di classi hello, creare un'interfaccia con un singolo metodo, `GetCountAsync`, ed estendere l'interfaccia hello da `Microsoft.ServiceFabric.Services.Remoting.IService`. interfaccia di comunicazione remota di Hello deve derivare da questa tooindicate interfaccia che è un'interfaccia di comunicazione remota del servizio.
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a>Implementa interfaccia hello nel servizio con stato
Ora che sono state definite interfaccia hello, è necessario tooimplement nel servizio con stato hello.

1. Nel servizio con stato, aggiungere un riferimento toohello progetto libreria di classi contenente interfaccia hello.
   
    ![Aggiunta di un progetto libreria di classi di riferimento toohello nel servizio con stato hello][vs-add-class-library-reference]
2. Trovare la classe che eredita da hello `StatefulService`, ad esempio `MyStatefulService`ed espanderlo hello tooimplement `ICounter` interfaccia.
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. A questo punto implementare hello unico metodo che è definito in hello `ICounter` interfaccia `GetCountAsync`.
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a>Esporre servizio informazioni sullo stato di hello utilizzo di un listener di comunicazione remota di servizio
Con hello `ICounter` interfaccia implementata, passaggio finale hello è canale di comunicazione tooopen hello comunicazione remota del servizio. Per i servizi con stato, Service Fabric offre un metodo sostituibile denominato `CreateServiceReplicaListeners`, Con questo metodo, è possibile specificare uno o più listener di comunicazione, in base al tipo di hello di comunicazione che si desidera tooenable per il servizio.

> [!NOTE]
> viene chiamato il metodo equivalente Hello per l'apertura di un servizi toostateless canale di comunicazione `CreateServiceInstanceListeners`.

In questo caso, è necessario sostituire hello esistente `CreateServiceReplicaListeners` metodo e fornire un'istanza di `ServiceRemotingListener`, che consente di creare un endpoint RPC che è possibile chiamare dal client tramite `ServiceProxy`.  

Hello `CreateServiceRemotingListener` metodo di estensione su hello `IService` interfaccia consente tooeasily creare un `ServiceRemotingListener` con tutte le impostazioni predefinite. toouse questo metodo di estensione, verificare di aver hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` dello spazio dei nomi importato. 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a>Utilizzare hello ServiceProxy classe toointeract con servizio hello
Il servizio con stato è ora pronto tooreceive traffico da altri servizi tramite RPC. In modo che rimane consiste nell'aggiunta toocommunicate codice hello con esso da hello servizio web ASP.NET.

1. Nel progetto ASP.NET, aggiungere una libreria di classi di riferimento toohello contenente hello `ICounter` interfaccia.

2. In precedenza è stato aggiunto hello **Microsoft.ServiceFabric.Services.Remoting** progetto ASP.NET toohello di pacchetto NuGet. Questo pacchetto fornisce hello `ServiceProxy` classe che si utilizza RPC toomake chiama toohello di servizio con stato. Verificare il che installazione di questo pacchetto NuGet nel progetto di servizio web ASP.NET Core hello.

4. In hello **controller** cartella, aprire hello `ValuesController` classe. Si noti che hello `Get` metodo restituisce attualmente solo una matrice di stringhe hardcoded di "value1" e "value2" - corrispondente è stato illustrato in precedenza nel browser di hello. Sostituire questa implementazione con hello seguente codice:
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    Hello prima riga di codice è una chiave di hello. toocreate hello ICounter toohello con stato servizio proxy, è necessario tooprovide due tipi di informazioni: un nome di hello e di ID di partizione del servizio hello.
   
    È possibile utilizzare i servizi con stato di partizionamento tooscale suddividendo lo stato in bucket diversi, in base a una chiave che definiscono, ad esempio un ID cliente o un codice postale. Nell'applicazione semplice, servizio con stato hello dispone solo di una partizione, in modo chiave hello non è rilevante. Qualsiasi chiave che fornisce determinerà toohello stessa partizione. toolearn più informazioni sul partizionamento dei servizi, vedere [come toopartition affidabili servizi dell'infrastruttura](service-fabric-concepts-partitioning.md).
   
    nome del servizio Hello è un URI dell'infrastruttura di modulo hello: /&lt;application_name&gt;/&lt;service_name&gt;.
   
    Con questi due tipi di informazioni, Service Fabric possibile identificare in modo univoco macchina hello che devono essere inviate richieste. Hello `ServiceProxy` classe gestisce inoltre facilmente caso hello in cui machine hello che ospita la partizione di servizio con stato hello ha esito negativo e un altro computer deve essere innalzate di livello tootake al suo posto. Questa astrazione consente la scrittura hello client codice toodeal con altri servizi decisamente più semplice.
   
    Una volta che il proxy di hello, è sufficiente richiamare hello `GetCountAsync` (metodo) e restituisce il risultato.

5. Premere F5 nuovamente hello toorun modificato l'applicazione. Come prima, Visual Studio avvia automaticamente hello browser toohello radice hello web progetto. Aggiungere il percorso di "api/values" hello e dovrebbe essere hello valore del contatore corrente restituito.
   
    ![valore del contatore con stato Hello visualizzata nel browser hello][browser-aspnet-counter-value]
   
    Aggiornare il browser hello aggiornamento del valore periodicamente toosee hello contatore.

## <a name="kestrel-and-weblistener"></a>Kestrel e WebListener

Hello ASP.NET Core server web predefinito, noto come Kestrel, è [attualmente non supportata per la gestione del traffico internet diretta](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel). Di conseguenza, hello modello di servizio senza stato ASP.NET Core per Service Fabric utilizza [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) per impostazione predefinita. 

toolearn ulteriori informazioni su Kestrel e WebListener in servizi di Service Fabric, fare riferimento troppo[ASP.NET Core in servizi di Service Fabric affidabile](service-fabric-reliable-services-communication-aspnetcore.md).

## <a name="connecting-tooa-reliable-actor-service"></a>Connessione del servizio Reliable Actor tooa
Questa esercitazione ha illustrato la procedura per aggiungere un front-end Web in grado di comunicare con un servizio con stato. Tuttavia, è possibile seguire una tooactors di tootalk modello molto simile. Quando si crea un progetto Reliable Actor, Visual Studio genera automaticamente un progetto interfaccia. È possibile utilizzare tale toogenerate interfaccia un proxy attore in hello web progetto toocommunicate con attore hello. il canale di comunicazione Hello viene fornito automaticamente. Pertanto non è necessario toodo nulla che è equivalente tooestablishing un `ServiceRemotingListener` come fatto in precedenza per il servizio con stato hello in questa esercitazione.

## <a name="how-web-services-work-on-your-local-cluster"></a>Funzionamento dei servizi Web in un cluster locale
In generale, è possibile distribuire esattamente hello stesso Service Fabric applicazione tooa con più computer che sono stati distribuiti cluster nel cluster locale e altamente certezza che funziona come previsto. In questo modo il cluster locale è semplicemente una configurazione di cinque nodi è compresso tooa singolo computer.

Per quanto riguarda i servizi tooweb, tuttavia, è una sfumatura di chiave. Quando il cluster si trova dietro un bilanciamento del carico, come invece avviene in Azure, è necessario assicurarsi che i servizi web vengono distribuiti in tutti i computer dal servizio di bilanciamento del carico hello round-robins semplicemente il traffico tra più computer hello. È possibile farlo dall'impostazione hello `InstanceCount` per hello servizio toohello valore speciale "-1".

Al contrario, quando si esegue un servizio web in locale, è necessario tooensure solo un'istanza del servizio hello è in esecuzione. In caso contrario, si verificano conflitti di più processi che sono in attesa sulla hello stesso percorso e la porta. Di conseguenza, numero di istanze del servizio web hello deve essere impostato troppo "1" per le distribuzioni locali.

toolearn tooconfigure valori diversi per un ambiente diverso, vedere [la gestione dei parametri dell'applicazione per più ambienti](service-fabric-manage-multiple-environment-app-configuration.md).

## <a name="next-steps"></a>Passaggi successivi
Dopo l'impostazione del front-end Web per l'applicazione con ASP.NET Core, vedere altre informazioni su [ASP.NET Core in Reliable Services di Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md) per un esame dettagliato dell'interazione tra ASP.NET Core e Service Fabric.

Successivamente, [ulteriori informazioni sulla comunicazione con i servizi](service-fabric-connect-and-communicate-with-services.md) in genere tooget un completamento immagine di servizio come comunicazione funziona nell'infrastruttura del servizio.

Dopo avere una buona conoscenza del funzionamento della comunicazione del servizio, [creare un cluster in Azure e la distribuzione del cloud toohello applicazione](service-fabric-cluster-creation-via-portal.md).

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
