---
title: aaaAzure SQL database metriche & registrazione diagnostica | Documenti Microsoft
description: "Informazioni sulla configurazione di utilizzo delle risorse di Database SQL di Azure resource toostore, connettività e le statistiche di esecuzione di query."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a>Metriche del database SQL di Azure e registrazione diagnostica 
Il database SQL di Azure può generare metriche e log di diagnostica per facilitare il monitoraggio. È possibile configurare l'utilizzo delle risorse di Database SQL di Azure toostore, thread di lavoro e le sessioni e connettività in una di queste risorse di Azure:
- **Archiviazione di Azure**: per l'archiviazione di enormi quantità di dati di telemetria a un costo conveniente
- **Hub eventi di Azure**: per l'integrazione dei dati di telemetria del database SQL di Azure con soluzioni di monitoraggio personalizzate o pipeline attive
- **Azure Log Analitica**: per predefinito hello soluzione con reporting, avvisi e riduzione delle funzionalità di monitoraggio 

    ![architettura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a>Abilitazione della registrazione

Le metriche e la registrazione diagnostica non sono abilitate per impostazione predefinita. È possibile abilitare e gestire le metriche e registrazione di diagnostica utilizzando uno dei seguenti metodi hello:
- Portale di Azure
- PowerShell
- Interfaccia della riga di comando di Azure
- API REST 
- Modello di Resource Manager

Quando si abilita metriche e registrazione diagnostica, è necessario toospecify hello risorse di Azure in cui vengono raccolti i dati selezionati. Opzioni disponibili:
- Log Analytics
- Hub eventi
- Archiviazione di Azure 

È possibile eseguire il provisioning di una nuova risorsa di Azure o selezionare una risorsa esistente. Dopo aver selezionato la risorsa di archiviazione hello, è necessario toospecify toocollect quali dati. Le opzioni disponibili includono:

- **[Metriche 1 minuto](sql-database-metrics-diag-logging.md#1-minute-metrics)**: contiene percentuale DTU, limite DTU, percentuale CPU, percentuale lettura dati fisici, percentuale scrittura log, riuscito/non riuscito/bloccato dalle connessioni firewall, percentuale sessioni, percentuale ruoli di lavoro, risorsa di archiviazione, percentuale di archiviazione, percentuale di archiviazione XTP

Se si specifica l'Hub eventi o un account di sottoscrizione di Azure, è possibile specificare un toospecify di criteri di conservazione dei dati precedenti a un determinato periodo di tempo viene eliminato. Se si specifica Log Analitica, criteri di conservazione hello dipendono dal piano tariffario selezionato hello. Per altre informazioni, vedere [Prezzi di Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/). 

È consigliabile leggere entrambi hello [panoramica delle metriche in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [Panoramica di Azure i log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articoli toogain comprendere non solo la modalità registrazione tooenable, ma hello categorie di metriche e di log supportati da hello diversi servizi di Azure.

### <a name="azure-portal"></a>Portale di Azure

metriche tooenable raccolta di log di diagnostica nel portale di Azure hello esplorare database SQL di Azure tooyour o pagina pool elastico e quindi fare clic su **le impostazioni di diagnostica**.

   ![abilitare in hello portale di Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a>PowerShell

tooenable metrica e registrazione di diagnostica tramite PowerShell, Usa hello seguenti comandi:

- tooenable archiviazione dei log di diagnostica in un Account di archiviazione, usare questo comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   ID dell'Account di archiviazione Hello è l'id di risorsa di hello per i registri hello toowhich di account di archiviazione desiderato toosend hello.

- tooenable il flusso di log di diagnostica tooan Hub eventi, usare questo comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   Hello ID regola Bus di servizio è una stringa con questo formato:

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- tooenable l'invio di log di diagnostica tooa Log Analitica dell'area di lavoro, usare questo comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- È possibile ottenere l'id di risorsa hello dell'area di lavoro Log Analitica utilizzando hello comando seguente:

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

È possibile combinare queste tooenable parametri più opzioni di output.

### <a name="cli"></a>CLI

tooenable metrica e registrazione di diagnostica utilizzando hello CLI di Azure, hello di utilizzare i comandi seguenti:

- tooenable archiviazione dei log di diagnostica in un Account di archiviazione, usare questo comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   ID dell'Account di archiviazione Hello è l'id di risorsa di hello per i registri hello toowhich di account di archiviazione desiderato toosend hello.

- tooenable il flusso di log di diagnostica tooan Hub eventi, usare questo comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   Hello ID regola Bus di servizio è una stringa con questo formato:

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- tooenable l'invio di log di diagnostica tooa Log Analitica dell'area di lavoro, usare questo comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

È possibile combinare queste tooenable parametri più opzioni di output.

### <a name="rest-api"></a>API REST

Ottenere informazioni su come troppo[modificare le impostazioni di diagnostica utilizzando l'API REST di Azure Monitor hello](https://msdn.microsoft.com/library/azure/dn931931.aspx). 

### <a name="resource-manager-template"></a>Modello di Resource Manager

Ottenere informazioni su come troppo[abilitare le impostazioni di diagnostica al momento della creazione di risorse utilizzando il modello di gestione risorse](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md). 

## <a name="stream-into-log-analytics"></a>Eseguire lo streaming in Log Analytics 
Le metriche di Database SQL Azure e i log di diagnostica possono essere trasmesso in Log Analitica opzione hello incorporati "Invia tooLog Analitica" nel portale di hello o abilitando Log Analitica in un'impostazione di diagnostica tramite i cmdlet PowerShell di Azure, CLI di Azure o Azure monitoraggio REST API.

### <a name="installation-overview"></a>Panoramica dell'installazione

Monitorare la flotta del database SQL di Azure è semplice con Log Analytics. Sono necessari tre passaggi:

1.  Creare la risorsa Log Analytics
2.  Configurare le metriche toorecord database e log di diagnostica in hello creato Log Analitica
3.  Installare la soluzione **Analisi SQL di Azure** dalla raccolta in Log Analytics

### <a name="create-log-analytics-resource"></a>Creare la risorsa Log Analytics

1. Fare clic su **New** nel menu a sinistra di hello.
2. Fare clic su **Monitoraggio e gestione**
3. Fare clic su **Log Analytics**
4. Compilare il modulo di Log Analitica hello con informazioni aggiuntive di hello necessarie: nome dell'area di lavoro, sottoscrizione, gruppo di risorse, posizione e livello di prezzo.

   ![log analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a>Configurare le metriche toorecord database e log di diagnostica

tooconfigure modo più semplice Hello in database registrano le metriche viene eseguita tramite hello portale di Azure. In hello portale di Azure, passare tooyour risorse di Database SQL di Azure e fare clic su **le impostazioni di diagnostica**. 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a>Installare una soluzione Analitica SQL Azure hello dalla raccolta  

1. Una volta hello risorse Analitica di Log viene creato e i dati vengono trasmessi al suo interno, installare la soluzione Analitica SQL Azure. Questa operazione può essere eseguita tramite hello **Solutions Gallery** che è possibile trovare nella home page OMS hello e nel menu laterale hello. Nella raccolta di hello, trovare e fare clic su **Analitica SQL Azure** soluzione e fare clic su **Aggiungi**.

   ![soluzione di monitoraggio](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. Nella home page di OMS viene visualizzato un nuovo riquadro chiamato **Analisi SQL di Azure**. Selezionare questo riquadro per aprire il dashboard di Azure SQL Analitica hello.

### <a name="using-azure-sql-analytics-solution"></a>Uso della soluzione Analisi SQL di Azure

Analitica SQL Azure è un dashboard gerarchico che consente di toonavigate tramite gerarchia hello di risorse di Database SQL di Azure. In questo modo la funzionalità tooscope consente toodo di alto livello monitoraggio ma anche il monitoraggio hello toojust destra imposta delle risorse.
Dashboard contiene elenchi di hello di diverse risorse nella risorsa hello selezionato. Ad esempio, per una sottoscrizione selezionata è possibile vedere hello tutti i server, il pool elastico e i database appartenenti toohello selezionato una sottoscrizione. Inoltre, per il pool elastico e i database, è possibile visualizzare metriche di utilizzo di risorse hello di tale risorsa. Sono inclusi grafici per DTU, CPU, IO, LOG, sessioni, processi di lavoro, connessioni e archiviazione in GB.

## <a name="stream-into-azure-event-hub"></a>Eseguire lo streaming nell'hub eventi di Azure

Le metriche di Database SQL Azure e i log di diagnostica possono essere trasmesso in Hub eventi utilizzando l'opzione predefinita "hub eventi tooan flusso" hello nel portale di hello o abilitando l'Id regola Bus di servizio in un'impostazione di diagnostica tramite i cmdlet PowerShell di Azure, Azure CLI o REST di monitoraggio di Azure API. 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a>Quali toodo con metriche e i log di diagnostica in Hub eventi?
Una volta dati hello selezionato viene trasmessa in Hub eventi, sono tooenabling più vicino di un passaggio avanzate scenari di monitoraggio. Hub eventi funge da hello "porta principale" per una pipeline di eventi e una volta in un Hub eventi vengono raccolti i dati possono essere trasformato e archiviate utilizzando qualsiasi provider analitica in tempo reale o schede dell'invio in batch o dell'archiviazione. Hub eventi separa produzione hello di un flusso di eventi dal consumo hello di tali eventi, in modo che i consumer di eventi può accedere agli eventi di hello in una pianificazione personalizzata. Per altre informazioni sull'hub eventi, vedere:

- [Cosa sono gli hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md)?
- [Introduzione all'Hub eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


Ecco alcune modalità è possibile utilizzare funzionalità di streaming hello:

-   Visualizzare l'integrità del servizio dal flusso "percorso critico" dati tooPowerBI - tramite hub di eventi, flusso Analitica e Power BI, è possibile trasformare facilmente i dati di metrica e diagnostica in prossimità di informazioni in tempo reale in servizi di Azure. Per una panoramica delle modalità tooset di un hub di eventi, elaborano i dati con flusso Analitica, usare Power BI come output, vedere [flusso Analitica e Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).
-   Flusso registri toothird parti registrazione e i dati di telemetria flussi – hub di eventi tramite il flusso è possono ottenere le metriche e i log di diagnostica in toodifferent soluzioni analitica di monitoraggio e di log di terze parti. 
-   Compilare una telemetria personalizzata e una piattaforma di registrazione: se si dispone già di una piattaforma dati di telemetria personalizzati o sono solo le compilazione uno, hello altamente scalabile di pubblicazione-sottoscrizione natura degli hub di eventi consente tooflexibly acquisire i log di diagnostica. Vedere [toousing di Guida di Dan Rosanova hub eventi in una piattaforma dati di telemetria su scala globale](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="stream-into-azure-storage"></a>Eseguire lo streaming in Archiviazione di Azure

Le metriche di Database SQL Azure e i log di diagnostica possono essere archiviati in archiviazione di Azure usando l'opzione "Archivia l'account di archiviazione tooa" incorporati hello nel portale di Azure hello o abilitando l'archiviazione di Azure in un'impostazione di diagnostica tramite i cmdlet PowerShell di Azure, CLI di Azure o Azure API REST del monitoraggio.

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a>Schema delle metriche e i log di diagnostica nell'account di archiviazione hello

Dopo aver configurato le metriche e la raccolta di log di diagnostica, viene creato un contenitore di archiviazione nell'account di archiviazione hello selezionato quando sono disponibili righe prima di hello dei dati. struttura Hello di tali BLOB è:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
O, più semplicemente:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

Ad esempio, un nome del BLOB per la metrica 1 minuto potrebbe essere:

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

Nel caso in cui si desiderano dati hello toorecord dal Pool elastico hello, nome del blob è leggermente diverso:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a>Scaricare le metriche e i log da Archiviazione di Azure

Vedere [Scaricare le metriche e i log di diagnostica da Archiviazione di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)

## <a name="1-minute-metrics"></a>metriche 1 minuto

| |  |
|---|---|
|**Risorsa**|**Metriche**|
|Database|Percentuale DTU, DTU utilizzata, limite DTU, percentuale CPU, percentuale lettura dati fisici, percentuale scrittura log, riuscito/non riuscito/bloccato dalle connessioni firewall, percentuale sessioni, percentuale ruoli di lavoro, risorsa di archiviazione, percentuale di archiviazione, percentuale di archiviazione XTP, deadlock |
|Pool elastico|Percentuale eDTU, eDTU utilizzata, limite eDTU, percentuale CPU, percentuale lettura dati fisici, percentuale scrittura log, percentuale sessioni, percentuale ruoli di lavoro, risorsa di archiviazione, percentuale di archiviazione, limite di archiviazione, percentuale di archiviazione XTP |
|||

## <a name="next-steps"></a>Passaggi successivi

- Leggere entrambi hello [panoramica delle metriche in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) e [Panoramica di Azure i log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articoli toogain comprendere non solo del tooenable registrazione, ma hello metriche e categorie di log è supportato da hello diversi servizi di Azure.
- Leggere queste toolearn articoli sugli hub di eventi:
   - [Cosa sono gli hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md)?
   - [Introduzione all'Hub eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- Vedere [Scaricare le metriche e i log di diagnostica da Archiviazione di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
