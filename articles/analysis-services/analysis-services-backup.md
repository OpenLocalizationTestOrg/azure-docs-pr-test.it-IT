---
title: database di Analysis Services aaaAzure di backup e ripristino | Documenti Microsoft
description: Viene descritto come toobackup e ripristino di un Azure Analysis Services database.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a>Backup e ripristino

Il backup dei database modello tabulare in Analysis Services di Azure è molto hello uguale a quello locale di Analysis Services. la differenza principale Hello è dove memorizzare i file di backup. I file di backup devono essere salvati tooa contenitore in un [account di archiviazione Azure](../storage/common/storage-create-storage-account.md). È possibile usare un account di archiviazione e un contenitore già esistenti, o è possibile crearne di nuovi durante la configurazione delle impostazioni di archiviazione per il server.

> [!NOTE]
> La creazione di un account di archiviazione può dare luogo a un nuovo servizio fatturabile. vedere, più toolearn [prezzi di archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).
> 
> 

I backup vengono salvati con estensione abf. Per i modelli tabulari in memoria, vengono archiviati sia i dati del modello che i metadati. Per i modelli tabulari DirectQuery, vengono archiviati solo i metadati del modello. I backup possono essere compressi e crittografati, a seconda delle opzioni di hello che prescelto. 



## <a name="configure-storage-settings"></a>Configurare le impostazioni di archiviazione
Prima del backup, è necessario tooconfigure le impostazioni di archiviazione per il server.


### <a name="tooconfigure-storage-settings"></a>impostazioni di archiviazione tooconfigure
1.  Nel portale di Azure > **Impostazioni**, fare clic su **Backup**.

    ![Backup in Impostazioni](./media/analysis-services-backup/aas-backup-backups.png)

2.  Fare clic su **Abilitata** e quindi su **Impostazioni di archiviazione**.

    ![Abilita](./media/analysis-services-backup/aas-backup-enable.png)

3. Selezionare l'account di archiviazione o crearne uno nuovo.

4. Selezionare un contenitore o crearne uno nuovo.

    ![Selezionare un contenitore](./media/analysis-services-backup/aas-backup-container.png)

5. Salvare le impostazioni di backup.

    ![Salvare le impostazioni di backup](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a>Backup

### <a name="toobackup-by-using-ssms"></a>toobackup utilizzando SQL Server Management Studio

1. In SSMS fare clic con il pulsante destro del mouse su un database > **Backup**.

2. In **Backup database** > **File di backup** fare clic su **Sfoglia**.

3. In hello **Salva file con nome** finestra di dialogo, verificare il percorso di cartella hello e quindi digitare un nome per il file di backup hello. 

4. In hello **Backup Database** finestra di dialogo, selezionare le opzioni.

    **Consenti file sovrascrivere** -selezionare questa opzione toooverwrite i file di backup di hello stesso nome. Se questa opzione non è selezionata, il file hello da salvare non può avere hello stesso nome come un file già esistente in hello stesso percorso.

    **Applicare la compressione** -selezionare l'opzione toocompress hello del file di backup. I file di backup compressi consentono di risparmiare spazio su disco, ma richiedono un utilizzo della CPU leggermente più elevato. 

    **Crittografare i file di backup** -selezionare l'opzione tooencrypt hello del file di backup. Questa opzione richiede un file di backup hello toosecure password fornita dall'utente. password Hello impedisce la lettura dei dati di backup hello qualsiasi altro mezzo di un'operazione di ripristino. Se si sceglie tooencrypt backup, archiviare password hello in un luogo sicuro.

5. Fare clic su **OK** toocreate e salvare i file di backup hello.


### <a name="powershell"></a>PowerShell
Usare il cmdlet [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).

## <a name="restore"></a>Ripristino
Durante il ripristino, il file di backup deve essere nell'account di archiviazione hello configurate per il server. Se è necessario un file di backup da un account di archiviazione locale percorso tooyour toomove, utilizzare [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) o hello [AzCopy](../storage/common/storage-use-azcopy.md) utilità della riga di comando. 



> [!NOTE]
> Se si esegue il ripristino da un server locale, è necessario rimuovere tutti gli utenti di dominio di hello dai ruoli del modello hello e aggiungerli nuovamente ruoli toohello come utenti di Azure Active Directory.
> 
> 

### <a name="toorestore-by-using-ssms"></a>toorestore utilizzando SQL Server Management Studio

1. In SSMS fare clic con il pulsante destro del mouse su un database > **Ripristina**.

2. In hello **Backup Database** finestra di dialogo, nella **file di Backup**, fare clic su **Sfoglia**.

3. In hello **Individua file di Database** finestra di dialogo, selezionare hello desiderata toorestore.

4. In **ripristinare il database**, selezionare il database di hello.

5. Specificare le opzioni. Opzioni di sicurezza devono corrispondere le opzioni di backup hello che è utilizzato per eseguire il backup.


### <a name="powershell"></a>PowerShell

Usare il cmdlet [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).


## <a name="related-information"></a>Informazioni correlate

[Account di archiviazione di Azure](../storage/common/storage-create-storage-account.md)  
[Disponibilità elevata](analysis-services-bcdr.md)     
[Gestire Azure Analysis Services](analysis-services-manage.md)
