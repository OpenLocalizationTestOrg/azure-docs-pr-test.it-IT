---
title: 'Connettere Intel Edison (C) ad Azure IoT: lezione 2: Strumenti di Azure (macOS) | Documentazione Microsoft'
description: Installare Python e l'interfaccia della riga di comando di Azure in macOS.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interfaccia della riga di comando di azure, servizio cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97beb04781f3f9809cdafc945d9499e71cbbd9b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="9d04b-104">Ottenere gli strumenti di Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="9d04b-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="9d04b-105">[Windows 7 e versioni successive][windows]</span><span class="sxs-lookup"><span data-stu-id="9d04b-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="9d04b-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="9d04b-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="9d04b-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="9d04b-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9d04b-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="9d04b-108">What you will do</span></span>
<span data-ttu-id="9d04b-109">Installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d04b-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="9d04b-110">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="9d04b-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9d04b-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="9d04b-111">What you will learn</span></span>
<span data-ttu-id="9d04b-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="9d04b-112">In this article, you will learn:</span></span>
* <span data-ttu-id="9d04b-113">Come installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d04b-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="9d04b-114">Come aggiungere un sottogruppo IoT dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d04b-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9d04b-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="9d04b-115">What you need</span></span>
* <span data-ttu-id="9d04b-116">Un Mac con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="9d04b-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="9d04b-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="9d04b-117">An active Azure subscription.</span></span> <span data-ttu-id="9d04b-118">Se non si ha un account Azure, è possibile [creare un account Azure gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9d04b-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="9d04b-119">Installare Python</span><span class="sxs-lookup"><span data-stu-id="9d04b-119">Install Python</span></span>
<span data-ttu-id="9d04b-120">Anche se Python 2.7 è preinstallato in macOS, è consigliabile installarlo tramite Homebrew.</span><span class="sxs-lookup"><span data-stu-id="9d04b-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="9d04b-121">Vedere [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/) (Installazione di Python in macOS).</span><span class="sxs-lookup"><span data-stu-id="9d04b-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="9d04b-122">Installare Python ed eseguire i parametri di inizializzazione del programma tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9d04b-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="9d04b-123">Installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="9d04b-123">Install the Azure CLI</span></span>
<span data-ttu-id="9d04b-124">L'interfaccia della riga di comando di Azure offre un'esperienza di riga di comando multipiattaforma per Azure.</span><span class="sxs-lookup"><span data-stu-id="9d04b-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="9d04b-125">Si opera direttamente dalla riga di comando per il provisioning e la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="9d04b-125">You work directly from your command line to provision and manage resources.</span></span> 

<span data-ttu-id="9d04b-126">Per installare l'interfaccia della riga di comando di Azure più recente, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="9d04b-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="9d04b-127">Eseguire i comandi seguenti in una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="9d04b-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="9d04b-128">L'installazione dell'interfaccia della riga di comando di Azure può richiedere cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="9d04b-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="9d04b-129">Verificare l'installazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9d04b-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="9d04b-130">Se l'installazione ha esito positivo, verrà visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="9d04b-130">You should see the following output if the installation is successful.</span></span>

![Output che indica l'esito positivo](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="9d04b-132">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="9d04b-132">Summary</span></span>
<span data-ttu-id="9d04b-133">È stata installata l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d04b-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="9d04b-134">L'attività successiva consiste nella creazione dell'hub IoT di Azure e dell'identità del dispositivo tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d04b-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d04b-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d04b-135">Next steps</span></span>
<span data-ttu-id="9d04b-136">[Creare l'hub IoT e registrare Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="9d04b-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
