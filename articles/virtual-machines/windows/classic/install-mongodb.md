---
title: aaaInstall MongoDB in una macchina virtuale Windows in Azure | Documenti Microsoft
description: Informazioni su come creare i tooinstall MongoDB in una macchina virtuale di Azure con il modello di distribuzione classica hello che esegue Windows Server.
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
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="0051c-103">Installare MongoDB in una VM Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="0051c-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0051c-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0051c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="0051c-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="0051c-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0051c-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="0051c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0051c-107">tooinstall e configurare MongoDB mediante modello di distribuzione di gestione risorse di hello, vedere [questo articolo](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="0051c-107">tooinstall and configure MongoDB using hello Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="0051c-108">[MongoDB][MongoDB] è un diffuso database NoSQL open source a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="0051c-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="0051c-109">In questo articolo viene descritta la creazione di una macchina virtuale Windows Server (VM) hello [portale di Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="0051c-109">This article guides you through creating a Windows Server virtual machine (VM) using hello [Azure portal][AzurePortal].</span></span> <span data-ttu-id="0051c-110">Creare e collegare un toohello disco dati VM prima dell'installazione e configurazione di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0051c-110">You then create and attach a data disk toohello VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="0051c-111">Se si dispone di una macchina virtuale esistente in cui si desidera toouse Azure, è possibile passare direttamente troppo[installazione e configurazione di MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="0051c-111">If you have an existing VM in Azure that you would like toouse, you can jump straight too[installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="0051c-112">Creare una macchina virtuale che esegue Windows Server</span><span class="sxs-lookup"><span data-stu-id="0051c-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="0051c-113">Seguire questi toocreate istruzioni una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0051c-113">Follow these instructions toocreate a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="0051c-114">È possibile aggiungere un endpoint per MongoDB durante la creazione della macchina virtuale hello e configurarlo come segue: il nome come **Mongo**, utilizzare **TCP** come protocollo di hello e impostare entrambi hello porte pubbliche e private troppo**27017**.</span><span class="sxs-lookup"><span data-stu-id="0051c-114">You can add an endpoint for MongoDB while creating hello virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as hello protocol, and set both hello public and private ports too**27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="0051c-115">Collegamento di un disco dati</span><span class="sxs-lookup"><span data-stu-id="0051c-115">Attach a data disk</span></span>
<span data-ttu-id="0051c-116">archiviazione tooprovide per la macchina virtuale hello, collegare un disco dati e quindi inizializzarlo in modo che Windows è possibile utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="0051c-116">tooprovide storage for hello virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="0051c-117">È possibile collegare un eventuale disco dati esistente o collegare un disco vuoto.</span><span class="sxs-lookup"><span data-stu-id="0051c-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="0051c-118">Per istruzioni sull'inizializzazione di hello disco, vedere "procedura: inizializzare un nuovo disco dati in Windows Server" in [come tooattach dati disco macchina virtuale di Windows tooa](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="0051c-118">For instructions on initializing hello disk, see "How to: Initialize a new data disk in Windows Server" in [How tooattach a data disk tooa Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a><span data-ttu-id="0051c-119">Installare ed eseguire MongoDB sulla macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="0051c-119">Install and run MongoDB on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="0051c-120">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="0051c-120">Summary</span></span>
<span data-ttu-id="0051c-121">In questa esercitazione è stato come toocreate una macchina virtuale che esegue Windows Server, in modalità remota connettersi tooit e collegare un disco dati.</span><span class="sxs-lookup"><span data-stu-id="0051c-121">In this tutorial, you learned how toocreate a virtual machine running Windows Server, remotely connect tooit, and attach a data disk.</span></span>  <span data-ttu-id="0051c-122">È inoltre appreso tooinstall e configurare MongoDB nella macchina virtuale basato su Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0051c-122">You also learned how tooinstall and configure MongoDB on hello Windows-based virtual machine.</span></span> <span data-ttu-id="0051c-123">È ora possibile accedere MongoDB sulla macchina virtuale basato su Windows hello, da seguenti hello avanzata nel hello [documentazione di MongoDB][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="0051c-123">You can now access MongoDB on hello Windows-based virtual machine, by following hello advanced topics in hello [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

