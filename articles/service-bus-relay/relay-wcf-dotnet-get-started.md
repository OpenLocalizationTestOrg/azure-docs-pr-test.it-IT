---
title: Introduzione all'inoltro WCF di Inoltro di Azure in .NET | Documentazione Microsoft
description: Informazioni sull'uso degli inoltri WCF di Inoltro di Azure per connettere due applicazioni ospitate in posizioni diverse.
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 1af1ac78398d65e6a87f0d24d6198f3dfbc82ffd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="217b6-103">Come usare gli inoltri WCF di Inoltro di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="217b6-103">How to use Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="217b6-104">Questo articolo descrive come usare il servizio di inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="217b6-104">This article describes how to use the Azure Relay service.</span></span> <span data-ttu-id="217b6-105">Negli esempi, scritti in C#, viene usata l'API di Windows Communication Foundation (WCF) con le estensioni contenute nell'assembly del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="217b6-105">The samples are written in C# and use the Windows Communication Foundation (WCF) API with extensions contained in the Service Bus assembly.</span></span> <span data-ttu-id="217b6-106">Per altre informazioni, vedere la [panoramica del servizio di inoltro di Azure](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="217b6-106">For more information about Azure relay, see the [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="217b6-107">Informazioni sull'inoltro WCF</span><span class="sxs-lookup"><span data-stu-id="217b6-107">What is WCF Relay?</span></span>

<span data-ttu-id="217b6-108">Il servizio di [*inoltro WCF*](relay-what-is-it.md) di Azure consente di creare applicazioni ibride eseguite sia in un data center di Azure che nell'ambiente aziendale locale.</span><span class="sxs-lookup"><span data-stu-id="217b6-108">The Azure [*WCF Relay*](relay-what-is-it.md) service enables you to build hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="217b6-109">Il servizio di inoltro facilita questo compito consentendo di esporre in modo sicuro nel cloud pubblico i servizi WCF (Windows Communication Foundation) che risiedono in una rete aziendale senza dover aprire una connessione firewall o richiedere modifiche di notevole impatto a un'infrastruttura di rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="217b6-109">The relay service facilitates this by enabling you to securely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or requiring intrusive changes to a corporate network infrastructure.</span></span>

![Concetti sull'inoltro con WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="217b6-111">Il servizio di inoltro di Azure consente di ospitare servizi WCF nell'ambiente aziendale esistente.</span><span class="sxs-lookup"><span data-stu-id="217b6-111">Azure Relay enables you to host WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="217b6-112">È quindi possibile delegare l'ascolto delle sessioni e delle richieste in ingresso per questi servizi WCF al servizio di inoltro in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="217b6-112">You can then delegate listening for incoming sessions and requests to these WCF services to the relay service running within Azure.</span></span> <span data-ttu-id="217b6-113">In questo modo è possibile esporre tali servizi al codice dell'applicazione in esecuzione in Azure oppure ad ambienti destinati a personale che accede da dispositivi mobili o a partner che accedono tramite Extranet.</span><span class="sxs-lookup"><span data-stu-id="217b6-113">This enables you to expose these services to application code running in Azure, or to mobile workers or extranet partner environments.</span></span> <span data-ttu-id="217b6-114">Il servizio di inoltro consente di controllare in modo sicuro ed estremamente dettagliato quali utenti possono accedere ai servizi.</span><span class="sxs-lookup"><span data-stu-id="217b6-114">Relay enables you to securely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="217b6-115">È uno strumento efficace e sicuro per esporre dati e funzionalità dell'applicazione dalle soluzioni aziendali esistenti e di sfruttarle dal cloud.</span><span class="sxs-lookup"><span data-stu-id="217b6-115">It provides a powerful and secure way to expose application functionality and data from your existing enterprise solutions and take advantage of it from the cloud.</span></span>

<span data-ttu-id="217b6-116">Questo articolo illustra come usare il servizio di inoltro di Azure per creare un servizio Web WCF, esposto con un'associazione di canale TCP, che implementa una conversazione sicura tra due parti.</span><span class="sxs-lookup"><span data-stu-id="217b6-116">This article discusses how to use Azure Relay to create a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-the-service-bus-nuget-package"></a><span data-ttu-id="217b6-117">Ottenere il pacchetto NuGet del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="217b6-117">Get the Service Bus NuGet package</span></span>
<span data-ttu-id="217b6-118">Il [pacchetto NuGet del bus di servizio](https://www.nuget.org/packages/WindowsAzure.ServiceBus) è il modo più semplice per recuperare l'API del bus di servizio e configurare l'applicazione con tutte le dipendenze di tale servizio.</span><span class="sxs-lookup"><span data-stu-id="217b6-118">The [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is the easiest way to get the Service Bus API and to configure your application with all of the Service Bus dependencies.</span></span> <span data-ttu-id="217b6-119">Per installare il pacchetto NuGet nel progetto, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="217b6-119">To install the NuGet package in your project, do the following:</span></span>

1. <span data-ttu-id="217b6-120">In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="217b6-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="217b6-121">Cercare "Bus di servizio" e selezionare la voce **Bus di servizio di Microsoft Azure** .</span><span class="sxs-lookup"><span data-stu-id="217b6-121">Search for "Service Bus" and select the **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="217b6-122">Fare clic su **Installa** per completare l'installazione e alla fine chiudere la finestra di dialogo successiva:</span><span class="sxs-lookup"><span data-stu-id="217b6-122">Click **Install** to complete the installation, then close the following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="217b6-123">Esporre e utilizzare un servizio Web SOAP con TCP</span><span class="sxs-lookup"><span data-stu-id="217b6-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="217b6-124">Per esporre un servizio Web SOAP WCF esistente per l'utilizzo esterno, è necessario apportare modifiche alle associazioni e agli indirizzi del servizio.</span><span class="sxs-lookup"><span data-stu-id="217b6-124">To expose an existing WCF SOAP web service for external consumption, you must make changes to the service bindings and addresses.</span></span> <span data-ttu-id="217b6-125">A seconda di come sono stati installati e configurati i servizi WCF, potrebbe essere necessario modificare il file di configurazione o il codice.</span><span class="sxs-lookup"><span data-stu-id="217b6-125">This may require changes to your configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="217b6-126">Si noti che WCF consente di usare più endpoint di rete con lo stesso servizio, quindi è possibile mantenere gli endpoint interni esistenti aggiungendo al tempo stesso endpoint di inoltro per l'accesso esterno.</span><span class="sxs-lookup"><span data-stu-id="217b6-126">Note that WCF allows you to have multiple network endpoints over the same service, so you can retain the existing internal endpoints while adding relay endpoints for external access at the same time.</span></span>

<span data-ttu-id="217b6-127">In questa attività si crea un semplice servizio WCF e si aggiunge un listener di inoltro a tale servizio.</span><span class="sxs-lookup"><span data-stu-id="217b6-127">In this task, you build a simple WCF service and add a relay listener to it.</span></span> <span data-ttu-id="217b6-128">Per questo esercizio si presuppone una certa conoscenza di Visual Studio, pertanto non è inclusa una spiegazione dettagliata della procedura di creazione di un progetto,</span><span class="sxs-lookup"><span data-stu-id="217b6-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all the details of creating a project.</span></span> <span data-ttu-id="217b6-129">ma l'attenzione è rivolta principalmente al codice.</span><span class="sxs-lookup"><span data-stu-id="217b6-129">Instead, it focuses on the code.</span></span>

<span data-ttu-id="217b6-130">Prima di iniziare, completare questa procedura per configurare l'ambiente:</span><span class="sxs-lookup"><span data-stu-id="217b6-130">Before starting these steps, complete the following procedure to set up your environment:</span></span>

1. <span data-ttu-id="217b6-131">In Visual Studio creare un'applicazione console contenente due progetti, "Client" e "Service", all'interno della soluzione.</span><span class="sxs-lookup"><span data-stu-id="217b6-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within the solution.</span></span>
2. <span data-ttu-id="217b6-132">Aggiungere il pacchetto NuGet del bus di servizio a entrambi i progetti.</span><span class="sxs-lookup"><span data-stu-id="217b6-132">Add the Service Bus NuGet package to both projects.</span></span> <span data-ttu-id="217b6-133">Questo pacchetto aggiunge ai progetti tutti i riferimenti ad assembly necessari.</span><span class="sxs-lookup"><span data-stu-id="217b6-133">This package adds all the necessary assembly references to your projects.</span></span>

### <a name="how-to-create-the-service"></a><span data-ttu-id="217b6-134">Come creare il servizio</span><span class="sxs-lookup"><span data-stu-id="217b6-134">How to create the service</span></span>
<span data-ttu-id="217b6-135">Creare innanzitutto il servizio stesso.</span><span class="sxs-lookup"><span data-stu-id="217b6-135">First, create the service itself.</span></span> <span data-ttu-id="217b6-136">Tutti i servizi WCF sono costituiti da almeno tre parti distinte:</span><span class="sxs-lookup"><span data-stu-id="217b6-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="217b6-137">Definizione di un contratto che descrive i messaggi da scambiare e le operazioni da richiamare.</span><span class="sxs-lookup"><span data-stu-id="217b6-137">Definition of a contract that describes what messages are exchanged and what operations are to be invoked.</span></span>
* <span data-ttu-id="217b6-138">Implementazione di tale contratto.</span><span class="sxs-lookup"><span data-stu-id="217b6-138">Implementation of that contract.</span></span>
* <span data-ttu-id="217b6-139">Host che ospita il servizio WCF ed espone diversi endpoint.</span><span class="sxs-lookup"><span data-stu-id="217b6-139">Host that hosts the WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="217b6-140">Negli esempi di codice di questa sezione vengono trattati singolarmente tutti questi componenti.</span><span class="sxs-lookup"><span data-stu-id="217b6-140">The code examples in this section address each of these components.</span></span>

<span data-ttu-id="217b6-141">Il contratto consente di definire una singola operazione, `AddNumbers`, che somma due numeri e restituisce il risultato.</span><span class="sxs-lookup"><span data-stu-id="217b6-141">The contract defines a single operation, `AddNumbers`, that adds two numbers and returns the result.</span></span> <span data-ttu-id="217b6-142">L'interfaccia `IProblemSolverChannel` consente al client di gestire più facilmente la durata del proxy.</span><span class="sxs-lookup"><span data-stu-id="217b6-142">The `IProblemSolverChannel` interface enables the client to more easily manage the proxy lifetime.</span></span> <span data-ttu-id="217b6-143">La creazione di tale interfaccia rientra tra le procedure consigliate.</span><span class="sxs-lookup"><span data-stu-id="217b6-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="217b6-144">È opportuno inserire questa definizione del contratto in un file separato in modo da potervi fare riferimento da entrambi i progetti "Client" e "Service", ma è comunque possibile copiare il codice in entrambi i progetti.</span><span class="sxs-lookup"><span data-stu-id="217b6-144">It's a good idea to put this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy the code into both projects.</span></span>

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

<span data-ttu-id="217b6-145">Dopo che il contratto è stato definito, l'implementazione è la seguente:</span><span class="sxs-lookup"><span data-stu-id="217b6-145">With the contract in place, the implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="217b6-146">Configurare un host del servizio a livello di codice</span><span class="sxs-lookup"><span data-stu-id="217b6-146">Configure a service host programmatically</span></span>
<span data-ttu-id="217b6-147">Una volta definiti il contratto e l'implementazione, è ora possibile ospitare il servizio.</span><span class="sxs-lookup"><span data-stu-id="217b6-147">With the contract and implementation in place, you can now host the service.</span></span> <span data-ttu-id="217b6-148">L'hosting viene eseguito all'interno di un oggetto [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx), che si occupa della gestione delle istanze del servizio e ospita gli endpoint che sono in ascolto dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="217b6-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of the service and hosts the endpoints that listen for messages.</span></span> <span data-ttu-id="217b6-149">Il codice seguente configura il servizio sia con un normale endpoint locale che con un endpoint di inoltro per illustrare come si presentano gli endpoint interni ed esterni affiancati.</span><span class="sxs-lookup"><span data-stu-id="217b6-149">The following code configures the service with both a regular local endpoint and a relay endpoint to illustrate the appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="217b6-150">Sostituire la stringa *namespace* con il nome dello spazio dei nomi e *yourKey* con la chiave SAS ottenuta nel passaggio di impostazione precedente.</span><span class="sxs-lookup"><span data-stu-id="217b6-150">Replace the string *namespace* with your namespace name and *yourKey* with the SAS key that you obtained in the previous setup step.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER to close");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="217b6-151">Nell'esempio vengono creati due endpoint inclusi nella stessa implementazione del contratto:</span><span class="sxs-lookup"><span data-stu-id="217b6-151">In the example, you create two endpoints that are on the same contract implementation.</span></span> <span data-ttu-id="217b6-152">Uno è locale e uno viene proiettato tramite il servizio di inoltro.</span><span class="sxs-lookup"><span data-stu-id="217b6-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="217b6-153">Le differenze principali tra di essi sono costituite dalle associazioni: [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) per l'endpoint locale e [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) per l'endpoint e gli indirizzi di inoltro.</span><span class="sxs-lookup"><span data-stu-id="217b6-153">The key differences between them are the bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for the local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for the relay endpoint and the addresses.</span></span> <span data-ttu-id="217b6-154">L'endpoint locale è dotato di un indirizzo di rete locale con una porta distinta.</span><span class="sxs-lookup"><span data-stu-id="217b6-154">The local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="217b6-155">L'endpoint di inoltro ha un indirizzo costituito dalla stringa `sb`, dal nome dello spazio dei nomi e dal percorso "solver".</span><span class="sxs-lookup"><span data-stu-id="217b6-155">The relay endpoint has an endpoint address composed of the string `sb`, your namespace name, and the path "solver."</span></span> <span data-ttu-id="217b6-156">Si ottiene così l'URI `sb://[serviceNamespace].servicebus.windows.net/solver`, che identifica l'endpoint del servizio come endpoint TCP (di inoltro) del bus di servizio con nome DNS esterno completo.</span><span class="sxs-lookup"><span data-stu-id="217b6-156">This results in the URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying the service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="217b6-157">Se si inserisce il codice sostituendo i segnaposto nella funzione `Main` dell'applicazione **Service**, si otterrà un servizio funzionante.</span><span class="sxs-lookup"><span data-stu-id="217b6-157">If you place the code replacing the placeholders into the `Main` function of the **Service** application, you will have a functional service.</span></span> <span data-ttu-id="217b6-158">Se si vuole che il servizio sia in ascolto esclusivamente sull'inoltro, rimuovere la dichiarazione dell'endpoint locale.</span><span class="sxs-lookup"><span data-stu-id="217b6-158">If you want your service to listen exclusively on the relay, remove the local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-the-appconfig-file"></a><span data-ttu-id="217b6-159">Come configurare un host del servizio nel file App.config</span><span class="sxs-lookup"><span data-stu-id="217b6-159">Configure a service host in the App.config file</span></span>
<span data-ttu-id="217b6-160">È anche possibile configurare l'host usando il file App.config.</span><span class="sxs-lookup"><span data-stu-id="217b6-160">You can also configure the host using the App.config file.</span></span> <span data-ttu-id="217b6-161">L'esempio seguente in questo caso visualizza il codice del servizio di hosting.</span><span class="sxs-lookup"><span data-stu-id="217b6-161">The service hosting code in this case appears in the next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER to close");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="217b6-162">Le definizioni dell'endpoint vengono spostate nel file App.config.</span><span class="sxs-lookup"><span data-stu-id="217b6-162">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="217b6-163">Il pacchetto NuGet ha già aggiunto al file App.config una serie di definizioni, che sono le estensioni di configurazione necessarie per il servizio di inoltro.</span><span class="sxs-lookup"><span data-stu-id="217b6-163">The NuGet package has already added a range of definitions to the App.config file, which are the required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="217b6-164">L'esempio seguente, che è l'esatto equivalente di quello riportato in precedenza, deve essere inserito direttamente sotto l'elemento **system.serviceModel**.</span><span class="sxs-lookup"><span data-stu-id="217b6-164">The following example, which is the exact equivalent of the previous code, should appear directly beneath the **system.serviceModel** element.</span></span> <span data-ttu-id="217b6-165">In questo esempio di codice si presuppone che il nome dello spazio dei nomi del progetto C# sia **Service**.</span><span class="sxs-lookup"><span data-stu-id="217b6-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="217b6-166">Sostituire i segnaposto con la chiave di firma di accesso condiviso e il nome dello spazio dei nomi dell'inoltro.</span><span class="sxs-lookup"><span data-stu-id="217b6-166">Replace the placeholders with your relay namespace name and SAS key.</span></span>

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

<span data-ttu-id="217b6-167">Dopo aver apportato queste modifiche, il servizio viene avviato come in precedenza, ma con due endpoint dinamici, uno locale e l'altro in ascolto nel cloud.</span><span class="sxs-lookup"><span data-stu-id="217b6-167">After you make these changes, the service starts as it did before, but with two live endpoints: one local and one listening in the cloud.</span></span>

### <a name="create-the-client"></a><span data-ttu-id="217b6-168">Creare il client</span><span class="sxs-lookup"><span data-stu-id="217b6-168">Create the client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="217b6-169">Configurare un client a livello di codice</span><span class="sxs-lookup"><span data-stu-id="217b6-169">Configure a client programmatically</span></span>
<span data-ttu-id="217b6-170">Per usare il servizio, è possibile costruire un client WCF tramite un oggetto [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx).</span><span class="sxs-lookup"><span data-stu-id="217b6-170">To consume the service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="217b6-171">Il bus di servizio usa un modello di sicurezza basato sui token implementato tramite la firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="217b6-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="217b6-172">La classe [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) rappresenta un provider di token di sicurezza con metodi factory incorporati che restituiscono alcuni provider di token noti.</span><span class="sxs-lookup"><span data-stu-id="217b6-172">The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="217b6-173">L'esempio seguente usa il metodo [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) per gestire l'acquisizione del token SAS appropriato.</span><span class="sxs-lookup"><span data-stu-id="217b6-173">The following example uses the [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method to handle the acquisition of the appropriate SAS token.</span></span> <span data-ttu-id="217b6-174">Il nome e la chiave sono quelli ottenuti dal portale come descritto nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="217b6-174">The name and key are those obtained from the portal as described in the previous section.</span></span>

<span data-ttu-id="217b6-175">In primo luogo, fare riferimento o copiare nel progetto client il codice del contratto `IProblemSolver` del servizio.</span><span class="sxs-lookup"><span data-stu-id="217b6-175">First, reference or copy the `IProblemSolver` contract code from the service into your client project.</span></span>

<span data-ttu-id="217b6-176">Sostituire quindi il codice nel metodo `Main` del client, anche in questo caso sostituendo il testo segnaposto con la chiave di firma di accesso condiviso e lo spazio dei nomi dell'inoltro.</span><span class="sxs-lookup"><span data-stu-id="217b6-176">Then, replace the code in the `Main` method of the client, again replacing the placeholder text with your relay namespace and SAS key.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="217b6-177">È ora possibile compilare il client e il servizio ed eseguirli (con il servizio per primo), in modo che il client chiami il servizio e visualizzi **9**.</span><span class="sxs-lookup"><span data-stu-id="217b6-177">You can now build the client and the service, run them (run the service first), and the client calls the service and prints **9**.</span></span> <span data-ttu-id="217b6-178">È possibile eseguire il client e il server in computer diversi, persino in reti diverse, senza riscontrare problemi di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="217b6-178">You can run the client and server on different machines, even across networks, and the communication will still work.</span></span> <span data-ttu-id="217b6-179">Il codice client può inoltre essere eseguito nel cloud o in locale.</span><span class="sxs-lookup"><span data-stu-id="217b6-179">The client code can also run in the cloud or locally.</span></span>

#### <a name="configure-a-client-in-the-appconfig-file"></a><span data-ttu-id="217b6-180">Configurare un client nel file App.config</span><span class="sxs-lookup"><span data-stu-id="217b6-180">Configure a client in the App.config file</span></span>
<span data-ttu-id="217b6-181">Il codice seguente illustra come configurare il client usando il file App.config.</span><span class="sxs-lookup"><span data-stu-id="217b6-181">The following code shows how to configure the client using the App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="217b6-182">Le definizioni dell'endpoint vengono spostate nel file App.config.</span><span class="sxs-lookup"><span data-stu-id="217b6-182">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="217b6-183">L'esempio seguente, che è identico al codice riportato in precedenza, deve essere inserito direttamente sotto l'elemento `<system.serviceModel>`.</span><span class="sxs-lookup"><span data-stu-id="217b6-183">The following example, which is the same as the code listed previously, should appear directly beneath the `<system.serviceModel>` element.</span></span> <span data-ttu-id="217b6-184">Anche in questo caso, come in precedenza, è necessario sostituire i segnaposto con la chiave di firma di accesso condiviso e lo spazio dei nomi dell'inoltro.</span><span class="sxs-lookup"><span data-stu-id="217b6-184">Here, as before, you must replace the placeholders with your relay namespace and SAS key.</span></span>

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a><span data-ttu-id="217b6-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="217b6-185">Next steps</span></span>
<span data-ttu-id="217b6-186">A questo punto, dopo aver appreso le nozioni di base del servizio di inoltro di Azure, selezionare i collegamenti seguenti per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="217b6-186">Now that you've learned the basics of Azure Relay, follow these links to learn more.</span></span>

* [<span data-ttu-id="217b6-187">Che cos'è il servizio di inoltro di Azure?</span><span class="sxs-lookup"><span data-stu-id="217b6-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="217b6-188">Panoramica dell'architettura del bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="217b6-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="217b6-189">Scaricare esempi del bus di servizio da [Esempi di Azure][Azure samples] o vedere la [panoramica degli esempi del bus di servizio][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="217b6-189">Download Service Bus samples from [Azure samples][Azure samples] or see the [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
