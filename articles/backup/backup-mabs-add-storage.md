---
title: aaaUse moderna archiviazione dei Backup con il Server di Backup di Azure v2 | Documenti Microsoft
description: "Informazioni sulle nuove funzionalità di hello Azure Backup Server v2. Questo articolo viene descritto come tooupgrade l'installazione del Server di Backup."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a>Aggiungere archiviazione tooAzure v2 Server Backup

Il server di Backup di Azure v2 include Modern Backup Storage di System Center 2016 Data Protection Manager. Modern Backup Storage garantisce un risparmio del 50% sullo spazio di archiviazione, backup tre volte più veloci e un'archiviazione più efficiente. Offre anche l'archiviazione con riconoscimento del carico di lavoro. 

> [!NOTE]
> toouse moderna archiviazione dei Backup, è necessario eseguire Backup Server v2 in Windows Server 2016. Se si esegue il server di Backup v2 in una versione precedente di Windows Server, il server di Backup di Azure non può avvalersi di Modern Backup Storage. Invece, i carichi di lavoro vengono protetti come avviene nel server di Backup v1. Per ulteriori informazioni, vedere versione del Server di Backup hello [matrice protezione](backup-mabs-protection-matrix.md).

## <a name="volumes-in-backup-server-v2"></a>Volumi nel server di Backup v2

Il server di Backup v2 accetta volumi di archiviazione. Quando si aggiunge un volume, Backup Server formatta hello volume tooResilient File System (ReFS), che richiede l'archiviazione dei Backup moderne. tooadd un volume, tooexpand e in un secondo momento, se necessario, si consiglia di utilizzare questo flusso di lavoro:

1.  Configurare il server di Backup v2 in una macchina virtuale.
2.  Creare un volume su un disco virtuale in un pool di archiviazione:
    1.  Aggiungere un pool di archiviazione su disco tooa e creare un disco virtuale con layout semplice.
    2.  Aggiungere ulteriori dischi ed estendere disco virtuale hello.
    3.  Creare volumi nel disco virtuale hello.
3.  Aggiungere hello volumi tooBackup Server.
4.  Configurare l'archiviazione con riconoscimento del carico di lavoro.

## <a name="create-a-volume-for-modern-backup-storage"></a>Creare un volume per Modern Backup Storage

L'utilizzo del server di Backup v2 con volumi come archiviazione su disco consente di mantenere il controllo sull'archiviazione. Un volume può essere un singolo disco. Tuttavia, se si desidera archiviazione tooextend in hello future, creare un volume da un disco creato tramite spazi di archiviazione. Questo può aiutare se si desidera volume hello tooexpand per archiviazione di backup. In questa sezione sono presentate le procedure consigliate per la creazione di un volume con questa configurazione.

1. In Server Manager selezionare **Servizi file e archiviazione** > **Volumi** > **Pool di archiviazione**. In **DISCHI FISICI**, selezionare **Nuovo pool di archiviazione**. 

    ![Creare un nuovo pool di archiviazione](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. In hello **attività** casella di riepilogo a discesa, selezionare **nuovo disco virtuale**.

    ![Aggiungere un disco virtuale](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. Selezionare il pool di archiviazione hello e quindi selezionare **Aggiungi disco fisico**.

    ![Aggiungere un disco fisico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. Disco fisico hello, scegliere quindi **estendere disco virtuale**.

    ![Estendere disco virtuale hello](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. Selezionare i dischi virtuali hello, quindi **nuovo Volume**.

    ![Creare un nuovo volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. In hello **selezionare server hello e il disco** finestra di dialogo, selezionare hello server e il disco di nuovo di hello. Quindi selezionare **Avanti**.

    ![Selezionare disco e il server hello](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a>Aggiungere spazio su disco Server tooBackup di volumi

tooadd tooBackup un volume Server, in hello **Management** riquadro Ripeti analisi archiviazione hello e quindi selezionare **Aggiungi**. Viene visualizzato un elenco di tutti i hello volumi disponibili toobe aggiunto per l'archiviazione di Backup del Server. Dopo che i volumi disponibili vengono aggiunte toohello elenco dei volumi selezionati, è possibile assegnare loro toohelp un nome descrittivo gestirli. tooformat tooReFS questi volumi, in modo da Server di Backup può utilizzare i vantaggi di hello di archiviazione dei Backup moderna, selezionare **OK**.

![Aggiungere i volumi disponibili](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>Configurare l'archiviazione con riconoscimento del carico di lavoro

Con l'archiviazione in grado di riconoscere il carico di lavoro, è possibile selezionare volumi hello che archiviano preferibilmente determinati tipi di carichi di lavoro. Ad esempio, è possibile impostare costosa volumi che supportano un numero elevato di operazioni di input/output al secondo (IOPS) toostore soli hello carichi di lavoro che richiedono frequenti backup volumi elevati. Un esempio è SQL Server con i log delle transazioni. Altri carichi di lavoro che vengono sottoposti a backup meno frequentemente, ad esempio le macchine virtuali, eseguirne il backup toolow costo volumi.

### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

È possibile impostare l'archiviazione del carico di lavoro tramite il cmdlet PowerShell hello aggiornamento DPMDiskStorage, che aggiorna le proprietà di hello di un volume nel pool di archiviazione hello in un server di Data Protection Manager.

Sintassi:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
Hello seguente schermata mostra cmdlet Update-DPMDiskStorage hello nella finestra di PowerShell hello.

![comando Update-DPMDiskStorage nella finestra di PowerShell hello Hello](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

Hello effettuate usando PowerShell vengono riflesse nell'hello Console di amministrazione di Server di Backup.

![I dischi e volumi nella Console di amministrazione di hello](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>Passaggi successivi
Dopo aver installato il Server di Backup, informazioni su come tooprepare del server, o iniziare a proteggere un carico di lavoro.

- [Preparare i carichi di lavoro del server di backup](backup-azure-microsoft-azure-backup.md)
- [Utilizzare tooback Server di Backup di un server VMware](backup-azure-backup-server-vmware.md)
- [Usare Backup Server tooback verticale di SQL Server](backup-azure-sql-mabs.md)

