---
title: Monitorare un cluster del servizio contenitore di Azure con Sysdig | Documentazione Microsoft
description: Monitorare un cluster del servizio contenitore di Azure con Sysdig.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenitori, controller di dominio/sistema operativo, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: e61001161e632a5d2e513107e30f1eaf06103989
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="618fd-104">Monitorare un cluster del servizio contenitore di Azure con Sysdig</span><span class="sxs-lookup"><span data-stu-id="618fd-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="618fd-105">In questo articolo verranno distribuiti agenti di Sysdig in tutti i nodi agente nel cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="618fd-105">In this article, we will deploy Sysdig agents to all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="618fd-106">Per questa configurazione, è necessario un account con Sysdig.</span><span class="sxs-lookup"><span data-stu-id="618fd-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="618fd-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="618fd-107">Prerequisites</span></span>
<span data-ttu-id="618fd-108">[Distribuire](container-service-deployment.md) e [connettere](../container-service-connect.md) un cluster configurato dal servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="618fd-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="618fd-109">Esplorare l' [interfaccia utente](container-service-mesos-marathon-ui.md)di Marathon.</span><span class="sxs-lookup"><span data-stu-id="618fd-109">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="618fd-110">Andare a [http://app.sysdigcloud.com](http://app.sysdigcloud.com) per configurare un account cloud Sysdig.</span><span class="sxs-lookup"><span data-stu-id="618fd-110">Go to [http://app.sysdigcloud.com](http://app.sysdigcloud.com) to set up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="618fd-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="618fd-111">Sysdig</span></span>
<span data-ttu-id="618fd-112">Sysdig è un servizio di monitoraggio che consente di monitorare i contenitori nel cluster.</span><span class="sxs-lookup"><span data-stu-id="618fd-112">Sysdig is a monitoring service that allows you to monitor your containers within your cluster.</span></span> <span data-ttu-id="618fd-113">Sysdig non solo consente di risolvere problemi, ma include anche le metriche di monitoraggio di base per CPU, rete, memoria e I/O.</span><span class="sxs-lookup"><span data-stu-id="618fd-113">Sysdig is known to help with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="618fd-114">Con Sysdig è facile determinare quali contenitori sono più usati o quali usano la maggior quantità di memoria e CPU.</span><span class="sxs-lookup"><span data-stu-id="618fd-114">Sysdig makes it easy to see which containers are working the hardest or essentially using the most memory and CPU.</span></span> <span data-ttu-id="618fd-115">Questa visualizzazione è disponibile nella sezione della panoramica, attualmente nella versione beta.</span><span class="sxs-lookup"><span data-stu-id="618fd-115">This view is in the “Overview” section, which is currently in beta.</span></span> 

![Interfaccia utente di Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="618fd-117">Configurare una distribuzione Sysdig con Marathon</span><span class="sxs-lookup"><span data-stu-id="618fd-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="618fd-118">Questi passaggi illustrano come configurare e distribuire le applicazioni Sysdig nel cluster con Marathon.</span><span class="sxs-lookup"><span data-stu-id="618fd-118">These steps will show you how to configure and deploy Sysdig applications to your cluster with Marathon.</span></span> 

<span data-ttu-id="618fd-119">Accedere all'interfaccia utente del controller di dominio/sistema operativo tramite [http://localhost:80/](http://localhost:80/)Dall'interfaccia utente del controller di dominio/sistema operativo passare a "Universe" ("Universo") in basso a sinistra e quindi cercare "Sysdig".</span><span class="sxs-lookup"><span data-stu-id="618fd-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to the "Universe", which is on the bottom left and then search for "Sysdig."</span></span>

![Sysdig in Universe (Universo) per il controller di dominio/sistema operativo](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="618fd-121">Per completare la configurazione, è necessario un account cloud Sysdig o un account di valutazione gratuito.</span><span class="sxs-lookup"><span data-stu-id="618fd-121">Now to complete the configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="618fd-122">Una volta connessi al sito Web del cloud di Sysdig, fare clic sul nome utente. Nella pagina verrà visualizzata la chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="618fd-122">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Chiave API di Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="618fd-124">Immettere quindi la chiave di accesso nella configurazione di Sysdig in Universe (Universo) per il controller di dominio/sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="618fd-124">Next enter your Access Key into the Sysdig configuration within the DC/OS Universe.</span></span> 

![Configurazione di Sysdig in Universe (Universo) per il controller di dominio/sistema operativo](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="618fd-126">Impostare ora le istanze su 10000000 in modo che, quando viene aggiunto un nuovo nodo al cluster, Sysdig distribuirà automaticamente un agente nel nuovo nodo.</span><span class="sxs-lookup"><span data-stu-id="618fd-126">Now set the instances to 10000000 so whenever a new node is added to the cluster Sysdig will automatically deploy an agent to that new node.</span></span> <span data-ttu-id="618fd-127">Questa è una soluzione provvisoria per verificare che Sysdig venga distribuito in tutti i nuovi agenti del cluster.</span><span class="sxs-lookup"><span data-stu-id="618fd-127">This is an interim solution to make sure Sysdig will deploy to all new agents within the cluster.</span></span> 

![Configurazione di Sysdig nelle istanze di Universe (Universo) per il controller di dominio/sistema operativo](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="618fd-129">Una volta installato il pacchetto, tornare all'interfaccia utente di Sysdig per esplorare le diverse metriche di utilizzo per i contenitori nel cluster.</span><span class="sxs-lookup"><span data-stu-id="618fd-129">Once you've installed the package navigate back to the Sysdig UI and you'll be able to explore the different usage metrics for the containers within your cluster.</span></span> 

<span data-ttu-id="618fd-130">È anche possibile installare i dashboard specifici di Mesos e Marathon tramite la [creazione guidata nuovo dashboard](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="618fd-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
