---
title: aaaAzure CLI Script di esempio - snapshot di esportazione o copia come account di archiviazione VHD tooa in area diversa | Documenti Microsoft
description: Esempio di Script Azure CLI - snapshot di esportazione o copia come account di archiviazione tooa disco rigido virtuale nella sottoscrizione uguale o diverso
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a>Esportazione o copia snapshot gestito come account di archiviazione tooa disco rigido virtuale in un paese diverso con CLI

Questo script consente di esportare un account di archiviazione snapshot gestito tooa in area diversa. Innanzitutto genera hello URI SAS dello snapshot hello e Usa quindi toocopy è tooa account di archiviazione in paese diverso. Utilizzare il backup di toomaintain script dei dischi gestiti nell'area geografica diversa per il ripristino di emergenza. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a>Spiegazione dello script

Questo script Usa i comandi toogenerate seguente URI SAS per un gestito hello snapshot e copie snapshot tooa account di archiviazione utilizzando URI SAS. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az snapshot grant-access](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | Genera l'errore SAS di sola lettura toocopy utilizzati account di archiviazione tooa file disco rigido virtuale sottostante o scaricarlo tooon locale  |
| [az storage blob copy start](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | Copia un blob in modo asincrono da un tooanother di account di archiviazione |

## <a name="next-steps"></a>Passaggi successivi

[Creare un disco gestito da un disco rigido virtuale](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[Creare una macchina virtuale da un disco gestito](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Macchina virtuale aggiuntiva e i dischi gestiti esempi di script CLI sono reperibile in hello [documentazione VM Linux di Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
