---
title: Ridistribuire macchine virtuali Windows in Azure | Documentazione Microsoft
description: Come ridistribuire macchine virtuali Windows in Azure per ridurre i problemi di connessione RDP.
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
ms.openlocfilehash: a607d0747f64ee6b224d300113905f54e003aef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="redeploy-windows-virtual-machine-to-new-azure-node"></a><span data-ttu-id="19318-103">Ridistribuire una macchina virtuale Windows in un nuovo nodo di Azure</span><span class="sxs-lookup"><span data-stu-id="19318-103">Redeploy Windows virtual machine to new Azure node</span></span>
<span data-ttu-id="19318-104">Se si stanno riscontrando difficoltà nella risoluzione dei problemi relativi a connessione di desktop remoto (RDP) o accesso delle applicazioni a una macchina virtuale (VM) di Azure basata su Windows, potrebbe essere utile la ridistribuzione.</span><span class="sxs-lookup"><span data-stu-id="19318-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access to Windows-based Azure virtual machine (VM), redeploying the VM may help.</span></span> <span data-ttu-id="19318-105">Quando si ridistribuisce una VM, quest'ultima viene spostata su un nuovo nodo dell'infrastruttura di Azure, quindi viene riattivata conservando tutte le opzioni di configurazione e le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="19318-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="19318-106">In questo articolo viene illustrato come ridistribuire una VM con Azure PowerShell o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="19318-106">This article shows you how to redeploy a VM using Azure PowerShell or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="19318-107">Dopo la ridistribuzione di una VM, il disco temporaneo viene perso e gli indirizzi IP dinamici associati all'interfaccia di rete virtuale vengono aggiornati.</span><span class="sxs-lookup"><span data-stu-id="19318-107">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="19318-108">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="19318-108">Using Azure PowerShell</span></span>
<span data-ttu-id="19318-109">Assicurarsi che sia installata la versione più recente di Azure PowerShell 1.x.</span><span class="sxs-lookup"><span data-stu-id="19318-109">Make sure you have the latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="19318-110">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="19318-110">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="19318-111">L'esempio seguente distribuisce la VM denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="19318-111">The following example deploys the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="19318-112">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="19318-112">Next steps</span></span>
<span data-ttu-id="19318-113">In caso di difficoltà di connessione alla VM, è possibile trovare assistenza specifica sulla [risoluzione dei problemi delle connessioni RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [passaggi dettagliati sulla risoluzione dei problemi RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="19318-113">If you are having issues connecting to your VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="19318-114">Se non si riesce ad accedere a un'applicazione in esecuzione sulla VM, è possibile leggere l'articolo sulle [difficoltà nella risoluzione dei problemi relativi alle applicazioni](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="19318-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

