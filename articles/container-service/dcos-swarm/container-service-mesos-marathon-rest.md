---
title: aaaManage Azure controller di dominio o sistema operativo del cluster con l'API REST maratona | Documenti Microsoft
description: Distribuire i cluster di Azure contenitore del servizio controller di dominio o del sistema operativo di contenitori tooan tramite l'API REST maratona hello.
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
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a><span data-ttu-id="23ee5-104">Gestione dei contenitori di controller di dominio o del sistema operativo tramite l'API REST maratona hello</span><span class="sxs-lookup"><span data-stu-id="23ee5-104">DC/OS container management through hello Marathon REST API</span></span>
<span data-ttu-id="23ee5-105">Controller di dominio/OS offre un ambiente per la distribuzione e scalabilità i carichi di lavoro cluster eliminando l'hardware sottostante hello.</span><span class="sxs-lookup"><span data-stu-id="23ee5-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="23ee5-106">In DC/OS è disponibile anche un framework che gestisce la pianificazione e l'esecuzione dei carichi di lavoro di calcolo.</span><span class="sxs-lookup"><span data-stu-id="23ee5-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="23ee5-107">Sebbene i Framework sono disponibili per molti carichi di lavoro comune, in questo documento consente di iniziare la creazione e scalabilità le distribuzioni di contenitori tramite l'API REST maratona hello.</span><span class="sxs-lookup"><span data-stu-id="23ee5-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using hello Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="23ee5-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="23ee5-108">Prerequisites</span></span>

<span data-ttu-id="23ee5-109">Prima di eseguire questi esempi, è necessario avere un cluster DC/OS configurato nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="23ee5-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="23ee5-110">È inoltre necessario cluster toothis di toohave connettività remota.</span><span class="sxs-lookup"><span data-stu-id="23ee5-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="23ee5-111">Per ulteriori informazioni su questi elementi, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="23ee5-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="23ee5-112">Distribuire un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="23ee5-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="23ee5-113">Connessione tooan cluster del servizio di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="23ee5-113">Connecting tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a><span data-ttu-id="23ee5-114">Hello accesso API di controller di dominio o del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="23ee5-114">Access hello DC/OS APIs</span></span>
<span data-ttu-id="23ee5-115">Dopo avere toohello connesso cluster del servizio di contenitore di Azure, è possibile accedere hello controller di dominio o del sistema operativo e le API REST correlate tramite http://localhost:local porta.</span><span class="sxs-lookup"><span data-stu-id="23ee5-115">After you are connected toohello Azure Container Service cluster, you can access hello DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="23ee5-116">Negli esempi di Hello in questo documento si presuppone che sono tunneling sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="23ee5-116">hello examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="23ee5-117">Ad esempio, gli endpoint maratona hello possono essere raggiunto all'URI a partire da `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="23ee5-117">For example, hello Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="23ee5-118">Per ulteriori informazioni su hello diverse API, vedere documentazione Mesosphere hello hello [API maratona](https://mesosphere.github.io/marathon/docs/rest-api.html) e [Chronos API](https://mesos.github.io/chronos/docs/api.html)e la documentazione di Apache per hello [API dell'utilità di pianificazione Mesos ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="23ee5-118">For more information on hello various APIs, see hello Mesosphere documentation for hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for hello [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="23ee5-119">Raccogliere informazioni da DC/OS e Marathon</span><span class="sxs-lookup"><span data-stu-id="23ee5-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="23ee5-120">Prima di distribuire cluster di controller di dominio/OS toohello contenitori, raccogliere informazioni sui cluster di controller di dominio/OS hello, ad esempio nomi di hello e lo stato degli agenti di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="23ee5-120">Before you deploy containers toohello DC/OS cluster, gather some information about hello DC/OS cluster, such as hello names and status of hello DC/OS agents.</span></span> <span data-ttu-id="23ee5-121">toodo in tal caso, eseguire una query hello `master/slaves` endpoint dell'API REST di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="23ee5-121">toodo so, query hello `master/slaves` endpoint of hello DC/OS REST API.</span></span> <span data-ttu-id="23ee5-122">Se tutto va bene, query hello restituisce un elenco di agenti di controller di dominio/OS e diverse proprietà per ogni.</span><span class="sxs-lookup"><span data-stu-id="23ee5-122">If everything goes well, hello query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="23ee5-123">A questo punto, usare hello maratona `/apps` toocheck endpoint per cluster di toohello controller di dominio o del sistema operativo per le distribuzioni dell'applicazione corrente.</span><span class="sxs-lookup"><span data-stu-id="23ee5-123">Now, use hello Marathon `/apps` endpoint toocheck for current application deployments toohello DC/OS cluster.</span></span> <span data-ttu-id="23ee5-124">Se si tratta di un nuovo cluster, viene visualizzata una matrice vuota di app.</span><span class="sxs-lookup"><span data-stu-id="23ee5-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="23ee5-125">Distribuire un contenitore Docker formattato</span><span class="sxs-lookup"><span data-stu-id="23ee5-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="23ee5-126">Distribuire contenitori Docker formattati tramite l'API REST maratona hello utilizzando un file JSON che descrive la distribuzione di hello previsto.</span><span class="sxs-lookup"><span data-stu-id="23ee5-126">You deploy Docker-formatted containers through hello Marathon REST API by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="23ee5-127">Hello esempio seguente consente di distribuire un Nginx contenitore tooa privata dell'agente nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23ee5-127">hello following sample deploys an Nginx container tooa private agent in hello cluster.</span></span> 

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

<span data-ttu-id="23ee5-128">toodeploy un contenitore Docker in formato, archiviare file JSON hello in un percorso accessibile.</span><span class="sxs-lookup"><span data-stu-id="23ee5-128">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="23ee5-129">Successivamente, toodeploy hello contenitore, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="23ee5-129">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="23ee5-130">Specificare il nome di hello del file JSON hello (`marathon.json` in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="23ee5-130">Specify hello name of hello JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="23ee5-131">output di Hello è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="23ee5-131">hello output is similar toohello following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="23ee5-132">A questo punto, se si esegue una query per le applicazioni maratona, questa nuova applicazione viene visualizzata nell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="23ee5-132">Now, if you query Marathon for applications, this new application appears in hello output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a><span data-ttu-id="23ee5-133">Raggiungere hello contenitore</span><span class="sxs-lookup"><span data-stu-id="23ee5-133">Reach hello container</span></span>

<span data-ttu-id="23ee5-134">È possibile verificare tale hello che nginx viene eseguita in un contenitore in uno degli agenti di privata hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23ee5-134">You can verify that hello Nginx is running in a container on one of hello private agents in hello cluster.</span></span> <span data-ttu-id="23ee5-135">host hello toofind e la porta in cui è in esecuzione il contenitore di hello, eseguire una query maratona per hello attività in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="23ee5-135">toofind hello host and port where hello container is running, query Marathon for hello running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="23ee5-136">Trovare il valore di hello `host` nell'output di hello (un indirizzo IP simile troppo`10.32.0.x`) e il valore di hello di `ports`.</span><span class="sxs-lookup"><span data-stu-id="23ee5-136">Find hello value of `host` in hello output (an IP address similar too`10.32.0.x`), and hello value of `ports`.</span></span>


<span data-ttu-id="23ee5-137">Creare una gestione SSH terminal connessione (non un tunnel) toohello FQDN del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="23ee5-137">Now make an SSH terminal connection (not a tunneled connection) toohello management FQDN of hello cluster.</span></span> <span data-ttu-id="23ee5-138">Una volta connessi, rendere hello richiesta seguente, sostituendo i valori corretti di hello di `host` e `ports`:</span><span class="sxs-lookup"><span data-stu-id="23ee5-138">Once connected, make hello following request, substituting hello correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="23ee5-139">Hello output server Nginx è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="23ee5-139">hello Nginx server output is similar toohello following:</span></span>

![Nginx dal contenitore](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="23ee5-141">Ridimensionare i contenitori</span><span class="sxs-lookup"><span data-stu-id="23ee5-141">Scale your containers</span></span>
<span data-ttu-id="23ee5-142">È possibile utilizzare hello maratona API tooscale out o la scala in distribuzioni di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="23ee5-142">You can use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="23ee5-143">Nell'esempio precedente hello, si è distribuito un'istanza di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="23ee5-143">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="23ee5-144">Possibile modificare le proporzioni toothree istanze di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="23ee5-144">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="23ee5-145">toodo in tal caso, creare un file JSON utilizzando hello dopo il testo JSON e archiviarlo in un percorso accessibile.</span><span class="sxs-lookup"><span data-stu-id="23ee5-145">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="23ee5-146">Eseguire la connessione di tunneling, hello successivo comando tooscale out applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="23ee5-146">From your tunneled connection, run hello following command tooscale out hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="23ee5-147">Hello URI è seguito dall'ID hello di hello applicazione tooscale http://localhost/marathon/v2/apps/.</span><span class="sxs-lookup"><span data-stu-id="23ee5-147">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="23ee5-148">Se si utilizza hello Nginx esempio fornito in questo caso, hello URI sarebbe http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="23ee5-148">If you are using hello Nginx sample that is provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="23ee5-149">Infine, eseguire una query endpoint maratona hello per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="23ee5-149">Finally, query hello Marathon endpoint for applications.</span></span> <span data-ttu-id="23ee5-150">Ora sono presenti tre contenitori Nginx.</span><span class="sxs-lookup"><span data-stu-id="23ee5-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="23ee5-151">Comandi di PowerShell equivalenti</span><span class="sxs-lookup"><span data-stu-id="23ee5-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="23ee5-152">È possibile eseguire queste stesse azioni usando i comandi di PowerShell in un sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="23ee5-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="23ee5-153">toogather informazioni sui cluster di controller di dominio/OS hello, ad esempio i nomi agente e lo stato dell'agente, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="23ee5-153">toogather information about hello DC/OS cluster, such as agent names and agent status, run hello following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="23ee5-154">Distribuire contenitori di Docker in formato tramite maratona utilizzando un file JSON che descrive la distribuzione di hello destinato.</span><span class="sxs-lookup"><span data-stu-id="23ee5-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="23ee5-155">Hello esempio seguente consente di distribuire contenitore Nginx hello, porta 80 dell'agente per controller di dominio/OS hello tooport 80 del contenitore hello di associazione.</span><span class="sxs-lookup"><span data-stu-id="23ee5-155">hello following sample deploys hello Nginx container, binding port 80 of hello DC/OS agent tooport 80 of hello container.</span></span>

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

<span data-ttu-id="23ee5-156">toodeploy un contenitore Docker in formato, archiviare file JSON hello in un percorso accessibile.</span><span class="sxs-lookup"><span data-stu-id="23ee5-156">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="23ee5-157">Successivamente, toodeploy hello contenitore, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="23ee5-157">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="23ee5-158">Specificare i file JSON di hello percorso toohello (`marathon.json` in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="23ee5-158">Specify hello path toohello JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="23ee5-159">È possibile utilizzare anche hello maratona API tooscale out o la scala in distribuzioni di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="23ee5-159">You can also use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="23ee5-160">Nell'esempio precedente hello, si è distribuito un'istanza di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="23ee5-160">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="23ee5-161">Possibile modificare le proporzioni toothree istanze di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="23ee5-161">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="23ee5-162">toodo in tal caso, creare un file JSON utilizzando hello dopo il testo JSON e archiviarlo in un percorso accessibile.</span><span class="sxs-lookup"><span data-stu-id="23ee5-162">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="23ee5-163">Eseguire hello tooscale comando out applicazione hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="23ee5-163">Run hello following command tooscale out hello application:</span></span>

> [!NOTE]
> <span data-ttu-id="23ee5-164">Hello URI è seguito dall'ID hello di hello applicazione tooscale http://localhost/marathon/v2/apps/.</span><span class="sxs-lookup"><span data-stu-id="23ee5-164">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="23ee5-165">Se si utilizza esempio Nginx hello fornito di seguito, hello URI sarebbe http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="23ee5-165">If you are using hello Nginx sample provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="23ee5-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23ee5-166">Next steps</span></span>
* [<span data-ttu-id="23ee5-167">Per ulteriori informazioni su endpoint HTTP Mesos hello</span><span class="sxs-lookup"><span data-stu-id="23ee5-167">Read more about hello Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="23ee5-168">Per ulteriori informazioni su hello maratona REST API</span><span class="sxs-lookup"><span data-stu-id="23ee5-168">Read more about hello Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

