---
title: 'Connettere Raspberry Pi (Node) ad Azure IoT: lezione 2: Ottenere gli strumenti (Windows) | Documentazione Microsoft'
description: Installare Python e l'interfaccia della riga di comando di Azure in Windows 7 e versioni successive.
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
ms.openlocfilehash: c7b927997b738f7a80b71c06d4dff2278dc7c64e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="70ebb-104">Ottenere gli strumenti di Azure (Windows 7 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="70ebb-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="70ebb-105">Windows 7 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="70ebb-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="70ebb-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="70ebb-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="70ebb-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="70ebb-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="70ebb-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="70ebb-108">What you will do</span></span>
<span data-ttu-id="70ebb-109">Installare Python e l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="70ebb-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="70ebb-110">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="70ebb-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="70ebb-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="70ebb-111">What you will learn</span></span>
<span data-ttu-id="70ebb-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="70ebb-112">In this article, you will learn:</span></span>
* <span data-ttu-id="70ebb-113">Come installare Python.</span><span class="sxs-lookup"><span data-stu-id="70ebb-113">How to install Python.</span></span>
* <span data-ttu-id="70ebb-114">Come installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="70ebb-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="70ebb-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="70ebb-115">What you need</span></span>
* <span data-ttu-id="70ebb-116">Un computer Windows con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="70ebb-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="70ebb-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="70ebb-117">An active Azure subscription.</span></span> <span data-ttu-id="70ebb-118">Se non si ha un account Azure, creare un [account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="70ebb-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="70ebb-119">Installare Python</span><span class="sxs-lookup"><span data-stu-id="70ebb-119">Install Python</span></span>
<span data-ttu-id="70ebb-120">[Installare Python](https://www.python.org/downloads/) nel computer Windows.</span><span class="sxs-lookup"><span data-stu-id="70ebb-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="70ebb-121">È possibile installare Python 2.7, 3.4 o 3.5.</span><span class="sxs-lookup"><span data-stu-id="70ebb-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="70ebb-122">Questa esercitazione è basata su Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="70ebb-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="70ebb-123">Se Python è già installato, passare alla sezione successiva e installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="70ebb-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="70ebb-124">È inoltre necessario aggiungere il percorso delle cartelle in cui vengono installati python.exe e pip.exe alla variabile di ambiente `PATH` del sistema.</span><span class="sxs-lookup"><span data-stu-id="70ebb-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="70ebb-125">Per impostazione predefinita, python.exe viene installato in `C:\Python27` e pip.exe viene installato in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="70ebb-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="70ebb-126">Installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="70ebb-126">Install the Azure CLI</span></span>
<span data-ttu-id="70ebb-127">L'interfaccia della riga di comando di Azure offre un'esperienza di riga di comando multipiattaforma per Azure.</span><span class="sxs-lookup"><span data-stu-id="70ebb-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="70ebb-128">Si opera direttamente dalla riga di comando per il provisioning e la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="70ebb-128">You work directly from your command-line to provision and manage resources.</span></span>

<span data-ttu-id="70ebb-129">Per installare l'interfaccia della riga di comando di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="70ebb-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="70ebb-130">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="70ebb-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="70ebb-131">Eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="70ebb-131">Run the following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="70ebb-132">Verificare l'installazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="70ebb-132">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="70ebb-133">Se l'installazione ha esito positivo, verrà visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="70ebb-133">You see the following output if the installation is successful.</span></span>

![Output che indica l'esito positivo](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="70ebb-135">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="70ebb-135">Summary</span></span>
<span data-ttu-id="70ebb-136">È stata installata l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="70ebb-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="70ebb-137">L'attività successiva consiste nella creazione dell'hub IoT di Azure e dell'identità del dispositivo tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="70ebb-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70ebb-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70ebb-138">Next steps</span></span>
[<span data-ttu-id="70ebb-139">Creare l'hub IoT e registrare Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="70ebb-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

