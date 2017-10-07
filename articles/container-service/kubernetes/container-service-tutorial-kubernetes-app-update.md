---
title: esercitazione per il servizio contenitore aaaAzure - l'applicazione di aggiornamento | Documenti Microsoft
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
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="7dd9c-104">Aggiornare un'applicazione in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7dd9c-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="7dd9c-105">Dopo aver distribuito un'applicazione in Kubernetes, è possibile aggiornarla specificando una nuova immagine del contenitore o una nuova versione dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="7dd9c-106">Quando si aggiorna un'applicazione, implementazione di update hello viene gestita in modo che solo una parte della distribuzione hello verrà aggiornata contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-106">When you update an application, hello update rollout is staged so that only a portion of hello deployment is concurrently updated.</span></span> <span data-ttu-id="7dd9c-107">Questo aggiornamento per la gestione temporanea consente tookeep applicazione hello in esecuzione durante l'aggiornamento di hello e fornisce un meccanismo di rollback se si verifica un errore di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-107">This staged update enables hello application tookeep running during hello update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="7dd9c-108">In questa esercitazione, parte 6 di sette, app di Azure voto esempio hello viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-108">In this tutorial, part six of seven, hello sample Azure Vote app is updated.</span></span> <span data-ttu-id="7dd9c-109">Le attività da completare comprendono:</span><span class="sxs-lookup"><span data-stu-id="7dd9c-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7dd9c-110">Aggiornamento del codice dell'applicazione front-end hello</span><span class="sxs-lookup"><span data-stu-id="7dd9c-110">Updating hello front-end application code</span></span>
> * <span data-ttu-id="7dd9c-111">Creazione di un'immagine del contenitore aggiornata</span><span class="sxs-lookup"><span data-stu-id="7dd9c-111">Creating an updated container image</span></span>
> * <span data-ttu-id="7dd9c-112">Push hello contenitore immagine tooAzure contenitore del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="7dd9c-112">Pushing hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="7dd9c-113">Distribuzione immagine contenitore aggiornato hello</span><span class="sxs-lookup"><span data-stu-id="7dd9c-113">Deploying hello updated container image</span></span>

<span data-ttu-id="7dd9c-114">Nelle esercitazioni successive, Operations Management Suite è cluster Kubernetes di hello toomonitor configurato.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-114">In subsequent tutorials, Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7dd9c-115">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="7dd9c-115">Before you begin</span></span>

<span data-ttu-id="7dd9c-116">Nelle esercitazioni precedenti, un'applicazione è stata distribuita in un'immagine contenitore, immagine hello caricato tooAzure contenitore del Registro di sistema e un cluster Kubernetes creato.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-116">In previous tutorials, an application was packaged into a container image, hello image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="7dd9c-117">un'applicazione Hello quindi è stata eseguita nel cluster Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-117">hello application was then run on hello Kubernetes cluster.</span></span> 

<span data-ttu-id="7dd9c-118">Se non sono state completate le operazioni di toofollow lungo, restituire troppo[esercitazione 1: creare le immagini contenitore](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="7dd9c-118">If you haven't completed these steps, and want toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="7dd9c-119">Aggiornare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="7dd9c-119">Update application</span></span>

<span data-ttu-id="7dd9c-120">passaggi di hello toocomplete in questa esercitazione, deve avere una copia clonata di hello applicazione Azure voto.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-120">toocomplete hello steps in this tutorial, you must have cloned a copy of hello Azure Vote application.</span></span> <span data-ttu-id="7dd9c-121">Se necessario, creare la copia clonata con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7dd9c-121">If necessary, create this cloned copy with hello following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="7dd9c-122">Aprire hello `config_file.cfg` file con qualsiasi editor di testo o codice.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-122">Open hello `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="7dd9c-123">È possibile trovare questo file nella seguente directory di repository clonato hello hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-123">You can find this file under hello following directory of hello cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="7dd9c-124">Modificare i valori hello per `VOTE1VALUE` e `VOTE2VALUE`e quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-124">Change hello values for `VOTE1VALUE` and `VOTE2VALUE`, and then save hello file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="7dd9c-125">Utilizzare [comporre docker](https://docs.docker.com/compose/) toore-creare immagine front-end hello e un'applicazione hello esecuzione aggiornato.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-125">Use [docker-compose](https://docs.docker.com/compose/) toore-create hello front-end image and run hello updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="7dd9c-126">Testare l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="7dd9c-126">Test application locally</span></span>

<span data-ttu-id="7dd9c-127">Sfoglia troppo`http://localhost:8080` toosee hello applicazione aggiornata.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-127">Browse too`http://localhost:8080` toosee hello updated application.</span></span>

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="7dd9c-129">Applicare tag ed eseguire il push delle immagini</span><span class="sxs-lookup"><span data-stu-id="7dd9c-129">Tag and push images</span></span>

<span data-ttu-id="7dd9c-130">Hello tag *azure voto-anteriore* immagine con loginServer hello del Registro di sistema di hello contenitore.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-130">Tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span>

<span data-ttu-id="7dd9c-131">Se si usa Azure del Registro di sistema contenitore, ottenere il nome di server di accesso di hello con hello [elenco acr az](/cli/azure/acr#list) comando.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-131">If you're using Azure Container Registry, get hello login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="7dd9c-132">Utilizzare [tag docker](https://docs.docker.com/engine/reference/commandline/tag/) immagine hello tootag.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello image.</span></span> <span data-ttu-id="7dd9c-133">Sostituire `<acrLoginServer>` con il nome di accesso del server del Registro contenitori di Azure o un nome host di un registro pubblico.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="7dd9c-134">Utilizzare [push di docker](https://docs.docker.com/engine/reference/commandline/push/) Registro di sistema tooupload hello immagine tooyour.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello image tooyour registry.</span></span> <span data-ttu-id="7dd9c-135">Sostituire `<acrLoginServer>` con il nome di accesso del server del Registro contenitori di Azure o un nome host di un registro pubblico.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="7dd9c-136">Distribuire l'aggiornamento dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="7dd9c-136">Deploy update application</span></span>

<span data-ttu-id="7dd9c-137">tempi tooensure più istanze di pod applicazione hello devono essere in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-137">tooensure maximum uptime, multiple instances of hello application pod must be running.</span></span> <span data-ttu-id="7dd9c-138">Verificare la configurazione con hello [kubectl ottenere pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-138">Verify this configuration with hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="7dd9c-139">Output:</span><span class="sxs-lookup"><span data-stu-id="7dd9c-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="7dd9c-140">Se non si dispone di più POD che esegue l'immagine di azure-anteriore voto hello, applicare la scalabilità hello *azure voto-anteriore* distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-140">If you don't have multiple pods running hello azure-vote-front image, scale hello *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="7dd9c-141">un'applicazione hello tooupdate, utilizzare hello [set kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) comando.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-141">tooupdate hello application, use hello [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="7dd9c-142">Aggiornamento `<acrLoginServer>` con hello account di accesso server o il nome host contenitore del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-142">Update `<acrLoginServer>` with hello login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="7dd9c-143">distribuzione di hello toomonitor, utilizzare hello [kubectl ottenere pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-143">toomonitor hello deployment, use hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="7dd9c-144">Come un'applicazione hello aggiornato viene distribuita, le unità vengono terminate e ricreato con nuova immagine contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-144">As hello updated application is deployed, your pods are terminated and re-created with hello new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="7dd9c-145">Output:</span><span class="sxs-lookup"><span data-stu-id="7dd9c-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="7dd9c-146">Testare l'applicazione aggiornata</span><span class="sxs-lookup"><span data-stu-id="7dd9c-146">Test updated application</span></span>

<span data-ttu-id="7dd9c-147">Ottenere l'indirizzo IP esterno hello di hello *azure voto-anteriore* servizio.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-147">Get hello external IP address of hello *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="7dd9c-148">Sfoglia toohello IP indirizzo toosee hello applicazione aggiornata.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-148">Browse toohello IP address toosee hello updated application.</span></span>

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="7dd9c-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7dd9c-150">Next steps</span></span>

<span data-ttu-id="7dd9c-151">In questa esercitazione, si aggiornata un'applicazione e il cluster di aggiornamento tooa Kubernetes di implementazione.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-151">In this tutorial, you updated an application and rolled out this update tooa Kubernetes cluster.</span></span> <span data-ttu-id="7dd9c-152">sono stata completata Hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="7dd9c-152">hello following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7dd9c-153">Codice dell'applicazione front-end hello aggiornato</span><span class="sxs-lookup"><span data-stu-id="7dd9c-153">Updated hello front-end application code</span></span>
> * <span data-ttu-id="7dd9c-154">Creazione di un'immagine del contenitore aggiornata</span><span class="sxs-lookup"><span data-stu-id="7dd9c-154">Created an updated container image</span></span>
> * <span data-ttu-id="7dd9c-155">Inserito hello contenitore immagine tooAzure contenitore del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="7dd9c-155">Pushed hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="7dd9c-156">Applicazione distribuita hello aggiornato</span><span class="sxs-lookup"><span data-stu-id="7dd9c-156">Deployed hello updated application</span></span>

<span data-ttu-id="7dd9c-157">Toohello Avanti toolearn esercitazione su come spostare toomonitor Kubernetes con Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="7dd9c-157">Advance toohello next tutorial toolearn about how toomonitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7dd9c-158">Monitorare Kubernetes con OMS</span><span class="sxs-lookup"><span data-stu-id="7dd9c-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)