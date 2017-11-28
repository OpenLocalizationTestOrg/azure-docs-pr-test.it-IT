---
title: 'Connect Raspberry PI (C) tooAzure IoT - lezione 2: strumenti di Azure (Windows) | Documenti Microsoft'
description: Installare Python e hello Azure interfaccia della riga di comando (CLI di Azure) in Windows 7 e versioni successive.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servizio cloud iot, interfaccia della riga di comando di azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a3c083b5-0d76-46af-bc77-2ad7d8aadc1e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1819d61fafbee6ac42a1bea5c16437cd8bf43af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="92f5b-104">Ottenere gli strumenti di Azure (Windows 7 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="92f5b-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="92f5b-105">Windows 7 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="92f5b-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="92f5b-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="92f5b-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="92f5b-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="92f5b-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="92f5b-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="92f5b-108">What you will do</span></span>
<span data-ttu-id="92f5b-109">Installare Python e hello Azure interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="92f5b-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="92f5b-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="92f5b-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="92f5b-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="92f5b-111">What you will learn</span></span>
<span data-ttu-id="92f5b-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="92f5b-112">In this article, you will learn:</span></span>
* <span data-ttu-id="92f5b-113">Come tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="92f5b-113">How tooinstall Python.</span></span>
* <span data-ttu-id="92f5b-114">Come tooinstall hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="92f5b-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="92f5b-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="92f5b-115">What you need</span></span>
* <span data-ttu-id="92f5b-116">Un computer Windows con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="92f5b-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="92f5b-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="92f5b-117">An active Azure subscription.</span></span> <span data-ttu-id="92f5b-118">Se non si ha un account Azure, creare un [account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="92f5b-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="92f5b-119">Installare Python</span><span class="sxs-lookup"><span data-stu-id="92f5b-119">Install Python</span></span>
<span data-ttu-id="92f5b-120">[Installare Python](https://www.python.org/downloads/) nel computer Windows.</span><span class="sxs-lookup"><span data-stu-id="92f5b-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="92f5b-121">È possibile installare Python 2.7, 3.4 o 3.5.</span><span class="sxs-lookup"><span data-stu-id="92f5b-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="92f5b-122">Questa esercitazione è basata su Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="92f5b-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="92f5b-123">Se è già stato installato Python, andare nella sezione successiva toohello e installare hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="92f5b-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="92f5b-124">È inoltre necessario percorso hello tooadd delle cartelle hello in python.exe e pip.exe sono installati toohello sistema `PATH` variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="92f5b-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="92f5b-125">Per impostazione predefinita, python.exe viene installato in `C:\Python27` e pip.exe viene installato in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="92f5b-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="92f5b-126">Installare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="92f5b-126">Install hello Azure CLI</span></span>
<span data-ttu-id="92f5b-127">Hello CLI di Azure fornisce un'esperienza della riga di comando multipiattaforma di Azure.</span><span class="sxs-lookup"><span data-stu-id="92f5b-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="92f5b-128">Si lavora direttamente da tooprovision la riga di comando e la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="92f5b-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="92f5b-129">hello tooinstall CLI di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="92f5b-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="92f5b-130">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="92f5b-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="92f5b-131">Eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="92f5b-131">Run hello following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="92f5b-132">Verificare l'installazione di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="92f5b-132">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="92f5b-133">Viene visualizzato l'output seguente hello se installazione hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="92f5b-133">You see hello following output if hello installation is successful.</span></span>

![Output che indica l'esito positivo](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="92f5b-135">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="92f5b-135">Summary</span></span>
<span data-ttu-id="92f5b-136">È stato installato hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="92f5b-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="92f5b-137">La prossima attività toocreate l'identità di Azure IoT hub e dispositivi tramite hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="92f5b-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92f5b-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="92f5b-138">Next steps</span></span>
[<span data-ttu-id="92f5b-139">Creare l'hub IoT e registrare Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="92f5b-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

