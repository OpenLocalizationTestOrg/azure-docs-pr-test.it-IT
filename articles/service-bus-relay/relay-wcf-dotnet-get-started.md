---
title: aaaGet avviato con gli inoltri Azure inoltro WCF in .NET | Documenti Microsoft
description: Informazioni su come toouse Azure inoltro WCF inoltra tooconnect due applicazioni ospitate in posizioni diverse.
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
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="6a07b-103">Come Azure inoltro WCF toouse degli inoltri con .NET</span><span class="sxs-lookup"><span data-stu-id="6a07b-103">How toouse Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="6a07b-104">In questo articolo viene descritto come toouse hello servizio di inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a07b-104">This article describes how toouse hello Azure Relay service.</span></span> <span data-ttu-id="6a07b-105">esempi di Hello vengono scritti in c# e usano API di Windows Communication Foundation (WCF) hello con estensioni contenute in assembly di Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-105">hello samples are written in C# and use hello Windows Communication Foundation (WCF) API with extensions contained in hello Service Bus assembly.</span></span> <span data-ttu-id="6a07b-106">Per ulteriori informazioni sull'inoltro di Azure, vedere hello [Cenni preliminari su Azure Relay](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="6a07b-106">For more information about Azure relay, see hello [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="6a07b-107">Informazioni sull'inoltro WCF</span><span class="sxs-lookup"><span data-stu-id="6a07b-107">What is WCF Relay?</span></span>

<span data-ttu-id="6a07b-108">Hello Azure [ *inoltro WCF* ](relay-what-is-it.md) servizio consente di applicazioni ibride toobuild eseguiti in un Data Center di Azure sia ambiente aziendale locale.</span><span class="sxs-lookup"><span data-stu-id="6a07b-108">hello Azure [*WCF Relay*](relay-what-is-it.md) service enables you toobuild hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="6a07b-109">il servizio di inoltro Hello facilita questo consentendo toosecurely espongono i servizi Windows Communication Foundation (WCF) che si trovano all'interno di un'organizzazione aziendale rete toohello pubblica cloud senza la necessità di una connessione firewall tooopen, o che richiedono infrastruttura della rete aziendale tooa modifiche intrusiva.</span><span class="sxs-lookup"><span data-stu-id="6a07b-109">hello relay service facilitates this by enabling you toosecurely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or requiring intrusive changes tooa corporate network infrastructure.</span></span>

![Concetti sull'inoltro con WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="6a07b-111">Inoltro di Azure permette di servizi WCF toohost nell'ambiente aziendale esistente.</span><span class="sxs-lookup"><span data-stu-id="6a07b-111">Azure Relay enables you toohost WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="6a07b-112">È quindi possibile delegare l'ascolto di arrivo sessioni e richieste toothese servizi toohello servizio di inoltro WCF in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="6a07b-112">You can then delegate listening for incoming sessions and requests toothese WCF services toohello relay service running within Azure.</span></span> <span data-ttu-id="6a07b-113">In questo modo si tooexpose codice di tooapplication questi servizi in esecuzione in Azure, o thread di lavoro toomobile o ambienti di partner extranet.</span><span class="sxs-lookup"><span data-stu-id="6a07b-113">This enables you tooexpose these services tooapplication code running in Azure, or toomobile workers or extranet partner environments.</span></span> <span data-ttu-id="6a07b-114">Inoltro consente di controllare toosecurely chi può accedere ai servizi a un livello con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="6a07b-114">Relay enables you toosecurely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="6a07b-115">Fornisce una funzionalità dell'applicazione tooexpose sistema efficiente e sicuro e i dati dalle soluzioni aziendali esistenti e sfruttare il dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-115">It provides a powerful and secure way tooexpose application functionality and data from your existing enterprise solutions and take advantage of it from hello cloud.</span></span>

<span data-ttu-id="6a07b-116">Questo articolo illustra come toouse Azure inoltro toocreate un servizio web WCF, esposte tramite un'associazione di canale TCP, che implementa una conversazione protetta tra due parti.</span><span class="sxs-lookup"><span data-stu-id="6a07b-116">This article discusses how toouse Azure Relay toocreate a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a><span data-ttu-id="6a07b-117">Ottenere il pacchetto NuGet di Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="6a07b-117">Get hello Service Bus NuGet package</span></span>
<span data-ttu-id="6a07b-118">Hello [pacchetto NuGet di Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus) è hello più semplice modo tooget hello API del Bus di servizio e tooconfigure l'applicazione con tutte le dipendenze di hello Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="6a07b-118">hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is hello easiest way tooget hello Service Bus API and tooconfigure your application with all of hello Service Bus dependencies.</span></span> <span data-ttu-id="6a07b-119">pacchetto NuGet di hello tooinstall nel progetto, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a07b-119">tooinstall hello NuGet package in your project, do hello following:</span></span>

1. <span data-ttu-id="6a07b-120">In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6a07b-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="6a07b-121">Ricerca di "Bus di servizio" e seleziona hello **Microsoft Azure Service Bus** elemento.</span><span class="sxs-lookup"><span data-stu-id="6a07b-121">Search for "Service Bus" and select hello **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="6a07b-122">Fare clic su **installare** toocomplete hello installazione, quindi chiudere la finestra di dialogo seguente hello:</span><span class="sxs-lookup"><span data-stu-id="6a07b-122">Click **Install** toocomplete hello installation, then close hello following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="6a07b-123">Esporre e utilizzare un servizio Web SOAP con TCP</span><span class="sxs-lookup"><span data-stu-id="6a07b-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="6a07b-124">tooexpose un servizio web SOAP WCF esistente per l'utilizzo esterno, è necessario apportare modifiche toohello servizio associazioni e gli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="6a07b-124">tooexpose an existing WCF SOAP web service for external consumption, you must make changes toohello service bindings and addresses.</span></span> <span data-ttu-id="6a07b-125">Potrebbe essere necessario il file di configurazione tooyour modifiche o potrebbe richiedere modifiche al codice, a seconda di come è impostato e configurato i servizi WCF.</span><span class="sxs-lookup"><span data-stu-id="6a07b-125">This may require changes tooyour configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="6a07b-126">Si noti che WCF consente toohave più endpoint di rete su hello stesso servizio, in modo da mantenere hello esistente endpoint interni durante l'aggiunta di endpoint di inoltro per esterno accedere in hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="6a07b-126">Note that WCF allows you toohave multiple network endpoints over hello same service, so you can retain hello existing internal endpoints while adding relay endpoints for external access at hello same time.</span></span>

<span data-ttu-id="6a07b-127">In questa attività, compilare un semplice servizio WCF e aggiungere un tooit di listener di inoltro.</span><span class="sxs-lookup"><span data-stu-id="6a07b-127">In this task, you build a simple WCF service and add a relay listener tooit.</span></span> <span data-ttu-id="6a07b-128">Questo esercizio si presuppone la conoscenza di Visual Studio e pertanto non analizzerà tutti i dettagli di hello di creazione di un progetto.</span><span class="sxs-lookup"><span data-stu-id="6a07b-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all hello details of creating a project.</span></span> <span data-ttu-id="6a07b-129">Si concentra invece sul codice hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-129">Instead, it focuses on hello code.</span></span>

<span data-ttu-id="6a07b-130">Prima di iniziare questa procedura, completare hello seguendo procedure tooset dell'ambiente:</span><span class="sxs-lookup"><span data-stu-id="6a07b-130">Before starting these steps, complete hello following procedure tooset up your environment:</span></span>

1. <span data-ttu-id="6a07b-131">In Visual Studio, creare un'applicazione console che contiene due progetti, "Client" e "Servizio", all'interno di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within hello solution.</span></span>
2. <span data-ttu-id="6a07b-132">Aggiungere progetti tooboth pacchetto NuGet di Service Bus di hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-132">Add hello Service Bus NuGet package tooboth projects.</span></span> <span data-ttu-id="6a07b-133">Questo pacchetto aggiunge tutti i progetti di tooyour i riferimenti di assembly necessari hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-133">This package adds all hello necessary assembly references tooyour projects.</span></span>

### <a name="how-toocreate-hello-service"></a><span data-ttu-id="6a07b-134">Come toocreate hello servizio</span><span class="sxs-lookup"><span data-stu-id="6a07b-134">How toocreate hello service</span></span>
<span data-ttu-id="6a07b-135">Innanzitutto, creare il servizio hello stesso.</span><span class="sxs-lookup"><span data-stu-id="6a07b-135">First, create hello service itself.</span></span> <span data-ttu-id="6a07b-136">Tutti i servizi WCF sono costituiti da almeno tre parti distinte:</span><span class="sxs-lookup"><span data-stu-id="6a07b-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="6a07b-137">Definizione di un contratto che descrive i messaggi vengono scambiati e quali operazioni sono toobe richiamato.</span><span class="sxs-lookup"><span data-stu-id="6a07b-137">Definition of a contract that describes what messages are exchanged and what operations are toobe invoked.</span></span>
* <span data-ttu-id="6a07b-138">Implementazione di tale contratto.</span><span class="sxs-lookup"><span data-stu-id="6a07b-138">Implementation of that contract.</span></span>
* <span data-ttu-id="6a07b-139">Host che ospita il servizio WCF hello ed espone più endpoint.</span><span class="sxs-lookup"><span data-stu-id="6a07b-139">Host that hosts hello WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="6a07b-140">esempi di codice Hello in questa sezione indirizzo ognuno di questi componenti.</span><span class="sxs-lookup"><span data-stu-id="6a07b-140">hello code examples in this section address each of these components.</span></span>

<span data-ttu-id="6a07b-141">contratto di Hello definisce una singola operazione `AddNumbers`, che aggiunge due numeri e restituisce il risultato di hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-141">hello contract defines a single operation, `AddNumbers`, that adds two numbers and returns hello result.</span></span> <span data-ttu-id="6a07b-142">Hello `IProblemSolverChannel` interfaccia abilita hello client toomore durata proxy hello gestire con facilità.</span><span class="sxs-lookup"><span data-stu-id="6a07b-142">hello `IProblemSolverChannel` interface enables hello client toomore easily manage hello proxy lifetime.</span></span> <span data-ttu-id="6a07b-143">La creazione di tale interfaccia rientra tra le procedure consigliate.</span><span class="sxs-lookup"><span data-stu-id="6a07b-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="6a07b-144">È una buona idea tooput questo contratto definizione in un file separato, in modo che è possibile fare riferimento a tale file da progetti sia i "Client" e "Servizio", ma è anche possibile copiare il codice hello in entrambi i progetti.</span><span class="sxs-lookup"><span data-stu-id="6a07b-144">It's a good idea tooput this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy hello code into both projects.</span></span>

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

<span data-ttu-id="6a07b-145">Con contratto hello sul posto, implementazione hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="6a07b-145">With hello contract in place, hello implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="6a07b-146">Configurare un host del servizio a livello di codice</span><span class="sxs-lookup"><span data-stu-id="6a07b-146">Configure a service host programmatically</span></span>
<span data-ttu-id="6a07b-147">Con il contratto di hello e l'implementazione sul posto, è ora possibile ospitare il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-147">With hello contract and implementation in place, you can now host hello service.</span></span> <span data-ttu-id="6a07b-148">Hosting si verifica all'interno di un [ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) dell'oggetto, che si occupa della gestione delle istanze del servizio hello e host hello gli endpoint di ascolto dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="6a07b-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of hello service and hosts hello endpoints that listen for messages.</span></span> <span data-ttu-id="6a07b-149">Hello codice riportato di seguito consente di configurare il servizio hello con un endpoint locale regolare sia un aspetto inoltro endpoint tooillustrate hello, affiancati, degli endpoint interni ed esterni.</span><span class="sxs-lookup"><span data-stu-id="6a07b-149">hello following code configures hello service with both a regular local endpoint and a relay endpoint tooillustrate hello appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="6a07b-150">Sostituire la stringa hello *dello spazio dei nomi* con il nome dello spazio dei nomi e *yourKey* con la chiave di firma di accesso condiviso hello ottenuto nel passaggio di installazione precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-150">Replace hello string *namespace* with your namespace name and *yourKey* with hello SAS key that you obtained in hello previous setup step.</span></span>

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

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="6a07b-151">Nell'esempio hello si creano due endpoint che si trovano in hello stessa implementazione del contratto.</span><span class="sxs-lookup"><span data-stu-id="6a07b-151">In hello example, you create two endpoints that are on hello same contract implementation.</span></span> <span data-ttu-id="6a07b-152">Uno è locale e uno viene proiettato tramite il servizio di inoltro.</span><span class="sxs-lookup"><span data-stu-id="6a07b-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="6a07b-153">differenze principali di Hello tra di essi sono associazioni hello; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) per hello uno locale e [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) per endpoint di inoltro hello e gli indirizzi di hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-153">hello key differences between them are hello bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for hello local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for hello relay endpoint and hello addresses.</span></span> <span data-ttu-id="6a07b-154">endpoint locale Hello ha un indirizzo di rete locale con una porta distinto.</span><span class="sxs-lookup"><span data-stu-id="6a07b-154">hello local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="6a07b-155">endpoint di inoltro Hello è un indirizzo endpoint composto da stringa hello `sb`, il nome dello spazio dei nomi e il percorso di hello "Risolutore."</span><span class="sxs-lookup"><span data-stu-id="6a07b-155">hello relay endpoint has an endpoint address composed of hello string `sb`, your namespace name, and hello path "solver."</span></span> <span data-ttu-id="6a07b-156">Di conseguenza, hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identificare gli endpoint del servizio hello come un endpoint TCP del Bus di servizio (inoltro) con un nome DNS esterno completo.</span><span class="sxs-lookup"><span data-stu-id="6a07b-156">This results in hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying hello service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="6a07b-157">Se inserire codice hello sostituendo i segnaposto hello in hello `Main` funzione di hello **servizio** un'applicazione, si disporrà di un servizio funzionale.</span><span class="sxs-lookup"><span data-stu-id="6a07b-157">If you place hello code replacing hello placeholders into hello `Main` function of hello **Service** application, you will have a functional service.</span></span> <span data-ttu-id="6a07b-158">Se si desidera toolisten il servizio esclusivamente in inoltro hello, rimuovere dichiarazione endpoint locale hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-158">If you want your service toolisten exclusively on hello relay, remove hello local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-hello-appconfig-file"></a><span data-ttu-id="6a07b-159">Configurare un host del servizio nel file app. config hello</span><span class="sxs-lookup"><span data-stu-id="6a07b-159">Configure a service host in hello App.config file</span></span>
<span data-ttu-id="6a07b-160">È inoltre possibile configurare l'host di hello utilizzando file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-160">You can also configure hello host using hello App.config file.</span></span> <span data-ttu-id="6a07b-161">servizio di Hello codice di hosting in questo caso viene visualizzato nell'esempio riportato di seguito hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-161">hello service hosting code in this case appears in hello next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="6a07b-162">le definizioni degli endpoint Hello spostare nel file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-162">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="6a07b-163">pacchetto NuGet Hello è già aggiunto un intervallo di file di definizione toohello app. config, che sono estensioni di configurazione hello necessario per l'inoltro di Azure.</span><span class="sxs-lookup"><span data-stu-id="6a07b-163">hello NuGet package has already added a range of definitions toohello App.config file, which are hello required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="6a07b-164">Hello seguente esempio, ovvero hello esatto equivalente del codice precedente hello, devono essere visualizzate direttamente sotto hello **System. ServiceModel** elemento.</span><span class="sxs-lookup"><span data-stu-id="6a07b-164">hello following example, which is hello exact equivalent of hello previous code, should appear directly beneath hello **system.serviceModel** element.</span></span> <span data-ttu-id="6a07b-165">In questo esempio di codice si presuppone che il nome dello spazio dei nomi del progetto C# sia **Service**.</span><span class="sxs-lookup"><span data-stu-id="6a07b-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="6a07b-166">Sostituire i segnaposto hello con il nome dello spazio dei nomi di inoltro e la chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="6a07b-166">Replace hello placeholders with your relay namespace name and SAS key.</span></span>

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

<span data-ttu-id="6a07b-167">Dopo aver apportato queste modifiche, avvio del servizio hello come in precedenza, ma con due endpoint in tempo reale: una locale e in attesa uno nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-167">After you make these changes, hello service starts as it did before, but with two live endpoints: one local and one listening in hello cloud.</span></span>

### <a name="create-hello-client"></a><span data-ttu-id="6a07b-168">Creare hello client</span><span class="sxs-lookup"><span data-stu-id="6a07b-168">Create hello client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="6a07b-169">Configurare un client a livello di codice</span><span class="sxs-lookup"><span data-stu-id="6a07b-169">Configure a client programmatically</span></span>
<span data-ttu-id="6a07b-170">servizio hello tooconsume, è possibile creare un client WCF usando un [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) oggetto.</span><span class="sxs-lookup"><span data-stu-id="6a07b-170">tooconsume hello service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="6a07b-171">Il bus di servizio usa un modello di sicurezza basato sui token implementato tramite la firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="6a07b-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="6a07b-172">Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) classe rappresenta un provider di token di sicurezza con metodi factory incorporati che restituiscono alcuni provider di token noti.</span><span class="sxs-lookup"><span data-stu-id="6a07b-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="6a07b-173">esempio Hello utilizza hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) metodo toohandle hello acquisizione token SAS appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-173">hello following example uses hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method toohandle hello acquisition of hello appropriate SAS token.</span></span> <span data-ttu-id="6a07b-174">chiave e il nome di hello sono quelli ottenuti dal portale hello come descritto nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-174">hello name and key are those obtained from hello portal as described in hello previous section.</span></span>

<span data-ttu-id="6a07b-175">Primo, riferimento o la copia hello `IProblemSolver` contratto codice dal servizio hello nel progetto client.</span><span class="sxs-lookup"><span data-stu-id="6a07b-175">First, reference or copy hello `IProblemSolver` contract code from hello service into your client project.</span></span>

<span data-ttu-id="6a07b-176">Quindi, sostituire il codice hello in hello `Main` metodo del client di hello, nuovamente sostituendo il testo segnaposto hello con la chiave di firma di accesso condiviso e l'inoltro dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6a07b-176">Then, replace hello code in hello `Main` method of hello client, again replacing hello placeholder text with your relay namespace and SAS key.</span></span>

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

<span data-ttu-id="6a07b-177">È ora possibile generare client hello e il servizio di hello, eseguirli (eseguire hello servizio innanzitutto), hello del client e chiama il servizio hello stampa **9**.</span><span class="sxs-lookup"><span data-stu-id="6a07b-177">You can now build hello client and hello service, run them (run hello service first), and hello client calls hello service and prints **9**.</span></span> <span data-ttu-id="6a07b-178">È possibile eseguire hello client e server in computer diversi, anche su reti e comunicazione hello continueranno a funzionare.</span><span class="sxs-lookup"><span data-stu-id="6a07b-178">You can run hello client and server on different machines, even across networks, and hello communication will still work.</span></span> <span data-ttu-id="6a07b-179">il codice client hello è anche possibile eseguire nel cloud hello o in locale.</span><span class="sxs-lookup"><span data-stu-id="6a07b-179">hello client code can also run in hello cloud or locally.</span></span>

#### <a name="configure-a-client-in-hello-appconfig-file"></a><span data-ttu-id="6a07b-180">Configurare un client nel file app. config hello</span><span class="sxs-lookup"><span data-stu-id="6a07b-180">Configure a client in hello App.config file</span></span>
<span data-ttu-id="6a07b-181">Hello seguente codice mostra come client hello tooconfigure utilizzando hello file app. config.</span><span class="sxs-lookup"><span data-stu-id="6a07b-181">hello following code shows how tooconfigure hello client using hello App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="6a07b-182">le definizioni degli endpoint Hello spostare nel file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="6a07b-182">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="6a07b-183">Hello esempio seguente, che è hello stesso come codice hello elencate in precedenza, deve essere visualizzate direttamente sotto hello `<system.serviceModel>` elemento.</span><span class="sxs-lookup"><span data-stu-id="6a07b-183">hello following example, which is hello same as hello code listed previously, should appear directly beneath hello `<system.serviceModel>` element.</span></span> <span data-ttu-id="6a07b-184">In questo caso, come in precedenza, è necessario sostituire i segnaposto hello con la chiave di firma di accesso condiviso e l'inoltro dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6a07b-184">Here, as before, you must replace hello placeholders with your relay namespace and SAS key.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6a07b-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a07b-185">Next steps</span></span>
<span data-ttu-id="6a07b-186">Ora che si sono appreso i concetti fondamentali di hello dell'inoltro di Azure, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="6a07b-186">Now that you've learned hello basics of Azure Relay, follow these links toolearn more.</span></span>

* [<span data-ttu-id="6a07b-187">Che cos'è il servizio di inoltro di Azure?</span><span class="sxs-lookup"><span data-stu-id="6a07b-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="6a07b-188">Panoramica dell'architettura del bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="6a07b-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="6a07b-189">Scaricare gli esempi di Service Bus da [Azure esempi] [ Azure samples] o vedere hello [panoramica degli esempi di Service Bus][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="6a07b-189">Download Service Bus samples from [Azure samples][Azure samples] or see hello [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
