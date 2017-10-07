---
title: cluster di controller di dominio o sistema operativo Azure aaaMonitor - Dynatrace | Documenti Microsoft
description: Monitorare un cluster DC/OS del servizio contenitore di Azure con Dynatrace. Distribuire hello Dynatrace OneAgent tramite il dashboard di controller di dominio/OS hello.
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
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="a59ca-105">Monitorare un cluster DC/OS del servizio contenitore di Azure con Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="a59ca-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="a59ca-106">In questo articolo verrà illustrato come hello toodeploy [Dynatrace](https://www.dynatrace.com/) toomonitor OneAgent tutti hello nodi agente nel cluster il servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="a59ca-106">In this article, we show you how toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor all hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="a59ca-107">Per questa configurazione, è necessario un account con Dynatrace SaaS/Managed.</span><span class="sxs-lookup"><span data-stu-id="a59ca-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="a59ca-108">Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="a59ca-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="a59ca-109">Dynatrace è una soluzione di monitoraggio nativa del cloud per gli ambienti cluster e dei contenitori altamente dinamici.</span><span class="sxs-lookup"><span data-stu-id="a59ca-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="a59ca-110">Consente di ottimizzare la toobetter contenitore distribuzioni e le allocazioni di memoria utilizzando i dati di utilizzo in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="a59ca-110">It allows you toobetter optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="a59ca-111">È in grado di individuare automaticamente problemi a livello di applicazioni e infrastruttura fornendo una baseline automatizzata, oltre alla correlazione dei problemi e al rilevamento delle cause principali.</span><span class="sxs-lookup"><span data-stu-id="a59ca-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="a59ca-112">Figura Hello seguente è illustrato hello UI Dynatrace:</span><span class="sxs-lookup"><span data-stu-id="a59ca-112">hello following figure shows hello Dynatrace UI:</span></span>

![Interfaccia utente di Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="a59ca-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a59ca-114">Prerequisites</span></span> 
<span data-ttu-id="a59ca-115">[Distribuire](container-service-deployment.md) e [connettersi](./../container-service-connect.md) tooa cluster configurato dal servizio di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="a59ca-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) tooa cluster configured by Azure Container Service.</span></span> <span data-ttu-id="a59ca-116">Esplorare hello [dell'interfaccia utente maratona](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="a59ca-116">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="a59ca-117">Andare troppo[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset conto Dynatrace SaaS.</span><span class="sxs-lookup"><span data-stu-id="a59ca-117">Go too[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="a59ca-118">Configurare una distribuzione Dynatrace con Marathon</span><span class="sxs-lookup"><span data-stu-id="a59ca-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="a59ca-119">La procedura mostra come tooconfigure e la distribuzione Dynatrace applicazioni tooyour cluster con maratona.</span><span class="sxs-lookup"><span data-stu-id="a59ca-119">These steps show you how tooconfigure and deploy Dynatrace applications tooyour cluster with Marathon.</span></span>

1. <span data-ttu-id="a59ca-120">Accedere all'interfaccia utente del controller di dominio/sistema operativo da [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="a59ca-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="a59ca-121">Una volta nell'interfaccia utente di controller di dominio/OS hello, passare toohello **universo** scheda e quindi cercare **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="a59ca-121">Once in hello DC/OS UI, navigate toohello **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace in Universe (Universo) di DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="a59ca-123">configurazione di hello toocomplete, è necessario un account Dynatrace SaaS o un account di prova.</span><span class="sxs-lookup"><span data-stu-id="a59ca-123">toocomplete hello configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="a59ca-124">Una volta accedere al dashboard Dynatrace hello, selezionare **distribuire Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="a59ca-124">Once you log into hello Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Dynatrace - Set up PaaS integration (Configura integrazione Paas)](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="a59ca-126">Nella pagina hello selezionare **configurare l'integrazione di PaaS**.</span><span class="sxs-lookup"><span data-stu-id="a59ca-126">On hello page, select **Set up PaaS integration**.</span></span> 

    ![Token API di Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="a59ca-128">Immettere il token dell'API in hello Dynatrace OneAgent configurazione all'interno di hello l'universo dei controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a59ca-128">Enter your API token into hello Dynatrace OneAgent configuration within hello DC/OS Universe.</span></span> 

    ![Configurazione Dynatrace OneAgent in hello l'universo dei controller di dominio o del sistema operativo](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="a59ca-130">Impostare le istanze di hello toohello numero dei nodi si intende toorun.</span><span class="sxs-lookup"><span data-stu-id="a59ca-130">Set hello instances toohello number of nodes you intend toorun.</span></span> <span data-ttu-id="a59ca-131">L'impostazione di un numero più alto inoltre funziona, ma i controller di dominio o del sistema operativo continuerà a tentare toofind nuove istanze fino a raggiungere quel numero effettivamente.</span><span class="sxs-lookup"><span data-stu-id="a59ca-131">Setting a higher number also works, but DC/OS will keep trying toofind new instances until that number is actually reached.</span></span> <span data-ttu-id="a59ca-132">Se si preferisce, è anche possibile impostare questo valore tooa come 1000000.</span><span class="sxs-lookup"><span data-stu-id="a59ca-132">If you prefer, you can also set this tooa value like 1000000.</span></span> <span data-ttu-id="a59ca-133">In questo caso, ogni volta che un nuovo nodo viene aggiunto il cluster toohello, Dynatrace distribuisce automaticamente un agente toothat nuovo nodo, il prezzo di hello del controller di dominio o sistema operativo costantemente tentativo toodeploy altre istanze.</span><span class="sxs-lookup"><span data-stu-id="a59ca-133">In this case, whenever a new node is added toohello cluster, Dynatrace automatically deploys an agent toothat new node, at hello price of DC/OS constantly trying toodeploy further instances.</span></span>

    ![Configurazione Dynatrace nel controller di dominio o del sistema operativo universo-le istanze di hello](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="a59ca-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a59ca-135">Next steps</span></span>

<span data-ttu-id="a59ca-136">Dopo aver installato il pacchetto di hello, spostarsi indietro toohello Dynatrace dashboard.</span><span class="sxs-lookup"><span data-stu-id="a59ca-136">Once you've installed hello package, navigate back toohello Dynatrace dashboard.</span></span> <span data-ttu-id="a59ca-137">È possibile esplorare le metriche di utilizzo diversi hello per contenitori hello all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="a59ca-137">You can explore hello different usage metrics for hello containers within your cluster.</span></span> 
