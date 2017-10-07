---
title: aaaMonitor e gestire le pipeline utilizzando hello portale di Azure e PowerShell | Documenti Microsoft
description: "Informazioni su come toouse hello portale di Azure e Azure PowerShell toomonitor e gestire hello Azure data factory e le pipeline che è stato creato."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a>Monitorare e gestire le pipeline di Data Factory di Azure tramite il portale di Azure hello e PowerShell
> [!div class="op_single_selector"]
> * [Con il portale di Azure/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Con l'app di monitoraggio e gestione](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> applicazione di monitoraggio e gestione Hello fornisce un supporto migliore per il monitoraggio e le pipeline di dati di gestione e risoluzione dei problemi relativi a eventuali problemi. Per informazioni dettagliate sull'utilizzo di un'applicazione hello, vedere [monitorare e gestire le pipeline di Data Factory tramite app di gestione e monitoraggio hello](data-factory-monitor-manage-app.md). 


In questo articolo viene descritto come toomonitor, gestire ed eseguire il debug le pipeline tramite il portale di Azure e PowerShell. Hello inoltre fornite informazioni su come toocreate gli avvisi e ottenere una notifica sugli errori.

## <a name="understand-pipelines-and-activity-states"></a>Informazioni sulle pipeline e sugli stati delle attività
Utilizzando hello portale di Azure, è possibile:

* Visualizzare la data factory come diagramma.
* Visualizzare le attività all'interno di una pipeline.
* Visualizzare set di dati di input e di output.

Questa sezione descrive anche la modalità di transizione dallo stato tooanother uno stato di una sezione di set di dati.   

### <a name="navigate-tooyour-data-factory"></a>Passare a data factory di tooyour
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Data factory** menu hello sulla sinistra hello. Se non è visualizzata, fare clic su **più servizi >**, quindi fare clic su **Data factory** in hello **INTELLIGENCE + analisi** categoria.

   ![Esplora tutto > Data factory](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. In hello **Data factory** blade, factory di hello selezionare dati che si è interessati.

    ![Selezionare la data factory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   Si dovrebbe essere hello home page per data factory di hello.

   ![Pannello Data factory](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a>Vista diagramma della data factory
Hello **diagramma** visualizzazione di una data factory offre un unico riquadro della finestra effetto cristallo toomonitor e gestire data factory di hello e delle relative risorse. hello toosee **diagramma** visualizzare la data factory, fare clic su **diagramma** hello home page per data factory di hello.

![Vista diagramma](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

È possibile eseguire lo zoom avanti, eseguire lo zoom indietro, toofit zoom, zoom too100%, blocco hello del layout hello diagramma e posiziona automaticamente le pipeline e set di dati. È inoltre possibile visualizzare informazioni sulla derivazione dei dati hello (vale a dire Mostra gli elementi a monte e a valle degli elementi selezionati).

### <a name="activities-inside-a-pipeline"></a>Attività all'interno di una pipeline
1. Fare clic sulla pipeline hello e quindi fare clic su **pipeline aprire** toosee tutte le attività in hello pipeline, insieme ai set di dati di input e output per le attività di hello. Questa funzionalità è utile quando la pipeline include più di un'attività e si desidera derivazione operative di hello toounderstand di una singola pipeline.

    ![Menu Apri pipeline](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. In hello l'esempio seguente, viene visualizzato nella pipeline hello con un input e un output di un'attività di copia. 

    ![Attività all'interno di una pipeline](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. È possibile spostarsi indietro toohello home page della data factory di hello facendo hello **Data factory** collegamento di navigazione hello nell'angolo superiore sinistro di hello.

    ![Spostarsi indietro toodata factory](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a>Stato di visualizzazione hello di ogni attività all'interno di una pipeline
È possibile visualizzare lo stato corrente di hello di un'attività visualizzando lo stato di hello di uno dei set di dati hello generati dalle attività hello.

Facendo doppio clic su hello **OutputBlobTable** in hello **diagramma**, è possibile visualizzare tutte le sezioni di hello generate dall'esecuzione di attività diverse all'interno di una pipeline. È possibile vedere che attività di copia hello è stato eseguito correttamente per hello ultime otto ore e prodotti sezioni hello hello **pronto** stato.  

![Stato della pipeline hello](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

sezioni di set di dati Hello nella data factory di hello possono avere uno dei seguenti stati hello:

<table>
<tr>
    <th align="left">Stato</th><th align="left">Sottostato</th><th align="left">Descrizione</th>
</tr>
<tr>
    <td rowspan="8">Waiting</td><td>ScheduleTime</td><td>tempo di Hello non venga per toorun sezione hello.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>le dipendenze upstream Hello non sono pronte.</td>
</tr>
<tr>
<td>ComputeResources</td><td>risorse di calcolo Hello non sono disponibili.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Tutte le istanze di attività hello sono occupate con l'esecuzione di altre sezioni.</td>
</tr>
<tr>
<td>ActivityResume</td><td>attività di Hello è sospesa e non possono essere eseguiti a intervalli hello finché non viene ripreso attività hello.</td>
</tr>
<tr>
<td>Retry</td><td>L'esecuzione dell'attività viene ritentata.</td>
</tr>
<tr>
<td>Convalida</td><td>La convalida non è ancora stata avviata.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>La convalida è in attesa toobe ripetuta.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Convalida in corso.</td><td>La convalida è in esecuzione.</td>
</tr>
<td>-</td>
<td>sezione Hello è stato elaborato.</td>
</tr>
<tr>
<td rowspan="4">Operazione non riuscita</td><td>TimedOut</td><td>l'esecuzione dell'attività Hello ha richiesto più tempo rispetto a quelle consentite dall'attività hello.</td>
</tr>
<tr>
<td>Canceled</td><td>sezione Hello è stata annullata dall'utente.</td>
</tr>
<tr>
<td>Convalida</td><td>Convalida non riuscita.</td>
</tr>
<tr>
<td>-</td><td>sezione Hello Impossibile toobe generato e/o convalidare.</td>
</tr>
<td>Ready</td><td>-</td><td>sezione di Hello è pronto per l'utilizzo.</td>
</tr>
<tr>
<td>Skipped</td><td>Nessuno</td><td>sezione Hello non elaborate.</td>
</tr>
<tr>
<td>Nessuno</td><td>-</td><td>Una sezione utilizza tooexist con un altro stato, ma è stato reimpostato.</td>
</tr>
</table>



È possibile visualizzare i dettagli di hello su una sezione facendo clic su una voce della sezione in hello **sezioni aggiornato di recente** blade.

![Dettagli della sezione](./media/data-factory-monitor-manage-pipelines/slice-details.png)

Se la sezione hello è stata eseguita più volte, vedrai più righe in hello **viene eseguita l'attività** elenco. È possibile visualizzare informazioni dettagliate su un'attività eseguire facendo voce hello eseguire hello **viene eseguita l'attività** elenco. Hello sono elencati tutti i file di log di hello, insieme a un messaggio di errore, se presente. Questa funzionalità è utili registri di debug e di tooview senza tooleave la data factory.

![Dettagli esecuzione attività](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

Se non è la sezione hello in hello **pronto** stato, è possibile vedere le sezioni upstream hello che non sono pronto e bloccano l'intervallo corrente di hello l'esecuzione in hello **sezioni Upstream non pronte** elenco. Questa funzionalità è utile quando è la sezione **in attesa** stato e si desidera che le dipendenze upstream toounderstand hello che hello sezione è in attesa.

![Sezioni upstream non pronte](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a>Diagramma di stato del set di dati
Dopo la distribuzione di una data factory e hello pipeline dispongono di un periodo attivo valido, set di dati hello seziona transizione da uno stato tooanother. Attualmente, lo stato della sezione hello segue hello seguente diagramma di stato:

![Diagramma di stato](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

il flusso di transizione dello stato di set di dati in data factory di Hello è hello seguente: in attesa -> In corso/In esecuzione (Validating) -> pronto/non riuscito.

sezione Hello viene avviato in un **in attesa** stato, in attesa di toobe precondizioni soddisfatti prima dell'esecuzione. Quindi avvia l'esecuzione di attività hello e sezione hello diventa un **In corso** stato. l'esecuzione dell'attività Hello potrebbe riuscire o meno. sezione Hello è contrassegnato come **pronto** o **Failed**, in base ai risultati di hello dell'esecuzione di hello.

È possibile reimpostare hello sezione toogo da hello **pronto** o **Failed** stato toohello **in attesa** stato. È inoltre possibile contrassegnare lo stato di sezione hello troppo**Skip**, impedendo così l'attività hello eseguire e di non elaborazione hello sezione.

## <a name="pause-and-resume-pipelines"></a>Sospendere e riprendere le pipeline
È possibile gestire le pipeline usando Azure PowerShell. Ad esempio, è possibile sospendere e riprendere le pipeline eseguendo i cmdlet di Azure PowerShell. 

> [!NOTE] 
> vista diagramma Hello non supporta la sospensione e ripresa di pipeline. Se si desidera toouse un'interfaccia utente, è possibile utilizzare Monitoraggio hello e la gestione di applicazioni. Per informazioni dettagliate sull'utilizzo di un'applicazione hello, vedere [monitorare e gestire le pipeline di Data Factory tramite app di gestione e monitoraggio hello](data-factory-monitor-manage-app.md) articolo. 

È possibile sospendere o sospendere le pipeline utilizzando hello **Suspend AzureRmDataFactoryPipeline** cmdlet di PowerShell. Questo cmdlet è utile quando non si desidera toorun le pipeline finché non viene risolto un problema. 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
ad esempio:

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

Dopo hello problema è stato risolto con pipeline hello, è possibile riprendere pipeline hello sospeso eseguendo hello comando PowerShell seguente:

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
ad esempio:

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a>Eseguire il debug delle pipeline
Data Factory di Azure offre funzionalità avanzate di toodebug e risolvere i problemi di pipeline utilizzando hello portale di Azure e Azure PowerShell.

> [! Si noti} è molto più semplice tootroubleshot hello di errori tramite Monitoraggio e gestione App. Per informazioni dettagliate sull'utilizzo di un'applicazione hello, vedere [monitorare e gestire le pipeline di Data Factory tramite app di gestione e monitoraggio hello](data-factory-monitor-manage-app.md) articolo. 

### <a name="find-errors-in-a-pipeline"></a>Trovare gli errori in una pipeline
Se l'esecuzione dell'attività hello ha esito negativo in una pipeline, i set di dati di hello viene generato dalla pipeline hello è in stato di errore a causa di errore hello. È possibile eseguire il debug e risolvere gli errori nella Data Factory di Azure tramite hello dei seguenti metodi.

#### <a name="use-hello-azure-portal-toodebug-an-error"></a>Utilizzare hello toodebug portale Azure un errore
1. In hello **tabella** pannello, fare clic sulla sezione problema hello con hello **stato** impostare troppo**non riuscito**.

   ![Pannello Tabella con sezione con errori](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. In hello **sezione dati** pannello, fare clic sull'attività hello eseguire che non è riuscita.

   ![Sezione dati con un errore](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. In hello **Dettagli esecuzione attività** pannello, è possibile scaricare i file di hello associati con l'elaborazione di HDInsight hello. Fare clic su **scaricare** per stato/stderr toodownload hello file di log che contiene dettagli sull'errore hello.

   ![Pannello Dettagli esecuzione attività con errore](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a>Utilizzare PowerShell toodebug un errore
1. Avviare **PowerShell**.
2. Eseguire hello **Get AzureRmDataFactorySlice** comando sezioni hello toosee e i relativi stati. Si noterà una sezione con stato hello **Failed**.        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   ad esempio:

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   Sostituire **StartDateTime** con l'ora di inizio della pipeline. 
3. A questo punto, eseguire hello **Get AzureRmDataFactoryRun** tooget cmdlet dettagli attività hello eseguire per sezione hello.

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    ad esempio:

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    il valore di Hello di StartDateTime è ora di inizio hello sezione errore/problema hello annotato nel passaggio precedente hello. Data e ora Hello deve essere racchiuse tra virgolette doppie.
4. Verrà visualizzato l'output con i dettagli sull'errore hello che è simile toohello seguente:

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. È possibile eseguire hello **Salva AzureRmDataFactoryLog** cmdlet con il valore Id vedere dall'output di hello e scaricare i file di log di hello utilizzando hello hello **- DownloadLogsoption** per hello cmdlet.

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a>Eseguire nuovamente le operazioni non riuscite in una pipeline

> [!IMPORTANT]
> È più facile tootroubleshoot errori ed eseguire di nuovo le sezioni non riuscite utilizzando hello monitoraggio e gestione delle App. Per informazioni dettagliate sull'utilizzo di un'applicazione hello, vedere [monitorare e gestire le pipeline di Data Factory tramite app di gestione e monitoraggio hello](data-factory-monitor-manage-app.md). 

### <a name="use-hello-azure-portal"></a>Utilizzare hello portale di Azure
Dopo aver il debug degli errori in una pipeline di risoluzione dei problemi, è possibile rieseguire errori passando sezione errore toohello e facendo clic su hello **eseguire** pulsante sulla barra dei comandi di hello.

![Nuova esecuzione di una sezione non riuscita](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

Nel caso sezione hello convalida non è riuscita a causa di un errore dei criteri (ad esempio, se dati non sono disponibili), è possibile correggere l'errore hello e convalidare di nuovo facendo hello **convalida** pulsante sulla barra dei comandi di hello.

![Correggere gli errori e convalidare](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a>Uso di Azure PowerShell
È possibile eseguire nuovamente gli errori utilizzando hello **Set AzureRmDataFactorySliceStatus** cmdlet. Vedere hello [Set AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) argomento per la sintassi e altri dettagli sul cmdlet hello.

**Esempio:**

esempio Hello Imposta stato hello di tutte le sezioni per hello nella tabella 'DAWikiAggregatedData' too'Waiting' in hello data factory di Azure 'WikiADF'.

Hello 'Tipo di aggiornamento' è impostato too'UpstreamInPipeline ', il che significa che gli stati di ogni sezione per la tabella hello e tutte le tabelle (upstream) dipendenti hello siano impostati too'Waiting'. Hello altri valori possibili per questo parametro sono 'Individuale'.

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a>Creare avvisi
Azure registra eventi utente quando una risorsa di Azure (ad esempio, una data factory) viene creata, aggiornata o eliminata. È possibile creare avvisi per questi eventi. È possibile utilizzare Data Factory toocapture diverse metriche e creare avvisi per le metriche. È consigliabile usare gli eventi per il monitoraggio in tempo reale e le metriche per motivi cronologici.

### <a name="alerts-on-events"></a>Avvisi relativi agli eventi
Gli eventi di Azure forniscono utili informazioni su quanto accade alle risorse di Azure. Quando si usa Azure Data Factory, vengono generati eventi quando:

* Una data factory viene creata, aggiornata o eliminata.
* L'elaborazione dati (esecuzione) viene avviata o completata.
* Un cluster HDInsight su richiesta viene creato o rimosso.

È possibile creare avvisi per questi eventi utente e configurarli amministratore toohello le notifiche di posta elettronica toosend e coadministrators della sottoscrizione hello. Inoltre, è possibile specificare gli indirizzi di posta elettronica aggiuntivi di utenti che necessitano di tooreceive notifiche di posta elettronica quando vengono soddisfatte le condizioni di hello. Questa funzionalità è utile quando si desidera tooget notifiche in caso di errori e non toocontinuously monitoraggio la data factory.

> [!NOTE]
> Attualmente, portale hello non vengono visualizzati avvisi sugli eventi. Hello utilizzare [monitoraggio e gestione di app](data-factory-monitor-manage-app.md) toosee tutti gli avvisi.


#### <a name="specify-an-alert-definition"></a>Specificare una definizione di avviso
toospecify una definizione di avviso, si crea un file JSON che descrive le operazioni che si desidera toobe avvisati sul hello. Nell'esempio seguente di hello, avviso hello invia una notifica di posta elettronica per hello RunFinished operazione. toobe specifico, viene inviata una notifica di posta elettronica quando è stata completata un'esecuzione in data factory di hello e hello eseguire non è riuscita (stato = FailedExecution).

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

È possibile rimuovere **subStatus** dalla definizione JSON se non si desidera ricevere un avviso in caso di errore specifico toobe hello.

In questo esempio imposta avviso hello per tutte le data factory nella sottoscrizione. Se si desidera toobe di avviso hello impostato per una particolare data factory, è possibile specificare data factory di **resourceUri** in hello **dataSource**:

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

Hello nella tabella seguente sono elencate per hello operazioni disponibili e gli stati (e stati secondari).

| Nome operazione | Stato | Stato secondario |
| --- | --- | --- |
| RunStarted |Started |Starting |
| RunFinished |Failed/Succeeded |Allocazione risorse non riuscita<br/><br/>Succeeded<br/><br/>FailedExecution<br/><br/>TimedOut<br/><br/><Canceled<br/><br/>FailedValidation<br/><br/>Abbandonato |
| OnDemandClusterCreateStarted |Started | |
| OnDemandClusterCreateSuccessful |Operazione completata | |
| OnDemandClusterDeleted |Operazione completata | |

Vedere [Crea regola di avviso](https://msdn.microsoft.com/library/azure/dn510366.aspx) per informazioni dettagliate sugli elementi JSON hello utilizzati nell'esempio hello.

#### <a name="deploy-hello-alert"></a>Distribuire avviso hello
avviso di hello toodeploy, utilizzare cmdlet di Azure PowerShell hello **New AzureRmResourceGroupDeployment**, come illustrato nell'esempio seguente hello:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

Dopo la distribuzione del gruppo di risorse hello è stato completato, vedrai hello seguenti messaggi:

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> È possibile utilizzare hello [Crea regola di avviso](https://msdn.microsoft.com/library/azure/dn510366.aspx) API REST toocreate una regola di avviso. payload JSON Hello è esempio JSON di toohello simile.  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a>Recuperare l'elenco di hello di distribuzioni del gruppo di risorse di Azure
elenco di hello tooretrieve di distribuito distribuzioni del gruppo di risorse di Azure, utilizzare i cmdlet di hello **Get AzureRmResourceGroupDeployment**, come illustrato nell'esempio seguente hello:

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a>Risolvere i problemi relativi a eventi utente
1. È possibile visualizzare tutti gli eventi di hello che vengono generati dopo aver fatto clic hello **operazioni e le metriche** riquadro.

    ![Riquadro Metriche e operazioni](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. Fare clic su hello **eventi** riquadro eventi hello toosee.

    ![Riquadro Eventi](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. In hello **eventi** pannello, è possibile visualizzare i dettagli sugli eventi, eventi filtrati e così via.

    ![Pannello Eventi](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. Fare clic su un **operazione** nell'elenco di operazioni hello che provoca un errore.

    ![Selezionare un'operazione](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. Fare clic su un **errore** dettagli sull'errore hello toosee dell'evento.

    ![Evento di errore](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

Vedere [informazioni dettagliate di Azure cmdlet](https://msdn.microsoft.com/library/mt282452.aspx) per i cmdlet di PowerShell che è possibile utilizzare tooadd, ottenere o rimuovere gli avvisi. Ecco alcuni esempi di utilizzo hello **Get AlertRule** cmdlet:

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

Eseguire hello seguente get-help comandi toosee dettagli ed esempi per cmdlet Get-AlertRule hello.

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


Se viene visualizzato gli eventi di generazione dell'avviso hello in hello portale pannello ma non ricevere notifiche tramite posta elettronica, controllare se l'indirizzo di posta elettronica hello specificato è impostato tooreceive messaggi di posta elettronica da mittenti esterni. messaggi di avviso Hello potrebbero sono state bloccate dalle impostazioni di posta elettronica.

### <a name="alerts-on-metrics"></a>Avvisi relativi alle metriche
Azure Data Factory consente di acquisire diverse metriche e di creare avvisi relativi alle metriche. È possibile monitorare e creare avvisi per hello seguenti metriche per le sezioni hello la data factory:

* **Esecuzioni non riuscite**
* **Esecuzioni riuscite**

Queste metriche sono utili e consentono una panoramica generale e non viene eseguito in data factory di hello tooget. Le metriche vengono emesse ogni volta che viene eseguita una sezione. Inizio hello ora hello, queste metriche vengono aggregate e inserito tooyour account di archiviazione. metriche tooenable, impostare un account di archiviazione.

#### <a name="enable-metrics"></a>Abilitazione di metriche
tooenable metriche, fare clic su informazioni seguenti hello hello **Data Factory** pannello:

**Monitoraggio** > **Metrica** > **Impostazioni di diagnostica** > **Diagnostica**

![Collegamento per la diagnostica](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

In hello **diagnostica** pannello, fare clic su **su**, selezionare l'account di archiviazione hello e fare clic su **salvare**.

![Pannello Diagnostica](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

Operazione può richiedere ora tooone per hello metriche toobe visibile in hello **monitoraggio** pannello poiché l'aggregazione di metriche si verifica ogni ora.

### <a name="set-up-an-alert-on-metrics"></a>Configurare un avviso relativo alle metriche
Fare clic su hello **metriche Data Factory** riquadro:

![Riquadro Metriche data factory](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

In hello **metrica** pannello, fare clic su **+ Aggiungi avviso** sulla barra degli strumenti hello.
![Pannello Metriche data factory > Aggiungi avviso](./media/data-factory-monitor-manage-pipelines/add-alert.png)

In hello **aggiungere una regola di avviso** pagina hello alla procedura seguente e fare clic su **OK**.

* Immettere un nome per l'avviso hello (esempio: "non riuscito-avviso").
* Immettere una descrizione dell'avviso hello (esempio: "Invia un messaggio di posta elettronica quando si verifica un errore").
* Selezionare una metrica tra "Esecuzioni non riuscite" ed "Esecuzioni riuscite".
* Specificare una condizione e un valore di soglia.   
* Specificare hello periodo di tempo.
* Specificare se è necessario inviare un messaggio di posta elettronica tooowners, contributors e readers.

![Pannello Metriche data factory > Aggiungi regola di avviso](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

Dopo che la regola di avviso hello viene aggiunto correttamente, pannello hello chiude e viene visualizzato di nuovo avviso hello in hello **metrica** blade.

![Pannello Metriche data factory > Nuovo avviso aggiunto](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

Verrà inoltre visualizzato il numero di hello di avvisi in hello **regole di avviso** riquadro. Fare clic su hello **regole di avviso** riquadro.

![Pannello Metriche data factory - Regole di avviso](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

In hello **avvisi regole** pannello viene visualizzato di tutti gli avvisi esistenti. tooadd un avviso, fare clic su **Aggiungi avviso** sulla barra degli strumenti hello.

![Pannello Regole di avviso](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a>Notifiche di avviso
Dopo che la regola di avviso hello corrisponde a hello condizione, viene visualizzato un messaggio di posta elettronica che segnala hello avviso viene attivato. Dopo che viene risolto hello e condizione di avviso hello non corrisponde più, viene visualizzato un messaggio di posta elettronica che segnala hello avviso verrà risolto.

Questo comportamento è diverso da quello degli eventi in cui viene inviata una notifica per ogni errore qualificato da una regola di avviso.

### <a name="deploy-alerts-by-using-powershell"></a>Distribuire avvisi tramite PowerShell
È possibile distribuire gli avvisi per le metriche hello stessa modalità utilizzata per gli eventi.

**Definizione di avviso**

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

Sostituire *subscriptionId*, *resourceGroupName*, e *dataFactoryName* nell'esempio hello con valori appropriati.

*metricName* supporta attualmente due valori:

* FailedRuns
* SuccessfulRuns

**Distribuire avviso hello**

avviso di hello toodeploy, utilizzare cmdlet di Azure PowerShell hello **New AzureRmResourceGroupDeployment**, come illustrato nell'esempio seguente hello:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

Al termine della distribuzione, verrà visualizzato il messaggio seguente:

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

È inoltre possibile utilizzare hello **Aggiungi AlertRule** toodeploy cmdlet una regola di avviso. Vedere hello [Aggiungi AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) argomento per informazioni dettagliate ed esempi.  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a>Spostare un gruppo di risorse diverso tooa data factory o una sottoscrizione
È possibile spostare un gruppo di risorse diverso dati tooa factory o una sottoscrizione diversa utilizzando hello **spostare** barra pulsante hello home page della data factory dei comandi.

![Spostare una data factory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

È inoltre possibile spostare le risorse correlate (ad esempio gli avvisi che sono associati a data factory di hello), insieme a data factory di hello.

![Finestra di dialogo Sposta risorse](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
