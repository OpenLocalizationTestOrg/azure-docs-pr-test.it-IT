---
title: un cluster di controller di dominio o sistema operativo di Azure - stack ELK aaaMonitor | Documenti Microsoft
description: Monitorare un cluster DC/OS nel cluster del servizio contenitore di Azure con ELK (Elasticsearch, Logstash e Kibana).
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Contenitori, DC/OS, Azure, monitoraggio, ELK
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="45803-104">Monitorare un cluster del servizio contenitore di Azure con ELK</span><span class="sxs-lookup"><span data-stu-id="45803-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="45803-105">In questo articolo viene illustrato come stack di chiamate toodeploy hello ELK (Elasticsearch, Logstash, Kibana) su un cluster di controller di dominio o del sistema operativo contenitore nel servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="45803-105">In this article, we demonstrate how toodeploy hello ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="45803-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="45803-106">Prerequisites</span></span>
<span data-ttu-id="45803-107">[Distribuire](container-service-deployment.md) e [connettere](../container-service-connect.md) un cluster DC/OS configurato dal servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="45803-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="45803-108">Esplorare il dashboard di controller di dominio/OS hello e servizi maratona [qui](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="45803-108">Explore hello DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="45803-109">Installare anche hello [bilanciamento del carico maratona](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="45803-109">Also install hello [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="45803-110">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="45803-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="45803-111">Stack ELK è una combinazione di Elasticsearch, Logstash, Kibana che fornisce uno stack tooend end che può essere utilizzati toomonitor e analizzare i log del cluster.</span><span class="sxs-lookup"><span data-stu-id="45803-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end tooend stack that can be used toomonitor and analyze logs in your cluster.</span></span>

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="45803-112">Configurare stack ELK hello in un cluster di controller di dominio o del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="45803-112">Configure hello ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="45803-113">Accedere all'interfaccia del controller di dominio o del sistema operativo tramite [http://localhost:80 /](http://localhost:80/) una volta nell'interfaccia utente di controller di dominio/OS passare troppo hello**universo**.</span><span class="sxs-lookup"><span data-stu-id="45803-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate too**Universe**.</span></span> <span data-ttu-id="45803-114">Cercare e installare Elasticsearch Logstash e Kibana da hello l'universo dei controller di dominio o del sistema operativo e in tale ordine specifico.</span><span class="sxs-lookup"><span data-stu-id="45803-114">Search and install Elasticsearch, Logstash, and Kibana from hello DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="45803-115">Ulteriori informazioni sulla configurazione se si passa toohello **installazione avanzata** collegamento.</span><span class="sxs-lookup"><span data-stu-id="45803-115">You can learn more about configuration if you go toohello **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="45803-119">Una volta hello contenitori ELK e vengono aggiornato e in esecuzione, è necessario tooenable Kibana toobe tramite maratona LB.</span><span class="sxs-lookup"><span data-stu-id="45803-119">Once hello ELK containers and are up and running, you need tooenable Kibana toobe accessed through Marathon-LB.</span></span> <span data-ttu-id="45803-120">Passare troppo **servizi** > **kibana**, fare clic su **modifica** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="45803-120">Navigate too **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="45803-122">Attivare o disattivare troppo**modalità JSON** e scorrere verso il basso sezione etichette toohello.</span><span class="sxs-lookup"><span data-stu-id="45803-122">Toggle too**JSON mode** and scroll down toohello labels section.</span></span>
<span data-ttu-id="45803-123">È necessario tooadd un `"HAPROXY_GROUP": "external"` voce qui come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="45803-123">You need tooadd a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="45803-124">Dopo avere fatto clic su **Distribuisci modifiche**, il contenitore viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="45803-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="45803-126">Se si desidera tooverify che Kibana viene registrato come un servizio nel dashboard HAPROXY hello, è necessario che sia tooopen porta 9090 nel cluster agente hello HAPROXY eseguita sulla porta 9090.</span><span class="sxs-lookup"><span data-stu-id="45803-126">If you want tooverify that Kibana is registered as a service in hello HAPROXY dashboard, you need tooopen port 9090 on hello agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="45803-127">Per impostazione predefinita, si apre le porte 80, 8080 e 443 in hello cluster agente controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="45803-127">By default, we open ports 80, 8080, and 443 in hello DC/OS agent cluster.</span></span>
<span data-ttu-id="45803-128">Istruzioni tooopen una porta e fornire pubblico valutare forniti [qui](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="45803-128">Instructions tooopen a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="45803-129">tooaccess hello dashboard dell'interfaccia di amministrazione aprire hello maratona LB in HAPROXY: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="45803-129">tooaccess hello HAPROXY dashboard, open hello Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="45803-130">Quando ci si sposta toohello URL, dashboard HAPROXY hello verrà visualizzato come illustrato di seguito, viene visualizzata una voce di servizio per Kibana.</span><span class="sxs-lookup"><span data-stu-id="45803-130">Once you navigate toohello URL, you should see hello HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="45803-132">tooaccess hello Kibana dashboard in cui viene distribuito sulla porta 5601, è necessario tooopen porta 5601.</span><span class="sxs-lookup"><span data-stu-id="45803-132">tooaccess hello Kibana dashboard, which is deployed on port 5601, you need tooopen port 5601.</span></span> <span data-ttu-id="45803-133">Seguire le istruzioni [qui](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="45803-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="45803-134">Quindi aprire il dashboard Kibana hello in: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="45803-134">Then open hello Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45803-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45803-135">Next steps</span></span>

* <span data-ttu-id="45803-136">Per l'inoltro e la configurazione del log di sistema e dell'applicazione, vedere [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Gestione log nel controller di dominio o sistema operativo con ELK).</span><span class="sxs-lookup"><span data-stu-id="45803-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="45803-137">vedere i log toofilter, [registri dei filtri con ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="45803-137">toofilter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

