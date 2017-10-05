---
title: 'Connettere Arduino ad Azure IoT: lezione 2: Strumenti di Azure (macOS) | Documentazione Microsoft'
description: Installare Python e l'interfaccia della riga di comando di Azure in macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interfaccia della riga di comando di azure, servizio cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9b719293-01d2-4a2d-9c49-476e67f4816d
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 037f8e3dba542773185fde43a345d5fd487b2d84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="5b600-104">Ottenere gli strumenti di Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="5b600-104">Get Azure tools (macOS 10.10)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="5b600-105">[Windows 7 o versione successiva][windows]</span><span class="sxs-lookup"><span data-stu-id="5b600-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="5b600-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="5b600-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="5b600-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="5b600-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5b600-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5b600-108">What you will do</span></span>

<span data-ttu-id="5b600-109">Installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b600-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="5b600-110">In caso di problemi con la scheda Arduino per Adafruit Feather M0 WiFi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5b600-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5b600-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5b600-111">What you will learn</span></span>
<span data-ttu-id="5b600-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="5b600-112">In this article, you will learn:</span></span>
* <span data-ttu-id="5b600-113">Come installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b600-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="5b600-114">Come aggiungere un sottogruppo IoT dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b600-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5b600-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="5b600-115">What you need</span></span>
* <span data-ttu-id="5b600-116">Un Mac con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="5b600-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="5b600-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="5b600-117">An active Azure subscription.</span></span> <span data-ttu-id="5b600-118">Se non si ha un account Azure, è possibile [creare un account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="5b600-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="5b600-119">Installare Python</span><span class="sxs-lookup"><span data-stu-id="5b600-119">Install Python</span></span>
<span data-ttu-id="5b600-120">Anche se Python 2.7 è preinstallato in macOS, è consigliabile installarlo tramite Homebrew.</span><span class="sxs-lookup"><span data-stu-id="5b600-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="5b600-121">Vedere [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/) (Installazione di Python in macOS).</span><span class="sxs-lookup"><span data-stu-id="5b600-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="5b600-122">Installare Python ed eseguire i parametri di inizializzazione del programma tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5b600-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="5b600-123">Installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="5b600-123">Install the Azure CLI</span></span>
<span data-ttu-id="5b600-124">L'interfaccia della riga di comando di Azure offre un'esperienza di riga di comando multipiattaforma per Azure.</span><span class="sxs-lookup"><span data-stu-id="5b600-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="5b600-125">Si opera direttamente dalla riga di comando per il provisioning e la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="5b600-125">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="5b600-126">Per installare l'interfaccia della riga di comando di Azure più recente, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="5b600-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="5b600-127">Eseguire i comandi seguenti in una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="5b600-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="5b600-128">L'installazione dell'interfaccia della riga di comando di Azure può richiedere cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="5b600-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="5b600-129">Verificare l'installazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5b600-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="5b600-130">Se l'installazione ha esito positivo, verrà visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="5b600-130">You should see the following output if the installation is successful.</span></span>

![Output che indica l'esito positivo][output]

## <a name="summary"></a><span data-ttu-id="5b600-132">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5b600-132">Summary</span></span>
<span data-ttu-id="5b600-133">È stata installata l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b600-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="5b600-134">L'attività successiva consiste nella creazione dell'hub IoT di Azure e dell'identità del dispositivo tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b600-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b600-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b600-135">Next steps</span></span>
<span data-ttu-id="5b600-136">[Creare l'hub IoT e registrare la scheda Arduino][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="5b600-136">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_osx.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md