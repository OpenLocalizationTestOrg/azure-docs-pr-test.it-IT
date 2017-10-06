---
title: aaaAzure CLI Script di esempio - creare un disco gestito da uno snapshot | Documenti Microsoft
description: 'Esempio di script dell''interfaccia della riga di comando di Azure: creare un disco gestito da uno snapshot'
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
ms.openlocfilehash: 549692f5027b3f50b0dd89fe701ebbf0f51d6031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a>Creare un disco gestito da uno snapshot con l'interfaccia della riga di comando

Questo script crea un disco gestito da uno snapshot. Usarlo toorestore una macchina virtuale da snapshot di dischi del sistema operativo e dati. Creare dischi dati e del sistema operativo gestiti dai rispettivi snapshot e quindi creare una nuova macchina virtuale collegando i dischi gestiti. Collegando i dischi dati creati da snapshot, è anche possibile ripristinare i dischi di dati di una macchina virtuale esistente.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza seguenti comandi toocreate un disco gestito da uno snapshot. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Ottiene tutte le proprietà hello di uno snapshot utilizzando il nome di hello e proprietà gruppo di risorse dello snapshot hello. Proprietà ID è disco gestito toocreate utilizzato.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Crea un disco gestito mediante l'ID dello snapshot di uno snapshot gestito |

## <a name="next-steps"></a>Passaggi successivi

[Creare una macchina virtuale collegando un disco gestito come disco del sistema operativo](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Macchina virtuale aggiuntiva e i dischi gestiti esempi di script CLI sono reperibile in hello [documentazione VM Linux di Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
