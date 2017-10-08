---
title: macchine virtuali di Windows aaaRedeploy in Azure | Documenti Microsoft
description: Come macchine virtuali di Windows tooredeploy nella connessione RDP toomitigate Azure problemi.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a><span data-ttu-id="ab5ae-103">Ridistribuire la macchina virtuale di Windows toonew nodo di Azure</span><span class="sxs-lookup"><span data-stu-id="ab5ae-103">Redeploy Windows virtual machine toonew Azure node</span></span>
<span data-ttu-id="ab5ae-104">Se si hanno stato con difficoltà risoluzione dei problemi di Desktop remoto (RDP) connessione o un'applicazione accedere tooWindows basato su macchina virtuale di Azure (VM), ridistribuire hello VM può essere utile.</span><span class="sxs-lookup"><span data-stu-id="ab5ae-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access tooWindows-based Azure virtual machine (VM), redeploying hello VM may help.</span></span> <span data-ttu-id="ab5ae-105">Quando si ridistribuisce una macchina virtuale, sposta hello VM tooa nuovo nodo all'interno dell'infrastruttura di Azure hello e quindi viene acceso, nuovo, mantenendo tutte le opzioni di configurazione e le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="ab5ae-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="ab5ae-106">In questo articolo illustra come tooredeploy una macchina virtuale utilizzando Azure PowerShell o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab5ae-106">This article shows you how tooredeploy a VM using Azure PowerShell or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ab5ae-107">Dopo la ridistribuzione di una macchina virtuale, disco temporaneo hello andrà persa e vengono aggiornati gli indirizzi IP dinamici associati con l'interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ab5ae-107">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="ab5ae-108">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab5ae-108">Using Azure PowerShell</span></span>
<span data-ttu-id="ab5ae-109">Assicurarsi che si hanno hello versione più recente di PowerShell Azure 1. x installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="ab5ae-109">Make sure you have hello latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="ab5ae-110">Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ab5ae-110">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="ab5ae-111">esempio Hello distribuisce hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ab5ae-111">hello following example deploys hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="ab5ae-112">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab5ae-112">Next steps</span></span>
<span data-ttu-id="ab5ae-113">Se si sono verificati problemi di connessione tooyour VM, è possibile trovare informazioni specifiche su [risoluzione dei problemi delle connessioni RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [dettagliate RDP risoluzione](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ab5ae-113">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ab5ae-114">Se non si riesce ad accedere a un'applicazione in esecuzione sulla VM, è possibile leggere l'articolo sulle [difficoltà nella risoluzione dei problemi relativi alle applicazioni](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ab5ae-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

