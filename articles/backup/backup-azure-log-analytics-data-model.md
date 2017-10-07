---
title: modello di dati aaaLog Analitica per il Backup di Azure
description: Questo articolo illustra i dettagli del modello di dati di Log Analytics per i dati di Backup di Azure.
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: dfd5c73d-0d34-4d48-959e-1936986f9fc0
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 04ac16e38b896851f60b1c4ffbea4343347ae32c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-model-for-azure-backup-data"></a>Modello di dati di Log Analytics per i dati di Backup di Azure
In questo articolo viene descritto il modello di dati hello usato per l'inserimento di reporting tooLog dati Analitica. Usando questo modello di dati, è possibile creare query personalizzate e dashboard e usarle in OMS. 

## <a name="using-azure-backup-data-model"></a>Uso del modello di dati di Backup di Azure
È possibile utilizzare i seguenti campi forniti come parte di oggetti visivi toocreate modello di dati hello, query personalizzate e dashboard in base alle esigenze di hello.

### <a name="alert"></a>Avviso
Questa tabella offre dettagli sui campi relativi agli avvisi.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| AlertUniqueId_s |Text |Id univoco di hello ha generato l'avviso |
| AlertType_s |Text |Tipo di hello generato l'avviso, ad esempio, Backup |
| AlertStatus_s |Text |Stato dell'avviso di hello, ad esempio, attivo |
| AlertOccurenceDateTime_s |Data/ora |Data e ora in cui è stato creato l'avviso |
| AlertSeverity_s |Text |Gravità dell'avviso di hello, ad esempio, critico |
| EventName_s |Text |Questo campo rappresenta il nome di questo evento, che è sempre AzureBackupCentralReport |
| BackupItemUniqueId_s |Text |Id univoco di questo avviso appartiene troppo di hello backup dell'elemento toowhich|
| SchemaVersion_s |Text |Questo campo indica la versione corrente dello schema di hello, è **V1** |
| State_s |Text |Stato corrente dell'oggetto avviso hello, ad esempio, attivo, eliminati |
| BackupManagementType_s |Text |Tipo di provider per l'esecuzione di backup, ad esempio, IaaSVM, toowhich FileFolder questo avviso appartiene troppo|
| OperationName |Text |Questo campo rappresenta nome dell'operazione corrente hello - avviso |
| Categoria |Text |Questo campo rappresenta una categoria di dati di diagnostica inseriti tooLog Analitica, è AzureBackupReport |
| Risorsa |Text |Si tratta di hello risorsa per cui sono stati raccolti i dati, verrà visualizzato nome insieme di credenziali di servizi di ripristino |
| ProtectedServerUniqueId_s |Text |Id univoco di hello protetto toowhich che questo avviso appartiene troppo|
| VaultUniqueId_s |Text |Id univoco di hello protetto toowhich che questo avviso appartiene troppo|
| SourceSystem |Text |Sistema di origine di dati corrente hello - Azure |
| ResourceId |Text |Questo campo rappresenta l'id risorsa per cui sono stati raccolti i dati, verrà visualizzato l'id risorsa dell'insieme di credenziali dei servizi di ripristino |
| SubscriptionId |Text |Questo campo rappresenta l'id sottoscrizione di risorse hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceGroup |Text |Questo campo rappresenta il gruppo di risorse della risorsa hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceProvider |Text |Questo campo rappresenta hello provider di risorse per cui sono stati raccolti dati - Microsoft.RecoveryServices |
| ResourceType |Text |Questo campo rappresenta tipo di risorsa hello per cui sono stati raccolti dati - insiemi di credenziali |

### <a name="backupitem"></a>BackupItem
Questa tabella offre dettagli sui campi relativi agli elementi di backup.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| EventName_s |Text |Questo campo rappresenta il nome di questo evento, che è sempre AzureBackupCentralReport |  
| BackupItemUniqueId_s |Text |Id univoco del backup dell'elemento hello |
| BackupItemId_s |Text |ID dell'elemento di backup |
| BackupItemName_s |Text |Nome dell'elemento di backup |
| BackupItemFriendlyName_s |Text |Nome descrittivo dell'elemento di backup |
| BackupItemType_s |Text |Tipo dell'elemento di backup, ad esempio macchina virtuale o FileFolder |
| ProtectedServerName_s |Text |Nome del server protetto toowhich backup dell'elemento appartiene troppo|
| ProtectionState_s |Text |Stato corrente della protezione di hello backup dell'elemento, ad esempio, Protected, ProtectionStopped |
| SchemaVersion_s |Text |Questo campo indica la versione corrente dello schema di hello, è **V1** |
| State_s |Text |Stato corrente dell'oggetto di backup dell'elemento hello, ad esempio, attivo, eliminati |
| BackupManagementType_s |Text |Tipo di provider per l'esecuzione di backup, ad esempio, IaaSVM, toowhich FileFolder l'elemento corrente backup appartiene troppo|
| OperationName |Text |Questo campo rappresenta nome dell'operazione corrente hello - BackupItem |
| Categoria |Text |Questo campo rappresenta una categoria di dati di diagnostica inseriti tooLog Analitica, è AzureBackupReport |
| Risorsa |Text |Si tratta di hello risorsa per cui sono stati raccolti i dati, verrà visualizzato nome insieme di credenziali di servizi di ripristino |
| SourceSystem |Text |Sistema di origine di dati corrente hello - Azure |
| ResourceId |Text |Questo campo rappresenta l'id risorsa per cui sono stati raccolti i dati, verrà visualizzato l'id risorsa dell'insieme di credenziali dei servizi di ripristino |
| SubscriptionId |Text |Questo campo rappresenta l'id sottoscrizione di risorse hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceGroup |Text |Questo campo rappresenta il gruppo di risorse della risorsa hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceProvider |Text |Questo campo rappresenta hello provider di risorse per cui sono stati raccolti dati - Microsoft.RecoveryServices |
| ResourceType |Text |Questo campo rappresenta tipo di risorsa hello per cui sono stati raccolti dati - insiemi di credenziali |

### <a name="backupitemassociation"></a>BackupItemAssociation
Questa tabella fornisce dettagli sulle associazioni degli elementi di backup con varie entità.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| EventName_s |Text |Questo campo rappresenta il nome di questo evento, che è sempre AzureBackupCentralReport |  
| BackupItemUniqueId_s |Text |Id univoco del backup dell'elemento hello |
| SchemaVersion_s |Text |Questo campo indica la versione corrente dello schema di hello, è **V1** |
| State_s |Text |Stato corrente di hello backup dell'elemento associazione oggetto, ad esempio, attivo, eliminati |
| BackupManagementType_s |Text |Tipo di provider per l'esecuzione di backup, ad esempio, IaaSVM, toowhich FileFolder l'elemento corrente backup appartiene troppo|
| OperationName |Text |Questo campo rappresenta nome dell'operazione corrente hello - BackupItemAssociation |
| Categoria |Text |Questo campo rappresenta una categoria di dati di diagnostica inseriti tooLog Analitica, è AzureBackupReport |
| Risorsa |Text |Si tratta di hello risorsa per cui sono stati raccolti i dati, verrà visualizzato nome insieme di credenziali di servizi di ripristino |
| PolicyUniqueId_g |Text |Id tooidentify hello criterio univoco, il backup dell'elemento è troppo associato|
| ProtectedServerUniqueId_s |Text |Id univoco di hello protetto toowhich server che l'elemento corrente backup appartiene troppo|
| VaultUniqueId_s |Text |Id univoco di hello toowhich di insieme di credenziali per che l'elemento corrente backup appartiene troppo|
| SourceSystem |Text |Sistema di origine di dati corrente hello - Azure |
| ResourceId |Text |Questo campo rappresenta l'id risorsa per cui sono stati raccolti i dati, verrà visualizzato l'id risorsa dell'insieme di credenziali dei servizi di ripristino |
| SubscriptionId |Text |Questo campo rappresenta l'id sottoscrizione di risorse hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceGroup |Text |Questo campo rappresenta il gruppo di risorse della risorsa hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceProvider |Text |Questo campo rappresenta hello provider di risorse per cui sono stati raccolti dati - Microsoft.RecoveryServices |
| ResourceType |Text |Questo campo rappresenta tipo di risorsa hello per cui sono stati raccolti dati - insiemi di credenziali |

### <a name="job"></a>Job
Questa tabella offre dettagli sui campi relativi al processo.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| EventName_s |Text |Questo campo rappresenta il nome di questo evento, che è sempre AzureBackupCentralReport |
| BackupItemUniqueId_s |Text |Id univoco di questo processo appartiene troppo di hello backup dell'elemento toowhich|
| SchemaVersion_s |Text |Questo campo indica la versione corrente dello schema di hello, è **V1** |
| State_s |Text |Stato corrente dell'oggetto processo hello, ad esempio, attivo, eliminati |
| BackupManagementType_s |Text |Tipo di provider per l'esecuzione di backup, ad esempio, IaaSVM, toowhich FileFolder questo processo appartiene troppo|
| OperationName |Text |Questo campo rappresenta nome dell'operazione corrente hello - processo |
| Categoria |Text |Questo campo rappresenta una categoria di dati di diagnostica inseriti tooLog Analitica, è AzureBackupReport |
| Risorsa |Text |Si tratta di hello risorsa per cui sono stati raccolti i dati, verrà visualizzato nome insieme di credenziali di servizi di ripristino |
| ProtectedServerUniqueId_s |Text |Id univoco di hello protetto toowhich che questo processo appartiene troppo|
| VaultUniqueId_s |Text |Id univoco di hello protetto toowhich che questo processo appartiene troppo|
| JobOperation_s |Text |Operazione per la quale viene eseguito il processo, ad esempio Backup, Restore o Configure Backup |
| JobStatus_s |Text |Stato di hello terminate processo, ad esempio, completato, non riuscito |
| JobFailureCode_s |Text |Stringa di codice contenente un errore e a causa della quale si è verificato un errore del processo |
| JobStartDateTime_s |Data/ora |Data e ora di avvio dell'esecuzione del processo |
| BackupStorageDestination_s |Text |Destinazione dell'archiviazione di backup, ad esempio Cloud o Disk  |
| JobDurationInSecs_s | Number |Durata totale del processo in secondi |
| DataTransferredInMB_s | Number |Dati trasferiti in MB per il processo|
| JobUniqueId_g |Text |Processo di hello tooidentify Id univoco |
| SourceSystem |Text |Sistema di origine di dati corrente hello - Azure |
| ResourceId |Text |Questo campo rappresenta l'id risorsa per cui sono stati raccolti i dati, verrà visualizzato l'id risorsa dell'insieme di credenziali dei servizi di ripristino |
| SubscriptionId |Text |Questo campo rappresenta l'id sottoscrizione di risorse hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceGroup |Text |Questo campo rappresenta il gruppo di risorse della risorsa hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceProvider |Text |Questo campo rappresenta hello provider di risorse per cui sono stati raccolti dati - Microsoft.RecoveryServices |
| ResourceType |Text |Questo campo rappresenta tipo di risorsa hello per cui sono stati raccolti dati - insiemi di credenziali |

### <a name="policy"></a>Criteri
Questa tabella offre dettagli sui campi relativi al criterio.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| EventName_s |Text |Questo campo rappresenta il nome di questo evento, che è sempre AzureBackupCentralReport |
| SchemaVersion_s |Text |Questo campo indica la versione corrente dello schema di hello, è **V1** |
| State_s |Text |Stato corrente dell'oggetto Criteri di hello, ad esempio, attivo, eliminati |
| BackupManagementType_s |Text |Tipo di provider per l'esecuzione di backup, ad esempio, IaaSVM, toowhich FileFolder troppo appartengono i criteri|
| OperationName |Text |Questo campo rappresenta nome dell'operazione corrente hello - criteri |
| Categoria |Text |Questo campo rappresenta una categoria di dati di diagnostica inseriti tooLog Analitica, è AzureBackupReport |
| Risorsa |Text |Si tratta di hello risorsa per cui sono stati raccolti i dati, verrà visualizzato nome insieme di credenziali di servizi di ripristino |
| PolicyUniqueId_g |Text |Criterio di hello tooidentify Id univoco |
| PolicyName_s |Text |Nome del criterio hello definito |
| BackupFrequency_s |Text |Frequenza con cui vengono eseguiti i backup, ad esempio daily o weekly |
| BackupTimes_s |Text |Data e ora in cui sono pianificati backup |
| BackupDaysOfTheWeek_s |Text |Giorni della settimana hello quando sono stati pianificati backup |
| RetentionDuration_s |Numero intero |Durata di mantenimento dei backup configurati |
| DailyRetentionDuration_s |Numero intero |Durata totale di mantenimento dati in giorni per i backup configurati |
| DailyRetentionTimes_s |Text |Data e ora di configurazione del mantenimento dati giornaliero |
| WeeklyRetentionDuration_s |Numero decimale |Durata totale del mantenimento dati settimanale in settimane per i backup configurati |
| WeeklyRetentionTimes_s |Text |Data e ora di configurazione del mantenimento dati settimanale |
| WeeklyRetentionDaysOfTheWeek_s |Text |Giorni della settimana hello selezionato per la conservazione settimanale |
| MonthlyRetentionDuration_s |Numero decimale |Durata totale di mantenimento dati in mesi per i backup configurati |
| MonthlyRetentionTimes_s |Text |Data e ora di configurazione del mantenimento dati mensile |
| MonthlyRetentionFormat_s |Text |Tipo di configurazione per il mantenimento dati mensile, ad esempio daily per la configurazione basata sui giorni o weekly per la configurazione basata sulle settimane |
| MonthlyRetentionDaysOfTheWeek_s |Text |Giorni della settimana hello selezionato per la conservazione mensile |
| MonthlyRetentionWeeksOfTheMonth_s |Text |Settimane del mese di hello quando conservazione mensile è configurato, ad esempio primo, ultimo via. |
| YearlyRetentionDuration_s |Numero decimale |Durata totale di mantenimento dati in anni per i backup configurati |
| YearlyRetentionTimes_s |Text |Data e ora di configurazione del mantenimento dati annuale |
| YearlyRetentionMonthsOfTheYear_s |Text |Mesi dell'anno di hello selezionato per la conservazione annuale |
| YearlyRetentionFormat_s |Text |Tipo di configurazione per il mantenimento dati annuale, ad esempio daily per la configurazione basata sui giorni o weekly per la configurazione basata sulle settimane |
| YearlyRetentionDaysOfTheMonth_s |Text |Date del mese hello selezionati per la conservazione annuale |
| SourceSystem |Text |Sistema di origine di dati corrente hello - Azure |
| ResourceId |Text |Questo campo rappresenta l'id risorsa per cui sono stati raccolti i dati, verrà visualizzato l'id risorsa dell'insieme di credenziali dei servizi di ripristino |
| SubscriptionId |Text |Questo campo rappresenta l'id sottoscrizione di risorse hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceGroup |Text |Questo campo rappresenta il gruppo di risorse della risorsa hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceProvider |Text |Questo campo rappresenta hello provider di risorse per cui sono stati raccolti dati - Microsoft.RecoveryServices |
| ResourceType |Text |Questo campo rappresenta tipo di risorsa hello per cui sono stati raccolti dati - insiemi di credenziali |

### <a name="policyassociation"></a>PolicyAssociation
Questa tabella fornisce dettagli sulle associazioni dei criteri con varie entità.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| EventName_s |Text |Questo campo rappresenta il nome di questo evento, che è sempre AzureBackupCentralReport |
| SchemaVersion_s |Text |Questo campo indica la versione corrente dello schema di hello, è **V1** |
| State_s |Text |Stato corrente dell'oggetto Criteri di hello, ad esempio, attivo, eliminati |
| BackupManagementType_s |Text |Tipo di provider per l'esecuzione di backup, ad esempio, IaaSVM, toowhich FileFolder troppo appartengono i criteri|
| OperationName |Text |Questo campo rappresenta nome dell'operazione corrente hello - PolicyAssociation |
| Categoria |Text |Questo campo rappresenta una categoria di dati di diagnostica inseriti tooLog Analitica, è AzureBackupReport |
| Risorsa |Text |Si tratta di hello risorsa per cui sono stati raccolti i dati, verrà visualizzato nome insieme di credenziali di servizi di ripristino |
| PolicyUniqueId_g |Text |Criterio di hello tooidentify Id univoco |
| VaultUniqueId_s |Text |Id univoco di hello insieme di credenziali toowhich che troppo appartengono i criteri|
| SourceSystem |Text |Sistema di origine di dati corrente hello - Azure |
| ResourceId |Text |Questo campo rappresenta l'id risorsa per cui sono stati raccolti i dati, verrà visualizzato l'id risorsa dell'insieme di credenziali dei servizi di ripristino |
| SubscriptionId |Text |Questo campo rappresenta l'id sottoscrizione di risorse hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceGroup |Text |Questo campo rappresenta il gruppo di risorse della risorsa hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceProvider |Text |Questo campo rappresenta hello provider di risorse per cui sono stati raccolti dati - Microsoft.RecoveryServices |
| ResourceType |Text |Questo campo rappresenta tipo di risorsa hello per cui sono stati raccolti dati - insiemi di credenziali |

### <a name="protectedserver"></a>ProtectedServer
Questa tabella offre dettagli sui campi relativi al server protetto.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| EventName_s |Text |Questo campo rappresenta il nome di questo evento, che è sempre AzureBackupCentralReport |
| ProtectedServerName_s |Text |Nome del server protetto |
| SchemaVersion_s |Text |Questo campo indica la versione corrente dello schema di hello, è **V1** |
| State_s |Text |Stato corrente di hello protetto oggetto server, ad esempio, attivo, eliminati |
| BackupManagementType_s |Text |Tipo di provider per l'esecuzione di backup, ad esempio, IaaSVM, toowhich FileFolder troppo cui appartiene questo server protetto|
| OperationName |Text |Questo campo rappresenta nome dell'operazione corrente hello - ProtectedServer |
| Categoria |Text |Questo campo rappresenta una categoria di dati di diagnostica inseriti tooLog Analitica, è AzureBackupReport |
| Risorsa |Text |Si tratta di hello risorsa per cui sono stati raccolti i dati, verrà visualizzato nome insieme di credenziali di servizi di ripristino |
| ProtectedServerUniqueId_s |Text |Id univoco di hello server protetto |
| RegisteredContainerId_s |Text |ID del contenitore registrato per il backup |
| ProtectedServerType_s |Text |Tipo di server protetto di cui si esegue il backup, ad esempio Windows |
| ProtectedServerFriendlyName_s |Text |Nome descrittivo del server protetto |
| AzureBackupAgentVersion_s |Text |Numero di versione dell'agente di Backup di Azure |
| SourceSystem |Text |Sistema di origine di dati corrente hello - Azure |
| ResourceId |Text |Questo campo rappresenta l'id risorsa per cui sono stati raccolti i dati, verrà visualizzato l'id risorsa dell'insieme di credenziali dei servizi di ripristino |
| SubscriptionId |Text |Questo campo rappresenta l'id sottoscrizione di risorse hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceGroup |Text |Questo campo rappresenta il gruppo di risorse della risorsa hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceProvider |Text |Questo campo rappresenta hello provider di risorse per cui sono stati raccolti dati - Microsoft.RecoveryServices |
| ResourceType |Text |Questo campo rappresenta tipo di risorsa hello per cui sono stati raccolti dati - insiemi di credenziali |

### <a name="protectedserverassociation"></a>ProtectedServerAssociation
Questa tabella fornisce dettagli sulle associazioni dei server protetti con altre entità.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| EventName_s |Text |Questo campo rappresenta il nome di questo evento, che è sempre AzureBackupCentralReport |
| SchemaVersion_s |Text |Questo campo indica la versione corrente dello schema di hello, è **V1** |
| State_s |Text |Stato corrente di hello protetto oggetto di associazione server, ad esempio, attivo, eliminati |
| BackupManagementType_s |Text |Tipo di provider per l'esecuzione di backup, ad esempio, IaaSVM, toowhich FileFolder troppo cui appartiene questo server protetto|
| OperationName |Text |Questo campo rappresenta nome dell'operazione corrente hello - ProtectedServerAssociation |
| Categoria |Text |Questo campo rappresenta una categoria di dati di diagnostica inseriti tooLog Analitica, è AzureBackupReport |
| Risorsa |Text |Si tratta di hello risorsa per cui sono stati raccolti i dati, verrà visualizzato nome insieme di credenziali di servizi di ripristino |
| ProtectedServerUniqueId_s |Text |Id univoco di hello server protetto |
| VaultUniqueId_s |Text |Id univoco di hello insieme di credenziali toowhich che troppo cui appartiene questo server protetto|
| SourceSystem |Text |Sistema di origine di dati corrente hello - Azure |
| ResourceId |Text |Questo campo rappresenta l'id risorsa per cui sono stati raccolti i dati, verrà visualizzato l'id risorsa dell'insieme di credenziali dei servizi di ripristino |
| SubscriptionId |Text |Questo campo rappresenta l'id sottoscrizione di risorse hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceGroup |Text |Questo campo rappresenta il gruppo di risorse della risorsa hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceProvider |Text |Questo campo rappresenta hello provider di risorse per cui sono stati raccolti dati - Microsoft.RecoveryServices |
| ResourceType |Text |Questo campo rappresenta tipo di risorsa hello per cui sono stati raccolti dati - insiemi di credenziali |

### <a name="storage"></a>Archiviazione
Questa tabella offre dettagli sui campi relativi all'archiviazione.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| CloudStorageInBytes_s |Numero decimale |Spazio di archiviazione nel cloud usato dal backup, calcolato in base al valore più recente |
| ProtectedInstances_s |Numero decimale |Numero di istanze protette usato per il calcolo dell'archiviazione front-end a scopo di fatturazione, calcolato in base al valore più recente |
| EventName_s |Text |Questo campo rappresenta il nome di questo evento, che è sempre AzureBackupCentralReport |
| SchemaVersion_s |Text |Questo campo indica la versione corrente dello schema di hello, è **V1** |
| State_s |Text |Stato corrente dell'oggetto di archiviazione hello, ad esempio, attivo, eliminati |
| BackupManagementType_s |Text |Tipo di provider per l'esecuzione di backup, ad esempio, IaaSVM, toowhich FileFolder questa risorsa di archiviazione appartiene troppo|
| OperationName |Text |Questo campo rappresenta nome dell'operazione corrente hello - archiviazione |
| Categoria |Text |Questo campo rappresenta una categoria di dati di diagnostica inseriti tooLog Analitica, è AzureBackupReport |
| Risorsa |Text |Si tratta di hello risorsa per cui sono stati raccolti i dati, verrà visualizzato nome insieme di credenziali di servizi di ripristino |
| ProtectedServerUniqueId_s |Text |Id univoco di hello protetto per cui viene calcolata l'archiviazione server |
| VaultUniqueId_s |Text |Id univoco dell'insieme di credenziali di hello per l'archiviazione viene calcolata |
| SourceSystem |Text |Sistema di origine di dati corrente hello - Azure |
| ResourceId |Text |Questo campo rappresenta l'id risorsa per cui sono stati raccolti i dati, verrà visualizzato l'id risorsa dell'insieme di credenziali dei servizi di ripristino |
| SubscriptionId |Text |Questo campo rappresenta l'id sottoscrizione di risorse hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceGroup |Text |Questo campo rappresenta il gruppo di risorse della risorsa hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceProvider |Text |Questo campo rappresenta hello provider di risorse per cui sono stati raccolti dati - Microsoft.RecoveryServices |
| ResourceType |Text |Questo representse campo tipo di risorsa hello per cui sono stati raccolti dati - insiemi di credenziali |

### <a name="vault"></a>Insiemi di credenziali
Questa tabella offre dettagli sui campi relativi all'insieme di credenziali.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| EventName_s |Text |Questo campo rappresenta il nome di questo evento, che è sempre AzureBackupCentralReport |
| SchemaVersion_s |Text |Questo campo indica la versione corrente dello schema di hello, è **V1** |
| State_s |Text |Stato corrente dell'oggetto insieme di credenziali hello, ad esempio, attivo, eliminati |
| OperationName |Text |Questo campo rappresenta nome dell'operazione corrente hello - insieme di credenziali |
| Categoria |Text |Questo campo rappresenta una categoria di dati di diagnostica inseriti tooLog Analitica, è AzureBackupReport |
| Risorsa |Text |Si tratta di hello risorsa per cui sono stati raccolti i dati, verrà visualizzato nome insieme di credenziali di servizi di ripristino |
| VaultUniqueId_s |Text |Id univoco dell'insieme di credenziali hello |
| VaultName_s |Text |Nome dell'insieme di credenziali hello |
| AzureDataCenter_s |Text |Data center in cui si trova l'insieme di credenziali |
| StorageReplicationType_s |Text |Tipo di replica di archiviazione per l'insieme di credenziali hello, ad esempio, GeoRedundant |
| SourceSystem |Text |Sistema di origine di dati corrente hello - Azure |
| ResourceId |Text |Questo campo rappresenta l'id risorsa per cui sono stati raccolti i dati, verrà visualizzato l'id risorsa dell'insieme di credenziali dei servizi di ripristino |
| SubscriptionId |Text |Questo campo rappresenta l'id sottoscrizione di risorse hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceGroup |Text |Questo campo rappresenta il gruppo di risorse della risorsa hello (insieme di credenziali RS) per il quale sono stati raccolti dati |
| ResourceProvider |Text |Questo campo rappresenta hello provider di risorse per cui sono stati raccolti dati - Microsoft.RecoveryServices |
| ResourceType |Text |Questo campo rappresenta tipo di risorsa hello per cui sono stati raccolti dati - insiemi di credenziali |

## <a name="next-steps"></a>Passaggi successivi
Dopo aver verificato il modello di dati hello per la creazione di rapporti di Backup di Azure, è possibile iniziare [la creazione di dashboard](../log-analytics/log-analytics-dashboards.md) in Log Analitica e OMS.
