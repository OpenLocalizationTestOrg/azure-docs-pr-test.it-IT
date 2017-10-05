---
title: Versione canary con Vamp nel cluster DC/OS di Azure | Microsoft Docs
description: Come usare Vamp per i servizi della versione canary e applicare filtri intelligenti al traffico in un cluster Azure DC/OS del servizio contenitore di Azure
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: 4a20091b59f2643ea71cce99c159a5075706e35d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="a6375-103">Microservizi della versione canary con Vamp in un cluster DC/OS del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="a6375-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="a6375-104">In questa procedura dettagliata viene configurato Vamp nel servizio contenitore di Azure con un cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="a6375-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="a6375-105">Viene rilasciata la versione canary del servizio demo "sava" di Vamp che risolvere un problema di incompatibilità del servizio con Firefox applicando filtri intelligenti al traffico.</span><span class="sxs-lookup"><span data-stu-id="a6375-105">We canary release the Vamp demo service "sava", and then resolve an incompatibility of the service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="a6375-106">In questa procedura dettagliata Vamp viene eseguito in un cluster DC/OS, ma è anche possibile usarlo con Kubernetes come agente di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="a6375-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as the orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="a6375-107">Informazioni sulle versioni canary e su Vamp</span><span class="sxs-lookup"><span data-stu-id="a6375-107">About canary releases and Vamp</span></span>


<span data-ttu-id="a6375-108">La [versione canary](https://martinfowler.com/bliki/CanaryRelease.html) è una strategia di distribuzione intelligente adottata da organizzazioni innovative come Netflix, Facebook e Spotify.</span><span class="sxs-lookup"><span data-stu-id="a6375-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="a6375-109">È un buon approccio che consente di ridurre i problemi, introdurre reti di sicurezza e aumentare l'innovazione.</span><span class="sxs-lookup"><span data-stu-id="a6375-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="a6375-110">Perché quindi non lo usato tutte le società?</span><span class="sxs-lookup"><span data-stu-id="a6375-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="a6375-111">L'estensione di una pipeline CI/CD per includere le strategie canary aggiunge complessità e richiede un'ampia esperienza e una vasta conoscenza di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="a6375-111">Extending a CI/CD pipeline to include canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="a6375-112">Questa è una motivazione sufficiente affinché società e organizzazioni di piccole dimensioni non riescano ad avviare il processo.</span><span class="sxs-lookup"><span data-stu-id="a6375-112">That’s enough to block smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="a6375-113">[Vamp](http://vamp.io/) è un sistema open source progettato per facilitare la transizione e portare le funzioni della versione canary all'utilità di pianificazione del contenitore preferita.</span><span class="sxs-lookup"><span data-stu-id="a6375-113">[Vamp](http://vamp.io/) is an open-source system designed to ease this transition and bring canary releasing features to your preferred container scheduler.</span></span> <span data-ttu-id="a6375-114">La funzionalità canary di Vamp va oltre le implementazioni basate su percentuale.</span><span class="sxs-lookup"><span data-stu-id="a6375-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="a6375-115">È possibile filtrare il traffico e dividerlo in base a una vasta gamma di condizioni, ad esempio in base a destinatari specifici, intervalli di indirizzi IP o dispositivi.</span><span class="sxs-lookup"><span data-stu-id="a6375-115">Traffic can be filtered and split on a wide range of conditions, for example to target specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="a6375-116">Vamp tiene traccia e analizza le metriche delle prestazioni, consentendo l'automazione in base a dati reali.</span><span class="sxs-lookup"><span data-stu-id="a6375-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="a6375-117">È possibile configurare il ripristino automatico dello stato precedente in caso di errori o aumentare le prestazioni delle varianti dei singoli servizi in base al carico o alla latenza.</span><span class="sxs-lookup"><span data-stu-id="a6375-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="a6375-118">Configurare il servizio contenitore di Azure con DC/OS</span><span class="sxs-lookup"><span data-stu-id="a6375-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="a6375-119">[Distribuire un cluster DC/OS](container-service-deployment.md) con un master e due agenti di dimensioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="a6375-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="a6375-120">[Creare un tunnel SSH](../container-service-connect.md) per connettersi al cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="a6375-120">[Create an SSH tunnel](../container-service-connect.md) to connect to the DC/OS cluster.</span></span> <span data-ttu-id="a6375-121">Questo articolo presuppone l'esecuzione del tunneling per il cluster sulla porta locale 80.</span><span class="sxs-lookup"><span data-stu-id="a6375-121">This article assumes that you tunnel to the cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="a6375-122">Configurare Vamp</span><span class="sxs-lookup"><span data-stu-id="a6375-122">Set up Vamp</span></span>

<span data-ttu-id="a6375-123">Ora che si dispone di un cluster DC/OS in esecuzione, è possibile installare Vamp dall'interfaccia utente DC/OS (http://localhost:80).</span><span class="sxs-lookup"><span data-stu-id="a6375-123">Now that you have a running DC/OS cluster, you can install Vamp from the DC/OS UI (http://localhost:80).</span></span> 

![Interfaccia utente di DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="a6375-125">L'installazione viene eseguita in due fasi:</span><span class="sxs-lookup"><span data-stu-id="a6375-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="a6375-126">**Distribuire Elasticsearch**.</span><span class="sxs-lookup"><span data-stu-id="a6375-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="a6375-127">Quindi **distribuire Vamp** installando il pacchetto Universo DC/OS di Vamp.</span><span class="sxs-lookup"><span data-stu-id="a6375-127">Then **deploy Vamp** by installing the Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="a6375-128">Distribuire Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="a6375-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="a6375-129">Per la raccolta delle metriche e l'aggregazione Vamp richiede Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="a6375-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="a6375-130">Per distribuire uno stack Vamp Elasticsearch compatibile è possibile usare le [immagini magneticio](https://hub.docker.com/r/magneticio/elastic/).</span><span class="sxs-lookup"><span data-stu-id="a6375-130">You can use the [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) to deploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="a6375-131">Nell'interfaccia utente DC/OS passare a **Servizi** e fare clic su **Distribuisci servizio**.</span><span class="sxs-lookup"><span data-stu-id="a6375-131">In the DC/OS UI, go to **Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="a6375-132">Selezionare **JSON mode** (Modalità JSON) dal popup **Deploy New Service** (Distribuisci il nuovo servizio).</span><span class="sxs-lookup"><span data-stu-id="a6375-132">Select **JSON mode** from the **Deploy New Service** pop-up.</span></span>

  ![Selezione della modalità JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="a6375-134">Incollare il JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="a6375-134">Paste in the following JSON.</span></span> <span data-ttu-id="a6375-135">Questa configurazione esegue il contenitore con 1 GB di RAM e un controllo di integrità di base sulla porta Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="a6375-135">This configuration runs the container with 1 GB of RAM and a basic health check on the Elasticsearch port.</span></span>
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. <span data-ttu-id="a6375-136">Fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="a6375-136">Click **Deploy**.</span></span>

  <span data-ttu-id="a6375-137">DC/OS consente di distribuire il contenitore Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="a6375-137">DC/OS deploys the Elasticsearch container.</span></span> <span data-ttu-id="a6375-138">Nella pagina **Servizi** è possibile monitorare l'avanzamento.</span><span class="sxs-lookup"><span data-stu-id="a6375-138">You can track progress on the **Services** page.</span></span>  

  ![distribuzione di Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="a6375-140">Distribuire Vamp</span><span class="sxs-lookup"><span data-stu-id="a6375-140">Deploy Vamp</span></span>

<span data-ttu-id="a6375-141">Quando Elasticsearch segnala lo stato **In esecuzione**, è possibile aggiungere il pacchetto Universo DC/OS di Vamp.</span><span class="sxs-lookup"><span data-stu-id="a6375-141">Once Elasticsearch reports as **Running**, you can add the Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="a6375-142">Passare a **Universe** (Universo) e cercare **vamp**.</span><span class="sxs-lookup"><span data-stu-id="a6375-142">Go to **Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="a6375-143">![Vamp in Universe (Universo) DC/OS](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="a6375-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="a6375-144">Fare clic su **Installa** accanto ai pacchetto vamp e scegliere **Advanced Installation** (Installazione avanzata).</span><span class="sxs-lookup"><span data-stu-id="a6375-144">Click **install** next to the vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="a6375-145">Scorrere verso il basso e immettere il seguente URL di Elasticsearch: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="a6375-145">Scroll down and enter the following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Immettere l'URL di Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="a6375-147">Fare clic su **Verifica e installa**, quindi fare clic su **Installa** per avviare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a6375-147">Click **Review and Install**, then click **Install** to start the deployment.</span></span>  

  <span data-ttu-id="a6375-148">DC/OS distribuisce tutti i componenti necessari di Vamp.</span><span class="sxs-lookup"><span data-stu-id="a6375-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="a6375-149">Nella pagina **Servizi** è possibile monitorare l'avanzamento.</span><span class="sxs-lookup"><span data-stu-id="a6375-149">You can track progress on the **Services** page.</span></span>
  
  ![Distribuire Vamp come pacchetto universo](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="a6375-151">Dopo aver completato la distribuzione, è possibile accedere all'interfaccia utente di Vamp:</span><span class="sxs-lookup"><span data-stu-id="a6375-151">Once deployment has completed, you can access the Vamp UI:</span></span>

  ![Servizio Vamp su DC/OS](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Interfaccia utente di Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="a6375-154">Distribuire il primo servizio</span><span class="sxs-lookup"><span data-stu-id="a6375-154">Deploy your first service</span></span>

<span data-ttu-id="a6375-155">Ora che Vamp è in esecuzione, è possibile distribuire un servizio da un progetto.</span><span class="sxs-lookup"><span data-stu-id="a6375-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="a6375-156">Nella forma più semplice, un [progetto Vamp](http://vamp.io/documentation/using-vamp/blueprints/) descrive gli endpoint, ovvero i gateway, i cluster e i servizi da distribuire.</span><span class="sxs-lookup"><span data-stu-id="a6375-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes the endpoints (gateways), clusters, and services to deploy.</span></span> <span data-ttu-id="a6375-157">Vamp usa i cluster per raggruppare diverse varianti dello stesso servizio in gruppi logici per la versione canary o i test A/B.</span><span class="sxs-lookup"><span data-stu-id="a6375-157">Vamp uses clusters to group different variants of the same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="a6375-158">Questo scenario usa un'applicazione monolitica di esempio denominata [**sava**](https://github.com/magneticio/sava), che è alla versione 1.0.</span><span class="sxs-lookup"><span data-stu-id="a6375-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="a6375-159">Il monolite viene compresso in un contenitore Docker, disponibile nell'hub Docker in magneticio/sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="a6375-159">The monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="a6375-160">L'app generalmente viene eseguita sulla porta 8080, ma in questo caso si desidera esporla nella porta 9050.</span><span class="sxs-lookup"><span data-stu-id="a6375-160">The app normally runs on port 8080, but you want to expose it under port 9050 in this case.</span></span> <span data-ttu-id="a6375-161">Distribuire l'app tramite Vamp usando un progetto semplice.</span><span class="sxs-lookup"><span data-stu-id="a6375-161">Deploy the app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="a6375-162">Andare in **Deployments** (Distribuzioni).</span><span class="sxs-lookup"><span data-stu-id="a6375-162">Go to **Deployments**.</span></span>

2. <span data-ttu-id="a6375-163">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a6375-163">Click **Add**.</span></span>

3. <span data-ttu-id="a6375-164">Incollare il progetto YAML seguente.</span><span class="sxs-lookup"><span data-stu-id="a6375-164">Paste in the following blueprint YAML.</span></span> <span data-ttu-id="a6375-165">Questo progetto contiene un cluster con solo una variante di servizio, che verrà modificata in un passaggio successivo:</span><span class="sxs-lookup"><span data-stu-id="a6375-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster to create
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="a6375-166">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a6375-166">Click **Save**.</span></span> <span data-ttu-id="a6375-167">Vamp avvia la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a6375-167">Vamp initiates the deployment.</span></span>

<span data-ttu-id="a6375-168">La distribuzione viene elencata nella pagina **Distribuzioni**.</span><span class="sxs-lookup"><span data-stu-id="a6375-168">The deployment is listed on the **Deployments** page.</span></span> <span data-ttu-id="a6375-169">Fare clic sulla distribuzione per monitorarne lo stato.</span><span class="sxs-lookup"><span data-stu-id="a6375-169">Click the deployment to monitor its status.</span></span>

![Interfaccia utente Vamp: distribuzione sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![servizio sava nell'interfaccia utente di Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="a6375-172">Sono stati creati due gateway, elencati nella pagina **Gateways** (Gateway):</span><span class="sxs-lookup"><span data-stu-id="a6375-172">Two gateways are created, which are listed on the **Gateways** page:</span></span>

* <span data-ttu-id="a6375-173">un endpoint stabile per accedere al servizio in esecuzione, sulla porta 9050</span><span class="sxs-lookup"><span data-stu-id="a6375-173">a stable endpoint to access the running service (port 9050)</span></span> 
* <span data-ttu-id="a6375-174">un gateway interno gestito da Vamp, altre informazioni su questo gateway verranno date in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="a6375-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Interfaccia utente di Vamp: gateway sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="a6375-176">Il servizio sava è stato distribuito, ma non è possibile accedervi dall'esterno perché Azure Load Balancer non può ancora inoltrarvi il traffico.</span><span class="sxs-lookup"><span data-stu-id="a6375-176">The sava service has now deployed, but you can’t access it externally because the Azure Load Balancer doesn’t know to forward traffic to it yet.</span></span> <span data-ttu-id="a6375-177">Per accedere al servizio, aggiornare la configurazione di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6375-177">To access the service, update the Azure networking configuration.</span></span>


## <a name="update-the-azure-network-configuration"></a><span data-ttu-id="a6375-178">Aggiornare la configurazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a6375-178">Update the Azure network configuration</span></span>

<span data-ttu-id="a6375-179">Vamp ha distribuito il servizio sava nei nodi dell'agente DC/OS, esponendo un endpoint stabile sulla porta 9050.</span><span class="sxs-lookup"><span data-stu-id="a6375-179">Vamp deployed the sava service on the DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="a6375-180">Per accedere al servizio dall'esterno del cluster DC/OS, apportare le modifiche seguenti alla configurazione di rete di Azure della distribuzione del cluster:</span><span class="sxs-lookup"><span data-stu-id="a6375-180">To access the service from outside the DC/OS cluster, make the following changes to the Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="a6375-181">**Configurare Azure Load Balancer** per gli agenti, la risorsa denominata **dcos-agent-lb-xxxx**, con un probe di integrità e una regola per inoltrare il traffico sulla porta 9050 alle istanze sava.</span><span class="sxs-lookup"><span data-stu-id="a6375-181">**Configure the Azure Load Balancer** for the agents (the resource named **dcos-agent-lb-xxxx**) with a health probe and a rule to forward traffic on port 9050 to the sava instances.</span></span> 

2. <span data-ttu-id="a6375-182">**Aggiornare il gruppo di sicurezza di rete** per gli agenti pubblici, la risorsa denominata **XXXX-agent-public-nsg-XXXX**, per consentire il traffico sulla porta 9050.</span><span class="sxs-lookup"><span data-stu-id="a6375-182">**Update the network security group** for the public agents (the resource named **XXXX-agent-public-nsg-XXXX**) to allow traffic on port 9050.</span></span>

<span data-ttu-id="a6375-183">Per istruzioni dettagliate su come completare queste attività tramite il portale di Azure, vedere [Abilitare l'accesso pubblico a un'applicazione del servizio contenitore di Azure](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="a6375-183">For detailed steps to complete these tasks using the Azure portal, see [Enable public access to an Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="a6375-184">Specificare la porta 9050 per tutte le impostazioni della porta.</span><span class="sxs-lookup"><span data-stu-id="a6375-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="a6375-185">Dopo aver creato tutti gli elementi, andare nel pannello **Panoramica** del servizio di bilanciamento del carico dell'agente DC/OS, ovvero la risorsa denominata **dcos-agent-lb-xxxx**.</span><span class="sxs-lookup"><span data-stu-id="a6375-185">Once everything has been created, go to the **Overview** blade of the DC/OS agent load balancer (the resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="a6375-186">Trovare l'**indirizzo IP pubblico** e usarlo per far accedere sava alla porta 9050.</span><span class="sxs-lookup"><span data-stu-id="a6375-186">Find the **Public IP address**, and use the address to access sava at port 9050.</span></span>

![Portale di Azure: ottenere l'indirizzo IP pubblico](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="a6375-189">Eseguire una versione canary</span><span class="sxs-lookup"><span data-stu-id="a6375-189">Run a canary release</span></span>

<span data-ttu-id="a6375-190">Si supponga di avere una nuova versione dell'applicazione per cui si desidera rilasciare una versione canary nella produzione.</span><span class="sxs-lookup"><span data-stu-id="a6375-190">Suppose you have a new version of this application that you want to canary release into production.</span></span> <span data-ttu-id="a6375-191">È stata inserita in un contenitore come magneticio/sava:1.1.0 ed è pronta all'uso.</span><span class="sxs-lookup"><span data-stu-id="a6375-191">You have it containerized as magneticio/sava:1.1.0 and are ready to go.</span></span> <span data-ttu-id="a6375-192">Vamp consente di aggiungere facilmente nuovi servizi alla distribuzione in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a6375-192">Vamp lets you easily add new services to the running deployment.</span></span> <span data-ttu-id="a6375-193">Questi servizi "uniti" vengono distribuiti insieme ai servizi esistenti nel cluster e viene assegnato loro un peso pari a 0%.</span><span class="sxs-lookup"><span data-stu-id="a6375-193">These "merged" services are deployed alongside the existing services in the cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="a6375-194">Il traffico non viene indirizzato a un nuovo servizio unito fino a quando la distribuzione del traffico non viene regolata.</span><span class="sxs-lookup"><span data-stu-id="a6375-194">No traffic is routed to a newly merged service until you adjust the traffic distribution.</span></span> <span data-ttu-id="a6375-195">Il dispositivo di scorrimento del peso nell'interfaccia utente di Vamp offre il controllo completo sulla distribuzione, consentendo di effettuare modifiche incrementali, ad esempio la versione canary, o un ripristino immediato dello stato precedente.</span><span class="sxs-lookup"><span data-stu-id="a6375-195">The weight slider in the Vamp UI gives you complete control over the distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="a6375-196">Unire una nuova variante di servizio</span><span class="sxs-lookup"><span data-stu-id="a6375-196">Merge a new service variant</span></span>

<span data-ttu-id="a6375-197">Per unire il nuovo servizio sava 1.1 con la distribuzione in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="a6375-197">To merge the new sava 1.1 service with the running deployment:</span></span>

1. <span data-ttu-id="a6375-198">Nell'interfaccia utente di Vamp fare clic su **Blueprints** (Progetti).</span><span class="sxs-lookup"><span data-stu-id="a6375-198">In the Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="a6375-199">Fare clic su **Add** (Aggiungi) e incollare il seguente progetto YAML: questo progetto descrive una nuova variante di servizio, sava: 1.1.0, da distribuire nel cluster esistente, sava_cluster.</span><span class="sxs-lookup"><span data-stu-id="a6375-199">Click **Add** and paste in the following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) to deploy within the existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster to update
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint to update
  ```
  
3. <span data-ttu-id="a6375-200">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a6375-200">Click **Save**.</span></span> <span data-ttu-id="a6375-201">Il progetto viene archiviato ed elencato nella pagina **Blueprints** (Progetti).</span><span class="sxs-lookup"><span data-stu-id="a6375-201">The blueprint is stored and listed on the **Blueprints** page.</span></span>

4. <span data-ttu-id="a6375-202">Aprire il menu di azione nel progetto sava:1.1 e fare clic su **Merge to** (Unisci a).</span><span class="sxs-lookup"><span data-stu-id="a6375-202">Open the action menu on the sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Interfaccia utente di Vamp: progetti](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="a6375-204">Selezionare la distribuzione **sava** e fare clic su **Merge** (Unisci).</span><span class="sxs-lookup"><span data-stu-id="a6375-204">Select the **sava** deployment and click **Merge**.</span></span>

  ![Interfaccia utente di Vamp: progetto di unione alla distribuzione](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="a6375-206">Vamp consente di distribuire la nuova variante di servizio sava:1.1.0 descritta nel progetto insieme a sava:1.0.0 in **sava_cluster** della distribuzione in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a6375-206">Vamp deploys the new sava:1.1.0 service variant described in the blueprint alongside sava:1.0.0 in the **sava_cluster** of the running deployment.</span></span> 

![Interfaccia utente di Vamp: distribuzione sava aggiornato](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="a6375-208">Anche il gateway **sava/sava_cluster/webport**, ovvero l'endpoint del cluster, viene aggiornato aggiungendo una route per sava:1.1.0 appena distribuito.</span><span class="sxs-lookup"><span data-stu-id="a6375-208">The **sava/sava_cluster/webport** gateway (the cluster endpoint) is also updated, adding a route to the newly deployed sava:1.1.0.</span></span> <span data-ttu-id="a6375-209">A questo punto, il traffico non viene indirizzato qui, infatti **WEIGHT** (PESO) è impostato su 0%.</span><span class="sxs-lookup"><span data-stu-id="a6375-209">At this point, no traffic is routed here (the **WEIGHT** is set to 0%).</span></span>

![Interfaccia utente di Vamp: gateway del cluster](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="a6375-211">Versione canary</span><span class="sxs-lookup"><span data-stu-id="a6375-211">Canary release</span></span>

<span data-ttu-id="a6375-212">Dopo aver distribuito entrambe le versioni di sava nello stesso cluster, modificare la distribuzione del traffico tra di essi spostando il dispositivo di scorrimento **WEIGHT** (PESO).</span><span class="sxs-lookup"><span data-stu-id="a6375-212">With both versions of sava deployed in the same cluster, adjust the distribution of traffic between them by moving the **WEIGHT** slider.</span></span>

1. <span data-ttu-id="a6375-213">Fare clic su ![Interfaccia utente di Vamp: modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) accanto a **WEIGHT** (PESO).</span><span class="sxs-lookup"><span data-stu-id="a6375-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT**.</span></span>

2. <span data-ttu-id="a6375-214">Impostare la distribuzione del peso su 50%/50% e fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="a6375-214">Set the weight distribution to 50%/50% and click **Save**.</span></span>

  ![Interfaccia utente di Vamp: dispositivo di scorrimento del peso del gateway](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="a6375-216">Tornare al browser e aggiornare la pagina di sava altre volte.</span><span class="sxs-lookup"><span data-stu-id="a6375-216">Go back to your browser and refresh the sava page a few more times.</span></span> <span data-ttu-id="a6375-217">Ora l'applicazione sava passa da una pagina sava:1.0 a una pagina sava:1.1.</span><span class="sxs-lookup"><span data-stu-id="a6375-217">The sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![alternanza dei servizi sava1.0 e sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="a6375-219">Questa alternanza della pagina funziona meglio con la modalità "Incognito" (In incognito) o "Anonymous" (Anonimo) del browser a causa della memorizzazione nella cache delle risorse statiche.</span><span class="sxs-lookup"><span data-stu-id="a6375-219">This alternation of the page works best with the "Incognito" or “Anonymous” mode of your browser because of the caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="a6375-220">Filtrare il traffico</span><span class="sxs-lookup"><span data-stu-id="a6375-220">Filter traffic</span></span>

<span data-ttu-id="a6375-221">Si supponga che in seguito alla distribuzione sia stato individuato un problema di incompatibilità in sava:1.1.0 che causa problemi di visualizzazione nel browser Firefox.</span><span class="sxs-lookup"><span data-stu-id="a6375-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="a6375-222">È possibile impostare Vamp affinché filtri il traffico in ingresso e indirizzi di nuovo tutti gli utenti di Firefox alla versione stabile di sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="a6375-222">You can set Vamp to filter incoming traffic and direct all Firefox users back to the known stable sava:1.0.0.</span></span> <span data-ttu-id="a6375-223">Questo filtro consente di risolvere immediatamente le interruzioni per gli utenti di Firefox, mentre gli altri utenti continuano a sfruttare i vantaggi della versione migliorata di sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="a6375-223">This filter instantly resolves the disruption for Firefox users, while everybody else continues to enjoy the benefits of the improved sava:1.1.0.</span></span>

<span data-ttu-id="a6375-224">Vamp usa le **condizioni** per filtrare il traffico tra le route in un gateway.</span><span class="sxs-lookup"><span data-stu-id="a6375-224">Vamp uses **conditions** to filter traffic between routes in a gateway.</span></span> <span data-ttu-id="a6375-225">Il traffico viene innanzitutto filtrato e indirizzato in base alle condizioni applicate a ogni route.</span><span class="sxs-lookup"><span data-stu-id="a6375-225">Traffic is first filtered and directed according to the conditions applied to each route.</span></span> <span data-ttu-id="a6375-226">Il traffico restante viene distribuito in base all'impostazione del peso del gateway.</span><span class="sxs-lookup"><span data-stu-id="a6375-226">All remaining traffic is distributed according to the gateway weight setting.</span></span>

<span data-ttu-id="a6375-227">È possibile creare una condizione per filtrare tutti gli utenti di Firefox e indirizzarli alla versione precedente di sava:1.0.0:</span><span class="sxs-lookup"><span data-stu-id="a6375-227">You can create a condition to filter all Firefox users and direct them to the old sava:1.0.0:</span></span>

1. <span data-ttu-id="a6375-228">Nella pagina **Gateways** (Gateway) sava/sava_cluster/webport fare clic su ![Interfaccia utente di Vamp: modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) per aggiungere una **CONDIZIONE** alla route sava/sava_cluster/sava:1.0.0/webport.</span><span class="sxs-lookup"><span data-stu-id="a6375-228">On the sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to add a **CONDITION** to the route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="a6375-229">Immettere la condizione **user-agent == Firefox** e fare clic su ![Interfaccia utente di Vamp: salva](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="a6375-229">Enter the condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="a6375-230">Vamp aggiunge la condizione con un livello pari a 0%.</span><span class="sxs-lookup"><span data-stu-id="a6375-230">Vamp adds the condition with a default strength of 0%.</span></span> <span data-ttu-id="a6375-231">Per avviare il filtraggio del traffico, è necessario regolare la forza della condizione.</span><span class="sxs-lookup"><span data-stu-id="a6375-231">To start filtering traffic, you need to adjust the condition strength.</span></span>

3. <span data-ttu-id="a6375-232">Fare clic su ![Interfaccia utente di Vamp: modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) per modificare la **forza** applicata alla condizione.</span><span class="sxs-lookup"><span data-stu-id="a6375-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to change the **STRENGTH** applied to the condition.</span></span>
 
4. <span data-ttu-id="a6375-233">Impostare **STRENGTH** (Forza) al 100% e fare clic su ![Interfaccia utente di Vamp: salva](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) per salvare.</span><span class="sxs-lookup"><span data-stu-id="a6375-233">Set the **STRENGTH** to 100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) to save.</span></span>

  <span data-ttu-id="a6375-234">Vamp ora invia tutto il traffico che corrisponde alla condizione, ovvero tutti gli utenti di Firefox, a sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="a6375-234">Vamp now sends all traffic matching the condition (all Firefox users) to sava:1.0.0.</span></span>

  ![Interfaccia utente di Vamp: condizione applicata al gateway](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="a6375-236">Infine, regolare il peso del gateway per l'invio di tutto il traffico rimanente, ovvero tutti gli utenti non Firefox, al nuovo sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="a6375-236">Finally, adjust the gateway weight to send all remaining traffic (all non-Firefox users) to the new sava:1.1.0.</span></span> <span data-ttu-id="a6375-237">Fare clic su ![Interfaccia utente di Vamp: modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) accanto a **WEIGHT** (PESO) e impostare la distribuzione del peso in modo che il 100% venga indirizzato alla route sava/sava_cluster/sava:1.1.0/webport.</span><span class="sxs-lookup"><span data-stu-id="a6375-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT** and set the weight distribution so 100% is directed to the route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="a6375-238">Tutto il traffico non filtrato dalla condizione ora viene indirizzato alla nuova versione di sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="a6375-238">All traffic not filtered by the condition is now directed to the new sava:1.1.0.</span></span>

6. <span data-ttu-id="a6375-239">Per visualizzare il filtro in azione, aprire due diversi browser, Firefox e un altro browser, e accedere al servizio sava da entrambi.</span><span class="sxs-lookup"><span data-stu-id="a6375-239">To see the filter in action, open two different browsers (one Firefox and one other browser) and access the sava service from both.</span></span> <span data-ttu-id="a6375-240">Tutte le richieste di Firefox vengono inviate a sava:1.0.0, mentre tutti gli altri browser vengono indirizzati a sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="a6375-240">All Firefox requests are sent to sava:1.0.0, while all other browsers are directed to sava:1.1.0.</span></span>

  ![Interfaccia utente di Vamp: filtrare il traffico](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="a6375-242">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="a6375-242">Summing up</span></span>

<span data-ttu-id="a6375-243">Questo articolo contiene una rapida introduzione a Vamp in un cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="a6375-243">This article was a quick introduction to Vamp on a DC/OS cluster.</span></span> <span data-ttu-id="a6375-244">Per i principianti, Vamp è stato messo in esecuzione nel cluster DC/OS del servizio contenitore di Azure, è stato distribuito un servizio con un progetto Vamp ed è stato effettuato l'accesso all'endpoint esposto, ovvero il gateway.</span><span class="sxs-lookup"><span data-stu-id="a6375-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at the exposed endpoint (gateway).</span></span>

<span data-ttu-id="a6375-245">Sono state trattate anche alcune funzioni importanti di Vamp: l'unione di una nuova variante di servizio alla distribuzione in esecuzione e l'introduzione incrementale, quindi il filtraggio del traffico per risolvere un'incompatibilità nota.</span><span class="sxs-lookup"><span data-stu-id="a6375-245">We also touched on some powerful features of Vamp:  merging a new service variant to the running deployment and introducing it incrementally, then filtering traffic to resolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a6375-246">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6375-246">Next steps</span></span>

* <span data-ttu-id="a6375-247">Informazioni sulla gestione delle azioni Vamp attraverso le [API REST di Vamp](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="a6375-247">Learn about managing Vamp actions through the [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="a6375-248">Creazione di script di automazione Vamp in Node.js ed esecuzione degli stessi come [flussi di lavoro di Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="a6375-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="a6375-249">Vedere altre [esercitazioni su Vamp](http://vamp.io/documentation/tutorials/overview/).</span><span class="sxs-lookup"><span data-stu-id="a6375-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

