---
title: aaaManage Kubernetes Azure cluster con interfaccia utente web | Documenti Microsoft
description: Utilizzo di hello Kubernetes web dell'interfaccia utente nel servizio contenitore di Azure
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
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="a334d-103">Utilizzo di hello Kubernetes web dell'interfaccia utente con il servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="a334d-103">Using hello Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a334d-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a334d-104">Prerequisites</span></span>
<span data-ttu-id="a334d-105">Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a334d-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="a334d-106">Si presuppone inoltre di aver hello Azure CLI 2.0 e `kubectl` installati gli strumenti.</span><span class="sxs-lookup"><span data-stu-id="a334d-106">It also assumes that you have hello Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="a334d-107">È possibile verificare se si dispone di hello `az` strumento installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="a334d-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="a334d-108">Se non si dispone di hello `az` strumento installato, non esistono istruzioni [qui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="a334d-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="a334d-109">È possibile verificare se si dispone di hello `kubectl` strumento installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="a334d-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="a334d-110">Se `kubectl` non è installato, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="a334d-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="a334d-111">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a334d-111">Overview</span></span>

### <a name="connect-toohello-web-ui"></a><span data-ttu-id="a334d-112">Connettere l'interfaccia utente web toohello</span><span class="sxs-lookup"><span data-stu-id="a334d-112">Connect toohello web UI</span></span>
<span data-ttu-id="a334d-113">È possibile avviare l'interfaccia utente web di Kubernetes hello eseguendo:</span><span class="sxs-lookup"><span data-stu-id="a334d-113">You can launch hello Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="a334d-114">Verrà aperto un web browser configurato tootalk tooa proxy sicuro connessione web Kubernetes toohello computer locale dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="a334d-114">This should open a web browser configured tootalk tooa secure proxy connecting your local machine toohello Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="a334d-115">Creare ed esporre un servizio</span><span class="sxs-lookup"><span data-stu-id="a334d-115">Create and expose a service</span></span>
1. <span data-ttu-id="a334d-116">Nell'interfaccia utente web di Kubernetes hello, fare clic su **crea** pulsante nella finestra di destra superiore hello.</span><span class="sxs-lookup"><span data-stu-id="a334d-116">In hello Kubernetes web UI, click **Create** button in hello upper right window.</span></span>

    ![Interfaccia utente di creazione Kubernetes](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="a334d-118">Viene visualizzata una finestra di dialogo in cui è possibile iniziare a creare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a334d-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="a334d-119">Assegnargli il nome di hello `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="a334d-119">Give it hello name `hello-nginx`.</span></span> <span data-ttu-id="a334d-120">Hello utilizzare [ `nginx` contenitore da Docker](https://hub.docker.com/_/nginx/) e distribuire i tre repliche di questo servizio web.</span><span class="sxs-lookup"><span data-stu-id="a334d-120">Use hello [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Finestra di dialogo Pod Create Kubernetes (Crea podcast Kubernetes)](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="a334d-122">In **Service** (Servizio) selezionare **External** (Esterno) e inserire la porta 80.</span><span class="sxs-lookup"><span data-stu-id="a334d-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="a334d-123">Questa impostazione di bilanciamento del carico tre repliche di traffico toohello.</span><span class="sxs-lookup"><span data-stu-id="a334d-123">This setting load-balances traffic toohello three replicas.</span></span>

    ![Finestra di dialogo Kubernetes Service Create (Crea servizio Kubernetes)](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="a334d-125">Fare clic su **Distribuisci** toodeploy questi contenitori e i servizi.</span><span class="sxs-lookup"><span data-stu-id="a334d-125">Click **Deploy** toodeploy these containers and services.</span></span>

    ![Distribuzione di Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="a334d-127">Visualizzare i contenitori</span><span class="sxs-lookup"><span data-stu-id="a334d-127">View your containers</span></span>
<span data-ttu-id="a334d-128">Dopo aver fatto clic **Distribuisci**, hello dell'interfaccia utente mostra una visualizzazione del servizio, come la distribuzione:</span><span class="sxs-lookup"><span data-stu-id="a334d-128">After you click **Deploy**, hello UI shows a view of your service as it deploys:</span></span>

![Stato di Kubernetes](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="a334d-130">È possibile visualizzare lo stato di hello di ciascun oggetto Kubernetes cerchio hello nella parte sinistra dell'interfaccia utente, hello in **POD**.</span><span class="sxs-lookup"><span data-stu-id="a334d-130">You can see hello status of each Kubernetes object in hello circle on hello left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="a334d-131">Se è un cerchio completo parzialmente, oggetto hello comunque la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a334d-131">If it is a partially full circle, then hello object is still deploying.</span></span> <span data-ttu-id="a334d-132">Quando un oggetto è completamente distribuito, viene visualizzato un segno di spunta verde:</span><span class="sxs-lookup"><span data-stu-id="a334d-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes distribuito](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="a334d-134">Una volta tutto ciò che è in esecuzione, fare clic su uno dei tuoi toosee POD su hello in esecuzione il servizio web.</span><span class="sxs-lookup"><span data-stu-id="a334d-134">Once everything is running, click one of your pods toosee details about hello running web service.</span></span>

![Podcast Kubernetes](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="a334d-136">In hello **POD** , è possibile visualizzare informazioni sui contenitori di hello pod hello, nonché le risorse di CPU e memoria hello utilizzate da tali contenitori:</span><span class="sxs-lookup"><span data-stu-id="a334d-136">In hello **Pods** view, you can see information about hello containers in hello pod as well as hello CPU and memory resources used by those containers:</span></span>

![Risorse Kubernetes](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="a334d-138">Se le risorse di hello non viene visualizzata, potrebbe essere toowait alcuni minuti per hello toopropagate dati di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="a334d-138">If you don't see hello resources, you may need toowait a few minutes for hello monitoring data toopropagate.</span></span>

<span data-ttu-id="a334d-139">toosee hello log per il contenitore, fare clic su **visualizzare log**.</span><span class="sxs-lookup"><span data-stu-id="a334d-139">toosee hello logs for your container, click **View logs**.</span></span>

![Log Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="a334d-141">Visualizzazione del servizio</span><span class="sxs-lookup"><span data-stu-id="a334d-141">Viewing your service</span></span>
<span data-ttu-id="a334d-142">In aggiunta toorunning ai contenitori, hello Kubernetes UI ha creato un riferimento esterno `Service` che esegue il provisioning di un carico del servizio di bilanciamento toobring traffico toohello contenitori il cluster.</span><span class="sxs-lookup"><span data-stu-id="a334d-142">In addition toorunning your containers, hello Kubernetes UI has created an external `Service` which provisions a load balancer toobring traffic toohello containers in your cluster.</span></span>

<span data-ttu-id="a334d-143">Nel riquadro di spostamento a sinistra di hello, fare clic su **servizi** tooview tutti i servizi (deve essere presente solo uno).</span><span class="sxs-lookup"><span data-stu-id="a334d-143">In hello left navigation pane, click **Services** tooview all services (there should be only one).</span></span>

![Servizi Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="a334d-145">In tale visualizzazione, verrà visualizzato un endpoint esterno (indirizzo IP) che è stato allocato il servizio tooyour.</span><span class="sxs-lookup"><span data-stu-id="a334d-145">In that view, you should see an external endpoint (IP address) that has been allocated tooyour service.</span></span>
<span data-ttu-id="a334d-146">Se si fa clic su tale indirizzo IP, si noterà il contenitore Nginx in esecuzione dietro il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="a334d-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![Visualizzazione di nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="a334d-148">Ridimensionamento del servizio</span><span class="sxs-lookup"><span data-stu-id="a334d-148">Resizing your service</span></span>
<span data-ttu-id="a334d-149">In aggiunta tooviewing degli oggetti in hello dell'interfaccia utente, è possibile modificare e aggiornare gli oggetti API Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="a334d-149">In addition tooviewing your objects in hello UI, you can edit and update hello Kubernetes API objects.</span></span>

<span data-ttu-id="a334d-150">In primo luogo, fare clic su **distribuzioni** in hello lasciato navigazione riquadro toosee hello la distribuzione per il servizio.</span><span class="sxs-lookup"><span data-stu-id="a334d-150">First, click **Deployments** in hello left navigation pane toosee hello deployment for your service.</span></span>

<span data-ttu-id="a334d-151">Una volta in tale visualizzazione, fare clic sul set di repliche hello e quindi fare clic su **modifica** nella barra di spostamento superiore hello:</span><span class="sxs-lookup"><span data-stu-id="a334d-151">Once you are in that view, click on hello replica set, and then click **Edit** in hello upper navigation bar:</span></span>

![Modifica di Kubernetes](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="a334d-153">Modifica hello `spec.replicas` campo toobe `2`, fare clic su **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="a334d-153">Edit hello `spec.replicas` field toobe `2`, and click **Update**.</span></span>

<span data-ttu-id="a334d-154">In questo modo il numero di hello di repliche toodrop tootwo eliminando una del POD.</span><span class="sxs-lookup"><span data-stu-id="a334d-154">This causes hello number of replicas toodrop tootwo by deleting one of your pods.</span></span>

 

