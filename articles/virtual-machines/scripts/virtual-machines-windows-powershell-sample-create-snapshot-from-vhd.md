---
title: "aaaAzure Script di PowerShell di esempio - creare uno snapshot da un disco rigido virtuale toocreate più dischi gestiti identici nel breve periodo di tempo | Documenti Microsoft"
description: "Script di Azure PowerShell di esempio: creare uno snapshot da un disco rigido virtuale toocreate più dischi gestiti identici nel breve periodo di tempo"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 5f11793b3669df099b6c31dfdbe906c96ba51786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>Creare uno snapshot da un disco rigido virtuale toocreate più dischi gestiti identici nel breve periodo di tempo con PowerShell

Questo script crea uno snapshot da un file VHD in un account di archiviazione nella stessa sottoscrizione o in una sottoscrizione diversa. Usare questo tooimport script uno snapshot tooa specializzato del disco rigido virtuale (non generalizzato/preparata con Sysprep) e quindi hello snapshot toocreate più dischi gestiti identici nel breve periodo di tempo. Utilizzare inoltre uno snapshot dei dati dei dischi rigidi Virtuali tooa tooimport e quindi utilizzare più dischi gestiti hello snapshot toocreate nel breve periodo di tempo. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza seguenti comandi toocreate un disco gestito da un disco rigido virtuale in una sottoscrizione diversa. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Crea la configurazione del disco usata per la creazione del disco. Include il tipo di archiviazione, percorso, Id risorsa di archiviazione VHD padre hello account di archiviazione di hello e VHD URI del VHD principale hello. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Crea un disco accettando come parametri la configurazione del disco, il nome del disco e il nome del gruppo di risorse. |

## <a name="next-steps"></a>Passaggi successivi

[Creare un disco gestito da uno snapshot](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).

Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
