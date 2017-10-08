---
title: Esempi di PowerShell di macchina virtuale aaaAzure | Documenti Microsoft
description: Esempi di macchina virtuale di Azure PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a>Esempi di macchina virtuale di Azure PowerShell

Hello nella tabella seguente include collegamenti tooPowerShell script esempi di creare e gestire macchine virtuali di Windows.

| | |
|---|---|
|**Creare macchine virtuali**||
| [Creare una macchina virtuale completamente configurata](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Consente di creare un gruppo di risorse, una macchina virtuale e tutte le risorse correlate.|
| [Creare macchine virtuali a disponibilità elevata](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Consente di creare più macchine virtuali in una configurazione a disponibilità elevata e con bilanciamento del carico.|
| [Creare una macchina virtuale ed eseguire script di configurazione](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea una macchina virtuale e utilizza hello Azure Custom Script estensione tooinstall IIS. |
| [Creare una macchina virtuale ed eseguire la configurazione DSC](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea una macchina virtuale e utilizza hello Azure configurazione DSC (Desired State) estensione tooinstall IIS. |
| [Caricare un disco rigido virtuale e creare VM](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | Uplaods un disco rigido virtuale locale file tooAzure, Crea immagine da VHD hello e quindi crea una macchina virtuale da quell'immagine. |
| [Creare una VM da un disco del sistema operativo gestito](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea una macchina virtuale collegando un disco gestito esistente come disco del sistema operativo. |
| [Creare una VM da uno snapshot](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea una macchina virtuale da uno snapshot prima creazione di un disco gestito da snapshot e quindi collegando nuovo disco gestito hello come disco del sistema operativo. |
|**Gestire l'archiviazione**||
| [Creare dischi gestiti da un disco rigido virtuale nella stessa sottoscrizione o in una sottoscrizione diversa](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea un disco gestito da un disco rigido virtuale specializzato come un disco del sistema operativo o da un disco rigido virtuale di dati come disco dati nella stessa sottoscrizione o in una sottoscrizione diversa.  |
| [Creare un disco gestito da uno snapshot](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea un disco gestito da uno snapshot. |
| [Copiare toosame disco gestito o una sottoscrizione diversa](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Copia gestiti disco toosame o altra sottoscrizione, ma in hello stessa area padre hello gestiti disco. 
| [Esportare uno snapshot del disco rigido virtuale tooa account di archiviazione](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Esporta uno snapshot gestito come account di archiviazione VHD tooa in area diversa. |
| [Creare uno snapshot da un disco rigido virtuale](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea snapshot da un disco rigido virtuale toocreate più identici dischi gestiti da snapshot nel breve periodo di tempo.  |
| [Copiare toosame snapshot o una sottoscrizione diversa](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Copie snapshot toosame o una sottoscrizione diversa mentre in hello stessa area come snapshot padre hello. |
|**Proteggere le macchine virtuali**||
| [Crittografare una macchina virtuale e i dischi dati](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | Crea un'istanza di Azure Key Vault, una chiave di crittografia e un'entità servizio, quindi crittografa una macchina virtuale. |
|**Monitorare le macchine virtuali**||
| [Monitorare una macchina virtuale con Operations Management Suite](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea una macchina virtuale, installa l'agente di Operations Management Suite hello e registra hello macchina virtuale in un'area di lavoro di OMS.  |
| | |

