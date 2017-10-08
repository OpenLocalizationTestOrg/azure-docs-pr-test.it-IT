---
title: aaaAutomated v2 Backup per SQL Server 2016 macchine virtuali di Azure | Documenti Microsoft
description: "Vengono illustrate funzionalità Backup automatizzato hello per SQL Server 2016 VM in esecuzione in Azure. Questo articolo è specifico tooVMs utilizzando hello Gestione risorse."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a>Backup automatico v2 per macchine virtuali SQL Server 2016 in Azure (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

V2 Backup automatizzato configura automaticamente [tooMicrosoft Backup gestito Azure](https://msdn.microsoft.com/library/dn449496.aspx) per tutti i database nuovi ed esistenti in una macchina virtuale di Azure in esecuzione SQL Server 2016 Standard, Enterprise Edition o Developer Edition. In questo modo tooconfigure normali backup di database che utilizzano l'archiviazione blob di Azure durevole. V2 Backup automatizzati dipende hello [estensione di SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Prerequisiti
toouse v2 Backup automatizzato, esaminare hello seguenti prerequisiti:

**Sistema operativo**:

- Windows Server 2012 R2
- Windows Server 2016

**Versione/edizione di SQL Server**:

- SQL Server 2016 Standard
- SQL Server 2016 Enterprise
- SQL Server 2016 Developer

> [!IMPORTANT]
> Backup automatico v2 funziona con SQL Server 2016. Se si utilizza SQL Server 2014, è possibile utilizzare Backup automatizzato v1 tooback backup dei database. Per altre informazioni, vedere [Backup automatico per SQL Server 2014 in Macchine virtuali di Azure](virtual-machines-windows-sql-automated-backup.md).

**Configurazione del database**:

- Database di destinazione devono utilizzare il modello di recupero con registrazione completa hello. Per ulteriori informazioni sull'impatto hello del modello di recupero con registrazione completa hello sui backup, vedere [hello Backup nel modello di recupero completo](https://technet.microsoft.com/library/ms190217.aspx).
- Database di sistema non dispone di toouse modello di recupero con registrazione completa. Tuttavia, se è necessario toobe backup log per modello o MSDB, è necessario utilizzare il modello di recupero con registrazione completa.
- Database di destinazione devono essere nell'istanza di SQL Server predefinito hello. Hello estensione IaaS di SQL Server non supporta le istanze denominate.

**Modello di distribuzione di Azure**:

- Gestione risorse

> [!NOTE]
> Backup automatizzato si basa su hello **estensione di SQL Server IaaS Agent**. Per impostazione predefinita, le attuali immagini della raccolta di macchine virtuali di SQL aggiungono questa estensione. Per altre informazioni, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Impostazioni
Hello nella tabella seguente vengono descritte hello opzioni che possono essere configurate per Backup automatizzato v2. passaggi di configurazione effettivi Hello variano a seconda che si utilizzi hello portale di Azure o i comandi di Windows PowerShell per Azure.

### <a name="basic-settings"></a>Basic Settings

| Impostazione | Intervallo (impostazione predefinita) | Descrizione |
| --- | --- | --- |
| **Backup automatico** | Enable/Disable (disabilitato) | Abilita o disabilita il backup automatico per una macchina virtuale di Azure in cui viene eseguito SQL Server 2016 Standard o Enterprise. |
| **Periodo di conservazione** | 1-30 giorni (30 giorni) | numero di Hello di backup di tooretain giorni. |
| **Storage Account** | Account di archiviazione di Azure | Toouse un account di archiviazione di Azure per archiviare i file di Backup automatizzato nell'archiviazione blob. Un contenitore viene creato in questo percorso toostore tutti i file di backup. file di backup Hello convenzione di denominazione include hello data, ora e il GUID del database. |
| **Crittografia** |Enable/Disable (disabilitato) | Abilita o disabilita la crittografia. Quando la crittografia è abilitata, hello i certificati utilizzati toorestore hello backup si trovano in hello specificato dell'account di archiviazione in hello stesso **automaticbackup** contenitore usando hello stessa convenzione di denominazione. Se la modifica di password hello, viene generato un nuovo certificato con la password, ma vecchio certificato hello rimane toorestore eventuale backup precedente. |
| **Password** |Testo della password | Password per le chiavi di crittografia. Questa impostazione è necessaria solo se la crittografia è abilitata. In ordine toorestore un backup crittografato, è necessario disporre la password corretta hello e del certificato correlato che è stato utilizzato in fase di hello hello del backup. |

### <a name="advanced-settings"></a>Impostazioni avanzate

| Impostazione | Intervallo (impostazione predefinita) | Descrizione |
| --- | --- | --- |
| **Backup dei database di sistema** | Enable/Disable (disabilitato) | Quando abilitata, questa funzionalità verrà anche eseguito il backup il database di sistema hello: Master, MSDB e modello. Per hello MSDB e modello di database, verificare che siano in modalità di recupero con registrazione completa se si desidera toobe i backup del log eseguito. Non vengono mai eseguiti backup di log per Master, né backup di alcun tipo per TempDB. |
| **Pianificazione backup** | Manual/Automated (Automated) (Manuale/Automatizzato - Automatizzato) | Per impostazione predefinita, pianificazione del backup hello verrà automaticamente determinato in base a una crescita log hello. Pianificazione del backup manuale consente l'intervallo di tempo hello toospecify hello utente per i backup. In questo caso, i backup avranno sempre luogo hello frequenza durante hello specificate e intervallo di tempo di un determinato giorno. |
| **Frequenza backup completo** | Giornaliera/settimanale | Frequenza dei backup completi. In entrambi i casi, i backup completi verranno avviato il successivo intervallo di tempo pianificato hello. Quando si seleziona la frequenza settimanale, i backup potrebbero durare più giorni fino ad aver incluso tutti i database. |
| **Ora di inizio backup completo** | 00:00 – 23:00 (01:00) | Ora di inizio di un determinato giorno in cui possono avere luogo i backup completi. |
| **Intervallo di tempo per il backup completo** | 1-23 ore (1 ora) | Durata dell'intervallo di tempo hello di un determinato giorno durante il quale può avvenire backup completi. |
| **Frequenza di backup del log** | 5-60 minuti (60 minuti) | Frequenza dei backup dei log. |

## <a name="understanding-full-backup-frequency"></a>Informazioni sulla frequenza dei backup completi
È importante toounderstand differenza di hello tra i backup completi giornalieri e settimanali. Per farlo, verranno illustrati due scenari di esempio.

### <a name="scenario-1-weekly-backups"></a>Scenario 1: Backup settimanali
Si dispone di una macchina virtuale di SQL Server che contiene una serie di database di dimensioni molto grandi.

Lunedì, si attiva v2 Backup automatizzato con hello seguenti impostazioni:

- Pianificazione backup: **Manuale**
- Frequenza backup completo: **Settimanale**
- Ora di inizio backup completo: **01:00**
- Intervallo di tempo dei backup completi: **1 ora**

Ciò significa che hello disponibili backup successivo è martedì alle 13.00 per 1 ora. In quel momento, Backup automatico inizierà a eseguire il backup dei database, uno alla volta. In questo scenario, i database sono sufficientemente grandi il completamento per i database coppia primo hello backup completi. Tuttavia, dopo un'ora non tutti i database hello è stato eseguito il.

In questo caso, verrà avviato Backup automatizzato backup hello rimanenti hello database giorno successivo, mercoledì alle 13.00 per 1 ora. Se non tutti i database sottoposti a backup in quel momento, si tenterà nuovamente hello giorno successivo a hello stesso tempo. fe così via fino a quando non sarà stato eseguito il backup di tutti i database.

Il martedì successivo, Backup automatico comincerà nuovamente il backup di tutti i database.

Questo scenario viene illustrato che funzionerà solo Backup automatizzato nell'intervallo di tempo specificato hello e ogni database da sottoporre a backup una volta alla settimana. Mostra anche che è possibile per backup toospan più giorni in hello caso in cui non è possibile toocomplete tutti i backup in un solo giorno.

### <a name="scenario-2-daily-backups"></a>Scenario 2: Backup giornalieri
Si dispone di una macchina virtuale di SQL Server che contiene una serie di database di dimensioni molto grandi.

Lunedì, si attiva v2 Backup automatizzato con hello seguenti impostazioni:

- Pianificazione backup: Manuale
- Frequenza backup completo: Ogni giorno
- Ora di inizio backup completo: 22:00
- Intervallo di tempo dei backup completi: 6 ore

Ciò significa che hello disponibili backup successivo è lunedì 10 PM per 6 ore. In quel momento, Backup automatico inizierà a eseguire il backup dei database, uno alla volta.

Il backup sarà quindi eseguito nuovamente martedì alle 22:00 per 6 ore.

> [!IMPORTANT]
> Durante la pianificazione dei backup giornalieri, è consigliabile pianificare un tooensure finestra wide ora che tutti i database è possibile eseguire backup entro questo intervallo. Ciò è particolarmente importante in caso di hello in cui si dispone di una grande quantità di dati tooback backup.

## <a name="configuration-in-hello-portal"></a>Configurazione di hello portale

È possibile utilizzare hello tooconfigure portale Azure Backup automatizzato v2 durante il provisioning o per le macchine virtuali di esistente SQL Server 2016.

### <a name="new-vms"></a>Nuove VM

Quando si crea una nuova macchina virtuale di SQL Server 2016 nel modello di distribuzione di gestione risorse di hello, utilizzare hello tooconfigure portale Azure Backup automatizzato v2. 

In hello **impostazioni di SQL Server** pannello seleziona **backup automatizzato**. schermata del portale di Azure seguente Hello Mostra hello **Backup automatizzato SQL** blade.

![Configurazione del backup automatico di SQL nel Portale di Azure](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> L'opzione Backup automatico v2 è disabilitata per impostazione predefinita.

Per contesto, vedere l'argomento completo hello in [provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>VM esistenti

Per le macchine virtuali SQL Server esistenti, selezionare la macchina virtuale SQL Server. Selezionare quindi hello **configurazione di SQL Server** sezione di hello **impostazioni** blade.

![Backup automatico di SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

In hello **configurazione di SQL Server** pannello, fare clic su hello **modifica** pulsante hello automatizzata sezione backup.

![Configurare il backup automatico di SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

Al termine, fare clic su hello **OK** pulsante nella parte inferiore di hello di hello **configurazione di SQL Server** pannello toosave le modifiche.

Se si sta abilitando Backup automatizzato per hello prima volta, Azure Configura hello agente IaaS di SQL Server in background hello. Durante questo periodo, hello portale di Azure potrebbe non visualizzare che Backup automatizzato è configurato. Attendere alcuni minuti per hello agente toobe installato, configurato. Dopo tale hello Azure portale rispecchierà le nuove impostazioni hello.

## <a name="configuration-with-powershell"></a>Configurazione con PowerShell

È possibile utilizzare PowerShell tooconfigure v2 Backup automatizzato. Prima di iniziare, è necessario eseguire queste operazioni:

- [Scaricare e installare hello più recente di Azure PowerShell](http://aka.ms/webpi-azps).
- Aprire Windows PowerShell e associarlo al proprio account. È possibile farlo attenendosi alla seguente procedura hello in hello [configura la sottoscrizione](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sezione di hello provisioning argomento.

### <a name="install-hello-sql-iaas-extension"></a>Installare hello estensione SQL IaaS
Se eseguito il provisioning di una macchina virtuale di SQL Server dal portale di Azure hello, hello estensione IaaS di SQL Server deve essere già installato. È possibile determinare se è installato per la macchina virtuale tramite la chiamata **Get AzureRmVM** comando ed esaminando hello **estensioni** proprietà.

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

Se è installato l'estensione di SQL Server IaaS Agent hello, si dovrebbe che è elencato come "SqlIaaSAgent" o "SQLIaaSExtension". **ProvisioningState** per estensione hello deve inoltre visualizzare "Succeeded". 

Se non è installato o non è stato possibile toobe il provisioning, è possibile installarlo con hello comando seguente. In aggiunta toohello VM nome e la risorsa gruppo, è necessario specificare anche area hello (**$region**) che la macchina virtuale si trova in.

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <a id="verifysettings"></a> Verificare le impostazioni correnti
Se è abilitato il backup automatizzato durante il provisioning, è possibile utilizzare PowerShell toocheck la configurazione corrente. Eseguire hello **Get AzureRmVMSqlServerExtension** comando ed esaminare hello **AutoBackupSettings** proprietà:

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

È necessario ottenere seguente toohello simili di output:

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

Se l'output mostra che **abilitare** è troppo**False**, è necessario tooenable backup automatico. Hello buone notizie sono attivare e configurare il Backup automatizzato in hello allo stesso modo. Vedere hello sezione successiva per ottenere questa informazione.

> [!NOTE] 
> Se si seleziona impostazioni hello immediatamente dopo aver apportato una modifica, è possibile che si otterranno nuovamente i valori di configurazione precedente hello. Attendere alcuni minuti e verificare le impostazioni di hello nuovamente toomake assicurarsi che siano state applicate le modifiche.

### <a name="configure-automated-backup-v2"></a>Configurare Backup automatico v2
È possibile utilizzare PowerShell tooenable Backup automatizzato, nonché toomodify la configurazione e il comportamento in qualsiasi momento. 

In primo luogo, selezionare o creare un account di archiviazione per hello i file di backup. Hello lo script seguente consente di selezionare un account di archiviazione o la crea se non esiste.

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> Backup automatico non supporta l'archiviazione di backup nell'archiviazione Premium, ma può ottenere i backup da dischi di macchine virtuali che usano l'archiviazione Premium.

Utilizzare quindi hello **New AzureRmVMSqlServerAutoBackupConfig** comando tooenable e configurare i backup di toostore impostazioni hello v2 Backup automatizzato nell'account di archiviazione Azure hello. In questo esempio, i backup di hello sono impostati toobe conservati per 10 giorni. I backup del database di sistema sono abilitati. I backup completi sono pianificati come settimanali, con un intervallo di tempo di due ore a partire dalle 20:00. I backup del log vengono eseguiti ogni 30 minuti. Hello secondo comando, **Set AzureRmVMSqlServerExtension**, hello aggiornamenti specificato macchina virtuale di Azure con queste impostazioni.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

Potrebbe richiedere diversi minuti tooinstall e configurare hello agente IaaS di SQL Server. 

crittografia tooenable, modificare hello di hello precedente script toopass **EnableEncryption** parametro e una password (stringa sicura) per hello **CertificatePassword** parametro. Hello seguente script abilita le impostazioni di Backup automatizzato hello nell'esempio precedente hello e aggiunge la crittografia.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

le impostazioni vengono applicate, tooconfirm [verificare la configurazione di Backup automatizzato hello](#verifysettings).

### <a name="disable-automated-backup"></a>Disabilitare Backup automatico
Backup automatizzato, esecuzione hello stesso script senza hello toodisable **-abilitare** parametro toohello **New AzureRmVMSqlServerAutoBackupConfig** comando. assenza di hello Hello **-abilitare** funzionalità di parametro segnali hello comando toodisable hello. Come per l'installazione, può richiedere diversi minuti toodisable Backup automatizzato.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a>Script di esempio
Hello script riportato di seguito fornisce un set di variabili che è possibile personalizzare tooenable e configurare il Backup automatizzato per la macchina virtuale. Il caso, potrebbe essere necessario script hello toocustomize in base alle esigenze. Ad esempio, si sarebbe sono state apportate modifiche toomake, se si desidera utilizzare backup hello toodisable dei database di sistema o abilitare la crittografia.

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Passaggi successivi
Backup automatico v2 configura backup gestito in Macchine virtuali di Azure. È importante troppo[, vedere la documentazione di hello per il Backup gestito](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello comportamento e le implicazioni.

È possibile trovare ulteriori backup e ripristino istruzioni for SQL Server in macchine virtuali di Azure nel seguente argomento hello: [di Backup e ripristino per SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-backup-recovery.md).

Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).

