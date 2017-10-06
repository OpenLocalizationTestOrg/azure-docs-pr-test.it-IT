---
title: aaaOverview dei log di diagnostica di Azure | Documenti Microsoft
description: "Informazioni su quali sono i log di diagnostica Azure e come è possibile usarli toounderstand eventi che si verificano all'interno di una risorsa di Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>Raccogliere e usare i dati dei log dalle risorse di Azure

## <a name="what-are-azure-resource-diagnostic-logs"></a>Definizione di log di diagnostica di risorse di Azure
**I log di diagnostica a livello di risorse Azure** sono registri generati da una risorsa che forniscono dati completo e frequenti sull'operazione di hello di tale risorsa. contenuto Hello di questi log varia in base al tipo di risorsa. I contatori delle regole di gruppo di sicurezza di rete e i controlli di insieme di credenziali delle chiavi, ad esempio, sono due categorie di log di risorsa.

I log di diagnostica a livello di risorse diversi da hello [Log attività](monitoring-overview-activity-logs.md). Log attività Hello fornisce informazioni approfondite operazioni hello eseguite sulle risorse nella sottoscrizione tramite Gestione risorse, ad esempio, la creazione di una macchina virtuale o l'eliminazione di un'app di logica. Log attività Hello è un log a livello di sottoscrizione. I log di diagnostica a livello di risorsa includono informazioni sulle operazioni eseguite all'interno della risorsa stessa, ad esempio, il recupero di un segreto da un insieme di credenziali delle chiavi.

I log di diagnostica a livello di risorsa differiscono anche dal log di diagnostica a livello del sistema operativo guest. I log di diagnostica del sistema operativo guest vengono compilati da un agente in esecuzione all'interno di una macchina virtuale o di un altro tipo di risorsa supportato. I log di diagnostica a livello di risorsa è richiesto alcun agente e acquisire dati specifici delle risorse da hello piattaforma Azure stesso, i log di diagnostica a livello del sistema operativo guest acquisiscono i dati dal sistema operativo hello e applicazioni in esecuzione in una macchina virtuale.

Non tutte le risorse supportano hello nuovo tipo di log di diagnostica risorse descritte di seguito. Questo articolo contiene un elenco di sezione, quali tipi di risorse supportano hello nuovi a livello di risorsa log di diagnostica.

![Log di diagnostica di risorsa e altri tipi di log ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>Possibili operazioni con i log di diagnostica a livello di risorsa
Ecco alcune delle operazioni di hello che è possibile eseguire con i log di diagnostica di risorse:

![Posizionamento logico dei log di diagnostica di risorsa](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* Salvarli tooa [ **Account di archiviazione** ](monitoring-archive-diagnostic-logs.md) per un controllo di controllo o manuale. È possibile specificare hello memorizzazione tempo (in giorni) utilizzando **le impostazioni di diagnostica di risorse**.
* [Trasmessi troppo**hub eventi** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) per l'inserimento di un servizio di terze parti o di una soluzione analitica personalizzato, ad esempio Power BI.
* Analizzarli con [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)

È possibile utilizzare un account di archiviazione o dello spazio dei nomi degli hub di eventi che non si trova in hello stessa sottoscrizione come hello una creazione di log. utente di Hello che configura l'impostazione di hello deve disporre di sottoscrizioni di hello appropriate RBAC accesso tooboth.

## <a name="resource-diagnostic-settings"></a>Impostazioni di diagnostica di risorsa
I log di diagnostica per le non di calcolo vengono configurati tramite le impostazioni di diagnostica di risorsa. Le **impostazioni di diagnostica di risorsa** permettono di controllare quanto segue:

* Destinazione dei log di diagnostica di risorsa e delle metriche, ad esempio un account di archiviazione, un Hub eventi e/o OMS Log Analytics.
* Categorie di log e metriche da inviare.
* Periodo di tempo in cui ogni log di categoria deve essere mantenuto nell'account di archiviazione
    - Un periodo di conservazione di zero giorni significa che i log vengono conservati all'infinito. In caso contrario, il valore di hello può essere qualsiasi numero di giorni compreso tra 1 e 2147483647.
    - Se i criteri di conservazione sono impostati, ma l'archiviazione dei log in un Account di archiviazione è disabilitata (ad esempio, se solo le opzioni di hub eventi o OMS sono selezionate), i criteri di conservazione hello non hanno alcun effetto.
    - Criteri di conservazione vengono applicati al giorno, vengono eliminati in modo a hello fine di un giorno (UTC), i log da giorno hello che si trova ora oltre i criteri di conservazione hello. Ad esempio, se si dispone di un criterio di conservazione di un giorno, all'inizio di hello del giorno hello oggi hello registri hello ieri dovrebbero essere eliminati.

Queste impostazioni vengono configurate facilmente tramite impostazioni di diagnostica per una risorsa nel portale di Azure hello hello, tramite i comandi di PowerShell di Azure e CLI o hello [API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931943.aspx).

> [!WARNING]
> I log di diagnostica e le metriche per dal livello di sistema operativo guest hello calcolo (ad esempio, le macchine virtuali o Service Fabric) sull'utilizzo delle risorse [un meccanismo separato per la selezione di output e di configurazione](../azure-diagnostics.md).
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a>Come tooenable raccolta dei log di diagnostica di risorse
Raccolta dei log di diagnostica di risorse può essere abilitata [durante la creazione di una risorsa in un modello di gestione risorse di](./monitoring-enable-diagnostic-logs-using-template.md) o dopo la creazione di una risorsa dalla pagina della risorsa nel portale di hello. È anche possibile abilitare insieme in qualsiasi momento mediante i comandi di Azure PowerShell o l'interfaccia CLI o hello API REST di monitoraggio di Azure.

> [!TIP]
> Queste istruzioni potrebbero non essere applicabili direttamente tooevery risorse. Vedere i collegamenti dello schema hello nella parte inferiore di hello di questa pagina toounderstand speciali i passaggi che possono applicare i tipi di risorsa toocertain.
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a>Abilitare la raccolta dei log di diagnostica di risorsa nel portale di hello
È possibile abilitare una raccolta di log di diagnostica di risorsa nel hello Azure portal dopo aver creata una risorsa da passare di risorsa specifico tooa o passando tooAzure Monitor. tooenable questo tramite il monitoraggio di Azure:

1. In hello [portale di Azure](http://portal.azure.com)passare tooAzure Monitor e fare clic su **le impostazioni di diagnostica**

    ![Sezione relativa al monitoraggio di Monitoraggio di Azure](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. Se lo si desidera filtrare l'elenco hello in base al tipo di risorsa o gruppo di risorse, fare clic sul risorse hello per il quale si desidera tooset un'impostazione di diagnostica.

3. Se nessuna impostazione esistano nella risorsa hello selezionata, verrà richiesta toocreate un'impostazione. Fare clic su "Attiva diagnostica".

   ![Aggiungi impostazione di diagnostica - Nessuna impostazione esistente](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   Se sono presenti le impostazioni esistenti sulla risorsa hello, vedrai un elenco di impostazioni già configurato per questa risorsa. Fare clic su "Add diagnostic setting" (Aggiungi impostazione di diagnostica).

   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. Assegnare un nome dell'impostazione, hello caselle di controllo per ogni toowhich destinazione desideri toosend dati e configurare la risorsa viene utilizzato per ogni destinazione. Facoltativamente, impostare il numero di giorni tooretain questi log tramite hello **conservazione (giorni)** cursori (solo toohello applicabile account destinazione di archiviazione). La riserva di zero giorni registri hello vengono archiviati per un periodo illimitato.
   
   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Fare clic su **Salva**.

Dopo alcuni istanti, hello nuova impostazione è visualizzata nell'elenco delle impostazioni per questa risorsa e i log di diagnostica vengono inviati toohello specificato destinazioni appena nuovi dati di evento viene generati.

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>Abilitare la raccolta dei log di diagnostica di risorsa con PowerShell
raccolta di tooenable dei log di diagnostica di risorse tramite Azure PowerShell, hello di utilizzare i comandi seguenti:

tooenable archiviazione dei log di diagnostica in un account di archiviazione, usare questo comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

archiviazione Hello ID dell'account è hello ID di risorsa per i registri hello toowhich di account di archiviazione desiderato toosend hello.

tooenable lo streaming di hub di eventi di log di diagnostica tooan, usare questo comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

ID regola bus di servizio Hello è una stringa con questo formato: `{Service Bus resource ID}/authorizationrules/{key name}`.

tooenable l'invio di log di diagnostica tooa Log Analitica dell'area di lavoro, usare questo comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

È possibile ottenere l'ID di risorsa hello dell'area di lavoro Log Analitica utilizzando hello comando seguente:

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

È possibile combinare queste tooenable parametri più opzioni di output.

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a>Abilitare la raccolta dei log di diagnostica di risorsa con l'interfaccia della riga di comando
raccolta tooenable dei log di diagnostica di risorse tramite hello CLI di Azure, utilizzare hello seguenti comandi:

tooenable archiviazione dei log di diagnostica in un Account di archiviazione, usare questo comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

archiviazione Hello ID dell'account è hello ID di risorsa per i registri hello toowhich di account di archiviazione desiderato toosend hello.

tooenable lo streaming di hub di eventi di log di diagnostica tooan, usare questo comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

ID regola bus di servizio Hello è una stringa con questo formato: `{Service Bus resource ID}/authorizationrules/{key name}`.

tooenable l'invio di log di diagnostica tooa Log Analitica dell'area di lavoro, usare questo comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

È possibile combinare queste tooenable parametri più opzioni di output.

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>Abilitare la raccolta dei log di diagnostica di risorsa con l'API REST
le impostazioni di diagnostica toochange utilizzando hello API REST di monitoraggio di Azure, vedere [questo documento](https://msdn.microsoft.com/library/azure/dn931931.aspx).

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a>Gestire le impostazioni di diagnostica di risorse nel portale di hello
Verificare che tutte le risorse siano configurate con le impostazioni di diagnostica. Passare troppo**monitoraggio** in hello portale e aprire **le impostazioni di diagnostica**.

![Pannello log diagnostico nel portale di hello](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

È possibile tooclick sezione di monitoraggio hello toofind "Più servizi".

Qui è possibile visualizzare e filtrare tutte le risorse che supportano le impostazioni di diagnostica toosee se dispongono di diagnostica è abilitata. È possibile eseguire il drill-down toosee se più vengono impostati su una risorsa e controllare quale account di archiviazione, spazio dei nomi di hub eventi, e/o area di lavoro Log Analitica per i dati vengono trasmessi.

![Risultati di Log di diagnostica nel portale](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

Aggiunta di che un'impostazione di diagnostica consente di visualizzare hello Visualizza impostazioni di diagnostica, in cui è possibile abilitare, disabilitare o modificare le impostazioni di diagnostica per hello selezionato risorse.

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>Servizi, categorie e schemi supportati per i log di diagnostica di risorsa
[Vedere l'articolo](monitoring-diagnostic-logs-schema.md) per un elenco completo dei servizi supportati e categorie log hello e schemi utilizzati da tali servizi.

## <a name="next-steps"></a>Passaggi successivi

* [I log di diagnostica di risorse di flusso troppo**hub eventi**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Modificare le impostazioni di diagnostica di risorse utilizzando l'API REST di Azure Monitor hello](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Analizzare i log di Archiviazione di Azure con Log Analytics](../log-analytics/log-analytics-azure-storage.md)
