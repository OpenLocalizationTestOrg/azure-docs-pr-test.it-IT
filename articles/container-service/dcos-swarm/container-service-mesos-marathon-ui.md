---
title: Gestire un cluster DC/OS di Azure con l'interfaccia utente di Marathon | Microsoft Docs
description: Distribuire contenitori in un cluster del servizio contenitore di Azure usando l'interfaccia utente Web di Marathon.
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
ms.openlocfilehash: b00088bb005519dc5d533433308c0e3e33c7f433
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-the-marathon-web-ui"></a><span data-ttu-id="39ee7-104">Gestire un cluster DC/OS del servizio contenitore di Azure tramite l'interfaccia utente Web di Marathon</span><span class="sxs-lookup"><span data-stu-id="39ee7-104">Manage an Azure Container Service DC/OS cluster through the Marathon web UI</span></span>
<span data-ttu-id="39ee7-105">DC/OS offre un ambiente di distribuzione e ridimensionamento dei carichi di lavoro cluster con l'astrazione dell'hardware sottostante.</span><span class="sxs-lookup"><span data-stu-id="39ee7-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="39ee7-106">In DC/OS è disponibile anche un framework che gestisce la pianificazione e l'esecuzione dei carichi di lavoro di calcolo.</span><span class="sxs-lookup"><span data-stu-id="39ee7-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="39ee7-107">Sono disponibili framework per molti dei carichi di lavoro più comuni. Questo documento illustra come iniziare la distribuzione di contenitori con Marathon.</span><span class="sxs-lookup"><span data-stu-id="39ee7-107">While frameworks are available for many popular workloads, this document describes how to get started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="39ee7-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="39ee7-108">Prerequisites</span></span>
<span data-ttu-id="39ee7-109">Prima di eseguire questi esempi, è necessario avere un cluster DC/OS configurato nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ee7-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="39ee7-110">È necessaria anche la connettività remota a questo cluster.</span><span class="sxs-lookup"><span data-stu-id="39ee7-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="39ee7-111">Per altre informazioni su questi elementi, vedere gli articoli indicati di seguito:</span><span class="sxs-lookup"><span data-stu-id="39ee7-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="39ee7-112">Distribuire un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="39ee7-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="39ee7-113">Connettersi a un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="39ee7-113">Connect to an Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="39ee7-114">Questo articolo presuppone il tunneling dell'utente al cluster DC/OS tramite la porta locale 80.</span><span class="sxs-lookup"><span data-stu-id="39ee7-114">This article assumes you are tunneling to the DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-the-dcos-ui"></a><span data-ttu-id="39ee7-115">Esplorare l'interfaccia utente di DC/OS</span><span class="sxs-lookup"><span data-stu-id="39ee7-115">Explore the DC/OS UI</span></span>
<span data-ttu-id="39ee7-116">Dopo aver [stabilito](../container-service-connect.md) un tunnel SSH (Secure Shell), passare a http://localhost/.</span><span class="sxs-lookup"><span data-stu-id="39ee7-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse to http://localhost/.</span></span> <span data-ttu-id="39ee7-117">Verrà caricata l'interfaccia utente Web di DC/OS che visualizza informazioni sul cluster, ad esempio le risorse usate, gli agenti attivi e i servizi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="39ee7-117">This loads the DC/OS web UI and shows information about the cluster, such as used resources, active agents, and running services.</span></span>

![Interfaccia utente di DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-the-marathon-ui"></a><span data-ttu-id="39ee7-119">Esplorare l'interfaccia utente di Marathon</span><span class="sxs-lookup"><span data-stu-id="39ee7-119">Explore the Marathon UI</span></span>
<span data-ttu-id="39ee7-120">Per visualizzare l'interfaccia utente di Marathon, andare su http://localhost/marathon.</span><span class="sxs-lookup"><span data-stu-id="39ee7-120">To see the Marathon UI, browse to http://localhost/marathon.</span></span> <span data-ttu-id="39ee7-121">In questa schermata è possibile avviare un nuovo contenitore o un'altra applicazione nel cluster DC/OS del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="39ee7-121">From this screen, you can start a new container or another application on the Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="39ee7-122">È anche possibile visualizzare le informazioni sull'esecuzione di contenitori e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="39ee7-122">You can also see information about running containers and applications.</span></span>  

![Interfaccia utente di Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="39ee7-124">Distribuire un contenitore Docker formattato</span><span class="sxs-lookup"><span data-stu-id="39ee7-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="39ee7-125">Per distribuire un nuovo contenitore con Marathon, fare clic sul pulsante **Create Application** (Crea applicazione) e immettere le informazioni seguenti nel modulo:</span><span class="sxs-lookup"><span data-stu-id="39ee7-125">To deploy a new container by using Marathon, click **Create Application**, and enter the following information into the form tabs:</span></span>

| <span data-ttu-id="39ee7-126">Campo</span><span class="sxs-lookup"><span data-stu-id="39ee7-126">Field</span></span> | <span data-ttu-id="39ee7-127">Valore</span><span class="sxs-lookup"><span data-stu-id="39ee7-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="39ee7-128">ID</span><span class="sxs-lookup"><span data-stu-id="39ee7-128">ID</span></span> |<span data-ttu-id="39ee7-129">nginx</span><span class="sxs-lookup"><span data-stu-id="39ee7-129">nginx</span></span> |
| <span data-ttu-id="39ee7-130">Memoria</span><span class="sxs-lookup"><span data-stu-id="39ee7-130">Memory</span></span> | <span data-ttu-id="39ee7-131">32</span><span class="sxs-lookup"><span data-stu-id="39ee7-131">32</span></span> |
| <span data-ttu-id="39ee7-132">Image</span><span class="sxs-lookup"><span data-stu-id="39ee7-132">Image</span></span> |<span data-ttu-id="39ee7-133">nginx</span><span class="sxs-lookup"><span data-stu-id="39ee7-133">nginx</span></span> |
| <span data-ttu-id="39ee7-134">Network</span><span class="sxs-lookup"><span data-stu-id="39ee7-134">Network</span></span> |<span data-ttu-id="39ee7-135">Bridged</span><span class="sxs-lookup"><span data-stu-id="39ee7-135">Bridged</span></span> |
| <span data-ttu-id="39ee7-136">Host Port</span><span class="sxs-lookup"><span data-stu-id="39ee7-136">Host Port</span></span> |<span data-ttu-id="39ee7-137">80</span><span class="sxs-lookup"><span data-stu-id="39ee7-137">80</span></span> |
| <span data-ttu-id="39ee7-138">Protocol</span><span class="sxs-lookup"><span data-stu-id="39ee7-138">Protocol</span></span> |<span data-ttu-id="39ee7-139">TCP</span><span class="sxs-lookup"><span data-stu-id="39ee7-139">TCP</span></span> |

![Interfaccia utente New Application--General](./media/container-service-mesos-marathon-ui/dcos4.png)

![Interfaccia utente New Application--Docker Container](./media/container-service-mesos-marathon-ui/dcos5.png)

![Interfaccia utente New Application--Ports and Service Discovery](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="39ee7-143">Per eseguire il mapping statico della porta del contenitore su una porta dell'agente è necessario usare la modalità JSON.</span><span class="sxs-lookup"><span data-stu-id="39ee7-143">If you want to statically map the container port to a port on the agent, you need to use JSON Mode.</span></span> <span data-ttu-id="39ee7-144">A tale scopo impostare la procedura guidata New Application su **JSON Mode** usando l'interruttore.</span><span class="sxs-lookup"><span data-stu-id="39ee7-144">To do so, switch the New Application wizard to **JSON Mode** by using the toggle.</span></span> <span data-ttu-id="39ee7-145">Specificare quindi l'impostazione seguente sotto la sezione `portMappings` della definizione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="39ee7-145">Then enter the following setting under the `portMappings` section of the application definition.</span></span> <span data-ttu-id="39ee7-146">Questo esempio associa la porta 80 del contenitore alla porta 80 dell'agente DC/OS.</span><span class="sxs-lookup"><span data-stu-id="39ee7-146">This example binds port 80 of the container to port 80 of the DC/OS agent.</span></span> <span data-ttu-id="39ee7-147">Dopo aver apportato questa modifica è possibile uscire dalla modalità JSON della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="39ee7-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Interfaccia utente New Application--esempio con porta 80](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="39ee7-149">Se si vuole abilitare le verifiche di integrità, impostare un percorso nella scheda **Health Checks** (Verifiche integrità).</span><span class="sxs-lookup"><span data-stu-id="39ee7-149">If you want to enable health checks, set a path on the **Health Checks** tab.</span></span>

![Nuova interfaccia utente dell'applicazione - Verifiche di integrità](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="39ee7-151">Il cluster CD/OS viene distribuito con un set di agenti privati e pubblici.</span><span class="sxs-lookup"><span data-stu-id="39ee7-151">The DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="39ee7-152">Per consentire al cluster di accedere alle applicazioni da Internet è necessario distribuire le applicazioni a un agente di pubblico.</span><span class="sxs-lookup"><span data-stu-id="39ee7-152">For the cluster to be able to access applications from the Internet, you need to deploy the applications to a public agent.</span></span> <span data-ttu-id="39ee7-153">A tale scopo, selezionare la scheda **Optional** (Facoltativo) della procedura guidata New Application (Nuova applicazione) e immettere **slave_public** in **Accepted Resource Roles** (Ruoli risorsa accettati).</span><span class="sxs-lookup"><span data-stu-id="39ee7-153">To do so, select the **Optional** tab of the New Application wizard and enter **slave_public** for the **Accepted Resource Roles**.</span></span>

<span data-ttu-id="39ee7-154">Fare clic su **Create Application** (Crea applicazione).</span><span class="sxs-lookup"><span data-stu-id="39ee7-154">Then click **Create Application**.</span></span>

![Interfaccia utente New Application--impostazione dell'agente pubblico](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="39ee7-156">Tornare alla pagina principale di Marathon, dove ora viene visualizzato lo stato di distribuzione del contenitore.</span><span class="sxs-lookup"><span data-stu-id="39ee7-156">Back on the Marathon main page, you can see the deployment status for the container.</span></span> <span data-ttu-id="39ee7-157">Inizialmente è visualizzato lo stato **Deploying** (Distribuzione).</span><span class="sxs-lookup"><span data-stu-id="39ee7-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="39ee7-158">Dopo una corretta distribuzione, lo stato cambia in **Running** (In esecuzione).</span><span class="sxs-lookup"><span data-stu-id="39ee7-158">After a successful deployment, the status changes to **Running**.</span></span>

![Interfaccia utente della pagina principale di Marathon--stato di distribuzione contenitore](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="39ee7-160">Quando si passa di nuovo all'interfaccia utente Web di DC/OS (http://localhost/) si noterà che nel cluster DC/OS è in esecuzione un'attività, in questo caso un contenitore in formato Docker.</span><span class="sxs-lookup"><span data-stu-id="39ee7-160">When you switch back to the DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on the DC/OS cluster.</span></span>

![Interfaccia utente Web di DC/OS--attività in esecuzione nel cluster](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="39ee7-162">Per visualizzare il nodo del cluster in cui viene eseguita l'attività, fare clic sulla scheda **Nodes** (Nodi).</span><span class="sxs-lookup"><span data-stu-id="39ee7-162">To see the cluster node that the task is running on, click the **Nodes** tab.</span></span>

![Interfaccia utente Web di DC/OS--nodo del cluster dell'attività](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-the-container"></a><span data-ttu-id="39ee7-164">Raggiungere il contenitore</span><span class="sxs-lookup"><span data-stu-id="39ee7-164">Reach the container</span></span>

<span data-ttu-id="39ee7-165">In questo esempio l'applicazione è in esecuzione su un nodo dell'agente pubblico.</span><span class="sxs-lookup"><span data-stu-id="39ee7-165">In this example, the application is running on a public agent node.</span></span> <span data-ttu-id="39ee7-166">Si raggiunge l'applicazione da Internet passando al FQDN dell'agente del cluster `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, dove:</span><span class="sxs-lookup"><span data-stu-id="39ee7-166">You reach the application from the internet by browsing to the agent FQDN of the cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="39ee7-167">**DNSPREFIX** è il prefisso DNS specificato al momento della distribuzione del cluster.</span><span class="sxs-lookup"><span data-stu-id="39ee7-167">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>
* <span data-ttu-id="39ee7-168">**REGION** è l'area in cui si trova il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="39ee7-168">**REGION** is the region in which your resource group is located.</span></span>

    ![Nginx da Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="39ee7-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="39ee7-170">Next steps</span></span>
* [<span data-ttu-id="39ee7-171">Usare DC/OS e l'API Marathon</span><span class="sxs-lookup"><span data-stu-id="39ee7-171">Work with DC/OS and the Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="39ee7-172">Approfondimento sul servizio contenitore di Azure con Mesos</span><span class="sxs-lookup"><span data-stu-id="39ee7-172">Deep dive on the Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
