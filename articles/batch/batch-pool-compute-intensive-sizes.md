---
title: aaaUse complesse macchine virtuali di Azure batch | Documenti Microsoft
description: Come vantaggio tootake della macchina virtuale che supportano RDMA o abilitata GPU dimensioni nei pool di Azure Batch
services: batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: danlep
ms.openlocfilehash: 6a462a5f2a44ddcec8bf4e5c200d444cac8fafe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-rdma-capable-or-gpu-enabled-instances-in-batch-pools"></a>Usare istanze con supporto per RDMA o abilitate per GPU in pool di Batch

toorun determinati processi Batch, è possibile usare tootake dimensioni delle macchine Virtuali di Azure progettata per il calcolo su larga scala. Ad esempio, toorun multi-istanza [carichi di lavoro MPI](batch-mpi.md), è possibile scegliere A8, A9, o le dimensioni della serie H che dispone di una rete di interfaccia per RDMA Remote Direct Memory Access (). Queste dimensioni connettono di rete InfiniBand tooan per la comunicazione tra i nodi, che consente di velocizzare le applicazioni MPI. Per le applicazioni CUDA è possibile scegliere le dimensioni della serie N, che includono schede GPU (Graphics Processing Unit, unità di elaborazione grafica) NVIDIA Tesla.

Questo articolo fornisce informazioni aggiuntive e toouse esempi le dimensioni di specializzata di Azure nei pool di Batch. Per le specifiche e le informazioni di base, vedere:

* Dimensioni delle VM High Performance Computing ([Linux](../virtual-machines/linux/sizes-hpc.md), [Windows](../virtual-machines/windows/sizes-hpc.md)) 

* Dimensioni delle VM con supporto per GPU ([Linux](../virtual-machines/linux/sizes-gpu.md), [Windows](../virtual-machines/windows/sizes-gpu.md)) 


## <a name="subscription-and-account-limits"></a>Limiti della sottoscrizione e dell'account

* **Le quote** -uno o più quote di Azure possono limitare il numero di hello o un tipo di nodi è possibile aggiungere il pool di Batch tooa. Si è più probabile toobe limitato quando si sceglie il supporto per RDMA, basate su GPU o altre dimensioni delle macchine Virtuali multicore. In base al tipo di hello dell'account Batch che è stato creato, è possibile applicare quote hello account toohello stesso o tooyour sottoscrizione.

    * Se è stato creato l'account Batch in hello **Batch servizio** configurazione, è limitata dalle hello [quota core dedicati per l'account Batch](batch-quota-limit.md#resource-quotas). Per impostazione predefinita, la quota è pari a 20 core. Una quota separata viene applicata troppo[macchine virtuali con priorità bassa](batch-low-pri-vms.md), se vengono usati. 

    * Se è stato creato account hello in hello **sottoscrizione utente** configurazione, la sottoscrizione consente di limitare il numero di hello di core VM per ogni area. Vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md). La sottoscrizione si applica anche una dimensioni di macchina virtuale toocertain internazionali quota, incluse le istanze HPC e GPU. Nella configurazione di sottoscrizione utente hello, nessun quote aggiuntive si applicano account Batch toohello. 

  Potrebbe essere necessario tooincrease uno o più quote quando si utilizza una dimensione di macchina virtuale specializzata in Batch. toorequest un aumento della quota, aprire un [richiesta di supporto clienti online](../azure-supportability/how-to-create-azure-support-request.md) senza alcun costo.

* **Disponibilità area** con utilizzo intensivo di calcolo - macchine virtuali potrebbero non essere disponibili in aree hello in cui si crea l'account Batch. toocheck che una dimensione è disponibile, vedere [i prodotti disponibili per area](https://azure.microsoft.com/regions/services/).


## <a name="dependencies"></a>Dipendenze

funzionalità GPU di dimensioni elevate e Hello RDMA sono supportate solo in determinati sistemi operativi. A seconda del sistema operativo, si potrebbe essere necessario tooinstall o configura aggiuntive per i driver o altro software. Hello le tabelle seguenti riepiloga queste dipendenze. Vedere gli articoli correlati per informazioni dettagliate. Per i pool di Batch tooconfigure opzioni, vedere più avanti in questo articolo.


### <a name="linux-pools---virtual-machine-configuration"></a>Pool Linux - Configurazione della macchina virtuale

| Dimensione | Funzionalità | Sistemi operativi | Requisiti software | Impostazioni pool |
| -------- | -------- | ----- |  -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/linux/sizes-hpc.md#rdma-capable-instances) | RDMA | HPC SUSE Linux Enterprise Server 12 oppure<br/>HPC basato su CentOS<br/>(Azure Marketplace) | Intel MPI 5 | Abilitare la comunicazione tra i nodi, disabilitare l'esecuzione di attività simultanee |
| [Serie NC*](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms) | GPU NVIDIA Tesla K80 | Ubuntu 16.04 LTS.<br/>Red Hat Enterprise Linux 7.3 oppure<br/>CentOS-based 7.3<br/>(Azure Marketplace) | Driver NVIDIA CUDA Toolkit 8.0 | N/D | 
| [Serie NV](../virtual-machines/linux/n-series-driver-setup.md#install-grid-drivers-for-nv-vms) | GPU NVIDIA Tesla M60 | Ubuntu 16.04 LTS<br/>Red Hat Enterprise Linux 7.3<br/>CentOS-based 7.3<br/>(Azure Marketplace) | Driver NVIDIA GRID 4.3 | N/D |

*La connettività RDMA nelle macchine virtuali NC24r è supportata in HPC basato su CentOS 7.3 con Intel MPI.



### <a name="windows-pools---virtual-machine-configuration"></a>Pool Windows - Configurazione della macchina virtuale

| Dimensione | Funzionalità | Sistemi operativi | Requisiti software | Impostazioni pool |
| -------- | ------ | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2 oppure<br/>Windows Server 2012 (Azure Marketplace) | Microsoft MPI 2012 R2 o versioni successive oppure<br/> Intel MPI 5<br/><br/>Estensione di VM Azure HpcVMDrivers | Abilitare la comunicazione tra i nodi, disabilitare l'esecuzione di attività simultanee |
| [Serie NC*](../virtual-machines/windows/n-series-driver-setup.md) | GPU NVIDIA Tesla K80 | Windows Server 2016 oppure <br/>Windows Server 2012 R2 (Azure Marketplace) | Driver NVIDIA Tesla o CUDA Toolkit 8.0| N/D | 
| [Serie NV](../virtual-machines/windows/n-series-driver-setup.md) | GPU NVIDIA Tesla M60 | Windows Server 2016 oppure<br/>Windows Server 2012 R2 (Azure Marketplace) | Driver NVIDIA GRID 4.3 | N/D |

*La connettività RDMA nelle macchine virtuali NC24r è supportata in Windows Server 2012 R2 con estensione HpcVMDrivers e Microsoft MPI o Intel MPI.

### <a name="windows-pools---cloud-services-configuration"></a>Pool Windows - Configurazione servizi cloud

> [!NOTE]
> Le dimensioni della serie di N non sono supportate nel pool di Batch con la configurazione di servizi cloud hello.
>

| Dimensione | Funzionalità | Sistemi operativi | Requisiti software | Impostazioni pool |
| -------- | ------- | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2,<br/>Windows Server 2012 oppure<br/>Windows Server 2008 R2 (famiglia di sistemi operativi guest) | Microsoft MPI 2012 R2 o versioni successive oppure<br/>Intel MPI 5<br/><br/>Estensione di VM Azure HpcVMDrivers | Abilitare la comunicazione tra i nodi,<br/> disabilitare l'esecuzione di attività simultanee |





## <a name="pool-configuration-options"></a>Opzioni di configurazione pool

tooconfigure una dimensione di macchina virtuale specializzata per pool Batch, hello Batch API e strumenti di fornire più software tooinstall necessarie opzioni o i driver, inclusi:

* [Attività di avvio](batch-api-basics.md#start-task) -caricare un pacchetto di installazione come un tooan di file di risorse account di archiviazione di Azure in hello stessa area hello account Batch. Creare automaticamente un file di risorse inizio attività riga di comando tooinstall hello pool hello all'avvio. Per ulteriori informazioni, vedere hello [documentazione dell'API REST](/rest/api/batchservice/add-a-pool-to-an-account#bk_starttask).

  > [!NOTE] 
  > attività di avvio Hello deve essere eseguito con autorizzazioni con privilegi elevati (amministratore) e perché deve attendere l'esito positivo.
  >

* [Pacchetto di applicazione](batch-application-packages.md) : aggiungere un tooyour pacchetto di installazione compresso account Batch e configurare un riferimento al pacchetto nel pool di hello. Questa impostazione consente di caricare e decomprime i pacchetti hello in tutti i nodi nel pool di hello. Se il pacchetto di hello è un programma di installazione, creare un'app installazione hello toosilently riga di comando di inizio attività in tutti i nodi del pool. Facoltativamente, installare il pacchetto di hello quando un'attività è pianificata toorun in un nodo.

* [Immagine personalizzata pool](batch-api-basics.md#pool) : creare Windows personalizzata o l'immagine VM Linux che contiene i driver, software o altre impostazioni necessarie per hello dimensioni della macchina virtuale. Se è stato creato l'account Batch nella configurazione di sottoscrizione utente hello, specificare l'immagine personalizzata di hello per il pool di Batch. (Le immagini personalizzate non sono supportate negli account di configurazione del servizio Batch hello.) Immagini personalizzate sono utilizzabili solo con i pool di configurazione della macchina virtuale hello.

  > [!IMPORTANT]
  > Nei pool di Batch non è attualmente possibile usare un'immagine personalizzata creata con dischi gestiti o con l'archiviazione Premium.
  >



* [Batch ambientali](https://github.com/Azure/batch-shipyard) configura automaticamente in modo trasparente hello GPU e RDMA toowork con carichi di lavoro nei contenitori nel Batch di Azure. Batch Shipyard si basa interamente su file di configurazione. Esistono molti recipe configurazioni di esempio disponibili che consentono di carichi di lavoro GPU e RDMA, ad esempio hello [CNTK GPU Recipe](https://github.com/Azure/batch-shipyard/tree/master/recipes/CNTK-GPU-OpenMPI) che configuri i driver GPU in macchine virtuali serie N e si carica software Microsoft cognitivi Toolkit come un'immagine Docker.


## <a name="example-microsoft-mpi-on-an-a8-vm-pool"></a>Esempio: Microsoft MPI in un pool di VM A8

applicazioni di Windows MPI toorun in un pool di nodi di Azure A8, è necessario tooinstall un'implementazione MPI supportata. Ecco l'esempio passaggi tooinstall [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) in un Windows pool utilizzando un pacchetto di applicazione di Batch.

1. Scaricare hello [pacchetto di installazione](http://go.microsoft.com/FWLink/p/?LinkID=389556) (MSMpiSetup.exe) per la versione più recente di hello di Microsoft MPI.
2. Creare un file zip del pacchetto di hello.
3. Caricare l'account di Batch di hello pacchetto tooyour. Per istruzioni, vedere hello [pacchetti di applicazioni](batch-application-packages.md) informazioni aggiuntive. Specificare un ID applicazione, ad esempio *MSMPI*, e una versione come *8.1*. 
4. Utilizza hello API Batch o il portale di Azure, creare un pool nella configurazione di servizi cloud hello con numero di hello desiderato di nodi e la scala. Hello nella tabella seguente mostra tooset le impostazioni di esempio di MPI in modalità automatica utilizzando un'attività di avvio:

| Impostazione | Valore |
| ---- | ----- | 
| **Tipo di immagine** | Servizi cloud |
| **Famiglia del sistema operativo** | Windows Server 2012 R2 (famiglia del sistema operativo 4) |
| **Dimensioni nodo** | A8 Standard |
| **Comunicazione tra nodi abilitata** | True  |
| **Numero massimo di attività per ogni nodo** | 1 |
| **Riferimenti ai pacchetti dell'applicazione** | MSMPI |
| **Attività di avvio abilitate** | True <br>**Riga di comando** - `"cmd /c %AZ_BATCH_APP_PACKAGE_MSMPI#8.1%\\MSMpiSetup.exe -unattend -force"`<br/>**Identità utente**: utente automatico pool, amministratore<br/>**Attendere il completamento dell'operazione**: True

## <a name="example-nvidia-tesla-drivers-on-nc-vm-pool"></a>Esempio: Driver NVIDIA Tesla in pool di VM NC

applicazioni di CUDA toorun in un pool di nodi di Linux NC, è necessario tooinstall CUDA Toolkit 8.0 nei nodi hello. Hello Toolkit consente di installare i driver GPU Tesla NVIDIA hello necessari. Ecco i passaggi di esempio toodeploy un'immagine personalizzata Ubuntu 16.04 LTS con i driver GPU hello:

1. Distribuire una macchina virtuale NC6 di Azure che esegue Ubuntu 16.04 LTS. Ad esempio, è possibile creare VM hello in hello ci meridionale area centrale. Assicurarsi di creare hello macchina virtuale con archiviazione standard, e *senza* dischi gestiti.
2. Seguire hello passaggi tooconnect toohello VM e [installare i driver CUDA](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms).
3. Eseguire il deprovisioning agente Linux di hello e quindi acquisire l'immagine VM Linux utilizzando i comandi CLI di Azure 1.0 hello. Per la procedura, vedere [Acquisire una VM Linux in esecuzione su Azure](../virtual-machines/linux/capture-image-nodejs.md). Prendere nota dell'immagine di hello URI.
  > [!IMPORTANT]
  > Non usare immagini di hello toocapture comandi CLI di Azure 2.0 per Azure Batch. Attualmente, i comandi CLI 2.0 hello acquisire solo macchine virtuali create utilizzando dischi gestiti.
  >
4. Creare un account di Batch, con la configurazione di sottoscrizione utente hello, in un'area che supporta le macchine virtuali dal controller.
5. Utilizzando le API Batch hello o il portale di Azure, creare un pool utilizzando l'immagine personalizzata hello e con hello numero desiderato di nodi e la scala. Hello nella tabella seguente mostra le impostazioni del pool di esempio per l'immagine di hello:

| Impostazione | Valore |
| ---- | ---- |
| **Tipo di immagine** | Immagine personalizzata |
| **Immagine personalizzata** | URI del modulo hello dell'immagine`https://yourstorageaccountdisks.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd` |
| **SKU agente nodo** | batch.node.ubuntu 16.04 |
| **Dimensioni nodo** | NC6 Standard |



## <a name="next-steps"></a>Passaggi successivi

* i processi MPI toorun in un pool di Batch di Azure, vedere hello [Windows](batch-mpi.md) o [Linux](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/) esempi.

* Per esempi di carichi di lavoro GPU in Batch, vedere hello [ambientali Batch](https://github.com/Azure/batch-shipyard/) ricette.
