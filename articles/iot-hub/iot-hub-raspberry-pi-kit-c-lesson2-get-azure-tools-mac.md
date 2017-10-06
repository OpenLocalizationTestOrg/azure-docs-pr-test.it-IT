---
title: 'Connect Raspberry PI (C) tooAzure IoT - lezione 2: strumenti di Azure (macOS) | Documenti Microsoft'
description: Installare Python e l'interfaccia della riga di comando di Azure in macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servizio cloud iot, interfaccia della riga di comando di azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a079250fd94fa9bc1c11b6c21de02a8d46f6f3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="d6ba4-104">Ottenere gli strumenti di Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="d6ba4-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6ba4-105">Windows 7 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="d6ba4-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="d6ba4-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="d6ba4-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="d6ba4-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="d6ba4-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="d6ba4-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="d6ba4-108">What you will do</span></span>
<span data-ttu-id="d6ba4-109">Installare hello Azure interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="d6ba4-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="d6ba4-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d6ba4-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d6ba4-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="d6ba4-111">What you will learn</span></span>
<span data-ttu-id="d6ba4-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="d6ba4-112">In this article, you will learn:</span></span>
* <span data-ttu-id="d6ba4-113">Come tooinstall CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="d6ba4-114">Come tooadd un sottogruppo di IoT di hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d6ba4-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="d6ba4-115">What you need</span></span>
* <span data-ttu-id="d6ba4-116">Un Mac con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="d6ba4-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-117">An active Azure subscription.</span></span> <span data-ttu-id="d6ba4-118">Se non si ha un account Azure, è possibile [creare un account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="d6ba4-119">Installare Python</span><span class="sxs-lookup"><span data-stu-id="d6ba4-119">Install Python</span></span>
<span data-ttu-id="d6ba4-120">Sebbene macOS include Python 2.7 predefinito hello, è consigliabile installare Python tramite Homebrew.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="d6ba4-121">Vedere [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/) (Installazione di Python in macOS).</span><span class="sxs-lookup"><span data-stu-id="d6ba4-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="d6ba4-122">Installare Python e pip eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6ba4-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="d6ba4-123">Installare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="d6ba4-123">Install hello Azure CLI</span></span>
<span data-ttu-id="d6ba4-124">Hello CLI di Azure fornisce un'esperienza della riga di comando multipiattaforma di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="d6ba4-125">Si lavora direttamente da tooprovision la riga di comando e la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-125">You work directly from your command line tooprovision and manage resources.</span></span> 

<span data-ttu-id="d6ba4-126">tooinstall hello CLI di Azure più recenti, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="d6ba4-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="d6ba4-127">Eseguire i seguenti comandi in una finestra terminale hello.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="d6ba4-128">Potrebbe richiedere cinque minuti tooinstall hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="d6ba4-129">Verificare l'installazione di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d6ba4-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="d6ba4-130">Verrà visualizzato l'output seguente hello se installazione hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-130">You should see hello following output if hello installation is successful.</span></span>

![Output che indica l'esito positivo](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="d6ba4-132">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="d6ba4-132">Summary</span></span>
<span data-ttu-id="d6ba4-133">È stato installato hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="d6ba4-134">L'attività successiva è toocreate l'identità di hub e dispositivi Azure IoT utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6ba4-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6ba4-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d6ba4-135">Next steps</span></span>
[<span data-ttu-id="d6ba4-136">Creare l'hub IoT e registrare Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="d6ba4-136">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

