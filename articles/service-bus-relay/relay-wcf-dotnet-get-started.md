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
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a>Come Azure inoltro WCF toouse degli inoltri con .NET
In questo articolo viene descritto come toouse hello servizio di inoltro di Azure. esempi di Hello vengono scritti in c# e usano API di Windows Communication Foundation (WCF) hello con estensioni contenute in assembly di Service Bus hello. Per ulteriori informazioni sull'inoltro di Azure, vedere hello [Cenni preliminari su Azure Relay](relay-what-is-it.md).

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a>Informazioni sull'inoltro WCF

Hello Azure [ *inoltro WCF* ](relay-what-is-it.md) servizio consente di applicazioni ibride toobuild eseguiti in un Data Center di Azure sia ambiente aziendale locale. il servizio di inoltro Hello facilita questo consentendo toosecurely espongono i servizi Windows Communication Foundation (WCF) che si trovano all'interno di un'organizzazione aziendale rete toohello pubblica cloud senza la necessità di una connessione firewall tooopen, o che richiedono infrastruttura della rete aziendale tooa modifiche intrusiva.

![Concetti sull'inoltro con WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

Inoltro di Azure permette di servizi WCF toohost nell'ambiente aziendale esistente. È quindi possibile delegare l'ascolto di arrivo sessioni e richieste toothese servizi toohello servizio di inoltro WCF in esecuzione in Azure. In questo modo si tooexpose codice di tooapplication questi servizi in esecuzione in Azure, o thread di lavoro toomobile o ambienti di partner extranet. Inoltro consente di controllare toosecurely chi può accedere ai servizi a un livello con granularità fine. Fornisce una funzionalità dell'applicazione tooexpose sistema efficiente e sicuro e i dati dalle soluzioni aziendali esistenti e sfruttare il dal cloud hello.

Questo articolo illustra come toouse Azure inoltro toocreate un servizio web WCF, esposte tramite un'associazione di canale TCP, che implementa una conversazione protetta tra due parti.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a>Ottenere il pacchetto NuGet di Service Bus hello
Hello [pacchetto NuGet di Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus) è hello più semplice modo tooget hello API del Bus di servizio e tooconfigure l'applicazione con tutte le dipendenze di hello Bus di servizio. pacchetto NuGet di hello tooinstall nel progetto, hello seguenti:

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.
2. Ricerca di "Bus di servizio" e seleziona hello **Microsoft Azure Service Bus** elemento. Fare clic su **installare** toocomplete hello installazione, quindi chiudere la finestra di dialogo seguente hello:
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a>Esporre e utilizzare un servizio Web SOAP con TCP
tooexpose un servizio web SOAP WCF esistente per l'utilizzo esterno, è necessario apportare modifiche toohello servizio associazioni e gli indirizzi. Potrebbe essere necessario il file di configurazione tooyour modifiche o potrebbe richiedere modifiche al codice, a seconda di come è impostato e configurato i servizi WCF. Si noti che WCF consente toohave più endpoint di rete su hello stesso servizio, in modo da mantenere hello esistente endpoint interni durante l'aggiunta di endpoint di inoltro per esterno accedere in hello stesso tempo.

In questa attività, compilare un semplice servizio WCF e aggiungere un tooit di listener di inoltro. Questo esercizio si presuppone la conoscenza di Visual Studio e pertanto non analizzerà tutti i dettagli di hello di creazione di un progetto. Si concentra invece sul codice hello.

Prima di iniziare questa procedura, completare hello seguendo procedure tooset dell'ambiente:

1. In Visual Studio, creare un'applicazione console che contiene due progetti, "Client" e "Servizio", all'interno di soluzione hello.
2. Aggiungere progetti tooboth pacchetto NuGet di Service Bus di hello. Questo pacchetto aggiunge tutti i progetti di tooyour i riferimenti di assembly necessari hello.

### <a name="how-toocreate-hello-service"></a>Come toocreate hello servizio
Innanzitutto, creare il servizio hello stesso. Tutti i servizi WCF sono costituiti da almeno tre parti distinte:

* Definizione di un contratto che descrive i messaggi vengono scambiati e quali operazioni sono toobe richiamato.
* Implementazione di tale contratto.
* Host che ospita il servizio WCF hello ed espone più endpoint.

esempi di codice Hello in questa sezione indirizzo ognuno di questi componenti.

contratto di Hello definisce una singola operazione `AddNumbers`, che aggiunge due numeri e restituisce il risultato di hello. Hello `IProblemSolverChannel` interfaccia abilita hello client toomore durata proxy hello gestire con facilità. La creazione di tale interfaccia rientra tra le procedure consigliate. È una buona idea tooput questo contratto definizione in un file separato, in modo che è possibile fare riferimento a tale file da progetti sia i "Client" e "Servizio", ma è anche possibile copiare il codice hello in entrambi i progetti.

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

Con contratto hello sul posto, implementazione hello è come segue:

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a>Configurare un host del servizio a livello di codice
Con il contratto di hello e l'implementazione sul posto, è ora possibile ospitare il servizio di hello. Hosting si verifica all'interno di un [ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) dell'oggetto, che si occupa della gestione delle istanze del servizio hello e host hello gli endpoint di ascolto dei messaggi. Hello codice riportato di seguito consente di configurare il servizio hello con un endpoint locale regolare sia un aspetto inoltro endpoint tooillustrate hello, affiancati, degli endpoint interni ed esterni. Sostituire la stringa hello *dello spazio dei nomi* con il nome dello spazio dei nomi e *yourKey* con la chiave di firma di accesso condiviso hello ottenuto nel passaggio di installazione precedente di hello.

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

Nell'esempio hello si creano due endpoint che si trovano in hello stessa implementazione del contratto. Uno è locale e uno viene proiettato tramite il servizio di inoltro. differenze principali di Hello tra di essi sono associazioni hello; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) per hello uno locale e [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) per endpoint di inoltro hello e gli indirizzi di hello. endpoint locale Hello ha un indirizzo di rete locale con una porta distinto. endpoint di inoltro Hello è un indirizzo endpoint composto da stringa hello `sb`, il nome dello spazio dei nomi e il percorso di hello "Risolutore." Di conseguenza, hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identificare gli endpoint del servizio hello come un endpoint TCP del Bus di servizio (inoltro) con un nome DNS esterno completo. Se inserire codice hello sostituendo i segnaposto hello in hello `Main` funzione di hello **servizio** un'applicazione, si disporrà di un servizio funzionale. Se si desidera toolisten il servizio esclusivamente in inoltro hello, rimuovere dichiarazione endpoint locale hello.

### <a name="configure-a-service-host-in-hello-appconfig-file"></a>Configurare un host del servizio nel file app. config hello
È inoltre possibile configurare l'host di hello utilizzando file app. config hello. servizio di Hello codice di hosting in questo caso viene visualizzato nell'esempio riportato di seguito hello.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

le definizioni degli endpoint Hello spostare nel file app. config hello. pacchetto NuGet Hello è già aggiunto un intervallo di file di definizione toohello app. config, che sono estensioni di configurazione hello necessario per l'inoltro di Azure. Hello seguente esempio, ovvero hello esatto equivalente del codice precedente hello, devono essere visualizzate direttamente sotto hello **System. ServiceModel** elemento. In questo esempio di codice si presuppone che il nome dello spazio dei nomi del progetto C# sia **Service**.
Sostituire i segnaposto hello con il nome dello spazio dei nomi di inoltro e la chiave di firma di accesso condiviso.

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

Dopo aver apportato queste modifiche, avvio del servizio hello come in precedenza, ma con due endpoint in tempo reale: una locale e in attesa uno nel cloud hello.

### <a name="create-hello-client"></a>Creare hello client
#### <a name="configure-a-client-programmatically"></a>Configurare un client a livello di codice
servizio hello tooconsume, è possibile creare un client WCF usando un [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) oggetto. Il bus di servizio usa un modello di sicurezza basato sui token implementato tramite la firma di accesso condiviso. Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) classe rappresenta un provider di token di sicurezza con metodi factory incorporati che restituiscono alcuni provider di token noti. esempio Hello utilizza hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) metodo toohandle hello acquisizione token SAS appropriato hello. chiave e il nome di hello sono quelli ottenuti dal portale hello come descritto nella sezione precedente hello.

Primo, riferimento o la copia hello `IProblemSolver` contratto codice dal servizio hello nel progetto client.

Quindi, sostituire il codice hello in hello `Main` metodo del client di hello, nuovamente sostituendo il testo segnaposto hello con la chiave di firma di accesso condiviso e l'inoltro dello spazio dei nomi.

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

È ora possibile generare client hello e il servizio di hello, eseguirli (eseguire hello servizio innanzitutto), hello del client e chiama il servizio hello stampa **9**. È possibile eseguire hello client e server in computer diversi, anche su reti e comunicazione hello continueranno a funzionare. il codice client hello è anche possibile eseguire nel cloud hello o in locale.

#### <a name="configure-a-client-in-hello-appconfig-file"></a>Configurare un client nel file app. config hello
Hello seguente codice mostra come client hello tooconfigure utilizzando hello file app. config.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

le definizioni degli endpoint Hello spostare nel file app. config hello. Hello esempio seguente, che è hello stesso come codice hello elencate in precedenza, deve essere visualizzate direttamente sotto hello `<system.serviceModel>` elemento. In questo caso, come in precedenza, è necessario sostituire i segnaposto hello con la chiave di firma di accesso condiviso e l'inoltro dello spazio dei nomi.

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

## <a name="next-steps"></a>Passaggi successivi
Ora che si sono appreso i concetti fondamentali di hello dell'inoltro di Azure, seguire questi ulteriori toolearn di collegamenti.

* [Che cos'è il servizio di inoltro di Azure?](relay-what-is-it.md)
* [Panoramica dell'architettura del bus di servizio di Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* Scaricare gli esempi di Service Bus da [Azure esempi] [ Azure samples] o vedere hello [panoramica degli esempi di Service Bus][overview of Service Bus samples].

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
