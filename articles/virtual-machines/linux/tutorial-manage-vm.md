---
title: aaaCreate e gestire le macchine virtuali Linux con hello CLI di Azure | Documenti Microsoft
description: 'Esercitazione: creare e gestire le macchine virtuali Linux con hello CLI di Azure'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a>Creare e gestire le macchine virtuali Linux con hello CLI di Azure

Le macchine virtuali di Azure offrono un ambiente di elaborazione completamente configurabile e flessibile. Questa esercitazione illustra gli elementi di base della distribuzione di una macchina virtuale di Azure, ad esempio la selezione delle dimensioni di una VM, la selezione dell'immagine di una VM e la distribuzione di una VM. Si apprenderà come:

> [!div class="checklist"]
> * Creare e connettersi tooa VM
> * Selezionare e usare le immagini di una macchina virtuale
> * Visualizzare e usare macchine virtuali di dimensioni specifiche
> * Ridimensionare una VM
> * Visualizzare e comprendere lo stato di una macchina virtuale


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](https://docs.microsoft.com/cli/azure/group#create) comando. 

Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. Il gruppo di risorse deve essere creato prima della macchina virtuale. In questo esempio, un gruppo di risorse denominato *myResourceGroupVM* viene creato in hello *eastus* area. 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

gruppo di risorse Hello viene specificato durante la creazione o modifica di una macchina virtuale, che può essere visualizzata in questa esercitazione.

## <a name="create-virtual-machine"></a>Crea macchina virtuale

Creare una macchina virtuale con hello [creare vm az](https://docs.microsoft.com/cli/azure/vm#create) comando. 

Per la creazione di una macchina virtuale sono disponibili diverse opzioni, ad esempio l'immagine del sistema operativo, il ridimensionamento del disco e le credenziali amministrative. In questo esempio viene creata una macchina virtuale denominata *myVM* che esegue Ubuntu Server. 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

Una volta hello che macchina virtuale è stata creata, hello CLI di Azure genera informazioni hello macchina virtuale. Prendere nota di hello `publicIpAddress`, questo indirizzo può essere una macchina virtuale di tooaccess utilizzati hello... 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a>Connettersi tooVM

È ora possibile connettersi toohello VM tramite SSH. Sostituire l'indirizzo IP di esempio hello con hello `publicIpAddress` annotate nel passaggio precedente hello.

```bash
ssh 52.174.34.95
```

Una volta terminato con hello VM, chiudere una sessione SSH hello. 

```bash
exit
```

## <a name="understand-vm-images"></a>Informazioni sulle immagini delle VM

Hello Azure marketplace include molte immagini che possono essere macchine virtuali toocreate utilizzato. Nei passaggi precedenti hello, una macchina virtuale è stata creata usando un'immagine Ubuntu. In questo passaggio, hello che CLI di Azure è marketplace hello toosearch utilizzato per un'immagine CentOS, che viene quindi utilizzato toodeploy una seconda macchina virtuale.  

un elenco di hello toosee utilizzato più di frequente immagini, utilizzare hello [elenco di immagini di macchina virtuale az](/cli/azure/vm/image#list) comando.

```azurecli-interactive 
az vm image list --output table
```

output del comando Hello restituisce le immagini di macchina virtuale più diffusi hello in Azure.

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

Un elenco completo può essere visualizzato mediante l'aggiunta di hello `--all` argomento. è inoltre possibile filtrare l'elenco di immagini Hello da `--publisher` o `–-offer`. In questo esempio hello viene filtrato per tutte le immagini con un'offerta corrispondente *CentOS*. 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

Output parziale:

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

toodeploy una macchina virtuale usando un'immagine specifica, prendere nota del valore di hello in hello *Urn* colonna. Quando si specifica l'immagine di hello, numero di versione di hello immagine può essere sostituito con "più recente", che consente di selezionare più recente della distribuzione hello hello. In questo esempio hello `--image` argomento è una versione più recente di hello toospecify utilizzati di un'immagine CentOS 6.5.  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a>Informazioni sulle dimensioni delle VM

Una dimensione di macchina virtuale determina la quantità hello delle risorse di calcolo, ad esempio memoria, CPU e GPU che vengono apportate una macchina virtuale disponibile toohello. Macchine virtuali devono toobe una dimensione appropriata per il carico di lavoro hello previsto. Se aumenta il carico di lavoro, è possibile ridimensionare una macchina virtuale esistente.

### <a name="vm-sizes"></a>Dimensioni delle VM

Hello nella tabella seguente classifica le dimensioni in casi di utilizzo.  

| Tipo                     | Dimensioni           |    Descrizione       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Utilizzo generico](sizes-general.md)         |Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7| Rapporto equilibrato tra CPU e memoria. La soluzione ideale per sviluppo / test e le soluzioni di applicazioni e dati toomedium di piccole dimensioni.  |
| [Ottimizzate per il calcolo](sizes-compute.md)   | Fs, F             | Rapporto elevato tra CPU e memoria. Soluzione idonea per applicazioni con livelli medi di traffico, dispositivi di rete e processi batch.        |
| [Ottimizzate per la memoria](../virtual-machines-windows-sizes-memory.md)    | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Rapporto elevato tra memoria e core. Ideale per i database relazionali, cache toolarge medium e analitica in memoria.                 |
| [Ottimizzate per l'archiviazione](../virtual-machines-windows-sizes-storage.md)      | Ls                | I/O e velocità effettiva del disco elevati. Ideale per Big Data, database SQL e NoSQL.                                                         |
| [GPU](sizes-gpu.md)          | NV, NC            | VM specializzate ottimizzate per livelli intensivi di rendering della grafica e modifica di video.       |
| [Prestazioni elevate](sizes-hpc.md) | H, A8-11          | Le VM con CPU più potenti, con interfacce di rete ad alta velocità effettiva opzionali (RDMA). 


### <a name="find-available-vm-sizes"></a>Trovare le dimensioni delle macchine virtuali disponibili

toosee un elenco di macchine Virtuali di dimensioni disponibili in una determinata area, usare hello [elenco-dimensioni delle macchine virtuali az](/cli/azure/vm#list-sizes) comando. 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

Output parziale:

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a>Creare una macchina virtuale con dimensioni specifiche

Nell'esempio di creazione macchina virtuale precedente hello, una dimensione non è stato specificato, in base alla quale le dimensioni predefinite. È possibile selezionare una dimensione di macchina virtuale al momento della creazione utilizzando [creare vm az](/cli/azure/vm#create) e hello `--size` argomento. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a>Ridimensionare una VM

Dopo la distribuzione di una macchina virtuale, può essere ridimensionato tooincrease o ridurre l'allocazione delle risorse.

Prima di ridimensionamento di una macchina virtuale, controllare se hello dimensione desiderata è disponibile nel cluster di Azure corrente hello. Hello [az vm elenco-vm--opzioni di ridimensionamento](/cli/azure/vm#list-vm-resize-options) restituisce hello elenco delle dimensioni di comando. 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
Se lo si desidera hello dimensione è disponibile, hello VM può essere ridimensionata da uno stato acceso, ma che è stato riavviato durante l'operazione di hello. Hello utilizzare [az vm ridimensionare]( /cli/azure/vm#resize) comando tooperform hello ridimensionamento.

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

Se hello dimensioni desiderate non è in cluster corrente hello, hello VM esigenze toobe deallocato prima operazione di ridimensionamento hello può verificarsi. Hello utilizzare [az vm deallocare]( /cli/azure/vm#deallocate) comando toostop e deallocare hello macchina virtuale. Si noti che quando hello VM viene acceso nuovamente, potrebbero venire rimosso tutti i dati su disco temporaneo hello. indirizzo IP pubblico Hello viene modificato anche se non viene utilizzato un indirizzo IP statico. 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

Una volta deallocato, può verificarsi hello ridimensionamento. 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

Dopo hello ridimensionare, hello VM può essere avviata.

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a>Stati di alimentazione di una macchina virtuale

Una macchina virtuale di Azure può avere uno dei diversi stati di alimentazione. Questo stato rappresenta lo stato corrente di hello di hello VM dal punto di vista hello di hello hypervisor. 

### <a name="power-states"></a>Stati di alimentazione

| Stato di alimentazione | Descrizione
|----|----|
| Avvio in corso | Indica la macchina virtuale hello viene avviata. |
| In esecuzione | Indica che la macchina virtuale hello è in esecuzione. |
| Arresto in corso | Indica che la macchina virtuale hello è stata arrestata. | 
| Arrestato | Indica che la macchina virtuale hello è stata arrestata. Macchine virtuali in stato arrestato hello continuerà a essere addebitati.  |
| Deallocazione | Indica che la macchina virtuale hello è in corso deallocazione. |
| Deallocato | Indica che la macchina virtuale hello è rimosso dall'hypervisor hello ma ancora disponibili nel piano di controllo hello. Macchine virtuali in stato deallocato hello non essere addebitati. |
| - | Indica che lo stato di alimentazione hello della macchina virtuale hello è sconosciuto. |

### <a name="find-power-state"></a>Trovare lo stato di alimentazione

stato di hello tooretrieve di una determinata macchina virtuale, utilizzare hello [az vm ottenere Vista istanza](/cli/azure/vm#get-instance-view) comando. Essere toospecify che un nome valido per una macchina virtuale e un gruppo di risorse. 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

Output:

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a>Attività di gestione

Durante il ciclo di vita hello di una macchina virtuale, è opportuno toorun attività di gestione, ad esempio avvio, arresto o l'eliminazione di una macchina virtuale. Inoltre, è consigliabile toocreate script tooautomate attività ripetitive o complesse. Utilizza hello CLI di Azure, molte attività comuni di gestione può essere eseguita dalla riga di comando hello o negli script. 

### <a name="get-ip-address"></a>Ottenere l'indirizzo IP

Questo comando restituisce gli indirizzi IP pubblici e privati di hello di una macchina virtuale.  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a>Arrestare la macchina virtuale

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a>Avviare la macchina virtuale

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a>Eliminare un gruppo di risorse

Se si elimina un gruppo di risorse, vengono eliminate anche tutte le risorse in esso contenute.

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione sono illustrate la creazione e la gestione di VM di base, ad esempio:

> [!div class="checklist"]
> * Creare e connettersi tooa VM
> * Selezionare e usare le immagini di una macchina virtuale
> * Visualizzare e usare macchine virtuali di dimensioni specifiche
> * Ridimensionare una VM
> * Visualizzare e comprendere lo stato di una macchina virtuale

Spostare toohello toolearn esercitazione successiva su dischi di macchina virtuale.  

> [!div class="nextstepaction"]
> [Creare e gestire dischi di macchine virtuali](./tutorial-manage-disks.md)
