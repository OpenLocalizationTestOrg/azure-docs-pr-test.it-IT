---
title: aaaManage controller di dominio o sistema operativo Azure cluster con interfaccia utente maratona | Documenti Microsoft
description: Distribuire i contenitori tooan Azure contenitore cluster del servizio tramite l'interfaccia utente web di maratona hello.
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Contenitori, Micro-servizi, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a><span data-ttu-id="2d3e6-104">Gestire un cluster di Azure contenitore del servizio controller di dominio o del sistema operativo tramite web maratona hello dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="2d3e6-104">Manage an Azure Container Service DC/OS cluster through hello Marathon web UI</span></span>
<span data-ttu-id="2d3e6-105">Controller di dominio/OS offre un ambiente per la distribuzione e scalabilità i carichi di lavoro cluster eliminando l'hardware sottostante hello.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="2d3e6-106">In DC/OS è disponibile anche un framework che gestisce la pianificazione e l'esecuzione dei carichi di lavoro di calcolo.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="2d3e6-107">Mentre i Framework sono disponibili per molti carichi di lavoro comuni, questo documento descrive come tooget iniziare la distribuzione di contenitori con maratona.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-107">While frameworks are available for many popular workloads, this document describes how tooget started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="2d3e6-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2d3e6-108">Prerequisites</span></span>
<span data-ttu-id="2d3e6-109">Prima di eseguire questi esempi, è necessario avere un cluster DC/OS configurato nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="2d3e6-110">È inoltre necessario cluster toothis di toohave connettività remota.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="2d3e6-111">Per ulteriori informazioni su questi elementi, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="2d3e6-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="2d3e6-112">Distribuire un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="2d3e6-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="2d3e6-113">Connettersi tooan cluster del servizio di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="2d3e6-113">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="2d3e6-114">In questo articolo si presuppone che sono di tunneling toohello cluster di controller di dominio o del sistema operativo tramite la porta locale 80.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-114">This article assumes you are tunneling toohello DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-hello-dcos-ui"></a><span data-ttu-id="2d3e6-115">Esplorare hello dell'interfaccia utente di controller di dominio o del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="2d3e6-115">Explore hello DC/OS UI</span></span>
<span data-ttu-id="2d3e6-116">Con un tunnel SSH (Secure Shell) [stabilita](../container-service-connect.md), Sfoglia toohttp://localhost/.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse toohttp://localhost/.</span></span> <span data-ttu-id="2d3e6-117">Questo carica l'interfaccia utente web di controller di dominio/OS hello e Mostra le informazioni sui cluster di hello, ad esempio le risorse, gli agenti active e servizi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-117">This loads hello DC/OS web UI and shows information about hello cluster, such as used resources, active agents, and running services.</span></span>

![Interfaccia utente di DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a><span data-ttu-id="2d3e6-119">Esplorare hello maratona UI</span><span class="sxs-lookup"><span data-stu-id="2d3e6-119">Explore hello Marathon UI</span></span>
<span data-ttu-id="2d3e6-120">hello toosee maratona dell'interfaccia utente, toohttp://localhost/marathon Sfoglia.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-120">toosee hello Marathon UI, browse toohttp://localhost/marathon.</span></span> <span data-ttu-id="2d3e6-121">In questa schermata è possibile avviare un nuovo contenitore o un'altra applicazione nel cluster di hello Azure contenitore del servizio controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-121">From this screen, you can start a new container or another application on hello Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="2d3e6-122">È anche possibile visualizzare le informazioni sull'esecuzione di contenitori e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-122">You can also see information about running containers and applications.</span></span>  

![Interfaccia utente di Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="2d3e6-124">Distribuire un contenitore Docker formattato</span><span class="sxs-lookup"><span data-stu-id="2d3e6-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="2d3e6-125">Fare clic su un nuovo contenitore usando maratona, toodeploy **Crea applicazione**e immettere le seguenti informazioni in schede modulo hello hello:</span><span class="sxs-lookup"><span data-stu-id="2d3e6-125">toodeploy a new container by using Marathon, click **Create Application**, and enter hello following information into hello form tabs:</span></span>

| <span data-ttu-id="2d3e6-126">Campo</span><span class="sxs-lookup"><span data-stu-id="2d3e6-126">Field</span></span> | <span data-ttu-id="2d3e6-127">Valore</span><span class="sxs-lookup"><span data-stu-id="2d3e6-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="2d3e6-128">ID</span><span class="sxs-lookup"><span data-stu-id="2d3e6-128">ID</span></span> |<span data-ttu-id="2d3e6-129">nginx</span><span class="sxs-lookup"><span data-stu-id="2d3e6-129">nginx</span></span> |
| <span data-ttu-id="2d3e6-130">Memoria</span><span class="sxs-lookup"><span data-stu-id="2d3e6-130">Memory</span></span> | <span data-ttu-id="2d3e6-131">32</span><span class="sxs-lookup"><span data-stu-id="2d3e6-131">32</span></span> |
| <span data-ttu-id="2d3e6-132">Image</span><span class="sxs-lookup"><span data-stu-id="2d3e6-132">Image</span></span> |<span data-ttu-id="2d3e6-133">nginx</span><span class="sxs-lookup"><span data-stu-id="2d3e6-133">nginx</span></span> |
| <span data-ttu-id="2d3e6-134">Network</span><span class="sxs-lookup"><span data-stu-id="2d3e6-134">Network</span></span> |<span data-ttu-id="2d3e6-135">Bridged</span><span class="sxs-lookup"><span data-stu-id="2d3e6-135">Bridged</span></span> |
| <span data-ttu-id="2d3e6-136">Host Port</span><span class="sxs-lookup"><span data-stu-id="2d3e6-136">Host Port</span></span> |<span data-ttu-id="2d3e6-137">80</span><span class="sxs-lookup"><span data-stu-id="2d3e6-137">80</span></span> |
| <span data-ttu-id="2d3e6-138">Protocol</span><span class="sxs-lookup"><span data-stu-id="2d3e6-138">Protocol</span></span> |<span data-ttu-id="2d3e6-139">TCP</span><span class="sxs-lookup"><span data-stu-id="2d3e6-139">TCP</span></span> |

![Interfaccia utente New Application--General](./media/container-service-mesos-marathon-ui/dcos4.png)

![Interfaccia utente New Application--Docker Container](./media/container-service-mesos-marathon-ui/dcos5.png)

![Interfaccia utente New Application--Ports and Service Discovery](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="2d3e6-143">Se si desidera toostatically mappa hello contenitore tooa porte nell'agente hello, è necessario toouse modalità JSON.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-143">If you want toostatically map hello container port tooa port on hello agent, you need toouse JSON Mode.</span></span> <span data-ttu-id="2d3e6-144">toodo passare in tal caso, creazione guidata nuova applicazione hello troppo**modalità JSON** utilizzando l'elemento toggle hello.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-144">toodo so, switch hello New Application wizard too**JSON Mode** by using hello toggle.</span></span> <span data-ttu-id="2d3e6-145">Immettere quindi hello seguente impostazione hello `portMappings` sezione hello dalla definizione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-145">Then enter hello following setting under hello `portMappings` section of hello application definition.</span></span> <span data-ttu-id="2d3e6-146">Questo esempio associa la porta 80 del contenitore di hello tooport 80 dell'agente di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-146">This example binds port 80 of hello container tooport 80 of hello DC/OS agent.</span></span> <span data-ttu-id="2d3e6-147">Dopo aver apportato questa modifica è possibile uscire dalla modalità JSON della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Interfaccia utente New Application--esempio con porta 80](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="2d3e6-149">Se si desidera tooenable controlli di integrità, è possibile impostare un percorso su hello **controlli di integrità** scheda.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-149">If you want tooenable health checks, set a path on hello **Health Checks** tab.</span></span>

![Nuova interfaccia utente dell'applicazione - Verifiche di integrità](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="2d3e6-151">cluster di controller di dominio/OS Hello viene distribuito con set di agenti privati e pubblici.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-151">hello DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="2d3e6-152">Applications hello cluster toobe tooaccess in grado di hello Internet, è necessario agente pubblica tooa toodeploy hello applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-152">For hello cluster toobe able tooaccess applications from hello Internet, you need toodeploy hello applications tooa public agent.</span></span> <span data-ttu-id="2d3e6-153">toodo in tal caso, selezionare hello **facoltativo** scheda della creazione guidata nuova applicazione hello e immettere **slave_public** per hello **accettato ruoli risorsa**.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-153">toodo so, select hello **Optional** tab of hello New Application wizard and enter **slave_public** for hello **Accepted Resource Roles**.</span></span>

<span data-ttu-id="2d3e6-154">Fare clic su **Create Application** (Crea applicazione).</span><span class="sxs-lookup"><span data-stu-id="2d3e6-154">Then click **Create Application**.</span></span>

![Interfaccia utente New Application--impostazione dell'agente pubblico](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="2d3e6-156">Indietro nella pagina principale di maratona hello, è possibile visualizzare lo stato di distribuzione hello per contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-156">Back on hello Marathon main page, you can see hello deployment status for hello container.</span></span> <span data-ttu-id="2d3e6-157">Inizialmente è visualizzato lo stato **Deploying** (Distribuzione).</span><span class="sxs-lookup"><span data-stu-id="2d3e6-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="2d3e6-158">Dopo una corretta distribuzione, hello modifiche allo stato troppo**esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-158">After a successful deployment, hello status changes too**Running**.</span></span>

![Interfaccia utente della pagina principale di Marathon--stato di distribuzione contenitore](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="2d3e6-160">Quando si passa indietro toohello web di controller di dominio o del sistema operativo dell'interfaccia utente (http://localhost/), vedrai che un'attività (in questo caso, un contenitore Docker in formato) sia in esecuzione nel cluster di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-160">When you switch back toohello DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on hello DC/OS cluster.</span></span>

![Controller di dominio o del sistema operativo interfaccia utente web - attività in esecuzione nel cluster hello](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="2d3e6-162">nodo del cluster hello toosee che hello attività è in esecuzione in, fare clic su hello **nodi** scheda.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-162">toosee hello cluster node that hello task is running on, click hello **Nodes** tab.</span></span>

![Interfaccia utente Web di DC/OS--nodo del cluster dell'attività](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a><span data-ttu-id="2d3e6-164">Raggiungere hello contenitore</span><span class="sxs-lookup"><span data-stu-id="2d3e6-164">Reach hello container</span></span>

<span data-ttu-id="2d3e6-165">In questo esempio, un'applicazione hello è in esecuzione in un nodo agente pubblica.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-165">In this example, hello application is running on a public agent node.</span></span> <span data-ttu-id="2d3e6-166">Si raggiunge un'applicazione hello da hello internet esplorando toohello agente FQDN del cluster hello: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, dove:</span><span class="sxs-lookup"><span data-stu-id="2d3e6-166">You reach hello application from hello internet by browsing toohello agent FQDN of hello cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="2d3e6-167">**DNSPREFIX** è un prefisso DNS hello fornito al momento della distribuzione cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-167">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>
* <span data-ttu-id="2d3e6-168">**AREA** hello area in cui si trova il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2d3e6-168">**REGION** is hello region in which your resource group is located.</span></span>

    ![Nginx da Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="2d3e6-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d3e6-170">Next steps</span></span>
* [<span data-ttu-id="2d3e6-171">Utilizzare i controller di dominio/OS e hello maratona API</span><span class="sxs-lookup"><span data-stu-id="2d3e6-171">Work with DC/OS and hello Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="2d3e6-172">Informazioni approfondite su hello servizio contenitore di Azure con Mesos</span><span class="sxs-lookup"><span data-stu-id="2d3e6-172">Deep dive on hello Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
