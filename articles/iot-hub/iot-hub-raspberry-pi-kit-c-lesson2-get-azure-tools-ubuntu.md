---
title: 'Connect Raspberry PI (C) tooAzure IoT - lezione 2: strumenti di Azure (Ubuntu) | Documenti Microsoft'
description: Installare Python e l'interfaccia della riga di comando di Azure in Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servizio cloud iot, interfaccia della riga di comando di azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a03512f2-fabe-40c5-8505-b93eef8e5bec
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1af4848f9fe0508e362c15b36eec8a35aea9ac5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="15734-104">Ottenere gli strumenti di Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="15734-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="15734-105">Windows 7 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="15734-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="15734-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="15734-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="15734-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="15734-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="15734-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="15734-108">What you will do</span></span>
<span data-ttu-id="15734-109">Installare hello Azure interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="15734-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="15734-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="15734-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="15734-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="15734-111">What you will learn</span></span>
<span data-ttu-id="15734-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="15734-112">In this article, you will learn:</span></span>
* <span data-ttu-id="15734-113">Come tooinstall hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="15734-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="15734-114">Come tooadd un sottogruppo di IoT di hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="15734-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="15734-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="15734-115">What you need</span></span>
* <span data-ttu-id="15734-116">Un computer Ubuntu con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="15734-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="15734-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="15734-117">An active Azure subscription.</span></span> <span data-ttu-id="15734-118">Se non si ha un account, è possibile creare un [account di valutazione gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="15734-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="15734-119">Installare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="15734-119">Install hello Azure CLI</span></span>
<span data-ttu-id="15734-120">Hello CLI di Azure offre un'esperienza della riga di comando multipiattaforma per Azure, consentendo toowork direttamente da tooprovision la riga di comando e gestire le risorse.</span><span class="sxs-lookup"><span data-stu-id="15734-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="15734-121">tooinstall hello CLI di Azure più recenti, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="15734-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="15734-122">Eseguire i seguenti comandi in una finestra terminale hello.</span><span class="sxs-lookup"><span data-stu-id="15734-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="15734-123">Potrebbe richiedere cinque minuti tooinstall hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="15734-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="15734-124">Verificare l'installazione di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="15734-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="15734-125">Verrà visualizzato l'output seguente hello se installazione hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="15734-125">You should see hello following output if hello installation is successful.</span></span>

![Output che indica l'esito positivo](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="15734-127">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="15734-127">Summary</span></span>
<span data-ttu-id="15734-128">È stato installato hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="15734-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="15734-129">L'attività successiva è toocreate l'hub IoT di Azure e l'utilizzo di identità dispositivo hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="15734-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15734-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15734-130">Next steps</span></span>
[<span data-ttu-id="15734-131">Creare l'hub IoT e registrare Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="15734-131">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

