---
title: aaaActions e NotActions - Azure basata sui ruoli (RBAC) di controllo degli accessi | Documenti Microsoft
description: Questo argomento descrive hello compilato nei ruoli per il controllo di accesso basato sui ruoli (RBAC). Hello i ruoli vengono continuamente aggiunti, in questo controllo hello documentazione aggiornamento.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: 
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/28/2017
ms.author: andredm
ms.reviewer: 
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a4ef9923fe05ec38e968534951911eaa4440b88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="built-in-roles-for-azure-role-based-access-control"></a>Ruoli predefiniti per il controllo degli accessi in base al ruolo di Azure
Azure Role-Based Access controllo (RBAC) viene fornito con hello seguenti ruoli predefiniti che possono essere assegnati toousers, gruppi e i servizi. È possibile modificare le definizioni di hello dei ruoli predefiniti. Tuttavia, è possibile creare [ruoli personalizzati in Azure RBAC](role-based-access-control-custom-roles.md) toofit hello specifiche esigenze aziendali.

## <a name="roles-in-azure"></a>Ruoli in Azure
Hello nella tabella seguente vengono fornite brevi descrizioni di hello ruoli predefiniti. Fare clic su hello ruolo nome toosee hello elenco dettagliato dei **azioni** e **notactions** per ruolo hello. Hello **azioni** proprietà specifica hello azioni consentita sulle risorse di Azure. Nelle stringhe delle azioni è possibile utilizzare caratteri jolly. Hello **notactions** proprietà specifica le azioni di hello che sono esclusi dalla hello azioni consentita.

azione di Hello definisce il tipo di operazioni è possibile eseguire su un tipo di risorsa specificata. ad esempio:
- **Scrivere** Abilita si tooperform PUT, POST, PATCH e le operazioni di eliminazione.
- **Lettura** consente le operazioni GET tooperform.

Questo articolo illustra solo i ruoli diversi hello attualmente esistenti. Quando si assegna un utente tooa ruolo, tuttavia, è possibile limitare hello consentita ulteriori azioni mediante la definizione di un ambito. Ciò risulta utile se un utente desidera toomake un collaboratore del sito Web, ma solo per un gruppo di risorse.

> [!NOTE]
> le definizioni di ruolo di Azure Hello sono in continua evoluzione. In questo articolo è conservato come backup toodate possibile, ma è sempre possibile individuare hello delle definizioni più recenti di ruoli in Azure PowerShell. Hello utilizzare [Get AzureRmRoleDefinition](/powershell/module/azurerm.resources/get-azurermroledefinition) toolist cmdlet tutti i ruoli correnti. È possibile iniziare utilizzando un ruolo specifico tooa `(get-azurermroledefinition "<role name>").actions` o `(get-azurermroledefinition "<role name>").notactions` come applicabile. Utilizzare [Get AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) operazioni toolist di provider di risorse di Azure specifico.


| Nome del ruolo | Descrizione |
| --- | --- |
| [Collaboratore servizio Gestione API](#api-management-service-contributor) |Può gestire il servizio Gestione API e hello API |
| [Ruolo operatore del servizio Gestione API](#api-management-service-operator-role) | Gestire il servizio Gestione API, ma non hello API stesse |
| [Ruolo lettura del servizio Gestione API](#api-management-service-reader-role) | Il servizio di gestione di accesso in sola lettura tooAPI e API |
| [Collaboratore componente di Application Insights](#application-insights-component-contributor) |È in grado di gestire i componenti di Application Insights |
| [Operatore di automazione](#automation-operator) |In grado di toostart, arrestare, sospendere e riprendere i processi |
| [Collaboratore di backup](#backup-contributor) | Consente di gestire il backup nell'insieme di credenziali dei Servizi di ripristino |
| [Operatore di backup](#backup-operator) | Consente di gestire il backup, ad eccezione della rimozione del backup, nell'insieme di credenziali dei Servizi di ripristino |
| [Lettore di backup](#backup-reader) | Consente di visualizzare tutti i servizi di gestione di backup  |
| [Lettore per la fatturazione](#billing-reader) | Consente di visualizzare tutte le informazioni di fatturazione  |
| [Collaboratore BizTalk](#biztalk-contributor) |È in grado di gestire i servizi BizTalk |
| [Collaboratore database ClearDB MySQL](#cleardb-mysql-db-contributor) |È in grado di gestire i database ClearDB MySQL |
| [Collaboratore](#contributor) |È in grado di gestire tutto ad eccezione degli accessi. |
| [Collaboratore Data Factory](#data-factory-contributor) |Può creare e gestire data factory e le relative risorse figlio. |
| [Utente DevTest Labs](#devtest-labs-user) |Può visualizzare tutti gli elementi e connettere, avviare, riavviare e arrestare macchine virtuali |
| [Collaboratore zona DNS](#dns-zone-contributor) |È in grado di gestire zone e record DNS |
| [Collaboratore per l'account Azure Cosmos DB](#documentdb-account-contributor) |È in grado di gestire account Azure Cosmos DB |
| [Collaboratore account Intelligent Systems](#intelligent-systems-account-contributor) |È in grado di gestire account Intelligent Systems |
| Collaboratore alle app per la logica | Può gestire tutti gli aspetti di un'app per la logica, ma non crearne una nuova. |
| Operatore delle app per la logica |Può avviare e arrestare i flussi di lavoro definiti all'interno di un'app per la logica. |
| [Lettore di monitoraggio](#monitoring-reader) |Può leggere tutti i dati del monitoraggio |
| [Collaboratore al monitoraggio](#monitoring-contributor) |Può leggere i dati del monitoraggio e modificare le impostazioni di monitoraggio |
| [Collaboratore di rete](#network-contributor) |È in grado di gestire tutte le risorse di rete |
| [Collaboratore account New Relic APM](#new-relic-apm-account-contributor) |Può gestire account e applicazioni di New Relic Application Performance Management |
| [Proprietario](#owner) |È in grado di gestire tutti gli elementi, compresi gli accessi |
| [Lettore](#reader) |È in grado di visualizzare tutti gli elementi, ma non può apportare modifiche |
| [Collaboratore cache Redis](#redis-cache-contributor) |È in grado di gestire le cache Redis |
| [Collaboratore raccolte di processi dell'unità di pianificazione](#scheduler-job-collections-contributor) |È in grado di gestire raccolte di processi dell'utilità di pianificazione |
| [Collaboratore servizi di ricerca](#search-service-contributor) |È in grado di gestire servizi di ricerca |
| [Gestore della sicurezza SQL](#security-manager) |Può gestire i componenti di protezione, i criteri di sicurezza e le macchine virtuali |
| [Collaboratore al ripristino sito](#site-recovery-contributor) | Consente di gestire il ripristino del sito nell'insieme di credenziali dei servizi di ripristino |
| [Operatore del ripristino sito](#site-recovery-operator) | Può gestire operazioni failover e failback di ripristino del sito nell'insieme di credenziali di servizi di ripristino |
| [Reader di ripristino sito](#site-recovery-reader) | Può visualizzare tutte le operazioni di gestione di ripristino del sito  |
| [Collaboratore database SQL](#sql-db-contributor) |Può gestire i database SQL, ma non i criteri correlati alla sicurezza |
| [Gestione della sicurezza SQL](#sql-security-manager) |Possibile gestire i criteri di sicurezza hello di SQL Server e database |
| [Collaboratore SQL Server](#sql-server-contributor) |È in grado di gestire server e database SQL, ma non i criteri di sicurezza correlati |
| [Collaboratore account di archiviazione classico](#classic-storage-account-contributor) |È in grado di gestire gli account di archiviazione classici |
| [Collaboratore account di archiviazione](#storage-account-contributor) |È in grado di gestire gli account di archiviazione |
| [Collaboratore alla richiesta di supporto](#support-request-contributor) | Può creare e gestire le richieste di supporto |
| [Amministratore accessi utente](#user-access-administrator) |Possono gestire le risorse tooAzure di accesso utente |
| [Collaboratore macchine virtuali classiche](#classic-virtual-machine-contributor) |Gestire macchine virtuali classiche, ma non una rete virtuale hello o toowhich di account di archiviazione che sono connessi |
| [Collaboratore macchine virtuali](#virtual-machine-contributor) |Gestire macchine virtuali, ma non hello virtuale rete o archiviazione account toowhich che sono connessi |
| [Collaboratore reti virtuali classiche](#classic-network-contributor) |È in grado di gestire reti virtuali classiche e IP riservati |
| [Collaboratore piani Web](#web-plan-contributor) |È in grado di gestire piani Web |
| [Collaboratore siti Web](#website-contributor) |Può gestire i siti Web, ma non hello web piani toowhich sono connessi |

## <a name="role-permissions"></a>Autorizzazioni ruoli
Hello nelle tabelle seguenti vengono descritti autorizzazioni specifiche di hello tooeach ruolo specificate. Può trattarsi di proprietà **Actions**, che concedono le autorizzazioni, e **NotActions**, che le limitano.

### <a name="api-management-service-contributor"></a>Collaboratore servizio Gestione API
È in grado di gestire i servizi Gestione API

| **Actions** |  |
| --- | --- |
| Microsoft.ApiManagement/Service/* |È in grado di creare e gestire il servizio Gestione API |
| Microsoft.Authorization/*/read |Autorizzazione Lettura |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="api-management-service-operator-role"></a>Ruolo operatore del servizio Gestione API
È in grado di gestire i servizi Gestione API

| **Actions** |  |
| --- | --- |
| Microsoft.ApiManagement/Service/*/read | Leggere le istanze del servizio Gestione API |
| Microsoft.ApiManagement/Service/backup/action | Eseguire il backup di contenitore specificato toohello di servizio Gestione API, un utente specificato l'account di archiviazione |
| Microsoft.ApiManagement/Service/delete | Eliminare un'istanza del servizio Gestione API |
| Microsoft.ApiManagement/Service/managedeployments/action | Modificare gli SKU/le unità; aggiungere o rimuovere distribuzioni regionali del servizio Gestione API |
| Microsoft.ApiManagement/Service/read | Leggere i metadati per un'istanza del servizio Gestione API |
| Microsoft.ApiManagement/Service/restore/action | Ripristinare il servizio Gestione API dal contenitore specificato di hello nell'account di archiviazione dall'utente |
| Microsoft.ApiManagement/Service/updatehostname/action | Configurare, aggiornare o rimuovere i nomi di dominio personalizzati per un servizio Gestione API |
| Microsoft.ApiManagement/Service/write | Creare una nuova istanza del servizio Gestione API |
| Microsoft.Authorization/*/read |Autorizzazione Lettura |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="api-management-service-reader-role"></a>Ruolo lettura del servizio Gestione API
È in grado di gestire i servizi Gestione API

| **Actions** |  |
| --- | --- |
| Microsoft.ApiManagement/Service/*/read | Leggere le istanze del servizio Gestione API |
| Microsoft.ApiManagement/Service/read | Leggere i metadati per un'istanza del servizio Gestione API |
| Microsoft.Authorization/*/read |Autorizzazione Lettura |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="application-insights-component-contributor"></a>Collaboratore componente di Application Insights
È in grado di gestire i componenti di Application Insights

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.Insights/components/* |È in grado di creare e gestire i componenti di Insights |
| Microsoft.Insights/webtests/* |È in grado di creare e gestire i test Web |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="automation-operator"></a>Operatore di automazione
In grado di toostart, arrestare, sospendere e riprendere i processi

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Automation/automationAccounts/jobs/read |Leggere processi di account di automazione |
| Microsoft.Automation/automationAccounts/jobs/resume/action |Riprendere un processo di account di automazione |
| Microsoft.Automation/automationAccounts/jobs/stop/action |Arrestare un processo di account di automazione |
| Microsoft.Automation/automationAccounts/jobs/streams/read |Leggere flussi di processi di account di automazione |
| Microsoft.Automation/automationAccounts/jobs/suspend/action |Sospendere un processo di account di automazione |
| Microsoft.Automation/automationAccounts/jobs/write |Scrivere processi di account di automazione |
| Microsoft.Automation/automationAccounts/jobSchedules/read |Leggere una pianificazione di processo di account di automazione |
| Microsoft.Automation/automationAccounts/jobSchedules/write |Leggere una pianificazione di processo di account di automazione |
| Microsoft.Automation/automationAccounts/read |Leggere account di automazione |
| Microsoft.Automation/automationAccounts/runbooks/read |Leggere runbook di automazione |
| Microsoft.Automation/automationAccounts/schedules/read |Leggere pianificazioni di account di automazione |
| Microsoft.Automation/automationAccounts/schedules/write |Scrivere pianificazioni di account di automazione |
| Microsoft.Insights/components/* |È in grado di creare e gestire i componenti di Insights |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="backup-contributor"></a>Collaboratore di backup
Possibile gestire tutte le azioni di gestione dei backup, ad eccezione di creazione dell'insieme di credenziali di servizi di ripristino e fornendo accesso tooothers

| **Actions** | |
| --- | --- |
| Microsoft.Network/virtualNetworks/read | Leggere reti virtuali |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/* | Consente di gestire i risultati dell'operazione sulla gestione del backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/* | Consente di creare e gestire i contenitori di backup all'interno delle infrastrutture di backup dell'insieme di credenziali dei Servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/backupJobs/* | Consente di creare e gestire i processi di backup |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | Consente di esportare i processi di backup in un file Excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/* | Creare e gestire i metadati relativi ai dati toobackup gestione |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/* | Consente di creare e gestire i risultati delle operazioni di gestione di backup |
| Microsoft.RecoveryServices/Vaults/backupPolicies/* | Consente di creare e gestire i criteri di backup |
| Microsoft.RecoveryServices/Vaults/backupProtectableItems/* | Consente di creare e gestire gli elementi su cui è possibile eseguire il backup |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/* | Consente di creare e gestire gli elementi su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/* | Consente di creare e gestire i contenitori che contengono gli elementi di backup |
| Microsoft.RecoveryServices/Vaults/certificates/* | Creare e gestire i certificati toobackup correlati nell'insieme di credenziali di servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/extendedInformation/* | Creare e gestire informazioni estese relative toovault |
| Microsoft.RecoveryServices/Vaults/read | Consente di leggere l'insieme di credenziali dei servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/refreshContainers/* | Consente di gestire le operazioni di individuazione per il recupero dei nuovi contenitori creati |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/* | Consente di creare e gestire le identità registrate |
| Microsoft.RecoveryServices/Vaults/usages/* | Consente di creare e gestire l'uso dell'insieme di credenziali dei Servizi di ripristino |
| Microsoft.Resources/deployments/* | Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read | Leggere gruppi di risorse |
| Microsoft.Storage/storageAccounts/read | Leggere account di archiviazione |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="backup-operator"></a>Operatore di backup
Possibile gestire tutte le azioni di gestione dei backup, ad eccezione di creazione di insiemi di credenziali, la rimozione di backup e fornendo accesso tooothers

| **Actions** | |
| --- | --- |
| Microsoft.Network/virtualNetworks/read | Leggere reti virtuali |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/read | Consente di leggere i risultati dell'operazione nella gestione dei backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/operationResults/read | Consente di leggere i risultati di un'operazione di lettura nei contenitori di protezione |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/backup/action | Consente di eseguire l'operazione di backup su richiesta su un elemento su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationResults/read | Consente di leggere il risultato dell'operazione eseguita su un elemento su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationStatus/read | Consente di leggere l'operazione eseguita su un elemento su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read | Consente di leggere gli elementi su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/recoveryPoints/read | Consente di leggere il punto di ripristino di un elemento su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/recoveryPoints/restore/action | Consente di eseguire un'operazione di ripristino usando un punto di ripristino di un elemento su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/write | Consente di creare un elemento di backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/read | Consente di leggere i contenitori che contengono l'elemento di backup |
| Microsoft.RecoveryServices/Vaults/backupJobs/* | Consente di creare e gestire i processi di backup |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | Consente di esportare i processi di backup in un file Excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/read | Lettura dei metadati relativi a gestione toobackup |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/* | Consente di creare e gestire i risultati delle operazioni di gestione di backup |
| Microsoft.RecoveryServices/Vaults/backupPolicies/operationResults/read | Consente di leggere i risultati delle operazioni eseguite sui criteri di backup |
| Microsoft.RecoveryServices/Vaults/backupPolicies/read | Consente di leggere i criteri di backup |
| Microsoft.RecoveryServices/Vaults/backupProtectableItems/* | Consente di creare e gestire gli elementi su cui è possibile eseguire il backup |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/read | Consente di leggere gli elementi su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/read | Consente di leggere i contenitori su cui è stato eseguito il backup che contengono gli elementi di backup |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read | Informazioni sulla lettura estesi correlati toovault |
| Microsoft.RecoveryServices/Vaults/extendedInformation/write | Informazioni sulla scrittura estesi correlati toovault |
| Microsoft.RecoveryServices/Vaults/read | Consente di leggere l'insieme di credenziali dei servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/refreshContainers/* | Consente di gestire le operazioni di individuazione per il recupero dei nuovi contenitori creati |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read | Lettura dei risultati dell'operazione eseguita sugli elementi registrato dell'insieme di credenziali hello |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read | Lettura registrati gli elementi dell'insieme di credenziali hello |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/write | Scrivere toovault elementi registrati |
| Microsoft.RecoveryServices/Vaults/usages/read | Leggere l'utilizzo di hello che insieme di credenziali di servizi di ripristino |
| Microsoft.Resources/deployments/* | Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read | Leggere gruppi di risorse |
| Microsoft.Storage/storageAccounts/read | Leggere account di archiviazione |
| Microsoft.Support/* | Creare e gestire ticket di supporto |

### <a name="backup-reader"></a>Lettore di backup
Consente di monitorare la gestione di backup nell'insieme di credenziali dei Servizi di ripristino

| **Actions** | |
| --- | --- |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/read  | Consente di leggere i risultati dell'operazione nella gestione dei backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/operationResults/read  | Consente di leggere i risultati di un'operazione di lettura nei contenitori di protezione |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationResults/read  | Consente di leggere il risultato dell'operazione eseguita su un elemento su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationStatus/read  | Consente di leggere l'operazione eseguita su un elemento su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read  | Consente di leggere gli elementi su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/read  | Consente di leggere i contenitori che contengono l'elemento di backup |
| Microsoft.RecoveryServices/Vaults/backupJobs/operationResults/read  | Consente di leggere i risultati dei processi di backup |
| Microsoft.RecoveryServices/Vaults/backupJobs/read  | Consente di leggere i processi di backup |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | Consente di esportare i processi di backup in un file Excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/read  | Lettura dei metadati relativi a gestione toobackup |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/read  | Consente di leggere i risultati dell'operazione di gestione di backup |
| Microsoft.RecoveryServices/Vaults/backupPolicies/operationResults/read  | Consente di leggere i risultati delle operazioni eseguite sui criteri di backup |
| Microsoft.RecoveryServices/Vaults/backupPolicies/read  | Consente di leggere i criteri di backup |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/read  |  Consente di leggere gli elementi su cui è stato eseguito il backup |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/read  | Consente di leggere i contenitori su cui è stato eseguito il backup che contengono gli elementi di backup |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read  | Informazioni sulla lettura estesi correlati toovault |
| Microsoft.RecoveryServices/Vaults/read  | Consente di leggere l'insieme di credenziali dei servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read  | Consente di leggere i risultati delle operazioni di individuazione per il recupero dei nuovi contenitori creati |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read  | Lettura dei risultati dell'operazione eseguita sugli elementi registrato dell'insieme di credenziali hello |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read  | Lettura registrati gli elementi dell'insieme di credenziali hello |
| Microsoft.RecoveryServices/Vaults/usages/read  |  Leggere l'utilizzo di hello che insieme di credenziali di servizi di ripristino |

### <a name="billing-reader"></a>Lettore per la fatturazione
Consente di visualizzare tutte le informazioni di fatturazione

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Billing/*/read |Lettura delle informazioni di fatturazione |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="biztalk-contributor"></a>Collaboratore BizTalk
È in grado di gestire i servizi BizTalk

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.BizTalkServices/BizTalk/* |È in grado di creare e gestire i servizi BizTalk |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="cleardb-mysql-db-contributor"></a>Collaboratore database ClearDB MySQL
È in grado di gestire i database ClearDB MySQL

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |
| successbricks.cleardb/databases/* |È in grado di creare e gestire i database ClearDB MySQL |

### <a name="contributor"></a>Collaboratore
Può gestire tutto ad eccezione degli accessi.

| **Actions** |  |
| --- | --- |
| * |È in grado di creare e gestire ogni tipo di risorsa |

| **NotActions** |  |
| --- | --- |
| Microsoft.Authorization/*/Delete |Non può eliminare ruoli e assegnazioni di ruoli |
| Microsoft.Authorization/*/Write |Non può creare ruoli e assegnazioni di ruoli |

### <a name="data-factory-contributor"></a>Collaboratore Data Factory
Creare e gestire data factory e le relative risorse figlio.

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.DataFactory/dataFactories/* |Creare e gestire data factory e le relative risorse figlio. |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="devtest-labs-user"></a>Utente DevTest Labs
Può visualizzare tutti gli elementi e connettere, avviare, riavviare e arrestare macchine virtuali

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Compute/availabilitySets/read |Leggere le proprietà di hello del set di disponibilità |
| Microsoft.Compute/virtualMachines/*/read |Leggere le proprietà di hello di una macchina virtuale (dimensioni di macchina virtuale, lo stato di runtime, le estensioni VM e così via) |
| Microsoft.Compute/virtualMachines/deallocate/action |Deallocare macchine virtuali |
| Microsoft.Compute/virtualMachines/read |Leggere le proprietà di hello di una macchina virtuale |
| Microsoft.Compute/virtualMachines/restart/action |Ottenere macchine virtuali |
| Microsoft.Compute/virtualMachines/start/action |Avviare macchine virtuali |
| Microsoft.DevTestLab/*/read |Leggere le proprietà di hello di un lab |
| Microsoft.DevTestLab/labs/createEnvironment/action |Creare un ambiente lab |
| Microsoft.DevTestLab/labs/formulas/delete |Eliminare le formule |
| Microsoft.DevTestLab/labs/formulas/read |Leggere le formule |
| Microsoft.DevTestLab/labs/formulas/write |Aggiunge o modifica le formule |
| Microsoft.DevTestLab/labs/policySets/evaluatePolicies/action |Valutare i criteri lab |
| Microsoft.Network/loadBalancers/backendAddressPools/join/action |Aggiungere un pool di indirizzi back-end di bilanciamento del carico |
| Microsoft.Network/loadBalancers/inboundNatRules/join/action |Aggiungere una regola NAT di bilanciamento del carico in entrata |
| Microsoft.Network/networkInterfaces/*/read |Leggere le proprietà di hello un'interfaccia di rete (ad esempio, tutti i servizi di bilanciamento del carico di hello interfaccia di rete hello è una parte di) |
| Microsoft.Network/networkInterfaces/join/action |Aggiungere un'interfaccia di rete di macchina virtuale tooa |
| Microsoft.Network/networkInterfaces/read |Leggere le interfacce di rete |
| Microsoft.Network/networkInterfaces/write |Scrivere interfacce di rete |
| Microsoft.Network/publicIPAddresses/*/read |Leggere le proprietà di hello di un indirizzo IP pubblico |
| Microsoft.Network/publicIPAddresses/join/action |Aggiungere un indirizzo IP pubblico |
| Microsoft.Network/publicIPAddresses/read |Leggere indirizzi IP pubblici di rete |
| Microsoft.Network/virtualNetworks/subnets/join/action |Aggiungere una rete virtuale |
| Microsoft.Resources/deployments/operations/read |Leggere le operazioni di distribuzione |
| Microsoft.Resources/deployments/read |Leggere le distribuzioni |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Storage/storageAccounts/listKeys/action |Ottenere chiavi degli account di archiviazione |

### <a name="dns-zone-contributor"></a>Collaboratore zona DNS
È in grado di gestire zone e record DNS.

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/\*/lettura |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Insights/alertRules/\* |Creare e gestire regole di avviso |
| Microsoft.Network/dnsZones/\* |Creazione e gestione di zone e record DNS |
| Microsoft.ResourceHealth/availabilityStatuses/read |Lettura hello integrità delle risorse hello |
| Microsoft.Resources/deployments/\* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/\* |Creare e gestire ticket di supporto |

### <a name="azure-cosmos-db-account-contributor"></a>Collaboratore per l'account Azure Cosmos DB
È in grado di gestire account Azure Cosmos DB

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.DocumentDb/databaseAccounts/* |Creare e gestire account DocumentDB |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="intelligent-systems-account-contributor"></a>Collaboratore account Intelligent Systems
È in grado di gestire account Intelligent Systems

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.IntelligentSystems/accounts/* |Creare e gestire account di Intelligent Systems |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="monitoring-reader"></a>Lettore di monitoraggio
Può leggere tutti i dati del monitoraggio (metriche, log e così via). Vedere anche [Introduzione a ruoli, autorizzazioni e sicurezza con il monitoraggio di Azure](/monitoring-and-diagnostics/monitoring-roles-permissions-security.md#built-in-monitoring-roles).

| **Actions** |  |
| --- | --- |
| */lettura |Legge risorse di tutti i tipi, eccetto i segreti. |
| Microsoft.OperationalInsights/workspaces/search/action |Ricerca di dati in Log Analytics |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="monitoring-contributor"></a>Collaboratore al monitoraggio
Può leggere tutti i dati del monitoraggio e modificare le impostazioni di monitoraggio. Vedere anche [Introduzione a ruoli, autorizzazioni e sicurezza con il monitoraggio di Azure](/monitoring-and-diagnostics/monitoring-roles-permissions-security.md#built-in-monitoring-roles).

| **Actions** |  |
| --- | --- |
| */lettura |Legge risorse di tutti i tipi, eccetto i segreti. |
| Microsoft.Insights/AlertRules/* |Regole di avviso di lettura, scrittura ed eliminazione. |
| Microsoft.Insights/components/* |Leggere, scrivere ed eliminare componenti di Application Insights. |
| Microsoft.Insights/DiagnosticSettings/* |Impostazioni di diagnostica di lettura, scrittura ed eliminazione. |
| Microsoft.Insights/eventtypes/* |Elenco degli eventi dei registri attività (eventi di gestione) in una sottoscrizione. Questa autorizzazione è applicabile tooboth accesso a livello di codice e portale toohello Log attività. |
| Microsoft.Insights/LogDefinitions/* |Questa autorizzazione è necessaria per gli utenti che devono accedere tooActivity log tramite il portale di hello. Elencare categorie di log nel log attività. |
| Microsoft.Insights/MetricDefinitions/* |Definizioni delle metriche (elenco dei tipi di metriche disponibili per una risorsa). |
| Microsoft.Insights/Metrics/* |Metriche per una risorsa. |
| Microsoft.Insights/Register/Action |Registrare il provider di Insights hello. |
| Microsoft.Insights/webtests/* |Leggere, scrivere ed eliminare test Web di Application Insights. |
| Microsoft.OperationalInsights/workspaces/intelligencepacks/* |Leggere, scrivere ed eliminare pacchetti di soluzioni Log Analytics. |
| Microsoft.OperationalInsights/workspaces/savedSearches/* |Leggere, scrivere ed eliminare ricerche salvate di Log Analytics. |
| Microsoft.OperationalInsights/workspaces/search/action |Cercare aree di lavoro di Log Analytics. |
| Microsoft.OperationalInsights/workspaces/sharedKeys/action |Elencare chiavi per un'area di lavoro di Log Analytics. |
| Microsoft.OperationalInsights/workspaces/storageinsightconfigs/* |Leggere, scrivere ed eliminare configurazione di dati di archiviazione di Log Analytics. |

### <a name="network-contributor"></a>Collaboratore di rete
È in grado di gestire tutte le risorse di rete

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.Network/* |Creare e gestire reti |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="new-relic-apm-account-contributor"></a>Collaboratore account New Relic APM
Può gestire account e applicazioni di New Relic Application Performance Management

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |
| NewRelic.APM/accounts/* |Creare e gestire account di gestione delle prestazioni delle applicazioni New Relic |

### <a name="owner"></a>Proprietario
È in grado di gestire tutti gli elementi, compresi gli accessi

| **Actions** |  |
| --- | --- |
| * |È in grado di creare e gestire ogni tipo di risorsa |

### <a name="reader"></a>Lettore
È in grado di visualizzare tutti gli elementi, ma non può apportare modifiche

| **Actions** |  |
| --- | --- |
| */lettura |Legge risorse di tutti i tipi, eccetto i segreti. |

### <a name="redis-cache-contributor"></a>Collaboratore cache Redis
È in grado di gestire le cache Redis

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Cache/redis/* |Creare e gestire cache Redis |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="scheduler-job-collections-contributor"></a>Collaboratore raccolte di processi dell'unità di pianificazione
È in grado di gestire raccolte di processi dell'utilità di pianificazione

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Scheduler/jobcollections/* |Creare e gestire raccolte di processi |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="search-service-contributor"></a>Collaboratore servizi di ricerca
È in grado di gestire servizi di ricerca

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Search/searchServices/* |È in grado di creare e gestire servizi di ricerca |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="security-manager"></a>Gestore della sicurezza SQL
Può gestire i componenti di protezione, i criteri di sicurezza e le macchine virtuali

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.ClassicCompute/*/read |Leggere le informazioni di configurazione delle macchine virtuali di calcolo classiche |
| Microsoft.ClassicCompute/virtualMachines/*/write |Scrivere la configurazione delle macchine virtuali |
| Microsoft.ClassicNetwork/*/read |Leggere le informazioni della configurazione sulla rete classica |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Security/* |Creare e gestire criteri e componenti di protezione |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="site-recovery-contributor"></a>Collaboratore al ripristino sito
Possibile gestire tutte le azioni di gestione di Site Recovery, ad eccezione di creazione dell'insieme di credenziali di servizi di ripristino e l'assegnazione di utenti tooother diritti di accesso

| **Actions** | |
| --- | --- |
| Microsoft.Authorization/*/read | Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Insights/alertRules/* | Creare e gestire regole di avviso |
| Microsoft.Network/virtualNetworks/read | Leggere reti virtuali |
| Microsoft.RecoveryServices/Vaults/certificates/write | Certificato della credenziale dell'insieme di credenziali di aggiornamenti hello |
| Microsoft.RecoveryServices/Vaults/extendedInformation/* | Creare e gestire informazioni estese relative toovault |
| Microsoft.RecoveryServices/Vaults/monitoringAlerts/*  | Lettura degli avvisi per l'insieme di credenziali di hello Recovery services |
| Microsoft.RecoveryServices/Vaults/monitoringConfigurations/ notificationConfiguration/read  | Consente di leggere la configurazione delle notifiche dell'insieme di credenziali dei servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/read | Consente di leggere l'insieme di credenziali dei servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read | Consente di gestire le operazioni di individuazione per il recupero dei nuovi contenitori creati |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/* | Consente di creare e gestire le identità registrate |
| Microsoft.RecoveryServices/vaults/replicationAlertSettings/* | Consente di creare o aggiornare le impostazioni degli avvisi di replica |
| Microsoft.RecoveryServices/vaults/replicationEvents/read | Consente di leggere gli eventi di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/* | Consente di creare e gestire le infrastrutture di replica |
| Microsoft.RecoveryServices/vaults/replicationJobs/* | Consente di creare e gestire i processi di replica |
| Microsoft.RecoveryServices/vaults/replicationPolicies/* | Consente di creare e gestire i criteri di replica |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/* | Consente di creare e gestire i piani di ripristino |
| Microsoft.RecoveryServices/Vaults/storageConfig/* | Consente di creare e gestire la configurazione di archiviazione dell'insieme di credenziali di Servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/tokenInfo/read | Consente di leggere le informazioni relative al token dell'insieme di credenziali di Servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/usages/read | Consente di leggere i dettagli di utilizzo di un insieme di credenziali di Servizi di ripristino |
| Microsoft.ResourceHealth/availabilityStatuses/read | Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* | Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read | Leggere gruppi di risorse |
| Microsoft.Storage/storageAccounts/read | Leggere account di archiviazione |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="site-recovery-operator"></a>Operatore del ripristino sito
Failover e Failback ma può Impossibile eseguire altre azioni di gestione del ripristino del sito o assegnare l'accesso agli utenti di tooother

| **Actions** | |
| --- | --- |
| Microsoft.Authorization/*/read | Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Insights/alertRules/* | Creare e gestire regole di avviso |
| Microsoft.Network/virtualNetworks/read | Leggere reti virtuali |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read | Informazioni sulla lettura estesi correlati toovault |
| Microsoft.RecoveryServices/Vaults/monitoringAlerts/*  | Lettura degli avvisi per l'insieme di credenziali di hello Recovery services |
| Microsoft.RecoveryServices/Vaults/monitoringConfigurations/ notificationConfiguration/read  | Consente di leggere la configurazione delle notifiche dell'insieme di credenziali dei servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/read | Consente di leggere l'insieme di credenziali dei servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read | Consente di gestire le operazioni di individuazione per il recupero dei nuovi contenitori creati |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read | Consente di leggere lo stato e il risultato di un'operazione inviata |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read | Consente di leggere i contenitori registrati per una risorsa |
| Microsoft.RecoveryServices/vaults/replicationAlertSettings/read | Consente di leggere le impostazioni degli avvisi di replica |
| Microsoft.RecoveryServices/vaults/replicationEvents/read | Consente di leggere gli eventi di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/checkConsistency/action | Verificare la coerenza di infrastrutture hello |
| Microsoft.RecoveryServices/vaults/replicationFabrics/read | Consente di leggere le infrastrutture di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ reassociateGateway/action | Consente di riassociare un gateway di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/renewcertificate/action | Consente di rinnovare il certificato dell'infrastruttura di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationNetworks/read | Consente di leggere le reti delle infrastrutture di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationNetworks/replicationNetworkMappings/read | Consente di leggere il mapping delle reti delle infrastrutture di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/read | Consente di leggere i contenitori di protezione |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectableItems/read | Restituisce l'elenco di tutti gli elementi da proteggere |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ applyRecoveryPoint/action | Consente di applicare un punto di recupero specifico |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ failoverCommit/action | Consente di eseguire il commit del failover per un elemento sottoposto a failover |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ plannedFailover/action | Consente di avviare un failover pianificato per un elemento protetto |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/read | Restituisce l'elenco di tutti gli elementi protetti |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/recoveryPoints/read | Consente di ottenere l'elenco di punti di recupero disponibili |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ repairReplication/action | Consente di ripristinare la replica di un elemento protetto |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/reProtect/action | Consente di avviare nuovamente la protezione per un elemento protetto|
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/testFailover/action | Consente di avviare il failover di test di un elemento protetto |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ testFailoverCleanup/action | Consente di avviare la pulizia di un failover di test |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ unplannedFailover/action | Consente di avviare il failover non pianificato di un elemento protetto |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ updateMobilityService/action | Aggiornare il servizio mobility hello |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectionContainerMappings/read | Consente di leggere i mapping dei contenitori di protezione |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationRecoveryServicesProviders/read | Consente di leggere tutti i provider dei servizi di ripristino |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationRecoveryServicesProviders/refreshProvider/action | Consente di aggiornare tutti i provider dei servizi di ripristino |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/read | Consente di configurare classificazioni di archiviazione per le infrastrutture di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/replicationStorageClassificationMappings/read | Consente di leggere tutti i mapping di classificazioni di archiviazione |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationvCenters/read | Consente di leggere le informazioni registrate di vCenter |
| Microsoft.RecoveryServices/vaults/replicationJobs/* | Consente di creare e gestire i processi di replica |
| Microsoft.RecoveryServices/vaults/replicationPolicies/read | Consente di leggere i criteri di replica |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ failoverCommit/action | Consente di eseguire il commit di failover per il failover del piano di ripristino |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ plannedFailover/action | Consente di avviare il failover di un piano di ripristino |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/read | Consente di leggere i piani di ripristino |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/reProtect/action | Consente di iniziare a proteggere nuovamente un piano di ripristino |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/testFailover/action | Consente di avviare il failover di test di un piano di ripristino |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ testFailoverCleanup/action | Consente di avviare la pulizia di un failover di test del piano di ripristino |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ unplannedFailover/action | Consente di avviare il failover non pianificato di un piano di ripristino |
| Microsoft.RecoveryServices/Vaults/storageConfig/read | Consente di leggere la configurazione di archiviazione di un insieme di credenziali di Servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/tokenInfo/read | Consente di leggere le informazioni relative al token dell'insieme di credenziali di Servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/usages/read | Consente di leggere i dettagli di utilizzo di un insieme di credenziali di Servizi di ripristino |
| Microsoft.ResourceHealth/availabilityStatuses/read | Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* | Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read | Leggere gruppi di risorse |
| Microsoft.Storage/storageAccounts/read | Leggere account di archiviazione |
| Microsoft.Support/* | Creare e gestire ticket di supporto |

### <a name="site-recovery-reader"></a>Reader di ripristino sito
Può monitorare lo stato di ripristino del sito nell'insieme di credenziali di servizi di ripristino e generare i ticket di supporto

| **Actions** | |
| --- | --- |
| Microsoft.Authorization/*/read | Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read  | Informazioni sulla lettura estesi correlati toovault |
| Microsoft.RecoveryServices/Vaults/monitoringAlerts/read  | Lettura degli avvisi per l'insieme di credenziali di hello Recovery services |
| Microsoft.RecoveryServices/Vaults/monitoringConfigurations/ notificationConfiguration/read  | Consente di leggere la configurazione delle notifiche dell'insieme di credenziali dei servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/read  | Consente di leggere l'insieme di credenziali dei servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read  | Consente di gestire le operazioni di individuazione per il recupero dei nuovi contenitori creati |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read  | Consente di leggere lo stato e il risultato di un'operazione inviata |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read  | Consente di leggere i contenitori registrati per una risorsa |
| Microsoft.RecoveryServices/vaults/replicationAlertSettings/read | Consente di leggere le impostazioni degli avvisi di replica |
| Microsoft.RecoveryServices/vaults/replicationEvents/read  | Consente di leggere gli eventi di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/read  | Consente di leggere le infrastrutture di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationNetworks/read  | Consente di leggere le reti delle infrastrutture di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationNetworks/replicationNetworkMappings/read  | Consente di leggere il mapping delle reti delle infrastrutture di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/read  |  Consente di leggere i contenitori di protezione |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectableItems/read  | Restituisce l'elenco di tutti gli elementi da proteggere |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/read  | Restituisce l'elenco di tutti gli elementi protetti |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/recoveryPoints/read  | Consente di ottenere l'elenco di punti di recupero disponibili |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectionContainerMappings/read  | Consente di leggere i mapping dei contenitori di protezione |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationRecoveryServicesProviders/read  | Consente di leggere tutti i provider dei servizi di ripristino |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/read  | Consente di configurare classificazioni di archiviazione per le infrastrutture di replica |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/replicationStorageClassificationMappings/read  |  Consente di leggere tutti i mapping di classificazioni di archiviazione |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationvCenters/read  |  Consente di leggere le informazioni registrate di vCenter |
| Microsoft.RecoveryServices/vaults/replicationJobs/read  |  Consente di leggere lo stato dei processi di replica |
| Microsoft.RecoveryServices/vaults/replicationPolicies/read  |  Consente di leggere i criteri di replica |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/read  |  Consente di leggere i piani di ripristino |
| Microsoft.RecoveryServices/Vaults/storageConfig/read  |  Consente di leggere la configurazione di archiviazione di un insieme di credenziali di Servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/tokenInfo/read  |  Consente di leggere le informazioni relative al token dell'insieme di credenziali di Servizi di ripristino |
| Microsoft.RecoveryServices/Vaults/usages/read  |  Consente di leggere i dettagli di utilizzo di un insieme di credenziali di Servizi di ripristino |
| Microsoft.Support/*  |  Creare e gestire ticket di supporto |

### <a name="sql-db-contributor"></a>Collaboratore database SQL
Può gestire i database SQL, ma non i criteri correlati alla sicurezza

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere i ruoli e le assegnazioni di ruoli |
| Microsoft.Insights/alertRules/* |Creare e gestire regole di avviso |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Sql/servers/databases/* |Creare e gestire database SQL |
| Microsoft.Sql/servers/read |È in grado di leggere i server SQL |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

| **NotActions** |  |
| --- | --- |
| Microsoft.Sql/servers/databases/auditingPolicies/* |Impossibile modificare i criteri di controllo |
| Microsoft.Sql/servers/databases/auditingSettings/* |Impossibile modificare le impostazioni di controllo |
| Microsoft.Sql/servers/databases/auditRecords/read |Non può leggere i record di controllo |
| Microsoft.Sql/servers/databases/connectionPolicies/* |Impossibile modificare i criteri di connessione |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |Impossibile modificare i criteri di mascheratura dei dati |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |Impossibile modificare i criteri di avviso di sicurezza |
| Microsoft.Sql/servers/databases/securityMetrics/* |Impossibile modificare i criteri di protezione |

### <a name="sql-security-manager"></a>Gestione della sicurezza SQL
Possibile gestire i criteri di sicurezza hello di SQL Server e database

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere l'autorizzazione Microsoft |
| Microsoft.Insights/alertRules/* |Creare e gestire le regole di avviso di Insight |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Sql/servers/auditingPolicies/* |Creare e gestire criteri di controllo di server SQL |
| Microsoft.Sql/servers/auditingSettings/* |Creare e gestire le impostazioni di controllo di SQL Server |
| Microsoft.Sql/servers/databases/auditingPolicies/* |Creare e gestire i criteri di controllo dei database SQL |
| Microsoft.Sql/servers/databases/auditingSettings/* |Creare e gestire le impostazioni di controllo dei database di SQL Server |
| Microsoft.Sql/servers/databases/auditRecords/read |Legge i record di controllo |
| Microsoft.Sql/servers/databases/connectionPolicies/* |Creare e gestire i criteri di connessione dei database dei server SQL |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |Creare e gestire i criteri della maschera dei dati dei database dei server SQL |
| Microsoft.Sql/servers/databases/read |Leggere database SQL |
| Microsoft.Sql/servers/databases/schemas/read |Leggere schemi di database di lettura di server SQL |
| Microsoft.Sql/servers/databases/schemas/tables/columns/read |Leggere colonne della tabella del database di server SQL |
| Microsoft.Sql/servers/databases/schemas/tables/read |Leggere tabelle di database di server SQL |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |Creare e gestire i criteri degli avvisi di sicurezza dei database di SQL Server |
| Microsoft.Sql/servers/databases/securityMetrics/* |Creare e gestire le metriche di sicurezza dei database di server SQL |
| Microsoft.Sql/servers/read |È in grado di leggere i server SQL |
| Microsoft.Sql/servers/securityAlertPolicies/* |Creare e gestire i criteri degli avvisi di sicurezza di SQL Server |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="sql-server-contributor"></a>Collaboratore SQL Server
Può gestire server e database SQL, ma non i criteri di protezione correlati

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Autorizzazione Lettura |
| Microsoft.Insights/alertRules/* |Creare e gestire le regole di avviso di Insight |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Sql/servers/* |Creare e gestire server SQL |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

| **NotActions** |  |
| --- | --- |
| Microsoft.Sql/servers/auditingPolicies/* |Non è in grado di modificare i criteri di controllo di server SQL |
| Microsoft.Sql/servers/auditingSettings/* |Non è in grado di modificare le impostazioni di controllo di SQL Server |
| Microsoft.Sql/servers/databases/auditingPolicies/* |Non è in grado di modificare i criteri di controllo dei database di server SQL |
| Microsoft.Sql/servers/databases/auditingSettings/* |Non è in grado di modificare le impostazioni di controllo dei database di SQL Server |
| Microsoft.Sql/servers/databases/auditRecords/read |Non può leggere i record di controllo |
| Microsoft.Sql/servers/databases/connectionPolicies/* |Non è in grado di modificare i criteri di connessione dei database di server SQL |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |Non è in grado di modificare i criteri di mascheratura dei dati dei database di server SQL |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |Non è in grado di modificare i criteri degli avvisi di sicurezza dei database di SQL server |
| Microsoft.Sql/servers/databases/securityMetrics/* |Non è in grado di modificare le metriche di protezione dei database di server SQL |
| Microsoft.Sql/servers/securityAlertPolicies/* |Non è in grado di modificare i criteri degli avvisi di sicurezza di SQL Server |

### <a name="classic-storage-account-contributor"></a>Collaboratore account di archiviazione classico
È in grado di gestire gli account di archiviazione classici

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Autorizzazione Lettura |
| Microsoft.ClassicStorage/storageAccounts/* |Creare e gestire account di archiviazione |
| Microsoft.Insights/alertRules/* |Creare e gestire le regole di avviso di Insight |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="storage-account-contributor"></a>Collaboratore account di archiviazione
Può gestire gli account di archiviazione, ma non accedere toothem.

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Leggere tutte le autorizzazioni |
| Microsoft.Insights/alertRules/* |Creare e gestire le regole di avviso di Insight |
| Microsoft.Insights/diagnosticSettings/* |Gestire le impostazioni di diagnostica |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Storage/storageAccounts/* |Creare e gestire account di archiviazione |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="support-request-contributor"></a>Collaboratore alla richiesta di supporto
Creare e gestire i ticket di supporto nell'ambito di sottoscrizione hello

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read | Autorizzazione Lettura |
| Microsoft.Support/* | Creare e gestire ticket di supporto |
| Microsoft.Resources/subscriptions/resourceGroups/read | Leggere i ruoli e le assegnazioni di ruoli |

### <a name="user-access-administrator"></a>Amministratore accessi utente
Possono gestire le risorse tooAzure di accesso utente

| **Actions** |  |
| --- | --- |
| */lettura |Legge risorse di tutti i tipi, eccetto i segreti. |
| Microsoft.Authorization/* |Gestire l'autorizzazione |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="classic-virtual-machine-contributor"></a>Collaboratore macchine virtuali classiche
Gestire macchine virtuali classiche, ma non una rete virtuale hello o toowhich di account di archiviazione che sono connessi

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Autorizzazione Lettura |
| Microsoft.ClassicCompute/domainNames/* |Creare e gestire nomi di dominio di calcolo classici |
| Microsoft.ClassicCompute/virtualMachines/* |Creare e gestire macchine virtuali |
| Microsoft.ClassicNetwork/networkSecurityGroups/join/action |Partecipare a gruppi di sicurezza di rete |
| Microsoft.ClassicNetwork/reservedIps/link/action |Collegare IP riservati |
| Microsoft.ClassicNetwork/reservedIps/read |Leggere indirizzi IP riservati |
| Microsoft.ClassicNetwork/virtualNetworks/join/action |Partecipare a reti virtuali |
| Microsoft.ClassicNetwork/virtualNetworks/read |Leggere reti virtuali |
| Microsoft.ClassicStorage/storageAccounts/disks/read |Leggere dischi di account di archiviazione |
| Microsoft.ClassicStorage/storageAccounts/images/read |Leggere immagini di account di archiviazione |
| Microsoft.ClassicStorage/storageAccounts/listKeys/action |Ottenere chiavi degli account di archiviazione |
| Microsoft.ClassicStorage/storageAccounts/read |Leggere account di archiviazione classici |
| Microsoft.Insights/alertRules/* |Creare e gestire le regole di avviso di Insight |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="virtual-machine-contributor"></a>Collaboratore macchine virtuali
Gestire le macchine virtuali ma non hello virtuale rete o archiviazione account toowhich che sono connessi

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Autorizzazione Lettura |
| Microsoft.Compute/availabilitySets/* |Creare e gestire set di disponibilità di calcolo |
| Microsoft.Compute/locations/* |Creare e gestire percorsi di calcolo |
| Microsoft.Compute/virtualMachines/* |Creare e gestire macchine virtuali |
| Microsoft.Compute/virtualMachineScaleSets/* |Creare e gestire i set di scalabilità delle macchine virtuali |
| Microsoft.Insights/alertRules/* |Creare e gestire le regole di avviso di Insight |
| Microsoft.Network/applicationGateways/backendAddressPools/join/action |Partecipare a pool di indirizzi backend di gateway delle applicazioni di rete |
| Microsoft.Network/loadBalancers/backendAddressPools/join/action |Partecipare a pool di indirizzi backend di servizi di bilanciamento del carico |
| Microsoft.Network/loadBalancers/inboundNatPools/join/action |Aggiungere pool NAT di bilanciamento del carico in entrata |
| Microsoft.Network/loadBalancers/inboundNatRules/join/action |Partecipa a regole NAT in entrata di servizi di bilanciamento del carico |
| Microsoft.Network/loadBalancers/read |Leggere servizi di bilanciamento del carico |
| Microsoft.Network/locations/* |Creare e gestire percorsi di rete |
| Microsoft.Network/networkInterfaces/* |Creare e gestire interfacce di rete |
| Microsoft.Network/networkSecurityGroups/join/action |Partecipare a gruppi di sicurezza di rete |
| Microsoft.Network/networkSecurityGroups/read |Leggere gruppi di sicurezza di rete |
| Microsoft.Network/publicIPAddresses/join/action |Partecipare a indirizzi IP pubblici di rete |
| Microsoft.Network/publicIPAddresses/read |Leggere indirizzi IP pubblici di rete |
| Microsoft.Network/virtualNetworks/read |Leggere reti virtuali |
| Microsoft.Network/virtualNetworks/subnets/join/action |Partecipare a subnet di reti virtuali |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Storage/storageAccounts/listKeys/action |Ottenere chiavi degli account di archiviazione |
| Microsoft.Storage/storageAccounts/read |Leggere account di archiviazione |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="classic-network-contributor"></a>Collaboratore reti virtuali classiche
È in grado di gestire reti virtuali classiche e IP riservati

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Autorizzazione Lettura |
| Microsoft.ClassicNetwork/* |Creare e gestire reti classiche |
| Microsoft.Insights/alertRules/* |Creare e gestire le regole di avviso di Insight |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |

### <a name="web-plan-contributor"></a>Collaboratore piani Web
È in grado di gestire piani Web

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Autorizzazione Lettura |
| Microsoft.Insights/alertRules/* |Creare e gestire le regole di avviso di Insight |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |
| Microsoft.Web/serverFarms/* |Creare e gestire server farm |

### <a name="website-contributor"></a>Collaboratore siti Web
Può gestire i siti Web ma non hello web piani toowhich sono connessi

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Autorizzazione Lettura |
| Microsoft.Insights/alertRules/* |Creare e gestire le regole di avviso di Insight |
| Microsoft.Insights/components/* |È in grado di creare e gestire i componenti di Insights |
| Microsoft.ResourceHealth/availabilityStatuses/read |Leggere l'integrità delle risorse hello |
| Microsoft.Resources/deployments/* |Creare e gestire distribuzioni di gruppi di risorse |
| Microsoft.Resources/subscriptions/resourceGroups/read |Leggere gruppi di risorse |
| Microsoft.Support/* |Creare e gestire ticket di supporto |
| Microsoft.Web/certificates/* |Creare e gestire certificati dei siti Web |
| Microsoft.Web/listSitesAssignedToHostName/read |Lettura siti assegnato il nome host tooa |
| Microsoft.Web/serverFarms/join/action |Partecipare a server farm |
| Microsoft.Web/serverFarms/read |Leggere server farm |
| Microsoft.Web/sites/* |Creare e gestire siti Web (creazione del sito è necessario toohello le autorizzazioni di scrittura associato il piano di servizio App) |

## <a name="see-also"></a>Vedere anche
* [Controllo di accesso basato sui ruoli](role-based-access-control-configure.md): Introduzione a RBAC in hello portale di Azure.
* [Ruoli personalizzati in Azure RBAC](role-based-access-control-custom-roles.md): informazioni su come toocreate ruoli personalizzati toofit le esigenze di accesso.
* [Creare un report della cronologia delle modifiche relative all'accesso](role-based-access-control-access-change-history-report.md): monitoraggio delle modifiche nelle assegnazioni dei ruoli nel controllo degli accessi in base al ruolo.
* [Risoluzione dei problemi del controllo degli accessi in base al ruolo](role-based-access-control-troubleshooting.md): suggerimenti per la risoluzione di problemi comuni.
