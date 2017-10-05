---
title: Risoluzione dei problemi relativi a Istanze di contenitore di Azure
description: Informazioni su come risolvere i problemi relativi a Istanze di contenitore di Azure
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 86fa4b7dca7c362f95c0243a33f03d1f2dd3ab42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="45c19-103">Risolvere i problemi di distribuzione in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="45c19-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="45c19-104">Questo articolo mostra come risolvere i problemi durante la distribuzione di contenitori in Istanze di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="45c19-104">This article shows how to troubleshoot issues when deploying containers to Azure Container Instances.</span></span> <span data-ttu-id="45c19-105">e illustra alcuni problemi comuni che è possibile incontrare.</span><span class="sxs-lookup"><span data-stu-id="45c19-105">It also describes some of the common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="45c19-106">Recupero degli eventi di diagnostica</span><span class="sxs-lookup"><span data-stu-id="45c19-106">Getting diagnostic events</span></span>

<span data-ttu-id="45c19-107">Per visualizzare i log generati dal codice dell'applicazione all'interno di un contenitore, è possibile usare il comando [az container logs](/cli/azure/container#logs).</span><span class="sxs-lookup"><span data-stu-id="45c19-107">To view logs from your application code within a container, you can use the [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="45c19-108">Se tuttavia il contenitore non viene distribuito correttamente, è necessario esaminare le informazioni di diagnostica fornite dal provider di risorse Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="45c19-108">But if your container does not deploy successfully, you need to review the diagnostic information provided by the Azure Container Instances resource provider.</span></span> <span data-ttu-id="45c19-109">Per visualizzare gli eventi per il proprio contenitore, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="45c19-109">To view the events for your container, run the following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="45c19-110">L'output include le proprietà principali del contenitore e gli eventi di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="45c19-110">The output includes the core properties of your container, along with deployment events:</span></span>

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a><span data-ttu-id="45c19-111">Problemi di distribuzione comuni</span><span class="sxs-lookup"><span data-stu-id="45c19-111">Common deployment issues</span></span>

<span data-ttu-id="45c19-112">La maggior parte degli errori riscontrati durante la distribuzione è dovuta ad alcuni problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="45c19-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-to-pull-image"></a><span data-ttu-id="45c19-113">Non è possibile eseguire il pull dell'immagine</span><span class="sxs-lookup"><span data-stu-id="45c19-113">Unable to pull image</span></span>

<span data-ttu-id="45c19-114">Se Istanze di contenitore di Azure non è inizialmente in grado di eseguire il pull dell'immagine, ripete il tentativo per un certo periodo di tempo prima di generare un errore.</span><span class="sxs-lookup"><span data-stu-id="45c19-114">If Azure Container Instances is unable to pull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="45c19-115">Se il pull dell'immagine non può essere eseguito, vengono visualizzati eventi simili al seguente:</span><span class="sxs-lookup"><span data-stu-id="45c19-115">If the image cannot be pulled, events like the following are shown:</span></span>

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed to pull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

<span data-ttu-id="45c19-116">Per risolvere il problema, eliminare il contenitore e ripetere il tentativo di distribuzione, facendo attenzione a digitare correttamente il nome dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="45c19-116">To resolve, delete the container and retry your deployment, paying close attention that you have typed the image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="45c19-117">Il contenitore viene continuamente chiuso e riavviato</span><span class="sxs-lookup"><span data-stu-id="45c19-117">Container continually exits and restarts</span></span>

<span data-ttu-id="45c19-118">Istanze di contenitore di Azure supporta attualmente solo servizi a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="45c19-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="45c19-119">Se il contenitore termina l'esecuzione e si chiude, viene riavviato in automatico ed eseguito nuovamente.</span><span class="sxs-lookup"><span data-stu-id="45c19-119">If your container runs to completion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="45c19-120">In questo caso, vengono visualizzati eventi simili ai seguenti.</span><span class="sxs-lookup"><span data-stu-id="45c19-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="45c19-121">Si noti che il contenitore viene avviato correttamente e quindi riavviato con rapidità.</span><span class="sxs-lookup"><span data-stu-id="45c19-121">Note that the container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="45c19-122">L'API di Istanze di contenitore include una proprietà `retryCount` che indica il numero di volte in cui un determinato contenitore è stato riavviato.</span><span class="sxs-lookup"><span data-stu-id="45c19-122">The Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> <span data-ttu-id="45c19-123">La maggior parte delle immagini di contenitore per le distribuzioni di Linux imposta una shell, ad esempio bash, come comando predefinito.</span><span class="sxs-lookup"><span data-stu-id="45c19-123">Most container images for Linux distributions set a shell, such as bash, as the default command.</span></span> <span data-ttu-id="45c19-124">Poiché una shell non è di per sé un servizio a esecuzione prolungata, questi contenitori vengono chiusi immediatamente e sono soggetti a un riavvio ciclico.</span><span class="sxs-lookup"><span data-stu-id="45c19-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-to-start"></a><span data-ttu-id="45c19-125">L'avvio di un contenitore richiede molto tempo</span><span class="sxs-lookup"><span data-stu-id="45c19-125">Container takes a long time to start</span></span>

<span data-ttu-id="45c19-126">Se per avviare il contenitore è necessario molto tempo, ma alla fine l'operazione ha esito positivo, esaminare innanzitutto la dimensione dell'immagine del contenitore.</span><span class="sxs-lookup"><span data-stu-id="45c19-126">If your container takes a long time to start, but eventually succeeds, start by looking at the size of your container image.</span></span> <span data-ttu-id="45c19-127">Poiché Istanze di contenitore di Azure esegue il pull dell'immagine del contenitore su richiesta, il tempo di avvio rilevato è direttamente correlato alla dimensione dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="45c19-127">Because Azure Container Instances pulls your container image on demand, the startup time you experience is directly related to its size.</span></span>

<span data-ttu-id="45c19-128">Per visualizzare la dimensione dell'immagine del contenitore è possibile usare l'interfaccia della riga di comando di Docker:</span><span class="sxs-lookup"><span data-stu-id="45c19-128">You can view the size of your container image using the Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="45c19-129">Output:</span><span class="sxs-lookup"><span data-stu-id="45c19-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="45c19-130">Il modo migliore per limitare le dimensioni delle immagini è quello di evitare che l'immagine finale contenga dati che non sono necessari in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="45c19-130">The key to keeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="45c19-131">A tale scopo è possibile eseguire [compilazioni in più fasi](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="45c19-131">One way to do this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="45c19-132">Le compilazioni di questo tipo consentono di assicurarsi che l'immagine finale contenga solo gli elementi necessari per l'applicazione, escludendo altro contenuto richiesto in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="45c19-132">Multi-stage builds make it easy to ensure that the final image contains only the artifacts you need for your application, and not any of the extra content that was required at build time.</span></span>

<span data-ttu-id="45c19-133">L'altro modo per ridurre l'impatto del pull dell'immagine sul tempo di avvio del contenitore è quello di ospitare l'immagine del contenitore usando il Registro contenitori di Azure nella stessa area in cui si intende usare Istanze di contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="45c19-133">The other way to reduce the impact of the image pull on your container's startup time is to host the container image using the Azure Container Registry in the same region where you intend to use Azure Container Instances.</span></span> <span data-ttu-id="45c19-134">Ciò consente di ridurre il percorso dell'immagine del contenitore attraverso la rete e quindi di limitare notevolmente il tempo di download.</span><span class="sxs-lookup"><span data-stu-id="45c19-134">This shortens the network path that the container image needs to travel, significantly shortening the download time.</span></span>