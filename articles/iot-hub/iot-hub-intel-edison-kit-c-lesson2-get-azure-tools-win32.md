---
title: 'Connettere Intel Edison (C) ad Azure IoT: lezione 2: Strumenti di Azure (Windows) | Documentazione Microsoft'
description: Installare Python e l'interfaccia della riga di comando di Azure in Windows 7 e versioni successive.
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
ms.openlocfilehash: 90ef113ae84ccc8cb3cbdbe8c245e138320a93c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="6be66-104">Ottenere gli strumenti di Azure (Windows 7 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="6be66-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="6be66-105">[Windows 7 e versioni successive][windows]</span><span class="sxs-lookup"><span data-stu-id="6be66-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="6be66-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="6be66-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="6be66-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="6be66-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="6be66-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="6be66-108">What you will do</span></span>
<span data-ttu-id="6be66-109">Installare Python e l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="6be66-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="6be66-110">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="6be66-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6be66-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="6be66-111">What you will learn</span></span>
<span data-ttu-id="6be66-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="6be66-112">In this article, you will learn:</span></span>
* <span data-ttu-id="6be66-113">Come installare Python.</span><span class="sxs-lookup"><span data-stu-id="6be66-113">How to install Python.</span></span>
* <span data-ttu-id="6be66-114">Come installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="6be66-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6be66-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="6be66-115">What you need</span></span>
* <span data-ttu-id="6be66-116">Un computer Windows con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="6be66-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="6be66-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="6be66-117">An active Azure subscription.</span></span> <span data-ttu-id="6be66-118">Se non si ha un account Azure, creare un [account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="6be66-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="6be66-119">Installare Python</span><span class="sxs-lookup"><span data-stu-id="6be66-119">Install Python</span></span>
<span data-ttu-id="6be66-120">[Installare Python](https://www.python.org/downloads/) nel computer Windows.</span><span class="sxs-lookup"><span data-stu-id="6be66-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="6be66-121">È possibile installare Python 2.7, 3.4 o 3.5.</span><span class="sxs-lookup"><span data-stu-id="6be66-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="6be66-122">Questa esercitazione è basata su Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="6be66-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="6be66-123">Se Python è già installato, passare alla sezione successiva e installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="6be66-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="6be66-124">È inoltre necessario aggiungere il percorso delle cartelle in cui vengono installati python.exe e pip.exe alla variabile di ambiente `PATH` del sistema.</span><span class="sxs-lookup"><span data-stu-id="6be66-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="6be66-125">Per impostazione predefinita, python.exe viene installato in `C:\Python27` e pip.exe viene installato in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="6be66-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="6be66-126">Installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="6be66-126">Install the Azure CLI</span></span>
<span data-ttu-id="6be66-127">L'interfaccia della riga di comando di Azure offre un'esperienza di riga di comando multipiattaforma per Azure.</span><span class="sxs-lookup"><span data-stu-id="6be66-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="6be66-128">Si opera direttamente dalla riga di comando per il provisioning e la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="6be66-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="6be66-129">Per installare l'interfaccia della riga di comando di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="6be66-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="6be66-130">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6be66-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="6be66-131">Eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6be66-131">Run the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="6be66-132">Verificare l'installazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6be66-132">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="6be66-133">Se l'installazione ha esito positivo, verrà visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="6be66-133">You see the following output if the installation is successful.</span></span>

![Output che indica l'esito positivo](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="6be66-135">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="6be66-135">Summary</span></span>
<span data-ttu-id="6be66-136">È stata installata l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="6be66-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="6be66-137">L'attività successiva consiste nella creazione dell'hub IoT di Azure e dell'identità del dispositivo tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="6be66-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6be66-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6be66-138">Next steps</span></span>
<span data-ttu-id="6be66-139">[Creare l'hub IoT e registrare Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="6be66-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
