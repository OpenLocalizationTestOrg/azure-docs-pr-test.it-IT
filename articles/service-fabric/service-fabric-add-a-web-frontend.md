---
title: Creare un front-end Web per l'app Azure Service Fabric tramite ASP.NET Core | Microsoft Docs
description: Esporre l'applicazione di Service Fabric al Web usando un progetto ASP.NET Core e la comunicazione tra servizi tramite servizio remoto.
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
ms.openlocfilehash: b19aaa652f2c15573ded632ca1348e1a6752f080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="2c090-103">Compilare un front-end di servizio Web per l'applicazione tramite ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2c090-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="2c090-104">Per impostazione predefinita, i servizi di Azure Service Fabric non forniscono un'interfaccia pubblica per il Web.</span><span class="sxs-lookup"><span data-stu-id="2c090-104">By default, Azure Service Fabric services do not provide a public interface to the web.</span></span> <span data-ttu-id="2c090-105">Per esporre la funzionalità dell'applicazione ai client HTTP è necessario creare un progetto Web da usare come punto di ingresso per comunicare con i singoli servizi.</span><span class="sxs-lookup"><span data-stu-id="2c090-105">To expose your application's functionality to HTTP clients, you have to create a web project to act as an entry point and then communicate from there to your individual services.</span></span>

<span data-ttu-id="2c090-106">Questa esercitazione è la prosecuzione dell'esercitazione [Creare la prima applicazione in Visual studio](service-fabric-create-your-first-application-in-visual-studio.md). Verrà aggiunto un servizio Web ASP.NET Core per il servizio dei contatori con stato.</span><span class="sxs-lookup"><span data-stu-id="2c090-106">In this tutorial, we pick up where we left off in the [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of the stateful counter service.</span></span> <span data-ttu-id="2c090-107">Se non è già stato fatto, è necessario tornare indietro ed eseguire prima quella esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2c090-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="2c090-108">Configurare l'ambiente per ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2c090-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="2c090-109">Per completare questa esercitazione è necessario Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2c090-109">You need Visual Studio 2017 to follow along with this tutorial.</span></span> <span data-ttu-id="2c090-110">Qualsiasi edizione è adeguata.</span><span class="sxs-lookup"><span data-stu-id="2c090-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="2c090-111">Installare Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="2c090-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="2c090-112">Per sviluppare applicazioni Service Fabric ASP.NET Core è necessario avere installato i carichi di lavoro seguenti:</span><span class="sxs-lookup"><span data-stu-id="2c090-112">To develop ASP.NET Core Service Fabric applications, you should have the following workloads installed:</span></span>
 - <span data-ttu-id="2c090-113">**Sviluppo di Azure** (in *Web e cloud*)</span><span class="sxs-lookup"><span data-stu-id="2c090-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="2c090-114">**Sviluppo ASP.NET e Web** (in *Web e cloud*)</span><span class="sxs-lookup"><span data-stu-id="2c090-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="2c090-115">**Sviluppo multipiattaforma .NET Core** (in *Altri set di strumenti*)</span><span class="sxs-lookup"><span data-stu-id="2c090-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="2c090-116">Gli strumenti .NET Core per Visual Studio 2015 non vengono più aggiornati. Se si usa Visual Studio 2015 è necessario avere installato [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="2c090-116">The .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need to have [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-to-your-application"></a><span data-ttu-id="2c090-117">Aggiungere un servizio ASP.NET Core all'applicazione</span><span class="sxs-lookup"><span data-stu-id="2c090-117">Add an ASP.NET Core service to your application</span></span>
<span data-ttu-id="2c090-118">ASP.NET Core è un framework di sviluppo Web multipiattaforma leggero, che consente di creare un'interfaccia utente Web e API Web moderne.</span><span class="sxs-lookup"><span data-stu-id="2c090-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> 

<span data-ttu-id="2c090-119">Ora verrà aggiunto un progetto API Web ASP.NET all'applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="2c090-119">Let's add an ASP.NET Web API project to our existing application.</span></span>

1. <span data-ttu-id="2c090-120">In Esplora soluzioni fare clic con il pulsante destro del mouse su **Servizi** nel progetto dell'applicazione e scegliere **Aggiungi > Nuovo servizio Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="2c090-120">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Aggiunta di un nuovo servizio a un'applicazione esistente][vs-add-new-service]
2. <span data-ttu-id="2c090-122">Nella pagina **Crea servizio** scegliere **ASP.NET Core** e assegnare un nome.</span><span class="sxs-lookup"><span data-stu-id="2c090-122">On the **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![Scelta di un servizio Web ASP.NET nella finestra di dialogo del nuovo servizio][vs-new-service-dialog]

3. <span data-ttu-id="2c090-124">Nella pagina successiva è disponibile un set di modelli di progetto ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="2c090-124">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="2c090-125">Si tratta degli stessi modelli che verrebbero visualizzati se si creasse un progetto ASP.NET Core all'esterno di un'applicazione di Service Fabric, con una piccola quantità di codice aggiuntivo per registrare il servizio con il runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2c090-125">Note that these are the same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code to register the service with the Service Fabric runtime.</span></span> <span data-ttu-id="2c090-126">Per questa esercitazione si sceglierà **API Web**,</span><span class="sxs-lookup"><span data-stu-id="2c090-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="2c090-127">ma è possibile applicare gli stessi concetti anche alla compilazione di un'applicazione Web completa.</span><span class="sxs-lookup"><span data-stu-id="2c090-127">However, you can apply the same concepts to building a full web application.</span></span>
   
    ![Scelta di un tipo di progetto ASP.NET][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="2c090-129">Dopo la creazione del progetto API Web l'applicazione includerà due servizi.</span><span class="sxs-lookup"><span data-stu-id="2c090-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="2c090-130">Man mano che si compila l'applicazione, si aggiungeranno altri servizi seguendo esattamente la stessa procedura</span><span class="sxs-lookup"><span data-stu-id="2c090-130">As you continue to build your application, you can add more services in exactly the same way.</span></span> <span data-ttu-id="2c090-131">e, per ogni servizio, sarà possibile eseguire in modo indipendente il controllo della versione e l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="2c090-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="2c090-132">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="2c090-132">Run the application</span></span>
<span data-ttu-id="2c090-133">Per avere un'idea di quanto è stato fatto, verrà ora distribuita la nuova applicazione ed esaminato il comportamento predefinito del modello API Web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="2c090-133">To get a sense of what we've done, let's deploy the new application and take a look at the default behavior that the ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="2c090-134">Premere F5 in Visual Studio per eseguire il debug dell'app.</span><span class="sxs-lookup"><span data-stu-id="2c090-134">Press F5 in Visual Studio to debug the app.</span></span>
2. <span data-ttu-id="2c090-135">Al termine della distribuzione Visual Studio avvia un browser nella radice del servizio API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2c090-135">When deployment is complete, Visual Studio launches a browser to the root of the ASP.NET Web API service.</span></span> <span data-ttu-id="2c090-136">Il modello API Web ASP.NET Core non prevede un comportamento predefinito per la radice, quindi nel browser viene visualizzato un errore 404.</span><span class="sxs-lookup"><span data-stu-id="2c090-136">The ASP.NET Core Web API template doesn't provide default behavior for the root, so you should see a 404 error in the browser.</span></span>
3. <span data-ttu-id="2c090-137">Aggiungere `/api/values` al percorso nel browser.</span><span class="sxs-lookup"><span data-stu-id="2c090-137">Add `/api/values` to the location in the browser.</span></span> <span data-ttu-id="2c090-138">Questa operazione chiama il metodo `Get` su ValuesController nel modello API Web</span><span class="sxs-lookup"><span data-stu-id="2c090-138">This invokes the `Get` method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="2c090-139">e restituisce la risposta predefinita trasmessa dal modello, una matrice JSON contenente due stringhe:</span><span class="sxs-lookup"><span data-stu-id="2c090-139">It returns the default response that is provided by the template--a JSON array that contains two strings:</span></span>
   
    ![Valori predefiniti restituiti dal modello API Web ASP.NET Core][browser-aspnet-template-values]
   
    <span data-ttu-id="2c090-141">Al termine dell'esercitazione questa pagina visualizza il valore del contatore più recente del servizio con stato anziché le stringhe predefinite.</span><span class="sxs-lookup"><span data-stu-id="2c090-141">By the end of the tutorial, this page will show the most recent counter value from our stateful service instead of the default strings.</span></span>

## <a name="connect-the-services"></a><span data-ttu-id="2c090-142">Connettere i servizi</span><span class="sxs-lookup"><span data-stu-id="2c090-142">Connect the services</span></span>
<span data-ttu-id="2c090-143">L'infrastruttura di servizi offre la massima flessibilità nella comunicazione con Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="2c090-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="2c090-144">In una singola applicazione possono coesistere servizi accessibili tramite TCP, altri tramite un'API REST HTTP e altri ancora tramite Web Socket.</span><span class="sxs-lookup"><span data-stu-id="2c090-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="2c090-145">Per informazioni sulle opzioni disponibili e sui compromessi necessari, vedere [Comunicazione con i servizi](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="2c090-145">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="2c090-146">In questa esercitazione si usa il [servizio remoto di Service Fabric](service-fabric-reliable-services-communication-remoting.md) disponibile nel SDK.</span><span class="sxs-lookup"><span data-stu-id="2c090-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in the SDK.</span></span>

<span data-ttu-id="2c090-147">Nell'approccio con servizio remoto, basato sulle chiamate Remote Procedure Call o RPC, viene definita un'interfaccia da usare come contratto pubblico per il servizio</span><span class="sxs-lookup"><span data-stu-id="2c090-147">In the Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface to act as the public contract for the service.</span></span> <span data-ttu-id="2c090-148">e quindi si usa tale interfaccia per generare una classe proxy per l'interazione con il servizio.</span><span class="sxs-lookup"><span data-stu-id="2c090-148">Then, you use that interface to generate a proxy class for interacting with the service.</span></span>

### <a name="create-the-remoting-interface"></a><span data-ttu-id="2c090-149">Creare l'interfaccia di comunicazione remota</span><span class="sxs-lookup"><span data-stu-id="2c090-149">Create the remoting interface</span></span>
<span data-ttu-id="2c090-150">Per iniziare si crea l'interfaccia da usare come contratto tra il servizio con stato e gli altri servizi, in questo caso il progetto Web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="2c090-150">Let's start by creating the interface to act as the contract between the stateful service and other services, in this case the ASP.NET Core web project.</span></span> <span data-ttu-id="2c090-151">Questa interfaccia deve essere condivisa da tutti i servizi che la usano per le chiamate RPC, pertanto va creata in un progetto Libreria di classi specifico.</span><span class="sxs-lookup"><span data-stu-id="2c090-151">This interface must be shared by all services that use it to make RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="2c090-152">In Esplora soluzioni fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Aggiungere** > **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="2c090-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="2c090-153">Scegliere la voce **Visual C#** nel riquadro di spostamento sinistro e quindi selezionare il modello **Libreria di classi**.</span><span class="sxs-lookup"><span data-stu-id="2c090-153">Choose the **Visual C#** entry in the left navigation pane and then select the **Class Library** template.</span></span> <span data-ttu-id="2c090-154">Verificare che la versione di .NET Framework sia impostata su **4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="2c090-154">Ensure that the .NET Framework version is set to **4.5.2**.</span></span>
   
    ![Creazione di un progetto interfaccia per il servizio con stato][vs-add-class-library-project]

3. <span data-ttu-id="2c090-156">Installare il pacchetto NuGet **Microsoft.ServiceFabric.Services.Remoting**.</span><span class="sxs-lookup"><span data-stu-id="2c090-156">Install the **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="2c090-157">Cercare **Microsoft.ServiceFabric.Services.Remoting** in Gestione pacchetti NuGet e installarlo per tutti i progetti della soluzione che usano il servizio remoto, tra cui:</span><span class="sxs-lookup"><span data-stu-id="2c090-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in the NuGet package manager and install it for all projects in the solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="2c090-158">Il progetto Libreria di classi che contiene l'interfaccia del servizio</span><span class="sxs-lookup"><span data-stu-id="2c090-158">The Class Library project that contains the service interface</span></span>
   - <span data-ttu-id="2c090-159">Il progetto di servizio con stato</span><span class="sxs-lookup"><span data-stu-id="2c090-159">The Stateful Service project</span></span>
   - <span data-ttu-id="2c090-160">Il progetto di servizio Web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2c090-160">The ASP.NET Core web service project</span></span>
   
    ![Aggiunta del pacchetto NuGet dei servizi][vs-services-nuget-package]

4. <span data-ttu-id="2c090-162">Nella libreria di classi creare un'interfaccia con un solo metodo, `GetCountAsync`, ed estendere l'interfaccia da `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="2c090-162">In the class library, create an interface with a single method, `GetCountAsync`, and extend the interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="2c090-163">L'interfaccia di comunicazione remota deve derivare da questa interfaccia, per indicare che si tratta di un'interfaccia di comunicazione remota del servizio.</span><span class="sxs-lookup"><span data-stu-id="2c090-163">The remoting interface must derive from this interface to indicate that it is a Service Remoting interface.</span></span>
   
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

### <a name="implement-the-interface-in-your-stateful-service"></a><span data-ttu-id="2c090-164">Implementare l'interfaccia nel servizio con stato</span><span class="sxs-lookup"><span data-stu-id="2c090-164">Implement the interface in your stateful service</span></span>
<span data-ttu-id="2c090-165">Dopo aver definito l'interfaccia, è ora necessario implementarla nel servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="2c090-165">Now that we have defined the interface, we need to implement it in the stateful service.</span></span>

1. <span data-ttu-id="2c090-166">Nel servizio con stato aggiungere un riferimento al progetto della libreria di classi contenente l'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2c090-166">In your stateful service, add a reference to the class library project that contains the interface.</span></span>
   
    ![Aggiunta di un riferimento al progetto libreria di classi nel servizio con stato][vs-add-class-library-reference]
2. <span data-ttu-id="2c090-168">Trovare la classe che eredita da `StatefulService`, ad esempio `MyStatefulService`, ed estenderla per implementare l'interfaccia `ICounter`.</span><span class="sxs-lookup"><span data-stu-id="2c090-168">Locate the class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it to implement the `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="2c090-169">Implementare ora il singolo metodo definito nell'interfaccia `ICounter`: `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="2c090-169">Now implement the single method that is defined in the `ICounter` interface, `GetCountAsync`.</span></span>
   
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

### <a name="expose-the-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="2c090-170">Esporre il servizio con stato usando un listener di comunicazione remota</span><span class="sxs-lookup"><span data-stu-id="2c090-170">Expose the stateful service using a service remoting listener</span></span>
<span data-ttu-id="2c090-171">Con l'interfaccia `ICounter` implementata, il passaggio finale è l'apertura del canale di comunicazione remota del servizio.</span><span class="sxs-lookup"><span data-stu-id="2c090-171">With the `ICounter` interface implemented, the final step is to open the Service Remoting communication channel.</span></span> <span data-ttu-id="2c090-172">Per i servizi con stato, Service Fabric offre un metodo sostituibile denominato `CreateServiceReplicaListeners`,</span><span class="sxs-lookup"><span data-stu-id="2c090-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="2c090-173">in cui è possibile specificare uno o più listener di comunicazione in base al tipo di comunicazione che si vuole abilitare per il servizio.</span><span class="sxs-lookup"><span data-stu-id="2c090-173">With this method, you can specify one or more communication listeners, based on the type of communication that you want to enable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="2c090-174">Il metodo equivalente per aprire un canale di comunicazione con i servizi senza stato è denominato `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="2c090-174">The equivalent method for opening a communication channel to stateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="2c090-175">In questo caso si sostituisce il metodo `CreateServiceReplicaListeners` esistente e si specifica un'istanza dell'oggetto `ServiceRemotingListener`, che crea un endpoint RPC chiamabile dai client tramite `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="2c090-175">In this case, we replace the existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="2c090-176">Il metodo di estensione `CreateServiceRemotingListener` sull'interfaccia `IService` consente di creare facilmente un `ServiceRemotingListener` con tutte le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="2c090-176">The `CreateServiceRemotingListener` extension method on the `IService` interface allows you to easily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="2c090-177">Per usare questo metodo di estensione verificare che sia stato importato lo spazio dei nomi `Microsoft.ServiceFabric.Services.Remoting.Runtime`.</span><span class="sxs-lookup"><span data-stu-id="2c090-177">To use this extension method, ensure you have the `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

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


### <a name="use-the-serviceproxy-class-to-interact-with-the-service"></a><span data-ttu-id="2c090-178">Usare la classe ServiceProxy per interagire con il servizio</span><span class="sxs-lookup"><span data-stu-id="2c090-178">Use the ServiceProxy class to interact with the service</span></span>
<span data-ttu-id="2c090-179">Il servizio con stato è ora pronto per ricevere traffico da altri servizi tramite RPC.</span><span class="sxs-lookup"><span data-stu-id="2c090-179">Our stateful service is now ready to receive traffic from other services over RPC.</span></span> <span data-ttu-id="2c090-180">e quindi non resta che aggiungere il codice per comunicare con esso dal servizio Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2c090-180">So all that remains is adding the code to communicate with it from the ASP.NET web service.</span></span>

1. <span data-ttu-id="2c090-181">Nel progetto ASP.NET aggiungere un riferimento alla libreria di classi contenente l'interfaccia `ICounter` .</span><span class="sxs-lookup"><span data-stu-id="2c090-181">In your ASP.NET project, add a reference to the class library that contains the `ICounter` interface.</span></span>

2. <span data-ttu-id="2c090-182">In precedenza è stato aggiunto al progetto ASP.NET il pacchetto NuGet **Microsoft.ServiceFabric.Services.Remoting**.</span><span class="sxs-lookup"><span data-stu-id="2c090-182">Earlier you added the **Microsoft.ServiceFabric.Services.Remoting** NuGet package to the ASP.NET project.</span></span> <span data-ttu-id="2c090-183">Questo pacchetto offre la classe `ServiceProxy` che consente di eseguire chiamate RPC al servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="2c090-183">This package provides the `ServiceProxy` class which you use to make RPC calls to the stateful service.</span></span> <span data-ttu-id="2c090-184">Verificare che questo pacchetto NuGet sia installato nel progetto di servizio Web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="2c090-184">Ensure this NuGet package is installed in the ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="2c090-185">Nella cartella **Controller** aprire la classe `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="2c090-185">In the **Controllers** folder, open the `ValuesController` class.</span></span> <span data-ttu-id="2c090-186">Si noti che il metodo `Get` restituisce attualmente solo una matrice di stringhe hardcoded con "value1" e "value2", che corrisponde a quanto visto in precedenza nel browser.</span><span class="sxs-lookup"><span data-stu-id="2c090-186">Note that the `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in the browser.</span></span> <span data-ttu-id="2c090-187">Sostituire l'implementazione con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2c090-187">Replace this implementation with the following code:</span></span>
   
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
   
    <span data-ttu-id="2c090-188">La prima riga del codice è quella più importante.</span><span class="sxs-lookup"><span data-stu-id="2c090-188">The first line of code is the key one.</span></span> <span data-ttu-id="2c090-189">Per creare il proxy ICounter per il servizio con stato, è necessario fornire due informazioni: un ID partizione e il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="2c090-189">To create the ICounter proxy to the stateful service, you need to provide two pieces of information: a partition ID and the name of the service.</span></span>
   
    <span data-ttu-id="2c090-190">Il partizionamento consente di ridimensionare i servizi con stato suddividendone lo stato in diversi bucket in base a una chiave definita, ad esempio l'ID cliente o il CAP.</span><span class="sxs-lookup"><span data-stu-id="2c090-190">You can use partitioning to scale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="2c090-191">In questa semplice applicazione la chiave non è importante, perché il servizio con stato ha una sola partizione</span><span class="sxs-lookup"><span data-stu-id="2c090-191">In our trivial application, the stateful service only has one partition, so the key doesn't matter.</span></span> <span data-ttu-id="2c090-192">e qualsiasi chiave specificata restituirà la stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="2c090-192">Any key that you provide will lead to the same partition.</span></span> <span data-ttu-id="2c090-193">Per altre informazioni sul partizionamento dei servizi, vedere [Partizionare Reliable Services di Service Fabric](service-fabric-concepts-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="2c090-193">To learn more about partitioning services, see [How to partition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="2c090-194">Il nome del servizio è un URI in formato fabric:/&lt;nome_applicazione&gt;/&lt;nome_servizio&gt;.</span><span class="sxs-lookup"><span data-stu-id="2c090-194">The service name is a URI of the form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="2c090-195">Con queste due informazioni, Service Fabric può identificare in modo univoco il computer a cui inviare le richieste.</span><span class="sxs-lookup"><span data-stu-id="2c090-195">With these two pieces of information, Service Fabric can uniquely identify the machine that requests should be sent to.</span></span> <span data-ttu-id="2c090-196">La classe `ServiceProxy` gestirà facilmente anche i casi in cui il computer che ospita la partizione del servizio con stato presenta un errore e un altro computer deve essere alzato di livello per sostituirlo.</span><span class="sxs-lookup"><span data-stu-id="2c090-196">The `ServiceProxy` class also seamlessly handles the case where the machine that hosts the stateful service partition fails and another machine must be promoted to take its place.</span></span> <span data-ttu-id="2c090-197">Questa astrazione semplifica notevolmente la scrittura di codice client per gestire gli altri servizi.</span><span class="sxs-lookup"><span data-stu-id="2c090-197">This abstraction makes writing the client code to deal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="2c090-198">Una volta che il proxy è disponibile, è sufficiente richiamare il metodo `GetCountAsync` e restituirne il risultato.</span><span class="sxs-lookup"><span data-stu-id="2c090-198">Once we have the proxy, we simply invoke the `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="2c090-199">Premere di nuovo F5 per eseguire l'applicazione modificata.</span><span class="sxs-lookup"><span data-stu-id="2c090-199">Press F5 again to run the modified application.</span></span> <span data-ttu-id="2c090-200">Come in precedenza, Visual Studio avvia automaticamente il browser nella radice del progetto Web.</span><span class="sxs-lookup"><span data-stu-id="2c090-200">As before, Visual Studio automatically launches the browser to the root of the web project.</span></span> <span data-ttu-id="2c090-201">Aggiungere il percorso "api/values" per visualizzare il valore del contatore attualmente restituito.</span><span class="sxs-lookup"><span data-stu-id="2c090-201">Add the "api/values" path, and you should see the current counter value returned.</span></span>
   
    ![Valore del contatore con stato visualizzato nel browser][browser-aspnet-counter-value]
   
    <span data-ttu-id="2c090-203">Aggiornare regolarmente il browser per visualizzare l'aggiornamento del valore del contatore.</span><span class="sxs-lookup"><span data-stu-id="2c090-203">Refresh the browser periodically to see the counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="2c090-204">Kestrel e WebListener</span><span class="sxs-lookup"><span data-stu-id="2c090-204">Kestrel and WebListener</span></span>

<span data-ttu-id="2c090-205">Il server Web ASP.NET Core predefinito, noto come Kestrel, [non è attualmente supportato per la gestione diretta del traffico Internet](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="2c090-205">The default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="2c090-206">Il modello del servizio senza stato ASP.NET Core per Service Fabric usa di conseguenza [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2c090-206">As a result, the ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="2c090-207">Per altre informazioni su Kestrel e WebListener nei servizi Service Fabric, fare riferimento all'articolo [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) (ASP.NET Core in Reliable Services di Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="2c090-207">To learn more about Kestrel and WebListener in Service Fabric services, please refer to [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-to-a-reliable-actor-service"></a><span data-ttu-id="2c090-208">Connessione a un servizio Reliable Actor</span><span class="sxs-lookup"><span data-stu-id="2c090-208">Connecting to a Reliable Actor service</span></span>
<span data-ttu-id="2c090-209">Questa esercitazione ha illustrato la procedura per aggiungere un front-end Web in grado di comunicare con un servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="2c090-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="2c090-210">Per comunicare con gli attori è possibile seguire un modello molto simile.</span><span class="sxs-lookup"><span data-stu-id="2c090-210">However, you can follow a very similar model to talk to actors.</span></span> <span data-ttu-id="2c090-211">Quando si crea un progetto Reliable Actor, Visual Studio genera automaticamente un progetto interfaccia.</span><span class="sxs-lookup"><span data-stu-id="2c090-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="2c090-212">È possibile usare tale interfaccia per generare un proxy attore nel progetto Web per comunicare con l'attore.</span><span class="sxs-lookup"><span data-stu-id="2c090-212">You can use that interface to generate an actor proxy in the web project to communicate with the actor.</span></span> <span data-ttu-id="2c090-213">Poiché il canale di comunicazione viene fornito automaticamente,</span><span class="sxs-lookup"><span data-stu-id="2c090-213">The communication channel is provided automatically.</span></span> <span data-ttu-id="2c090-214">non è necessario eseguire operazioni, ad esempio stabilire un oggetto `ServiceRemotingListener`, come per il servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="2c090-214">So you do not need to do anything that is equivalent to establishing a `ServiceRemotingListener` like you did for the stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="2c090-215">Funzionamento dei servizi Web in un cluster locale</span><span class="sxs-lookup"><span data-stu-id="2c090-215">How web services work on your local cluster</span></span>
<span data-ttu-id="2c090-216">In generale è possibile distribuire esattamente la stessa applicazione Service Fabric anche in un cluster con più computer distribuito nel cluster locale con la certezza che funzionerà come previsto,</span><span class="sxs-lookup"><span data-stu-id="2c090-216">In general, you can deploy exactly the same Service Fabric application to a multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="2c090-217">perché il cluster locale è semplicemente una configurazione a cinque nodi compressa in un solo computer.</span><span class="sxs-lookup"><span data-stu-id="2c090-217">This is because your local cluster is simply a five-node configuration that is collapsed to a single machine.</span></span>

<span data-ttu-id="2c090-218">Quando si tratta di servizi Web, tuttavia, c'è una sola possibilità.</span><span class="sxs-lookup"><span data-stu-id="2c090-218">When it comes to web services, however, there is one key nuance.</span></span> <span data-ttu-id="2c090-219">Quando il cluster si trova dietro un servizio di bilanciamento del carico, come in Azure, è necessario assicurarsi che i servizi Web vengano distribuiti in ogni computer, perché il servizio di bilanciamento del carico si limita a eseguire il round robin del traffico tra i computer.</span><span class="sxs-lookup"><span data-stu-id="2c090-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since the load balancer simply round-robins traffic across the machines.</span></span> <span data-ttu-id="2c090-220">A tale scopo, è possibile impostare `InstanceCount` per il servizio sul valore speciale "-1".</span><span class="sxs-lookup"><span data-stu-id="2c090-220">You can do this by setting the `InstanceCount` for the service to the special value of "-1".</span></span>

<span data-ttu-id="2c090-221">Quando invece si esegue il servizio Web in locale, è necessario assicurarsi che solo un'istanza del servizio sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2c090-221">By contrast, when you run a web service locally, you need to ensure that only one instance of the service is running.</span></span> <span data-ttu-id="2c090-222">In caso contrario si verificano conflitti tra più processi in ascolto sullo stesso percorso e sulla stessa porta.</span><span class="sxs-lookup"><span data-stu-id="2c090-222">Otherwise, you run into conflicts from multiple processes that are listening on the same path and port.</span></span> <span data-ttu-id="2c090-223">Per le distribuzioni locali, quindi, è opportuno impostare il numero delle istanze del servizio Web su 1.</span><span class="sxs-lookup"><span data-stu-id="2c090-223">As a result, the web service instance count should be set to "1" for local deployments.</span></span>

<span data-ttu-id="2c090-224">Per informazioni su come configurare valori diversi a seconda dell'ambiente, vedere [Gestione dei parametri dell'applicazione per più ambienti](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="2c090-224">To learn how to configure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c090-225">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2c090-225">Next steps</span></span>
<span data-ttu-id="2c090-226">Dopo l'impostazione del front-end Web per l'applicazione con ASP.NET Core, vedere altre informazioni su [ASP.NET Core in Reliable Services di Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md) per un esame dettagliato dell'interazione tra ASP.NET Core e Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2c090-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="2c090-227">[Altre informazioni sulla comunicazione tra servizi](service-fabric-connect-and-communicate-with-services.md) in generale sono disponibili per completare il quadro del funzionamento della comunicazione tra servizi in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2c090-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general to get a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="2c090-228">Dopo avere acquisito una buona comprensione del funzionamento della comunicazione tra servizi, [creare un cluster in Azure e distribuire la propria applicazione nel cloud](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2c090-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application to the cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

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
