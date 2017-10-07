---
title: aaaAzure Script di PowerShell di esempio - creare un disco gestito da un file di disco rigido virtuale in un account di archiviazione nella sottoscrizione uguale o diverso | Documenti Microsoft
description: 'Esempio di script di Azure PowerShell: creare un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un''altra'
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
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>Creare un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un'altra con PowerShell

Questo script crea un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un'altra. Utilizzare questo tooimport script un specializzata (non generalizzato/preparata con Sysprep) disco rigido virtuale del sistema operativo toomanaged disco toocreate una macchina virtuale. Inoltre, utilizzarla tooimport un disco di dati dati toomanaged disco rigido virtuale. 

Non creare più dischi gestiti identici da un file VHD in poco tempo. toocreate dischi gestiti da un file vhd, snapshot del blob del file di disco rigido virtuale hello viene creato e quindi i dischi utilizzati toocreate gestito è. È possibile creare snapshot del blob di un solo in un minuto che causa errori di creazione del disco toothrottling scadenza. tooavoid questa limitazione, creare un [snapshot gestito dal file di disco rigido virtuale hello](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) e quindi utilizzare hello gestiti snapshot toocreate più dischi gestiti nel periodo di tempo breve. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza seguenti comandi toocreate un disco gestito da un disco rigido virtuale in una sottoscrizione diversa. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Crea la configurazione del disco usata per la creazione del disco. Tipo di archiviazione, posizione, Id risorsa di hello account di archiviazione in cui è archiviato il padre di hello VHD, VHD URI del VHD principale hello include. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Crea un disco accettando come parametri la configurazione del disco, il nome del disco e il nome del gruppo di risorse. |

## <a name="next-steps"></a>Passaggi successivi

[Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).

Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
