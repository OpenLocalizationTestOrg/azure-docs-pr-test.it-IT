---
title: cluster di controller di dominio o sistema operativo Azure aaaMonitor - Datadog | Documenti Microsoft
description: Monitorare un cluster del servizio contenitore di Azure con Datadog. Utilizzare hello controller di dominio o del sistema operativo dell'interfaccia utente toodeploy hello Datadog agenti tooyour cluster web.
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
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="8074c-105">Monitorare un cluster DC/OS del servizio contenitore di Azure con Datadog</span><span class="sxs-lookup"><span data-stu-id="8074c-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="8074c-106">In questo articolo si distribuirà Datadog agenti tooall hello agente i nodi del cluster del servizio di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="8074c-106">In this article we will deploy Datadog agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="8074c-107">Per questa configurazione, sarà necessario un account con Datadog.</span><span class="sxs-lookup"><span data-stu-id="8074c-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8074c-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8074c-108">Prerequisites</span></span>
<span data-ttu-id="8074c-109">[Distribuire](container-service-deployment.md) e [connettere](../container-service-connect.md) un cluster configurato dal servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="8074c-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="8074c-110">Esplorare hello [dell'interfaccia utente maratona](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="8074c-110">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="8074c-111">Andare troppo[http://datadoghq.com](http://datadoghq.com) tooset Datadog conto.</span><span class="sxs-lookup"><span data-stu-id="8074c-111">Go too[http://datadoghq.com](http://datadoghq.com) tooset up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="8074c-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="8074c-112">Datadog</span></span>
<span data-ttu-id="8074c-113">Datadog è un servizio che raccoglie dati di monitoraggio dai contenitori all'interno del cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="8074c-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="8074c-114">Datadog è dotato di un dashboard di integrazione Docker in cui è possibile visualizzare metriche specifiche all'interno dei propri contenitori.</span><span class="sxs-lookup"><span data-stu-id="8074c-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="8074c-115">Le metriche raccolte dai contenitori sono organizzate per CPU, memoria, rete e I/O.</span><span class="sxs-lookup"><span data-stu-id="8074c-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="8074c-116">Datadog suddivide le metriche in contenitori e immagini.</span><span class="sxs-lookup"><span data-stu-id="8074c-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="8074c-117">Un esempio di quali hello dell'interfaccia utente sembra che per la CPU è di sotto l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="8074c-117">An example of what hello UI looks like for CPU usage is below.</span></span>

![Interfaccia utente Datadog](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="8074c-119">Configurare una distribuzione Datadog con Marathon</span><span class="sxs-lookup"><span data-stu-id="8074c-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="8074c-120">Questa procedura viene illustrato come tooconfigure e la distribuzione Datadog applicazioni tooyour cluster con maratona.</span><span class="sxs-lookup"><span data-stu-id="8074c-120">These steps will show you how tooconfigure and deploy Datadog applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="8074c-121">Accedere all'interfaccia utente del controller di dominio/sistema operativo da [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="8074c-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="8074c-122">Una volta nell'interfaccia utente di controller di dominio/OS passare hello toohello "Universo" che si trova in hello in basso a sinistra e quindi cercare "Datadog" e fare clic su "Installa".</span><span class="sxs-lookup"><span data-stu-id="8074c-122">Once in hello DC/OS UI navigate toohello "Universe" which is on hello bottom left and then search for "Datadog" and click "Install."</span></span>

![Pacchetto Datadog all'interno di hello l'universo dei controller di dominio o del sistema operativo](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="8074c-124">Ora toocomplete hello configurazione sarà necessario un account Datadog o un account di prova.</span><span class="sxs-lookup"><span data-stu-id="8074c-124">Now toocomplete hello configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="8074c-125">Dopo aver eseguito il nel sito Web Datadog toohello cercare toohello sinistra e passare tooIntegrations -> quindi [API](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="8074c-125">Once you're logged in toohello Datadog website look toohello left and go tooIntegrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Chiave API di Datadog](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="8074c-127">Quindi immettere la chiave API in configurazione Datadog hello all'interno di hello l'universo dei controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="8074c-127">Next enter your API key into hello Datadog configuration within hello DC/OS Universe.</span></span> 

![Configurazione Datadog in hello l'universo dei controller di dominio o del sistema operativo](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="8074c-129">In hello sopra configurazione istanze sono impostate too10000000 pertanto ogni volta che viene aggiunto un nuovo nodo cluster toohello Datadog distribuirà automaticamente un nodo toothat agente.</span><span class="sxs-lookup"><span data-stu-id="8074c-129">In hello above configuration instances are set too10000000 so whenever a new node is added toohello cluster Datadog will automatically deploy an agent toothat node.</span></span> <span data-ttu-id="8074c-130">Si tratta di una soluzione temporanea.</span><span class="sxs-lookup"><span data-stu-id="8074c-130">This is an interim solution.</span></span> <span data-ttu-id="8074c-131">Dopo aver installato il pacchetto di hello si deve passare sito Web Datadog toohello indietro e si trova "[dashboard](https://app.datadoghq.com/dash/list)."</span><span class="sxs-lookup"><span data-stu-id="8074c-131">Once you've installed hello package you should navigate back toohello Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="8074c-132">Da qui si vedrà Custom and Integration Dashboards.</span><span class="sxs-lookup"><span data-stu-id="8074c-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="8074c-133">Hello [dashboard Docker](https://app.datadoghq.com/screen/integration/docker) disporrà di tutte le metriche di contenitore hello è necessario per il monitoraggio del cluster.</span><span class="sxs-lookup"><span data-stu-id="8074c-133">hello [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all hello container metrics you need for monitoring your cluster.</span></span> 

