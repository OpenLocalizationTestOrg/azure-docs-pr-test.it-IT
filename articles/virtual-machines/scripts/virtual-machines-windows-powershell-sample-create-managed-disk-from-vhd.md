---
title: 'Esempio di script di Azure PowerShell: creare un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un''altra | Microsoft Docs'
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
ms.openlocfilehash: 6d37fb1308ce0b866b42f961ada84d0869f25615
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>Creare un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un'altra con PowerShell

Questo script crea un disco gestito da un file VHD in un account di archiviazione nella stessa sottoscrizione o in un'altra. Usare questo script per importare un disco rigido virtuale specializzato (non generico/preparato con Sysprep) nel disco del sistema operativo gestito per creare una macchina virtuale. In alternativa, usarlo per importare un disco rigido virtuale di dati in un disco dati gestito. 

Non creare più dischi gestiti identici da un file VHD in poco tempo. Per creare dischi gestiti da un file VHD, viene creato lo snapshot del BLOB del file VHD e successivamente viene usato per creare dischi gestiti. È possibile creare un solo snapshot del BLOB in un minuto perché causa errori di creazione del disco dovuti alla limitazione. Per evitare questa limitazione, creare uno [snapshot gestito dal file VHD](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) e quindi usarlo per creare più dischi gestiti in poco tempo. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

Se si sceglie di installare e usare PowerShell in locale, per questa esercitazione è necessario il modulo Azure PowerShell versione 4.0 o successiva. Eseguire `Get-Module -ListAvailable AzureRM` per trovare la versione. Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare Azure PowerShell](/powershell/azure/install-azurerm-ps). Se si esegue PowerShell in locale, è anche necessario eseguire `Login-AzureRmAccount` per creare una connessione con Azure. 

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a>Spiegazione dello script

Questo script usa i comandi seguenti per creare un disco gestito da un file VHD in una sottoscrizione diversa. Ogni comando della tabella include collegamenti alla documentazione specifica del comando.

| Comando | Note |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Crea la configurazione del disco usata per la creazione del disco. Include il tipo di archiviazione, la posizione, l'ID risorsa dell'account di archiviazione in cui è archiviato il VHD di origine e l'URI VHD del VHD padre. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Crea un disco accettando come parametri la configurazione del disco, il nome del disco e il nome del gruppo di risorse. |

## <a name="next-steps"></a>Passaggi successivi

[Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).

Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).