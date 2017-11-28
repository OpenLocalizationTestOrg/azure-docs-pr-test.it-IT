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
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="81c3d-103">Compilare un front-end di servizio Web per l'applicazione tramite ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="81c3d-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="81c3d-104">Per impostazione predefinita, i servizi di Azure Service Fabric non forniscono un web toohello interfaccia pubblica.</span><span class="sxs-lookup"><span data-stu-id="81c3d-104">By default, Azure Service Fabric services do not provide a public interface toohello web.</span></span> <span data-ttu-id="81c3d-105">tooexpose client tooHTTP di funzionalità dell'applicazione, si dispone di toocreate web tooact come punto di ingresso del progetto e quindi comunicare da tooyour sono singoli servizi.</span><span class="sxs-lookup"><span data-stu-id="81c3d-105">tooexpose your application's functionality tooHTTP clients, you have toocreate a web project tooact as an entry point and then communicate from there tooyour individual services.</span></span>

<span data-ttu-id="81c3d-106">In questa esercitazione è prelevare in cui è stata interrotta in hello [creazione di un'applicazione in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) esercitazione e aggiungere un servizio web ASP.NET Core davanti servizio con stato contatore hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-106">In this tutorial, we pick up where we left off in hello [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of hello stateful counter service.</span></span> <span data-ttu-id="81c3d-107">Se non è già stato fatto, è necessario tornare indietro ed eseguire prima quella esercitazione.</span><span class="sxs-lookup"><span data-stu-id="81c3d-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="81c3d-108">Configurare l'ambiente per ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="81c3d-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="81c3d-109">È necessario Visual Studio 2017 toofollow insieme a questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="81c3d-109">You need Visual Studio 2017 toofollow along with this tutorial.</span></span> <span data-ttu-id="81c3d-110">Qualsiasi edizione è adeguata.</span><span class="sxs-lookup"><span data-stu-id="81c3d-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="81c3d-111">Installare Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="81c3d-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="81c3d-112">applicazioni ASP.NET Core Service Fabric toodevelop, è necessario avere hello installati i carichi di lavoro seguente:</span><span class="sxs-lookup"><span data-stu-id="81c3d-112">toodevelop ASP.NET Core Service Fabric applications, you should have hello following workloads installed:</span></span>
 - <span data-ttu-id="81c3d-113">**Sviluppo di Azure** (in *Web e cloud*)</span><span class="sxs-lookup"><span data-stu-id="81c3d-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="81c3d-114">**Sviluppo ASP.NET e Web** (in *Web e cloud*)</span><span class="sxs-lookup"><span data-stu-id="81c3d-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="81c3d-115">**Sviluppo multipiattaforma .NET Core** (in *Altri set di strumenti*)</span><span class="sxs-lookup"><span data-stu-id="81c3d-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="81c3d-116">Hello strumenti di .NET Core per Visual Studio 2015 non è più corso l'aggiornamento, tuttavia se si utilizza ancora Visual Studio 2015, è necessario toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installato.</span><span class="sxs-lookup"><span data-stu-id="81c3d-116">hello .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-tooyour-application"></a><span data-ttu-id="81c3d-117">Aggiungere un'applicazione di tooyour servizio ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="81c3d-117">Add an ASP.NET Core service tooyour application</span></span>
<span data-ttu-id="81c3d-118">ASP.NET Core è un framework di sviluppo web lightweight e multipiattaforma che è possibile utilizzare l'interfaccia utente web moderna toocreate e le API web.</span><span class="sxs-lookup"><span data-stu-id="81c3d-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> 

<span data-ttu-id="81c3d-119">Aggiungere un'applicazione esistente di progetto tooour ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="81c3d-119">Let's add an ASP.NET Web API project tooour existing application.</span></span>

1. <span data-ttu-id="81c3d-120">In Esplora soluzioni fare doppio clic su **servizi** interno hello progetto di applicazione e scegliere **Aggiungi > nuovo servizio Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="81c3d-120">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Aggiunta di una nuova applicazione esistente tooan di servizio][vs-add-new-service]
2. <span data-ttu-id="81c3d-122">In hello **creare un servizio** pagina, scegliere **ASP.NET Core** e assegnargli un nome.</span><span class="sxs-lookup"><span data-stu-id="81c3d-122">On hello **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![Scelta di servizi web ASP.NET nella finestra di dialogo di hello nuovo servizio][vs-new-service-dialog]

3. <span data-ttu-id="81c3d-124">la pagina successiva di Hello fornisce un set di ASP.NET Core modelli di progetto.</span><span class="sxs-lookup"><span data-stu-id="81c3d-124">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="81c3d-125">Si noti che questi sono hello stesso scelte che si otterrebbe se è stato creato un progetto ASP.NET Core all'esterno di un'applicazione di Service Fabric, con una piccola quantità di codice aggiuntivo tooregister hello servizio con il runtime di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-125">Note that these are hello same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code tooregister hello service with hello Service Fabric runtime.</span></span> <span data-ttu-id="81c3d-126">Per questa esercitazione si sceglierà **API Web**,</span><span class="sxs-lookup"><span data-stu-id="81c3d-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="81c3d-127">Tuttavia, è possibile applicare hello stessi concetti toobuilding un'applicazione web completa.</span><span class="sxs-lookup"><span data-stu-id="81c3d-127">However, you can apply hello same concepts toobuilding a full web application.</span></span>
   
    ![Scelta di un tipo di progetto ASP.NET][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="81c3d-129">Dopo la creazione del progetto API Web l'applicazione includerà due servizi.</span><span class="sxs-lookup"><span data-stu-id="81c3d-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="81c3d-130">Mentre si continua a toobuild l'applicazione, è possibile aggiungere più servizi in hello esattamente allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="81c3d-130">As you continue toobuild your application, you can add more services in exactly hello same way.</span></span> <span data-ttu-id="81c3d-131">Per ogni servizio, sarà possibile eseguire in modo indipendente il controllo della versione e l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="81c3d-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="81c3d-132">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="81c3d-132">Run hello application</span></span>
<span data-ttu-id="81c3d-133">tooget un'idea di cosa i professionisti IT, si distribuire nuova applicazione hello e intraprendere fornisce un'occhiata al comportamento predefinito di hello che hello modello API Web di ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="81c3d-133">tooget a sense of what we've done, let's deploy hello new application and take a look at hello default behavior that hello ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="81c3d-134">Premere F5 in Visual Studio toodebug hello app.</span><span class="sxs-lookup"><span data-stu-id="81c3d-134">Press F5 in Visual Studio toodebug hello app.</span></span>
2. <span data-ttu-id="81c3d-135">Una volta completata la distribuzione, Visual Studio avvia una radice di toohello browser di hello servizio ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="81c3d-135">When deployment is complete, Visual Studio launches a browser toohello root of hello ASP.NET Web API service.</span></span> <span data-ttu-id="81c3d-136">modello API Web di ASP.NET Core Hello non fornisce il comportamento predefinito per la radice di hello, pertanto viene visualizzato un errore 404 nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-136">hello ASP.NET Core Web API template doesn't provide default behavior for hello root, so you should see a 404 error in hello browser.</span></span>
3. <span data-ttu-id="81c3d-137">Aggiungere `/api/values` toohello posizione nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-137">Add `/api/values` toohello location in hello browser.</span></span> <span data-ttu-id="81c3d-138">Viene richiamato hello `Get` metodo hello ValuesController nel modello di hello API Web.</span><span class="sxs-lookup"><span data-stu-id="81c3d-138">This invokes hello `Get` method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="81c3d-139">Restituisce una risposta predefinita hello fornito dal modello hello: una matrice JSON contenente due stringhe:</span><span class="sxs-lookup"><span data-stu-id="81c3d-139">It returns hello default response that is provided by hello template--a JSON array that contains two strings:</span></span>
   
    ![Valori predefiniti restituiti dal modello API Web ASP.NET Core][browser-aspnet-template-values]
   
    <span data-ttu-id="81c3d-141">Fine hello di esercitazione hello, questa pagina mostrerà hello contatore il valore più recente dal servizio informazioni sullo stato anziché hello stringhe predefinite.</span><span class="sxs-lookup"><span data-stu-id="81c3d-141">By hello end of hello tutorial, this page will show hello most recent counter value from our stateful service instead of hello default strings.</span></span>

## <a name="connect-hello-services"></a><span data-ttu-id="81c3d-142">Connessione dei servizi di hello</span><span class="sxs-lookup"><span data-stu-id="81c3d-142">Connect hello services</span></span>
<span data-ttu-id="81c3d-143">L'infrastruttura di servizi offre la massima flessibilità nella comunicazione con Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="81c3d-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="81c3d-144">In una singola applicazione possono coesistere servizi accessibili tramite TCP, altri tramite un'API REST HTTP e altri ancora tramite Web Socket.</span><span class="sxs-lookup"><span data-stu-id="81c3d-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="81c3d-145">Per informazioni sulle opzioni di hello disponibili e gli svantaggi di hello relativi, vedere [comunicazione con i servizi](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="81c3d-145">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="81c3d-146">In questa esercitazione, si usa [comunicazione remota del servizio Service Fabric](service-fabric-reliable-services-communication-remoting.md), fornito in hello SDK.</span><span class="sxs-lookup"><span data-stu-id="81c3d-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in hello SDK.</span></span>

<span data-ttu-id="81c3d-147">In hello approccio di comunicazione remota del servizio (basato su RPC o di chiamate di procedura remota), viene definito un tooact interfaccia come contratto pubblico di hello per servizio hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-147">In hello Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface tooact as hello public contract for hello service.</span></span> <span data-ttu-id="81c3d-148">È quindi possibile utilizzare tale toogenerate interfaccia, una classe proxy per l'interazione con il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-148">Then, you use that interface toogenerate a proxy class for interacting with hello service.</span></span>

### <a name="create-hello-remoting-interface"></a><span data-ttu-id="81c3d-149">Creare l'interfaccia di comunicazione remota di hello</span><span class="sxs-lookup"><span data-stu-id="81c3d-149">Create hello remoting interface</span></span>
<span data-ttu-id="81c3d-150">Iniziamo creando hello interfaccia tooact come contratto hello tra servizio con stato hello e altri servizi, in questo caso hello progetto web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="81c3d-150">Let's start by creating hello interface tooact as hello contract between hello stateful service and other services, in this case hello ASP.NET Core web project.</span></span> <span data-ttu-id="81c3d-151">Questa interfaccia deve essere condiviso da tutti i servizi che utilizzano le chiamate RPC toomake, pertanto si creerà il proprio progetto libreria di classi.</span><span class="sxs-lookup"><span data-stu-id="81c3d-151">This interface must be shared by all services that use it toomake RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="81c3d-152">In Esplora soluzioni fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Aggiungere** > **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="81c3d-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="81c3d-153">Scegliere hello **Visual c#** voce nel riquadro di spostamento e quindi seleziona hello a sinistra hello **libreria di classi** modello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-153">Choose hello **Visual C#** entry in hello left navigation pane and then select hello **Class Library** template.</span></span> <span data-ttu-id="81c3d-154">Verificare che tale versione di .NET Framework hello sia impostato troppo**4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="81c3d-154">Ensure that hello .NET Framework version is set too**4.5.2**.</span></span>
   
    ![Creazione di un progetto interfaccia per il servizio con stato][vs-add-class-library-project]

3. <span data-ttu-id="81c3d-156">Installare hello **Microsoft.ServiceFabric.Services.Remoting** pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="81c3d-156">Install hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="81c3d-157">Cercare **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager e installarlo per tutti i progetti nella soluzione hello utilizzano Assistenza remota, tra cui:</span><span class="sxs-lookup"><span data-stu-id="81c3d-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager and install it for all projects in hello solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="81c3d-158">progetto libreria di classi Hello che contiene l'interfaccia del servizio hello</span><span class="sxs-lookup"><span data-stu-id="81c3d-158">hello Class Library project that contains hello service interface</span></span>
   - <span data-ttu-id="81c3d-159">progetto di servizio con stato Hello</span><span class="sxs-lookup"><span data-stu-id="81c3d-159">hello Stateful Service project</span></span>
   - <span data-ttu-id="81c3d-160">progetto di servizio web ASP.NET Core Hello</span><span class="sxs-lookup"><span data-stu-id="81c3d-160">hello ASP.NET Core web service project</span></span>
   
    ![Aggiunta del pacchetto NuGet Services hello][vs-services-nuget-package]

4. <span data-ttu-id="81c3d-162">Nella libreria di classi hello, creare un'interfaccia con un singolo metodo, `GetCountAsync`, ed estendere l'interfaccia hello da `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="81c3d-162">In hello class library, create an interface with a single method, `GetCountAsync`, and extend hello interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="81c3d-163">interfaccia di comunicazione remota di Hello deve derivare da questa tooindicate interfaccia che è un'interfaccia di comunicazione remota del servizio.</span><span class="sxs-lookup"><span data-stu-id="81c3d-163">hello remoting interface must derive from this interface tooindicate that it is a Service Remoting interface.</span></span>
   
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

### <a name="implement-hello-interface-in-your-stateful-service"></a><span data-ttu-id="81c3d-164">Implementa interfaccia hello nel servizio con stato</span><span class="sxs-lookup"><span data-stu-id="81c3d-164">Implement hello interface in your stateful service</span></span>
<span data-ttu-id="81c3d-165">Ora che sono state definite interfaccia hello, è necessario tooimplement nel servizio con stato hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-165">Now that we have defined hello interface, we need tooimplement it in hello stateful service.</span></span>

1. <span data-ttu-id="81c3d-166">Nel servizio con stato, aggiungere un riferimento toohello progetto libreria di classi contenente interfaccia hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-166">In your stateful service, add a reference toohello class library project that contains hello interface.</span></span>
   
    ![Aggiunta di un progetto libreria di classi di riferimento toohello nel servizio con stato hello][vs-add-class-library-reference]
2. <span data-ttu-id="81c3d-168">Trovare la classe che eredita da hello `StatefulService`, ad esempio `MyStatefulService`ed espanderlo hello tooimplement `ICounter` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="81c3d-168">Locate hello class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it tooimplement hello `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="81c3d-169">A questo punto implementare hello unico metodo che è definito in hello `ICounter` interfaccia `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="81c3d-169">Now implement hello single method that is defined in hello `ICounter` interface, `GetCountAsync`.</span></span>
   
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

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="81c3d-170">Esporre servizio informazioni sullo stato di hello utilizzo di un listener di comunicazione remota di servizio</span><span class="sxs-lookup"><span data-stu-id="81c3d-170">Expose hello stateful service using a service remoting listener</span></span>
<span data-ttu-id="81c3d-171">Con hello `ICounter` interfaccia implementata, passaggio finale hello è canale di comunicazione tooopen hello comunicazione remota del servizio.</span><span class="sxs-lookup"><span data-stu-id="81c3d-171">With hello `ICounter` interface implemented, hello final step is tooopen hello Service Remoting communication channel.</span></span> <span data-ttu-id="81c3d-172">Per i servizi con stato, Service Fabric offre un metodo sostituibile denominato `CreateServiceReplicaListeners`,</span><span class="sxs-lookup"><span data-stu-id="81c3d-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="81c3d-173">Con questo metodo, è possibile specificare uno o più listener di comunicazione, in base al tipo di hello di comunicazione che si desidera tooenable per il servizio.</span><span class="sxs-lookup"><span data-stu-id="81c3d-173">With this method, you can specify one or more communication listeners, based on hello type of communication that you want tooenable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="81c3d-174">viene chiamato il metodo equivalente Hello per l'apertura di un servizi toostateless canale di comunicazione `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="81c3d-174">hello equivalent method for opening a communication channel toostateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="81c3d-175">In questo caso, è necessario sostituire hello esistente `CreateServiceReplicaListeners` metodo e fornire un'istanza di `ServiceRemotingListener`, che consente di creare un endpoint RPC che è possibile chiamare dal client tramite `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="81c3d-175">In this case, we replace hello existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="81c3d-176">Hello `CreateServiceRemotingListener` metodo di estensione su hello `IService` interfaccia consente tooeasily creare un `ServiceRemotingListener` con tutte le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="81c3d-176">hello `CreateServiceRemotingListener` extension method on hello `IService` interface allows you tooeasily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="81c3d-177">toouse questo metodo di estensione, verificare di aver hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` dello spazio dei nomi importato.</span><span class="sxs-lookup"><span data-stu-id="81c3d-177">toouse this extension method, ensure you have hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

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


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a><span data-ttu-id="81c3d-178">Utilizzare hello ServiceProxy classe toointeract con servizio hello</span><span class="sxs-lookup"><span data-stu-id="81c3d-178">Use hello ServiceProxy class toointeract with hello service</span></span>
<span data-ttu-id="81c3d-179">Il servizio con stato è ora pronto tooreceive traffico da altri servizi tramite RPC.</span><span class="sxs-lookup"><span data-stu-id="81c3d-179">Our stateful service is now ready tooreceive traffic from other services over RPC.</span></span> <span data-ttu-id="81c3d-180">In modo che rimane consiste nell'aggiunta toocommunicate codice hello con esso da hello servizio web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="81c3d-180">So all that remains is adding hello code toocommunicate with it from hello ASP.NET web service.</span></span>

1. <span data-ttu-id="81c3d-181">Nel progetto ASP.NET, aggiungere una libreria di classi di riferimento toohello contenente hello `ICounter` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="81c3d-181">In your ASP.NET project, add a reference toohello class library that contains hello `ICounter` interface.</span></span>

2. <span data-ttu-id="81c3d-182">In precedenza è stato aggiunto hello **Microsoft.ServiceFabric.Services.Remoting** progetto ASP.NET toohello di pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="81c3d-182">Earlier you added hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello ASP.NET project.</span></span> <span data-ttu-id="81c3d-183">Questo pacchetto fornisce hello `ServiceProxy` classe che si utilizza RPC toomake chiama toohello di servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="81c3d-183">This package provides hello `ServiceProxy` class which you use toomake RPC calls toohello stateful service.</span></span> <span data-ttu-id="81c3d-184">Verificare il che installazione di questo pacchetto NuGet nel progetto di servizio web ASP.NET Core hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-184">Ensure this NuGet package is installed in hello ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="81c3d-185">In hello **controller** cartella, aprire hello `ValuesController` classe.</span><span class="sxs-lookup"><span data-stu-id="81c3d-185">In hello **Controllers** folder, open hello `ValuesController` class.</span></span> <span data-ttu-id="81c3d-186">Si noti che hello `Get` metodo restituisce attualmente solo una matrice di stringhe hardcoded di "value1" e "value2" - corrispondente è stato illustrato in precedenza nel browser di hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-186">Note that hello `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in hello browser.</span></span> <span data-ttu-id="81c3d-187">Sostituire questa implementazione con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="81c3d-187">Replace this implementation with hello following code:</span></span>
   
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
   
    <span data-ttu-id="81c3d-188">Hello prima riga di codice è una chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-188">hello first line of code is hello key one.</span></span> <span data-ttu-id="81c3d-189">toocreate hello ICounter toohello con stato servizio proxy, è necessario tooprovide due tipi di informazioni: un nome di hello e di ID di partizione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-189">toocreate hello ICounter proxy toohello stateful service, you need tooprovide two pieces of information: a partition ID and hello name of hello service.</span></span>
   
    <span data-ttu-id="81c3d-190">È possibile utilizzare i servizi con stato di partizionamento tooscale suddividendo lo stato in bucket diversi, in base a una chiave che definiscono, ad esempio un ID cliente o un codice postale.</span><span class="sxs-lookup"><span data-stu-id="81c3d-190">You can use partitioning tooscale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="81c3d-191">Nell'applicazione semplice, servizio con stato hello dispone solo di una partizione, in modo chiave hello non è rilevante.</span><span class="sxs-lookup"><span data-stu-id="81c3d-191">In our trivial application, hello stateful service only has one partition, so hello key doesn't matter.</span></span> <span data-ttu-id="81c3d-192">Qualsiasi chiave che fornisce determinerà toohello stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="81c3d-192">Any key that you provide will lead toohello same partition.</span></span> <span data-ttu-id="81c3d-193">toolearn più informazioni sul partizionamento dei servizi, vedere [come toopartition affidabili servizi dell'infrastruttura](service-fabric-concepts-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="81c3d-193">toolearn more about partitioning services, see [How toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="81c3d-194">nome del servizio Hello è un URI dell'infrastruttura di modulo hello: /&lt;application_name&gt;/&lt;service_name&gt;.</span><span class="sxs-lookup"><span data-stu-id="81c3d-194">hello service name is a URI of hello form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="81c3d-195">Con questi due tipi di informazioni, Service Fabric possibile identificare in modo univoco macchina hello che devono essere inviate richieste.</span><span class="sxs-lookup"><span data-stu-id="81c3d-195">With these two pieces of information, Service Fabric can uniquely identify hello machine that requests should be sent to.</span></span> <span data-ttu-id="81c3d-196">Hello `ServiceProxy` classe gestisce inoltre facilmente caso hello in cui machine hello che ospita la partizione di servizio con stato hello ha esito negativo e un altro computer deve essere innalzate di livello tootake al suo posto.</span><span class="sxs-lookup"><span data-stu-id="81c3d-196">hello `ServiceProxy` class also seamlessly handles hello case where hello machine that hosts hello stateful service partition fails and another machine must be promoted tootake its place.</span></span> <span data-ttu-id="81c3d-197">Questa astrazione consente la scrittura hello client codice toodeal con altri servizi decisamente più semplice.</span><span class="sxs-lookup"><span data-stu-id="81c3d-197">This abstraction makes writing hello client code toodeal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="81c3d-198">Una volta che il proxy di hello, è sufficiente richiamare hello `GetCountAsync` (metodo) e restituisce il risultato.</span><span class="sxs-lookup"><span data-stu-id="81c3d-198">Once we have hello proxy, we simply invoke hello `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="81c3d-199">Premere F5 nuovamente hello toorun modificato l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="81c3d-199">Press F5 again toorun hello modified application.</span></span> <span data-ttu-id="81c3d-200">Come prima, Visual Studio avvia automaticamente hello browser toohello radice hello web progetto.</span><span class="sxs-lookup"><span data-stu-id="81c3d-200">As before, Visual Studio automatically launches hello browser toohello root of hello web project.</span></span> <span data-ttu-id="81c3d-201">Aggiungere il percorso di "api/values" hello e dovrebbe essere hello valore del contatore corrente restituito.</span><span class="sxs-lookup"><span data-stu-id="81c3d-201">Add hello "api/values" path, and you should see hello current counter value returned.</span></span>
   
    ![valore del contatore con stato Hello visualizzata nel browser hello][browser-aspnet-counter-value]
   
    <span data-ttu-id="81c3d-203">Aggiornare il browser hello aggiornamento del valore periodicamente toosee hello contatore.</span><span class="sxs-lookup"><span data-stu-id="81c3d-203">Refresh hello browser periodically toosee hello counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="81c3d-204">Kestrel e WebListener</span><span class="sxs-lookup"><span data-stu-id="81c3d-204">Kestrel and WebListener</span></span>

<span data-ttu-id="81c3d-205">Hello ASP.NET Core server web predefinito, noto come Kestrel, è [attualmente non supportata per la gestione del traffico internet diretta](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="81c3d-205">hello default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="81c3d-206">Di conseguenza, hello modello di servizio senza stato ASP.NET Core per Service Fabric utilizza [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="81c3d-206">As a result, hello ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="81c3d-207">toolearn ulteriori informazioni su Kestrel e WebListener in servizi di Service Fabric, fare riferimento troppo[ASP.NET Core in servizi di Service Fabric affidabile](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="81c3d-207">toolearn more about Kestrel and WebListener in Service Fabric services, please refer too[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-tooa-reliable-actor-service"></a><span data-ttu-id="81c3d-208">Connessione del servizio Reliable Actor tooa</span><span class="sxs-lookup"><span data-stu-id="81c3d-208">Connecting tooa Reliable Actor service</span></span>
<span data-ttu-id="81c3d-209">Questa esercitazione ha illustrato la procedura per aggiungere un front-end Web in grado di comunicare con un servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="81c3d-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="81c3d-210">Tuttavia, è possibile seguire una tooactors di tootalk modello molto simile.</span><span class="sxs-lookup"><span data-stu-id="81c3d-210">However, you can follow a very similar model tootalk tooactors.</span></span> <span data-ttu-id="81c3d-211">Quando si crea un progetto Reliable Actor, Visual Studio genera automaticamente un progetto interfaccia.</span><span class="sxs-lookup"><span data-stu-id="81c3d-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="81c3d-212">È possibile utilizzare tale toogenerate interfaccia un proxy attore in hello web progetto toocommunicate con attore hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-212">You can use that interface toogenerate an actor proxy in hello web project toocommunicate with hello actor.</span></span> <span data-ttu-id="81c3d-213">il canale di comunicazione Hello viene fornito automaticamente.</span><span class="sxs-lookup"><span data-stu-id="81c3d-213">hello communication channel is provided automatically.</span></span> <span data-ttu-id="81c3d-214">Pertanto non è necessario toodo nulla che è equivalente tooestablishing un `ServiceRemotingListener` come fatto in precedenza per il servizio con stato hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="81c3d-214">So you do not need toodo anything that is equivalent tooestablishing a `ServiceRemotingListener` like you did for hello stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="81c3d-215">Funzionamento dei servizi Web in un cluster locale</span><span class="sxs-lookup"><span data-stu-id="81c3d-215">How web services work on your local cluster</span></span>
<span data-ttu-id="81c3d-216">In generale, è possibile distribuire esattamente hello stesso Service Fabric applicazione tooa con più computer che sono stati distribuiti cluster nel cluster locale e altamente certezza che funziona come previsto.</span><span class="sxs-lookup"><span data-stu-id="81c3d-216">In general, you can deploy exactly hello same Service Fabric application tooa multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="81c3d-217">In questo modo il cluster locale è semplicemente una configurazione di cinque nodi è compresso tooa singolo computer.</span><span class="sxs-lookup"><span data-stu-id="81c3d-217">This is because your local cluster is simply a five-node configuration that is collapsed tooa single machine.</span></span>

<span data-ttu-id="81c3d-218">Per quanto riguarda i servizi tooweb, tuttavia, è una sfumatura di chiave.</span><span class="sxs-lookup"><span data-stu-id="81c3d-218">When it comes tooweb services, however, there is one key nuance.</span></span> <span data-ttu-id="81c3d-219">Quando il cluster si trova dietro un bilanciamento del carico, come invece avviene in Azure, è necessario assicurarsi che i servizi web vengono distribuiti in tutti i computer dal servizio di bilanciamento del carico hello round-robins semplicemente il traffico tra più computer hello.</span><span class="sxs-lookup"><span data-stu-id="81c3d-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since hello load balancer simply round-robins traffic across hello machines.</span></span> <span data-ttu-id="81c3d-220">È possibile farlo dall'impostazione hello `InstanceCount` per hello servizio toohello valore speciale "-1".</span><span class="sxs-lookup"><span data-stu-id="81c3d-220">You can do this by setting hello `InstanceCount` for hello service toohello special value of "-1".</span></span>

<span data-ttu-id="81c3d-221">Al contrario, quando si esegue un servizio web in locale, è necessario tooensure solo un'istanza del servizio hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="81c3d-221">By contrast, when you run a web service locally, you need tooensure that only one instance of hello service is running.</span></span> <span data-ttu-id="81c3d-222">In caso contrario, si verificano conflitti di più processi che sono in attesa sulla hello stesso percorso e la porta.</span><span class="sxs-lookup"><span data-stu-id="81c3d-222">Otherwise, you run into conflicts from multiple processes that are listening on hello same path and port.</span></span> <span data-ttu-id="81c3d-223">Di conseguenza, numero di istanze del servizio web hello deve essere impostato troppo "1" per le distribuzioni locali.</span><span class="sxs-lookup"><span data-stu-id="81c3d-223">As a result, hello web service instance count should be set too"1" for local deployments.</span></span>

<span data-ttu-id="81c3d-224">toolearn tooconfigure valori diversi per un ambiente diverso, vedere [la gestione dei parametri dell'applicazione per più ambienti](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="81c3d-224">toolearn how tooconfigure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="81c3d-225">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81c3d-225">Next steps</span></span>
<span data-ttu-id="81c3d-226">Dopo l'impostazione del front-end Web per l'applicazione con ASP.NET Core, vedere altre informazioni su [ASP.NET Core in Reliable Services di Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md) per un esame dettagliato dell'interazione tra ASP.NET Core e Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="81c3d-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="81c3d-227">Successivamente, [ulteriori informazioni sulla comunicazione con i servizi](service-fabric-connect-and-communicate-with-services.md) in genere tooget un completamento immagine di servizio come comunicazione funziona nell'infrastruttura del servizio.</span><span class="sxs-lookup"><span data-stu-id="81c3d-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general tooget a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="81c3d-228">Dopo avere una buona conoscenza del funzionamento della comunicazione del servizio, [creare un cluster in Azure e la distribuzione del cloud toohello applicazione](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="81c3d-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application toohello cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

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
