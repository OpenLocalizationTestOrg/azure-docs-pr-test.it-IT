---
title: Accesso a Macchine virtuali di Azure da Esplora server | Documentazione Microsoft
description: Panoramica su come visualizzare, creare e gestire macchine virtuali di Azure (VM) in Esplora Server in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fcbb00cc2f00691e25ea84333e8c418b08210a67
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a><span data-ttu-id="a3df2-103">Accesso alle macchine virtuali di Azure da Esplora server</span><span class="sxs-lookup"><span data-stu-id="a3df2-103">Accessing Azure Virtual Machines from Server Explorer</span></span>
<span data-ttu-id="a3df2-104">Con Esplora server in Visual Studio è possibile visualizzare informazioni sulle macchine virtuali ospitate da Azure.</span><span class="sxs-lookup"><span data-stu-id="a3df2-104">By using Server Explorer in Visual Studio, you can display information about your virtual machines hosted by Azure.</span></span>

## <a name="accessing-virtual-machines-in-server-explorer"></a><span data-ttu-id="a3df2-105">Accesso alle macchine virtuali in Esplora server</span><span class="sxs-lookup"><span data-stu-id="a3df2-105">Accessing virtual machines in Server Explorer</span></span>
<span data-ttu-id="a3df2-106">Se ci sono macchine virtuali ospitate da Azure, è possibile accedervi in Esplora server.</span><span class="sxs-lookup"><span data-stu-id="a3df2-106">If you have virtual machines hosted by Azure, you can access them in Server Explorer.</span></span> <span data-ttu-id="a3df2-107">Per visualizzare i servizi mobili, è necessario prima di tutto accedere alla sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="a3df2-107">You must first sign in to your Azure subscription to view your mobile services.</span></span> <span data-ttu-id="a3df2-108">Per accedere, aprire il menu di scelta rapida per il nodo Azure e scegliere **Connetti a Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="a3df2-108">To sign in, open the shortcut menu for the Azure node in Server Explorer, and choose **Connect to Microsoft Azure**.</span></span>

### <a name="to-get-information-about-your-virtual-machines"></a><span data-ttu-id="a3df2-109">Per ottenere informazioni sulle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="a3df2-109">To get information about your virtual machines</span></span>
1. <span data-ttu-id="a3df2-110">In Esplora server scegliere una macchina virtuale, quindi premere F4 per visualizzare la finestra delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="a3df2-110">In Server Explorer, choose a virtual machine, and then choose the F4 key to show its properties window.</span></span>
   
    <span data-ttu-id="a3df2-111">La tabella seguente illustra le proprietà disponibili, le quali sono tuttavia di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="a3df2-111">The following table shows what properties are available, but they are all read-only.</span></span> <span data-ttu-id="a3df2-112">Per modificarle, usare il [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="a3df2-112">To change them, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
   
   | <span data-ttu-id="a3df2-113">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a3df2-113">Property</span></span> | <span data-ttu-id="a3df2-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a3df2-114">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="a3df2-115">Nome DNS</span><span class="sxs-lookup"><span data-stu-id="a3df2-115">DNS Name</span></span> |<span data-ttu-id="a3df2-116">URL con l'indirizzo Internet della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a3df2-116">The URL with the Internet address of the virtual machine.</span></span> |
   | <span data-ttu-id="a3df2-117">Environment</span><span class="sxs-lookup"><span data-stu-id="a3df2-117">Environment</span></span> |<span data-ttu-id="a3df2-118">Per una macchina virtuale, il valore di questa proprietà è sempre Produzione.</span><span class="sxs-lookup"><span data-stu-id="a3df2-118">For a virtual machine, the value of this property is always Production.</span></span> |
   | <span data-ttu-id="a3df2-119">Name</span><span class="sxs-lookup"><span data-stu-id="a3df2-119">Name</span></span> |<span data-ttu-id="a3df2-120">Nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a3df2-120">The name of the virtual machine.</span></span> |
   | <span data-ttu-id="a3df2-121">Dimensione</span><span class="sxs-lookup"><span data-stu-id="a3df2-121">Size</span></span> |<span data-ttu-id="a3df2-122">Dimensioni della macchina virtuale corrispondenti alla quantità di memoria e spazio su disco disponibili.</span><span class="sxs-lookup"><span data-stu-id="a3df2-122">The size of the virtual machine, which reflects the amount of memory and disk space that’s available.</span></span> <span data-ttu-id="a3df2-123">Per altre informazioni, vedere Come configurare le dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a3df2-123">For more information, see How To: Configure Virtual Machine Sizes.</span></span> |
   | <span data-ttu-id="a3df2-124">Stato</span><span class="sxs-lookup"><span data-stu-id="a3df2-124">Status</span></span> |<span data-ttu-id="a3df2-125">I valori includono Avvio in corso, Avviato, Arresto, Arrestato e Recupero dello stato.</span><span class="sxs-lookup"><span data-stu-id="a3df2-125">Values include Starting, Started, Stopping, Stopped, and Retrieving Status.</span></span> <span data-ttu-id="a3df2-126">Se viene visualizzato Recupero dello stato, lo stato corrente è sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="a3df2-126">If Retrieving Status appears, the current status is unknown.</span></span> <span data-ttu-id="a3df2-127">I valori di questa proprietà differiscono da quelli usati nel [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="a3df2-127">The values for this property differ from the values that are used on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> |
   | <span data-ttu-id="a3df2-128">SubscriptionID</span><span class="sxs-lookup"><span data-stu-id="a3df2-128">SubscriptionID</span></span> |<span data-ttu-id="a3df2-129">ID sottoscrizione dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="a3df2-129">The subscription ID for your Azure account.</span></span> <span data-ttu-id="a3df2-130">È possibile vedere queste informazioni nel [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885) visualizzando le proprietà di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a3df2-130">You can show this information on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) by viewing the properties for a subscription.</span></span> |
2. <span data-ttu-id="a3df2-131">Scegliere un nodo di endpoint e quindi visualizzare la finestra **Proprietà** .</span><span class="sxs-lookup"><span data-stu-id="a3df2-131">Choose an endpoint node, and then view the **Properties** window.</span></span>
3. <span data-ttu-id="a3df2-132">La tabella seguente descrive le proprietà disponibili degli endpoint, che però sono di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="a3df2-132">The following table describes the available properties of endpoints, but they are read-only.</span></span> <span data-ttu-id="a3df2-133">Per aggiungere o modificare gli endpoint di una macchina virtuale, usare il [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="a3df2-133">To add or edit the endpoints for a virtual machine, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> 
   
   | <span data-ttu-id="a3df2-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a3df2-134">Property</span></span> | <span data-ttu-id="a3df2-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a3df2-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="a3df2-136">Name</span><span class="sxs-lookup"><span data-stu-id="a3df2-136">Name</span></span> |<span data-ttu-id="a3df2-137">Identificatore dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="a3df2-137">An identifier for the endpoint.</span></span> |
   | <span data-ttu-id="a3df2-138">Private Port</span><span class="sxs-lookup"><span data-stu-id="a3df2-138">Private Port</span></span> |<span data-ttu-id="a3df2-139">Porta per l'accesso di rete interno all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a3df2-139">The port for network access internal to your application.</span></span> |
   | <span data-ttu-id="a3df2-140">Protocol</span><span class="sxs-lookup"><span data-stu-id="a3df2-140">Protocol</span></span> |<span data-ttu-id="a3df2-141">Protocollo usato dal livello di trasporto per l'endpoint TCP o UDP.</span><span class="sxs-lookup"><span data-stu-id="a3df2-141">The protocol that the transport layer for this endpoint uses, either TCP or UDP.</span></span> |
   | <span data-ttu-id="a3df2-142">Public Port</span><span class="sxs-lookup"><span data-stu-id="a3df2-142">Public Port</span></span> |<span data-ttu-id="a3df2-143">Porta usata per l'accesso pubblico all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a3df2-143">The port that’s used for public access to your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a3df2-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3df2-144">Next steps</span></span>
<span data-ttu-id="a3df2-145">Per ulteriori informazioni sull'utilizzo dei ruoli di Azure in Visual Studio, vedere [Utilizzo di Desktop remoto con i ruoli di Azure](vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a3df2-145">To learn more about using Azure roles in Visual Studio, see [Using Remote Desktop with Azure Roles](vs-azure-tools-remote-desktop-roles.md).</span></span>

