---
title: Effettuare il push di un'immagine Docker in un registro di Azure privato | Microsoft Docs
description: Effettuare il push e il pull di immagini Docker in un registro di contenitori privati in Azure tramite l'interfaccia della riga di comando di Docker
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
ms.openlocfilehash: 07d4d72e94eda02e8594dfddb0e911eb0e63012d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="push-your-first-image-to-a-private-docker-container-registry-using-the-docker-cli"></a><span data-ttu-id="889cb-103">Effettuare il push della prima immagine in un registro per contenitori Docker privati tramite l'interfaccia della riga di comando di Docker</span><span class="sxs-lookup"><span data-stu-id="889cb-103">Push your first image to a private Docker container registry using the Docker CLI</span></span>
<span data-ttu-id="889cb-104">Un registro di contenitori di Azure archivia e gestisce le immagini dei contenitori [Docker](http://hub.docker.com) private, in modo analogo a come [Docker Hub](https://hub.docker.com/) archivia le immagini Docker pubbliche.</span><span class="sxs-lookup"><span data-stu-id="889cb-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar to the way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="889cb-105">Usare l'[interfaccia della riga di comando di Docker](https://docs.docker.com/engine/reference/commandline/cli/) per eseguire l'[accesso](https://docs.docker.com/engine/reference/commandline/login/), il [push](https://docs.docker.com/engine/reference/commandline/push/), il [pull](https://docs.docker.com/engine/reference/commandline/pull/) e altre operazioni sul registro di contenitori.</span><span class="sxs-lookup"><span data-stu-id="889cb-105">You use the [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="889cb-106">Per altre informazioni di base e concetti, vedere la [panoramica](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="889cb-106">For more background and concepts, see [the overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="889cb-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="889cb-107">Prerequisites</span></span>
* <span data-ttu-id="889cb-108">**Registro di contenitori di Azure**: creare un registro di contenitori nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="889cb-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="889cb-109">Ad esempio, usare il [Portale di Azure](container-registry-get-started-portal.md) o l'[interfaccia della riga di comando di Azure 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="889cb-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="889cb-110">**Interfaccia della riga di comando di Docker**: per configurare il computer locale come host Docker e accedere ai comandi della riga di comando di Docker, installare [Docker Engine](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="889cb-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-to-a-registry"></a><span data-ttu-id="889cb-111">Accedere a un registro</span><span class="sxs-lookup"><span data-stu-id="889cb-111">Log in to a registry</span></span>
<span data-ttu-id="889cb-112">Eseguire `docker login` per accedere al registro di contenitori con le [credenziali del registro](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="889cb-112">Run `docker login` to log in to your container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="889cb-113">L'esempio seguente passa l'ID e la password di un'[entità servizio](../active-directory/active-directory-application-objects.md) di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="889cb-113">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="889cb-114">Ad esempio, è possibile che sia stata assegnata un'entità servizio al registro per uno scenario di automazione.</span><span class="sxs-lookup"><span data-stu-id="889cb-114">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="889cb-115">Assicurarsi di specificare il nome del registro completo (tutto in lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="889cb-115">Make sure to specify the fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="889cb-116">In questo esempio si tratta di `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="889cb-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-to-pull-and-push-an-image"></a><span data-ttu-id="889cb-117">Passaggi per effettuare il pull e il push di un'immagine</span><span class="sxs-lookup"><span data-stu-id="889cb-117">Steps to pull and push an image</span></span>
<span data-ttu-id="889cb-118">L'esempio seguente scarica l'immagine di Nginx dal registro pubblico di Docker Hub, contrassegna l'immagine per il registro di contenitori di Azure privato, effettua il push dell'immagine nel registro e quindi ne effettua nuovamente il pull.</span><span class="sxs-lookup"><span data-stu-id="889cb-118">The follow example downloads the Nginx image from the public Docker Hub registry, tags it for your private Azure container registry, pushes it to your registry, then pulls it again.</span></span>

<span data-ttu-id="889cb-119">**1. Effettuare il pull dell'immagine ufficiale di Docker per Nginx**</span><span class="sxs-lookup"><span data-stu-id="889cb-119">**1. Pull the Docker official image for Nginx**</span></span>

<span data-ttu-id="889cb-120">Innanzitutto effettuare il pull dell'immagine pubblica di Nginx nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="889cb-120">First pull the public Nginx image to your local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="889cb-121">**2. Avviare il contenitore Nginx**</span><span class="sxs-lookup"><span data-stu-id="889cb-121">**2. Start the Nginx container**</span></span>

<span data-ttu-id="889cb-122">Il comando seguente avvia il contenitore Nginx locale in modo interattivo sulla porta 8080, consentendo di visualizzare l'output da Nginx,</span><span class="sxs-lookup"><span data-stu-id="889cb-122">The following command starts the local Nginx container interactively on port 8080, allowing you to see output from Nginx.</span></span> <span data-ttu-id="889cb-123">e quindi rimuove il contenitore in esecuzione dopo l'arresto.</span><span class="sxs-lookup"><span data-stu-id="889cb-123">It removes the running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="889cb-124">Passare a [http://localhost:8080/](http://localhost:8080) per visualizzare il contenitore in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="889cb-124">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span> <span data-ttu-id="889cb-125">Verrà visualizzata una schermata simile alla seguente.</span><span class="sxs-lookup"><span data-stu-id="889cb-125">You see a screen similar to the following one.</span></span>

![Nginx sul computer locale](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="889cb-127">Per arrestare il contenitore in esecuzione, premere [CTRL]+[C].</span><span class="sxs-lookup"><span data-stu-id="889cb-127">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="889cb-128">**3. Creare un alias dell'immagine nel registro**</span><span class="sxs-lookup"><span data-stu-id="889cb-128">**3. Create an alias of the image in your registry**</span></span>

<span data-ttu-id="889cb-129">Il comando seguente crea un alias dell'immagine, con un percorso completo del registro.</span><span class="sxs-lookup"><span data-stu-id="889cb-129">The following command creates an alias of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="889cb-130">Questo esempio specifica lo spazio dei nomi `samples` per evitare confusione nella radice del registro.</span><span class="sxs-lookup"><span data-stu-id="889cb-130">This example specifies the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="889cb-131">**4. Effettuare il push dell'immagine nel registro**</span><span class="sxs-lookup"><span data-stu-id="889cb-131">**4. Push the image to your registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="889cb-132">**5. Effettuare il pull dell'immagine dal registro**</span><span class="sxs-lookup"><span data-stu-id="889cb-132">**5. Pull the image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="889cb-133">**6. Avviare il contenitore Nginx dal registro**</span><span class="sxs-lookup"><span data-stu-id="889cb-133">**6. Start the Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="889cb-134">Passare a [http://localhost:8080/](http://localhost:8080) per visualizzare il contenitore in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="889cb-134">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span>

<span data-ttu-id="889cb-135">Per arrestare il contenitore in esecuzione, premere [CTRL]+[C].</span><span class="sxs-lookup"><span data-stu-id="889cb-135">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="889cb-136">**7. (Facoltativo) Rimuovere l'immagine**</span><span class="sxs-lookup"><span data-stu-id="889cb-136">**7. (Optional) Remove the image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="889cb-137">Limiti delle chiamate simultanee</span><span class="sxs-lookup"><span data-stu-id="889cb-137">Concurrent Limits</span></span>
<span data-ttu-id="889cb-138">In alcuni scenari, l'esecuzione di chiamate simultanee può provocare errori.</span><span class="sxs-lookup"><span data-stu-id="889cb-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="889cb-139">La tabella seguente contiene i limiti delle chiamate simultanee con operazioni "Push" e "Pull" nel registro contenitori di Azure:</span><span class="sxs-lookup"><span data-stu-id="889cb-139">The following table contains the limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="889cb-140">Operazione</span><span class="sxs-lookup"><span data-stu-id="889cb-140">Operation</span></span>  | <span data-ttu-id="889cb-141">Limite</span><span class="sxs-lookup"><span data-stu-id="889cb-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="889cb-142">PULL</span><span class="sxs-lookup"><span data-stu-id="889cb-142">PULL</span></span>       | <span data-ttu-id="889cb-143">Fino a 10 pull simultanei per registro</span><span class="sxs-lookup"><span data-stu-id="889cb-143">Up to 10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="889cb-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="889cb-144">PUSH</span></span>       | <span data-ttu-id="889cb-145">Fino a 5 push simultanei per registro</span><span class="sxs-lookup"><span data-stu-id="889cb-145">Up to 5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="889cb-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="889cb-146">Next steps</span></span>
<span data-ttu-id="889cb-147">Una volta apprese le nozioni di base, si è pronti per iniziare a usare il proprio registro.</span><span class="sxs-lookup"><span data-stu-id="889cb-147">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="889cb-148">È ad esempio possibile iniziare a distribuire immagini di contenitore in un cluster del [servizio contenitore di Azure](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="889cb-148">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
