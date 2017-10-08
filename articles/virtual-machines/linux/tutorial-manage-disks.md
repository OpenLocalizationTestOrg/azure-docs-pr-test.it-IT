---
title: aaaManage Azure dischi con hello CLI di Azure | Documenti Microsoft
description: 'Esercitazione: gestire i dischi di Azure con hello CLI di Azure'
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
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a>Gestire i dischi di Azure con hello CLI di Azure

Macchine virtuali di Azure utilizzano il sistema operativo macchine virtuali di dischi toostore hello, applicazioni e dati. Quando si crea una macchina virtuale è importante toochoose una dimensione del disco e il carico di lavoro di configurazione appropriato toohello previsto. Questa esercitazione illustra la distribuzione e la gestione dei dischi di VM. Vengono fornite informazioni su:

> [!div class="checklist"]
> * Dischi del sistema operativo e dischi temporanei
> * Dischi dati
> * Dischi Standard e Premium
> * Prestazioni dei dischi
> * Collegamento e preparazione dei dischi dati
> * Ridimensionamento dei dischi
> * Snapshot dei dischi


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="default-azure-disks"></a>Dischi di Azure predefiniti

Quando viene creata una macchina virtuale di Azure, due dischi sono macchina virtuale toohello automaticamente collegato. 

**Disco del sistema operativo** : i dischi del sistema operativo possono essere dimensionati backup too1 terabyte e host hello del sistema operativo di macchine virtuali. disco del sistema operativo Hello viene etichettato *dev/sda* per impostazione predefinita. disco Hello la memorizzazione nella cache di configurazione del disco del sistema operativo hello è ottimizzato per le prestazioni del sistema operativo. A causa di questa configurazione, hello disco del sistema operativo **non** ospitare applicazioni o i dati. Per le applicazioni e i dati, usare un disco dati, descritto in dettaglio più avanti in questo articolo. 

**Disco temporaneo** -i dischi temporanei utilizzano un'unità SSD che si trova in hello stesso host hello VM Azure. I dischi temporanei sono altamente efficienti e possono essere usati per operazioni quali l'elaborazione dei dati temporanei. Tuttavia, se hello macchina virtuale viene spostata tooa nuovo host, i dati archiviati in un disco temporaneo viene rimosso. dimensione di Hello del disco temporaneo hello è determinata dalla hello dimensioni della macchina virtuale. I dischi temporanei vengono etichettati come */dev/sdb* e hanno un punto di montaggio */mnt*.

### <a name="temporary-disk-sizes"></a>Dimensioni del disco temporaneo

| Tipo | Dimensioni macchina virtuale | Dimensioni massime del disco temporaneo (GB) |
|----|----|----|
| [Utilizzo generico](sizes-general.md) | Serie A e D | 800 |
| [Ottimizzate per il calcolo](sizes-compute.md) | Serie F | 800 |
| [Ottimizzate per la memoria](../virtual-machines-windows-sizes-memory.md) | Serie D e G | 6144 |
| [Ottimizzate per l'archiviazione](../virtual-machines-windows-sizes-storage.md) | Serie L | 5630 |
| [GPU](sizes-gpu.md) | Serie N | 1.440 |
| [Prestazioni elevate](sizes-hpc.md) | Serie A e H | 2000 |

## <a name="azure-data-disks"></a>Dischi dati di Azure

È possibile aggiungere altri dischi dati per l'installazione di applicazioni e l'archiviazione dei dati. I dischi dati devono essere usati in qualsiasi situazione in cui si desidera un'archiviazione dei dati durevoli e reattiva. Ciascun disco dati ha una capacità massima di 1 terabyte. dimensioni Hello della macchina virtuale hello determinano il numero di dischi dati può essere collegato tooa macchina virtuale. Per ogni core della macchina virtuale, è possibile collegare due dischi dati. 

### <a name="max-data-disks-per-vm"></a>Numero massimo di dischi di dati per macchina virtuale

| Tipo | Dimensioni macchina virtuale | Numero massimo di dischi di dati per macchina virtuale |
|----|----|----|
| [Utilizzo generico](sizes-general.md) | Serie A e D | 32 |
| [Ottimizzate per il calcolo](sizes-compute.md) | Serie F | 32 |
| [Ottimizzate per la memoria](../virtual-machines-windows-sizes-memory.md) | Serie D e G | 64 |
| [Ottimizzate per l'archiviazione](../virtual-machines-windows-sizes-storage.md) | Serie L | 64 |
| [GPU](sizes-gpu.md) | Serie N | 48 |
| [Prestazioni elevate](sizes-hpc.md) | Serie A e H | 32 |

## <a name="vm-disk-types"></a>Tipi di dischi per la VM

Azure offre due tipi di dischi.

### <a name="standard-disk"></a>Disco standard

Archiviazione Standard è supportata da unità disco rigido e offre un'archiviazione conveniente con buone prestazioni. I dischi standard sono ideali per un carico di lavoro di test e sviluppo conveniente.

### <a name="premium-disk"></a>Disco premium

I dischi premium sono supportati da un disco a bassa latenza e ad alte prestazioni basato su SSD. Ideale per le macchine virtuali che eseguono il carico di lavoro della produzione. L'archiviazione premium supporta le macchine virtuali serie DS, DSv2, GS e FS. I dischi Premium sono disponibili in tre tipi (P10, P20, P30), dimensione hello del disco di hello determina il tipo di disco hello. Quando si seleziona, un valore di hello dimensioni disco viene arrotondato per eccesso tipo successivo toohello. Ad esempio, se la dimensione del disco hello è inferiore a 128 GB, il tipo di disco hello è P10. Se la dimensione del disco hello è tra 129 e 512 GB, hello sono un P20. Un valore superiore a 512 GB, dimensioni hello sono un P30.

### <a name="premium-disk-performance"></a>Prestazioni disco premium

|Tipo di disco di Archiviazione Premium | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Dimensioni del disco (arrotondate) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| Operazioni IOPS al secondo max per disco | 500 | 2.300 | 5.000 |
Velocità effettiva per disco | 100 MB/s | 150 MB/s | 200 MB/s |

Mentre hello sopra tabella identifica massimo di IOPS per disco, un livello di prestazioni superiore può essere ottenuto lo striping di più dischi dati. Ad esempio, una macchina virtuale Standard_GS5 può raggiungere un massimo di 80.000 operazioni di I/O al secondo. Per informazioni dettagliate sul numero massimo di operazioni di I/O al secondo per macchina virtuale, vedere [Dimensioni delle VM Linux](sizes.md).

## <a name="create-and-attach-disks"></a>Creare e collegare dischi

I dischi dati possono essere creati e collegati in fase di creazione macchina virtuale o tooan macchina virtuale esistente.

### <a name="attach-disk-at-vm-creation"></a>Collegare un disco al momento della creazione della macchina virtuale

Creare un gruppo di risorse con hello [gruppo az creare](https://docs.microsoft.com/cli/azure/group#create) comando. 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

Creare una macchina virtuale utilizzando hello [creare vm az]( /cli/azure/vm#create) comando. Hello `--datadisk-sizes-gb` argomento è utilizzato toospecify che un disco aggiuntivo deve essere creato e collegato macchina virtuale toohello. toocreate e collegare più di un disco, utilizzare un elenco delimitato da virgole dei valori di dimensioni del disco. Nell'esempio seguente di hello, viene creata una macchina virtuale con dischi di dati di due, entrambi 128 GB. Poiché le dimensioni dei dischi hello sono 128 GB, entrambi i dischi sono configurati come P10s, che forniscono numero massimo di 500 IOPS per disco.

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a>Collegare tooexisting disco VM

toocreate e collegare una nuovo disco tooan macchina virtuale esistente, utilizzare hello [collegare il disco di macchina virtuale az](/cli/azure/vm/disk#attach) comando. Hello esempio seguente crea un disco premium, 128 gigabyte di spazio e la collega toohello che macchina virtuale creata nell'ultimo passaggio hello.

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a>Preparare i dischi di dati

Dopo aver macchina virtuale toohello collegato, un disco del sistema operativo hello deve toobe configurato toouse hello disco. Hello di esempio seguente viene illustrato come toomanually configurare un disco. È anche possibile automatizzare questo processo puòcon cloud-init, di cui si parlerà nell'[esercitazione successiva](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Configurazione manuale

Creare una connessione SSH con la macchina virtuale hello. Sostituire l'indirizzo IP di esempio hello con indirizzo IP pubblico della macchina virtuale hello hello.

```azurecli-interactive 
ssh 52.174.34.95
```

Partizione disco hello con `fdisk`.

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

Scrittura di una partizione toohello usando hello `mkfs` comando.

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Montare il disco nuovo hello in modo che siano accessibile nel sistema operativo hello.

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

disco Hello è ora possibile accedere tramite hello *datadrive* punto di montaggio, che può essere verificato eseguendo hello `df -h` comando. 

```bash
df -h
```

output di Hello Mostra nuova unità hello montato su */datadrive*.

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

tooensure che hello unità viene rimontato dopo il riavvio, è necessario aggiungerlo toohello */e così via/fstab* file. toodo in tal caso, ottenere hello UUID del disco hello con hello `blkid` utilità.

```bash
sudo -i blkid
```

output di Hello Visualizza hello UUID dell'unità hello `/dev/sdc1` in questo caso.

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

Aggiungere un toohello simile di riga segue toohello */e così via/fstab* file. Si noti anche che le barriere di scrittura possono essere disabilitate mediante *barrier=0*; questa configurazione può migliorare le prestazioni del disco. 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

Ora che hello disco è stato configurato, chiudere una sessione SSH hello.

```bash
exit
```

## <a name="resize-vm-disk"></a>Ridimensionare il disco della macchina virtuale

Dopo la distribuzione di una macchina virtuale, possono essere aumentati le dimensioni disco del sistema operativo hello o eventuali dischi dati collegati. Aumento delle dimensioni di hello di un disco è utile quando è necessario più spazio di archiviazione o un livello superiore di prestazioni (P10, P20, P30). Si noti che non è possibile diminuire le dimensioni dei dischi.

Prima di aumentare le dimensioni del disco, hello Id o nome del disco hello è necessaria. Hello utilizzare [elenco disco az](/cli/azure/vm/disk#list) tooreturn comando tutti i dischi in un gruppo di risorse. Prendere nota del nome del disco hello che si desidera tooresize.

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

Hello VM deve inoltre essere deallocata. Hello utilizzare [az vm deallocare]( /cli/azure/vm#deallocate) comando toostop e deallocare hello macchina virtuale.

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

Hello utilizzare [aggiornamento disco az](/cli/azure/vm/disk#update) disco hello tooresize di comando. In questo esempio ridimensiona un disco denominato *myDataDisk* too1 terabyte.

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

Una volta completata l'operazione di ridimensionamento hello, avviare hello macchina virtuale.

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

Se è stato ridimensionato hello disco del sistema operativo, la partizione hello viene estesa automaticamente. Se è stato ridimensionato un disco dati, tutte le partizioni correnti necessario toobe espansa nel sistema operativo di hello macchine virtuali.

## <a name="snapshot-azure-disks"></a>Snapshot di dischi di Azure

Creare uno snapshot del disco crea un letto solo nel momento copia del disco hello. Gli snapshot macchina virtuale di Azure sono utili per salvare rapidamente lo stato di hello di una macchina virtuale prima di apportare modifiche di configurazione. In caso di hello modifiche alla configurazione hello dimostrare toobe indesiderati, stato delle macchine Virtuali può essere ripristinato mediante snapshot hello. Quando una macchina virtuale dispone di più di un disco, viene eseguito uno snapshot di ogni disco in modo indipendente da hello ad altri utenti. Per l'esecuzione di backup coerenti con l'applicazione, prendere in considerazione l'arresto di hello VM prima di eseguire gli snapshot del disco. In alternativa, utilizzare hello [servizio Azure Backup](/azure/backup/), che consente di tooperform automatizzata backup mentre hello macchina virtuale è in esecuzione.

### <a name="create-snapshot"></a>Creare uno snapshot

Prima di creare uno snapshot di dischi di macchina virtuale, hello Id o nome del disco hello è necessaria. Hello utilizzare [Mostra vm az](https://docs.microsoft.com/en-us/cli/azure/vm#show) id di comando tooreturn hello del disco. In questo esempio, id disco hello è archiviato in una variabile in modo che può essere utilizzato in un passaggio successivo.

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

Dopo aver creato id hello del disco della macchina virtuale hello, hello comando seguente crea uno snapshot del disco hello.

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a>Creare un disco da uno snapshot

Lo snapshot può quindi essere convertito in un disco, che può essere una macchina virtuale di hello toorecreate utilizzato.

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a>Ripristinare una macchina virtuale da uno snapshot

ripristino della macchina virtuale toodemonstrate, macchina virtuale esistente di eliminazione hello. 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

Creare una nuova macchina virtuale dal disco snapshot hello.

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a>Ricollegare un disco dati

Tutti i dischi di dati necessario macchina virtuale di toohello toobe ricollegato.

Prima di tutto trovare nome del disco dati hello utilizzando hello [elenco disco az](https://docs.microsoft.com/cli/azure/disk#list) comando. In questo esempio posizioni hello nome del disco hello in una variabile denominata *datadisk*, che viene utilizzato nel passaggio successivo hello.

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

Hello utilizzare [collegare il disco di macchina virtuale az](https://docs.microsoft.com/cli/azure/vm/disk#attach) disco hello tooattach di comando.

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione sono stati descritti argomenti relativi ai dischi delle VM, ad esempio:

> [!div class="checklist"]
> * Dischi del sistema operativo e dischi temporanei
> * Dischi dati
> * Dischi Standard e Premium
> * Prestazioni dei dischi
> * Collegamento e preparazione dei dischi dati
> * Ridimensionamento dei dischi
> * Snapshot dei dischi

Spostare toohello Avanti toolearn esercitazione sull'automazione di configurazione della macchina virtuale.

> [!div class="nextstepaction"]
> [Automatizzare la configurazione delle macchine virtuali](./tutorial-automate-vm-deployment.md)
