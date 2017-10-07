---
title: aaaHow tooresize una VM Linux con hello Azure CLI 2.0 | Documenti Microsoft
description: Scala verso il basso di una macchina virtuale Linux, modificando o tooscale backup hello come dimensione della macchina virtuale.
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a>Ridimensionare una macchina virtuale Linux con l'interfaccia della riga di comando 2.0

Dopo avere stabilito una macchina virtuale (VM), è possibile applicare la scalabilità hello VM verso l'alto o verso il basso modificando hello [dimensioni delle macchine Virtuali][vm-sizes]. In alcuni casi, è necessario deallocare prima hello VM. Se lo si desidera hello dimensione non è disponibile nel cluster hardware hello che ospita hello VM, è necessario toodeallocate hello macchina virtuale. In questo articolo illustra in dettaglio come tooresize una VM Linux con hello CLI di Azure 2.0. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="resize-a-vm"></a>Ridimensionare una VM
tooresize una macchina virtuale, è necessario hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

1. Ridimensiona elenco hello di vista della macchina virtuale a disponibilità nel cluster hardware hello ospita hello VM con [az vm elenco-vm--opzioni di ridimensionamento](/cli/azure/vm#list-vm-resize-options). Hello esempio seguente vengono elencate le dimensioni delle macchine Virtuali per macchina virtuale denominata hello `myVM` nel gruppo di risorse hello `myResourceGroup` area:
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. Se lo si desidera hello dimensioni della macchina virtuale sono elencata, ridimensionare hello macchina virtuale con [az vm ridimensionare](/cli/azure/vm#resize). Hello seguente esempio ridimensiona hello macchina virtuale denominata `myVM` toohello `Standard_DS3_v2` dimensioni:
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    Hello VM viene riavviato durante questo processo. Dopo il riavvio di hello, il sistema operativo esistente e i dischi di dati vengono rimappati. Qualsiasi elemento sul disco temporaneo hello viene persa.

3. Se lo si desidera hello dimensioni della macchina virtuale non sono elencata, è necessario toofirst deallocare hello macchina virtuale con [az vm deallocare](/cli/azure/vm#deallocate). Questo processo consente hello VM toothen essere ridimensionato tooany dimensioni disponibili hello area supporta e quindi avviato. Hello segue deallocare, ridimensionare e quindi avviare hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > Deallocazione di hello VM rilascia anche indirizzi IP dinamici assegnati toohello macchina virtuale. Hello del sistema operativo e i dischi di dati non sono interessati.

## <a name="next-steps"></a>Passaggi successivi
Per una maggiore scalabilità, eseguire più istanze di VM e la scalabilità orizzontale. Per altre informazioni, vedere [Ridimensionare automaticamente macchine virtuali Linux in un set di scalabilità di macchine virtuali][scale-set]. 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
