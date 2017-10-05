---
title: 'Connettere Intel Edison (C) ad Azure IoT: lezione 2: Strumenti di Azure (Ubuntu) | Documentazione Microsoft'
description: Installare Python e l'interfaccia della riga di comando di Azure in Ubuntu.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interfaccia della riga di comando di azure, servizio cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 2463cb8e-5758-4d72-af98-62520d41f2f7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 897ab63af85a1f830ed49084ce7c3e74c84a4cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="605b5-104">Ottenere gli strumenti di Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="605b5-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="605b5-105">[Windows 7 e versioni successive][windows]</span><span class="sxs-lookup"><span data-stu-id="605b5-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="605b5-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="605b5-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="605b5-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="605b5-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="605b5-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="605b5-108">What you will do</span></span>
<span data-ttu-id="605b5-109">Installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="605b5-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="605b5-110">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="605b5-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="605b5-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="605b5-111">What you will learn</span></span>
<span data-ttu-id="605b5-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="605b5-112">In this article, you will learn:</span></span>
* <span data-ttu-id="605b5-113">Come installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="605b5-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="605b5-114">Come aggiungere un sottogruppo IoT dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="605b5-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="605b5-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="605b5-115">What you need</span></span>
* <span data-ttu-id="605b5-116">Un computer Ubuntu con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="605b5-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="605b5-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="605b5-117">An active Azure subscription.</span></span> <span data-ttu-id="605b5-118">Se non si ha un account, è possibile creare un [account di valutazione gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="605b5-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="605b5-119">Installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="605b5-119">Install the Azure CLI</span></span>
<span data-ttu-id="605b5-120">L'interfaccia della riga di comando di Azure offre un'esperienza multipiattaforma per Azure, permettendo di lavorare direttamente dalla riga di comando per effettuare il provisioning delle risorse e gestirle.</span><span class="sxs-lookup"><span data-stu-id="605b5-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="605b5-121">Per installare l'interfaccia della riga di comando di Azure più recente, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="605b5-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="605b5-122">Eseguire i comandi seguenti in una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="605b5-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="605b5-123">L'installazione dell'interfaccia della riga di comando di Azure può richiedere cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="605b5-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="605b5-124">Verificare l'installazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="605b5-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="605b5-125">Se l'installazione ha esito positivo, verrà visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="605b5-125">You should see the following output if the installation is successful.</span></span>

![Output che indica l'esito positivo](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="605b5-127">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="605b5-127">Summary</span></span>
<span data-ttu-id="605b5-128">È stata installata l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="605b5-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="605b5-129">L'attività successiva consiste nella creazione dell'hub IoT di Azure e dell'identità del dispositivo tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="605b5-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="605b5-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="605b5-130">Next steps</span></span>
<span data-ttu-id="605b5-131">[Creare l'hub IoT e registrare Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="605b5-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
