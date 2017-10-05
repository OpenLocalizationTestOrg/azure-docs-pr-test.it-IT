---
title: Monitorare cluster DC/OS di Azure - Dynatrace | Documentazione Microsoft
description: Monitorare un cluster DC/OS del servizio contenitore di Azure con Dynatrace. Distribuire Dynatrace OneAgent tramite il dashboard di DC/OS.
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: Contenitori, controller di dominio/sistema operativo, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 6fa23728680779e33eda7bb9aa8a01b9cad9a82b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="6cab9-105">Monitorare un cluster DC/OS del servizio contenitore di Azure con Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="6cab9-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="6cab9-106">Questo articolo mostra come distribuire [Dynatrace](https://www.dynatrace.com/) OneAgent per monitorare tutti i nodi dell'agente nel cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cab9-106">In this article, we show you how to deploy the [Dynatrace](https://www.dynatrace.com/) OneAgent to monitor all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="6cab9-107">Per questa configurazione, è necessario un account con Dynatrace SaaS/Managed.</span><span class="sxs-lookup"><span data-stu-id="6cab9-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="6cab9-108">Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="6cab9-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="6cab9-109">Dynatrace è una soluzione di monitoraggio nativa del cloud per gli ambienti cluster e dei contenitori altamente dinamici.</span><span class="sxs-lookup"><span data-stu-id="6cab9-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="6cab9-110">Consente di ottimizzare le distribuzioni dei contenitori e le allocazioni di memoria usando i dati di utilizzo in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="6cab9-110">It allows you to better optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="6cab9-111">È in grado di individuare automaticamente problemi a livello di applicazioni e infrastruttura fornendo una baseline automatizzata, oltre alla correlazione dei problemi e al rilevamento delle cause principali.</span><span class="sxs-lookup"><span data-stu-id="6cab9-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="6cab9-112">La figura seguente mostra l'interfaccia utente di Dynatrace:</span><span class="sxs-lookup"><span data-stu-id="6cab9-112">The following figure shows the Dynatrace UI:</span></span>

![Interfaccia utente di Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="6cab9-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6cab9-114">Prerequisites</span></span> 
<span data-ttu-id="6cab9-115">[Distribuire](container-service-deployment.md) ed [eseguire la connessione](./../container-service-connect.md) a un cluster configurato dal servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cab9-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) to a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="6cab9-116">Esplorare l' [interfaccia utente](container-service-mesos-marathon-ui.md)di Marathon.</span><span class="sxs-lookup"><span data-stu-id="6cab9-116">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="6cab9-117">Passare a [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) per configurare un account Dynatrace SaaS.</span><span class="sxs-lookup"><span data-stu-id="6cab9-117">Go to [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) to set up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="6cab9-118">Configurare una distribuzione Dynatrace con Marathon</span><span class="sxs-lookup"><span data-stu-id="6cab9-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="6cab9-119">Questi passaggi illustrano come configurare e distribuire le applicazioni Dynatrace nel cluster con Marathon.</span><span class="sxs-lookup"><span data-stu-id="6cab9-119">These steps show you how to configure and deploy Dynatrace applications to your cluster with Marathon.</span></span>

1. <span data-ttu-id="6cab9-120">Accedere all'interfaccia utente del controller di dominio/sistema operativo da [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="6cab9-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="6cab9-121">Una volta nell'interfaccia utente di DC/OS, passare alla scheda **Universe** (Universo) e quindi cercare **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="6cab9-121">Once in the DC/OS UI, navigate to the **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace in Universe (Universo) di DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="6cab9-123">Per completare la configurazione, è necessario un account Dynatrace SaaS o un account di prova gratuito.</span><span class="sxs-lookup"><span data-stu-id="6cab9-123">To complete the configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="6cab9-124">Dopo avere eseguito l'accesso al dashboard di Dynatrace, selezionare **Deploy Dynatrace** (Distribuisci Dynatrace).</span><span class="sxs-lookup"><span data-stu-id="6cab9-124">Once you log into the Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Dynatrace - Set up PaaS integration (Configura integrazione Paas)](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="6cab9-126">Nella pagina selezionare **Set up PaaS integration** (Configura integrazione Paas).</span><span class="sxs-lookup"><span data-stu-id="6cab9-126">On the page, select **Set up PaaS integration**.</span></span> 

    ![Token API di Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="6cab9-128">Immettere il token API nella configurazione di Dynatrace OneAgent in Universe (Universo) di DC/OS.</span><span class="sxs-lookup"><span data-stu-id="6cab9-128">Enter your API token into the Dynatrace OneAgent configuration within the DC/OS Universe.</span></span> 

    ![Configurazione di Dynatrace OneAgent in Universe (Universo) di DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="6cab9-130">Impostare le istanze sul numero di nodi che si intende eseguire.</span><span class="sxs-lookup"><span data-stu-id="6cab9-130">Set the instances to the number of nodes you intend to run.</span></span> <span data-ttu-id="6cab9-131">È anche possibile impostare un numero superiore, ma DC/OS tenterà di trovare nuove istanze finché tale numero non viene effettivamente raggiunto.</span><span class="sxs-lookup"><span data-stu-id="6cab9-131">Setting a higher number also works, but DC/OS will keep trying to find new instances until that number is actually reached.</span></span> <span data-ttu-id="6cab9-132">Se si preferisce, è possibile impostarlo su un valore come 1000000.</span><span class="sxs-lookup"><span data-stu-id="6cab9-132">If you prefer, you can also set this to a value like 1000000.</span></span> <span data-ttu-id="6cab9-133">In questo caso, ogni volta che viene aggiunto un nuovo nodo al cluster, Dynatrace distribuisce automaticamente un agente per il nuovo nodo, ma DC/OS tenterà costantemente di distribuire altre istanze.</span><span class="sxs-lookup"><span data-stu-id="6cab9-133">In this case, whenever a new node is added to the cluster, Dynatrace automatically deploys an agent to that new node, at the price of DC/OS constantly trying to deploy further instances.</span></span>

    ![Configurazione di Dynatrace nelle istanze di Universe (Universo) di DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="6cab9-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6cab9-135">Next steps</span></span>

<span data-ttu-id="6cab9-136">Dopo avere installato il pacchetto, tornare al dashboard di Dynatrace.</span><span class="sxs-lookup"><span data-stu-id="6cab9-136">Once you've installed the package, navigate back to the Dynatrace dashboard.</span></span> <span data-ttu-id="6cab9-137">È possibile esplorare le diverse metriche di utilizzo per i contenitori all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="6cab9-137">You can explore the different usage metrics for the containers within your cluster.</span></span> 