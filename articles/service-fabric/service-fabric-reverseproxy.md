---
title: proxy inverso aaaAzure Service Fabric | Documenti Microsoft
description: Utilizza un proxy inverso dell'infrastruttura servizio per la comunicazione toomicroservices dall'interno e all'esterno del cluster di hello.
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="23351-103">Proxy inverso in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="23351-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="23351-104">proxy inverso Hello compilato in Azure Service Fabric indirizzi microservizi nel cluster di Service Fabric hello che espone gli endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="23351-104">hello reverse proxy that's built into Azure Service Fabric addresses microservices in hello Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="23351-105">Modello di comunicazione di microservizi</span><span class="sxs-lookup"><span data-stu-id="23351-105">Microservices communication model</span></span>
<span data-ttu-id="23351-106">Microservizi nell'infrastruttura del servizio in genere eseguiti su un sottoinsieme di macchine virtuali nel cluster hello e spostarsi da una macchina virtuale tooanother per vari motivi.</span><span class="sxs-lookup"><span data-stu-id="23351-106">Microservices in Service Fabric typically run on a subset of virtual machines in hello cluster and can move from one virtual machine tooanother for various reasons.</span></span> <span data-ttu-id="23351-107">In tal caso, gli endpoint di hello per microservizi può essere modificato dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="23351-107">So, hello endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="23351-108">Hello tipico modello toocommunicate toohello microservizio è seguente hello risolvere ciclo:</span><span class="sxs-lookup"><span data-stu-id="23351-108">hello typical pattern toocommunicate toohello microservice is hello following resolve loop:</span></span>

1. <span data-ttu-id="23351-109">Risolvere il percorso del servizio hello inizialmente tramite servizio di denominazione hello.</span><span class="sxs-lookup"><span data-stu-id="23351-109">Resolve hello service location initially through hello naming service.</span></span>
2. <span data-ttu-id="23351-110">Connettere il servizio toohello.</span><span class="sxs-lookup"><span data-stu-id="23351-110">Connect toohello service.</span></span>
3. <span data-ttu-id="23351-111">Determinare hello causa degli errori di connessione e risolvere nuovo percorso del servizio di hello quando necessario.</span><span class="sxs-lookup"><span data-stu-id="23351-111">Determine hello cause of connection failures, and resolve hello service location again when necessary.</span></span>

<span data-ttu-id="23351-112">Questo processo è in genere implica il wrapping delle librerie di comunicazione client-side in un ciclo di tentativi che implementa criteri di risoluzione e ripetere servizi hello.</span><span class="sxs-lookup"><span data-stu-id="23351-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements hello service resolution and retry policies.</span></span>
<span data-ttu-id="23351-113">Per altre informazioni, vedere [Connettersi e comunicare con i servizi](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="23351-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-hello-reverse-proxy"></a><span data-ttu-id="23351-114">La comunicazione tramite proxy inverso hello</span><span class="sxs-lookup"><span data-stu-id="23351-114">Communicating by using hello reverse proxy</span></span>
<span data-ttu-id="23351-115">proxy inverso di Hello nell'infrastruttura del servizio viene eseguito su tutti i nodi nel cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="23351-115">hello reverse proxy in Service Fabric runs on all hello nodes in hello cluster.</span></span> <span data-ttu-id="23351-116">Consente di processo di risoluzione hello intero servizio per conto del client e inoltra la richiesta di hello del client.</span><span class="sxs-lookup"><span data-stu-id="23351-116">It performs hello entire service resolution process on a client's behalf and then forwards hello client request.</span></span> <span data-ttu-id="23351-117">In tal caso, i client in esecuzione nel cluster hello possono usare qualsiasi servizio di destinazione di sul lato client HTTP comunicazione librerie tootalk toohello mediante un proxy inverso di hello che viene eseguito localmente su hello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="23351-117">So, clients that run on hello cluster can use any client-side HTTP communication libraries tootalk toohello target service by using hello reverse proxy that runs locally on hello same node.</span></span>

![Comunicazione interna][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a><span data-ttu-id="23351-119">Raggiungere microservizi dal cluster hello esterno</span><span class="sxs-lookup"><span data-stu-id="23351-119">Reaching microservices from outside hello cluster</span></span>
<span data-ttu-id="23351-120">modello di comunicazione esterna Hello predefinito per microservizi è un modello di consenso esplicito in ogni servizio può accedervi direttamente da client esterni.</span><span class="sxs-lookup"><span data-stu-id="23351-120">hello default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="23351-121">[Il bilanciamento del carico Azure](../load-balancer/load-balancer-overview.md), che è un limite di rete tra microservizi e i client esterni, esegue la conversione degli indirizzi di rete e che esegue l'inoltro esterno richiede toointernal creato endpoint.</span><span class="sxs-lookup"><span data-stu-id="23351-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests toointernal IP:port endpoints.</span></span> <span data-ttu-id="23351-122">toomake client di tooexternal direttamente accessibile del microservizio un endpoint, è innanzitutto necessario configurare il bilanciamento del carico tooforward traffico tooeach porta che hello servizio utilizza cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23351-122">toomake a microservice's endpoint directly accessible tooexternal clients, you must first configure Load Balancer tooforward traffic tooeach port that hello service uses in hello cluster.</span></span> <span data-ttu-id="23351-123">Inoltre, la maggior parte delle microservizi, soprattutto con stato microservizi, non in tempo reale su tutti i nodi del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="23351-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of hello cluster.</span></span> <span data-ttu-id="23351-124">Hello microservizi possono spostare tra i nodi di failover.</span><span class="sxs-lookup"><span data-stu-id="23351-124">hello microservices can move between nodes on failover.</span></span> <span data-ttu-id="23351-125">In questi casi, bilanciamento del carico non è possibile determinare in modo efficace percorso hello del nodo di destinazione hello di hello repliche toowhich inoltra il traffico.</span><span class="sxs-lookup"><span data-stu-id="23351-125">In such cases, Load Balancer cannot effectively determine hello location of hello target node of hello replicas toowhich it should forward traffic.</span></span>

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a><span data-ttu-id="23351-126">Raggiungere microservizi attraverso il proxy inverso hello dal cluster hello esterno</span><span class="sxs-lookup"><span data-stu-id="23351-126">Reaching microservices via hello reverse proxy from outside hello cluster</span></span>
<span data-ttu-id="23351-127">Anziché configurare una porta hello di un singolo servizio di bilanciamento del carico, è possibile configurare solo hello porta proxy inverso hello nel servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="23351-127">Instead of configuring hello port of an individual service in Load Balancer, you can configure just hello port of hello reverse proxy in Load Balancer.</span></span> <span data-ttu-id="23351-128">Questa configurazione consente ai client esterni a cluster hello raggiungere servizi all'interno di cluster hello tramite proxy inverso di hello senza alcuna configurazione aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="23351-128">This configuration lets clients outside hello cluster reach services inside hello cluster by using hello reverse proxy without additional configuration.</span></span>

![Comunicazione esterna][0]

> [!WARNING]
> <span data-ttu-id="23351-130">Quando si configura la porta del proxy inverso hello in servizio di bilanciamento del carico, sono indirizzabili da all'esterno del cluster hello microservizi tutti i cluster hello che espongono un endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="23351-130">When you configure hello reverse proxy's port in Load Balancer, all microservices in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a><span data-ttu-id="23351-131">Formato dell'URI per l'indirizzamento di servizi mediante un proxy inverso hello</span><span class="sxs-lookup"><span data-stu-id="23351-131">URI format for addressing services by using hello reverse proxy</span></span>
<span data-ttu-id="23351-132">Usa proxy inverso di Hello che deve essere inoltrata un'URI specifico identifier (URI) formato tooidentify hello partizione toowhich hello in arrivo richiesta di servizio:</span><span class="sxs-lookup"><span data-stu-id="23351-132">hello reverse proxy uses a specific uniform resource identifier (URI) format tooidentify hello service partition toowhich hello incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="23351-133">**http (s):** proxy inverso hello può essere configurato tooaccept HTTP o il traffico HTTPS.</span><span class="sxs-lookup"><span data-stu-id="23351-133">**http(s):** hello reverse proxy can be configured tooaccept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="23351-134">Per l'inoltro di HTTPS, fare riferimento troppo[connessione servizio protetto tooa con proxy inverso hello](service-fabric-reverseproxy-configure-secure-communication.md) dopo aver toolisten il programma di installazione di proxy inverso su HTTPS.</span><span class="sxs-lookup"><span data-stu-id="23351-134">For HTTPS forwarding, refer too[Connect tooa secure service with hello reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup toolisten on HTTPS.</span></span>
* <span data-ttu-id="23351-135">**Nome del cluster nome di dominio completo (FQDN) | indirizzo IP interno:** per i client esterni, è possibile configurare proxy inverso hello in modo che sia raggiungibile tramite dominio cluster hello, ad esempio mycluster.eastus.cloudapp.azure.com. Per impostazione predefinita, i proxy inverso hello viene eseguito in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="23351-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure hello reverse proxy so that it is reachable through hello cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, hello reverse proxy runs on every node.</span></span> <span data-ttu-id="23351-136">Per il traffico interno, proxy inverso hello può essere raggiunto in localhost o in qualsiasi indirizzo IP nodo interno, ad esempio 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="23351-136">For internal traffic, hello reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="23351-137">**Porta:** porta hello, ad esempio 19081, che è stato specificato per il proxy inverso hello.</span><span class="sxs-lookup"><span data-stu-id="23351-137">**Port:** This is hello port, such as 19081, that has been specified for hello reverse proxy.</span></span>
* <span data-ttu-id="23351-138">**ServiceInstanceName:** hello di nome completo dell'istanza di servizio hello distribuito che si sta tentando di tooreach senza hello "fabric: /" dello schema.</span><span class="sxs-lookup"><span data-stu-id="23351-138">**ServiceInstanceName:** This is hello fully-qualified name of hello deployed service instance that you are trying tooreach without hello "fabric:/" scheme.</span></span> <span data-ttu-id="23351-139">Ad esempio, tooreach hello *fabric: / myapp/myservice/* servizio, si utilizzerebbe *myapp/myservice*.</span><span class="sxs-lookup"><span data-stu-id="23351-139">For example, tooreach hello *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="23351-140">nome dell'istanza del servizio Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="23351-140">hello service instance name is case-sensitive.</span></span> <span data-ttu-id="23351-141">Utilizzando una maiuscole/minuscole del nome di istanza servizio hello nell'URL hello determina hello richieste toofail con 404 (non trovato).</span><span class="sxs-lookup"><span data-stu-id="23351-141">Using a different casing for hello service instance name in hello URL causes hello requests toofail with 404 (Not Found).</span></span>
* <span data-ttu-id="23351-142">**Percorso di suffisso:** si tratta di percorso URL effettivo hello, ad esempio *myapi/valori/Aggiungi/3*, per il servizio di hello che si desidera tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="23351-142">**Suffix path:** This is hello actual URL path, such as *myapi/values/add/3*, for hello service that you want tooconnect to.</span></span>
* <span data-ttu-id="23351-143">**PartitionKey:** per un servizio partizionato, si tratta di chiave di partizione calcolata hello della partizione hello che si desidera tooreach.</span><span class="sxs-lookup"><span data-stu-id="23351-143">**PartitionKey:** For a partitioned service, this is hello computed partition key of hello partition that you want tooreach.</span></span> <span data-ttu-id="23351-144">Si noti che questo *non* hello GUID dell'ID di partizione.</span><span class="sxs-lookup"><span data-stu-id="23351-144">Note that this is *not* hello partition ID GUID.</span></span> <span data-ttu-id="23351-145">Questo parametro non è obbligatorio per i servizi che utilizzano lo schema di partizione singleton hello.</span><span class="sxs-lookup"><span data-stu-id="23351-145">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="23351-146">**PartitionKind:** schema di partizione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="23351-146">**PartitionKind:** This is hello service partition scheme.</span></span> <span data-ttu-id="23351-147">Può essere "Int64Range" o "Named".</span><span class="sxs-lookup"><span data-stu-id="23351-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="23351-148">Questo parametro non è obbligatorio per i servizi che utilizzano lo schema di partizione singleton hello.</span><span class="sxs-lookup"><span data-stu-id="23351-148">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="23351-149">**ListenerName** endpoint hello dal servizio hello sono hello formato {"Endpoint": {"Listener1": "Endpoint1", "Listener2": "Endpoint2"...}}.</span><span class="sxs-lookup"><span data-stu-id="23351-149">**ListenerName** hello endpoints from hello service are of hello form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="23351-150">Quando il servizio di hello espone più endpoint, endpoint hello identifica tale richiesta hello del client deve essere inoltrato a.</span><span class="sxs-lookup"><span data-stu-id="23351-150">When hello service exposes multiple endpoints, this identifies hello endpoint that hello client request should be forwarded to.</span></span> <span data-ttu-id="23351-151">Può essere omesso se hello servizio dispone di un solo listener.</span><span class="sxs-lookup"><span data-stu-id="23351-151">This can be omitted if hello service has only one listener.</span></span>
* <span data-ttu-id="23351-152">**TargetReplicaSelector** specifica come replica di destinazione hello o istanza deve essere selezionata.</span><span class="sxs-lookup"><span data-stu-id="23351-152">**TargetReplicaSelector** This specifies how hello target replica or instance should be selected.</span></span>
  * <span data-ttu-id="23351-153">Quando il servizio di destinazione hello è con stato, può essere uno dei seguenti hello hello TargetReplicaSelector: 'PrimaryReplica', 'RandomSecondaryReplica' o 'RandomReplica'.</span><span class="sxs-lookup"><span data-stu-id="23351-153">When hello target service is stateful, hello TargetReplicaSelector can be one of hello following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="23351-154">Quando questo parametro viene omesso, il valore predefinito di hello è 'PrimaryReplica'.</span><span class="sxs-lookup"><span data-stu-id="23351-154">When this parameter is not specified, hello default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="23351-155">Quando il servizio di destinazione hello è senza stato, proxy inverso prende un'istanza di hello partizione tooforward hello richiesta al servizio per casuale.</span><span class="sxs-lookup"><span data-stu-id="23351-155">When hello target service is stateless, reverse proxy picks a random instance of hello service partition tooforward hello request to.</span></span>
* <span data-ttu-id="23351-156">**Timeout:** specifica hello timeout per la richiesta HTTP hello creato dal servizio di toohello hello proxy inverso per conto di richiesta di hello del client.</span><span class="sxs-lookup"><span data-stu-id="23351-156">**Timeout:**  This specifies hello timeout for hello HTTP request created by hello reverse proxy toohello service on behalf of hello client request.</span></span> <span data-ttu-id="23351-157">valore predefinito di Hello è 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="23351-157">hello default value is 60 seconds.</span></span> <span data-ttu-id="23351-158">Questo è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="23351-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="23351-159">Esempio di utilizzo</span><span class="sxs-lookup"><span data-stu-id="23351-159">Example usage</span></span>
<span data-ttu-id="23351-160">Ad esempio, è opportuno hello *fabric: / MyApp/MyService* servizio che consente di aprire un listener HTTP sull'hello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="23351-160">As an example, let's take hello *fabric:/MyApp/MyService* service that opens an HTTP listener on hello following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="23351-161">Di seguito sono risorse hello per il servizio di hello:</span><span class="sxs-lookup"><span data-stu-id="23351-161">Following are hello resources for hello service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="23351-162">Se il servizio di hello utilizza singleton hello schema di partizionamento, hello *PartitionKey* e *PartitionKind* parametri di stringa di query non sono necessari e servizio hello può essere raggiunto tramite gateway hello come:</span><span class="sxs-lookup"><span data-stu-id="23351-162">If hello service uses hello singleton partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters are not required, and hello service can be reached by using hello gateway as:</span></span>

* <span data-ttu-id="23351-163">Esternamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="23351-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="23351-164">Internamente: `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="23351-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="23351-165">Se il servizio di hello utilizza hello Int64 uniformi schema di partizionamento, hello *PartitionKey* e *PartitionKind* i parametri di stringa di query devono essere utilizzato tooreach una partizione del servizio hello:</span><span class="sxs-lookup"><span data-stu-id="23351-165">If hello service uses hello Uniform Int64 partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters must be used tooreach a partition of hello service:</span></span>

* <span data-ttu-id="23351-166">Esternamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="23351-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="23351-167">Internamente: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="23351-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="23351-168">risorse hello tooreach che espone il servizio di hello, posizionare semplicemente percorso della risorsa hello dopo il nome del servizio hello hello URL:</span><span class="sxs-lookup"><span data-stu-id="23351-168">tooreach hello resources that hello service exposes, simply place hello resource path after hello service name in hello URL:</span></span>

* <span data-ttu-id="23351-169">Esternamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="23351-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="23351-170">Internamente: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="23351-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="23351-171">gateway Hello inoltrerà quindi URL del servizio toohello queste richieste:</span><span class="sxs-lookup"><span data-stu-id="23351-171">hello gateway will then forward these requests toohello service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="23351-172">Gestione speciale per servizi di condivisione porta</span><span class="sxs-lookup"><span data-stu-id="23351-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="23351-173">Gateway applicazione Azure tenta tooresolve un servizio risolvere nuovamente e ripetere la richiesta di hello quando un servizio non è raggiungibile.</span><span class="sxs-lookup"><span data-stu-id="23351-173">Azure Application Gateway attempts tooresolve a service address again and retry hello request when a service cannot be reached.</span></span> <span data-ttu-id="23351-174">Si tratta dei principali vantaggi di Gateway applicazione perché il codice client non necessario tooimplement risoluzione per il proprio servizio e risolvere il ciclo.</span><span class="sxs-lookup"><span data-stu-id="23351-174">This is a major benefit of Application Gateway because client code does not need tooimplement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="23351-175">In genere, quando un servizio non è raggiungibile, l'istanza del servizio hello o la replica è stato spostato tooa nodo diverso come parte del ciclo di vita normale.</span><span class="sxs-lookup"><span data-stu-id="23351-175">Generally, when a service cannot be reached, hello service instance or replica has moved tooa different node as part of its normal lifecycle.</span></span> <span data-ttu-id="23351-176">In questo caso, Gateway applicazione potrebbe ricevere un rete connessione errore che indica che un endpoint non aperto più hello risolto originariamente indirizzo.</span><span class="sxs-lookup"><span data-stu-id="23351-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on hello originally resolved address.</span></span>

<span data-ttu-id="23351-177">Tuttavia, le repliche o le istanze del servizio possono condividere un processo host e una porta quando ospitate da un server Web basato su http.sys, tra cui:</span><span class="sxs-lookup"><span data-stu-id="23351-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="23351-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="23351-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="23351-179">WebListener ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="23351-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="23351-180">Katana</span><span class="sxs-lookup"><span data-stu-id="23351-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="23351-181">In questo caso, è probabile che il server web hello è disponibile nel processo host hello e risponde toorequests ma hello risolto l'istanza del servizio o di replica non è più disponibile nell'host di hello.</span><span class="sxs-lookup"><span data-stu-id="23351-181">In this situation, it is likely that hello web server is available in hello host process and responding toorequests, but hello resolved service instance or replica is no longer available on hello host.</span></span> <span data-ttu-id="23351-182">In questo caso, i gateway hello riceverà una risposta HTTP 404 dal server web hello.</span><span class="sxs-lookup"><span data-stu-id="23351-182">In this case, hello gateway will receive an HTTP 404 response from hello web server.</span></span> <span data-ttu-id="23351-183">Un errore HTTP 404 presenta quindi due significati distinti:</span><span class="sxs-lookup"><span data-stu-id="23351-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="23351-184">Caso #1: indirizzo del servizio hello è corretto, ma la risorsa hello che hello l'utente ha richiesto non esiste.</span><span class="sxs-lookup"><span data-stu-id="23351-184">Case #1: hello service address is correct, but hello resource that hello user requested does not exist.</span></span>
- <span data-ttu-id="23351-185">Caso &#2;: indirizzo del servizio hello è corretto e potrebbe esistere risorsa hello hello richiesto dall'utente in un nodo diverso.</span><span class="sxs-lookup"><span data-stu-id="23351-185">Case #2: hello service address is incorrect, and hello resource that hello user requested might exist on a different node.</span></span>

<span data-ttu-id="23351-186">Hello primo caso è un normale HTTP 404, che è considerata un errore dell'utente.</span><span class="sxs-lookup"><span data-stu-id="23351-186">hello first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="23351-187">Tuttavia, nel secondo caso hello utente hello ha richiesto una risorsa che esiste.</span><span class="sxs-lookup"><span data-stu-id="23351-187">However, in hello second case, hello user has requested a resource that does exist.</span></span> <span data-ttu-id="23351-188">Gateway applicazione è stato Impossibile toolocate che è stato spostato perché hello servizio stesso.</span><span class="sxs-lookup"><span data-stu-id="23351-188">Application Gateway was unable toolocate it because hello service itself has moved.</span></span> <span data-ttu-id="23351-189">Applicazione esigenze tooresolve hello indirizzo Gateway nuovamente e ripetere la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="23351-189">Application Gateway needs tooresolve hello address again and retry hello request.</span></span>

<span data-ttu-id="23351-190">Gateway applicazione deve pertanto un toodistinguish modo tra questi due casi.</span><span class="sxs-lookup"><span data-stu-id="23351-190">Application Gateway thus needs a way toodistinguish between these two cases.</span></span> <span data-ttu-id="23351-191">toomake che distinzione, un suggerimento dal server hello è necessario.</span><span class="sxs-lookup"><span data-stu-id="23351-191">toomake that distinction, a hint from hello server is required.</span></span>

* <span data-ttu-id="23351-192">Per impostazione predefinita, il Gateway applicazione presuppone caso &#2; e tenta nuovamente di richiesta hello tooresolve e il problema.</span><span class="sxs-lookup"><span data-stu-id="23351-192">By default, Application Gateway assumes case #2 and attempts tooresolve and issue hello request again.</span></span>
* <span data-ttu-id="23351-193">tooindicate caso &#1; tooApplication Gateway, il servizio di hello deve restituire hello intestazione risposta HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="23351-193">tooindicate case #1 tooApplication Gateway, hello service should return hello following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="23351-194">L'intestazione della risposta HTTP indica una situazione di HTTP 404 normale in cui hello risorsa richiesta non esiste e il Gateway applicazione non tenterà nuovamente indirizzo del servizio tooresolve hello.</span><span class="sxs-lookup"><span data-stu-id="23351-194">This HTTP response header indicates a normal HTTP 404 situation in which hello requested resource does not exist, and Application Gateway will not attempt tooresolve hello service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="23351-195">Installazione e configurazione</span><span class="sxs-lookup"><span data-stu-id="23351-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="23351-196">Abilitare il proxy inverso tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="23351-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="23351-197">Portale di Azure fornisce un proxy inverso di opzione tooenable durante la creazione di un nuovo cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="23351-197">Azure portal provides an option tooenable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="23351-198">In **cluster di Service Fabric crea**, passaggio 2: configurazione del Cluster, configurazione del tipo di nodo, selezionare la casella di controllo di hello troppo "Abilitazione proxy inverso".</span><span class="sxs-lookup"><span data-stu-id="23351-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select hello checkbox too"Enable reverse proxy".</span></span>
<span data-ttu-id="23351-199">Per la configurazione di proxy inverso sicura, è possibile specificare il certificato SSL nel passaggio 3: protezione, configurare le impostazioni di sicurezza cluster, la casella di controllo selezionare hello troppo "Include un certificato SSL per il proxy inverso" e immettere i dettagli del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="23351-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select hello checkbox too"Include a SSL certificate for reverse proxy" and enter hello certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="23351-200">Abilitare il proxy inverso tramite modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="23351-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="23351-201">È possibile utilizzare hello [modello di Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable hello proxy inverso nell'infrastruttura del servizio per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23351-201">You can use hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) tooenable hello reverse proxy in Service Fabric for hello cluster.</span></span>

<span data-ttu-id="23351-202">Fare riferimento troppo[Proxy inverso HTTPS di configurare in un cluster protetto](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) per Gestione risorse di Azure tooconfigure proxy inverso protetta con un rollover dei certificati di certificato e la gestione degli esempi di modello.</span><span class="sxs-lookup"><span data-stu-id="23351-202">Refer too[Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples tooconfigure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="23351-203">In primo luogo, si ottiene il modello di hello per cluster hello che si desidera toodeploy.</span><span class="sxs-lookup"><span data-stu-id="23351-203">First, you get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="23351-204">È possibile utilizzare i modelli di esempio hello o creare un modello di gestione risorse personalizzato.</span><span class="sxs-lookup"><span data-stu-id="23351-204">You can either use hello sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="23351-205">Quindi, è possibile abilitare i proxy inverso hello utilizzando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="23351-205">Then, you can enable hello reverse proxy by using hello following steps:</span></span>

1. <span data-ttu-id="23351-206">Definire una porta per il proxy inverso hello in hello [sezione parametri](../azure-resource-manager/resource-group-authoring-templates.md) del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="23351-206">Define a port for hello reverse proxy in hello [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of hello template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="23351-207">Specificare la porta hello per tutti gli oggetti di tipo di nodo hello in hello **Cluster** [sezione tipo di risorsa](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="23351-207">Specify hello port for each of hello nodetype objects in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="23351-208">porta Hello è identificata dal nome del parametro hello, reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="23351-208">hello port is identified by hello parameter name, reverseProxyEndpointPort.</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. <span data-ttu-id="23351-209">hello tooaddress proxy inverso da hello all'esterno del cluster di Azure, imposta le regole di bilanciamento del carico di Azure hello per la porta hello specificata nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="23351-209">tooaddress hello reverse proxy from outside hello Azure cluster, set up hello Azure Load Balancer rules for hello port that you specified in step 1.</span></span>

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. <span data-ttu-id="23351-210">i certificati SSL tooconfigure sulla porta hello di proxy inverso hello, aggiungere hello certificato toohello ***reverseProxyCertificate*** proprietà hello **Cluster** [sezionetipodirisorsa](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="23351-210">tooconfigure SSL certificates on hello port for hello reverse proxy, add hello certificate toohello ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a><span data-ttu-id="23351-211">Supporto di un certificato di proxy inverso che è diverso dal certificato cluster hello</span><span class="sxs-lookup"><span data-stu-id="23351-211">Supporting a reverse proxy certificate that's different from hello cluster certificate</span></span>
 <span data-ttu-id="23351-212">Se il certificato di proxy inverso hello è diverso dal certificato hello che protegge cluster hello, quindi hello specificato in precedenza certificato deve essere installato nella macchina virtuale hello e aggiunti toohello elenco di controllo di accesso (ACL) in modo che possano Service Fabric diritti di accesso.</span><span class="sxs-lookup"><span data-stu-id="23351-212">If hello reverse proxy certificate is different from hello certificate that secures hello cluster, then hello previously specified certificate should be installed on hello virtual machine and added toohello access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="23351-213">Questa operazione può essere eseguita in hello **virtualMachineScaleSets** [sezione tipo di risorsa](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="23351-213">This can be done in hello **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="23351-214">Per l'installazione, aggiungere tale osProfile toohello certificato.</span><span class="sxs-lookup"><span data-stu-id="23351-214">For installation, add that certificate toohello osProfile.</span></span> <span data-ttu-id="23351-215">sezione di estensione Hello del modello di hello è possibile aggiornare il certificato di hello in hello ACL.</span><span class="sxs-lookup"><span data-stu-id="23351-215">hello extension section of hello template can update hello certificate in hello ACL.</span></span>

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> <span data-ttu-id="23351-216">Quando si usano i certificati che sono diversi da hello cluster certificato tooenable hello proxy inverso di un cluster esistente, installare il certificato di proxy inverso hello e aggiornare hello ACL nel cluster hello prima di abilitare proxy inverso hello.</span><span class="sxs-lookup"><span data-stu-id="23351-216">When you use certificates that are different from hello cluster certificate tooenable hello reverse proxy on an existing cluster, install hello reverse proxy certificate and update hello ACL on hello cluster before you enable hello reverse proxy.</span></span> <span data-ttu-id="23351-217">Hello completo [modello di Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) distribuzione usando le impostazioni di hello menzionate in precedenza prima di avviare un proxy inverso di distribuzione tooenable hello in passaggi 1-4.</span><span class="sxs-lookup"><span data-stu-id="23351-217">Complete hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using hello settings mentioned previously before you start a deployment tooenable hello reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23351-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23351-218">Next steps</span></span>
* <span data-ttu-id="23351-219">Vedere un esempio di comunicazione HTTP tra i servizi in un [progetto di esempio in GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="23351-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="23351-220">Servizio HTTP toosecure di inoltro con proxy inverso hello</span><span class="sxs-lookup"><span data-stu-id="23351-220">Forwarding toosecure HTTP service with hello reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="23351-221">Chiamate di procedura remota con i Reliable Services remoti</span><span class="sxs-lookup"><span data-stu-id="23351-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="23351-222">Web API che usa OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="23351-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="23351-223">Comunicazione di WCF tramite Reliable Services</span><span class="sxs-lookup"><span data-stu-id="23351-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="23351-224">Per altre opzioni di configurazione del proxy inverso, vedere la sezione ApplicationGateway/Http in [Personalizzare le impostazioni del cluster Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="23351-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
