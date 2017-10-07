---
title: analisi aaaLog per la rete CDN di Azure | Documenti Microsoft
description: "Il cliente può abilitare l'analisi dei log per la rete CDN di Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Log di diagnostica per la rete CDN di Azure

Dopo l'abilitazione della rete CDN per l'applicazione, verrà probabilmente desidera utilizzo della rete CDN di hello toomonitor, controllare l'integrità di hello del recapito e risolvere eventuali problemi. La rete CDN di Azure offre queste funzionalità tramite l'[analisi principale della rete CDN](cdn-analyze-usage-patterns.md) e i [log di diagnostica](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)

## <a name="cdn-core-analytics"></a>Analisi principale della rete CDN
Come un utente di rete CDN di Azure corrente con Verizon standard o un profilo premium, si è già analitica core tooview in grado di nel portale supplementare hello accessibile tramite l'opzione "Gestisci" hello da hello portale di Azure. 

## <a name="azure-diagnostic-logs"></a>Log di diagnostica di Azure

Con questa nuova funzionalità di Azure è ora possibile visualizzare analisi principali e salvarle in una o più destinazioni, tra cui:

 - Account di archiviazione di Azure
 - Hub eventi di Azure
 - [Repository di OMS Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 Questa funzionalità è disponibile per tutti gli endpoint rete CDN appartenenti tooVerizon (Standard e Premium) e i profili di rete CDN Akamai (Standard).

I log di diagnostica consentono di metriche di utilizzo di base tooexport dalla gamma di tooa endpoint rete CDN di origini in modo che sia possibile utilizzarli in modo personalizzato. Ad esempio, è possibile eseguire hello i tipi di esportazione dei dati seguenti:

- Esportare l'archiviazione dei dati tooblob, esportare tooCSV e generare grafici in excel.
- Esportare gli hub tooevent dati e correlare i dati da altri servizi di azure.
- Esportare dati toolog analitica e visualizzare i dati nello spazio di lavoro OMS

Hello figura seguente mostra una vista Analitica Core della rete CDN tipico nei dati.

![portale - Log di diagnostica](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*Figura 1 - Visualizzazione di analisi principale della rete CDN*

seguendo questa procedura dettagliata Hello passa attraverso schema hello dati hello core analitica, i passaggi necessari per abilitare la funzionalità di hello e inviarli toovarious destinazioni e utilizzo di queste destinazioni.

## <a name="enable-logging-with-azure-portal"></a>Abilitare la registrazione con il portale di Azure

> [!NOTE]
> Hello log di diagnostica sono attivati **off** per impostazione predefinita. 

Seguire i passaggi di hello sotto registrazione tooenable con Analitica Core della rete CDN:

Accedi toohello [portale di Azure](http://portal.azure.com). Se non si è già abilitata per il proprio flusso di lavoro, [abilitare la rete CDN di Azure](cdn-create-new-endpoint.md) prima di continuare.

1. Nel portale di hello passare troppo**profilo CDN**.
2. Selezionare un profilo di rete CDN, quindi selezionare l'endpoint rete CDN hello che si desidera tooenable **log di diagnostica**.

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. Andare troppo**log di diagnostica** pannello **monitoraggio** sezione, quindi modificare lo stato di hello troppo**su**.

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>Abilitare la registrazione con Archiviazione di Azure
    
toouse archiviazione di Azure toostore hello registri, selezionare **archiviare l'account di archiviazione tooa**, selezionare i giorni di conservazione e fare clic su **CoreAnalytics** in **Log**.

![portale - Log di diagnostica](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*Figura 2 - Registrazione con Archiviazione di Azure*

### <a name="logging-with-oms-log-analytics"></a>Registrazione con OMS Log Analytics

log hello toostore di toouse Analitica di Log di OMS, seguire questi passaggi:

1. Da hello **log di diagnostica** pannello **monitoraggio**selezionare **inviare tooLog Analitica** da 

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. Configurare la registrazione Analitica Log hello facendo clic su Configura. Verrà visualizzata la finestra di dialogo tooa in cui è possibile selezionare un'area di lavoro precedente o crearne uno nuovo.

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. Fare clic su **Crea una nuova area di lavoro**.

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/07_Create-new.png)

4. È quindi necessario selezionare il nome della nuova area di lavoro, la sottoscrizione esistente, un gruppo di risorse (nuovo o esistente), la posizione e il piano tariffario. È possibile hello di aggiunta di questo dashboard tooyour di configurazione. Fare clic su configurazione hello toocomplete OK.

    È quindi necessario visualizzare l'area di lavoro con i nomi dell'area di lavoro e del gruppo di risorse di OMS. I nomi devono essere univoci e possono contenere solo lettere, numeri e trattini. Gli spazi e i caratteri di sottolineatura non sono supportati. 

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. È quindi ottenere un breve messaggio che informa che è stato creato l'area di lavoro e si ritorna tooyour schermata di configurazione di registrazione. È possibile verificare il nome di hello dell'area di lavoro Log Analitica.

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    Dopo aver impostato la configurazione di Log Analitica hello, assicurarsi che anche casella hello CoreAnalytics per la registrazione della rete CDN.

6. Se tutto è tooyour desiderato, fare clic su hello **salvare** pulsante nella parte superiore di hello della finestra di dialogo Configurazione hello.

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/10_Save-me.png)

    Hello **salvare** pulsante non è più attivo e tale hello in/DISATTIVAZIONE pulsante è ON, ma blu anziché viola.

7. Se si desidera toosee nuova area di lavoro OMS, tooyour visitare il portale di Azure Dashboard, fare clic su nome hello dell'area di lavoro Log Analitica. Successivamente verrà visualizzato nell'area di lavoro (verificare che l'area di lavoro OMS è evidenziato a sinistra di hello). Fare clic su hello portale OMS riquadro toosee l'area di lavoro nel repository OMS hello. 

    ![portale - Log di diagnostica](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    Il repository OMS è ora pronto toolog dati. Ordinare tooconsume che i dati, è necessario utilizzare un [soluzioni OMS](#consuming-oms-log-analytics-data), coperto più avanti in questo articolo.

Per altre informazioni sui ritardi dei dati di log, vedere [qui](#log-data-delays).

## <a name="enable-logging-with-powershell"></a>Abilitare la registrazione con PowerShell

Di seguito è riportato un esempio di come tooenable e ottenere log di diagnostica tramite hello cmdlet PowerShell di Azure.

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>Abilitare log di diagnostica in un account di archiviazione

Prima di tutto, accedere e selezionare una sottoscrizione:

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


tooEnable i log di diagnostica in un Account di archiviazione, usare questo comando:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
tooEnable i log di diagnostica in un'area di lavoro OMS, usare questo comando:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>Utilizzo di log di diagnostica da Archiviazione di Azure
In questa sezione descrive schema hello di analitica di core della rete CDN hello, come questi sono organizzati all'interno di un Account di archiviazione di Azure e fornisce hello toodownload codice di esempio i log nel file CSV tooa.

### <a name="using-microsoft-azure-storage-explorer"></a>Uso di Microsoft Azure Storage Explorer
Prima di accedere a dati analitica di hello principali da hello Account di archiviazione di Azure, è necessario innanzitutto un contenuto hello tooaccess di strumento in un account di archiviazione. Anche se sono disponibili diversi strumenti disponibili in commercio hello, hello che è consigliabile è hello Microsoft Azure Storage Explorer. È possibile scaricare lo strumento hello da [qui](http://storageexplorer.com/). Dopo il download e installazione del software di hello, configurare toouse hello stesso Account di archiviazione di Azure che è stato configurato come un toohello di destinazione, i log di diagnostica di rete CDN.

1.  Aprire **Microsoft Azure Storage Explorer**
2.  Individuare l'account di archiviazione hello
3.  Passare toohello **"Contenitori Blob"** nodo in questo archivio account ed espandere il nodo di hello
4.  Contenitore hello selezionare denominato **"insights-log-coreanalytics"** e fare doppio clic
5.  Mostra i risultati di in hello riquadro di destra a partire da hello primo livello, che è simile **"resourceId ="**. Continuare a fare clic tutti modo hello fino a visualizzare il file hello **PT1H.json**. Vedere la nota per una descrizione del percorso hello seguente hello.
6.  Ogni blob **PT1H.json** rappresenta hello registri analitica per un'ora per un endpoint rete CDN specifico o il dominio personalizzato.
7.  schema di Hello contenuto hello di questo file JSON viene descritta nella sezione di hello dello Schema di hello registri Analitica Core


> [!NOTE]
> **Formato del percorso BLOB**
> 
> I log dell'analisi principale vengono generati ogni ora. Tutti i dati per un'ora sono raccolti e archiviati all'interno di un unico BLOB di Azure come payload JSON. percorso di Hello toothis Blob di Azure viene visualizzato come se vi è una struttura gerarchica. Questo è perché lo strumento Esplora di archiviazione hello interpreta '/' come separatore di directory e viene illustrata la gerarchia hello per praticità. In realtà, percorso completo di hello rappresenta solo il nome di blob hello. Questo nome di blob hello segue hello convenzione di denominazione seguente 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**Descrizione dei campi:**

|value|description|
|-------|---------|
|ID sottoscrizione    |ID della sottoscrizione di Azure hello. Questo è in formato Guid hello.|
|Risorsa |Nome gruppo di risorse della rete CDN di hello risorsa gruppo toowhich hello appartiene.|
|Nome profilo |Nome del profilo CDN hello|
|Nome endpoint |Nome dell'Endpoint rete CDN hello|
|Year|  rappresentazione di 4 cifre dell'anno hello 2017, ad esempio,|
|Mese| rappresentazione di 2 cifre del numero del mese hello. 01=Gennaio... 12=Dicembre|
|Giorno|   rappresentazione a 2 cifre del giorno hello hello mese|
|PT1H.json| File JSON effettivo dove vengono archiviati dati analitica hello|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a>Esportazione di hello Core Analitica dati tooa File CSV

toomake it tooaccess facile hello Core Analitica, Microsoft fornisce un esempio di codice per uno strumento che consente il download di file JSON di hello in un formato di file flat delimitato da virgole, che può essere utilizzato tooeasily, creare grafici o altre aggregazioni.

Ecco come è possibile utilizzare lo strumento hello:

1.  Visitare il collegamento di github hello: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  Scaricare codice hello
3.  Seguire le istruzioni toocompile e configurare
4.  Eseguire lo strumento hello
5.  File CSV risultante Mostra dati analitica hello in una semplice gerarchia flat.

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>Utilizzo di log di diagnostica da un repository di OMS Log Analytics
Log Analitica è un servizio Operations Management Suite (OMS) che consente di monitorare il toomaintain ambienti cloud e locali loro disponibilità e prestazioni. Vengono raccolti i dati generati dalle risorse negli ambienti di cloud e locali e da altre analisi di tooprovide strumenti monitoraggio in più origini. 

toouse Log Analitica, è necessario [abilitare la registrazione](#enable-logging-with-azure-storage) repository di Azure OMS Log Analitica toohello, come illustrato in precedenza in questo articolo.

### <a name="using-hello-oms-repository"></a>Utilizzo di hello Repository OMS

 Hello seguente diagramma illustra l'architettura hello di input hello e di output del repository hello:

![Repository di OMS Log Analytics](./media/cdn-diagnostics-log/12_Repo-overview.png)

*Figura 3 - Repository di Log Analytics*

È possibile visualizzare dati hello in diversi modi con le soluzioni di gestione. Per ottenere soluzioni di gestione di hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

È possibile installare le soluzioni di gestione da Azure marketplace facendo hello **Scarica adesso** collegamento nella parte inferiore di hello di ciascuna soluzione.

### <a name="adding-an-oms-cdn-management-solution"></a>Aggiunta di una soluzione di gestione della rete CDN di OMS

Seguire questi tooadd passaggi una soluzione di gestione:

1.   Se non già stato fatto, accedere toohello portale di Azure tramite la sottoscrizione di Azure e passare tooyour Dashboard.
    ![Dashboard di Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. In hello **New** pannello **Marketplace**selezionare **monitoraggio + gestione**.

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. In hello **monitoraggio + gestione** pannello, fare clic su **tutti**.

    ![Visualizzare tutto](./media/cdn-diagnostics-log/15_See-all.png)

4.  Ricerca per la rete CDN nella casella di ricerca hello.

    ![Visualizzare tutto](./media/cdn-diagnostics-log/16_Search-for.png)

5.  Selezionare **Azure CDN Core Analytics** (Analisi principale rete CDN di Azure). 

    ![Visualizzare tutto](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  Dopo aver fatto clic **crea**, sarà richiesto toocreate una nuova area di lavoro OMS o utilizzarne uno esistente. 

    ![Visualizzare tutto](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  Selezionare l'area di lavoro hello creata prima. È quindi necessario tooadd un account di automazione.

    ![Visualizzare tutto](./media/cdn-diagnostics-log/19_Add-automation.png)

8. Hello seguente schermata Mostra form dell'account di automazione hello che è necessario compilare. 

    ![Visualizzare tutto](./media/cdn-diagnostics-log/20_Automation.png)

9. Dopo aver creato l'account di automazione hello, si è pronti tooadd la soluzione. Fare clic su hello **crea** pulsante.

    ![Visualizzare tutto](./media/cdn-diagnostics-log/21_Ready.png)

10. La soluzione è stato aggiunto a questo punto tooyour dell'area di lavoro. Tornare tooyour Dashboard portale di Azure.

    ![Visualizzare tutto](./media/cdn-diagnostics-log/22_Dashboard.png)

    Fare clic su area di lavoro di Log Analitica hello creata toogo tooyour area di lavoro. 

11. Fare clic su hello **portale OMS** riquadro toosee la nuova soluzione nel portale OMS hello.

    ![Visualizzare tutto](./media/cdn-diagnostics-log/23_workspace.png)

12. Il portale OMS a questo punto dovrebbe essere simile hello seguente schermata:

    ![Visualizzare tutto](./media/cdn-diagnostics-log/24_OMS-solution.png)

    Fare clic su uno di hello riquadri toosee diverse visualizzazioni sui dati.

    ![Visualizzare tutto](./media/cdn-diagnostics-log/25_Interior-view.png)

    È possibile scorrere a sinistra o destra toosee ulteriormente riquadri rappresentano visualizzazioni singole in dati hello. 

    Fare clic su uno dei riquadri hello vengono forniti maggiori dettagli sui dati.

     ![Visualizzare tutto](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>Offerte e piani tariffari

Le offerte e i piani tariffari per le soluzioni di gestione di OMS sono disponibili [qui](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).

### <a name="customizing-views"></a>Personalizzazione delle visualizzazioni

È possibile personalizzare hello Visualizza i dati utilizzando hello **Visualizza finestra di progettazione**. Visitare l'area di lavoro OMS tooyour e inizia a progettare facendo hello **Visualizza finestra di progettazione** riquadro.

![Progettazione viste](./media/cdn-diagnostics-log/27_Designer.png)

È possibile trascinare ed eliminare i tipi di grafici da sinistra hello e specificare i dettagli di dati hello desiderato tooanalyze su hello a sinistra.

![Progettazione viste](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>Ritardi dei dati di log

Ritardi dei dati di log di Verizon | Ritardi dei dati di log di Akamai
--- | ---
Dati del log Verizon viene posticipati 1 ora e richiedere too2 ore toostart visualizzati dopo il completamento di propagazione di endpoint. | Dati del log Akamai sono 24 ore ritardate e occupano too2 ore toostart visualizzato se è stato creato più di 24 ore. Se è stato creato di recente, può richiedere ore too25 per hello registri toostart visualizzati.

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>Tipi di log di diagnostica per l'analisi principale della rete CDN

Offriamo attualmente solo Core Analitica nei registri, che contengono le metriche che mostra le statistiche in uscita come illustrato da hello POP CDN/bordi e risposta HTTP.

### <a name="core-analytics-metrics-details"></a>Dettagli delle metriche dell'analisi principale
Hello nella tabella seguente mostra un elenco delle metriche disponibili in hello che Analitica di componenti di base del log. Non tutte le metriche sono disponibili da tutti i provider, sebbene le differenze siano minime. Nella tabella seguente, anche Hello Mostra se una determinata metrica è disponibile presso un provider. Si noti che le metriche hello sono disponibili per solo gli endpoint CDN con il traffico su di essi.


|Metrica                     | Descrizione   | Verizon  | Akamai 
|---------------------------|---------------|---|---|
| RequestCountTotal         |Numero totale di riscontri della richiesta durante questo periodo| Sì  |Sì   |
| RequestCountHttpStatus2xx |Conteggio di tutte le richieste che hanno generato un codice HTTP 2xx (ad esempio 200, 202)              | Sì  |Sì   |
| RequestCountHttpStatus3xx | Conteggio di tutte le richieste che hanno generato un codice HTTP 3xx (ad esempio 300, 302)              | Sì  |Sì   |
| RequestCountHttpStatus4xx |Conteggio di tutte le richieste che hanno generato un codice HTTP 4xx (ad esempio 400, 404)               | Sì   |Sì   |
| RequestCountHttpStatus5xx | Conteggio di tutte le richieste che hanno generato un codice HTTP 5xx (ad esempio 500, 504)              | Sì  |Sì   |
| RequestCountHttpStatusOthers |  Conteggio di tutti gli altri codici HTTP (non inclusi nell'intervallo 2xx-5xx) | Sì  |Sì   |
| RequestCountHttpStatus200 | Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 200              |No   |Sì   |
| RequestCountHttpStatus206 | Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 206              |No   |Sì   |
| RequestCountHttpStatus302 | Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 302              |No   |Sì   |
| RequestCountHttpStatus304 |  Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 304             |No   |Sì   |
| RequestCountHttpStatus404 | Conteggio di tutte le richieste che hanno generato una risposta di codice HTTP 404              |No   |Sì   |
| RequestCountCacheHit |Conteggio di tutte le richieste che hanno generato un riscontro nella cache. Ciò significa che è stata gestita asset hello direttamente da toohello POP hello Client.               | Sì  |No   |
| RequestCountCacheMiss | Conteggio di tutte le richieste che hanno generato un mancato riscontro nella cache. Ciò significa hello asset non trovato nel client toohello più vicino di hello POP e pertanto è stato recuperato dall'origine hello.              |Sì   | No  |
| RequestCountCacheNoCache | Conteggio di tutte le richieste asset tooan esclusi dalla memorizzazione nella cache a causa di configurazione utente tooa sul bordo hello.              |Sì   | No  |
| RequestCountCacheUncacheable | Conteggio di tutti i richiede tooassets esclusi dalla memorizzazione nella cache dalla Cache-Control dell'asset hello e scade intestazioni, che indicano che è necessario non memorizzare nella cache in un POP o da client hello HTTP                |Sì   |No   |
| RequestCountCacheOthers | Conteggio di tutte le richieste con stato della cache non coperto dalle metriche precedenti.              |Sì   | No  |
| EgressTotal | Trasferimento di dati in uscita in GB              |Sì   |Sì   |
| EgressHttpStatus2xx | Trasferimento di dati in uscita* per risposte con codici di stato HTTP 2xx in GB            |Sì   |No   |
| EgressHttpStatus3xx | Trasferimento di dati in uscita per risposte con codici di stato HTTP 3xx in GB              |Sì   |No   |
| EgressHttpStatus4xx | Trasferimento di dati in uscita per risposte con codici di stato HTTP 4xx in GB               |Sì   | No  |
| EgressHttpStatus5xx | Trasferimento di dati in uscita per risposte con codici di stato HTTP 5xx in GB               |Sì   |  No |
| EgressHttpStatusOthers | Trasferimento di dati in uscita per risposte con altri codici di stato HTTP in GB                |Sì   |No   |
| EgressCacheHit |  In uscita di trasferimento dei dati per le risposte che sono state recapitate direttamente dalla cache di hello CDN in hello POP CDN/bordi  |Sì   |  No |
| EgressCacheMiss | Trasferimento dati in uscita per le risposte che non trovate in hello più vicino al server POP e recuperate dal server di origine hello              |Sì   |  No |
| EgressCacheNoCache | Trasferimento dei dati in uscita per le risorse che hanno impediti viene memorizzato nella cache a causa di configurazione utente tooa sul bordo hello.                |Sì   |No   |
| EgressCacheUncacheable | Trasferimento dati in uscita per le risorse che hanno impediti viene memorizzato nella cache dal controllo della Cache e/o intestazioni Expires, che indicano che è necessario non memorizzare nella cache in un POP o da client hello HTTP dell'asset hello                    |Sì   | No  |
| EgressCacheOthers |  Trasferimento di dati in uscita per altri scenari di cache.             |Sì   | No  |

* Trasferimento dati in uscita fa riferimento tootraffic inviato dal client di toohello server POP della rete CDN.


### <a name="schema-of-hello-core-analytics-logs"></a>Schema di hello registri Analitica Core 

Tutti i log vengono archiviati in formato JSON e ogni voce include campi stringa in seguito hello schema seguente:

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

Dove 'tempo di hello' rappresenta hello ora di inizio del limite di hello ora per il quale viene segnalata statistiche hello. Quando una metrica non è supportata da un provider di rete CDN, anziché un valore double o integer, è specificato un valore null. Questo valore null indica l'assenza di hello di una metrica e questo comportamento è diverso da un valore 0. Si noti inoltre che non vi saranno una set di queste metriche per ogni dominio configurato nell'endpoint hello.

Di seguito sono riportate proprietà di esempio:

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a>Risorse aggiuntive

* [Log di diagnostica di Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [Analisi principale tramite il portale supplementare della rete CDN di Azure](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [Azure OMS Log Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [API REST di Azure Log Analytics](https://docs.microsoft.com/en-us/rest/api/loganalytics)







