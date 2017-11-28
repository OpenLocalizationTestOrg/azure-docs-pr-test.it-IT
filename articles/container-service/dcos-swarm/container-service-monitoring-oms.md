---
title: cluster di controller di dominio o sistema operativo Azure aaaMonitor - Operations Manager | Documenti Microsoft
description: Monitorare un cluster DC/OS del servizio contenitore di Azure con Microsoft Operations Management Suite.
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="7bb88-103">Monitorare un cluster DC/OS del servizio contenitore di Azure con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="7bb88-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="7bb88-104">Microsoft Operations Management Suite (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud.</span><span class="sxs-lookup"><span data-stu-id="7bb88-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="7bb88-105">Soluzione di contenitore è una soluzione Analitica di Log di OMS, che consente di visualizzare l'inventario contenitore hello, prestazioni e i log in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="7bb88-105">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="7bb88-106">È possibile audit, risoluzione dei contenitori di visualizzazione dei log di hello in posizione centralizzata e trovare rumore utilizzo in eccesso contenitore in un host.</span><span class="sxs-lookup"><span data-stu-id="7bb88-106">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="7bb88-107">Per ulteriori informazioni sulla soluzione di contenitore, vedere toothe [contenitore soluzione Log Analitica](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="7bb88-107">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-hello-dcos-universe"></a><span data-ttu-id="7bb88-108">Configurazione di OMS da universo di controller di dominio/OS hello</span><span class="sxs-lookup"><span data-stu-id="7bb88-108">Setting up OMS from hello DC/OS universe</span></span>


<span data-ttu-id="7bb88-109">In questo articolo presuppone che sia stato configurato un controller di dominio o sistema operativo e aver distribuito le applicazioni web semplice contenitore nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7bb88-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on hello cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="7bb88-110">Prerequisito.</span><span class="sxs-lookup"><span data-stu-id="7bb88-110">Pre-requisite</span></span>
- <span data-ttu-id="7bb88-111">[Sottoscrizione di Microsoft Azure](https://azure.microsoft.com/free/): è gratuita.</span><span class="sxs-lookup"><span data-stu-id="7bb88-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="7bb88-112">Configurazione dell'area di lavoro di Microsoft OMS (vedere il "Passaggio 3" sotto)</span><span class="sxs-lookup"><span data-stu-id="7bb88-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="7bb88-113">[Interfaccia della riga di comando di DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) installata.</span><span class="sxs-lookup"><span data-stu-id="7bb88-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="7bb88-114">Nel dashboard di controller di dominio/OS hello, fare clic su universo e cercare "OMS', come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7bb88-114">In hello DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="7bb88-115">Fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="7bb88-115">Click **Install**.</span></span> <span data-ttu-id="7bb88-116">Verrà visualizzato un pop backup con informazioni sulla versione di hello OMS e un **Installa pacchetto** o **installazione avanzata** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7bb88-116">You will see a pop up with hello OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="7bb88-117">Quando fa clic su **installazione avanzata**, determinando toohello **proprietà di configurazione specifiche OMS** pagina.</span><span class="sxs-lookup"><span data-stu-id="7bb88-117">When you click **Advanced Installation**, which leads you toohello **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="7bb88-118">In questo caso, verrà chiesto hello tooenter `wsid` (hello ID area di lavoro OMS) e `wskey` (hello OMS chiave primaria per l'id dell'area di lavoro hello).</span><span class="sxs-lookup"><span data-stu-id="7bb88-118">Here, you will be asked tooenter hello `wsid` (hello OMS workspace ID) and `wskey` (hello OMS primary key for hello workspace id).</span></span> <span data-ttu-id="7bb88-119">entrambi tooget `wsid` e `wskey` toocreate è necessario un account OMS alla <https://mms.microsoft.com>. Seguire hello passaggi toocreate un account.</span><span class="sxs-lookup"><span data-stu-id="7bb88-119">tooget both `wsid` and `wskey` you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="7bb88-120">Dopo aver terminato la creazione di account di hello, è necessario tooobtain il `wsid` e `wskey` facendo **impostazioni**, quindi **Connected Sources**e quindi **server Linux** , come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7bb88-120">Once you are done creating hello account, you need tooobtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="7bb88-121">Selezionare hello numero è OMS istanze desiderate e fare clic sul pulsante di hello 'Verifica e installa'.</span><span class="sxs-lookup"><span data-stu-id="7bb88-121">Select hello number you OMS instances that you want and click hello ‘Review and Install’ button.</span></span> <span data-ttu-id="7bb88-122">In genere, si desidererà toohave hello numero OMS istanze toohello uguale della macchina virtuale è presente nel cluster di agente.</span><span class="sxs-lookup"><span data-stu-id="7bb88-122">Typically, you will want toohave hello number of OMS instances equal toohello number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="7bb88-123">Agente OMS per Linux viene installato come singoli contenitori in ogni macchina virtuale che desideri toocollect informazioni per il monitoraggio e registrazione.</span><span class="sxs-lookup"><span data-stu-id="7bb88-123">OMS Agent for Linux is installs as individual containers on each VM that it wants toocollect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="7bb88-124">Configurazione di un dashboard OMS semplice</span><span class="sxs-lookup"><span data-stu-id="7bb88-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="7bb88-125">Dopo aver installato hello agente OMS per Linux in macchine virtuali di hello, il passaggio successivo è tooset i dashboard OMS hello.</span><span class="sxs-lookup"><span data-stu-id="7bb88-125">Once you have installed hello OMS Agent for Linux on hello VMs, next step is tooset up hello OMS dashboard.</span></span> <span data-ttu-id="7bb88-126">Esistono due modi toodo questo: portale OMS o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bb88-126">There are two ways toodo this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="7bb88-127">Portale di OMS</span><span class="sxs-lookup"><span data-stu-id="7bb88-127">OMS Portal</span></span> 

<span data-ttu-id="7bb88-128">Accedi al portale di OMS toohello (<https://mms.microsoft.com>) e passare toohello **raccolta soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="7bb88-128">Log in toohello OMS portal (<https://mms.microsoft.com>) and go toohello **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="7bb88-129">Una volta nel hello **raccolta soluzioni**selezionare **contenitori**.</span><span class="sxs-lookup"><span data-stu-id="7bb88-129">Once you are in hello **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="7bb88-130">Dopo aver selezionato hello contenitore soluzione, si noterà hello riquadro nella pagina Dashboard panoramica di OMS hello.</span><span class="sxs-lookup"><span data-stu-id="7bb88-130">Once you’ve selected hello Container Solution, you will see hello tile on hello OMS Overview Dashboard page.</span></span> <span data-ttu-id="7bb88-131">Una volta hello caricamento dati del contenitore sono indicizzati, si noterà riquadro hello popolato con informazioni sui riquadri di visualizzazione delle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="7bb88-131">Once hello ingested container data is indexed, you will see hello tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="7bb88-132">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7bb88-132">Azure Portal</span></span> 

<span data-ttu-id="7bb88-133">Portale di account di accesso tooAzure all'indirizzo <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="7bb88-133">Login tooAzure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="7bb88-134">Passare a **Marketplace**, selezionare **Monitoraggio + gestione** e fare clic su **Visualizza tutto**.</span><span class="sxs-lookup"><span data-stu-id="7bb88-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="7bb88-135">Dopodiché, digitare `containers` nella ricerca</span><span class="sxs-lookup"><span data-stu-id="7bb88-135">Then Type `containers` in search.</span></span> <span data-ttu-id="7bb88-136">Verrà visualizzato "contenitori" nei risultati della ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="7bb88-136">You will see "containers" in hello search results.</span></span> <span data-ttu-id="7bb88-137">Selezionare **Contenitori** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7bb88-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="7bb88-138">Dopo avere fatto clic su **Crea**, verrà chiesto di indicare l'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7bb88-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="7bb88-139">Selezionarne una esistente, oppure creare una nuova area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7bb88-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="7bb88-140">Dopo averla selezionata, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7bb88-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="7bb88-141">Per ulteriori informazioni sulla soluzione contenitore OMS hello, consultare toothe [contenitore soluzione Log Analitica](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="7bb88-141">For more information about hello OMS Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a><span data-ttu-id="7bb88-142">Come tooscale agente OMS con ACS controller di dominio o del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="7bb88-142">How tooscale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="7bb88-143">Nel caso in cui è necessario toohave installato l'agente OMS insufficiente conteggio effettivo nodo hello o scalabilità VMSS aggiungendo altre VM, è possibile farlo scalando hello `msoms` servizio.</span><span class="sxs-lookup"><span data-stu-id="7bb88-143">In case you need toohave installed OMS agent short of hello actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling hello `msoms` service.</span></span>

<span data-ttu-id="7bb88-144">È possibile andare tooMarathon o hello scheda DC/servizi del sistema operativo dell'interfaccia utente e la scalabilità verticale il numero di nodi.</span><span class="sxs-lookup"><span data-stu-id="7bb88-144">You can either go tooMarathon or hello DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="7bb88-145">Nodi tooother che non hanno ancora installato l'agente OMS hello verrà distribuito.</span><span class="sxs-lookup"><span data-stu-id="7bb88-145">This will deploy tooother nodes which have not yet deployed hello OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="7bb88-146">Disinstallare OMS di Microsoft</span><span class="sxs-lookup"><span data-stu-id="7bb88-146">Uninstall MS OMS</span></span>

<span data-ttu-id="7bb88-147">toouninstall MS OMS immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7bb88-147">toouninstall MS OMS enter hello following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="7bb88-148">Facci sapere</span><span class="sxs-lookup"><span data-stu-id="7bb88-148">Let us know!!!</span></span>
<span data-ttu-id="7bb88-149">Cosa funziona?</span><span class="sxs-lookup"><span data-stu-id="7bb88-149">What works?</span></span> <span data-ttu-id="7bb88-150">Cosa manca?</span><span class="sxs-lookup"><span data-stu-id="7bb88-150">What is missing?</span></span> <span data-ttu-id="7bb88-151">Altre è necessario per questa toobe utili per l'utente?</span><span class="sxs-lookup"><span data-stu-id="7bb88-151">What else do you need for this toobe useful for you?</span></span> <span data-ttu-id="7bb88-152">Scrivere a <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="7bb88-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bb88-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7bb88-153">Next steps</span></span>

 <span data-ttu-id="7bb88-154">Ora che è stato impostato toomonitor OMS ai contenitori,[visualizzare il dashboard di contenitore](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="7bb88-154">Now that you have set up OMS toomonitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
