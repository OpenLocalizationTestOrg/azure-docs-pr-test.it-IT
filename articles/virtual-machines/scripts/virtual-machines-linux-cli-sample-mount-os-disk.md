---
title: Esempio di Script CLI - montaggio disco del sistema operativo aaaAzure | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - montaggio del disco del sistema operativo
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a>Risolvere i problemi del disco del sistema operativo della VM

Questo script Monta disco del sistema operativo di una macchina virtuale non riuscita o problematico hello come dati disco tooa seconda macchina virtuale. Può essere utile quando si esegue la risoluzione dei problemi del disco o il ripristino di dati. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az vm show](https://docs.microsoft.com/cli/azure/vm#show) | Recupera un elenco di macchine virtuali. In questo caso, l'opzione query hello è disco del sistema operativo utilizzato tooreturn hello macchina virtuale. Questo valore viene quindi aggiunto tooa. nome della variabile 'uri'. |
| [az vm delete](https://docs.microsoft.com/cli/azure/vm#delete) | Consente di eliminare una macchina virtuale. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Consente di creare una macchina virtuale.  |
| [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) | Collega una macchina virtuale di tooa disco. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Restituisce hello gli indirizzi IP di una macchina virtuale. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
