---
title: Installare MongoDB in una VM Windows in Azure | Documentazione Microsoft
description: Informazioni su come installare MongoDB in una macchina virtuale di Azure creata con il modello di distribuzione classica che esegue Windows Server.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: 6b5af18d02fd508a21cdc21b38b1c16e79f07ecb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="1b15c-103">Installare MongoDB in una VM Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="1b15c-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1b15c-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1b15c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="1b15c-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="1b15c-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="1b15c-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="1b15c-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="1b15c-107">Per installare e configurare MongoDB tramite il modello di distribuzione Resource Manager, vedere [questo articolo](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="1b15c-107">To install and configure MongoDB using the Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="1b15c-108">[MongoDB][MongoDB] è un diffuso database NoSQL open source a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="1b15c-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="1b15c-109">Questo articolo illustra come creare una macchina virtuale (VM) di Windows Server usando il [portale di Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="1b15c-109">This article guides you through creating a Windows Server virtual machine (VM) using the [Azure portal][AzurePortal].</span></span> <span data-ttu-id="1b15c-110">Quindi, creare e collegare un disco dati alla macchina virtuale prima di installare e configurare MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1b15c-110">You then create and attach a data disk to the VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="1b15c-111">Se in Azure è già disponibile una macchina virtuale da usare, è possibile passare direttamente all'[installazione e configurazione di MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="1b15c-111">If you have an existing VM in Azure that you would like to use, you can jump straight to [installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="1b15c-112">Creare una macchina virtuale che esegue Windows Server</span><span class="sxs-lookup"><span data-stu-id="1b15c-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="1b15c-113">Per creare una macchina virtuale, seguire queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="1b15c-113">Follow these instructions to create a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="1b15c-114">Durante la creazione della macchina virtuale, è possibile aggiungere un endpoint per MongoDB e configurarlo come segue: denominarlo **Mongo**, usare il protocollo **TCP** e impostare le porte pubbliche e private su **27017**.</span><span class="sxs-lookup"><span data-stu-id="1b15c-114">You can add an endpoint for MongoDB while creating the virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as the protocol, and set both the public and private ports to **27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="1b15c-115">Collegamento di un disco dati</span><span class="sxs-lookup"><span data-stu-id="1b15c-115">Attach a data disk</span></span>
<span data-ttu-id="1b15c-116">Per fornire la risorsa di archiviazione per la macchina virtuale, collegare un disco dati e inizializzarlo affinché possa essere utilizzato da Windows.</span><span class="sxs-lookup"><span data-stu-id="1b15c-116">To provide storage for the virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="1b15c-117">È possibile collegare un eventuale disco dati esistente o collegare un disco vuoto.</span><span class="sxs-lookup"><span data-stu-id="1b15c-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="1b15c-118">Per istruzioni sull’inizializzazione del disco, vedere "Procedura: inizializzazione di un nuovo disco dati in Windows Server" in [Come collegare un disco dati a una macchina virtuale di Windows](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="1b15c-118">For instructions on initializing the disk, see "How to: Initialize a new data disk in Windows Server" in [How to attach a data disk to a Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-the-virtual-machine"></a><span data-ttu-id="1b15c-119">Installare ed eseguire MongoDB nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1b15c-119">Install and run MongoDB on the virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="1b15c-120">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="1b15c-120">Summary</span></span>
<span data-ttu-id="1b15c-121">In questa esercitazione è stato illustrato come creare una macchina virtuale che esegue Windows Server, come stabilire una connessione remota a quest'ultima e come collegare un disco dati.</span><span class="sxs-lookup"><span data-stu-id="1b15c-121">In this tutorial, you learned how to create a virtual machine running Windows Server, remotely connect to it, and attach a data disk.</span></span>  <span data-ttu-id="1b15c-122">È stato inoltre illustrato come installare e configurare MongoDB sulla macchina virtuale basata su Windows.</span><span class="sxs-lookup"><span data-stu-id="1b15c-122">You also learned how to install and configure MongoDB on the Windows-based virtual machine.</span></span> <span data-ttu-id="1b15c-123">È ora possibile accedere a MongoDB nella macchina virtuale basata su Windows, seguendo gli argomenti avanzati illustrati nella [documentazione di MongoDB][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="1b15c-123">You can now access MongoDB on the Windows-based virtual machine, by following the advanced topics in the [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

