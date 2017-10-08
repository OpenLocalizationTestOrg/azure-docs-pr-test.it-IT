---
title: Macchine virtuali Linux in Azure aaaRedeploy | Documenti Microsoft
description: Come le macchine virtuali Linux tooredeploy nella connessione SSH toomitigate Azure problemi.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a>Ridistribuire la macchina virtuale di Linux toonew nodo di Azure
Se si trovano ad affrontare problemi di risoluzione dei problemi SSH o applicazione accedere tooa Linux macchina virtuale (VM) in Azure, ridistribuire hello VM può essere utile. Quando si ridistribuisce una macchina virtuale, sposta hello VM tooa nuovo nodo all'interno dell'infrastruttura di Azure hello e quindi accende viene nuovamente. Tutte le opzioni di configurazione e le risorse associate vengono mantenute. In questo articolo illustra come tooredeploy una macchina virtuale tramite l'interfaccia CLI di Azure o hello portale di Azure.

> [!NOTE]
> Dopo la ridistribuzione di una macchina virtuale, disco temporaneo hello andrà persa e vengono aggiornati gli indirizzi IP dinamici associati con l'interfaccia di rete virtuale. 

È possibile ridistribuire una macchina virtuale usando una delle seguenti opzioni hello. È sufficiente toochoose una opzione tooredeploy la macchina virtuale:

- [Interfaccia della riga di comando di Azure 2.0](#azure-cli-20)
- [Interfaccia della riga di comando di Azure 1.0](#azure-cli-10)
- [Portale di Azure](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a>Utilizzare hello Azure CLI 2.0
Hello installazione più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).

Ridistribuire la VM con il comando [az vm redeploy](/cli/azure/vm#redeploy). Hello seguenti distribuzioni di esempio hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a>Utilizzare hello Azure CLI 1.0
Installare hello [più recente di Azure CLI 1.0](../../cli-install-nodejs.md), accedi tooan account Azure e assicurarsi che siano in modalità di gestione risorse (`azure config mode arm`).

Hello seguenti distribuzioni di esempio hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Passaggi successivi
Se si sono verificati problemi di connessione tooyour VM, è possibile trovare informazioni specifiche su [risoluzione dei problemi relativi a connessioni SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [dettagliate SSH risoluzione](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Se non si riesce ad accedere a un'applicazione in esecuzione sulla VM, è possibile leggere l'articolo sulle [difficoltà nella risoluzione dei problemi relativi alle applicazioni](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

