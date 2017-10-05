---
title: Monitorare cluster DC/OS di Azure - Datadog | Documentazione Microsoft
description: Monitorare un cluster del servizio contenitore di Azure con Datadog. Usare l'interfaccia utente Web del controller di dominio/sistema operativo per distribuire gli agenti Datadog al cluster.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenitori, controller di dominio/sistema operativo, Docker Swarm, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 9dd451f994940d7cc3a59bd7fd08a8f067345e34
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="02cc6-105">Monitorare un cluster DC/OS del servizio contenitore di Azure con Datadog</span><span class="sxs-lookup"><span data-stu-id="02cc6-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="02cc6-106">In questo articolo verranno distribuiti agenti di Datadog in tutti i nodi agente nel cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="02cc6-106">In this article we will deploy Datadog agents to all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="02cc6-107">Per questa configurazione, sarà necessario un account con Datadog.</span><span class="sxs-lookup"><span data-stu-id="02cc6-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="02cc6-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="02cc6-108">Prerequisites</span></span>
<span data-ttu-id="02cc6-109">[Distribuire](container-service-deployment.md) e [connettere](../container-service-connect.md) un cluster configurato dal servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="02cc6-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="02cc6-110">Esplorare l' [interfaccia utente](container-service-mesos-marathon-ui.md)di Marathon.</span><span class="sxs-lookup"><span data-stu-id="02cc6-110">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="02cc6-111">Andare a [http://datadoghq.com](http://datadoghq.com) per configurare un account Datadog.</span><span class="sxs-lookup"><span data-stu-id="02cc6-111">Go to [http://datadoghq.com](http://datadoghq.com) to set up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="02cc6-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="02cc6-112">Datadog</span></span>
<span data-ttu-id="02cc6-113">Datadog è un servizio che raccoglie dati di monitoraggio dai contenitori all'interno del cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="02cc6-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="02cc6-114">Datadog è dotato di un dashboard di integrazione Docker in cui è possibile visualizzare metriche specifiche all'interno dei propri contenitori.</span><span class="sxs-lookup"><span data-stu-id="02cc6-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="02cc6-115">Le metriche raccolte dai contenitori sono organizzate per CPU, memoria, rete e I/O.</span><span class="sxs-lookup"><span data-stu-id="02cc6-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="02cc6-116">Datadog suddivide le metriche in contenitori e immagini.</span><span class="sxs-lookup"><span data-stu-id="02cc6-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="02cc6-117">Un esempio dell'aspetto dell'interfaccia utente per l'utilizzo della CPU è riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="02cc6-117">An example of what the UI looks like for CPU usage is below.</span></span>

![Interfaccia utente Datadog](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="02cc6-119">Configurare una distribuzione Datadog con Marathon</span><span class="sxs-lookup"><span data-stu-id="02cc6-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="02cc6-120">Questi passaggi illustrano come configurare e distribuire le applicazioni Datadog nel cluster con Marathon.</span><span class="sxs-lookup"><span data-stu-id="02cc6-120">These steps will show you how to configure and deploy Datadog applications to your cluster with Marathon.</span></span> 

<span data-ttu-id="02cc6-121">Accedere all'interfaccia utente del controller di dominio/sistema operativo da [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="02cc6-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="02cc6-122">Dall'interfaccia utente del controller di dominio/sistema operativo passare a "Universe" ("Universo") in basso a sinistra e quindi cercare "Datadog" e fare clic su "Install".</span><span class="sxs-lookup"><span data-stu-id="02cc6-122">Once in the DC/OS UI navigate to the "Universe" which is on the bottom left and then search for "Datadog" and click "Install."</span></span>

![Pacchetto Datadog in Universe (Universo) per il controller di dominio/sistema operativo](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="02cc6-124">Per completare la configurazione, sarà necessario un account cloud Datadog o un account di valutazione gratuita.</span><span class="sxs-lookup"><span data-stu-id="02cc6-124">Now to complete the configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="02cc6-125">Dopo aver eseguito l'accesso al sito Web di Datadog, a sinistra passare a Integrations (Integrazioni) -> [APIs](https://app.datadoghq.com/account/settings#api) (API).</span><span class="sxs-lookup"><span data-stu-id="02cc6-125">Once you're logged in to the Datadog website look to the left and go to Integrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Chiave API di Datadog](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="02cc6-127">Immettere quindi la chiave API nella configurazione di Datadog in Universe (Universo) per il controller di dominio/sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="02cc6-127">Next enter your API key into the Datadog configuration within the DC/OS Universe.</span></span> 

![Configurazione di Datadog in Universe (Universo) per il controller di dominio/sistema operativo](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="02cc6-129">Nella configurazione precedente le istanze sono impostate su 10000000 in modo che quando viene aggiunto un nuovo nodo al cluster Datadog distribuirà automaticamente un agente in tale nodo.</span><span class="sxs-lookup"><span data-stu-id="02cc6-129">In the above configuration instances are set to 10000000 so whenever a new node is added to the cluster Datadog will automatically deploy an agent to that node.</span></span> <span data-ttu-id="02cc6-130">Si tratta di una soluzione temporanea.</span><span class="sxs-lookup"><span data-stu-id="02cc6-130">This is an interim solution.</span></span> <span data-ttu-id="02cc6-131">Dopo aver installato il pacchetto si dovrebbe tornare al sito Web Datadog e cercare "[Dashboards](https://app.datadoghq.com/dash/list)" (Dashboard).</span><span class="sxs-lookup"><span data-stu-id="02cc6-131">Once you've installed the package you should navigate back to the Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="02cc6-132">Da qui si vedrà Custom and Integration Dashboards.</span><span class="sxs-lookup"><span data-stu-id="02cc6-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="02cc6-133">Il [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) (Dashboard Docker) conterrà tutte le metriche del contenitore necessarie per il monitoraggio del cluster.</span><span class="sxs-lookup"><span data-stu-id="02cc6-133">The [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all the container metrics you need for monitoring your cluster.</span></span> 

