---
title: 'Connect Intel Edison (C) tooAzure IoT - lezione 2: strumenti di Azure (Windows) | Documenti Microsoft'
description: Installare Python e hello Azure interfaccia della riga di comando (CLI di Azure) in Windows 7 e versioni successive.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interfaccia della riga di comando di azure, servizio cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 1035760e-cdd1-4d99-8003-067e98b29762
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 46f964541c00674500e4f6a072a9a2547b5b24d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="e61c0-104">Ottenere gli strumenti di Azure (Windows 7 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="e61c0-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e61c0-105">[Windows 7 e versioni successive][windows]</span><span class="sxs-lookup"><span data-stu-id="e61c0-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="e61c0-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="e61c0-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="e61c0-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="e61c0-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e61c0-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="e61c0-108">What you will do</span></span>
<span data-ttu-id="e61c0-109">Installare Python e hello Azure interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="e61c0-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="e61c0-110">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e61c0-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e61c0-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="e61c0-111">What you will learn</span></span>
<span data-ttu-id="e61c0-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="e61c0-112">In this article, you will learn:</span></span>
* <span data-ttu-id="e61c0-113">Come tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="e61c0-113">How tooinstall Python.</span></span>
* <span data-ttu-id="e61c0-114">Come tooinstall hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="e61c0-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e61c0-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="e61c0-115">What you need</span></span>
* <span data-ttu-id="e61c0-116">Un computer Windows con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="e61c0-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="e61c0-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="e61c0-117">An active Azure subscription.</span></span> <span data-ttu-id="e61c0-118">Se non si ha un account Azure, creare un [account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="e61c0-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="e61c0-119">Installare Python</span><span class="sxs-lookup"><span data-stu-id="e61c0-119">Install Python</span></span>
<span data-ttu-id="e61c0-120">[Installare Python](https://www.python.org/downloads/) nel computer Windows.</span><span class="sxs-lookup"><span data-stu-id="e61c0-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="e61c0-121">È possibile installare Python 2.7, 3.4 o 3.5.</span><span class="sxs-lookup"><span data-stu-id="e61c0-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="e61c0-122">Questa esercitazione è basata su Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="e61c0-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="e61c0-123">Se è già stato installato Python, andare nella sezione successiva toohello e installare hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="e61c0-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="e61c0-124">È inoltre necessario percorso hello tooadd delle cartelle hello in python.exe e pip.exe sono installati toohello sistema `PATH` variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="e61c0-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="e61c0-125">Per impostazione predefinita, python.exe viene installato in `C:\Python27` e pip.exe viene installato in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="e61c0-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="e61c0-126">Installare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="e61c0-126">Install hello Azure CLI</span></span>
<span data-ttu-id="e61c0-127">Hello CLI di Azure fornisce un'esperienza della riga di comando multipiattaforma di Azure.</span><span class="sxs-lookup"><span data-stu-id="e61c0-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="e61c0-128">Si lavora direttamente da tooprovision la riga di comando e la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="e61c0-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="e61c0-129">hello tooinstall CLI di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="e61c0-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="e61c0-130">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e61c0-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="e61c0-131">Eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="e61c0-131">Run hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="e61c0-132">Verificare l'installazione di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e61c0-132">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="e61c0-133">Viene visualizzato l'output seguente hello se installazione hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="e61c0-133">You see hello following output if hello installation is successful.</span></span>

![Output che indica l'esito positivo](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="e61c0-135">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="e61c0-135">Summary</span></span>
<span data-ttu-id="e61c0-136">È stato installato hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="e61c0-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="e61c0-137">La prossima attività toocreate l'identità di Azure IoT hub e dispositivi tramite hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="e61c0-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e61c0-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e61c0-138">Next steps</span></span>
<span data-ttu-id="e61c0-139">[Creare l'hub IoT e registrare Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="e61c0-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
