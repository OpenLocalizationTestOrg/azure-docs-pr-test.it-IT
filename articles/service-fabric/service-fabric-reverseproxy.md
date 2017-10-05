---
title: Proxy inverso di Azure Service Fabric | Microsoft Docs
description: Usare un proxy inverso di Service Fabric per comunicare con i microservizi dall'interno e dall'esterno del cluster.
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
ms.openlocfilehash: 7897458e9e4a0bbe185bd3f7b4c133c1b26769f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="3a77a-103">Proxy inverso in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3a77a-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="3a77a-104">Il proxy inverso disponibile in Azure Service Fabric comunica con i microservizi nel cluster Service Fabric che espongono endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="3a77a-104">The reverse proxy that's built into Azure Service Fabric addresses microservices in the Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="3a77a-105">Modello di comunicazione di microservizi</span><span class="sxs-lookup"><span data-stu-id="3a77a-105">Microservices communication model</span></span>
<span data-ttu-id="3a77a-106">I microservizi in Service Fabric vengono in genere eseguiti su un sottoinsieme di macchine virtuali nel cluster e possono spostarsi da una macchina virtuale a un'altra per diversi motivi.</span><span class="sxs-lookup"><span data-stu-id="3a77a-106">Microservices in Service Fabric typically run on a subset of virtual machines in the cluster and can move from one virtual machine to another for various reasons.</span></span> <span data-ttu-id="3a77a-107">Gli endpoint per microservizi possono quindi cambiare in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="3a77a-107">So, the endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="3a77a-108">Il modello tipico di comunicazione con il microservizio è il ciclo di risoluzione seguente:</span><span class="sxs-lookup"><span data-stu-id="3a77a-108">The typical pattern to communicate to the microservice is the following resolve loop:</span></span>

1. <span data-ttu-id="3a77a-109">Risolvere la posizione del servizio inizialmente tramite il servizio Naming.</span><span class="sxs-lookup"><span data-stu-id="3a77a-109">Resolve the service location initially through the naming service.</span></span>
2. <span data-ttu-id="3a77a-110">Connettersi al servizio.</span><span class="sxs-lookup"><span data-stu-id="3a77a-110">Connect to the service.</span></span>
3. <span data-ttu-id="3a77a-111">Determinare la causa degli errori di connessione e risolvere nuovamente la posizione del servizio quando necessario.</span><span class="sxs-lookup"><span data-stu-id="3a77a-111">Determine the cause of connection failures, and resolve the service location again when necessary.</span></span>

<span data-ttu-id="3a77a-112">Questo processo implica in genere il wrapping delle librerie di comunicazione lato client in un ciclo di nuovi tentativi che implementa la risoluzione del servizio e i criteri di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="3a77a-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements the service resolution and retry policies.</span></span>
<span data-ttu-id="3a77a-113">Per altre informazioni, vedere [Connettersi e comunicare con i servizi](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="3a77a-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-the-reverse-proxy"></a><span data-ttu-id="3a77a-114">Comunicare tramite il proxy inverso</span><span class="sxs-lookup"><span data-stu-id="3a77a-114">Communicating by using the reverse proxy</span></span>
<span data-ttu-id="3a77a-115">Il proxy inverso in Service Fabric viene eseguito in tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="3a77a-115">The reverse proxy in Service Fabric runs on all the nodes in the cluster.</span></span> <span data-ttu-id="3a77a-116">Esegue l'intero processo di risoluzione del servizio per conto di un client e quindi inoltra la richiesta del client.</span><span class="sxs-lookup"><span data-stu-id="3a77a-116">It performs the entire service resolution process on a client's behalf and then forwards the client request.</span></span> <span data-ttu-id="3a77a-117">I client in esecuzione nel cluster possono quindi usare le librerie di comunicazione HTTP lato client per comunicare con il servizio di destinazione tramite il proxy inverso in esecuzione in locale nello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="3a77a-117">So, clients that run on the cluster can use any client-side HTTP communication libraries to talk to the target service by using the reverse proxy that runs locally on the same node.</span></span>

![Comunicazione interna][1]

## <a name="reaching-microservices-from-outside-the-cluster"></a><span data-ttu-id="3a77a-119">Raggiungere i microservizi dall'esterno del cluster</span><span class="sxs-lookup"><span data-stu-id="3a77a-119">Reaching microservices from outside the cluster</span></span>
<span data-ttu-id="3a77a-120">Il modello di comunicazione esterna predefinito per i microservizi è un modello di consenso esplicito nei casi in cui non è possibile accedere direttamente a ogni servizio dai client esterni.</span><span class="sxs-lookup"><span data-stu-id="3a77a-120">The default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="3a77a-121">Il servizio [Azure Load Balancer](../load-balancer/load-balancer-overview.md) è un limite di rete tra microservizi e client esterni che esegue la conversione degli indirizzi di rete e inoltra le richieste esterne agli endpoint IP:port interni.</span><span class="sxs-lookup"><span data-stu-id="3a77a-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests to internal IP:port endpoints.</span></span> <span data-ttu-id="3a77a-122">Per rendere un endpoint del microservizio direttamente accessibile ai client esterni, è prima di tutto necessario configurare il servizio Load Balancer per l'inoltro del traffico a ogni porta usata dal servizio nel cluster.</span><span class="sxs-lookup"><span data-stu-id="3a77a-122">To make a microservice's endpoint directly accessible to external clients, you must first configure Load Balancer to forward traffic to each port that the service uses in the cluster.</span></span> <span data-ttu-id="3a77a-123">La maggior parte dei microservizi, in particolare i microservizi con stato, non è inoltre presente in tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="3a77a-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of the cluster.</span></span> <span data-ttu-id="3a77a-124">I microservizi possono spostarsi tra i nodi in caso di failover.</span><span class="sxs-lookup"><span data-stu-id="3a77a-124">The microservices can move between nodes on failover.</span></span> <span data-ttu-id="3a77a-125">In questi casi, il servizio Load Balancer non può determinare in modo efficace la posizione del nodo di destinazione delle repliche a cui deve inoltrare il traffico.</span><span class="sxs-lookup"><span data-stu-id="3a77a-125">In such cases, Load Balancer cannot effectively determine the location of the target node of the replicas to which it should forward traffic.</span></span>

### <a name="reaching-microservices-via-the-reverse-proxy-from-outside-the-cluster"></a><span data-ttu-id="3a77a-126">Raggiungere i microservizi tramite il proxy inverso dall'esterno del cluster</span><span class="sxs-lookup"><span data-stu-id="3a77a-126">Reaching microservices via the reverse proxy from outside the cluster</span></span>
<span data-ttu-id="3a77a-127">Invece di configurare la porta di un singolo servizio in Load Balancer, è possibile configurare solo la porta del proxy inverso in Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="3a77a-127">Instead of configuring the port of an individual service in Load Balancer, you can configure just the port of the reverse proxy in Load Balancer.</span></span> <span data-ttu-id="3a77a-128">Questa configurazione consente ai client all'esterno del cluster di raggiungere i servizi all'interno tramite il proxy inverso senza configurazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="3a77a-128">This configuration lets clients outside the cluster reach services inside the cluster by using the reverse proxy without additional configuration.</span></span>

![Comunicazione esterna][0]

> [!WARNING]
> <span data-ttu-id="3a77a-130">Quando si configura la porta del proxy inverso nel servizio Load Balancer, tutti i microservizi nel cluster che espone un endpoint HTTP sono indirizzabili dall'esterno del cluster.</span><span class="sxs-lookup"><span data-stu-id="3a77a-130">When you configure the reverse proxy's port in Load Balancer, all microservices in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-the-reverse-proxy"></a><span data-ttu-id="3a77a-131">Formato URI di indirizzamento dei servizi tramite il proxy inverso</span><span class="sxs-lookup"><span data-stu-id="3a77a-131">URI format for addressing services by using the reverse proxy</span></span>
<span data-ttu-id="3a77a-132">Il proxy inverso usa un formato URI (Uniform Resource Identifier) specifico per identificare la partizione del servizio a cui deve essere inoltrata la richiesta in ingresso:</span><span class="sxs-lookup"><span data-stu-id="3a77a-132">The reverse proxy uses a specific uniform resource identifier (URI) format to identify the service partition to which the incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="3a77a-133">**http(s):** il proxy inverso può essere configurato per accettare il traffico HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3a77a-133">**http(s):** The reverse proxy can be configured to accept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="3a77a-134">Per l'inoltro di HTTPS, fare riferimento a [Connect to a secure service with the reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) (Connettersi a un servizio protetto con il proxy inverso) dopo aver configurato il proxy inverso per l'ascolto su HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3a77a-134">For HTTPS forwarding, refer to [Connect to a secure service with the reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup to listen on HTTPS.</span></span>
* <span data-ttu-id="3a77a-135">**Nome di dominio completo del cluster | IP interno:** Per i client esterni è possibile configurare il proxy inverso in modo che sia raggiungibile tramite il dominio del cluster, ad esempio mycluster.eastus.cloudapp.azure.com. Per impostazione predefinita, il proxy inverso è in esecuzione in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="3a77a-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure the reverse proxy so that it is reachable through the cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, the reverse proxy runs on every node.</span></span> <span data-ttu-id="3a77a-136">Per il traffico interno, il proxy inverso può essere raggiunto sugli host locali o all'indirizzo IP di qualsiasi nodo interno, ad esempio, 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="3a77a-136">For internal traffic, the reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="3a77a-137">**Porta:** la porta che è stata specificata per il proxy inverso, ad esempio 19081.</span><span class="sxs-lookup"><span data-stu-id="3a77a-137">**Port:** This is the port, such as 19081, that has been specified for the reverse proxy.</span></span>
* <span data-ttu-id="3a77a-138">**ServiceInstanceName:** nome completo dell'istanza del servizio distribuito che si sta provando a raggiungere senza lo schema "fabric:/".</span><span class="sxs-lookup"><span data-stu-id="3a77a-138">**ServiceInstanceName:** This is the fully-qualified name of the deployed service instance that you are trying to reach without the "fabric:/" scheme.</span></span> <span data-ttu-id="3a77a-139">Ad esempio, per raggiungere il servizio *fabric:/myapp/myservice/*, si usa *myapp/myservice*.</span><span class="sxs-lookup"><span data-stu-id="3a77a-139">For example, to reach the *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="3a77a-140">Il nome dell'istanza del servizio fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="3a77a-140">The service instance name is case-sensitive.</span></span> <span data-ttu-id="3a77a-141">L'uso di maiuscole/minuscole per il nome dell'istanza del servizio nell'URL fa sì che le richieste abbiano esito negativo con errore 404 (Non trovato).</span><span class="sxs-lookup"><span data-stu-id="3a77a-141">Using a different casing for the service instance name in the URL causes the requests to fail with 404 (Not Found).</span></span>
* <span data-ttu-id="3a77a-142">**Suffix path:** percorso effettivo dell'URL, ad esempio *myapi/values/add/3*, per il servizio a cui ci si vuole connettere.</span><span class="sxs-lookup"><span data-stu-id="3a77a-142">**Suffix path:** This is the actual URL path, such as *myapi/values/add/3*, for the service that you want to connect to.</span></span>
* <span data-ttu-id="3a77a-143">**PartitionKey:** per un servizio partizionato, questa è la chiave di partizione calcolata della partizione che si vuole raggiungere.</span><span class="sxs-lookup"><span data-stu-id="3a77a-143">**PartitionKey:** For a partitioned service, this is the computed partition key of the partition that you want to reach.</span></span> <span data-ttu-id="3a77a-144">Si noti che questo *non* è il GUID dell'ID di partizione.</span><span class="sxs-lookup"><span data-stu-id="3a77a-144">Note that this is *not* the partition ID GUID.</span></span> <span data-ttu-id="3a77a-145">Questo parametro non è obbligatorio per i servizi che usano lo schema di partizione singleton.</span><span class="sxs-lookup"><span data-stu-id="3a77a-145">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="3a77a-146">**PartitionKind:** lo schema di partizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="3a77a-146">**PartitionKind:** This is the service partition scheme.</span></span> <span data-ttu-id="3a77a-147">Può essere "Int64Range" o "Named".</span><span class="sxs-lookup"><span data-stu-id="3a77a-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="3a77a-148">Questo parametro non è obbligatorio per i servizi che usano lo schema di partizione singleton.</span><span class="sxs-lookup"><span data-stu-id="3a77a-148">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="3a77a-149">**ListenerName** Gli endpoint del servizio hanno la forma {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span><span class="sxs-lookup"><span data-stu-id="3a77a-149">**ListenerName** The endpoints from the service are of the form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="3a77a-150">Quando il servizio espone più endpoint, questa forma indica gli endpoint a cui deve essere inoltrata la richiesta del client.</span><span class="sxs-lookup"><span data-stu-id="3a77a-150">When the service exposes multiple endpoints, this identifies the endpoint that the client request should be forwarded to.</span></span> <span data-ttu-id="3a77a-151">Può essere omessa se il servizio ha un solo listener.</span><span class="sxs-lookup"><span data-stu-id="3a77a-151">This can be omitted if the service has only one listener.</span></span>
* <span data-ttu-id="3a77a-152">**TargetReplicaSelector** Specifica la modalità di selezione della replica o dell'istanza di destinazione.</span><span class="sxs-lookup"><span data-stu-id="3a77a-152">**TargetReplicaSelector** This specifies how the target replica or instance should be selected.</span></span>
  * <span data-ttu-id="3a77a-153">Quando il servizio di destinazione è con stato, TargetReplicaSelector può essere uno dei valori seguenti: "PrimaryReplica", "RandomSecondaryReplica" o "RandomReplica".</span><span class="sxs-lookup"><span data-stu-id="3a77a-153">When the target service is stateful, the TargetReplicaSelector can be one of the following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="3a77a-154">Il valore predefinito quando non viene specificato questo parametro è "PrimaryReplica".</span><span class="sxs-lookup"><span data-stu-id="3a77a-154">When this parameter is not specified, the default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="3a77a-155">Quando il servizio di destinazione è senza stato, il proxy inverso sceglie un'istanza casuale della partizione del servizio a cui inoltrare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="3a77a-155">When the target service is stateless, reverse proxy picks a random instance of the service partition to forward the request to.</span></span>
* <span data-ttu-id="3a77a-156">**Timeout:** specifica il timeout per la richiesta HTTP creata dal proxy inverso al servizio per conto della richiesta del client.</span><span class="sxs-lookup"><span data-stu-id="3a77a-156">**Timeout:**  This specifies the timeout for the HTTP request created by the reverse proxy to the service on behalf of the client request.</span></span> <span data-ttu-id="3a77a-157">Il valore predefinito è 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="3a77a-157">The default value is 60 seconds.</span></span> <span data-ttu-id="3a77a-158">Questo è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="3a77a-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="3a77a-159">Esempio di utilizzo</span><span class="sxs-lookup"><span data-stu-id="3a77a-159">Example usage</span></span>
<span data-ttu-id="3a77a-160">Si prenda come esempio il servizio *fabric:/MyApp/MyService* che apre un listener HTTP nell'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="3a77a-160">As an example, let's take the *fabric:/MyApp/MyService* service that opens an HTTP listener on the following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="3a77a-161">Di seguito sono indicate le risorse per il servizio:</span><span class="sxs-lookup"><span data-stu-id="3a77a-161">Following are the resources for the service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="3a77a-162">Se il servizio usa lo schema di partizionamento singleton, i parametri della stringa di query *PartitionKey* e *PartitionKind* non sono obbligatori e il servizio può essere raggiunto tramite gateway nei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a77a-162">If the service uses the singleton partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters are not required, and the service can be reached by using the gateway as:</span></span>

* <span data-ttu-id="3a77a-163">Esternamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="3a77a-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="3a77a-164">Internamente: `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="3a77a-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="3a77a-165">Se il servizio usa lo schema di partizionamento Uniform Int64, è necessario usare i parametri della stringa di query *PartitionKey* e *PartitionKind* per raggiungere una partizione del servizio:</span><span class="sxs-lookup"><span data-stu-id="3a77a-165">If the service uses the Uniform Int64 partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters must be used to reach a partition of the service:</span></span>

* <span data-ttu-id="3a77a-166">Esternamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="3a77a-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="3a77a-167">Internamente: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="3a77a-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="3a77a-168">Per raggiungere le risorse esposte dal servizio, è sufficiente inserire il percorso della risorsa dopo il nome del servizio nell'URL:</span><span class="sxs-lookup"><span data-stu-id="3a77a-168">To reach the resources that the service exposes, simply place the resource path after the service name in the URL:</span></span>

* <span data-ttu-id="3a77a-169">Esternamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="3a77a-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="3a77a-170">Internamente: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="3a77a-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="3a77a-171">Il gateway inoltrerà quindi queste richieste all'URL del servizio:</span><span class="sxs-lookup"><span data-stu-id="3a77a-171">The gateway will then forward these requests to the service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="3a77a-172">Gestione speciale per servizi di condivisione porta</span><span class="sxs-lookup"><span data-stu-id="3a77a-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="3a77a-173">Il gateway applicazione di Azure prova a risolvere di nuovo un indirizzo del servizio e ripetere la richiesta quando non è possibile raggiungere un servizio.</span><span class="sxs-lookup"><span data-stu-id="3a77a-173">Azure Application Gateway attempts to resolve a service address again and retry the request when a service cannot be reached.</span></span> <span data-ttu-id="3a77a-174">Questo è uno dei principali vantaggi del gateway applicazione, dal momento che il codice client non necessita di implementare la propria risoluzione del servizio e il proprio ciclo di risoluzione.</span><span class="sxs-lookup"><span data-stu-id="3a77a-174">This is a major benefit of Application Gateway because client code does not need to implement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="3a77a-175">Quando un servizio non può essere raggiunto, la replica o l'istanza del servizio si è in genere spostata in un nodo diverso come parte del ciclo di vita normale.</span><span class="sxs-lookup"><span data-stu-id="3a77a-175">Generally, when a service cannot be reached, the service instance or replica has moved to a different node as part of its normal lifecycle.</span></span> <span data-ttu-id="3a77a-176">In questo caso, il gateway applicazione potrebbe ricevere un errore di connessione di rete che indica che un endpoint non è più aperto sull'indirizzo risolto in origine.</span><span class="sxs-lookup"><span data-stu-id="3a77a-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on the originally resolved address.</span></span>

<span data-ttu-id="3a77a-177">Tuttavia, le repliche o le istanze del servizio possono condividere un processo host e una porta quando ospitate da un server Web basato su http.sys, tra cui:</span><span class="sxs-lookup"><span data-stu-id="3a77a-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="3a77a-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="3a77a-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="3a77a-179">WebListener ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="3a77a-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="3a77a-180">Katana</span><span class="sxs-lookup"><span data-stu-id="3a77a-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="3a77a-181">In questa circostanza è probabile che il server Web sia disponibile nel processo host e che risponda alle richieste, ma la replica o l'istanza del servizio risolto non è più disponibile nell'host.</span><span class="sxs-lookup"><span data-stu-id="3a77a-181">In this situation, it is likely that the web server is available in the host process and responding to requests, but the resolved service instance or replica is no longer available on the host.</span></span> <span data-ttu-id="3a77a-182">In questo caso il gateway riceve una risposta HTTP 404 dal server Web.</span><span class="sxs-lookup"><span data-stu-id="3a77a-182">In this case, the gateway will receive an HTTP 404 response from the web server.</span></span> <span data-ttu-id="3a77a-183">Un errore HTTP 404 presenta quindi due significati distinti:</span><span class="sxs-lookup"><span data-stu-id="3a77a-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="3a77a-184">Caso n. 1: l'indirizzo del servizio è corretto, ma la risorsa richiesta dall'utente non esiste.</span><span class="sxs-lookup"><span data-stu-id="3a77a-184">Case #1: The service address is correct, but the resource that the user requested does not exist.</span></span>
- <span data-ttu-id="3a77a-185">Caso n. 2: l'indirizzo del servizio non è corretto ed è possibile che la risorsa richiesta dall'utente esista su un nodo diverso.</span><span class="sxs-lookup"><span data-stu-id="3a77a-185">Case #2: The service address is incorrect, and the resource that the user requested might exist on a different node.</span></span>

<span data-ttu-id="3a77a-186">Nel primo caso si tratta di una normale situazione HTTP 404, che viene considerata come un errore dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3a77a-186">The first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="3a77a-187">Nel secondo caso, tuttavia, l'utente ha richiesto una risorsa che non esiste.</span><span class="sxs-lookup"><span data-stu-id="3a77a-187">However, in the second case, the user has requested a resource that does exist.</span></span> <span data-ttu-id="3a77a-188">Il gateway applicazione non è riuscito a individuarla perché il servizio stesso è stato spostato.</span><span class="sxs-lookup"><span data-stu-id="3a77a-188">Application Gateway was unable to locate it because the service itself has moved.</span></span> <span data-ttu-id="3a77a-189">Il gateway applicazione deve risolvere di nuovo l'indirizzo e ripetere la richiesta.</span><span class="sxs-lookup"><span data-stu-id="3a77a-189">Application Gateway needs to resolve the address again and retry the request.</span></span>

<span data-ttu-id="3a77a-190">Il gateway applicazione necessita quindi di un modo per distinguere tra questi due casi.</span><span class="sxs-lookup"><span data-stu-id="3a77a-190">Application Gateway thus needs a way to distinguish between these two cases.</span></span> <span data-ttu-id="3a77a-191">Per eseguire questa distinzione, è necessario un suggerimento dal server.</span><span class="sxs-lookup"><span data-stu-id="3a77a-191">To make that distinction, a hint from the server is required.</span></span>

* <span data-ttu-id="3a77a-192">Per impostazione predefinita, il gateway applicazione presuppone la sussistenza del caso n. 2 e prova a risolvere di nuovo l'indirizzo e inviare nuovamente la richiesta.</span><span class="sxs-lookup"><span data-stu-id="3a77a-192">By default, Application Gateway assumes case #2 and attempts to resolve and issue the request again.</span></span>
* <span data-ttu-id="3a77a-193">Per indicare il caso n. 1 al gateway applicazione, il servizio deve restituire l'intestazione della risposta HTTP seguente:</span><span class="sxs-lookup"><span data-stu-id="3a77a-193">To indicate case #1 to Application Gateway, the service should return the following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="3a77a-194">L'intestazione della risposta HTTP indica una situazione HTTP 404 normale, in cui la risorsa richiesta non esiste e il gateway applicazione non prova a risolvere di nuovo l'indirizzo del servizio.</span><span class="sxs-lookup"><span data-stu-id="3a77a-194">This HTTP response header indicates a normal HTTP 404 situation in which the requested resource does not exist, and Application Gateway will not attempt to resolve the service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="3a77a-195">Installazione e configurazione</span><span class="sxs-lookup"><span data-stu-id="3a77a-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="3a77a-196">Abilitare il proxy inverso tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3a77a-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="3a77a-197">Il portale di Azure fornisce un'opzione per abilitare il proxy inverso durante la creazione di un nuovo cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3a77a-197">Azure portal provides an option to enable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="3a77a-198">In **Crea cluster di Service Fabric**, Passaggio 2: Configurazione cluster, Configurazione del tipo di nodo, selezionare la casella di controllo "Abilita proxy inverso".</span><span class="sxs-lookup"><span data-stu-id="3a77a-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select the checkbox to "Enable reverse proxy".</span></span>
<span data-ttu-id="3a77a-199">Per la configurazione di un proxy inverso sicuro, è possibile specificare un certificato SSL nel Passaggio 3: Sicurezza, Configurare le impostazioni di sicurezza del cluster, selezionare la casella di controllo "Includi un certificato SSL per il proxy inverso" e immettere i dettagli del certificato.</span><span class="sxs-lookup"><span data-stu-id="3a77a-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select the checkbox to "Include a SSL certificate for reverse proxy" and enter the certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="3a77a-200">Abilitare il proxy inverso tramite modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3a77a-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="3a77a-201">È possibile usare il [modello di Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) per abilitare il proxy inverso in Service Fabric per il cluster.</span><span class="sxs-lookup"><span data-stu-id="3a77a-201">You can use the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) to enable the reverse proxy in Service Fabric for the cluster.</span></span>

<span data-ttu-id="3a77a-202">Per esempi del modello di Azure Resource Manager per la configurazione del proxy inverso sicuro con un certificato e la gestione del rollover dei certificati, vedere [Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) (Configurare il proxy inverso HTTPS in un cluster sicuro).</span><span class="sxs-lookup"><span data-stu-id="3a77a-202">Refer to [Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples to configure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="3a77a-203">Ottenere prima di tutto il modello per il cluster da distribuire.</span><span class="sxs-lookup"><span data-stu-id="3a77a-203">First, you get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="3a77a-204">È possibile usare i modelli di esempio o creare un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3a77a-204">You can either use the sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="3a77a-205">È quindi possibile abilitare il proxy inverso seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3a77a-205">Then, you can enable the reverse proxy by using the following steps:</span></span>

1. <span data-ttu-id="3a77a-206">Definire una porta per il proxy inverso nella [sezione dei parametri](../azure-resource-manager/resource-group-authoring-templates.md) del modello.</span><span class="sxs-lookup"><span data-stu-id="3a77a-206">Define a port for the reverse proxy in the [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of the template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="3a77a-207">Specificare la porta per ogni oggetto nodetype nella sezione **Cluster** [Tipo di risorsa](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3a77a-207">Specify the port for each of the nodetype objects in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="3a77a-208">La porta è identificata dal nome del parametro reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="3a77a-208">The port is identified by the parameter name, reverseProxyEndpointPort.</span></span>

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
3. <span data-ttu-id="3a77a-209">Per fare riferimento al proxy inverso dall'esterno del cluster di Azure, configurare le regole di Azure Load Balancer per la porta specificata nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="3a77a-209">To address the reverse proxy from outside the Azure cluster, set up the Azure Load Balancer rules for the port that you specified in step 1.</span></span>

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
4. <span data-ttu-id="3a77a-210">Per configurare i certificati SSL sulla porta per il proxy inverso, aggiungere il certificato alla proprietà ***reverseProxyCertificate*** nella sezione **Cluster** [Tipo di risorsa](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3a77a-210">To configure SSL certificates on the port for the reverse proxy, add the certificate to the ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

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

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-the-cluster-certificate"></a><span data-ttu-id="3a77a-211">Supporto di un certificato di proxy inverso diverso dal certificato di cluster</span><span class="sxs-lookup"><span data-stu-id="3a77a-211">Supporting a reverse proxy certificate that's different from the cluster certificate</span></span>
 <span data-ttu-id="3a77a-212">Se il certificato di proxy inverso è diverso dal certificato che protegge il cluster, il certificato specificato in precedenza deve essere installato nella macchina virtuale e aggiunto all'elenco di controllo di accesso, in modo che Service Fabric possa accedervi.</span><span class="sxs-lookup"><span data-stu-id="3a77a-212">If the reverse proxy certificate is different from the certificate that secures the cluster, then the previously specified certificate should be installed on the virtual machine and added to the access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="3a77a-213">Questa operazione può essere eseguita tramite la sezione di **virtualMachineScaleSets** [Tipo di risorsa](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3a77a-213">This can be done in the **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="3a77a-214">Per l'installazione, aggiungere il certificato a osProfile.</span><span class="sxs-lookup"><span data-stu-id="3a77a-214">For installation, add that certificate to the osProfile.</span></span> <span data-ttu-id="3a77a-215">La sezione del modello relativa all'estensione può aggiornare il certificato nell'elenco di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="3a77a-215">The extension section of the template can update the certificate in the ACL.</span></span>

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
> <span data-ttu-id="3a77a-216">Quando si usano certificati diversi dal certificato del cluster per abilitare il proxy inverso in un cluster esistente, installare il certificato di proxy inverso e aggiornare l'elenco di controllo di accesso sul cluster prima di abilitare il proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="3a77a-216">When you use certificates that are different from the cluster certificate to enable the reverse proxy on an existing cluster, install the reverse proxy certificate and update the ACL on the cluster before you enable the reverse proxy.</span></span> <span data-ttu-id="3a77a-217">Completare la distribuzione del [modello di Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) usando le impostazioni indicate in precedenza prima di avviare una distribuzione per abilitare il proxy inverso nei passaggi 1-4.</span><span class="sxs-lookup"><span data-stu-id="3a77a-217">Complete the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using the settings mentioned previously before you start a deployment to enable the reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a77a-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a77a-218">Next steps</span></span>
* <span data-ttu-id="3a77a-219">Vedere un esempio di comunicazione HTTP tra i servizi in un [progetto di esempio in GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="3a77a-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* <span data-ttu-id="3a77a-220">[Forwarding to secure HTTP service with the reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) (Inoltro per la protezione del servizio HTTP con il proxy inverso)</span><span class="sxs-lookup"><span data-stu-id="3a77a-220">[Forwarding to secure HTTP service with the reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md)</span></span>
* [<span data-ttu-id="3a77a-221">Chiamate di procedura remota con i Reliable Services remoti</span><span class="sxs-lookup"><span data-stu-id="3a77a-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="3a77a-222">Web API che usa OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="3a77a-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="3a77a-223">Comunicazione di WCF tramite Reliable Services</span><span class="sxs-lookup"><span data-stu-id="3a77a-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="3a77a-224">Per altre opzioni di configurazione del proxy inverso, vedere la sezione ApplicationGateway/Http in [Personalizzare le impostazioni del cluster Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="3a77a-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
