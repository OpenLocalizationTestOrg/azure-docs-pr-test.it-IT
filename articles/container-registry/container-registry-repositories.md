---
title: repository del Registro di sistema di contenitore aaaAzure | Documenti Microsoft
description: Il repository del Registro di sistema di Azure contenitore toouse per le immagini Docker
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
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="25974-103">Archivi di registri contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="25974-103">Azure container registry repositories</span></span>

<span data-ttu-id="25974-104">Registro di sistema di contenitore di Azure consente di immagini contenitore toostore nel repository.</span><span class="sxs-lookup"><span data-stu-id="25974-104">Azure container registry allows you toostore container images in repositories.</span></span> <span data-ttu-id="25974-105">Archiviando le immagini nei repository, è possibile avere gruppi di immagini (o versioni delle immagini) in ambienti isolati.</span><span class="sxs-lookup"><span data-stu-id="25974-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="25974-106">Quando si esegue il push del Registro di sistema tooyour immagini, è possibile specificare questi archivi.</span><span class="sxs-lookup"><span data-stu-id="25974-106">You can specify these repositories when you push images tooyour registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="25974-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="25974-107">Prerequisites</span></span>
* <span data-ttu-id="25974-108">**Registro di contenitori di Azure**: creare un registro di contenitori nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="25974-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="25974-109">Ad esempio, utilizzare hello [portale di Azure](container-registry-get-started-portal.md) o hello [CLI di Azure 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="25974-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="25974-110">**Docker CLI** -tooset del computer locale come un host e accesso hello Docker CLI i comandi di Docker, installare [motore Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="25974-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="25974-111">**Estrarre un'immagine** - Pull un'immagine dal Registro di sistema di hello pubblico Hub Docker, tag e spingerla tooyour del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="25974-111">**Pull an image** - Pull an image from hello public Docker Hub registry, tag it, and push it tooyour registry.</span></span> <span data-ttu-id="25974-112">Per indicazioni su come eseguire il push e pull immagini, vedere [Registro di sistema privata Push Docker immagine tooAzure](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="25974-112">For guidance on how push and pull images, see [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="25974-113">Visualizzazione di repository in hello portale</span><span class="sxs-lookup"><span data-stu-id="25974-113">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="25974-114">Dopo avere eseguito il push del Registro di sistema di immagini tooyour contenitore, è possibile visualizzare un elenco dei repository hello hosting immagini hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="25974-114">Once you have pushed images tooyour container registry, you can see a list of hello repositories hosting hello images in hello Azure portal.</span></span>

<span data-ttu-id="25974-115">Se è stata seguita la procedura hello in hello [registro privata di Push di Docker immagini tooAzure](container-registry-get-started-docker-cli.md) articolo, è stata acquisita un'immagine di Nginx nel Registro di sistema contenitore.</span><span class="sxs-lookup"><span data-stu-id="25974-115">If you followed hello steps in hello [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="25974-116">Come parte delle istruzioni di hello, si deve specificare uno spazio dei nomi per l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="25974-116">As part of hello instructions, you should have specified a namespace for hello image.</span></span> <span data-ttu-id="25974-117">Nell'esempio hello seguente comando hello inserisce i repository di hello NGinx immagini toohello "esempi":</span><span class="sxs-lookup"><span data-stu-id="25974-117">In hello example below, hello command pushes hello NGinx image toohello "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="25974-118">Registro contenitori di Azure supporta spazi dei nomi dei repository multilivello.</span><span class="sxs-lookup"><span data-stu-id="25974-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="25974-119">Questa funzionalità consente di toogroup raccolte di app specifica tooa correlati di immagini, o una raccolta di sviluppo di App toospecific o i team operativi.</span><span class="sxs-lookup"><span data-stu-id="25974-119">This feature enables you toogroup collections of images related tooa specific app, or a collection of apps toospecific development or operational teams.</span></span> <span data-ttu-id="25974-120">tooread ulteriori informazioni su repository nei registri di sistema di contenitore, vedere [registri contenitore privato Docker in Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="25974-120">tooread more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="25974-121">repository del Registro di sistema di tooview hello contenitore:</span><span class="sxs-lookup"><span data-stu-id="25974-121">tooview hello container registry repositories:</span></span>

1. <span data-ttu-id="25974-122">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="25974-122">Log in toohello Azure portal</span></span>
2. <span data-ttu-id="25974-123">In hello **Registro di sistema di Azure contenitore** blade, Registro di sistema selezionare hello desiderato tooinspect</span><span class="sxs-lookup"><span data-stu-id="25974-123">On hello **Azure Container Registry** blade, select hello registry you wish tooinspect</span></span>
3. <span data-ttu-id="25974-124">Nel Pannello di hello del Registro di sistema, fare clic su **repository** toosee un elenco di tutti i repository hello e proprie immagini</span><span class="sxs-lookup"><span data-stu-id="25974-124">In hello registry blade, click **Repositories** toosee a list of all hello repositories and their images</span></span>
4. <span data-ttu-id="25974-125">(Facoltativo) Selezionare un tag di immagine specifico toosee</span><span class="sxs-lookup"><span data-stu-id="25974-125">(Optional) Select a specific image toosee tags</span></span>

![Repository nel portale di hello](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="25974-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25974-127">Next steps</span></span>
<span data-ttu-id="25974-128">Ora che si conoscono i concetti di base hello, si è pronti toostart mediante il Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="25974-128">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="25974-129">Ad esempio, iniziare la distribuzione di contenitore immagini tooan [servizio contenitore di Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span><span class="sxs-lookup"><span data-stu-id="25974-129">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
