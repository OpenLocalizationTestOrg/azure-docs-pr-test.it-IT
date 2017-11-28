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
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="11f3b-103">Abilitare la comunicazione delle istanze del ruolo in azure</span><span class="sxs-lookup"><span data-stu-id="11f3b-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="11f3b-104">I ruoli del servizio cloud comunicano tramite connessioni interne ed esterne.</span><span class="sxs-lookup"><span data-stu-id="11f3b-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="11f3b-105">Le connessioni esterne vengono chiamate **endpoint di input** mentre le connessioni interne vengono chiamate **endpoint interni**.</span><span class="sxs-lookup"><span data-stu-id="11f3b-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="11f3b-106">Questo argomento viene descritto come hello toomodify [definizione servizio](cloud-services-model-and-package.md#csdef) toocreate endpoint.</span><span class="sxs-lookup"><span data-stu-id="11f3b-106">This topic describes how toomodify hello [service definition](cloud-services-model-and-package.md#csdef) toocreate endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="11f3b-107">Endpoint di input</span><span class="sxs-lookup"><span data-stu-id="11f3b-107">Input endpoint</span></span>
<span data-ttu-id="11f3b-108">endpoint di input Hello viene utilizzato quando si desidera tooexpose toohello una porta all'esterno.</span><span class="sxs-lookup"><span data-stu-id="11f3b-108">hello input endpoint is used when you want tooexpose a port toohello outside.</span></span> <span data-ttu-id="11f3b-109">Specificare il tipo di protocollo hello e porta hello dell'endpoint hello che viene quindi applicato per entrambe le porte interne ed esterne di hello per endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="11f3b-109">You specify hello protocol type and hello port of hello endpoint which then applies for both hello external and internal ports for hello endpoint.</span></span> <span data-ttu-id="11f3b-110">Se si desidera, è possibile specificare un'altra porta interna per l'endpoint di hello con hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attributo.</span><span class="sxs-lookup"><span data-stu-id="11f3b-110">If you want, you can specify a different internal port for hello endpoint with hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="11f3b-111">endpoint di input Hello è possibile utilizzare hello seguenti protocolli: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="11f3b-111">hello input endpoint can use hello following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="11f3b-112">toocreate un endpoint di input, aggiungere hello **InputEndpoint** toohello elemento figlio **endpoint** elemento del ruolo di lavoro o web.</span><span class="sxs-lookup"><span data-stu-id="11f3b-112">toocreate an input endpoint, add hello **InputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="11f3b-113">Endpoint di input dell'istanza</span><span class="sxs-lookup"><span data-stu-id="11f3b-113">Instance input endpoint</span></span>
<span data-ttu-id="11f3b-114">Gli endpoint di input istanza simile tooinput endpoint consente tuttavia di eseguire il mapping di porte pubbliche specifiche per ogni singola istanza del ruolo mediante port forwarding nel servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="11f3b-114">Instance input endpoints are similar tooinput endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on hello load balancer.</span></span> <span data-ttu-id="11f3b-115">È possibile specificare una singola porta pubblica o un intervallo di porte.</span><span class="sxs-lookup"><span data-stu-id="11f3b-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="11f3b-116">endpoint di input istanza Hello è possibile utilizzare solo **tcp** o **udp** come protocollo di hello.</span><span class="sxs-lookup"><span data-stu-id="11f3b-116">hello instance input endpoint can only use **tcp** or **udp** as hello protocol.</span></span>

<span data-ttu-id="11f3b-117">toocreate un endpoint di input di istanza, aggiungere hello **InstanceInputEndpoint** toohello elemento figlio **endpoint** elemento del ruolo di lavoro o web.</span><span class="sxs-lookup"><span data-stu-id="11f3b-117">toocreate an instance input endpoint, add hello **InstanceInputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="11f3b-118">Endpoint interno</span><span class="sxs-lookup"><span data-stu-id="11f3b-118">Internal endpoint</span></span>
<span data-ttu-id="11f3b-119">Gli endpoint interni sono disponibili per la comunicazione da istanza a istanza.</span><span class="sxs-lookup"><span data-stu-id="11f3b-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="11f3b-120">porta Hello è facoltativa e se omesso, una porta dinamica viene assegnata toohello endpoint.</span><span class="sxs-lookup"><span data-stu-id="11f3b-120">hello port is optional and if omitted, a dynamic port is assigned toohello endpoint.</span></span> <span data-ttu-id="11f3b-121">Può essere utilizzato un intervallo di porte.</span><span class="sxs-lookup"><span data-stu-id="11f3b-121">A port range can be used.</span></span> <span data-ttu-id="11f3b-122">Esiste un limite di cinque endpoint interni per ogni ruolo.</span><span class="sxs-lookup"><span data-stu-id="11f3b-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="11f3b-123">endpoint interno Hello è possibile utilizzare hello seguenti protocolli: **http, tcp, udp, qualsiasi**.</span><span class="sxs-lookup"><span data-stu-id="11f3b-123">hello internal endpoint can use hello following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="11f3b-124">un endpoint di input interno, toocreate aggiungere hello **InternalEndpoint** toohello elemento figlio **endpoint** elemento del ruolo di lavoro o web.</span><span class="sxs-lookup"><span data-stu-id="11f3b-124">toocreate an internal input endpoint, add hello **InternalEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="11f3b-125">È possibile inoltre utilizzare un intervallo di porte.</span><span class="sxs-lookup"><span data-stu-id="11f3b-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="11f3b-126">Ruoli di lavoro a confronto con Ruoli Web</span><span class="sxs-lookup"><span data-stu-id="11f3b-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="11f3b-127">Esiste una piccola differenza tra gli endpoint quando si lavora con i ruoli di lavoro e i ruoli  web.</span><span class="sxs-lookup"><span data-stu-id="11f3b-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="11f3b-128">Hello ruolo web deve avere almeno un solo endpoint di input utilizzando hello **HTTP** protocollo.</span><span class="sxs-lookup"><span data-stu-id="11f3b-128">hello web role must have at minimum a single input endpoint using hello **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a><span data-ttu-id="11f3b-129">Hello .NET SDK tooaccess un endpoint di utilizzo</span><span class="sxs-lookup"><span data-stu-id="11f3b-129">Using hello .NET SDK tooaccess an endpoint</span></span>
<span data-ttu-id="11f3b-130">Hello libreria gestita di Azure fornisce metodi per toocommunicate le istanze di ruolo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="11f3b-130">hello Azure Managed Library provides methods for role instances toocommunicate at runtime.</span></span> <span data-ttu-id="11f3b-131">Dal codice eseguito all'interno di un'istanza del ruolo, è possibile recuperare informazioni sull'esistenza hello di altre istanze del ruolo e sui relativi endpoint, nonché informazioni sull'istanza del ruolo corrente hello.</span><span class="sxs-lookup"><span data-stu-id="11f3b-131">From code running within a role instance, you can retrieve information about hello existence of other role instances and their endpoints, as well as information about hello current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="11f3b-132">È possibile recuperare solo le informazioni sulle istanze dei ruoli che sono in esecuzione nel servizio cloud e che definiscono almeno un endpoint interno.</span><span class="sxs-lookup"><span data-stu-id="11f3b-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="11f3b-133">Non è possibile ottenere dati sulle istanze dei ruoli in esecuzione in un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="11f3b-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="11f3b-134">È possibile utilizzare hello [istanze](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) istanze tooretrieve di proprietà di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="11f3b-134">You can use hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property tooretrieve instances of a role.</span></span> <span data-ttu-id="11f3b-135">Utilizzare innanzitutto hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn un ruolo di riferimento toohello corrente dell'istanza e quindi utilizzare hello [ruolo](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) proprietà tooreturn un ruolo toohello riferimento stesso.</span><span class="sxs-lookup"><span data-stu-id="11f3b-135">First use hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn a reference toohello current role instance, and then use hello [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property tooreturn a reference toohello role itself.</span></span>

<span data-ttu-id="11f3b-136">Quando ci si connette tooa istanza del ruolo a livello di programmazione tramite hello .NET SDK, è relativamente facile tooaccess informazioni sull'endpoint di hello.</span><span class="sxs-lookup"><span data-stu-id="11f3b-136">When you connect tooa role instance programmatically through hello .NET SDK, it's relatively easy tooaccess hello endpoint information.</span></span> <span data-ttu-id="11f3b-137">Ad esempio, dopo l'ambiente del ruolo specifico tooa già connesse, è possibile ottenere porta hello di un endpoint specifico con il seguente codice:</span><span class="sxs-lookup"><span data-stu-id="11f3b-137">For example, after you've already connected tooa specific role environment, you can get hello port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="11f3b-138">Hello **istanze** proprietà restituisce una raccolta di **RoleInstance** oggetti.</span><span class="sxs-lookup"><span data-stu-id="11f3b-138">hello **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="11f3b-139">Questa raccolta contiene sempre istanza corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="11f3b-139">This collection always contains hello current instance.</span></span> <span data-ttu-id="11f3b-140">Se il ruolo di hello non definisce un endpoint interno, raccolta di hello include l'istanza corrente di hello ma non altre istanze.</span><span class="sxs-lookup"><span data-stu-id="11f3b-140">If hello role does not define an internal endpoint, hello collection includes hello current instance but no other instances.</span></span> <span data-ttu-id="11f3b-141">numero di Hello di istanze del ruolo nella raccolta hello sarà sempre 1 in caso di hello in cui non è definito alcun endpoint interno per il ruolo di hello.</span><span class="sxs-lookup"><span data-stu-id="11f3b-141">hello number of role instances in hello collection will always be 1 in hello case where no internal endpoint is defined for hello role.</span></span> <span data-ttu-id="11f3b-142">Se il ruolo di hello definisce un endpoint interno, le relative istanze sono individuabili in fase di esecuzione e numero hello di istanze nella raccolta hello corrisponderà toohello numero di istanze specificato per il ruolo di hello in file di configurazione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="11f3b-142">If hello role defines an internal endpoint, its instances are discoverable at runtime, and hello number of instances in hello collection will correspond toohello number of instances specified for hello role in hello service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="11f3b-143">Hello libreria gestita di Azure non fornisce un modo per determinare l'integrità di hello di altre istanze del ruolo, ma è possibile implementare tali valutazioni manualmente se il servizio deve disporre di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="11f3b-143">hello Azure Managed Library does not provide a means of determining hello health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="11f3b-144">È possibile utilizzare [diagnostica Azure](cloud-services-dotnet-diagnostics.md) tooobtain informazioni sull'esecuzione di istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="11f3b-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="11f3b-145">numero di porta hello toodetermine per un endpoint interno in un'istanza del ruolo, è possibile utilizzare hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn proprietà risolve un oggetto dizionario che contiene i nomi degli endpoint e i corrispondenti IP e porte.</span><span class="sxs-lookup"><span data-stu-id="11f3b-145">toodetermine hello port number for an internal endpoint on a role instance, you can use hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property tooreturn a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="11f3b-146">Hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) proprietà restituisce l'indirizzo IP hello e la porta per un endpoint specificato.</span><span class="sxs-lookup"><span data-stu-id="11f3b-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns hello IP address and port for a specified endpoint.</span></span> <span data-ttu-id="11f3b-147">Hello **PublicIPEndpoint** restituirà porta hello per un endpoint con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="11f3b-147">hello **PublicIPEndpoint** property returns hello port for a load balanced endpoint.</span></span> <span data-ttu-id="11f3b-148">parte dell'indirizzo IP Hello di hello **PublicIPEndpoint** proprietà non viene utilizzata.</span><span class="sxs-lookup"><span data-stu-id="11f3b-148">hello IP address portion of hello **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="11f3b-149">Di seguito è riportato un esempio che consente di eseguire l’iterazione delle istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="11f3b-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="11f3b-150">Di seguito è riportato un esempio di un ruolo di lavoro che ottiene endpoint hello esposto tramite la definizione di servizio hello e avvia l'ascolto delle connessioni.</span><span class="sxs-lookup"><span data-stu-id="11f3b-150">Here is an example of a worker role that gets hello endpoint exposed through hello service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="11f3b-151">Questo codice funziona solo per un servizio distribuito.</span><span class="sxs-lookup"><span data-stu-id="11f3b-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="11f3b-152">Quando si esegue hello emulatore di calcolo di Azure, gli elementi di configurazione che creano endpoint porte dirette del servizio (**InstanceInputEndpoint** elementi) vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="11f3b-152">When running in hello Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

## <a name="network-traffic-rules-toocontrol-role-communication"></a><span data-ttu-id="11f3b-153">Comunicazione dei ruoli toocontrol regole del traffico di rete</span><span class="sxs-lookup"><span data-stu-id="11f3b-153">Network traffic rules toocontrol role communication</span></span>
<span data-ttu-id="11f3b-154">Dopo aver definito gli endpoint interni, è possibile aggiungere toocontrol regole (in base agli endpoint creati hello) del traffico di rete come istanze del ruolo possono comunicare tra loro.</span><span class="sxs-lookup"><span data-stu-id="11f3b-154">After you define internal endpoints, you can add network traffic rules (based on hello endpoints that you created) toocontrol how role instances can communicate with each other.</span></span> <span data-ttu-id="11f3b-155">Hello diagramma seguente illustra alcuni scenari comuni per il controllo di comunicazione con il ruolo:</span><span class="sxs-lookup"><span data-stu-id="11f3b-155">hello following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="11f3b-156">![Scenari di regole del traffico di rete](./media/cloud-services-enable-communication-role-instances/scenarios.png "Scenari di regole del traffico di rete")</span><span class="sxs-lookup"><span data-stu-id="11f3b-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="11f3b-157">Hello esempio di codice seguente mostra le definizioni di ruolo per i ruoli di hello illustrati nel diagramma precedente hello.</span><span class="sxs-lookup"><span data-stu-id="11f3b-157">hello following code example shows role definitions for hello roles shown in hello previous diagram.</span></span> <span data-ttu-id="11f3b-158">Ogni definizione di ruolo include almeno un endpoint interno definito:</span><span class="sxs-lookup"><span data-stu-id="11f3b-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="11f3b-159">La restrizione della comunicazione tra ruoli può verificarsi con endpoint interni di porte fisse o assegnate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="11f3b-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="11f3b-160">Per impostazione predefinita, dopo aver definito un endpoint interno, la comunicazione può avvenire da qualsiasi endpoint interno toohello di ruolo di un ruolo senza restrizioni.</span><span class="sxs-lookup"><span data-stu-id="11f3b-160">By default, after an internal endpoint is defined, communication can flow from any role toohello internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="11f3b-161">comunicazione toorestrict, è necessario aggiungere un **NetworkTrafficRules** elemento toohello **ServiceDefinition** elemento nel file di definizione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="11f3b-161">toorestrict communication, you must add a **NetworkTrafficRules** element toohello **ServiceDefinition** element in hello service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="11f3b-162">Scenario 1</span><span class="sxs-lookup"><span data-stu-id="11f3b-162">Scenario 1</span></span>
<span data-ttu-id="11f3b-163">Consentire solo il traffico di rete da **WebRole1** troppo**WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="11f3b-163">Only allow network traffic from **WebRole1** too**WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="11f3b-164">Scenario 2</span><span class="sxs-lookup"><span data-stu-id="11f3b-164">Scenario 2</span></span>
<span data-ttu-id="11f3b-165">Consente solo il traffico di rete da **WebRole1** troppo**WorkerRole1** e **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="11f3b-165">Only allows network traffic from **WebRole1** too**WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="11f3b-166">Scenario 3</span><span class="sxs-lookup"><span data-stu-id="11f3b-166">Scenario 3</span></span>
<span data-ttu-id="11f3b-167">Consente solo il traffico di rete da **WebRole1** troppo**WorkerRole1**, e **WorkerRole1** troppo**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="11f3b-167">Only allows network traffic from **WebRole1** too**WorkerRole1**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="11f3b-168">Scenario 4</span><span class="sxs-lookup"><span data-stu-id="11f3b-168">Scenario 4</span></span>
<span data-ttu-id="11f3b-169">Consente solo il traffico di rete da **WebRole1** troppo**WorkerRole1**, **WebRole1** troppo**WorkerRole2**, e  **WorkerRole1** troppo**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="11f3b-169">Only allows network traffic from **WebRole1** too**WorkerRole1**, **WebRole1** too**WorkerRole2**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

<span data-ttu-id="11f3b-170">Un riferimento XML schema per gli elementi di hello precedente è reperibile [qui](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="11f3b-170">An XML schema reference for hello elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="11f3b-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11f3b-171">Next steps</span></span>
<span data-ttu-id="11f3b-172">Per ulteriori informazioni sugli hello servizio Cloud [modello](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="11f3b-172">Read more about hello Cloud Service [model](cloud-services-model-and-package.md).</span></span>

