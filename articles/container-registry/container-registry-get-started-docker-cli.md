---
title: aaaPush Docker immagine tooprivate del Registro di sistema Azure | Documenti Microsoft
description: Push e pull immagini tooa contenitore privato del Registro di sistema in Azure utilizzando hello Docker CLI di Docker
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a><span data-ttu-id="8c878-103">La prima immagine tooa privata Docker contenitore del Registro di sistema utilizzando hello Docker CLI push</span><span class="sxs-lookup"><span data-stu-id="8c878-103">Push your first image tooa private Docker container registry using hello Docker CLI</span></span>
<span data-ttu-id="8c878-104">Un registro di sistema di contenitore di Azure archivia e gestisce privata [Docker](http://hub.docker.com) immagini contenitore, simile toohello modo [Hub Docker](https://hub.docker.com/) archivia le immagini Docker pubbliche.</span><span class="sxs-lookup"><span data-stu-id="8c878-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar toohello way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="8c878-105">Utilizzare hello [interfaccia della riga di comando di Docker](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) per [accesso](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/)e altre operazioni sul contenitore Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="8c878-105">You use hello [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="8c878-106">Per altre sfondo e i concetti, vedere [hello Panoramica](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="8c878-106">For more background and concepts, see [hello overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="8c878-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8c878-107">Prerequisites</span></span>
* <span data-ttu-id="8c878-108">**Registro di contenitori di Azure**: creare un registro di contenitori nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c878-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="8c878-109">Ad esempio, utilizzare hello [portale di Azure](container-registry-get-started-portal.md) o hello [CLI di Azure 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8c878-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="8c878-110">**Docker CLI** -tooset del computer locale come un host e accesso hello Docker CLI i comandi di Docker, installare [motore Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="8c878-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-tooa-registry"></a><span data-ttu-id="8c878-111">Accedi al Registro di sistema tooa</span><span class="sxs-lookup"><span data-stu-id="8c878-111">Log in tooa registry</span></span>
<span data-ttu-id="8c878-112">Eseguire `docker login` toolog nel Registro di sistema tooyour contenitore con il [le credenziali del Registro di sistema](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8c878-112">Run `docker login` toolog in tooyour container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="8c878-113">Hello seguente esempio passa hello ID e la password di Azure Active Directory [dell'entità servizio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="8c878-113">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="8c878-114">Ad esempio, è stato assegnato un registro di sistema tooyour dell'entità servizio per uno scenario di automazione.</span><span class="sxs-lookup"><span data-stu-id="8c878-114">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="8c878-115">Verificare nome completo del Registro di sistema di hello che toospecify (tutti in lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="8c878-115">Make sure toospecify hello fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="8c878-116">In questo esempio si tratta di `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="8c878-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-toopull-and-push-an-image"></a><span data-ttu-id="8c878-117">Passaggi toopull e inserire un'immagine</span><span class="sxs-lookup"><span data-stu-id="8c878-117">Steps toopull and push an image</span></span>
<span data-ttu-id="8c878-118">Hello seguire l'esempio download hello immagine Nginx da hello pubblica Hub Docker del Registro di sistema, i tag per il Registro di sistema contenitore privato di Azure, inserisce tooyour del Registro di sistema, quindi grado di estrarre nuovamente.</span><span class="sxs-lookup"><span data-stu-id="8c878-118">hello follow example downloads hello Nginx image from hello public Docker Hub registry, tags it for your private Azure container registry, pushes it tooyour registry, then pulls it again.</span></span>

<span data-ttu-id="8c878-119">**1. Pull immagine ufficiale di hello Docker per Nginx**</span><span class="sxs-lookup"><span data-stu-id="8c878-119">**1. Pull hello Docker official image for Nginx**</span></span>

<span data-ttu-id="8c878-120">Primo pull hello pubblica Nginx immagine tooyour computer locale.</span><span class="sxs-lookup"><span data-stu-id="8c878-120">First pull hello public Nginx image tooyour local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="8c878-121">**2. Avviare il contenitore Nginx hello**</span><span class="sxs-lookup"><span data-stu-id="8c878-121">**2. Start hello Nginx container**</span></span>

<span data-ttu-id="8c878-122">Hello comando seguente avvia hello locale Nginx contenitore in modo interattivo sulla porta 8080, consentendo di output toosee Nginx.</span><span class="sxs-lookup"><span data-stu-id="8c878-122">hello following command starts hello local Nginx container interactively on port 8080, allowing you toosee output from Nginx.</span></span> <span data-ttu-id="8c878-123">Rimuove hello in esecuzione una volta arrestato contenitore.</span><span class="sxs-lookup"><span data-stu-id="8c878-123">It removes hello running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="8c878-124">Sfoglia troppo[http://localhost:8080](http://localhost:8080) tooview hello in esecuzione contenitore.</span><span class="sxs-lookup"><span data-stu-id="8c878-124">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span> <span data-ttu-id="8c878-125">Viene visualizzato un toohello simile schermata segue quello.</span><span class="sxs-lookup"><span data-stu-id="8c878-125">You see a screen similar toohello following one.</span></span>

![Nginx sul computer locale](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="8c878-127">toostop hello contenitore in esecuzione, premere [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="8c878-127">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="8c878-128">**3. Creare un alias dell'immagine di hello nel Registro di sistema**</span><span class="sxs-lookup"><span data-stu-id="8c878-128">**3. Create an alias of hello image in your registry**</span></span>

<span data-ttu-id="8c878-129">Hello seguente comando crea un alias dell'immagine di hello, con un registro di sistema tooyour il percorso completo.</span><span class="sxs-lookup"><span data-stu-id="8c878-129">hello following command creates an alias of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="8c878-130">In questo esempio specifica hello `samples` disordine tooavoid dello spazio dei nomi nella directory radice del Registro di sistema hello hello.</span><span class="sxs-lookup"><span data-stu-id="8c878-130">This example specifies hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="8c878-131">**4. Eseguire il push del Registro di sistema di hello immagine tooyour**</span><span class="sxs-lookup"><span data-stu-id="8c878-131">**4. Push hello image tooyour registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="8c878-132">**5. Immagine di hello pull dal Registro di sistema**</span><span class="sxs-lookup"><span data-stu-id="8c878-132">**5. Pull hello image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="8c878-133">**6. Avviare il contenitore di Nginx hello dal Registro di sistema**</span><span class="sxs-lookup"><span data-stu-id="8c878-133">**6. Start hello Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="8c878-134">Sfoglia troppo[http://localhost:8080](http://localhost:8080) tooview hello in esecuzione contenitore.</span><span class="sxs-lookup"><span data-stu-id="8c878-134">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span>

<span data-ttu-id="8c878-135">toostop hello contenitore in esecuzione, premere [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="8c878-135">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="8c878-136">**7. (Facoltativo) Rimuovere un'immagine di hello**</span><span class="sxs-lookup"><span data-stu-id="8c878-136">**7. (Optional) Remove hello image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="8c878-137">Limiti delle chiamate simultanee</span><span class="sxs-lookup"><span data-stu-id="8c878-137">Concurrent Limits</span></span>
<span data-ttu-id="8c878-138">In alcuni scenari, l'esecuzione di chiamate simultanee può provocare errori.</span><span class="sxs-lookup"><span data-stu-id="8c878-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="8c878-139">Hello nella tabella seguente contiene i limiti di hello di chiamate simultanee con operazioni "Push" e "Pull" del Registro di sistema di contenitore di Azure:</span><span class="sxs-lookup"><span data-stu-id="8c878-139">hello following table contains hello limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="8c878-140">Operazione</span><span class="sxs-lookup"><span data-stu-id="8c878-140">Operation</span></span>  | <span data-ttu-id="8c878-141">Limite</span><span class="sxs-lookup"><span data-stu-id="8c878-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="8c878-142">PULL</span><span class="sxs-lookup"><span data-stu-id="8c878-142">PULL</span></span>       | <span data-ttu-id="8c878-143">Backup too10 simultanee estrae al Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="8c878-143">Up too10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="8c878-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="8c878-144">PUSH</span></span>       | <span data-ttu-id="8c878-145">Backup too5 simultanee inserisce al Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="8c878-145">Up too5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8c878-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c878-146">Next steps</span></span>
<span data-ttu-id="8c878-147">Ora che si conoscono i concetti di base hello, si è pronti toostart mediante il Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="8c878-147">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="8c878-148">Ad esempio, iniziare la distribuzione di contenitore immagini tooan [servizio contenitore di Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span><span class="sxs-lookup"><span data-stu-id="8c878-148">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
