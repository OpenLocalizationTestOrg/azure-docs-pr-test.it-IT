---
title: 'Connettersi Raspberry Pi (nodo) tooAzure IoT - lezione 2: ottenere gli strumenti (Windows) | Documenti Microsoft'
description: Installare Python e hello Azure interfaccia della riga di comando (CLI di Azure) in Windows 7 e versioni successive.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: servizio cloud iot, interfaccia della riga di comando di azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: acfa13e3-6d2c-4e68-9a77-1cbc2cf3f9c1
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 25b50214322137ea32861fd1131c474e2fc7ebb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="0f106-104">Ottenere gli strumenti di Azure (Windows 7 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="0f106-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f106-105">Windows 7 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="0f106-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="0f106-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="0f106-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="0f106-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="0f106-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="0f106-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0f106-108">What you will do</span></span>
<span data-ttu-id="0f106-109">Installare Python e hello Azure interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="0f106-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="0f106-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0f106-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0f106-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0f106-111">What you will learn</span></span>
<span data-ttu-id="0f106-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="0f106-112">In this article, you will learn:</span></span>
* <span data-ttu-id="0f106-113">Come tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="0f106-113">How tooinstall Python.</span></span>
* <span data-ttu-id="0f106-114">Come tooinstall hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f106-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0f106-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="0f106-115">What you need</span></span>
* <span data-ttu-id="0f106-116">Un computer Windows con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="0f106-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="0f106-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="0f106-117">An active Azure subscription.</span></span> <span data-ttu-id="0f106-118">Se non si ha un account Azure, creare un [account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="0f106-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="0f106-119">Installare Python</span><span class="sxs-lookup"><span data-stu-id="0f106-119">Install Python</span></span>
<span data-ttu-id="0f106-120">[Installare Python](https://www.python.org/downloads/) nel computer Windows.</span><span class="sxs-lookup"><span data-stu-id="0f106-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="0f106-121">È possibile installare Python 2.7, 3.4 o 3.5.</span><span class="sxs-lookup"><span data-stu-id="0f106-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="0f106-122">Questa esercitazione è basata su Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="0f106-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="0f106-123">Se è già stato installato Python, andare nella sezione successiva toohello e installare hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f106-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="0f106-124">È inoltre necessario percorso hello tooadd delle cartelle hello in python.exe e pip.exe sono installati toohello sistema `PATH` variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="0f106-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="0f106-125">Per impostazione predefinita, python.exe viene installato in `C:\Python27` e pip.exe viene installato in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="0f106-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="0f106-126">Installare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="0f106-126">Install hello Azure CLI</span></span>
<span data-ttu-id="0f106-127">Hello CLI di Azure fornisce un'esperienza della riga di comando multipiattaforma di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f106-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="0f106-128">Si lavora direttamente il tooprovision della riga di comando e la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="0f106-128">You work directly from your command-line tooprovision and manage resources.</span></span>

<span data-ttu-id="0f106-129">hello tooinstall CLI di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="0f106-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="0f106-130">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0f106-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="0f106-131">Eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="0f106-131">Run hello following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="0f106-132">Verificare l'installazione di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0f106-132">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="0f106-133">Viene visualizzato l'output seguente hello se installazione hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="0f106-133">You see hello following output if hello installation is successful.</span></span>

![Output che indica l'esito positivo](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="0f106-135">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="0f106-135">Summary</span></span>
<span data-ttu-id="0f106-136">È stato installato hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f106-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="0f106-137">La prossima attività toocreate l'identità di Azure IoT hub e dispositivi tramite hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f106-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f106-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f106-138">Next steps</span></span>
[<span data-ttu-id="0f106-139">Creare l'hub IoT e registrare Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="0f106-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

