---
title: 'Connettere Raspberry Pi (C) ad Azure IoT: lezione 2: Strumenti di Azure (Ubuntu) | Documentazione Microsoft'
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
ms.openlocfilehash: be1506edf0e63190dbb85a3adb7897bd1cc84d38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="79c7c-104">Ottenere gli strumenti di Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="79c7c-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79c7c-105">Windows 7 e versioni successive</span><span class="sxs-lookup"><span data-stu-id="79c7c-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="79c7c-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="79c7c-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="79c7c-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="79c7c-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="79c7c-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="79c7c-108">What you will do</span></span>
<span data-ttu-id="79c7c-109">Installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="79c7c-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="79c7c-110">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="79c7c-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="79c7c-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="79c7c-111">What you will learn</span></span>
<span data-ttu-id="79c7c-112">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="79c7c-112">In this article, you will learn:</span></span>
* <span data-ttu-id="79c7c-113">Come installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="79c7c-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="79c7c-114">Come aggiungere un sottogruppo IoT dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="79c7c-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="79c7c-115">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="79c7c-115">What you need</span></span>
* <span data-ttu-id="79c7c-116">Un computer Ubuntu con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="79c7c-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="79c7c-117">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="79c7c-117">An active Azure subscription.</span></span> <span data-ttu-id="79c7c-118">Se non si ha un account, è possibile creare un [account di valutazione gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="79c7c-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="79c7c-119">Installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="79c7c-119">Install the Azure CLI</span></span>
<span data-ttu-id="79c7c-120">L'interfaccia della riga di comando di Azure offre un'esperienza multipiattaforma per Azure, permettendo di lavorare direttamente dalla riga di comando per effettuare il provisioning delle risorse e gestirle.</span><span class="sxs-lookup"><span data-stu-id="79c7c-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="79c7c-121">Per installare l'interfaccia della riga di comando di Azure più recente, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="79c7c-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="79c7c-122">Eseguire i comandi seguenti in una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="79c7c-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="79c7c-123">L'installazione dell'interfaccia della riga di comando di Azure può richiedere cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="79c7c-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="79c7c-124">Verificare l'installazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="79c7c-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="79c7c-125">Se l'installazione ha esito positivo, verrà visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="79c7c-125">You should see the following output if the installation is successful.</span></span>

![Output che indica l'esito positivo](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="79c7c-127">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="79c7c-127">Summary</span></span>
<span data-ttu-id="79c7c-128">È stata installata l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="79c7c-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="79c7c-129">L'attività successiva consiste nella creazione dell'hub IoT di Azure e dell'identità del dispositivo tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="79c7c-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79c7c-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="79c7c-130">Next steps</span></span>
[<span data-ttu-id="79c7c-131">Creare l'hub IoT e registrare Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="79c7c-131">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

