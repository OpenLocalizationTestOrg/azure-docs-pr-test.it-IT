---
title: Esercitazione per il servizio contenitore di Azure - Aggiornare un'applicazione | Microsoft Docs
description: Esercitazione per il servizio contenitore di Azure - Aggiornare un'applicazione
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: db580da3e2d70892bc37305394df5be609ebb8a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="6a4b5-104">Aggiornare un'applicazione in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6a4b5-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="6a4b5-105">Dopo aver distribuito un'applicazione in Kubernetes, è possibile aggiornarla specificando una nuova immagine del contenitore o una nuova versione dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="6a4b5-106">Quando si aggiorna un'applicazione, viene eseguito lo staging dell'implementazione dell'aggiornamento, in modo che solo una parte della distribuzione sia aggiornata contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-106">When you update an application, the update rollout is staged so that only a portion of the deployment is concurrently updated.</span></span> <span data-ttu-id="6a4b5-107">Questo aggiornamento in staging consente all'applicazione di continuare la sua esecuzione durante l'aggiornamento e fornisce un meccanismo di rollback in caso si verifichi un errore nella distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-107">This staged update enables the application to keep running during the update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="6a4b5-108">In questa esercitazione, parte sei di sette, viene aggiornata l'app Azure Vote di esempio.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span></span> <span data-ttu-id="6a4b5-109">Le attività da completare comprendono:</span><span class="sxs-lookup"><span data-stu-id="6a4b5-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6a4b5-110">Aggiornamento del codice dell'applicazione front-end</span><span class="sxs-lookup"><span data-stu-id="6a4b5-110">Updating the front-end application code</span></span>
> * <span data-ttu-id="6a4b5-111">Creazione di un'immagine del contenitore aggiornata</span><span class="sxs-lookup"><span data-stu-id="6a4b5-111">Creating an updated container image</span></span>
> * <span data-ttu-id="6a4b5-112">Push dell'immagine del contenitore in Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="6a4b5-112">Pushing the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="6a4b5-113">Distribuzione di un'immagine del contenitore aggiornata</span><span class="sxs-lookup"><span data-stu-id="6a4b5-113">Deploying the updated container image</span></span>

<span data-ttu-id="6a4b5-114">Nelle esercitazioni successive, Operations Management Suite verrà configurato per monitorare il cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-114">In subsequent tutorials, Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6a4b5-115">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="6a4b5-115">Before you begin</span></span>

<span data-ttu-id="6a4b5-116">Nelle esercitazioni precedenti è stato creato un pacchetto di un'applicazione in un'immagine del contenitore, caricata poi in Registro contenitori di Azure, ed è stato creato un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-116">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="6a4b5-117">L'applicazione è stata quindi eseguita nel cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-117">The application was then run on the Kubernetes cluster.</span></span> 

<span data-ttu-id="6a4b5-118">Se questi passaggi non sono stati ancora eseguiti e si vuole procedere, tornare a [Esercitazione 1 - Creare immagini del contenitore](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="6a4b5-118">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="6a4b5-119">Aggiornare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="6a4b5-119">Update application</span></span>

<span data-ttu-id="6a4b5-120">Per completare i passaggi di questa esercitazione, è necessario avere clonato una copia dell'applicazione Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-120">To complete the steps in this tutorial, you must have cloned a copy of the Azure Vote application.</span></span> <span data-ttu-id="6a4b5-121">Se necessario, creare la copia clonata con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6a4b5-121">If necessary, create this cloned copy with the following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="6a4b5-122">Aprire il file `config_file.cfg` con qualsiasi editor di testo o codice.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-122">Open the `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="6a4b5-123">È possibile trovare questo file nella directory seguente del repository clonato.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-123">You can find this file under the following directory of the cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="6a4b5-124">Cambiare i valori per `VOTE1VALUE` e `VOTE2VALUE`, quindi salvare il file.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-124">Change the values for `VOTE1VALUE` and `VOTE2VALUE`, and then save the file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="6a4b5-125">Usare [docker-compose](https://docs.docker.com/compose/) per ricreare l'immagine front-end ed eseguire l'applicazione aggiornata.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-125">Use [docker-compose](https://docs.docker.com/compose/) to re-create the front-end image and run the updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="6a4b5-126">Testare l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="6a4b5-126">Test application locally</span></span>

<span data-ttu-id="6a4b5-127">Passare a `http://localhost:8080` per vedere l'applicazione aggiornata.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-127">Browse to `http://localhost:8080` to see the updated application.</span></span>

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="6a4b5-129">Applicare tag ed eseguire il push delle immagini</span><span class="sxs-lookup"><span data-stu-id="6a4b5-129">Tag and push images</span></span>

<span data-ttu-id="6a4b5-130">Applicare all'immagine *azure voto-anteriore* il tag loginServer del registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-130">Tag the *azure-vote-front* image with the loginServer of the container registry.</span></span>

<span data-ttu-id="6a4b5-131">Se si usa il Registro contenitori di Azure, ottenere il nome di accesso del server con il comando [az acr list](/cli/azure/acr#list).</span><span class="sxs-lookup"><span data-stu-id="6a4b5-131">If you're using Azure Container Registry, get the login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="6a4b5-132">Usare [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) per assegnare il tag all'immagine.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) to tag the image.</span></span> <span data-ttu-id="6a4b5-133">Sostituire `<acrLoginServer>` con il nome di accesso del server del Registro contenitori di Azure o un nome host di un registro pubblico.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="6a4b5-134">Usare [docker push](https://docs.docker.com/engine/reference/commandline/push/) per caricare l'immagine nel registro.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) to upload the image to your registry.</span></span> <span data-ttu-id="6a4b5-135">Sostituire `<acrLoginServer>` con il nome di accesso del server del Registro contenitori di Azure o un nome host di un registro pubblico.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="6a4b5-136">Distribuire l'aggiornamento dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="6a4b5-136">Deploy update application</span></span>

<span data-ttu-id="6a4b5-137">Per garantire il tempo di attività massimo, è necessario eseguire più istanze del pod dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-137">To ensure maximum uptime, multiple instances of the application pod must be running.</span></span> <span data-ttu-id="6a4b5-138">Verificare questa configurazione con il comando [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="6a4b5-138">Verify this configuration with the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="6a4b5-139">Output:</span><span class="sxs-lookup"><span data-stu-id="6a4b5-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="6a4b5-140">Se non si dispone di più pod che eseguono l'immagine azure-vote-front, scalare la distribuzione *azure-vote-front*.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-140">If you don't have multiple pods running the azure-vote-front image, scale the *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="6a4b5-141">Per aggiornare l'applicazione, usare il comando [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set).</span><span class="sxs-lookup"><span data-stu-id="6a4b5-141">To update the application, use the [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="6a4b5-142">Aggiornare `<acrLoginServer>` con il server di accesso o il nome host del registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-142">Update `<acrLoginServer>` with the login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="6a4b5-143">Per monitorare la distribuzione, utilizzare il comando [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="6a4b5-143">To monitor the deployment, use the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="6a4b5-144">Quando l'applicazione aggiornata viene distribuita, le unità vengono terminate e ricreate con la nuova immagine del contenitore.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-144">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="6a4b5-145">Output:</span><span class="sxs-lookup"><span data-stu-id="6a4b5-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="6a4b5-146">Testare l'applicazione aggiornata</span><span class="sxs-lookup"><span data-stu-id="6a4b5-146">Test updated application</span></span>

<span data-ttu-id="6a4b5-147">Ottenere l'indirizzo IP esterno del servizio *azure-vote-front*.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-147">Get the external IP address of the *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="6a4b5-148">Passare all'indirizzo IP per vedere l'applicazione aggiornata.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-148">Browse to the IP address to see the updated application.</span></span>

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="6a4b5-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a4b5-150">Next steps</span></span>

<span data-ttu-id="6a4b5-151">In questa esercitazione è stata aggiornata un'applicazione e l'aggiornamento è stato distribuito in un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-151">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span></span> <span data-ttu-id="6a4b5-152">Sono state completate le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a4b5-152">The following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6a4b5-153">Aggiornamento del codice dell'applicazione front-end</span><span class="sxs-lookup"><span data-stu-id="6a4b5-153">Updated the front-end application code</span></span>
> * <span data-ttu-id="6a4b5-154">Creazione di un'immagine del contenitore aggiornata</span><span class="sxs-lookup"><span data-stu-id="6a4b5-154">Created an updated container image</span></span>
> * <span data-ttu-id="6a4b5-155">Push dell'immagine del contenitore in Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="6a4b5-155">Pushed the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="6a4b5-156">Distribuzione dell'applicazione aggiornata</span><span class="sxs-lookup"><span data-stu-id="6a4b5-156">Deployed the updated application</span></span>

<span data-ttu-id="6a4b5-157">Passare alla prossima esercitazione per apprendere come monitorare Kubernetes con Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="6a4b5-157">Advance to the next tutorial to learn about how to monitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a4b5-158">Monitorare Kubernetes con OMS</span><span class="sxs-lookup"><span data-stu-id="6a4b5-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)