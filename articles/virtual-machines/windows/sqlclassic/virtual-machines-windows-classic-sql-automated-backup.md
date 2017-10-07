---
title: aaaAutomated Backup per SQL Server le macchine virtuali (classico) | Documenti Microsoft
description: "Vengono illustrate funzionalità Backup automatizzato hello per SQL Server in esecuzione in Azure VM con Gestione risorse. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a>Backup automatico per SQL Server in macchine virtuali di Azure (distribuzione classica)
> [!div class="op_single_selector"]
> * [Gestione risorse](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [Classico](../classic/sql-automated-backup.md)
> 
> 

Backup automatizzato configura automaticamente [tooMicrosoft Backup gestito Azure](https://msdn.microsoft.com/library/dn449496.aspx) per tutti i database nuovi ed esistenti in una macchina virtuale di Azure che esegue SQL Server 2014 Standard o Enterprise. In questo modo tooconfigure normali backup di database che utilizzano l'archiviazione blob di Azure durevole. Backup automatizzato dipende hello [estensione di SQL Server IaaS Agent](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. tooview hello Gestione risorse di questo articolo, vedere [Backup automatizzato per SQL Server in Gestione risorse di macchine virtuali Azure](../sql/virtual-machines-windows-sql-automated-backup.md).

## <a name="prerequisites"></a>Prerequisiti
toouse Backup automatizzato, prendere in considerazione hello seguenti prerequisiti:

**Sistema operativo**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Versione/edizione di SQL Server**:

* SQL Server 2014 Standard
* SQL Server 2014 Enterprise

> [!NOTE]
> SQL Server 2016 non supporta ancora il backup automatizzato.
> 
> 

**Configurazione del database**:

* Database di destinazione devono utilizzare il modello di recupero con registrazione completa hello.

**Azure PowerShell**:

* [Installare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview).

**Estensione di SQL Server IaaS**:

* [Installare l'estensione di SQL Server IaaS hello](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Impostazioni
Hello nella tabella seguente vengono descritte hello opzioni che possono essere configurate per il Backup automatizzato. Per le macchine virtuali classiche, è necessario utilizzare PowerShell tooconfigure queste impostazioni.

| Impostazione | Intervallo (impostazione predefinita) | Descrizione |
| --- | --- | --- |
| **Backup automatico** |Enable/Disable (disabilitato) |Abilita o disabilita il backup automatico per una macchina virtuale di Azure in cui viene eseguito SQL Server 2014 Standard o Enterprise. |
| **Periodo di conservazione** |1-30 giorni (30 giorni) |numero di Hello di giorni tooretain una copia di backup. |
| **Storage Account** |Account di archiviazione di Azure (account di archiviazione hello creato per hello specificato VM) |Toouse un account di archiviazione di Azure per archiviare i file di Backup automatizzato nell'archiviazione blob. Un contenitore viene creato in questo percorso toostore tutti i file di backup. file di backup Hello convenzione di denominazione include hello data, ora e nome del computer. |
| **Crittografia** |Enable/Disable (disabilitato) |Abilita o disabilita la crittografia. Quando è abilitata la crittografia, certificati hello backup hello toorestore utilizzati si trovano in hello specificato l'account di archiviazione in hello automaticbackup stesso contenitore usando hello stessa convenzione di denominazione. Se la modifica di password hello, viene generato un nuovo certificato con la password, ma vecchio certificato hello rimane toorestore eventuale backup precedente. |
| **Password** |Testo della password (nessuno) |Password per le chiavi di crittografia. Questa impostazione è necessaria solo se la crittografia è abilitata. In ordine toorestore un backup crittografato, è necessario disporre la password corretta hello e del certificato correlato che è stato utilizzato in fase di hello hello del backup. | **Backup system databases** (Backup dei database di sistema) | Enable/Disable (disabilitato) | Eseguire backup completi di database master, modello e MSDB |
| **Configure backup schedule** (Configura la pianificazione dei backup) | Manual/Automated (Automated) (Manuale/Automatizzato - Automatizzato) | Selezionare **automatizzata** tooautomatically sfruttare e accedere in base all'aumento delle dimensioni del log. Selezionare **manuale** pianificazione hello toospecify per full e i backup del log. |

## <a name="configuration-with-powershell"></a>Configurazione con PowerShell
Nel seguente esempio di PowerShell di hello, Backup automatizzato è configurato per una VM esistente di SQL Server 2014. Hello **New AzureVMSqlServerAutoBackupConfig** comando Configura backup toostore le impostazioni del Backup automatizzato hello nell'account di archiviazione Azure hello specificata dalla variabile hello $storageaccount. Questi backup verranno conservati per 10 giorni. Hello **Set AzureVMSqlServerExtension** comando hello aggiornamenti specificato macchina virtuale di Azure con queste impostazioni.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

Potrebbe richiedere diversi minuti tooinstall e configurare hello agente IaaS di SQL Server.

crittografia tooenable, modificare hello precedente script toopass hello parametro EnableEncryption e una password (stringa sicura) per il parametro CertificatePassword hello. Hello seguente script abilita le impostazioni di Backup automatizzato hello nell'esempio precedente hello e aggiunge la crittografia.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

backup automatico toodisable, esecuzione hello stesso script senza hello **-abilitare** toohello parametro **New AzureVMSqlServerAutoBackupConfig**. Come per l'installazione, può richiedere diversi minuti toodisable Backup automatizzato.

> [!NOTE]
> Disabilitazione e disinstallazione di SQL Server IaaS Agent hello non rimuove le impostazioni di Backup gestito di hello configurato in precedenza. È necessario disabilitare i Backup automatizzato prima di disabilitare o disinstallare hello agente IaaS di SQL Server.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Backup automatico configura backup gestito in Macchine virtuali di Azure. È importante troppo[, vedere la documentazione di hello per il Backup gestito](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello comportamento e le implicazioni.

È possibile trovare ulteriori backup e ripristino istruzioni for SQL Server in macchine virtuali di Azure nel seguente argomento hello: [di Backup e ripristino per SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](../classic/sql-server-agent-extension.md).

Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

