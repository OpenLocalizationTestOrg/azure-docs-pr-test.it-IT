---
title: aaaAzure CLI Script di esempio - creare un disco gestito da un file di disco rigido virtuale in un account di archiviazione in hello stessa sottoscrizione | Documenti Microsoft
description: 'Azure CLI Script di esempio: creare un disco gestito da un file VHD in un account di archiviazione in hello stessa sottoscrizione'
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
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a>Creare un disco gestito da un file di disco rigido virtuale in un account di archiviazione in hello stessa sottoscrizione con CLI

Questo script crea un disco gestito da un file VHD in un account di archiviazione in hello stessa sottoscrizione. Utilizzare questo tooimport script un specializzata (non generalizzato/preparata con Sysprep) disco rigido virtuale del sistema operativo toomanaged disco toocreate una macchina virtuale. Oppure, tooimport un disco di dati dati toomanaged disco rigido virtuale. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza seguenti comandi toocreate un disco gestito da un disco rigido virtuale. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Crea un disco gestito utilizzando l'URI di un disco rigido virtuale in un account di archiviazione in hello stessa sottoscrizione |

## <a name="next-steps"></a>Passaggi successivi

[Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Macchina virtuale aggiuntiva e i dischi gestiti esempi di script CLI sono reperibile in hello [documentazione VM Linux di Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
