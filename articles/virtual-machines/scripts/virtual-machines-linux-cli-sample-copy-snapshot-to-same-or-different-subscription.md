---
title: Esempio di Script CLI - snapshot (spostare) copia di un disco gestito toosame o altra sottoscrizione con CLI aaaAzure | Documenti Microsoft
description: Esempio di Script Azure CLI - snapshot (spostare) copia di un disco gestito toosame o altra sottoscrizione con CLI
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
ms.openlocfilehash: f214ab1fc1cb2cb42479d82e455f20a8cc55c83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a>Snapshot di copia di un disco gestito toosame o altra sottoscrizione con CLI

Questo script consente di copiare uno snapshot di un disco gestito toosame o di una sottoscrizione diversa. Utilizzare questo toomove script una sottoscrizione toodifferent snapshot hello snapshot padre hello stessa area.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a>Spiegazione dello script

Questo script Usa la seguente comandi toocreate uno snapshot nella sottoscrizione di destinazione hello utilizzando hello Id dello snapshot di origine hello. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Ottiene tutte le proprietà hello di uno snapshot utilizzando il nome di hello e proprietà gruppo di risorse dello snapshot hello. Proprietà ID è utilizzato toocopy hello snapshot toodifferent sottoscrizione.  |
| [az snapshot create](https://docs.microsoft.com/cli/azure/snapshot#create) | Copie di uno snapshot creando uno snapshot diversa sottoscrizione utilizzando hello Id e nome del hello snapshot padre.  |

## <a name="next-steps"></a>Passaggi successivi

[Creare una macchina virtuale da uno snapshot](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Macchina virtuale aggiuntiva e i dischi gestiti esempi di script CLI sono reperibile in hello [documentazione VM Linux di Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
