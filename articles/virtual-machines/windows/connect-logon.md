---
title: Connettersi a una VM Windows Server | Microsoft Docs
description: Informazioni su come connettersi e accedere a una VM Windows mediante il portale di Azure e il modello di distribuzione Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: 88431377a36d5bc36220c630f0c8d4a46ab4a434
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-and-log-on-to-an-azure-virtual-machine-running-windows"></a><span data-ttu-id="a3701-103">Come connettersi e accedere a una macchina virtuale di Azure che esegue Windows</span><span class="sxs-lookup"><span data-stu-id="a3701-103">How to connect and log on to an Azure virtual machine running Windows</span></span>
<span data-ttu-id="a3701-104">Per avviare una sessione di Desktop remoto (RDP) da un desktop di Windows, sarà necessario usare il pulsante **Connetti** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3701-104">You'll use the **Connect** button in the Azure portal to start a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="a3701-105">Effettuare la connessione alla macchina virtuale, quindi accedere al sistema.</span><span class="sxs-lookup"><span data-stu-id="a3701-105">First you connect to the virtual machine, then you log on.</span></span>

<span data-ttu-id="a3701-106">Se si sta tentando di effettuare la connessione a una macchina virtuale Windows da un Mac, è necessario installare un client RDP per Mac come [Desktop remoto Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="a3701-106">If you are trying to connect to a Windows VM from a Mac, you need to install an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="a3701-107">Connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a3701-107">Connect to the virtual machine</span></span>
1. <span data-ttu-id="a3701-108">Accedere al [portale di Azure](https://portal.azure.com/), se questa operazione non è già stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="a3701-108">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a3701-109">Scegliere **Macchine virtuali**dal menu Hub.</span><span class="sxs-lookup"><span data-stu-id="a3701-109">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="a3701-110">Selezionare la macchina virtuale dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="a3701-110">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="a3701-111">Nel pannello della macchina virtuale fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="a3701-111">On the blade for the virtual machine, click **Connect**.</span></span>
   
    ![Screenshot del portale di Azure che illustra come connettersi alla VM.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="a3701-113">Se il pulsante **Connetti** nel portale è disattivato e non si è connessi ad Azure tramite una connessione [Express Route](../../expressroute/expressroute-introduction.md) o [VPN da sito a sito](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), per poter usare il protocollo RDP è necessario creare un indirizzo IP pubblico e assegnarlo alla VM.</span><span class="sxs-lookup"><span data-stu-id="a3701-113">If the **Connect** button in the portal is greyed out and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="a3701-114">Altre informazioni sono disponibili in [Indirizzi IP pubblici in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a3701-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="a3701-115">Accesso alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a3701-115">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="a3701-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3701-116">Next steps</span></span>
<span data-ttu-id="a3701-117">In caso di problemi quando si cerca di eseguire la connessione, vedere [Risolvere i problemi di connessioni Desktop remoto](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a3701-117">If you run into trouble when you try to connect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a3701-118">In questo articolo viene illustrato come diagnosticare e risolvere i problemi più comuni.</span><span class="sxs-lookup"><span data-stu-id="a3701-118">This article walks you through diagnosing and resolving common problems.</span></span>

