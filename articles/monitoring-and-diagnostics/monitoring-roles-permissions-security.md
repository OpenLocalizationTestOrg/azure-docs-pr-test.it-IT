---
title: aaaGet avviato con i ruoli, autorizzazioni e sicurezza con Monitor di Azure | Documenti Microsoft
description: Informazioni su come ruoli predefiniti e autorizzazioni toorestrict toouse Azure monitoraggio accedere alle risorse di toomonitoring.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a>Introduzione a ruoli, autorizzazioni e sicurezza con il monitoraggio di Azure
Molti team necessario toostrictly regolare toomonitoring accedere ai dati e impostazioni. Ad esempio, se si dispongono di membri del team che lavorano esclusivamente sul monitoraggio (tecnici del supporto, i tecnici devops) o se si utilizza un provider del servizio gestito, è opportuno toogrant tooonly dati di monitoraggio limitando la possibilità toocreate loro l'accesso, modificare, o eliminare le risorse. Questo articolo illustra come tooquickly applicare un monitoraggio RBAC ruolo tooa utente incorporato in Azure o creare il proprio ruolo personalizzato per un utente che necessita di autorizzazioni limitate di monitoraggio. Quindi illustra le considerazioni sulla sicurezza per le risorse correlate al monitoraggio di Azure e come è possibile limitare l'accesso ai dati toohello contengono.

## <a name="built-in-monitoring-roles"></a>Ruoli di monitoraggio predefiniti
Ruoli predefiniti del monitoraggio di Azure sono progettate toohelp limite accesso tooresources in una sottoscrizione durante l'abilitazione di quelli ancora responsabili del monitoraggio dell'infrastruttura tooobtain e configurare dati hello che necessari. Il monitoraggio di Azure fornisce due ruoli predefiniti: un lettore di monitoraggio e un collaboratore al monitoraggio.

### <a name="monitoring-reader"></a>Lettore di monitoraggio
Persone assegnate il ruolo di lettore monitoraggio hello possono visualizzare tutti i dati di monitoraggio in una sottoscrizione, ma non è possibile modificare qualsiasi risorsa o modificare tutte le risorse correlate toomonitoring impostazioni. Questo ruolo è appropriato per gli utenti in un'organizzazione, ad esempio i tecnici del supporto o operazioni, che necessitano di toobe in grado di:

* Visualizzare i dashboard di monitoraggio nel portale di hello e creare i propri dashboard di monitoraggio privato.
* Query per le metriche utilizzando hello [API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931930.aspx), [i cmdlet di PowerShell](insights-powershell-samples.md), o [CLI multipiattaforma](insights-cli-samples.md).
* Query hello Log attività utilizzando portale hello, API REST di monitoraggio di Azure, i cmdlet di PowerShell o CLI multipiattaforma.
* Hello vista [le impostazioni di diagnostica](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) per una risorsa.
* Hello vista [log profilo](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) per una sottoscrizione.
* Visualizzare le impostazioni di scalabilità automatica.
* Visualizzare impostazioni e attività di avviso.
* Accedere ai dati di Application Insights e visualizzarli in AI Analytics.
* Cercare nei dati dell'area di lavoro Analitica Log (OMS) tra i dati di utilizzo per l'area di lavoro hello.
* Visualizzare i gruppi di gestione di Log Analytics (OMS).
* Recuperare lo schema di ricerca di hello Analitica Log (OMS).
* Elencare gli Intelligence Pack di Log Analytics (OMS).
* Recuperare ed eseguire le ricerche salvate di Log Analytics (OMS).
* Recuperare la configurazione di archiviazione di hello Analitica Log (OMS).

> [!NOTE]
> Questo ruolo non fornisce l'accesso in lettura i dati di toolog hub eventi tooan con flusso o memorizzati in un account di archiviazione. [Vedere di seguito](#security-considerations-for-monitoring-data) per informazioni sulla configurazione toothese di accedere alle risorse.
> 
> 

### <a name="monitoring-contributor"></a>Collaboratore al monitoraggio
Gli utenti assegnati hello collaboratore monitoraggio ruolo può visualizzare tutti i dati di monitoraggio in una sottoscrizione e creare o modificare le impostazioni di monitoraggio, ma non è possibile modificare tutte le altre risorse. Questo ruolo è un superset del ruolo di lettore monitoraggio hello ed è appropriato per i membri del team di monitoraggio o provider di servizi gestiti che, inoltre autorizzazioni toohello precedente, nonché toobe in grado di un'organizzazione:

* Pubblicare dashboard di monitoraggio come dashboard condivisi.
* Configurare le [impostazioni di diagnostica](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) per una risorsa.*
* Set hello [log profilo](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) per un subscription.*
* Configurare impostazioni e attività di avviso.
* Creare componenti e test Web di Application Insights.
* Elencare le chiavi condivise dell'area di lavoro di Log Analytics (OMS).
* Abilitare o disabilitare gli Intelligence Pack di Log Analytics (OMS).
* Creare ed eliminare poi eseguire le ricerche salvate di Log Analytics (OMS).
* Creare ed eliminare le configurazioni di archiviazione di hello Analitica Log (OMS).

* utente separatamente anche concedere elenco chiavi dell'autorizzazione per tooset risorse (archiviazione account o l'evento hub dello spazio dei nomi) di destinazione hello un profilo di log o impostazione diagnostica.

> [!NOTE]
> Questo ruolo non fornisce l'accesso in lettura i dati di toolog hub eventi tooan con flusso o memorizzati in un account di archiviazione. [Vedere di seguito](#security-considerations-for-monitoring-data) per informazioni sulla configurazione toothese di accedere alle risorse.
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a>Autorizzazioni per il monitoraggio e ruoli personalizzati nel Controllo degli accessi in base al ruolo
Se hello sopra ruoli predefiniti non soddisfa esigenze specifiche hello del team, è possibile [creare un ruolo RBAC personalizzato](../active-directory/role-based-access-control-custom-roles.md) con autorizzazioni più granulari. Di seguito è hello operazioni comuni di Azure monitoraggio RBAC con le relative descrizioni.

| Operazione | Descrizione |
| --- | --- |
| Microsoft.Insights/AlertRules/[Read, Write, Delete] |Regole di avviso di lettura, scrittura ed eliminazione. |
| Microsoft.Insights/AlertRules/Incidents/Read |Elenco eventi imprevisti (cronologia della regola di avviso hello venga attivata) per le regole di avviso. Si applica solo toohello portale. |
| Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete] |Impostazioni di scalabilità automatica di lettura, scrittura ed eliminazione. |
| Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete] |Impostazioni di diagnostica di lettura, scrittura ed eliminazione. |
| Microsoft.Insights/eventtypes/digestevents/Read |Questa autorizzazione è necessaria per gli utenti che devono accedere tooActivity log tramite il portale di hello. |
| Microsoft.Insights/eventtypes/values/Read |Elenco degli eventi dei registri attività (eventi di gestione) in una sottoscrizione. Questa autorizzazione è applicabile tooboth accesso a livello di codice e portale toohello Log attività. |
| Microsoft.Insights/LogDefinitions/Read |Questa autorizzazione è necessaria per gli utenti che devono accedere tooActivity log tramite il portale di hello. |
| Microsoft.Insights/MetricDefinitions/Read |Definizioni delle metriche (elenco dei tipi di metriche disponibili per una risorsa). |
| Microsoft.Insights/Metrics/Read |Metriche per una risorsa. |

> [!NOTE]
> Accedere a tooalerts, le impostazioni di diagnostica e le metriche per una risorsa, è necessario che l'utente hello è di tipo di risorsa toohello accesso in lettura e l'ambito di tale risorsa. Creazione ("scrittura"), un profilo di impostazione o di log diagnostico che gli archivi tooa storage account o flussi tooevent hub richiede hello utente tooalso dispone dell'autorizzazione di elenco chiavi sulla risorsa di destinazione hello.
> 
> 

Ad esempio, utilizzando hello sopra tabella è possibile creare un ruolo RBAC personalizzato per un "attività di lettura Log" simile al seguente:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a>Considerazioni sulla sicurezza per i dati sul monitoraggio
I dati sul monitoraggio dei dati, in particolare i file di registro, possono contenere informazioni sensibili, come indirizzi IP o nomi utente. I dati sul monitoraggio di Azure sono forniti in tre forme base:

1. Hello registro attività, che descrive tutte le azioni del piano di controllo nella sottoscrizione di Azure.
2. Registri di diagnostica, cioè registri generati da una risorsa.
3. Metriche, generate dalle risorse.

Tutte e tre questi tipi di dati possono essere archiviati in un account di archiviazione o trasmessi tooEvent Hub, entrambi i quali sono le risorse di Azure di uso generale. Poiché si tratta di risorse di scopo generico, la creazione, l'eliminazione e l'accesso sono operazioni privilegiate e generalmente riservate agli amministratori. Si consiglia di utilizzare hello consigliate per l'utilizzo improprio tooprevent relativi al monitoraggio delle risorse seguenti:

* Usare un account di archiviazione singolo e dedicato per il monitoraggio dei dati. Se è necessario tooseparate dati di monitoraggio in più account di archiviazione, non condividono mai l'utilizzo di un account di archiviazione tra il monitoraggio e dati sul monitoraggio, come si possono concedere inavvertitamente coloro che devono accedere solo ai dati toomonitoring (ad es. un SIEM di terze parti) accedere ai dati di monitoraggio toonon.
* Utilizzare nomi di hub eventi o Bus di servizio dedicato in tutte le impostazioni di diagnostica per hello stesso motivo sopra.
* Limitare gli account di accesso correlati toomonitoring archiviazione o hub eventi salvandole in un gruppo di risorse distinto, e [utilizzare ambito](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) nei ruoli monitoraggio toolimit accedere tooonly tale gruppo di risorse.
* Non concedere l'autorizzazione di elenco chiavi dell'hello per gli account di archiviazione o hub eventi nell'ambito di sottoscrizione quando un utente deve solo toomonitoring accedere ai dati. Ma è possibile ottenere questi toohello autorizzazioni degli utenti a una risorsa o un gruppo di risorse (se si dispone di un gruppo di risorse di monitoraggio dedicato) ambito.

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a>Account di archiviazione correlati toomonitoring limitazione accesso
Quando un utente o un'applicazione deve accedere a dati toomonitoring in un account di archiviazione, è necessario [generare una firma di accesso condiviso](https://msdn.microsoft.com/library/azure/mt584140.aspx) nell'account di archiviazione hello che contiene i dati di monitoraggio con l'archiviazione tooblob accesso in sola lettura a livello di servizio. In PowerShell, potrebbe avere un aspetto simile al seguente:

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

È quindi possibile assegnare entità toohello token hello necessarie tooread dall'account di archiviazione e può elencare e leggere tutti i BLOB nell'account di archiviazione.

In alternativa, se è necessario toocontrol questa autorizzazione con RBAC, è possibile concedere tale autorizzazione Microsoft.Storage/storageAccounts/listkeys/action per tale account di archiviazione specifico di hello entità. Ciò è necessario per gli utenti che necessitano di toobe in grado di tooset una diagnostica impostazione o log profilo tooarchive tooa account di archiviazione. Ad esempio, è possibile creare hello seguente ruolo RBAC personalizzato per un utente o applicazione che richiede solo tooread da un account di archiviazione:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> elenco chiavi dell'autorizzazione Hello consente chiavi dell'account di hello utente toolist hello archiviazione primaria e secondaria. Queste chiavi concedono hello tutti firmati autorizzazioni (lettura, scrittura, creare BLOB, eliminare i BLOB e così via) in tutti i servizi (blob, coda, tabella, file) in tale account di archiviazione firmato. Se possibile, si consiglia di usare una firma di accesso condiviso dell'account come descritto sopra.
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a>Hub di eventi correlati al toomonitoring limitazione accesso
Un modello simile può essere seguito con hub eventi, ma è necessario innanzitutto toocreate una regola di autorizzazione di ascolto dedicata. Se si desidera toogrant accesso tooan applicazione necessarie solo per gli hub di eventi correlati al toomonitoring toolisten, hello seguenti:

1. Creare un criterio di accesso condiviso in hub eventi resteranno hello che sono stati creati per il flusso di dati di monitoraggio con solo le attestazioni di attesa. Questa operazione può essere eseguita nel portale di hello. Ad esempio, è possibile chiamarlo "monitoringReadOnly". Se possibile, si desidererà toogive chiave direttamente toohello consumer e ignorare il passaggio successivo hello.
2. Se il consumer hello deve toobe tooget in grado di hello chiave ad hoc, concedere hello hello elenco chiavi dell'intervento per l'hub eventi. Questo è anche necessario per gli utenti che devono toobe in grado di tooset un'impostazione di diagnostica o di log hub tooevent toostream di profilo. Ad esempio, è possibile creare una regola nel Controllo degli accessi in base al ruolo:
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a>Passaggi successivi
* [Controllo degli accessi in base al ruolo e autorizzazioni in Resource Manager](../active-directory/role-based-access-control-what-is.md)
* [Panoramica di hello di monitoraggio in Azure](monitoring-overview.md)

