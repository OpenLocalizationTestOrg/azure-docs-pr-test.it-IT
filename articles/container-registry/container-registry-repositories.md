---
title: Archivi di registri contenitori di Azure | Documentazione Microsoft
description: Come usare gli archivi di registri contenitori di Azure per le immagini Docker
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 06b809c31cecef1714f60d04657eb74c611be8cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="61648-103">Archivi di registri contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="61648-103">Azure container registry repositories</span></span>

<span data-ttu-id="61648-104">Il registro contenitori di Azure consente di archiviare le immagini dei contenitori in repository.</span><span class="sxs-lookup"><span data-stu-id="61648-104">Azure container registry allows you to store container images in repositories.</span></span> <span data-ttu-id="61648-105">Archiviando le immagini nei repository, è possibile avere gruppi di immagini (o versioni delle immagini) in ambienti isolati.</span><span class="sxs-lookup"><span data-stu-id="61648-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="61648-106">È possibile specificare questi repository quando si effettua il push delle immagini nel registro.</span><span class="sxs-lookup"><span data-stu-id="61648-106">You can specify these repositories when you push images to your registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="61648-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="61648-107">Prerequisites</span></span>
* <span data-ttu-id="61648-108">**Registro di contenitori di Azure**: creare un registro di contenitori nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="61648-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="61648-109">Ad esempio, usare il [Portale di Azure](container-registry-get-started-portal.md) o l'[interfaccia della riga di comando di Azure 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="61648-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="61648-110">**Interfaccia della riga di comando di Docker**: per configurare il computer locale come host Docker e accedere ai comandi della riga di comando di Docker, installare [Docker Engine](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="61648-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="61648-111">**Eseguire il pull di un'immagine**: estrarre un'immagine dal registro Docker Hub pubblico, aggiungervi un tag ed eseguirne il push nel registro.</span><span class="sxs-lookup"><span data-stu-id="61648-111">**Pull an image** - Pull an image from the public Docker Hub registry, tag it, and push it to your registry.</span></span> <span data-ttu-id="61648-112">Per istruzioni su come eseguire il push e il pull delle immagini, vedere [Effettuare il push della prima immagine in un registro per contenitori Docker privati tramite l'interfaccia della riga di comando di Docker](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="61648-112">For guidance on how push and pull images, see [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="61648-113">Visualizzazione dei repository nel portale</span><span class="sxs-lookup"><span data-stu-id="61648-113">Viewing repositories in the Portal</span></span>

<span data-ttu-id="61648-114">Dopo aver eseguito il push delle immagini nel registro contenitori, è possibile vedere un elenco dei repository che ospitano le immagini nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="61648-114">Once you have pushed images to your container registry, you can see a list of the repositories hosting the images in the Azure portal.</span></span>

<span data-ttu-id="61648-115">Se è stata seguita la procedura descritta nell'articolo [Effettuare il push della prima immagine in un registro per contenitori Docker privati tramite l'interfaccia della riga di comando di Docker](container-registry-get-started-docker-cli.md), si dovrebbe avere un'immagine Nginx nel registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="61648-115">If you followed the steps in the [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="61648-116">Come parte delle istruzioni sarà stato specificato uno spazio dei nomi per l'immagine.</span><span class="sxs-lookup"><span data-stu-id="61648-116">As part of the instructions, you should have specified a namespace for the image.</span></span> <span data-ttu-id="61648-117">Nell'esempio seguente il comando esegue il push dell'immagine NGinx nel repository "samples":</span><span class="sxs-lookup"><span data-stu-id="61648-117">In the example below, the command pushes the NGinx image to the "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="61648-118">Registro contenitori di Azure supporta spazi dei nomi dei repository multilivello.</span><span class="sxs-lookup"><span data-stu-id="61648-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="61648-119">Questa funzionalità consente di raggruppare raccolte di immagini correlate a un'app specifica oppure una raccolta di app per specifici team operativi o di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="61648-119">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span></span> <span data-ttu-id="61648-120">Per altre informazioni sul repository nei registri contenitori, vedere [Effettuare il push della prima immagine in un registro per contenitori Docker privati tramite l'interfaccia della riga di comando di Docker](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="61648-120">To read more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="61648-121">Per visualizzare i repository del registro contenitori:</span><span class="sxs-lookup"><span data-stu-id="61648-121">To view the container registry repositories:</span></span>

1. <span data-ttu-id="61648-122">Accedere al Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="61648-122">Log in to the Azure portal</span></span>
2. <span data-ttu-id="61648-123">Nel pannello **Registro contenitori di Azure** selezionare il registro che si desidera esaminare</span><span class="sxs-lookup"><span data-stu-id="61648-123">On the **Azure Container Registry** blade, select the registry you wish to inspect</span></span>
3. <span data-ttu-id="61648-124">Nel pannello del registro fare clic su **Repository** per vedere un elenco di tutti i repository e le relative immagini</span><span class="sxs-lookup"><span data-stu-id="61648-124">In the registry blade, click **Repositories** to see a list of all the repositories and their images</span></span>
4. <span data-ttu-id="61648-125">(Facoltativo) Selezionare un'immagine specifica per vedere i tag</span><span class="sxs-lookup"><span data-stu-id="61648-125">(Optional) Select a specific image to see tags</span></span>

![I repository nel portale](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="61648-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61648-127">Next steps</span></span>
<span data-ttu-id="61648-128">Una volta apprese le nozioni di base, si è pronti per iniziare a usare il proprio registro.</span><span class="sxs-lookup"><span data-stu-id="61648-128">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="61648-129">È ad esempio possibile iniziare a distribuire immagini di contenitore in un cluster del [servizio contenitore di Azure](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="61648-129">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
