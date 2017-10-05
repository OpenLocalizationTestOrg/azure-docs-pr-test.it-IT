---
title: "Verificare la connettività con Azure Network Watcher - Portale di Azure | Microsoft Docs"
description: "Questa pagina descrive come verificare la connettività con Network Watcher usando il portale di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: 84774d0f40e06a819ca6de6cf0be68e17ba474e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-the-azure-portal"></a><span data-ttu-id="3df76-103">Verificare la connettività con Azure Network Watcher usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3df76-103">Check connectivity with Azure Network Watcher using the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3df76-104">Portale</span><span class="sxs-lookup"><span data-stu-id="3df76-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="3df76-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3df76-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="3df76-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="3df76-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="3df76-107">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="3df76-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="3df76-108">Informazioni su come usare la connettività per verificare se è possibile stabilire una connessione TCP diretta da una macchina virtuale a uno specifico endpoint.</span><span class="sxs-lookup"><span data-stu-id="3df76-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3df76-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3df76-109">Before you begin</span></span>

<span data-ttu-id="3df76-110">Questo articolo presuppone che l'utente disponga delle risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="3df76-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="3df76-111">Un'istanza di Network Watcher nell'area di cui si vuole controllare la connettività.</span><span class="sxs-lookup"><span data-stu-id="3df76-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="3df76-112">Macchine virtuali con cui controllare la connettività.</span><span class="sxs-lookup"><span data-stu-id="3df76-112">Virtual machines to check connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3df76-113">Il controllo della connettività richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="3df76-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="3df76-114">Per installare l'estensione in una VM Windows, vedere [Estensione macchina virtuale agente Azure Network Watcher per Windows](../virtual-machines/windows/extensions-nwa.md) e per una VM Linux VM vedere [Estensione macchina virtuale Azure Network Watcher Agent per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="3df76-114">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="3df76-115">Controllare la connettività a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3df76-115">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="3df76-116">Questo esempio controlla la connettività a una macchina virtuale di destinazione sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="3df76-116">This example checks connectivity to a destination virtual machine over port 80.</span></span>

<span data-ttu-id="3df76-117">Passare a Network Watcher e fare clic su **Verifica della connettività (anteprima)**.</span><span class="sxs-lookup"><span data-stu-id="3df76-117">Navigate to your Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="3df76-118">Selezionare la macchina virtuale di cui si vuole verificare la connettività.</span><span class="sxs-lookup"><span data-stu-id="3df76-118">Select the virtual machine to check connectivity from.</span></span> <span data-ttu-id="3df76-119">Nella sezione **Destinazione** fare clic su **Selezionare una macchina virtuale** e scegliere la macchina virtuale e la porta da testare.</span><span class="sxs-lookup"><span data-stu-id="3df76-119">In the **Destination** section choose **Select a virtual machine** and choose the correct virtual machine and port to test.</span></span>

<span data-ttu-id="3df76-120">Quando si fa clic su **Verifica**, viene verificata la connettività tra le macchine virtuali sulla porta specificata.</span><span class="sxs-lookup"><span data-stu-id="3df76-120">Once you click **Check**, the connectivity between the virtual machines on the port specified are checked.</span></span> <span data-ttu-id="3df76-121">Nell'esempio, la macchina virtuale di destinazione non è raggiungibile e viene visualizzato un elenco di hop.</span><span class="sxs-lookup"><span data-stu-id="3df76-121">In the example, the destination VM is unreachable, a listing of hops are shown.</span></span>

![Verificare i risultati di connettività per una macchina virtuale][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="3df76-123">Verificare la connettività dell'endpoint remoto</span><span class="sxs-lookup"><span data-stu-id="3df76-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="3df76-124">Per verificare la connettività e la latenza in un endpoint remoto, scegliere il pulsante di opzione **Specificare manualmente** nella sezione **Destinazione**, immettere l'URL e la porta e fare clic su **Verifica**.</span><span class="sxs-lookup"><span data-stu-id="3df76-124">To check the connectivity and latency to a remote endpoint, choose the **Specify manually** radio button in the **Destination** section, input the url and the port and click **Check**.</span></span>  <span data-ttu-id="3df76-125">Questa procedura può essere usata per endpoint remoti come siti Web ed endpoint di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3df76-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Verificare i risultati di connettività per un sito Web][2]

## <a name="next-steps"></a><span data-ttu-id="3df76-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3df76-127">Next steps</span></span>

<span data-ttu-id="3df76-128">Per altre informazioni su come automatizzare le acquisizioni di pacchetti tramite gli avvisi della macchina virtuale, leggere l'articolo su come [creare un'acquisizione di pacchetti attivata da un avviso](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="3df76-128">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="3df76-129">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).</span><span class="sxs-lookup"><span data-stu-id="3df76-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
