---
title: Gestire un cluster Azure Kubernetes con l'interfaccia utente Web | Documentazione Microsoft
description: Uso dell'interfaccia utente Web Kubernetes nel servizio contenitore di Azure
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e31f90d61fc61f17582372fe9f491a1e21f628b0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="b4903-103">Uso dell'interfaccia utente Web Kubernetes con il servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="b4903-103">Using the Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4903-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b4903-104">Prerequisites</span></span>
<span data-ttu-id="b4903-105">Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="b4903-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="b4903-106">Si presume anche che l'interfaccia della riga di comando di Azure 2.0 e gli strumenti `kubectl` siano installati.</span><span class="sxs-lookup"><span data-stu-id="b4903-106">It also assumes that you have the Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="b4903-107">È possibile verificare se lo strumento `az` è installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="b4903-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="b4903-108">Se lo strumento `az` non è installato, le istruzioni sono disponibili [qui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="b4903-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="b4903-109">È possibile verificare se lo strumento `kubectl` è installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="b4903-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="b4903-110">Se `kubectl` non è installato, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="b4903-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="b4903-111">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b4903-111">Overview</span></span>

### <a name="connect-to-the-web-ui"></a><span data-ttu-id="b4903-112">Connettersi all'interfaccia utente Web</span><span class="sxs-lookup"><span data-stu-id="b4903-112">Connect to the web UI</span></span>
<span data-ttu-id="b4903-113">È possibile avviare l'interfaccia utente Web Kubernetes eseguendo:</span><span class="sxs-lookup"><span data-stu-id="b4903-113">You can launch the Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="b4903-114">Viene aperto un Web browser configurato per comunicare con un proxy sicuro che connette il computer locale all'interfaccia utente Web Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b4903-114">This should open a web browser configured to talk to a secure proxy connecting your local machine to the Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="b4903-115">Creare ed esporre un servizio</span><span class="sxs-lookup"><span data-stu-id="b4903-115">Create and expose a service</span></span>
1. <span data-ttu-id="b4903-116">Nell'interfaccia utente Web Kubernetes, fare clic sul pulsante **Create** (Crea) nella finestra in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="b4903-116">In the Kubernetes web UI, click **Create** button in the upper right window.</span></span>

    ![Interfaccia utente di creazione Kubernetes](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="b4903-118">Viene visualizzata una finestra di dialogo in cui è possibile iniziare a creare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b4903-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="b4903-119">Assegnare il nome `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="b4903-119">Give it the name `hello-nginx`.</span></span> <span data-ttu-id="b4903-120">Utilizzare il contenitore [ `nginx` da Docker](https://hub.docker.com/_/nginx/) e distribuire tre repliche del servizio web.</span><span class="sxs-lookup"><span data-stu-id="b4903-120">Use the [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Finestra di dialogo Pod Create Kubernetes (Crea podcast Kubernetes)](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="b4903-122">In **Service** (Servizio) selezionare **External** (Esterno) e inserire la porta 80.</span><span class="sxs-lookup"><span data-stu-id="b4903-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="b4903-123">Questa impostazione bilancia il carico del traffico verso le tre repliche.</span><span class="sxs-lookup"><span data-stu-id="b4903-123">This setting load-balances traffic to the three replicas.</span></span>

    ![Finestra di dialogo Kubernetes Service Create (Crea servizio Kubernetes)](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="b4903-125">Fare clic su **Deploy** (Distribuisci) per distribuire questi contenitori e servizi.</span><span class="sxs-lookup"><span data-stu-id="b4903-125">Click **Deploy** to deploy these containers and services.</span></span>

    ![Distribuzione di Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="b4903-127">Visualizzare i contenitori</span><span class="sxs-lookup"><span data-stu-id="b4903-127">View your containers</span></span>
<span data-ttu-id="b4903-128">Dopo aver fatto clic su **Deploy** (Distribuisci), l'interfaccia utente mostra una visualizzazione del servizio distribuito:</span><span class="sxs-lookup"><span data-stu-id="b4903-128">After you click **Deploy**, the UI shows a view of your service as it deploys:</span></span>

![Stato di Kubernetes](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="b4903-130">È possibile visualizzare lo stato di ciascun oggetto Kubernetes nel cerchio sul lato sinistro dell'interfaccia utente, in **Pods** (Pod).</span><span class="sxs-lookup"><span data-stu-id="b4903-130">You can see the status of each Kubernetes object in the circle on the left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="b4903-131">Se il cerchio è parzialmente completo, l'oggetto è ancora in fase di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b4903-131">If it is a partially full circle, then the object is still deploying.</span></span> <span data-ttu-id="b4903-132">Quando un oggetto è completamente distribuito, viene visualizzato un segno di spunta verde:</span><span class="sxs-lookup"><span data-stu-id="b4903-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes distribuito](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="b4903-134">Quanto tutto è in esecuzione, fare clic su uno dei pod per visualizzare i dettagli relativi al servizio Web in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b4903-134">Once everything is running, click one of your pods to see details about the running web service.</span></span>

![Podcast Kubernetes](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="b4903-136">Nella vista **Pods** (Pod), è possibile visualizzare le informazioni sui contenitori nel pod e le risorse di CPU e di memoria usate da questi contenitori:</span><span class="sxs-lookup"><span data-stu-id="b4903-136">In the **Pods** view, you can see information about the containers in the pod as well as the CPU and memory resources used by those containers:</span></span>

![Risorse Kubernetes](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="b4903-138">Se le risorse non vengono visualizzate, potrebbe essere necessario attendere alcuni minuti per propagare i dati di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="b4903-138">If you don't see the resources, you may need to wait a few minutes for the monitoring data to propagate.</span></span>

<span data-ttu-id="b4903-139">Per visualizzare i log relativi al contenitore, fare clic su **View logs** (Visualizza log).</span><span class="sxs-lookup"><span data-stu-id="b4903-139">To see the logs for your container, click **View logs**.</span></span>

![Log Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="b4903-141">Visualizzazione del servizio</span><span class="sxs-lookup"><span data-stu-id="b4903-141">Viewing your service</span></span>
<span data-ttu-id="b4903-142">Oltre a eseguire i contenitori, l'interfaccia utente di Kubernetes ha creato un riferimento esterno `Service` che esegue il provisioning di un bilanciamento del carico per portare il traffico ai contenitori all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="b4903-142">In addition to running your containers, the Kubernetes UI has created an external `Service` which provisions a load balancer to bring traffic to the containers in your cluster.</span></span>

<span data-ttu-id="b4903-143">Nel riquadro di spostamento a sinistra, fare clic su **Services** (Servizi) per visualizzare tutti i servizi (deve essere presente solo un servizio).</span><span class="sxs-lookup"><span data-stu-id="b4903-143">In the left navigation pane, click **Services** to view all services (there should be only one).</span></span>

![Servizi Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="b4903-145">In tale visualizzazione, dovrebbe essere visualizzato un endpoint esterno (indirizzo IP) che è stato allocato al servizio.</span><span class="sxs-lookup"><span data-stu-id="b4903-145">In that view, you should see an external endpoint (IP address) that has been allocated to your service.</span></span>
<span data-ttu-id="b4903-146">Se si fa clic su tale indirizzo IP, si noterà il contenitore Nginx in esecuzione dietro il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="b4903-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![Visualizzazione di nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="b4903-148">Ridimensionamento del servizio</span><span class="sxs-lookup"><span data-stu-id="b4903-148">Resizing your service</span></span>
<span data-ttu-id="b4903-149">Oltre a visualizzare gli oggetti nell'interfaccia utente, è possibile modificare e aggiornare gli oggetti API di Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b4903-149">In addition to viewing your objects in the UI, you can edit and update the Kubernetes API objects.</span></span>

<span data-ttu-id="b4903-150">Innanzitutto, fare clic su **Deployments** (Distribuzioni) nel riquadro di navigazione a sinistra per visualizzare la distribuzione relativa al servizio.</span><span class="sxs-lookup"><span data-stu-id="b4903-150">First, click **Deployments** in the left navigation pane to see the deployment for your service.</span></span>

<span data-ttu-id="b4903-151">Una volta aperta la visualizzazione, fare clic sul set di repliche, quindi sul pulsante **Edit** (Modifica) nella barra di navigazione superiore:</span><span class="sxs-lookup"><span data-stu-id="b4903-151">Once you are in that view, click on the replica set, and then click **Edit** in the upper navigation bar:</span></span>

![Modifica di Kubernetes](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="b4903-153">Impostare il campo `spec.replicas` su `2` e fare clic su **Update** (Aggiorna).</span><span class="sxs-lookup"><span data-stu-id="b4903-153">Edit the `spec.replicas` field to be `2`, and click **Update**.</span></span>

<span data-ttu-id="b4903-154">In questo modo il numero di repliche si riduce a due eliminando uno dei pod.</span><span class="sxs-lookup"><span data-stu-id="b4903-154">This causes the number of replicas to drop to two by deleting one of your pods.</span></span>

 

