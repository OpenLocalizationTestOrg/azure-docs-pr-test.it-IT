---
title: aaaAzure CLI Script di esempio - creare due macchine virtuali con un gruppo interno ed esterno | Documenti Microsoft
description: Script dell'interfaccia della riga di comando Azure di esempio - Creare due macchine virtuali con NSG interno ed esterno
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
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a>Proteggere il traffico di rete tra le macchine virtuali

Questo script crea due macchine virtuali e protegge tooboth il traffico in ingresso. Una macchina virtuale è accessibile su internet di hello e non è un gruppo di sicurezza di rete (gruppo) configurato tooallow traffico sulla porta 22 e la porta 80. Hello seconda macchina virtuale non è accessibile su internet hello e ha tooonly un gruppo configurato consentano il traffico dalla macchina virtuale prima di hello. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Consente di creare una rete virtuale e una subnet di Azure. |
| [az network vnet subnet create](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | Consente di creare una subnet. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo. Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.  |
| [az network nsg rule list](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | Restituisce informazioni sulla regola del gruppo di sicurezza di rete. In questo esempio, il nome della regola hello è archiviato in una variabile per l'utilizzo più avanti nello script hello. |
| [az network nsg rule update](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | Consente di aggiornare una regola NSG. In questo esempio, regola di back-end hello è toopass aggiornato al traffico solo dalla subnet front-end di hello. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
