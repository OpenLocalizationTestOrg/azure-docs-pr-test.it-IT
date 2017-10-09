---
title: versione aaaCanary con Vamp nel cluster di controller di dominio o sistema operativo di Azure | Documenti Microsoft
description: Come toouse Vamp toocanary servizi di rilascio e applicare smart traffico filtro in un cluster di Azure contenitore del servizio controller di dominio o del sistema operativo
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
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="d66ed-103">Microservizi della versione canary con Vamp in un cluster DC/OS del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="d66ed-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="d66ed-104">In questa procedura dettagliata viene configurato Vamp nel servizio contenitore di Azure con un cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="d66ed-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="d66ed-105">Abbiamo canary rilasciare servizio demo di hello Vamp "sava" e quindi risolvere un problema di incompatibilità del servizio hello con Firefox applicando filtri traffico smart.</span><span class="sxs-lookup"><span data-stu-id="d66ed-105">We canary release hello Vamp demo service "sava", and then resolve an incompatibility of hello service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="d66ed-106">In questa procedura dettagliata Vamp viene eseguito in un cluster di controller di dominio o del sistema operativo, ma è anche possibile utilizzare Vamp con Kubernetes come orchestrator hello.</span><span class="sxs-lookup"><span data-stu-id="d66ed-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as hello orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="d66ed-107">Informazioni sulle versioni canary e su Vamp</span><span class="sxs-lookup"><span data-stu-id="d66ed-107">About canary releases and Vamp</span></span>


<span data-ttu-id="d66ed-108">La [versione canary](https://martinfowler.com/bliki/CanaryRelease.html) è una strategia di distribuzione intelligente adottata da organizzazioni innovative come Netflix, Facebook e Spotify.</span><span class="sxs-lookup"><span data-stu-id="d66ed-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="d66ed-109">È un buon approccio che consente di ridurre i problemi, introdurre reti di sicurezza e aumentare l'innovazione.</span><span class="sxs-lookup"><span data-stu-id="d66ed-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="d66ed-110">Perché quindi non lo usato tutte le società?</span><span class="sxs-lookup"><span data-stu-id="d66ed-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="d66ed-111">Estendere un tooinclude pipeline CI/CD strategie Canarie aggiunge complessità e richiede esperienza e le informazioni estese devops.</span><span class="sxs-lookup"><span data-stu-id="d66ed-111">Extending a CI/CD pipeline tooinclude canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="d66ed-112">È sufficiente tooblock piccole aziende e le aziende possono preliminari sono anche.</span><span class="sxs-lookup"><span data-stu-id="d66ed-112">That’s enough tooblock smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="d66ed-113">[Vamp](http://vamp.io/) è tooease un sistema open source progettato questa transizione e portare canary rilascio funzionalità tooyour preferito contenitore dell'utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="d66ed-113">[Vamp](http://vamp.io/) is an open-source system designed tooease this transition and bring canary releasing features tooyour preferred container scheduler.</span></span> <span data-ttu-id="d66ed-114">La funzionalità canary di Vamp va oltre le implementazioni basate su percentuale.</span><span class="sxs-lookup"><span data-stu-id="d66ed-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="d66ed-115">Possibile filtrare il traffico e diviso in base a un'ampia gamma di condizioni, ad esempio tootarget utenti, gli intervalli IP o dispositivi specifici.</span><span class="sxs-lookup"><span data-stu-id="d66ed-115">Traffic can be filtered and split on a wide range of conditions, for example tootarget specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="d66ed-116">Vamp tiene traccia e analizza le metriche delle prestazioni, consentendo l'automazione in base a dati reali.</span><span class="sxs-lookup"><span data-stu-id="d66ed-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="d66ed-117">È possibile configurare il ripristino automatico dello stato precedente in caso di errori o aumentare le prestazioni delle varianti dei singoli servizi in base al carico o alla latenza.</span><span class="sxs-lookup"><span data-stu-id="d66ed-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="d66ed-118">Configurare il servizio contenitore di Azure con DC/OS</span><span class="sxs-lookup"><span data-stu-id="d66ed-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="d66ed-119">[Distribuire un cluster DC/OS](container-service-deployment.md) con un master e due agenti di dimensioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="d66ed-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="d66ed-120">[Creare un tunnel SSH](../container-service-connect.md) cluster di tooconnect toohello controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d66ed-120">[Create an SSH tunnel](../container-service-connect.md) tooconnect toohello DC/OS cluster.</span></span> <span data-ttu-id="d66ed-121">Questo articolo si presuppone che si tunnel cluster toohello porta locale 80.</span><span class="sxs-lookup"><span data-stu-id="d66ed-121">This article assumes that you tunnel toohello cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="d66ed-122">Configurare Vamp</span><span class="sxs-lookup"><span data-stu-id="d66ed-122">Set up Vamp</span></span>

<span data-ttu-id="d66ed-123">Dopo aver creato un cluster di controller di dominio o del sistema operativo in esecuzione, è possibile installare Vamp da hello controller di dominio o del sistema operativo dell'interfaccia utente (http://localhost:80).</span><span class="sxs-lookup"><span data-stu-id="d66ed-123">Now that you have a running DC/OS cluster, you can install Vamp from hello DC/OS UI (http://localhost:80).</span></span> 

![Interfaccia utente di DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="d66ed-125">L'installazione viene eseguita in due fasi:</span><span class="sxs-lookup"><span data-stu-id="d66ed-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="d66ed-126">**Distribuire Elasticsearch**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="d66ed-127">Quindi **distribuire Vamp** installando pacchetto universo di hello controller di dominio di Vamp del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d66ed-127">Then **deploy Vamp** by installing hello Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="d66ed-128">Distribuire Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="d66ed-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="d66ed-129">Per la raccolta delle metriche e l'aggregazione Vamp richiede Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="d66ed-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="d66ed-130">È possibile utilizzare hello [immagini Docker magneticio](https://hub.docker.com/r/magneticio/elastic/) toodeploy uno stack Vamp Elasticsearch compatibile.</span><span class="sxs-lookup"><span data-stu-id="d66ed-130">You can use hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="d66ed-131">Nell'interfaccia utente di controller di dominio/OS hello, andare troppo**servizi** e fare clic su **distribuzione servizio**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-131">In hello DC/OS UI, go too**Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="d66ed-132">Selezionare **modalità JSON** da hello **distribuire nuovo servizio** popup.</span><span class="sxs-lookup"><span data-stu-id="d66ed-132">Select **JSON mode** from hello **Deploy New Service** pop-up.</span></span>

  ![Selezione della modalità JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="d66ed-134">Incollare in hello seguente JSON.</span><span class="sxs-lookup"><span data-stu-id="d66ed-134">Paste in hello following JSON.</span></span> <span data-ttu-id="d66ed-135">Questa configurazione esegue contenitore hello con 1 GB di RAM e di controllo di integrità di base sulla porta Elasticsearch hello.</span><span class="sxs-lookup"><span data-stu-id="d66ed-135">This configuration runs hello container with 1 GB of RAM and a basic health check on hello Elasticsearch port.</span></span>
  
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
  

3. <span data-ttu-id="d66ed-136">Fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-136">Click **Deploy**.</span></span>

  <span data-ttu-id="d66ed-137">Controller di dominio o sistema operativo distribuisce contenitore Elasticsearch hello.</span><span class="sxs-lookup"><span data-stu-id="d66ed-137">DC/OS deploys hello Elasticsearch container.</span></span> <span data-ttu-id="d66ed-138">È possibile monitorare lo stato di avanzamento in hello **servizi** pagina.</span><span class="sxs-lookup"><span data-stu-id="d66ed-138">You can track progress on hello **Services** page.</span></span>  

  ![distribuzione di Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="d66ed-140">Distribuire Vamp</span><span class="sxs-lookup"><span data-stu-id="d66ed-140">Deploy Vamp</span></span>

<span data-ttu-id="d66ed-141">Una volta che viene segnalato da Elasticsearch **in esecuzione**, è possibile aggiungere pacchetti di hello Vamp universo dei controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d66ed-141">Once Elasticsearch reports as **Running**, you can add hello Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="d66ed-142">Andare troppo**universo** e cercare **vamp**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-142">Go too**Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="d66ed-143">![Vamp in Universe (Universo) DC/OS](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="d66ed-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="d66ed-144">Fare clic su **installare** toohello Avanti vamp pacchetto e scegliere **installazione avanzata**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-144">Click **install** next toohello vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="d66ed-145">Scorrere verso il basso e immettere hello elasticsearch url seguente: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="d66ed-145">Scroll down and enter hello following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Immettere l'URL di Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="d66ed-147">Fare clic su **verifica e installa**, quindi fare clic su **installare** distribuzione hello toostart.</span><span class="sxs-lookup"><span data-stu-id="d66ed-147">Click **Review and Install**, then click **Install** toostart hello deployment.</span></span>  

  <span data-ttu-id="d66ed-148">DC/OS distribuisce tutti i componenti necessari di Vamp.</span><span class="sxs-lookup"><span data-stu-id="d66ed-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="d66ed-149">È possibile monitorare lo stato di avanzamento in hello **servizi** pagina.</span><span class="sxs-lookup"><span data-stu-id="d66ed-149">You can track progress on hello **Services** page.</span></span>
  
  ![Distribuire Vamp come pacchetto universo](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="d66ed-151">Una volta completata la distribuzione, è possibile accedere hello Vamp dell'interfaccia utente:</span><span class="sxs-lookup"><span data-stu-id="d66ed-151">Once deployment has completed, you can access hello Vamp UI:</span></span>

  ![Servizio Vamp su DC/OS](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Interfaccia utente di Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="d66ed-154">Distribuire il primo servizio</span><span class="sxs-lookup"><span data-stu-id="d66ed-154">Deploy your first service</span></span>

<span data-ttu-id="d66ed-155">Ora che Vamp è in esecuzione, è possibile distribuire un servizio da un progetto.</span><span class="sxs-lookup"><span data-stu-id="d66ed-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="d66ed-156">Nella sua forma più semplice, un [Vamp progetto](http://vamp.io/documentation/using-vamp/blueprints/) descrive gli endpoint hello (gateway), i cluster e toodeploy di servizi.</span><span class="sxs-lookup"><span data-stu-id="d66ed-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes hello endpoints (gateways), clusters, and services toodeploy.</span></span> <span data-ttu-id="d66ed-157">Vamp utilizza cluster toogroup diverse varianti di hello stesso servizio in gruppi logici per il rilascio canary o A / B test.</span><span class="sxs-lookup"><span data-stu-id="d66ed-157">Vamp uses clusters toogroup different variants of hello same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="d66ed-158">Questo scenario usa un'applicazione monolitica di esempio denominata [**sava**](https://github.com/magneticio/sava), che è alla versione 1.0.</span><span class="sxs-lookup"><span data-stu-id="d66ed-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="d66ed-159">monolito Hello viene compresso in un contenitore Docker, incluso nell'Hub Docker magneticio/sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="d66ed-159">hello monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="d66ed-160">applicazione Hello viene normalmente eseguito sulla porta 8080, ma si desidera tooexpose nella porta 9050 in questo caso.</span><span class="sxs-lookup"><span data-stu-id="d66ed-160">hello app normally runs on port 8080, but you want tooexpose it under port 9050 in this case.</span></span> <span data-ttu-id="d66ed-161">Distribuire app hello tramite Vamp utilizzando un progetto semplice.</span><span class="sxs-lookup"><span data-stu-id="d66ed-161">Deploy hello app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="d66ed-162">Andare troppo**distribuzioni**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-162">Go too**Deployments**.</span></span>

2. <span data-ttu-id="d66ed-163">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-163">Click **Add**.</span></span>

3. <span data-ttu-id="d66ed-164">Incolla in seguito hello cianografia YAML.</span><span class="sxs-lookup"><span data-stu-id="d66ed-164">Paste in hello following blueprint YAML.</span></span> <span data-ttu-id="d66ed-165">Questo progetto contiene un cluster con solo una variante di servizio, che verrà modificata in un passaggio successivo:</span><span class="sxs-lookup"><span data-stu-id="d66ed-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="d66ed-166">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-166">Click **Save**.</span></span> <span data-ttu-id="d66ed-167">Vamp Avvia distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="d66ed-167">Vamp initiates hello deployment.</span></span>

<span data-ttu-id="d66ed-168">distribuzione di Hello viene elencata in hello **distribuzioni** pagina.</span><span class="sxs-lookup"><span data-stu-id="d66ed-168">hello deployment is listed on hello **Deployments** page.</span></span> <span data-ttu-id="d66ed-169">Fare clic su hello distribuzione toomonitor il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="d66ed-169">Click hello deployment toomonitor its status.</span></span>

![Interfaccia utente Vamp: distribuzione sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![servizio sava nell'interfaccia utente di Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="d66ed-172">Vengono creati due gateway, che sono elencati nella hello **gateway** pagina:</span><span class="sxs-lookup"><span data-stu-id="d66ed-172">Two gateways are created, which are listed on hello **Gateways** page:</span></span>

* <span data-ttu-id="d66ed-173">un hello tooaccess stabile endpoint servizio (porta 9050)</span><span class="sxs-lookup"><span data-stu-id="d66ed-173">a stable endpoint tooaccess hello running service (port 9050)</span></span> 
* <span data-ttu-id="d66ed-174">un gateway interno gestito da Vamp, altre informazioni su questo gateway verranno date in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="d66ed-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Interfaccia utente di Vamp: gateway sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="d66ed-176">servizio sava Hello è ora distribuito, ma non è possibile accedervi esternamente perché hello bilanciamento del carico di Azure non riconosce tooforward traffico tooit ancora.</span><span class="sxs-lookup"><span data-stu-id="d66ed-176">hello sava service has now deployed, but you can’t access it externally because hello Azure Load Balancer doesn’t know tooforward traffic tooit yet.</span></span> <span data-ttu-id="d66ed-177">servizio di hello tooaccess, hello aggiornamento configurazione di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="d66ed-177">tooaccess hello service, update hello Azure networking configuration.</span></span>


## <a name="update-hello-azure-network-configuration"></a><span data-ttu-id="d66ed-178">Aggiornare la configurazione di rete di Azure hello</span><span class="sxs-lookup"><span data-stu-id="d66ed-178">Update hello Azure network configuration</span></span>

<span data-ttu-id="d66ed-179">Vamp servizio sava hello distribuito nei nodi di agente DC/OS hello, che espone un endpoint porta 9050 stabile.</span><span class="sxs-lookup"><span data-stu-id="d66ed-179">Vamp deployed hello sava service on hello DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="d66ed-180">servizio hello tooaccess dal cluster di controller di dominio/OS hello esterno, apportare hello seguente configurazione di rete di Azure toohello modifiche nella distribuzione di cluster:</span><span class="sxs-lookup"><span data-stu-id="d66ed-180">tooaccess hello service from outside hello DC/OS cluster, make hello following changes toohello Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="d66ed-181">**Configurare Bilanciamento carico di Azure hello** per gli agenti di hello (hello risorsa denominata **dcos-agente lb xxxx**) con un probe di integrità e il traffico sulla porta 9050 toohello sava a istanze tooforward una regola di.</span><span class="sxs-lookup"><span data-stu-id="d66ed-181">**Configure hello Azure Load Balancer** for hello agents (hello resource named **dcos-agent-lb-xxxx**) with a health probe and a rule tooforward traffic on port 9050 toohello sava instances.</span></span> 

2. <span data-ttu-id="d66ed-182">**Gruppo di sicurezza di rete hello aggiornamento** per gli agenti pubblica hello (hello risorsa denominata **XXXX-agent-public-gruppo-XXXX**) tooallow traffico sulla porta 9050.</span><span class="sxs-lookup"><span data-stu-id="d66ed-182">**Update hello network security group** for hello public agents (hello resource named **XXXX-agent-public-nsg-XXXX**) tooallow traffic on port 9050.</span></span>

<span data-ttu-id="d66ed-183">Per i passaggi dettagliati toocomplete queste operazioni usando hello Azure portale, vedere [abilitare l'applicazione del servizio di contenitore di Azure tooan accesso pubblico](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="d66ed-183">For detailed steps toocomplete these tasks using hello Azure portal, see [Enable public access tooan Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="d66ed-184">Specificare la porta 9050 per tutte le impostazioni della porta.</span><span class="sxs-lookup"><span data-stu-id="d66ed-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="d66ed-185">Una volta tutto ciò che è stato creato, andare toohello **Panoramica** blade di bilanciamento del carico di hello DC/OS agente (hello risorsa denominata **dcos-agente lb xxxx**).</span><span class="sxs-lookup"><span data-stu-id="d66ed-185">Once everything has been created, go toohello **Overview** blade of hello DC/OS agent load balancer (hello resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="d66ed-186">Trovare hello **indirizzo IP pubblico**e utilizzare hello indirizzo tooaccess sava porta 9050.</span><span class="sxs-lookup"><span data-stu-id="d66ed-186">Find hello **Public IP address**, and use hello address tooaccess sava at port 9050.</span></span>

![Portale di Azure: ottenere l'indirizzo IP pubblico](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="d66ed-189">Eseguire una versione canary</span><span class="sxs-lookup"><span data-stu-id="d66ed-189">Run a canary release</span></span>

<span data-ttu-id="d66ed-190">Si supponga di che avere una nuova versione dell'applicazione che si desidera toocanary versione nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d66ed-190">Suppose you have a new version of this application that you want toocanary release into production.</span></span> <span data-ttu-id="d66ed-191">È contenitore come magneticio/sava:1.1.0 e sono pronto toogo.</span><span class="sxs-lookup"><span data-stu-id="d66ed-191">You have it containerized as magneticio/sava:1.1.0 and are ready toogo.</span></span> <span data-ttu-id="d66ed-192">Vamp consente di aggiungere facilmente nuovi toohello servizi in esecuzione la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d66ed-192">Vamp lets you easily add new services toohello running deployment.</span></span> <span data-ttu-id="d66ed-193">Questi servizi "merge" vengono distribuiti insieme ai servizi esistenti di hello cluster hello e assegnati un peso pari a 0%.</span><span class="sxs-lookup"><span data-stu-id="d66ed-193">These "merged" services are deployed alongside hello existing services in hello cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="d66ed-194">Nessun traffico è tooa indirizzato appena unito servizio fino a quando non è regolare la distribuzione del traffico hello.</span><span class="sxs-lookup"><span data-stu-id="d66ed-194">No traffic is routed tooa newly merged service until you adjust hello traffic distribution.</span></span> <span data-ttu-id="d66ed-195">dispositivo di scorrimento peso Hello in hello Vamp UI offre controllo completo sulla distribuzione di hello, consentendo di modifiche incrementali (versione canary) o un rollback immediato.</span><span class="sxs-lookup"><span data-stu-id="d66ed-195">hello weight slider in hello Vamp UI gives you complete control over hello distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="d66ed-196">Unire una nuova variante di servizio</span><span class="sxs-lookup"><span data-stu-id="d66ed-196">Merge a new service variant</span></span>

<span data-ttu-id="d66ed-197">toomerge hello nuovo sava 1.1 servizio con hello in esecuzione la distribuzione:</span><span class="sxs-lookup"><span data-stu-id="d66ed-197">toomerge hello new sava 1.1 service with hello running deployment:</span></span>

1. <span data-ttu-id="d66ed-198">In hello Vamp dell'interfaccia utente, fare clic su **disegni**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-198">In hello Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="d66ed-199">Fare clic su **Aggiungi** e Incolla in seguito hello cianografia YAML: questo progetto viene descritto un nuovo toodeploy variant (sava: 1.1.0) di servizio all'interno di cluster esistente hello (sava_cluster).</span><span class="sxs-lookup"><span data-stu-id="d66ed-199">Click **Add** and paste in hello following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) toodeploy within hello existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. <span data-ttu-id="d66ed-200">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-200">Click **Save**.</span></span> <span data-ttu-id="d66ed-201">progetto iniziale di Hello viene archiviata ed elencato in hello **disegni** pagina.</span><span class="sxs-lookup"><span data-stu-id="d66ed-201">hello blueprint is stored and listed on hello **Blueprints** page.</span></span>

4. <span data-ttu-id="d66ed-202">Dal menu azione hello Apri progetto sava: 1.1 hello e fare clic su **di Merge per**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-202">Open hello action menu on hello sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Interfaccia utente di Vamp: progetti](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="d66ed-204">Seleziona hello **sava** distribuzione e fare clic su **Merge**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-204">Select hello **sava** deployment and click **Merge**.</span></span>

  ![Vamp dell'interfaccia utente - toodeployment progetto iniziale di tipo merge](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="d66ed-206">Vamp distribuisce hello nuovo sava: 1.1.0 variante servizio descritto nel progetto hello insieme sava: 1.0.0 in hello **sava_cluster** di hello in esecuzione la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d66ed-206">Vamp deploys hello new sava:1.1.0 service variant described in hello blueprint alongside sava:1.0.0 in hello **sava_cluster** of hello running deployment.</span></span> 

![Interfaccia utente di Vamp: distribuzione sava aggiornato](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="d66ed-208">Hello **sava_cluster/sava/webport** gateway (endpoint cluster hello) viene anche aggiornato, aggiunta di una route toohello appena distribuito sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="d66ed-208">hello **sava/sava_cluster/webport** gateway (hello cluster endpoint) is also updated, adding a route toohello newly deployed sava:1.1.0.</span></span> <span data-ttu-id="d66ed-209">A questo punto, nessun traffico viene indirizzato qui (hello **peso** è set % too0).</span><span class="sxs-lookup"><span data-stu-id="d66ed-209">At this point, no traffic is routed here (hello **WEIGHT** is set too0%).</span></span>

![Interfaccia utente di Vamp: gateway del cluster](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="d66ed-211">Versione canary</span><span class="sxs-lookup"><span data-stu-id="d66ed-211">Canary release</span></span>

<span data-ttu-id="d66ed-212">Entrambe le versioni di sava distribuito in hello stesso cluster, regolare hello distribuzione del traffico tra di essi spostando hello **peso** dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="d66ed-212">With both versions of sava deployed in hello same cluster, adjust hello distribution of traffic between them by moving hello **WEIGHT** slider.</span></span>

1. <span data-ttu-id="d66ed-213">Fare clic su ![Vamp dell'interfaccia utente - modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Avanti troppo**peso**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT**.</span></span>

2. <span data-ttu-id="d66ed-214">Hello peso distribuzione too50%/50% e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="d66ed-214">Set hello weight distribution too50%/50% and click **Save**.</span></span>

  ![Interfaccia utente di Vamp: dispositivo di scorrimento del peso del gateway](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="d66ed-216">Tornare indietro del browser tooyour e aggiornare pagina sava hello alcune altre volte.</span><span class="sxs-lookup"><span data-stu-id="d66ed-216">Go back tooyour browser and refresh hello sava page a few more times.</span></span> <span data-ttu-id="d66ed-217">un'applicazione sava Hello ora si passa dalla pagina sava: 1.0 e una pagina sava: 1.1.</span><span class="sxs-lookup"><span data-stu-id="d66ed-217">hello sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![alternanza dei servizi sava1.0 e sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="d66ed-219">L'alternanza della pagina hello funziona meglio con hello "Incognito" o "Anonimo" modalità del browser a causa di risorse statiche la memorizzazione nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="d66ed-219">This alternation of hello page works best with hello "Incognito" or “Anonymous” mode of your browser because of hello caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="d66ed-220">Filtrare il traffico</span><span class="sxs-lookup"><span data-stu-id="d66ed-220">Filter traffic</span></span>

<span data-ttu-id="d66ed-221">Si supponga che in seguito alla distribuzione sia stato individuato un problema di incompatibilità in sava:1.1.0 che causa problemi di visualizzazione nel browser Firefox.</span><span class="sxs-lookup"><span data-stu-id="d66ed-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="d66ed-222">È possibile impostare il traffico in entrata toofilter Vamp e indirizzare che tutti gli utenti di Firefox nuovamente toohello noto sava: 1.0.0 stabile.</span><span class="sxs-lookup"><span data-stu-id="d66ed-222">You can set Vamp toofilter incoming traffic and direct all Firefox users back toohello known stable sava:1.0.0.</span></span> <span data-ttu-id="d66ed-223">Questo filtro in modo istantaneo risolve hello interruzioni per gli utenti di Firefox, mentre qualsiasi altro utente continua hello vantaggi hello tooenjoy migliorate sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="d66ed-223">This filter instantly resolves hello disruption for Firefox users, while everybody else continues tooenjoy hello benefits of hello improved sava:1.1.0.</span></span>

<span data-ttu-id="d66ed-224">Usa vamp **condizioni** toofilter il traffico tra le route in un gateway.</span><span class="sxs-lookup"><span data-stu-id="d66ed-224">Vamp uses **conditions** toofilter traffic between routes in a gateway.</span></span> <span data-ttu-id="d66ed-225">Il traffico viene innanzitutto filtrato e indirizzati in base toohello condizioni applicate tooeach route.</span><span class="sxs-lookup"><span data-stu-id="d66ed-225">Traffic is first filtered and directed according toohello conditions applied tooeach route.</span></span> <span data-ttu-id="d66ed-226">Tutto il traffico rimanente viene distribuito in base a impostazioni del peso toohello gateway.</span><span class="sxs-lookup"><span data-stu-id="d66ed-226">All remaining traffic is distributed according toohello gateway weight setting.</span></span>

<span data-ttu-id="d66ed-227">È possibile creare una condizione toofilter tutti gli utenti di Firefox e invita toohello precedente sava: 1.0.0:</span><span class="sxs-lookup"><span data-stu-id="d66ed-227">You can create a condition toofilter all Firefox users and direct them toohello old sava:1.0.0:</span></span>

1. <span data-ttu-id="d66ed-228">In hello sava/sava_cluster/webport **gateway** pagina, fare clic su ![Vamp dell'interfaccia utente - modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd un **condizione** toohello route sava/sava_cluster/sava:1.0.0/webport.</span><span class="sxs-lookup"><span data-stu-id="d66ed-228">On hello sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd a **CONDITION** toohello route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="d66ed-229">Immettere una condizione di hello **agente utente = = Firefox** e fare clic su ![Vamp dell'interfaccia utente - Salva](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="d66ed-229">Enter hello condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="d66ed-230">Vamp aggiunge condizione hello con un livello di attendibilità predefinito pari a 0%.</span><span class="sxs-lookup"><span data-stu-id="d66ed-230">Vamp adds hello condition with a default strength of 0%.</span></span> <span data-ttu-id="d66ed-231">toostart filtrando il traffico, è necessario livello di condizione tooadjust hello.</span><span class="sxs-lookup"><span data-stu-id="d66ed-231">toostart filtering traffic, you need tooadjust hello condition strength.</span></span>

3. <span data-ttu-id="d66ed-232">Fare clic su ![Vamp dell'interfaccia utente - modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **forza** toohello condizione applicata.</span><span class="sxs-lookup"><span data-stu-id="d66ed-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **STRENGTH** applied toohello condition.</span></span>
 
4. <span data-ttu-id="d66ed-233">Set hello **forza** too100% e fare clic su ![Vamp dell'interfaccia utente - Salva](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span><span class="sxs-lookup"><span data-stu-id="d66ed-233">Set hello **STRENGTH** too100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span></span>

  <span data-ttu-id="d66ed-234">Vamp ora invia tutto il traffico corrispondente hello condizione (tutti gli utenti Firefox) toosava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="d66ed-234">Vamp now sends all traffic matching hello condition (all Firefox users) toosava:1.0.0.</span></span>

  ![Vamp dell'interfaccia utente - applicare toogateway condizione](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="d66ed-236">Infine, regolare hello gateway peso toosend tutti i rimanenti traffico (tutti gli utenti non Firefox) toohello nuova sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="d66ed-236">Finally, adjust hello gateway weight toosend all remaining traffic (all non-Firefox users) toohello new sava:1.1.0.</span></span> <span data-ttu-id="d66ed-237">Fare clic su ![Vamp dell'interfaccia utente - modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Avanti troppo**peso** e impostare distribuzione del peso hello in modo diretto toohello route sava/sava_cluster/sava:1.1.0/webport di è 100%.</span><span class="sxs-lookup"><span data-stu-id="d66ed-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT** and set hello weight distribution so 100% is directed toohello route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="d66ed-238">Tutto il traffico non filtrato condizione hello è diretto toohello nuova sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="d66ed-238">All traffic not filtered by hello condition is now directed toohello new sava:1.1.0.</span></span>

6. <span data-ttu-id="d66ed-239">filtro hello toosee in azione, aprire due diversi browser (uno Firefox e un altro browser) e accedere hello sava servizio da entrambi.</span><span class="sxs-lookup"><span data-stu-id="d66ed-239">toosee hello filter in action, open two different browsers (one Firefox and one other browser) and access hello sava service from both.</span></span> <span data-ttu-id="d66ed-240">Tutte le richieste di Firefox vengono inviate toosava:1.0.0, mentre tutti gli altri browser sono toosava:1.1.0 diretto.</span><span class="sxs-lookup"><span data-stu-id="d66ed-240">All Firefox requests are sent toosava:1.0.0, while all other browsers are directed toosava:1.1.0.</span></span>

  ![Interfaccia utente di Vamp: filtrare il traffico](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="d66ed-242">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="d66ed-242">Summing up</span></span>

<span data-ttu-id="d66ed-243">Questo articolo è stato tooVamp una rapida introduzione in un cluster di controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d66ed-243">This article was a quick introduction tooVamp on a DC/OS cluster.</span></span> <span data-ttu-id="d66ed-244">Per iniziare, ottenuto Vamp e in esecuzione in Azure contenitore del servizio controller di dominio o sistema operativo cluster, distribuito un servizio con un progetto iniziale Vamp e vi ha avuto accesso all'endpoint esposto hello (gateway).</span><span class="sxs-lookup"><span data-stu-id="d66ed-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at hello exposed endpoint (gateway).</span></span>

<span data-ttu-id="d66ed-245">È inoltre stata presa in considerazione alcune potenti funzionalità di Vamp: unione di un nuovo toohello variant di servizio in esecuzione la distribuzione e introducendo in modo incrementale, quindi filtrare il traffico tooresolve un'incompatibilità nota.</span><span class="sxs-lookup"><span data-stu-id="d66ed-245">We also touched on some powerful features of Vamp:  merging a new service variant toohello running deployment and introducing it incrementally, then filtering traffic tooresolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d66ed-246">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d66ed-246">Next steps</span></span>

* <span data-ttu-id="d66ed-247">Informazioni sulla gestione delle azioni Vamp tramite hello [Vamp API REST](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="d66ed-247">Learn about managing Vamp actions through hello [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="d66ed-248">Creazione di script di automazione Vamp in Node.js ed esecuzione degli stessi come [flussi di lavoro di Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="d66ed-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="d66ed-249">Vedere altre [esercitazioni su Vamp](http://vamp.io/documentation/tutorials/overview/).</span><span class="sxs-lookup"><span data-stu-id="d66ed-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

