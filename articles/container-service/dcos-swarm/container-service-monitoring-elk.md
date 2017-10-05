---
title: Monitorare un cluster DC/OS di Azure - Stack ELK | Documentazione Microsoft
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
ms.openlocfilehash: fcfa277cdd0f3cebc0fbbb23e771fb23ffbe2ca6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="9e64a-104">Monitorare un cluster del servizio contenitore di Azure con ELK</span><span class="sxs-lookup"><span data-stu-id="9e64a-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="9e64a-105">Questo articolo descrive come distribuire lo stack ELK (Elasticsearch, Logstash, Kibana) in un cluster DC/OS nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e64a-105">In this article, we demonstrate how to deploy the ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9e64a-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9e64a-106">Prerequisites</span></span>
<span data-ttu-id="9e64a-107">[Distribuire](container-service-deployment.md) e [connettere](../container-service-connect.md) un cluster DC/OS configurato dal servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e64a-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="9e64a-108">Esplorare il dashboard di DC/OS e i servizi Marathon [qui](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="9e64a-108">Explore the DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="9e64a-109">Installare anche il [servizio di bilanciamento del carico Marathon](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="9e64a-109">Also install the [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="9e64a-110">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="9e64a-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="9e64a-111">Lo stack ELK, una combinazione di Elasticsearch, Logstash e Kibana, fornisce uno stack end-to-end che può essere usato per monitorare e analizzare i log nel cluster.</span><span class="sxs-lookup"><span data-stu-id="9e64a-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end to end stack that can be used to monitor and analyze logs in your cluster.</span></span>

## <a name="configure-the-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="9e64a-112">Configurare lo stack ELK in un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="9e64a-112">Configure the ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="9e64a-113">Accedere all'interfaccia utente di DC/OS usando [http://localhost:80/](http://localhost:80/) Nell'interfaccia utente di DC/OS passare a **Universe**.</span><span class="sxs-lookup"><span data-stu-id="9e64a-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to **Universe**.</span></span> <span data-ttu-id="9e64a-114">Cercare e installare Elasticsearch, Logstash e Kibana da DC/OS Universe in questo ordine specifico.</span><span class="sxs-lookup"><span data-stu-id="9e64a-114">Search and install Elasticsearch, Logstash, and Kibana from the DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="9e64a-115">Altre informazioni sulla configurazione sono disponibili nel collegamento relativo all'**installazione avanzata**.</span><span class="sxs-lookup"><span data-stu-id="9e64a-115">You can learn more about configuration if you go to the **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="9e64a-119">Dopo che i contenitori ELK sono attivi, è necessario abilitare l'accesso a Kibana tramite Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="9e64a-119">Once the ELK containers and are up and running, you need to enable Kibana to be accessed through Marathon-LB.</span></span> <span data-ttu-id="9e64a-120">Passare a **Servizi** > **kibana** e fare clic su **Modifica**, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9e64a-120">Navigate to **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="9e64a-122">Passare alla **modalità JSON** ed eseguire lo scorrimento fino alla sezione relativa alle etichette.</span><span class="sxs-lookup"><span data-stu-id="9e64a-122">Toggle to **JSON mode** and scroll down to the labels section.</span></span>
<span data-ttu-id="9e64a-123">È necessario aggiungere una voce `"HAPROXY_GROUP": "external"` qui, come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9e64a-123">You need to add a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="9e64a-124">Dopo avere fatto clic su **Distribuisci modifiche**, il contenitore viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="9e64a-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="9e64a-126">Se si vuole verificare che Kibana sia registrato come servizio nel dashboard di HAPROXY, è necessario aprire la porta 9090 nel cluster agente poiché HAPROXY viene eseguito in questa porta.</span><span class="sxs-lookup"><span data-stu-id="9e64a-126">If you want to verify that Kibana is registered as a service in the HAPROXY dashboard, you need to open port 9090 on the agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="9e64a-127">Per impostazione predefinita vengono aperte le porte 80, 8080 e 443 nel cluster agente DC/OS.</span><span class="sxs-lookup"><span data-stu-id="9e64a-127">By default, we open ports 80, 8080, and 443 in the DC/OS agent cluster.</span></span>
<span data-ttu-id="9e64a-128">Istruzioni su come aprire una porta e fornire l'accesso pubblico sono disponibili [qui](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="9e64a-128">Instructions to open a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="9e64a-129">Per accedere al dashboard di HAPROXY, aprire l'interfaccia di amministrazione di Marathon LB all'indirizzo: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="9e64a-129">To access the HAPROXY dashboard, open the Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="9e64a-130">Quando si passa all'URL, verrà visualizzato il dashboard di HAPROXY come illustrato di seguito e verrà visualizzata una voce del servizio per Kibana.</span><span class="sxs-lookup"><span data-stu-id="9e64a-130">Once you navigate to the URL, you should see the HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="9e64a-132">Per accedere al dashboard di Kibana distribuito nella porta 5601, è necessario aprire la porta 5601.</span><span class="sxs-lookup"><span data-stu-id="9e64a-132">To access the Kibana dashboard, which is deployed on port 5601, you need to open port 5601.</span></span> <span data-ttu-id="9e64a-133">Seguire le istruzioni [qui](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="9e64a-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="9e64a-134">Aprire quindi il dashboard di Kibana all'indirizzo: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="9e64a-134">Then open the Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e64a-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9e64a-135">Next steps</span></span>

* <span data-ttu-id="9e64a-136">Per l'inoltro e la configurazione del log di sistema e dell'applicazione, vedere [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Gestione log nel controller di dominio o sistema operativo con ELK).</span><span class="sxs-lookup"><span data-stu-id="9e64a-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="9e64a-137">Per filtrare i log, vedere [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/) (Filtrare i log con ELK).</span><span class="sxs-lookup"><span data-stu-id="9e64a-137">To filter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

