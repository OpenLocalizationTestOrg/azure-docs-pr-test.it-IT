---
title: aaaAzure CLI Script di esempio - copia (spostare) gestiti toosame dischi o una sottoscrizione diversa | Documenti Microsoft
description: Azure CLI Script di esempio - toosame dischi gestito di copia (spostare) o una sottoscrizione diversa
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a>Copia di dischi gestiti toosame o altra sottoscrizione con CLI

Questo script viene copiato un toosame disco gestito o una sottoscrizione diversa, ma in hello stessa area. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a>Spiegazione dello script

Questo script Usa la seguente comandi toocreate un nuovo disco gestito nella sottoscrizione di destinazione hello utilizzando hello Id dell'origine hello gestiti disco. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az disk show](https://docs.microsoft.com/cli/azure/disk#show) | Ottiene tutte le proprietà di hello di un disco gestito utilizzando proprietà di gruppo di risorse e nome hello del disco gestito hello. Proprietà ID è utilizzato toocopy hello gestito disco toodifferent sottoscrizione.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Copia un disco gestito mediante la creazione di un nuovo disco gestito nella sottoscrizione diversi tramite Id e nome padre hello gestiti disco.  |

## <a name="next-steps"></a>Passaggi successivi

[Creare una macchina virtuale da un disco gestito](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Macchina virtuale aggiuntiva e i dischi gestiti esempi di script CLI sono reperibile in hello [documentazione VM Linux di Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
