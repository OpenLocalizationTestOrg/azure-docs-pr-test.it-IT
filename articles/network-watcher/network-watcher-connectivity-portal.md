---
title: "connettività aaaCheck con Watcher di rete di Azure - portale di Azure | Documenti Microsoft"
description: "Questa pagina viene illustrato come toouse connettività verificare con il Watcher di rete utilizzando hello portale di Azure"
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
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="d43ad-103">Verificare la connettività con Watcher di rete di Azure utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d43ad-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d43ad-104">Portale</span><span class="sxs-lookup"><span data-stu-id="d43ad-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="d43ad-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d43ad-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="d43ad-106">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="d43ad-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="d43ad-107">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="d43ad-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="d43ad-108">Informazioni su come è possibile stabilire toouse connettività tooverify se una connessione TCP diretta da una macchina virtuale di tooa dato endpoint.</span><span class="sxs-lookup"><span data-stu-id="d43ad-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d43ad-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d43ad-109">Before you begin</span></span>

<span data-ttu-id="d43ad-110">Questo articolo si presuppone di che aver hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="d43ad-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="d43ad-111">Un'istanza del controllo di rete nell'area di hello desiderato toocheck connettività.</span><span class="sxs-lookup"><span data-stu-id="d43ad-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="d43ad-112">Connettività toocheck di macchine virtuali con.</span><span class="sxs-lookup"><span data-stu-id="d43ad-112">Virtual machines toocheck connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d43ad-113">Il controllo della connettività richiede un'estensione macchina virtuale `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="d43ad-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="d43ad-114">Per l'installazione dell'estensione hello in una macchina virtuale di Windows, visitare [estensione della macchina virtuale Azure rete Watcher agente per Windows](../virtual-machines/windows/extensions-nwa.md) e per la visita di VM Linux [estensione della macchina virtuale Azure rete Watcher agente per Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="d43ad-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="d43ad-115">Verificare la connettività tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="d43ad-115">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="d43ad-116">Questo esempio viene verificata la connettività tooa macchina virtuale di destinazione sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="d43ad-116">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

<span data-ttu-id="d43ad-117">Passare tooyour Watcher di rete e fare clic su **verifica della connettività (anteprima)**.</span><span class="sxs-lookup"><span data-stu-id="d43ad-117">Navigate tooyour Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="d43ad-118">Selezionare la connettività di hello macchina virtuale toocheck da.</span><span class="sxs-lookup"><span data-stu-id="d43ad-118">Select hello virtual machine toocheck connectivity from.</span></span> <span data-ttu-id="d43ad-119">In hello **destinazione** sezione scegliere **selezionare una macchina virtuale** e scegliere porta tootest e la macchina virtuale corretta hello.</span><span class="sxs-lookup"><span data-stu-id="d43ad-119">In hello **Destination** section choose **Select a virtual machine** and choose hello correct virtual machine and port tootest.</span></span>

<span data-ttu-id="d43ad-120">Quando si fa clic su **controllare**, vengono controllati connettività hello tra le macchine virtuali hello sulla porta hello specificato.</span><span class="sxs-lookup"><span data-stu-id="d43ad-120">Once you click **Check**, hello connectivity between hello virtual machines on hello port specified are checked.</span></span> <span data-ttu-id="d43ad-121">Nell'esempio hello hello destinazione macchina virtuale non è raggiungibile, vengono visualizzati un elenco di hop.</span><span class="sxs-lookup"><span data-stu-id="d43ad-121">In hello example, hello destination VM is unreachable, a listing of hops are shown.</span></span>

![Verificare i risultati di connettività per una macchina virtuale][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="d43ad-123">Verificare la connettività dell'endpoint remoto</span><span class="sxs-lookup"><span data-stu-id="d43ad-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="d43ad-124">connettività hello toocheck e l'endpoint remoto tooa di latenza, scegliere hello **specificare manualmente** pulsante di opzione nella hello **destinazione** sezione input hello url e la porta hello e fare clic su **controllare** .</span><span class="sxs-lookup"><span data-stu-id="d43ad-124">toocheck hello connectivity and latency tooa remote endpoint, choose hello **Specify manually** radio button in hello **Destination** section, input hello url and hello port and click **Check**.</span></span>  <span data-ttu-id="d43ad-125">Questa procedura può essere usata per endpoint remoti come siti Web ed endpoint di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d43ad-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Verificare i risultati di connettività per un sito Web][2]

## <a name="next-steps"></a><span data-ttu-id="d43ad-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d43ad-127">Next steps</span></span>

<span data-ttu-id="d43ad-128">Informazioni su come acquisizioni di pacchetti tooautomate con gli avvisi di macchina virtuale visualizzando [creare un'acquisizione pacchetto attivati avvisi](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="d43ad-128">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="d43ad-129">Per stabilire se un traffico specificato è consentito all'interno o all'esterno di una macchina virtuale, vedere [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Controllare la verifica del flusso IP).</span><span class="sxs-lookup"><span data-stu-id="d43ad-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
