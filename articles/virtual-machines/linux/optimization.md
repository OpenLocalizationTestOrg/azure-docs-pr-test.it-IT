---
title: aaaOptimize VM Linux su Azure | Documenti Microsoft
description: "Informazioni su alcune toomake suggerimenti di ottimizzazione che è stato configurato per ottenere prestazioni ottimali in Azure VM Linux"
keywords: linux macchina virtuale,macchina virtuale linux,macchina virtuale ubuntu
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 8baa30c8-d40e-41ac-93d0-74e96fe18d4c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 89a9ac022928a2801a9a15e1c172340352745354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-linux-vm-on-azure"></a>Ottimizzare la VM Linux su Azure
Creazione di una macchina virtuale Linux (VM) è facile toodo dalla riga di comando hello o dal portale hello. Questa esercitazione viene illustrato come tooensure impostati, toooptimize le prestazioni sulla piattaforma Microsoft Azure hello. Questo argomento usa una VM di Ubuntu Server, ma è anche possibile creare una macchina virtuale Linux usando le [proprie immagini come modelli](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="prerequisites"></a>Prerequisiti
Questo argomento presuppone che sia disponibile una sottoscrizione di Azure attiva ([registrazione alla versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)) e che sia già stato eseguito il provisioning di una macchina virtuale nella sottoscrizione di Azure. Assicurarsi di aver hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato nel tooyour sottoscrizione di Azure con [accesso az](/cli/azure/#login) prima [creare una macchina virtuale](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-os-disk"></a>Disco del sistema operativo di Azure
Dopo la creazione, alla macchina virtuale Linux in Azure sono associati due dischi. **/dev/sda** è il disco del sistema operativo mentre **/dev/sdb** è il disco temporaneo.  Non utilizzare il disco del sistema operativo principale di hello (**dev/sda**) per qualsiasi valore ad eccezione del sistema operativo hello perché è ottimizzato per l'avvio rapido di macchina virtuale e garantisce prestazioni ottimali per i carichi di lavoro. Si desidera tooattach uno o più dischi tooyour VM tooget persistente e con ottimizzazione per la memoria per i dati. 

## <a name="adding-disks-for-size-and-performance-targets"></a>Aggiunta di dischi per risultati a livello di dimensioni e prestazioni
In base alle dimensioni della macchina virtuale hello, è possibile collegare too16 dischi aggiuntivi in una serie, 32 dischi su una serie di D e 64 dischi in un computer serie G - ogni backup too1 TB nella dimensione. Aggiungere altri dischi in base alle necessità specificate dai requisiti per spazio e IOps. Ogni disco dispone di una destinazione di prestazioni di operazioni 500 IOps per archiviazione Standard e versioni successive too5000 di IOps per disco per l'archiviazione Premium.  Per altre informazioni sui dischi di Archiviazione Premium vedere [Archiviazione Premium: archiviazione a prestazioni elevate per macchine virtuali di Azure](../../storage/common/storage-premium-storage.md)

tooachieve hello più elevato di IOps nei dischi di archiviazione Premium in cui le impostazioni della cache impostate tooeither **ReadOnly** o **Nessuno**, è necessario disabilitare **barriere** mentre file system di montaggio hello in Linux. Non è necessario barriere perché hello scrive tooPremium archiviazione dischi sottoposti a backup sono durevoli per tali impostazioni della cache.

* Se si utilizza **reiserFS**, disabilitare barriere utilizzando l'opzione di montaggio hello `barrier=none` (per l'abilitazione di barriere, utilizzare `barrier=flush`)
* Se si utilizza **ext3/ext4**, disabilitare barriere utilizzando l'opzione di montaggio hello `barrier=0` (per l'abilitazione di barriere, utilizzare `barrier=1`)
* Se si utilizza **XFS**, disabilitare barriere utilizzando l'opzione di montaggio hello `nobarrier` (per l'abilitazione di barriere, utilizzare l'opzione di hello `barrier`)

## <a name="unmanaged-storage-account-considerations"></a>Considerazioni sull'account di archiviazione non gestito
azione predefinita di Hello quando si crea una macchina virtuale con Azure CLI 2.0 hello è toouse Azure gestito dischi.  I dischi vengono gestiti dalla piattaforma Azure hello e non richiedono alcun toostore preparazione o percorso li.  I dischi non gestiti richiedono un account di archiviazione e presentano alcune considerazioni aggiuntive sulle prestazioni.  Per altre informazioni sui dischi gestiti, vedere [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Panoramica di Azure Managed Disks).  Hello sezione seguente illustra le considerazioni sulle prestazioni solo quando si utilizzano dischi non gestiti.  Nuovamente, hello predefinito e soluzione di archiviazione consigliato è dischi toouse gestiti.

Se si crea una macchina virtuale con dischi non gestiti, assicurarsi che si collega dischi dagli account di archiviazione che si trovano in hello stessa area del tooensure VM vicini e ridurre al minimo la latenza di rete.  Ogni account di archiviazione Standard ha capacitò pari ad almeno 20.000 IOps e a dimensioni di 500 TB.  Questo limite determina automaticamente i dischi tooapproximately 40 usato frequentemente inclusi disco hello del sistema operativo e i dischi di dati create. Per gli account di archiviazione Premium non sono previsti limiti massimi per IOps ma è previsto un limite di 32 TB per le dimensioni. 

Quando la gestione di carichi di lavoro di IOps elevata e si è scelto di archiviazione Standard per i dischi, potrebbe essere necessario dischi hello toosplit tra più toomake account archiviazione che non è stato raggiunto hello 20.000 IOps limitare per gli account di archiviazione Standard. La macchina virtuale può contenere una combinazione di dischi da tra diversi account di archiviazione e storage account tipi tooachieve la configurazione ottimale.
 

## <a name="your-vm-temporary-drive"></a>Unità temporanea per la VM
Per impostazione predefinita, quando si crea una macchina virtuale, Azure mette a disposizione un disco del sistema operativo (**/dev/sda**) e un disco temporaneo (**/dev/sdb**).  Tutti gli altri dischi aggiuntivi verranno visualizzati come **/dev/sdc**, **/dev/sdd**, **/dev/sde** e così via. Tutti i dati nei dischi temporanei (**/dev/sdb**) non sono durevoli e possono andare persi se eventi specifici come il ridimensionamento, la ridistribuzione o la manutenzione della macchina virtuale impongono un riavvio.  dimensione Hello e il tipo del disco temporaneo è dimensioni delle macchine Virtuali correlate toohello scelto al momento della distribuzione. Le unità temporanee di hello premium dimensioni macchine virtuali (serie DS, G e DS_V2) hello sono supportate da un'unità SSD locale per aggiuntivi relativi alle prestazioni di backup too48k IOps. 

## <a name="linux-swap-file"></a>File di scambio Linux
Se la macchina virtuale di Azure da un'immagine Ubuntu o CoreOS, è possibile utilizzare CustomData toosend una configurazione cloud toocloud-init. Se è stata [caricata un'immagine Linux personalizzata](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) che usa cloud-init, si configurano anche partizioni di scambio con cloud-init.

In Ubuntu Cloud immagini, è necessario utilizzare partizione di scambio hello tooconfigure cloud init. Per altre informazioni vedere [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

Per le immagini senza supporto per cloud init, immagini di macchina virtuale distribuite da hello Azure Marketplace sono un agente di Linux VM integrato con hello del sistema operativo. Questo agente consente hello VM toointeract con diversi servizi di Azure. Supponendo che è stata distribuita un'immagine standard da hello Azure Marketplace, è necessario toodo hello seguente toocorrectly Configura le impostazioni di file di scambio di Linux:

Individuare e modificare due voci hello **/etc/waagent.conf** file. Viene controllata l'esistenza di hello di un file di swapping dedicato e dimensioni del file di scambio hello. i parametri di Hello desiderata toomodify sono `ResourceDisk.EnableSwap=N` e`ResourceDisk.SwapSizeMB=0` 

Modificare toohello parametri hello seguenti impostazioni:

* ResourceDisk.EnableSwap=Y
* ResourceDisk.SwapSizeMB={size in MB toomeet esigenze} 

Dopo avere apportato hello modificare, è necessario toorestart hello waagent o riavviare il tooreflect VM Linux tali modifiche.  Si conosce sono state implementate modifiche hello e un file di scambio è stato creato quando si utilizza hello `free` comando tooview spazio. esempio Hello è un file di scambio di 512MB creato come risultato della modifica hello **waagent.conf** file:

```bash
azuseruser@myVM:~$ free
            total       used       free     shared    buffers     cached
Mem:       3525156     804168    2720988        408       8428     633192
-/+ buffers/cache:     162548    3362608
Swap:       524284          0     524284
```

## <a name="io-scheduling-algorithm-for-premium-storage"></a>Algoritmo di pianificazione I/O per l'Archiviazione Premium
Con kernel Linux 2.6.18 hello, l'algoritmo di pianificazione di hello predefinito i/o è stato modificato da scadenza tooCFQ (algoritmo Accodamento completamente equo). Per modelli I/O ad accesso casuale, la differenza tra le prestazioni per CFQ e Deadline è minima.  Per i dischi basate su SSD in modello dei / o disco hello è principalmente sequenziale, eseguire il passaggio toohello NOOP o scadenza algoritmo possibile ottenere migliori prestazioni dei / o.

### <a name="view-hello-current-io-scheduler"></a>Visualizzazione hello correnti i/o dell'utilità di pianificazione
Utilizzare hello comando seguente:  

```bash
cat /sys/block/sda/queue/scheduler
```

Vedrai dopo l'output, che indica l'utilità di pianificazione corrente hello.  

```bash
noop [deadline] cfq
```

### <a name="change-hello-current-device-devsda-of-io-scheduling-algorithm"></a>Modificare hello dispositivo (dev/sda) corrente dei / o l'algoritmo di pianificazione
Utilizzare hello seguenti comandi:  

```bash
azureuser@myVM:~$ sudo su -
root@myVM:~# echo "noop" >/sys/block/sda/queue/scheduler
root@myVM:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
root@myVM:~# update-grub
```

> [!NOTE]
> Applicare questa impostazione esclusivamente a **/dev/sda** non serve a niente. Impostare su tutti i dischi di dati in cui i/o sequenziali domina il modello dei / o hello.  

Dovrebbe essere hello seguendo l'output, che indica che **grub.cfg** è stato ricompilato correttamente e l'utilità di pianificazione predefinita hello è stato aggiornato tooNOOP.  

```bash
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.13.0-34-generic
Found initrd image: /boot/initrd.img-3.13.0-34-generic
Found linux image: /boot/vmlinuz-3.13.0-32-generic
Found initrd image: /boot/initrd.img-3.13.0-32-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
done
```

Per hello Redhat famiglia di distribuzione, è necessario solo hello comando seguente:   

```bash
echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local
```

## <a name="using-software-raid-tooachieve-higher-iops"></a>Con RAID Software tooachieve superiore si / Ops
Se i carichi di lavoro richiede delle operazioni IOps che può fornire un singolo disco, è necessario toouse una configurazione RAID software di più dischi. Perché Azure esegue già resilienza disco al livello dell'infrastruttura locale hello, ottenere hello massimo livello di prestazioni da una configurazione di striping RAID-0.  Eseguire il provisioning e creare i dischi in hello ambiente Azure e collegarli tooyour VM Linux prima di partizionamento, la formattazione e montaggio hello unità.  Ulteriori informazioni sulla configurazione di una configurazione RAID software nella VM Linux in azure sono reperibile in hello  **[configurazione RAID Software in Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**  documento.

## <a name="next-steps"></a>Passaggi successivi
Tenere presente, come con tutte le discussioni di ottimizzazione, è necessario tooperform test prima e dopo ogni impatto di modifiche toomeasure hello hello modifica ha.  L'ottimizzazione è un processo graduale che potrà avere risultati diversi in diversi computer nell'ambiente.  Le impostazioni ottimali per una configurazione potrebbero non essere appropriate per altre.

Alcune risorse tooadditional collegamenti utili: 

* [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/common/storage-premium-storage.md)
* [Guida dell'utente dell'agente Linux di Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ottimizzazione delle prestazioni di MySQL in macchine virtuali Linux di Azure](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configurare RAID software in Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

