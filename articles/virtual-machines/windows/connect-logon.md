---
title: aaaConnect tooa macchina virtuale Windows Server | Documenti Microsoft
description: Informazioni su come tooconnect e accedere utilizzando la macchina virtuale Windows tooa hello Azure portal e hello Gestione risorse modello di distribuzione.
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
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a><span data-ttu-id="059f9-103">Come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows</span><span class="sxs-lookup"><span data-stu-id="059f9-103">How tooconnect and log on tooan Azure virtual machine running Windows</span></span>
<span data-ttu-id="059f9-104">Si userà hello **Connetti** pulsante hello Azure toostart portale una sessione di Desktop remoto (RDP) da un desktop di Windows.</span><span class="sxs-lookup"><span data-stu-id="059f9-104">You'll use hello **Connect** button in hello Azure portal toostart a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="059f9-105">Prima connettersi macchina virtuale toohello, quindi si accede.</span><span class="sxs-lookup"><span data-stu-id="059f9-105">First you connect toohello virtual machine, then you log on.</span></span>

<span data-ttu-id="059f9-106">Se si sta tentando di tooconnect tooa macchina virtuale Windows da un Mac, è necessario un client RDP per Mac come tooinstall [Desktop remoto Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="059f9-106">If you are trying tooconnect tooa Windows VM from a Mac, you need tooinstall an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="059f9-107">Connettere la macchina virtuale di toohello</span><span class="sxs-lookup"><span data-stu-id="059f9-107">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="059f9-108">Se non già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="059f9-108">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="059f9-109">Nel menu Hub hello, fare clic su **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="059f9-109">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="059f9-110">Selezionare macchina virtuale hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="059f9-110">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="059f9-111">Nel Pannello di hello per la macchina virtuale hello, fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="059f9-111">On hello blade for hello virtual machine, click **Connect**.</span></span>
   
    ![Schermata di hello che Mostra portale Azure come tooconnect tooyour macchina virtuale.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="059f9-113">Se hello **Connetti** pulsante nel portale di hello è disattivata e non si è connessi tooAzure tramite un [Express Route](../../expressroute/expressroute-introduction.md) o [VPN Site-to-Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connessione, è necessario toocreate e assegnare la macchina virtuale un indirizzo IP pubblico per poter utilizzare il protocollo RDP.</span><span class="sxs-lookup"><span data-stu-id="059f9-113">If hello **Connect** button in hello portal is greyed out and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="059f9-114">Altre informazioni sono disponibili in [Indirizzi IP pubblici in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="059f9-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="059f9-115">Accedere alla macchina virtuale toohello</span><span class="sxs-lookup"><span data-stu-id="059f9-115">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="059f9-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="059f9-116">Next steps</span></span>
<span data-ttu-id="059f9-117">Se si verificano problemi quando si tenta di tooconnect, vedere [le connessioni Desktop remoto di risolvere i problemi](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="059f9-117">If you run into trouble when you try tooconnect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="059f9-118">In questo articolo viene illustrato come diagnosticare e risolvere i problemi più comuni.</span><span class="sxs-lookup"><span data-stu-id="059f9-118">This article walks you through diagnosing and resolving common problems.</span></span>

