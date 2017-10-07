---
title: Script di PowerShell - esempio di snapshot di esportazione o copia come account di archiviazione VHD tooa in area diversa aaaAzure | Documenti Microsoft
description: Esempio di Script di PowerShell Azure - snapshot di esportazione o copia come account di archiviazione VHD tooa nella stessa area diversa
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
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a>Esportazione o copia snapshot gestito come account di archiviazione tooa disco rigido virtuale in un paese diverso con PowerShell

Questo script consente di esportare un account di archiviazione snapshot gestito tooa in area diversa. Innanzitutto genera hello URI SAS dello snapshot hello e Usa quindi toocopy è tooa account di archiviazione in paese diverso. Utilizzare il backup di toomaintain script dei dischi gestiti nell'area geografica diversa per il ripristino di emergenza.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Spiegazione dello script

Questo script Usa i comandi toogenerate seguente URI SAS per un gestito hello snapshot e copie snapshot tooa account di archiviazione utilizzando URI SAS. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [Grant-AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | Genera l'errore URI SAS per uno snapshot che è usato toocopy è tooa account di archiviazione. |
| [New-AzureStorageContext](/powershell/module/azure.storage/New-AzureStorageContext) | Crea un contesto di account di archiviazione utilizzando la chiave e il nome di account hello. In questo contesto può essere operazioni di lettura/scrittura tooperform utilizzati account di archiviazione hello. |
| [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | Copie hello disco rigido virtuale sottostante di un account di archiviazione snapshot tooa |

## <a name="next-steps"></a>Passaggi successivi

[Creare un disco gestito da un disco rigido virtuale](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[Creare una macchina virtuale da un disco gestito](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).

Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
