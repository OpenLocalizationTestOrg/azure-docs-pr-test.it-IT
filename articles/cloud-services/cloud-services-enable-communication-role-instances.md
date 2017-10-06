---
title: aaaCommunication per i ruoli di servizi Cloud | Documenti Microsoft
description: Le istanze del ruolo in servizi Cloud possono essere endpoint (http, https, tcp, udp) predefiniti che comunicano con hello all'esterno o tra altre istanze del ruolo.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7008a083-acbe-4fb8-ae60-b837ef971ca1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 1fb39215ceb8a3f0381ef5e108c1149de115ff8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a>Abilitare la comunicazione delle istanze del ruolo in azure
I ruoli del servizio cloud comunicano tramite connessioni interne ed esterne. Le connessioni esterne vengono chiamate **endpoint di input** mentre le connessioni interne vengono chiamate **endpoint interni**. Questo argomento viene descritto come hello toomodify [definizione servizio](cloud-services-model-and-package.md#csdef) toocreate endpoint.

## <a name="input-endpoint"></a>Endpoint di input
endpoint di input Hello viene utilizzato quando si desidera tooexpose toohello una porta all'esterno. Specificare il tipo di protocollo hello e porta hello dell'endpoint hello che viene quindi applicato per entrambe le porte interne ed esterne di hello per endpoint hello. Se si desidera, è possibile specificare un'altra porta interna per l'endpoint di hello con hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attributo.

endpoint di input Hello è possibile utilizzare hello seguenti protocolli: **http, https, tcp, udp**.

toocreate un endpoint di input, aggiungere hello **InputEndpoint** toohello elemento figlio **endpoint** elemento del ruolo di lavoro o web.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a>Endpoint di input dell'istanza
Gli endpoint di input istanza simile tooinput endpoint consente tuttavia di eseguire il mapping di porte pubbliche specifiche per ogni singola istanza del ruolo mediante port forwarding nel servizio di bilanciamento del carico hello. È possibile specificare una singola porta pubblica o un intervallo di porte.

endpoint di input istanza Hello è possibile utilizzare solo **tcp** o **udp** come protocollo di hello.

toocreate un endpoint di input di istanza, aggiungere hello **InstanceInputEndpoint** toohello elemento figlio **endpoint** elemento del ruolo di lavoro o web.

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a>Endpoint interno
Gli endpoint interni sono disponibili per la comunicazione da istanza a istanza. porta Hello è facoltativa e se omesso, una porta dinamica viene assegnata toohello endpoint. Può essere utilizzato un intervallo di porte. Esiste un limite di cinque endpoint interni per ogni ruolo.

endpoint interno Hello è possibile utilizzare hello seguenti protocolli: **http, tcp, udp, qualsiasi**.

un endpoint di input interno, toocreate aggiungere hello **InternalEndpoint** toohello elemento figlio **endpoint** elemento del ruolo di lavoro o web.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

È possibile inoltre utilizzare un intervallo di porte.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a>Ruoli di lavoro a confronto con Ruoli Web
Esiste una piccola differenza tra gli endpoint quando si lavora con i ruoli di lavoro e i ruoli  web. Hello ruolo web deve avere almeno un solo endpoint di input utilizzando hello **HTTP** protocollo.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a>Hello .NET SDK tooaccess un endpoint di utilizzo
Hello libreria gestita di Azure fornisce metodi per toocommunicate le istanze di ruolo in fase di esecuzione. Dal codice eseguito all'interno di un'istanza del ruolo, è possibile recuperare informazioni sull'esistenza hello di altre istanze del ruolo e sui relativi endpoint, nonché informazioni sull'istanza del ruolo corrente hello.

> [!NOTE]
> È possibile recuperare solo le informazioni sulle istanze dei ruoli che sono in esecuzione nel servizio cloud e che definiscono almeno un endpoint interno. Non è possibile ottenere dati sulle istanze dei ruoli in esecuzione in un altro servizio.
> 
> 

È possibile utilizzare hello [istanze](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) istanze tooretrieve di proprietà di un ruolo. Utilizzare innanzitutto hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn un ruolo di riferimento toohello corrente dell'istanza e quindi utilizzare hello [ruolo](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) proprietà tooreturn un ruolo toohello riferimento stesso.

Quando ci si connette tooa istanza del ruolo a livello di programmazione tramite hello .NET SDK, è relativamente facile tooaccess informazioni sull'endpoint di hello. Ad esempio, dopo l'ambiente del ruolo specifico tooa già connesse, è possibile ottenere porta hello di un endpoint specifico con il seguente codice:

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

Hello **istanze** proprietà restituisce una raccolta di **RoleInstance** oggetti. Questa raccolta contiene sempre istanza corrente di hello. Se il ruolo di hello non definisce un endpoint interno, raccolta di hello include l'istanza corrente di hello ma non altre istanze. numero di Hello di istanze del ruolo nella raccolta hello sarà sempre 1 in caso di hello in cui non è definito alcun endpoint interno per il ruolo di hello. Se il ruolo di hello definisce un endpoint interno, le relative istanze sono individuabili in fase di esecuzione e numero hello di istanze nella raccolta hello corrisponderà toohello numero di istanze specificato per il ruolo di hello in file di configurazione del servizio hello.

> [!NOTE]
> Hello libreria gestita di Azure non fornisce un modo per determinare l'integrità di hello di altre istanze del ruolo, ma è possibile implementare tali valutazioni manualmente se il servizio deve disporre di questa funzionalità. È possibile utilizzare [diagnostica Azure](cloud-services-dotnet-diagnostics.md) tooobtain informazioni sull'esecuzione di istanze del ruolo.
> 
> 

numero di porta hello toodetermine per un endpoint interno in un'istanza del ruolo, è possibile utilizzare hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn proprietà risolve un oggetto dizionario che contiene i nomi degli endpoint e i corrispondenti IP e porte. Hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) proprietà restituisce l'indirizzo IP hello e la porta per un endpoint specificato. Hello **PublicIPEndpoint** restituirà porta hello per un endpoint con carico bilanciato. parte dell'indirizzo IP Hello di hello **PublicIPEndpoint** proprietà non viene utilizzata.

Di seguito è riportato un esempio che consente di eseguire l’iterazione delle istanze del ruolo.

```csharp
foreach (RoleInstance roleInst in RoleEnvironment.CurrentRoleInstance.Role.Instances)
{
    Trace.WriteLine("Instance ID: " + roleInst.Id);
    foreach (RoleInstanceEndpoint roleInstEndpoint in roleInst.InstanceEndpoints.Values)
    {
        Trace.WriteLine("Instance endpoint IP address and port: " + roleInstEndpoint.IPEndpoint);
    }
}
```

Di seguito è riportato un esempio di un ruolo di lavoro che ottiene endpoint hello esposto tramite la definizione di servizio hello e avvia l'ascolto delle connessioni.

> [!WARNING]
> Questo codice funziona solo per un servizio distribuito. Quando si esegue hello emulatore di calcolo di Azure, gli elementi di configurazione che creano endpoint porte dirette del servizio (**InstanceInputEndpoint** elementi) vengono ignorati.
> 
> 

```csharp
using System;
using System.Diagnostics;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Threading;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Diagnostics;
using Microsoft.WindowsAzure.ServiceRuntime;
using Microsoft.WindowsAzure.StorageClient;

namespace WorkerRole1
{
  public class WorkerRole : RoleEntryPoint
  {
    public override void Run()
    {
      try
      {
        // Initialize method-wide variables
        var epName = "Endpoint1";
        var roleInstance = RoleEnvironment.CurrentRoleInstance;

        // Identify direct communication port
        var myPublicEp = roleInstance.InstanceEndpoints[epName].PublicIPEndpoint;
        Trace.TraceInformation("IP:{0}, Port:{1}", myPublicEp.Address, myPublicEp.Port);

        // Identify public endpoint
        var myInternalEp = roleInstance.InstanceEndpoints[epName].IPEndpoint;

        // Create socket listener
        var listener = new Socket(
          myInternalEp.AddressFamily, SocketType.Stream, ProtocolType.Tcp);

        // Bind socket listener toointernal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block hello thread and wait for a client request
          Socket handler = listener.Accept();
          Trace.TraceInformation("Client request received.");

          // Define body of socket handler
          var handlerThread = new Thread(
            new ParameterizedThreadStart(h =>
            {
              var socket = h as Socket;
              Trace.TraceInformation("Local:{0} Remote{1}",
                socket.LocalEndPoint, socket.RemoteEndPoint);

              // Shut down and close socket
              socket.Shutdown(SocketShutdown.Both);
              socket.Close();
            }
          ));

          // Start socket handler on new thread
          handlerThread.Start(handler);
        }
      }
      catch (Exception e)
      {
        Trace.TraceError("Caught exception in run. Details: {0}", e);
      }
    }

    public override bool OnStart()
    {
      // Set hello maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-toocontrol-role-communication"></a>Comunicazione dei ruoli toocontrol regole del traffico di rete
Dopo aver definito gli endpoint interni, è possibile aggiungere toocontrol regole (in base agli endpoint creati hello) del traffico di rete come istanze del ruolo possono comunicare tra loro. Hello diagramma seguente illustra alcuni scenari comuni per il controllo di comunicazione con il ruolo:

![Scenari di regole del traffico di rete](./media/cloud-services-enable-communication-role-instances/scenarios.png "Scenari di regole del traffico di rete")

Hello esempio di codice seguente mostra le definizioni di ruolo per i ruoli di hello illustrati nel diagramma precedente hello. Ogni definizione di ruolo include almeno un endpoint interno definito:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalTCP1" protocol="tcp" />
    </Endpoints>
  </WebRole>
  <WorkerRole name="WorkerRole1">
    <Endpoints>
      <InternalEndpoint name="InternalTCP2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
  <WorkerRole name="WorkerRole2">
    <Endpoints>
      <InternalEndpoint name="InternalTCP3" protocol="tcp" />
      <InternalEndpoint name="InternalTCP4" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

> [!NOTE]
> La restrizione della comunicazione tra ruoli può verificarsi con endpoint interni di porte fisse o assegnate automaticamente.
> 
> 

Per impostazione predefinita, dopo aver definito un endpoint interno, la comunicazione può avvenire da qualsiasi endpoint interno toohello di ruolo di un ruolo senza restrizioni. comunicazione toorestrict, è necessario aggiungere un **NetworkTrafficRules** elemento toohello **ServiceDefinition** elemento nel file di definizione del servizio hello.

### <a name="scenario-1"></a>Scenario 1
Consentire solo il traffico di rete da **WebRole1** troppo**WorkerRole1**.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-2"></a>Scenario 2
Consente solo il traffico di rete da **WebRole1** troppo**WorkerRole1** e **WorkerRole2**.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-3"></a>Scenario 3
Consente solo il traffico di rete da **WebRole1** troppo**WorkerRole1**, e **WorkerRole1** troppo**WorkerRole2**.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-4"></a>Scenario 4
Consente solo il traffico di rete da **WebRole1** troppo**WorkerRole1**, **WebRole1** troppo**WorkerRole2**, e  **WorkerRole1** troppo**WorkerRole2**.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP4" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

Un riferimento XML schema per gli elementi di hello precedente è reperibile [qui](https://msdn.microsoft.com/library/azure/gg557551.aspx).

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sugli hello servizio Cloud [modello](cloud-services-model-and-package.md).

