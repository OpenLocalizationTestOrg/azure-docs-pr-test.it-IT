---
title: Gestire un cluster DC/OS di Azure con l'API REST Marathon | Microsoft Docs
description: Distribuire contenitori in un cluster DC/OS del servizio contenitore di Azure usando l'API REST di Marathon.
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Contenitori, Micro-servizi, Mesos, Azure
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 65f8e0170fa7b89162e811a1d5dd58775fd20d7b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-container-management-through-the-marathon-rest-api"></a><span data-ttu-id="d8318-104">Gestione dei contenitori DC/OS tramite l'API REST Marathon</span><span class="sxs-lookup"><span data-stu-id="d8318-104">DC/OS container management through the Marathon REST API</span></span>
<span data-ttu-id="d8318-105">DC/OS offre un ambiente di distribuzione e ridimensionamento dei carichi di lavoro cluster con l'astrazione dell'hardware sottostante.</span><span class="sxs-lookup"><span data-stu-id="d8318-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="d8318-106">In DC/OS è disponibile anche un framework che gestisce la pianificazione e l'esecuzione dei carichi di lavoro di calcolo.</span><span class="sxs-lookup"><span data-stu-id="d8318-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="d8318-107">Sono disponibili framework per molti dei carichi di lavoro più comuni. Questo documento illustra come iniziare a creare e ridimensionare le distribuzioni di contenitori usando l'API REST di Marathon.</span><span class="sxs-lookup"><span data-stu-id="d8318-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using the Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d8318-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d8318-108">Prerequisites</span></span>

<span data-ttu-id="d8318-109">Prima di eseguire questi esempi, è necessario avere un cluster DC/OS configurato nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8318-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="d8318-110">È necessaria anche la connettività remota a questo cluster.</span><span class="sxs-lookup"><span data-stu-id="d8318-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="d8318-111">Per altre informazioni su questi elementi, vedere gli articoli indicati di seguito:</span><span class="sxs-lookup"><span data-stu-id="d8318-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="d8318-112">Distribuire un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="d8318-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="d8318-113">Connettersi a un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="d8318-113">Connecting to an Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-the-dcos-apis"></a><span data-ttu-id="d8318-114">Accedere alle API di DC/OS</span><span class="sxs-lookup"><span data-stu-id="d8318-114">Access the DC/OS APIs</span></span>
<span data-ttu-id="d8318-115">Dopo essersi connessi al cluster del servizio contenitore di Azure, è possibile accedere a DC/OS e alle API REST correlate tramite http://localhost:local-port.</span><span class="sxs-lookup"><span data-stu-id="d8318-115">After you are connected to the Azure Container Service cluster, you can access the DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="d8318-116">Gli esempi riportati in questo documento presuppongono il tunneling sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="d8318-116">The examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="d8318-117">Ad esempio, gli endpoint Marathon sono raggiungibili usando gli URI che iniziano con `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="d8318-117">For example, the Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="d8318-118">Per altre informazioni sulle varie API, vedere la documentazione di Mesosphere per l'[API Marathon](https://mesosphere.github.io/marathon/docs/rest-api.html) e l'[API Chronos](https://mesos.github.io/chronos/docs/api.html), nonché la documentazione di Apache per l'[API dell'utilità di pianificazione Mesos](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="d8318-118">For more information on the various APIs, see the Mesosphere documentation for the [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for the [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="d8318-119">Raccogliere informazioni da DC/OS e Marathon</span><span class="sxs-lookup"><span data-stu-id="d8318-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="d8318-120">Prima di distribuire contenitori nel cluster DC/OS, è necessario raccogliere informazioni relative a tale cluster, ad esempio il nome e lo stato degli agenti di DC/OS.</span><span class="sxs-lookup"><span data-stu-id="d8318-120">Before you deploy containers to the DC/OS cluster, gather some information about the DC/OS cluster, such as the names and status of the DC/OS agents.</span></span> <span data-ttu-id="d8318-121">A tale scopo, eseguire una query sull'endpoint `master/slaves` dell'API REST di DC/OS.</span><span class="sxs-lookup"><span data-stu-id="d8318-121">To do so, query the `master/slaves` endpoint of the DC/OS REST API.</span></span> <span data-ttu-id="d8318-122">Se la query riesce, verrà restituito un elenco di agenti di DC/OS e diverse proprietà per ognuno.</span><span class="sxs-lookup"><span data-stu-id="d8318-122">If everything goes well, the query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="d8318-123">A questo punto, usare l'endpoint `/apps` di DC/OS per cercare le distribuzioni correnti dell'applicazione nel cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="d8318-123">Now, use the Marathon `/apps` endpoint to check for current application deployments to the DC/OS cluster.</span></span> <span data-ttu-id="d8318-124">Se si tratta di un nuovo cluster, viene visualizzata una matrice vuota di app.</span><span class="sxs-lookup"><span data-stu-id="d8318-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="d8318-125">Distribuire un contenitore Docker formattato</span><span class="sxs-lookup"><span data-stu-id="d8318-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="d8318-126">I contenitori Docker formattati vengono distribuiti tramite l'API REST di Marathon usando un file JSON che descrive la distribuzione prevista.</span><span class="sxs-lookup"><span data-stu-id="d8318-126">You deploy Docker-formatted containers through the Marathon REST API by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="d8318-127">L'esempio seguente distribuisce un contenitore Nginx a un agente privato del cluster.</span><span class="sxs-lookup"><span data-stu-id="d8318-127">The following sample deploys an Nginx container to a private agent in the cluster.</span></span> 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="d8318-128">Per distribuire un contenitore Docker formattato, archiviare il file JSON in un percorso accessibile.</span><span class="sxs-lookup"><span data-stu-id="d8318-128">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="d8318-129">Successivamente, eseguire il comando riportato di seguito per distribuire il contenitore.</span><span class="sxs-lookup"><span data-stu-id="d8318-129">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="d8318-130">Specificare il nome del file JSON (`marathon.json` in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="d8318-130">Specify the name of the JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="d8318-131">L'output è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d8318-131">The output is similar to the following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="d8318-132">Se ora si esegue una query per cercare applicazioni in Marathon, la nuova applicazione viene visualizzata nell'output.</span><span class="sxs-lookup"><span data-stu-id="d8318-132">Now, if you query Marathon for applications, this new application appears in the output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-the-container"></a><span data-ttu-id="d8318-133">Raggiungere il contenitore</span><span class="sxs-lookup"><span data-stu-id="d8318-133">Reach the container</span></span>

<span data-ttu-id="d8318-134">È possibile verificare che il Nginx sia in esecuzione in un contenitore su uno degli agenti privati del cluster.</span><span class="sxs-lookup"><span data-stu-id="d8318-134">You can verify that the Nginx is running in a container on one of the private agents in the cluster.</span></span> <span data-ttu-id="d8318-135">Per trovare l'host e la porta in cui è in esecuzione il contenitore, eseguire una query a Marathon per le attività in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="d8318-135">To find the host and port where the container is running, query Marathon for the running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="d8318-136">Trovare il valore di `host` nell'output (un indirizzo IP simile a `10.32.0.x`) e il valore di `ports`.</span><span class="sxs-lookup"><span data-stu-id="d8318-136">Find the value of `host` in the output (an IP address similar to `10.32.0.x`), and the value of `ports`.</span></span>


<span data-ttu-id="d8318-137">Ora creare una connessione terminal SSH (non una connessione con tunnel) al FQDN di gestione del cluster.</span><span class="sxs-lookup"><span data-stu-id="d8318-137">Now make an SSH terminal connection (not a tunneled connection) to the management FQDN of the cluster.</span></span> <span data-ttu-id="d8318-138">Quindi eseguire la richiesta seguente, sostituendo i valori corretti di `host` e `ports`:</span><span class="sxs-lookup"><span data-stu-id="d8318-138">Once connected, make the following request, substituting the correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="d8318-139">L'output del server di Nginx è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d8318-139">The Nginx server output is similar to the following:</span></span>

![Nginx dal contenitore](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="d8318-141">Ridimensionare i contenitori</span><span class="sxs-lookup"><span data-stu-id="d8318-141">Scale your containers</span></span>
<span data-ttu-id="d8318-142">L'API Marathon può essere usata per aumentare o ridurre il numero di istanze delle distribuzioni di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d8318-142">You can use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="d8318-143">Nell'esempio precedente è stata distribuita un'istanza di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8318-143">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="d8318-144">Il numero di istanze dell'applicazione viene ora aumentato a tre.</span><span class="sxs-lookup"><span data-stu-id="d8318-144">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="d8318-145">A tale scopo, creare un file JSON usando il testo JSON seguente e archiviarlo in un percorso accessibile.</span><span class="sxs-lookup"><span data-stu-id="d8318-145">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="d8318-146">Dalla connessione con tunnel, eseguire il comando seguente per aumentare il numero di istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8318-146">From your tunneled connection, run the following command to scale out the application.</span></span>

> [!NOTE]
> <span data-ttu-id="d8318-147">L'URI è http://localhost/marathon/v2/apps/ seguito dall'ID dell'applicazione da ridimensionare.</span><span class="sxs-lookup"><span data-stu-id="d8318-147">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="d8318-148">Se si usa l'esempio di nginx fornito qui, l'URI sarà http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="d8318-148">If you are using the Nginx sample that is provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="d8318-149">Infine, eseguire una query per le istanze dell'applicazione nell'endpoint Marathon.</span><span class="sxs-lookup"><span data-stu-id="d8318-149">Finally, query the Marathon endpoint for applications.</span></span> <span data-ttu-id="d8318-150">Ora sono presenti tre contenitori Nginx.</span><span class="sxs-lookup"><span data-stu-id="d8318-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="d8318-151">Comandi di PowerShell equivalenti</span><span class="sxs-lookup"><span data-stu-id="d8318-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="d8318-152">È possibile eseguire queste stesse azioni usando i comandi di PowerShell in un sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="d8318-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="d8318-153">Per raccogliere informazioni sul cluster DC/OS, ad esempio il nome e lo stato degli agenti, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d8318-153">To gather information about the DC/OS cluster, such as agent names and agent status, run the following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="d8318-154">I contenitori Docker formattati vengono distribuiti tramite Marathon usando un file JSON che descrive la distribuzione prevista.</span><span class="sxs-lookup"><span data-stu-id="d8318-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="d8318-155">L'esempio seguente mostra come distribuire il contenitore Nginx associando la porta 80 dell'agente di DC/OS alla porta 80 del contenitore.</span><span class="sxs-lookup"><span data-stu-id="d8318-155">The following sample deploys the Nginx container, binding port 80 of the DC/OS agent to port 80 of the container.</span></span>

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="d8318-156">Per distribuire un contenitore Docker formattato, archiviare il file JSON in un percorso accessibile.</span><span class="sxs-lookup"><span data-stu-id="d8318-156">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="d8318-157">Successivamente, eseguire il comando riportato di seguito per distribuire il contenitore.</span><span class="sxs-lookup"><span data-stu-id="d8318-157">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="d8318-158">Specificare il percorso del file JSON (`marathon.json` in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="d8318-158">Specify the path to the JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="d8318-159">L'API Marathon può anche essere usata per aumentare o ridurre il numero di istanze delle distribuzioni di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d8318-159">You can also use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="d8318-160">Nell'esempio precedente è stata distribuita un'istanza di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8318-160">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="d8318-161">Il numero di istanze dell'applicazione viene ora aumentato a tre.</span><span class="sxs-lookup"><span data-stu-id="d8318-161">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="d8318-162">A tale scopo, creare un file JSON usando il testo JSON seguente e archiviarlo in un percorso accessibile.</span><span class="sxs-lookup"><span data-stu-id="d8318-162">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="d8318-163">Eseguire questo comando per aumentare il numero di istanze dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="d8318-163">Run the following command to scale out the application:</span></span>

> [!NOTE]
> <span data-ttu-id="d8318-164">L'URI è http://localhost/marathon/v2/apps/ seguito dall'ID dell'applicazione da ridimensionare.</span><span class="sxs-lookup"><span data-stu-id="d8318-164">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="d8318-165">Se si usa l'esempio di nginx fornito qui, l'URI sarà http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="d8318-165">If you are using the Nginx sample provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="d8318-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8318-166">Next steps</span></span>
* [<span data-ttu-id="d8318-167">Altre informazioni sugli endpoint HTTP Mesos</span><span class="sxs-lookup"><span data-stu-id="d8318-167">Read more about the Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="d8318-168">Altre informazioni sull'API REST di Marathon</span><span class="sxs-lookup"><span data-stu-id="d8318-168">Read more about the Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

