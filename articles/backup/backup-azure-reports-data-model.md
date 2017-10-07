---
title: modello aaaData per il Backup di Azure
description: Questo articolo illustra i dettagli del modello di dati di Power BI per i report di Backup di Azure.
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 0767c330-690d-474d-85a6-aa8ddc410bb2
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/26/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5e3e7ca13c7a3f007c206bd56b8753166a2c264b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-model-for-azure-backup-reports"></a>Modello di dati per i report di Backup di Azure
Questo articolo descrive modello di dati di Power BI hello usato per la creazione di report di Azure Backup. Utilizzando questo modello di dati, è possibile filtrare i report esistenti in base ai campi pertinenti e più importante, creare report personalizzati utilizzando le tabelle e campi nel modello di hello. 

## <a name="creating-new-reports-in-power-bi"></a>Creazione di nuovi report in Power BI
Power BI fornisce funzionalità di personalizzazione tramite il quale è possibile [creare report utilizzando il modello di dati hello](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/).

## <a name="using-azure-backup-data-model"></a>Uso del modello di dati di Backup di Azure
È possibile utilizzare i seguenti campi forniti come parte dei dati hello toocreate report del modello e personalizzare i report esistenti hello.

### <a name="alert"></a>Avviso
Questa tabella presenta i campi e le aggregazioni di base per diversi campi correlati agli avvisi.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| #AlertsCreatedInPeriod |Numero intero |Numero di avvisi creati nel periodo di tempo selezionato |
| %ActiveAlertsCreatedInPeriod |Percentuale |Percentuale di avvisi attivi nel periodo di tempo selezionato |
| %CriticalAlertsCreatedInPeriod |Percentuale |Percentuale di avvisi critici nel periodo di tempo selezionato |
| AlertOccurenceDate |Data |Data di creazione dell'avviso |
| AlertSeverity |Text |Gravità dell'avviso hello ad esempio, critico |
| AlertStatus |Text |Stato di avviso hello ad esempio, attivo |
| AlertType |Text |Tipo di avviso hello generato, ad esempio, Backup |
| AlertUniqueId |Text |Id univoco di hello ha generato l'avviso |
| AsOnDateTime |Data/ora |Ora per la riga selezionata hello di aggiornamento più recente |
| AvgResolutionTimeInMinsForAlertsCreatedInPeriod |Numero decimale |Avviso tooresolve tempo medio (in minuti) per il periodo di tempo selezionato |
| EntityState |Text |Stato corrente dell'oggetto di avviso hello ad esempio, attivo, eliminati |

### <a name="backup-item"></a>Elementi di backup
Questa tabella presenta i campi e le aggregazioni di base per diversi campi correlati agli elementi di backup.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| #BackupItems |Numero intero |Numero di elementi di backup |
| #UnprotectedBackupItems |Numero intero |Numero di elementi di backup arrestati per protezione o configurati per il backup, ma con backup non avviato|
| AsOnDateTime |Data/ora |Ora per la riga selezionata hello di aggiornamento più recente |
| BackupItemFriendlyName |Text |Nome descrittivo dell'elemento di backup |
| BackupItemId |Text |ID dell'elemento di backup |
| BackupItemName |Text |Nome dell'elemento di backup |
| BackupItemType |Text |Tipo dell'elemento di backup, ad esempio, VM o FileFolder |
| EntityState |Text |Stato corrente dell'oggetto di backup dell'elemento hello ad esempio, attivo, eliminati |
| LastBackupDateTime |Data/ora |Data e ora del backup più recente dell'elemento di backup selezionato |
| LastBackupState |Text |Stato del backup più recente dell'elemento di backup selezionato, ad esempio, Successful o Failed |
| LastSuccessfulBackupDateTime |Data/ora |Data e ora del backup più recente con esito positivo dell'elemento di backup selezionato |
| ProtectionState |Text |Stato di protezione corrente dell'elemento di backup hello ad esempio, Protected, ProtectionStopped |

### <a name="calendar"></a>Calendario
Questa tabella offre dettagli sui campi relativi al calendario.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| Data |Data |Data selezionata per il filtro dei dati |
| DateKey |Text |Chiave univoca per ogni elemento data |
| DayDiff |Numero decimale |Differenza relativa al giorno per il filtro dei dati. Ad esempio, 0 indica i dati del giorno corrente, -1 i dati del giorno precedente, 0 e -1 indicano i dati del giorno corrente e di quello precedente  |
| Mese |Text |Mese dell'anno hello selezionata per filtrare i dati, inizia il primo giorno mese e finisce 31 giorni |
| MonthDate | Date |Data fine mese, mese di hello selezionato per il filtro dei dati |
| MonthDiff |Numero decimale |Differenza relativa al mese per il filtro dei dati. Ad esempio, 0 indica i dati del mese corrente, -1 i dati del mese precedente, 0 e -1 indicano i dati del mese corrente e di quello precedente |
| Settimana |Text |Settimana selezionata come filtro dei dati. La settimana inizia la domenica e finisce il sabato |
| WeekDate |Date |Data di fine settimana, settimana di hello selezionato per il filtro dei dati |
| WeekDiff |Numero decimale |Differenza relativa alla settimana per il filtro dei dati. Ad esempio, 0 indica i dati della settimana corrente, -1 i dati della settimana precedente, 0 e -1 indicano i dati della settimana corrente e di quella precedente |
| Year |Text |Anno di calendario selezionato per il filtro dei dati |
| YearDate |Date |Data di fine anno, anno di hello selezionato per il filtro dei dati |

### <a name="job"></a>Job
Questa tabella presenta i campi e le aggregazioni di base per diversi campi correlati ai processi.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| #JobsCreatedInPeriod |Numero intero |Numero di processi creati in hello periodo di tempo selezionato |
| %FailuresForJobsCreatedInPeriod |Percentuale |Percentuale di errori nel periodo di tempo selezionato hello complessiva del processo |
| 80thPercentileDataTransferredInMBForBackupJobsCreatedInPeriod |Numero decimale |valore percentile 80 ° dei dati trasferiti in MB per **backup** i processi creati nella hello periodo di tempo selezionato |
| AsOnDateTime |Data/ora |Ora per la riga selezionata hello di aggiornamento più recente |
| AvgBackupDurationInMinsForJobsCreatedInPeriod |Numero decimale |Durata media espressa in minuti per i processi di **backup completati** creati nel periodo di tempo selezionato |
| AvgRestoreDurationInMinsForJobsCreatedInPeriod |Numero decimale |Durata media espressa in minuti per i processi di **ripristino completati** creati nel periodo di tempo selezionato |
| BackupStorageDestination |Text |Destinazione dell'archiviazione di backup, ad esempio, Cloud o Disk  |
| EntityState |Text |Stato corrente dell'oggetto processo hello ad esempio, attivo, eliminati |
| JobFailureCode |Text |Stringa di codice contenente un errore e a causa della quale si è verificato un errore del processo |
| JobOperation |Text |Operazione per la quale viene eseguito il processo, ad esempio Backup, Restore o Configure Backup |
| JobStartDate |Data |Data di avvio dell'esecuzione del processo |
| JobStartTime |Time |Ora di avvio dell'esecuzione del processo |
| Stato processo |Text |Stato di hello terminate processo, ad esempio, completato, non è riuscita |
| JobUniqueId |Text |Processo di hello tooidentify Id univoco |

### <a name="policy"></a>Criteri
Questa tabella presenta i campi e le aggregazioni di base per diversi campi correlati ai criteri.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| #Policies |Numero intero |Numero di criteri di backup presenti nel sistema hello |
| #PoliciesInUse |Numero intero |Numero di criteri attualmente in uso per la configurazione di backup |
| AsOnDateTime |Data/ora |Ora per la riga selezionata hello di aggiornamento più recente |
| BackupDaysOfTheWeek |Text |Giorni della settimana hello quando sono stati pianificati backup |
| BackupFrequency |Text |Frequenza con cui vengono eseguiti i backup, ad esempio, daily o weekly |
| BackupTimes |Text |Data e ora in cui sono pianificati backup |
| DailyRetentionDuration |Numero intero |Durata totale di mantenimento dati in giorni per i backup configurati |
| DailyRetentionTimes |Text |Data e ora di configurazione del mantenimento dati giornaliero |
| EntityState |Text |Stato corrente dell'oggetto Criteri di hello ad esempio, attivo, eliminati |
| MonthlyRetentionDaysOfTheMonth |Text |Date del mese hello selezionati per la conservazione mensile |
| MonthlyRetentionDaysOfTheWeek |Text |Giorni della settimana hello selezionato per la conservazione mensile |
| MonthlyRetentionDuration |Numero decimale |Durata totale di mantenimento dati in mesi per i backup configurati |
| MonthlyRetentionFormat |Text |Tipo di configurazione per il mantenimento dati mensile, ad esempio, daily per la configurazione basata sui giorni o weekly per la configurazione basata sulle settimane |
| MonthlyRetentionTimes |Text |Data e ora di configurazione del mantenimento dati mensile |
| MonthlyRetentionWeeksOfTheMonth |Text |Settimane del mese di hello quando conservazione mensile è configurato, ad esempio, primo, ultimo ecc. |
| PolicyName |Text |Nome del criterio hello definito |
| PolicyUniqueId |Text |Criterio di hello tooidentify Id univoco |
| RetentionType |Text |Tipo di criteri di mantenimento dati, ad esempio, Daily, Weekly, Monthly, Yearly |
| WeeklyRetentionDaysOfTheWeek |Text |Giorni della settimana hello selezionato per la conservazione settimanale |
| WeeklyRetentionDuration |Numero decimale |Durata totale del mantenimento dati settimanale in settimane per i backup configurati |
| WeeklyRetentionTimes |Text |Data e ora di configurazione del mantenimento dati settimanale |
| YearlyRetentionDaysOfTheMonth |Text |Date del mese hello selezionati per la conservazione annuale |
| YearlyRetentionDaysOfTheWeek |Text |Giorni della settimana hello selezionato per la conservazione annuale |
| YearlyRetentionDuration |Numero decimale |Durata totale di mantenimento dati in anni per i backup configurati |
| YearlyRetentionFormat |Text |Tipo di configurazione per il mantenimento dati annuale, ad esempio, daily per la configurazione basata sui giorni o weekly per la configurazione basata sulle settimane |
| YearlyRetentionMonthsOfTheYear |Text |Mesi dell'anno di hello selezionato per la conservazione annuale |
| YearlyRetentionTimes |Text |Data e ora di configurazione del mantenimento dati annuale |
| YearlyRetentionWeeksOfTheMonth |Text |Settimane del mese di hello quando conservazione annuale è configurato, ad esempio, primo, ultimo ecc. |

### <a name="protected-server"></a>Server protetti
Questa tabella presenta i campi e le aggregazioni di base per diversi campi correlati ai server protetti.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| #ProtectedServers |Numero intero |Numero di server protetti |
| AsOnDateTime |Data/ora |Ora per la riga selezionata hello di aggiornamento più recente |
| AzureBackupAgentOSType |Text |Tipo del sistema operativo dell'agente di Backup di Azure |
| AzureBackupAgentOSVersion |Text |Versione del sistema operativo dell'agente di Backup di Azure |
| AzureBackupAgentUpdateDate |Text |Data di aggiornamento dell'agente di Backup di Azure |
| AzureBackupAgentVersion |Text |Numero di versione dell'agente di Backup di Azure |
| BackupManagementType |Text |Tipo di provider per l'esecuzione del backup, ad esempio, IaaSVM o FileFolder |
| EntityState |Text |Stato corrente dell'oggetto server protetto hello ad esempio, attivo, eliminati |
| ProtectedServerFriendlyName |Text |Nome descrittivo del server protetto |
| ProtectedServerName |Text |Nome del server protetto |
| ProtectedServerType |Text |Tipo del server protetto di cui si esegue il backup, ad esempio, IaaSVMContainer |
| ProtectedServerName |Text |Nome del server protetto toowhich backup dell'elemento appartiene |
| RegisteredContainerId |Text |ID del contenitore registrato per il backup |

### <a name="storage"></a>Archiviazione
Questa tabella presenta i campi e le aggregazioni di base per diversi campi correlati all'archiviazione.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| #ProtectedInstances |Numero decimale |Numero di istanze protette usato per il calcolo dell'archiviazione front-end a scopo di fatturazione, calcolato in base al valore più recente nel periodo selezionato |
| AsOnDateTime |Data/ora |Ora per la riga selezionata hello di aggiornamento più recente |
| CloudStorageInMB |Numero decimale |Spazio di archiviazione nel cloud usato dal backup, calcolato in base al valore più recente nel periodo selezionato |
| EntityState |Text |Stato corrente dell'oggetto hello ad esempio, attivo, eliminati |
| LastUpdatedDate |Data |Data dell'aggiornamento più recente della riga selezionata |

### <a name="time"></a>Time
Questa tabella offre dettagli sui campi relativi al tempo.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| Hour |Tempo |Ora del giorno hello, ad esempio 1:00:00 PM |
| HourNumber |Numero decimale |Numero di ore nel giorno hello 13.00, ad esempio, |
| Minuto |Numero decimale |Minuti dell'ora hello |
| PeriodOfTheDay |Text |Periodo tempo giorno hello, ad esempio, 12-3 AM |
| Tempo |Tempo |Ora del giorno hello, ad esempio, 12:00:01 AM |
| TimeKey |Text |Tempo toorepresent valore della chiave |

### <a name="vault"></a>Insiemi di credenziali
Questa tabella presenta i campi e le aggregazioni di base per diversi campi correlati agli insiemi di credenziali.

| Campo | Tipo di dati | Descrizione |
| --- | --- | --- |
| #Vaults |Numero intero |Numero di insiemi di credenziali |
| AsOnDateTime |Data/ora |Ora per la riga selezionata hello di aggiornamento più recente |
| AzureDataCenter |Text |Data center in cui si trova l'insieme di credenziali |
| EntityState |Text |Stato corrente dell'oggetto insieme di credenziali hello ad esempio, attivo, eliminati |
| StorageReplicationType |Text |Tipo di replica di archiviazione per l'insieme di credenziali di hello GeoRedundant, ad esempio, |
| SubscriptionId |Text |Id sottoscrizione del cliente hello selezionato per la generazione di report |
| VaultName |Text |Nome dell'insieme di credenziali hello |
| VaultTags |Text |Insieme di credenziali associate toohello tag |

## <a name="next-steps"></a>Passaggi successivi
Dopo aver verificato il modello di dati hello per la creazione di report di Azure Backup, fare riferimento hello seguenti articoli per ulteriori informazioni sulla creazione e visualizzazione di report in Power BI.

* [Creazione dei report in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)
* [Applicazione di filtri ai report in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
