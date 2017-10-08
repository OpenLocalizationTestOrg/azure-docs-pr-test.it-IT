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
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a>Ridistribuire la macchina virtuale di Windows toonew nodo di Azure
Se si hanno stato con difficoltà risoluzione dei problemi di Desktop remoto (RDP) connessione o un'applicazione accedere tooWindows basato su macchina virtuale di Azure (VM), ridistribuire hello VM può essere utile. Quando si ridistribuisce una macchina virtuale, sposta hello VM tooa nuovo nodo all'interno dell'infrastruttura di Azure hello e quindi viene acceso, nuovo, mantenendo tutte le opzioni di configurazione e le risorse associate. In questo articolo illustra come tooredeploy una macchina virtuale utilizzando Azure PowerShell o hello portale di Azure.

> [!NOTE]
> Dopo la ridistribuzione di una macchina virtuale, disco temporaneo hello andrà persa e vengono aggiornati gli indirizzi IP dinamici associati con l'interfaccia di rete virtuale. 


## <a name="using-azure-powershell"></a>Uso di Azure PowerShell
Assicurarsi che si hanno hello versione più recente di PowerShell Azure 1. x installati nel computer. Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

esempio Hello distribuisce hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Passaggi successivi
Se si sono verificati problemi di connessione tooyour VM, è possibile trovare informazioni specifiche su [risoluzione dei problemi delle connessioni RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [dettagliate RDP risoluzione](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Se non si riesce ad accedere a un'applicazione in esecuzione sulla VM, è possibile leggere l'articolo sulle [difficoltà nella risoluzione dei problemi relativi alle applicazioni](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

