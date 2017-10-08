---
title: una macchina virtuale di Linux in Azure da codice non aaaConvert dischi toomanaged dischi - Azure gestito | Documenti Microsoft
description: Come tooconvert una VM Linux di dischi non gestito toomanaged dischi tramite Azure CLI 2.0 nel modello di distribuzione di gestione risorse di hello
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Convertire una macchina virtuale Linux da dischi toomanaged dischi non gestito

Se si dispone di macchine virtuali Linux esistenti (VM) che usano dischi non gestiti, è possibile convertire hello macchine virtuali gestite toouse dischi tramite hello [dischi gestiti di Azure](../windows/managed-disks-overview.md) servizio. Questo processo converte disco hello del sistema operativo sia eventuali dischi dati collegati.

Questo articolo illustra come tooconvert macchine virtuali tramite hello CLI di Azure. Se è necessario tooinstall o eseguirne l'aggiornamento, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Prima di iniziare

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>Convertire VM a istanza singola
Questa sezione vengono trattati come tooconvert a istanza singola macchine virtuali di Azure da codice non dischi toomanaged dischi. (Se le macchine virtuali si trovano in un set di disponibilità, vedere la sezione successiva di hello). È possibile utilizzare questo toostandard gestiti dischi dischi di macchine virtuali da dischi di toopremium gestiti i dischi premium (SSD) non gestita o da standard (HDD) non gestite di processo tooconvert hello.

1. Deallocare hello VM utilizzando [az vm deallocare](/cli/azure/vm#deallocate). esempio Hello dealloca hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. Convertire i dischi di hello VM toomanaged utilizzando [az vm convertire](/cli/azure/vm#convert). Hello seguente converte processo hello macchina virtuale denominata `myVM`, tra cui disco hello del sistema operativo e qualsiasi disco dati:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. Avviare hello VM dopo i dischi di hello conversione toomanaged utilizzando [inizio vm az](/cli/azure/vm#start). Dopo l'avvio di esempio Hello hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>Convertire VM in un set di disponibilità

Se le macchine virtuali hello che si desidera tooconvert toomanaged dischi sono in un set di disponibilità, è necessario innanzitutto tooconvert hello disponibilità set tooa gestito set di disponibilità.

Tutte le macchine virtuali nel set di disponibilità hello devono essere deallocate prima di convertire il set di disponibilità hello. Piano tooconvert tutti i dischi di macchine virtuali toomanaged dopo la disponibilità di hello impostare autonomamente è stato convertito tooa gestito set di disponibilità. Quindi, avviare tutte le macchine virtuali hello e continuare a funzionare come di consueto.

1. Elencare tutte le macchine virtuali in un set di disponibilità con il comando [az vm availability-set list](/cli/azure/vm/availability-set#list). Hello esempio seguente vengono elencate tutte le macchine virtuali in disponibilità hello set denominata `myAvailabilitySet` nel gruppo di risorse hello denominato `myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. Deallocare tutte le macchine virtuali hello utilizzando [az vm deallocare](/cli/azure/vm#deallocate). esempio Hello dealloca hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. Convertire disponibilità hello impostare utilizzando [convert di set di disponibilità vm az](/cli/azure/vm/availability-set#convert). esempio Hello converte disponibilità hello set denominata `myAvailabilitySet` nel gruppo di risorse hello denominato `myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. Convertire tutti i dischi di toomanaged hello macchine virtuali tramite [az vm convertire](/cli/azure/vm#convert). Hello seguente converte processo hello macchina virtuale denominata `myVM`, tra cui disco hello del sistema operativo e qualsiasi disco dati:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. Avviare tutte le macchine virtuali hello dopo i dischi di hello conversione toomanaged utilizzando [inizio vm az](/cli/azure/vm#start). Dopo l'avvio di esempio Hello hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sulle opzioni di archiviazione, vedere [Panoramica di Azure Managed Disks](../windows/managed-disks-overview.md).
