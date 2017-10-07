---
title: aaaHow tooresize una VM Linux con hello Azure CLI 1.0 | Documenti Microsoft
description: Scala verso il basso di una macchina virtuale Linux, modificando o tooscale backup hello come dimensione della macchina virtuale.
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a>Ridimensionare una VM Linux con l'interfaccia della riga di comando di Azure 1.0

## <a name="overview"></a>Panoramica

Dopo avere stabilito una macchina virtuale (VM), è possibile applicare la scalabilità hello VM verso l'alto o verso il basso modificando hello [dimensioni delle macchine Virtuali][vm-sizes]. In alcuni casi, è necessario deallocare prima hello VM. Questa situazione può verificarsi se hello nuova dimensione non è disponibile nel cluster hardware hello che ospita hello macchina virtuale.

Questo articolo viene illustrato come tooresize una VM Linux utilizzando hello [CLI di Azure][azure-cli].

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#resize-a-linux-vm) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello


## <a name="resize-a-linux-vm"></a>Ridimensionare una VM di Linux
tooresize una macchina virtuale, eseguire hello alla procedura seguente.

1. Eseguire il comando CLI seguente hello. Questo comando Elenca le dimensioni VM hello che sono disponibili nel cluster hardware hello hello VM ospita.
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. Se lo si desidera hello dimensioni sono elencata, eseguire hello successivo comando tooresize hello macchina virtuale.
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    Hello VM verrà riavviato durante questo processo. Dopo il riavvio di hello, il sistema operativo esistente e i dischi di dati verranno reimpostati. Qualsiasi elemento sul disco temporaneo hello andranno persa.
   
    Hello utilizzare `--enable-boot-diagnostics` opzione Abilita [diagnostica di avvio][boot-diagnostics], toolog qualsiasi toostartup correlati a errori.
3. In caso contrario, se lo si desidera hello dimensioni non sono elencata, eseguire hello seguenti comandi toodeallocate hello VM, ridimensionarlo e quindi riavviare hello macchina virtuale.
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > Deallocazione di hello VM rilascia anche indirizzi IP dinamici assegnati toohello macchina virtuale. Hello del sistema operativo e i dischi di dati non sono interessati.
   > 
   > 

## <a name="next-steps"></a>Passaggi successivi
Per una maggiore scalabilità, eseguire più istanze di VM e la scalabilità orizzontale. Per altre informazioni, vedere [Ridimensionare automaticamente macchine virtuali Linux in un set di scalabilità di macchine virtuali][scale-set]. 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
