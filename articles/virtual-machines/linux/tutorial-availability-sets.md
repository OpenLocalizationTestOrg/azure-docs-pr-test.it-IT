---
title: aaaAvailability imposta esercitazione per le macchine virtuali Linux in Azure | Documenti Microsoft
description: "Informazioni sui set di disponibilità hello per le macchine virtuali Linux in Azure."
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
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Il set di disponibilità di toouse


In questa esercitazione si apprenderà come tooincrease hello disponibilità e affidabilità delle soluzioni di macchina virtuale in Azure mediante una funzionalità denominata set di disponibilità. Set di disponibilità garantiscono che hello macchine virtuali di distribuire in Azure vengono distribuite tra più cluster hardware isolato. Questa operazione assicura che se si verifica un errore hardware o software all'interno di Azure, solo un sottoinsieme di macchine virtuali che verrà interessato e che la soluzione complessiva rimangono disponibili e operative dal punto di vista hello dei clienti di utilizzarlo.

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un set di disponibilità
> * Creare una macchina virtuale in un set di disponibilità
> * Controllare le dimensioni delle macchine virtuali disponibili


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Informazioni generali sui set di disponibilità

Un Set di disponibilità è una raggruppamento logico di funzionalità che è possibile utilizzare in Azure tooensure che le risorse VM hello posizionate all'interno di essa sono isolate tra loro quando vengono distribuiti all'interno di un Data Center Azure. Azure garantisce che le macchine virtuali posizionate all'interno di un Set di disponibilità esegue tra più server fisici hello, calcolo rack, unità di archiviazione e commutatori di rete. Ciò garantisce che nell'evento hello di un errore hardware o software di Azure, solo un subset delle macchine virtuali sarà interessato e in generale l'applicazione rimanere e continuare toobe tooyour disponibili clienti. Utilizzo di set di disponibilità è un tooleverage funzionalità essenziali quando si desidera che le soluzioni di cloud affidabile toobuild.

Si consideri una soluzione tipica basata su macchine virtuali, in cui si dispone di 4 server Web front-end e vengono usate 2 macchine virtuali di back-end che ospitano un database. Con Azure, si toodefine due set di disponibilità prima di distribuire le macchine virtuali: set di disponibilità di uno per il livello di "web" hello e un set di disponibilità per il livello di "database" hello. Quando si crea una nuova macchina virtuale, è possibile specificare la disponibilità di hello imposta come comando di creazione di una macchina virtuale az toohello di parametro e di Azure automaticamente verificare che le macchine virtuali create all'interno di hello disponibile hello set vengono isolati in più risorse hardware fisiche. Ciò significa che se si è verificato un problema hardware fisico hello in esecuzione in uno dei Server Web o macchine virtuali del Server di Database, si conosce tale hello altre istanze del Server Web e macchine virtuali del Database rimarrà in esecuzione correttamente perché sono in un hardware diverso.

Quando si desidera toodeploy affidabile VM soluzioni basate su all'interno di Azure, è necessario utilizzare sempre i set di disponibilità.


## <a name="create-an-availability-set"></a>Creare un set di disponibilità

È possibile creare un set di disponibilità usando il comando [az vm availability-set create](/cli/azure/vm/availability-set#create). In questo esempio, è impostato sia il numero di domini di aggiornamento e di errore hello *2* per la disponibilità di hello set denominata *myAvailabilitySet* in hello *myResourceGroupAvailability*gruppo di risorse.

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

Set di disponibilità consentono tooisolate risorse tra "domini di errore di" e "domini di aggiornamento". Un **dominio di errore** rappresenta una raccolta isolata di server + rete + risorse di archiviazione. Hello sopra riportato, si indica che la disponibilità impostare toobe distribuiti in almeno due domini di errore quando vengono distribuite i macchine virtuali. Viene anche indicato che si desidera distribuire il set di disponibilità su due **domini di aggiornamento**.  Assicurarsi di due domini di aggiornamento quando Azure esegue gli aggiornamenti software sono isolate, impedendo a tutti i software hello in esecuzione sotto la macchina virtuale da cui viene aggiornata in hello le risorse della macchina virtuale contemporaneamente.

## <a name="configure-virtual-network"></a>Configurare la rete virtuale
Prima di distribuire alcune macchine virtuali e possibile eseguire il servizio di bilanciamento del test, creare hello che supporta le risorse di rete virtuale. Per ulteriori informazioni sulle reti virtuali, vedere hello [gestire reti virtuali di Azure](tutorial-virtual-network.md) esercitazione.

### <a name="create-network-resources"></a>Creare risorse di rete
Creare una rete virtuale con [az network vnet create](/cli/azure/network/vnet#create). esempio Hello crea una rete virtuale denominata *myVnet* con una subnet denominata *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
Le schede di interfaccia di rete virtuale vengono create con [az network nic create](/cli/azure/network/nic#create). Hello esempio crea tre schede di rete virtuale. (Una scheda di rete virtuale per ogni macchina virtuale viene creato per l'app in hello seguendo i passaggi). È possibile creare macchine virtuali e schede di rete virtuali aggiuntive in qualsiasi momento e aggiungerli toohello servizio di bilanciamento del carico:

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

Macchine virtuali devono essere create all'interno di hello toomake set di disponibilità che vengono distribuite correttamente su hardware hello. È possibile aggiungere un gruppo di disponibilità tooan VM impostato dopo la sua creazione. 

Quando si crea una macchina virtuale mediante [creare vm az](/cli/azure/vm#create) specificare hello set di disponibilità usando hello `--availability-set` nome del parametro toospecify hello hello del set di disponibilità.

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

Sono ora disponibili due macchine virtuali all'interno del set di disponibilità appena creato. Poiché sono presenti in hello stesso set di disponibilità, Azure garantisce che le macchine virtuali hello e tutte le risorse (inclusi i dischi di dati) vengono distribuite tra isolato hardware fisico. Questa distribuzione consente di garantire una disponibilità molto maggiore della soluzione complessiva delle macchine virtuali.

Una cosa che potrebbero verificarsi quando si aggiungono macchine virtuali è che una determinata dimensione di macchina virtuale non è più disponibile toouse all'interno del set di disponibilità. Questo problema può verificarsi se non è più sufficiente tooadd capacità mantenendo i set di disponibilità di hello isolamento regole hello applica. È possibile controllare le dimensioni delle macchine Virtuali sono disponibili toouse all'interno di un gruppo di disponibilità impostati utilizzando hello toosee `--availability-set list-sizes` parametro.

## <a name="check-for-available-vm-sizes"></a>Controllare le dimensioni delle macchine virtuali disponibili 

È possibile aggiungere ulteriori disponibilità toohello di macchine virtuali in un momento successivo, ma è necessario tooknow le dimensioni delle macchine Virtuali sono disponibili su hardware hello. Utilizzare [az set di disponibilità elenco-dimensioni delle macchine virtuali](/cli/azure/availability-set#list-sizes) toolist tutte le dimensioni disponibili hello hardware hello del cluster per il set di disponibilità hello.

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

Spostare toohello toolearn esercitazione successiva sui set di scalabilità di macchine virtuali.

> [!div class="nextstepaction"]
> [Creare un set di scalabilità di macchine virtuali](tutorial-create-vmss.md)

