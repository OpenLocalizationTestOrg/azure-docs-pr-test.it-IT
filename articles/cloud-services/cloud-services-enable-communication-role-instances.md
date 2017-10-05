---
title: Comunicazione per i ruoli in servizi Cloud | Documentazione Microsoft
description: Le istanze del ruolo in servizi Cloud possono avere endpoint (http, https, tcp, udp) definiti appositamente che comunicano con l'esterno oppure tra le altre istanze del ruolo.
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
ms.openlocfilehash: 8e171d56bb67c971337fa383014988074ec828b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="16c31-103">Abilitare la comunicazione delle istanze del ruolo in azure</span><span class="sxs-lookup"><span data-stu-id="16c31-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="16c31-104">I ruoli del servizio cloud comunicano tramite connessioni interne ed esterne.</span><span class="sxs-lookup"><span data-stu-id="16c31-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="16c31-105">Le connessioni esterne vengono chiamate **endpoint di input** mentre le connessioni interne vengono chiamate **endpoint interni**.</span><span class="sxs-lookup"><span data-stu-id="16c31-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="16c31-106">In questo argomento viene descritto come modificare la [definizione del servizio](cloud-services-model-and-package.md#csdef) per creare gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="16c31-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="16c31-107">Endpoint di input</span><span class="sxs-lookup"><span data-stu-id="16c31-107">Input endpoint</span></span>
<span data-ttu-id="16c31-108">L'endpoint di input viene utilizzato quando si desidera esporre una porta all'esterno.</span><span class="sxs-lookup"><span data-stu-id="16c31-108">The input endpoint is used when you want to expose a port to the outside.</span></span> <span data-ttu-id="16c31-109">Specificare il tipo di protocollo e porta dell'endpoint che vengono poi applicati per le porte interne ed esterne per l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="16c31-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span></span> <span data-ttu-id="16c31-110">Se si desidera, è possibile specificare una porta interna diversa per l'endpoint con l’attributo [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) .</span><span class="sxs-lookup"><span data-stu-id="16c31-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="16c31-111">L'endpoint di input può utilizzare i seguenti protocolli: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="16c31-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="16c31-112">Per creare un endpoint di input, aggiungere elemento figlio **InputEndpoint** all'elemento **Endpoints** del ruolo di lavoro o del ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="16c31-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="16c31-113">Endpoint di input dell'istanza</span><span class="sxs-lookup"><span data-stu-id="16c31-113">Instance input endpoint</span></span>
<span data-ttu-id="16c31-114">Gli endpoint di input dell'istanza sono simili agli endpoint di input ma consentono di eseguire il mapping di specifiche porte pubbliche per ogni singola istanza del ruolo mediante il port forwarding nel servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="16c31-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span></span> <span data-ttu-id="16c31-115">È possibile specificare una singola porta pubblica o un intervallo di porte.</span><span class="sxs-lookup"><span data-stu-id="16c31-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="16c31-116">L'endpoint di input dell’istanza può usare solo i protocolli **tcp** o **udp**.</span><span class="sxs-lookup"><span data-stu-id="16c31-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span></span>

<span data-ttu-id="16c31-117">Per creare un endpoint di input dell'istanza, aggiungere l'elemento figlio **InstanceInputEndpoint** all'elemento **Endpoints** del ruolo di lavoro o del ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="16c31-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="16c31-118">Endpoint interno</span><span class="sxs-lookup"><span data-stu-id="16c31-118">Internal endpoint</span></span>
<span data-ttu-id="16c31-119">Gli endpoint interni sono disponibili per la comunicazione da istanza a istanza.</span><span class="sxs-lookup"><span data-stu-id="16c31-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="16c31-120">La porta è facoltativa e se omessa, viene assegnata una porta dinamica all'endpoint.</span><span class="sxs-lookup"><span data-stu-id="16c31-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span></span> <span data-ttu-id="16c31-121">Può essere utilizzato un intervallo di porte.</span><span class="sxs-lookup"><span data-stu-id="16c31-121">A port range can be used.</span></span> <span data-ttu-id="16c31-122">Esiste un limite di cinque endpoint interni per ogni ruolo.</span><span class="sxs-lookup"><span data-stu-id="16c31-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="16c31-123">L'endpoint interno può utilizzare i seguenti protocolli: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="16c31-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="16c31-124">Per creare un endpoint di input interno, aggiungere l'elemento figlio **InternalEndpoint** all'elemento **Endpoints** del ruolo di lavoro o del ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="16c31-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="16c31-125">È possibile inoltre utilizzare un intervallo di porte.</span><span class="sxs-lookup"><span data-stu-id="16c31-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="16c31-126">Ruoli di lavoro a confronto con Ruoli Web</span><span class="sxs-lookup"><span data-stu-id="16c31-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="16c31-127">Esiste una piccola differenza tra gli endpoint quando si lavora con i ruoli di lavoro e i ruoli  web.</span><span class="sxs-lookup"><span data-stu-id="16c31-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="16c31-128">Il ruolo web deve disporre almeno di un singolo endpoint di input che utilizzi il protocollo **HTTP** .</span><span class="sxs-lookup"><span data-stu-id="16c31-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after the first InputEndPoint -->
</Endpoints>
```

## <a name="using-the-net-sdk-to-access-an-endpoint"></a><span data-ttu-id="16c31-129">Uso di .NET SDK per accedere ad un endpoint</span><span class="sxs-lookup"><span data-stu-id="16c31-129">Using the .NET SDK to access an endpoint</span></span>
<span data-ttu-id="16c31-130">La libreria gestita di Azure fornisce metodi per la comunicazione di istanze del ruolo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="16c31-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span></span> <span data-ttu-id="16c31-131">Dal codice eseguito all'interno di un'istanza del ruolo, è possibile recuperare informazioni sull'esistenza di altre istanze del ruolo e sui relativi endpoint, nonché le informazioni sull'istanza del ruolo corrente.</span><span class="sxs-lookup"><span data-stu-id="16c31-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="16c31-132">È possibile recuperare solo le informazioni sulle istanze dei ruoli che sono in esecuzione nel servizio cloud e che definiscono almeno un endpoint interno.</span><span class="sxs-lookup"><span data-stu-id="16c31-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="16c31-133">Non è possibile ottenere dati sulle istanze dei ruoli in esecuzione in un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="16c31-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="16c31-134">È possibile utilizzare la proprietà [Istanze](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) per recuperare le istanze di un ruolo.</span><span class="sxs-lookup"><span data-stu-id="16c31-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span></span> <span data-ttu-id="16c31-135">Usare prima di tutto [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) per restituire un riferimento all'istanza del ruolo corrente, quindi usare la proprietà [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) per restituire un riferimento al ruolo stesso.</span><span class="sxs-lookup"><span data-stu-id="16c31-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span></span>

<span data-ttu-id="16c31-136">Quando ci si connette a un'istanza del ruolo a livello di programmazione tramite il SDK di .NET, è relativamente semplice accedere alle informazioni relative all’endpoint.</span><span class="sxs-lookup"><span data-stu-id="16c31-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span></span> <span data-ttu-id="16c31-137">Ad esempio, dopo essersi connessi a un ambiente di ruolo specifico, è possibile ottenere la porta di un endpoint specifico con il seguente codice:</span><span class="sxs-lookup"><span data-stu-id="16c31-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="16c31-138">La proprietà **Instances** restituisce una raccolta di oggetti **RoleInstance**.</span><span class="sxs-lookup"><span data-stu-id="16c31-138">The **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="16c31-139">Tale raccolta contiene sempre l'istanza corrente.</span><span class="sxs-lookup"><span data-stu-id="16c31-139">This collection always contains the current instance.</span></span> <span data-ttu-id="16c31-140">Se il ruolo non definisce un endpoint interno, la raccolta include l'istanza corrente ma non altre istanze.</span><span class="sxs-lookup"><span data-stu-id="16c31-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span></span> <span data-ttu-id="16c31-141">Il numero di istanze del ruolo nella raccolta sarà sempre 1 nel caso in cui non sia stato definito alcun endpoint interno per il ruolo.</span><span class="sxs-lookup"><span data-stu-id="16c31-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span></span> <span data-ttu-id="16c31-142">Se il ruolo definisce un endpoint interno, le relative istanze sono individuabili in fase di esecuzione e il numero di istanze nella raccolta corrisponderà al numero di istanze specificato per il ruolo nel file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="16c31-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="16c31-143">La libreria gestita di Azure non rappresenta un mezzo per determinare lo stato di altre istanze del ruolo, ma è possibile implementare tali valutazioni manualmente se il servizio necessita di tale funzionalità.</span><span class="sxs-lookup"><span data-stu-id="16c31-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="16c31-144">È possibile utilizzare la [Diagnostica di Azure](cloud-services-dotnet-diagnostics.md) per ottenere informazioni sull'esecuzione di istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="16c31-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="16c31-145">Per determinare il numero di porta per un endpoint interno in un'istanza del ruolo, è possibile utilizzare la proprietà [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) per restituire un oggetto Dictionary che contenga i nomi degli endpoint e i corrispondenti indirizzi IP e porte.</span><span class="sxs-lookup"><span data-stu-id="16c31-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="16c31-146">La proprietà [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) restituisce l'indirizzo IP e la porta per un endpoint specificato.</span><span class="sxs-lookup"><span data-stu-id="16c31-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span></span> <span data-ttu-id="16c31-147">La proprietà **PublicIPEndpoint** restituisce la porta per un endpoint con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="16c31-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span></span> <span data-ttu-id="16c31-148">La parte relativa all’indirizzo IP della proprietà **PublicIPEndpoint** non viene utilizzata.</span><span class="sxs-lookup"><span data-stu-id="16c31-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="16c31-149">Di seguito è riportato un esempio che consente di eseguire l’iterazione delle istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="16c31-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="16c31-150">Di seguito è riportato un esempio di un ruolo di lavoro che ottiene l'endpoint esposto tramite la definizione del servizio e avvia l'ascolto per le connessioni.</span><span class="sxs-lookup"><span data-stu-id="16c31-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="16c31-151">Questo codice funziona solo per un servizio distribuito.</span><span class="sxs-lookup"><span data-stu-id="16c31-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="16c31-152">Durante l'esecuzione nell'emulatore di calcolo di Azure, gli elementi di configurazione del servizio che creano endpoint porte dirette (elementi**InstanceInputEndpoint** ) vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="16c31-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

        // Bind socket listener to internal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block the thread and wait for a client request
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
      // Set the maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-to-control-role-communication"></a><span data-ttu-id="16c31-153">Regole di traffico di rete per controllare la comunicazione di ruolo</span><span class="sxs-lookup"><span data-stu-id="16c31-153">Network traffic rules to control role communication</span></span>
<span data-ttu-id="16c31-154">Dopo aver definito gli endpoint interni, è possibile aggiungere regole del traffico di rete (in base agli endpoint che sono stati creati) per controllare il modo in cui le istanze del ruolo possono comunicare tra loro.</span><span class="sxs-lookup"><span data-stu-id="16c31-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span></span> <span data-ttu-id="16c31-155">Nel diagramma seguente vengono illustrati alcuni scenari comuni relativi al controllo della comunicazione del ruolo:</span><span class="sxs-lookup"><span data-stu-id="16c31-155">The following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="16c31-156">![Scenari di regole del traffico di rete](./media/cloud-services-enable-communication-role-instances/scenarios.png "Scenari di regole del traffico di rete")</span><span class="sxs-lookup"><span data-stu-id="16c31-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="16c31-157">Il seguente esempio di codice mostra le definizioni di ruolo per i ruoli illustrati nel diagramma precedente.</span><span class="sxs-lookup"><span data-stu-id="16c31-157">The following code example shows role definitions for the roles shown in the previous diagram.</span></span> <span data-ttu-id="16c31-158">Ogni definizione di ruolo include almeno un endpoint interno definito:</span><span class="sxs-lookup"><span data-stu-id="16c31-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="16c31-159">La restrizione della comunicazione tra ruoli può verificarsi con endpoint interni di porte fisse o assegnate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="16c31-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="16c31-160">Per impostazione predefinita, dopo aver definito un endpoint interno, la comunicazione può avvenire tra qualsiasi ruolo e l’endpoint interno di un ruolo senza restrizioni.</span><span class="sxs-lookup"><span data-stu-id="16c31-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="16c31-161">Per limitare la comunicazione, è necessario aggiungere un elemento **NetworkTrafficRules** all'elemento **ServiceDefinition** nel file di definizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="16c31-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="16c31-162">Scenario 1</span><span class="sxs-lookup"><span data-stu-id="16c31-162">Scenario 1</span></span>
<span data-ttu-id="16c31-163">Consentire solo il traffico di rete da **WebRole1** a **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="16c31-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="16c31-164">Scenario 2</span><span class="sxs-lookup"><span data-stu-id="16c31-164">Scenario 2</span></span>
<span data-ttu-id="16c31-165">Consente solo il traffico di rete da **WebRole1** a **WorkerRole1** e **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="16c31-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="16c31-166">Scenario 3</span><span class="sxs-lookup"><span data-stu-id="16c31-166">Scenario 3</span></span>
<span data-ttu-id="16c31-167">Consente solo il traffico di rete da **WebRole1** a **WorkerRole1** e da **WorkerRole1** a **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="16c31-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="16c31-168">Scenario 4</span><span class="sxs-lookup"><span data-stu-id="16c31-168">Scenario 4</span></span>
<span data-ttu-id="16c31-169">Consente solo il traffico di rete da **WebRole1** a **WorkerRole1**, **WebRole1** a **WorkerRole2** e da **WorkerRole1** a **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="16c31-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span></span>

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

<span data-ttu-id="16c31-170">Un riferimento allo schema XML per gli elementi utilizzati in precedenza è reperibile [qui](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="16c31-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="16c31-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16c31-171">Next steps</span></span>
<span data-ttu-id="16c31-172">Ulteriori informazioni sul [modello](cloud-services-model-and-package.md)del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="16c31-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span></span>

