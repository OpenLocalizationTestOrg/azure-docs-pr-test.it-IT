---
title: "Esercitazione sui set di disponibilità per macchine virtuali Linux in Azure | Microsoft Docs"
description: "Informazioni sui set di disponibilità per macchine virtuali Linux in Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 63fe3f165864f06228604cac56d06cc061ab25f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-availability-sets"></a>Come usare i set di disponibilità


In questa esercitazione si apprenderà come aumentare la disponibilità e l'affidabilità delle soluzioni delle proprie macchine virtuali in Azure tramite una funzionalità denominata set di disponibilità. I set di disponibilità assicurano che le macchine virtuali distribuite in Azure vengano distribuite tra più cluster hardware isolati. Questa operazione assicura che, se si verifica un errore hardware o software all'interno di Azure, solo un sottoinsieme delle macchine virtuali verrà interessato e la soluzione complessiva rimarrà disponibile e operativa dal punto di vista dei clienti che la usano.

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un set di disponibilità
> * Creare una macchina virtuale in un set di disponibilità
> * Controllare le dimensioni delle macchine virtuali disponibili


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva. Eseguire `az --version` per trovare la versione. Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Informazioni generali sui set di disponibilità

Un set di disponibilità è una funzionalità di raggruppamento logico che è possibile usare in Azure per garantire che le risorse delle macchine virtuali inserite dall'utente siano isolate tra loro quando vengono distribuite all'interno di un data center di Azure. Azure garantisce che le macchine virtuali inserite all'interno di un set di disponibilità vengano eseguite tra più server fisici, rack di calcolo, unità di archiviazione e commutatori di rete. Ciò garantisce che in caso di errore hardware o software in Azure, verrà interessato solo un sottoinsieme delle macchine virtuali e l'applicazione complessiva si manterrà aggiornata e continuerà a essere disponibile per i clienti. L'uso dei set di disponibilità è una funzionalità essenziale da sfruttare quando si desidera creare soluzioni di cloud affidabili.

Si consideri una soluzione tipica basata su macchine virtuali, in cui si dispone di 4 server Web front-end e vengono usate 2 macchine virtuali di back-end che ospitano un database. Con Azure è possibile definire due set di disponibilità prima di distribuire le macchine virtuali: un set di disponibilità per il livello "Web" e un set di disponibilità per il livello "database". Quando si crea una nuova macchina virtuale, è quindi possibile specificare il set di disponibilità come parametro per il comando az vm create. Azure automaticamente garantirà che le macchine virtuali create all'interno del set di disponibilità vengano isolate su più risorse hardware fisiche. Ciò significa che, se l'hardware fisico su cui è in esecuzione una delle macchine virtuali dei server di database o dei server Web presenta un problema, le altre istanze delle macchine virtuali dei server Web e di database rimarranno in esecuzione correttamente perché si trovano su un hardware diverso.

Usare sempre i set di disponibilità quando si vuole distribuire soluzioni affidabili basate su macchine virtuali all'interno di Azure.


## <a name="create-an-availability-set"></a>Creare un set di disponibilità

È possibile creare un set di disponibilità usando il comando [az vm availability-set create](/cli/azure/vm/availability-set#create). In questo esempio sia il numero di domini di aggiornamento che quello di domini di errore viene impostato a *2* per il set di disponibilità denominato *myAvailabilitySet* nel gruppo di risorse *myResourceGroupAvailability*.

Creare un gruppo di risorse.

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

I set di disponibilità consentono di isolare le risorse su "domini di errore" e "domini di aggiornamento". Un **dominio di errore** rappresenta una raccolta isolata di server + rete + risorse di archiviazione. Nell'esempio precedente viene indicato che si desidera distribuire il set di disponibilità su almeno due domini di errore quando vengono distribuite le macchine virtuali. Viene anche indicato che si desidera distribuire il set di disponibilità su due **domini di aggiornamento**.  Due domini di aggiornamento assicurano che, quando Azure esegue gli aggiornamenti software, le risorse delle macchine virtuali siano isolate, impedendo che tutto il software in esecuzione nelle macchine virtuali venga aggiornato contemporaneamente.

## <a name="configure-virtual-network"></a>Configurare la rete virtuale
Prima di distribuire alcune macchine virtuali e testare il servizio di bilanciamento, creare le risorse di rete virtuale di supporto. Per altre informazioni sulle reti virtuali, vedere l'esercitazione [Gestire le reti virtuali di Azure](tutorial-virtual-network.md).

### <a name="create-network-resources"></a>Creare risorse di rete
Creare una rete virtuale con [az network vnet create](/cli/azure/network/vnet#create). L'esempio seguente crea una rete virtuale denominata *myVnet* con una subnet denominata *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
Le schede di interfaccia di rete virtuale vengono create con [az network nic create](/cli/azure/network/nic#create). L'esempio seguente crea tre schede di interfaccia di rete virtuali, Una scheda di interfaccia di rete virtuale per ogni VM creata per l'app nei passaggi successivi. È possibile creare altre schede di interfaccia di rete virtuale e macchine virtuali in qualsiasi momento e aggiungerle al bilanciamento del carico:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a>Creare macchine virtuali in un set di disponibilità

Per garantire la corretta distribuzione delle macchine virtuali in tutto l'hardware, le VM devono essere create all'interno del set di disponibilità. Non è possibile aggiungere una macchina virtuale esistente a un set di disponibilità dopo la sua creazione. 

Quando si crea una macchina virtuale usando il comando [az vm create](/cli/azure/vm#create) si specifica il set di disponibilità usando il parametro `--availability-set` per indicare il nome del set di disponibilità.

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

Sono ora disponibili due macchine virtuali all'interno del set di disponibilità appena creato. Poiché sono nello stesso set di disponibilità, Azure assicura che le macchine virtuali e tutte le relative risorse (inclusi i dischi di dati) siano distribuite su un hardware fisico isolato. Questa distribuzione consente di garantire una disponibilità molto maggiore della soluzione complessiva delle macchine virtuali.

Quando si aggiungono macchine virtuali, potrebbe verificarsi che una determinata dimensione di macchina virtuale non sia più disponibile per l'uso all'interno del set di disponibilità. Questo problema può verificarsi se non è più disponibile una capacità sufficiente per aggiungerla, mentre vengono mantenute le regole di isolamento che il set di disponibilità applica. È possibile verificare quali dimensioni di macchina virtuale sono disponibili per l'uso all'interno di un set di disponibilità esistente tramite il parametro `--availability-set list-sizes`.

## <a name="check-for-available-vm-sizes"></a>Controllare le dimensioni delle macchine virtuali disponibili 

È possibile aggiungere più macchine virtuali al set di disponibilità in un secondo momento, ma è necessario conoscere le dimensioni delle macchine virtuali disponibili nell'hardware. Usare il comando [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) per elencare tutte le dimensioni disponibili nel cluster hardware per il set di disponibilità.

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Creare un set di disponibilità
> * Creare una macchina virtuale in un set di disponibilità
> * Controllare le dimensioni delle macchine virtuali disponibili

Passare all'esercitazione successiva per informazioni sui set di scalabilità di macchine virtuali.

> [!div class="nextstepaction"]
> [Creare un set di scalabilità di macchine virtuali](tutorial-create-vmss.md)

