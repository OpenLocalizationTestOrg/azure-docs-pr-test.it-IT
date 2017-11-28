---
title: un servizio di contenitore di Azure aaaMonitor cluster con Sysdig | Documenti Microsoft
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
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="969db-104">Monitorare un cluster del servizio contenitore di Azure con Sysdig</span><span class="sxs-lookup"><span data-stu-id="969db-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="969db-105">In questo articolo, si distribuirà Sysdig agenti tooall hello agente i nodi del cluster del servizio di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="969db-105">In this article, we will deploy Sysdig agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="969db-106">Per questa configurazione, è necessario un account con Sysdig.</span><span class="sxs-lookup"><span data-stu-id="969db-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="969db-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="969db-107">Prerequisites</span></span>
<span data-ttu-id="969db-108">[Distribuire](container-service-deployment.md) e [connettere](../container-service-connect.md) un cluster configurato dal servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="969db-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="969db-109">Esplorare hello [dell'interfaccia utente maratona](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="969db-109">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="969db-110">Andare troppo[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset di un account cloud Sysdig.</span><span class="sxs-lookup"><span data-stu-id="969db-110">Go too[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="969db-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="969db-111">Sysdig</span></span>
<span data-ttu-id="969db-112">Sysdig è un servizio di monitoraggio che consente di toomonitor ai contenitori all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="969db-112">Sysdig is a monitoring service that allows you toomonitor your containers within your cluster.</span></span> <span data-ttu-id="969db-113">Sysdig è noto toohelp la risoluzione dei problemi, ma include anche le metriche di monitoraggio di base per la CPU, rete, memoria e i/o.</span><span class="sxs-lookup"><span data-stu-id="969db-113">Sysdig is known toohelp with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="969db-114">Sysdig rende facile toosee utilizzano i contenitori hello più difficili o essenzialmente utilizzando hello la maggior parte di memoria e CPU.</span><span class="sxs-lookup"><span data-stu-id="969db-114">Sysdig makes it easy toosee which containers are working hello hardest or essentially using hello most memory and CPU.</span></span> <span data-ttu-id="969db-115">Questa visualizzazione è nella sezione "Overview", in cui è attualmente in versione beta di hello.</span><span class="sxs-lookup"><span data-stu-id="969db-115">This view is in hello “Overview” section, which is currently in beta.</span></span> 

![Interfaccia utente di Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="969db-117">Configurare una distribuzione Sysdig con Marathon</span><span class="sxs-lookup"><span data-stu-id="969db-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="969db-118">Questa procedura viene illustrato come tooconfigure e la distribuzione Sysdig applicazioni tooyour cluster con maratona.</span><span class="sxs-lookup"><span data-stu-id="969db-118">These steps will show you how tooconfigure and deploy Sysdig applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="969db-119">Accedere all'interfaccia del controller di dominio o del sistema operativo tramite [http://localhost:80 /](http://localhost:80/) una volta nell'interfaccia utente di controller di dominio/OS hello passare toohello "Universo", che si trova in hello in basso a sinistra e quindi cerca "Sysdig".</span><span class="sxs-lookup"><span data-stu-id="969db-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate toohello "Universe", which is on hello bottom left and then search for "Sysdig."</span></span>

![Sysdig in Universe (Universo) per il controller di dominio/sistema operativo](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="969db-121">Ora configuration hello toocomplete è necessario un Sysdig cloud account o un account di prova.</span><span class="sxs-lookup"><span data-stu-id="969db-121">Now toocomplete hello configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="969db-122">Dopo aver eseguito il nel sito Web di toohello Sysdig cloud, fare clic sul nome utente e nella pagina di hello si dovrebbe visualizzare la "chiave di accesso".</span><span class="sxs-lookup"><span data-stu-id="969db-122">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Chiave API di Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="969db-124">Quindi immettere la chiave di accesso alla configurazione Sysdig hello all'interno di hello l'universo dei controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="969db-124">Next enter your Access Key into hello Sysdig configuration within hello DC/OS Universe.</span></span> 

![Configurazione Sysdig in hello l'universo dei controller di dominio o del sistema operativo](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="969db-126">Ora impostato hello istanze too10000000 pertanto ogni volta che viene aggiunto un nuovo nodo cluster toohello Sysdig distribuirà automaticamente un agente toothat nuovo nodo.</span><span class="sxs-lookup"><span data-stu-id="969db-126">Now set hello instances too10000000 so whenever a new node is added toohello cluster Sysdig will automatically deploy an agent toothat new node.</span></span> <span data-ttu-id="969db-127">Si tratta di un toomake soluzione temporanea che Sysdig distribuirà tooall nuovi agenti all'interno di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="969db-127">This is an interim solution toomake sure Sysdig will deploy tooall new agents within hello cluster.</span></span> 

![Configurazione Sysdig nel controller di dominio o del sistema operativo universo-le istanze di hello](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="969db-129">Dopo aver installato il pacchetto di hello spostarsi indietro toohello Sysdig UI e sarà in grado di tooexplore hello diversi le metriche di utilizzo contenitori hello all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="969db-129">Once you've installed hello package navigate back toohello Sysdig UI and you'll be able tooexplore hello different usage metrics for hello containers within your cluster.</span></span> 

<span data-ttu-id="969db-130">È anche possibile installare i dashboard specifici di Mesos e Marathon tramite la [creazione guidata nuovo dashboard](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="969db-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
