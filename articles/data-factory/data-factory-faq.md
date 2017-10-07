---
title: aaaAzure Data Factory - domande frequenti
description: Domande frequenti su Azure Data Factory.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 532dec5a-7261-4770-8f54-bfe527918058
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 78289fb4b6e15d74772af6c71ec25c7d2ca1a0bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a>Azure Data Factory - Domande frequenti
## <a name="general-questions"></a>Domande generali
### <a name="what-is-azure-data-factory"></a>Che cos'è Azure Data Factory?
Data Factory è basato su cloud integrazione dei dati del servizio che **automatizza lo spostamento di hello e trasformazione dei dati**. Come una factory che viene eseguito apparecchiature tootake materie prime e li trasforma in finiti, Data Factory Orchestra servizi esistenti per la raccolta dati non elaborati e trasformano in informazioni pronte per l'uso.

Data Factory consente dati toomove di flussi di lavoro basati su dati toocreate tra sia locale e archivi dati cloud, nonché dati di processo/trasformazione utilizzando i servizi di calcolo, ad esempio HDInsight di Azure e Azure Data Lake Analitica. Dopo aver creato una pipeline che esegue l'azione di hello che è necessario, è possibile pianificare periodicamente toorun (oraria, giornaliera, settimanale e così via).   

Per altre informazioni, vedere [Cenni preliminari e concetti chiave](data-factory-introduction.md).

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a>Dove posso trovare informazioni dettagliate sui prezzi di Azure Data Factory?
Vedere [pagina prezzi Factory dati] [ adf-pricing-details] per hello dettagli dei prezzi per hello Azure Data Factory.  

### <a name="how-do-i-get-started-with-azure-data-factory"></a>In che modo è possibile iniziare a usare Azure Data Factory?
* Per una panoramica di Data Factory di Azure, vedere [tooAzure introduzione Data Factory](data-factory-introduction.md).
* Per un'esercitazione sulla troppo**copiare o spostare dati** tramite attività di copia, vedere [copiare i dati da tooAzure di archiviazione Blob di Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* Per un'esercitazione sulla troppo**trasformare dati** utilizzando l'attività Hive di HDInsight. vedere [Elaborare i dati eseguendo lo script Hive in un cluster Hadoop](data-factory-build-your-first-pipeline.md)

### <a name="what-is-hello-data-factorys-region-availability"></a>Che cos'è la disponibilità dell'hello Data Factory area?
Data Factory è disponibile negli **Stati Uniti occidentali** e in **Europa settentrionale**. Hello calcolo e i servizi di archiviazione utilizzati da data factory possono essere in altre aree. Vedere [Aree supportate](data-factory-introduction.md#supported-regions).

### <a name="what-are-hello-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a>Quali sono i limiti di hello sul numero di data factory/pipeline/attività/set di dati?
Vedere **limiti di Azure Data Factory** sezione di hello [sottoscrizione Azure e limiti dei servizi, quote e vincoli](../azure-subscription-service-limits.md#data-factory-limits) articolo.

### <a name="what-is-hello-authoringdeveloper-experience-with-azure-data-factory-service"></a>Che cos'è hello creazione/esperienza dello sviluppatore con il servizio Data Factory di Azure?
È possibile autore/creare data factory con uno dei seguenti SDK di strumenti/hello:

* **Portale di Azure** pannelli di hello Data Factory nel portale di Azure hello servizi interfaccia utente avanzata per l'utente toocreate dati factory ad collegato. Hello **Editor delle Data Factory**, che fa parte del portale di hello consente tooeasily creare servizi collegati, tabelle, set di dati e le pipeline specificando le definizioni di JSON per questi elementi. Vedere [compilare il primo pipeline di dati tramite il portale di Azure](data-factory-build-your-first-pipeline-using-editor.md) per un esempio di utilizzo hello toocreate/editor di portale e distribuire una data factory.
* **Visual Studio** è possibile utilizzare Visual Studio toocreate una data factory di Azure. Per i dettagli, vedere [Creare la prima data factory di Azure con Microsoft Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) .
* **Azure PowerShell** : per un'esercitazione o la procedura dettagliata per la creazione di una data factory tramite PowerShell, vedere [Creare la prima data factory di Azure con Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md) . Per la documentazione completa dei cmdlet di Data Factory, vedere [Data Factory Cmdlet Reference][adf-powershell-reference] (Informazioni di riferimento sui cmdlet di Data Factory) in MSDN Library.
* **.NET Class Library** È possibile creare data factory a livello di programmazione usando .NET SDK per Data Factory. Per la procedura dettagliata per la creazione di un'istanza di Data Factory con .NET SDK, vedere [Creazione, monitoraggio e gestione delle istanze di Azure Data Factory mediante .NET SDK](data-factory-create-data-factories-programmatically.md) . Per la documentazione completa di Data Factory .NET SDK, vedere [Data Factory Class Library Reference][msdn-class-library-reference] (Informazioni di riferimento sulla libreria di classi per Data Factory).
* **API REST** è anche possibile utilizzare hello API REST esposta da toocreate servizio Azure Data Factory di hello e distribuire data factory. Per la documentazione completa, vedere [Data Factory REST API Reference][msdn-rest-api-reference] (Informazioni di riferimento sull'API REST di Data Factory).
* **Modello di Azure Resource Manager** Per i dettagli, vedere [Esercitazione: Creare la prima data factory di Azure usando il modello di Azure Resource Manager](data-factory-build-your-first-pipeline-using-arm.md) .

### <a name="can-i-rename-a-data-factory"></a>È possibile rinominare una data factory?
No. Quali altre risorse di Azure, il nome di hello di una data factory di Azure non può essere modificato.

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-tooanother"></a>È possibile spostare una data factory da una sottoscrizione di Azure tooanother?
Sì. Hello utilizzare **spostare** pulsante nel Pannello di factory dati, come illustrato nel seguente diagramma hello:

![Spostare una data factory](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-hello-compute-environments-supported-by-data-factory"></a>Quali sono gli ambienti di calcolo hello è supportati da Data Factory?
Hello nella tabella seguente fornisce un elenco degli ambienti di elaborazione supportata dalle attività di Data Factory e hello che è possibile eseguire su di essi.

| Ambiente di calcolo | attività |
| --- | --- |
| [Cluster HDInsight su richiesta](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) o [il proprio cluster HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md) |
| [Azure Batch](data-factory-compute-linked-services.md#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[Attività di Machine Learning: esecuzione batch e aggiornamento risorse](data-factory-azure-ml-batch-execution-activity.md) |
| [Azure Data Lake Analytics.](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[Attività U-SQL di Data Lake Analytics](data-factory-usql-activity.md) |
| [Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service), [Azure SQL Data Warehouse](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service), [SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service) |[Stored procedure](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a>Come si confronta Azure Data Factory con SQL Server Integration Services (SSIS)? 
Vedere hello [vs Data Factory di Azure. SSIS](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS) di uno dei nostri MVP (Most Valued Professional): Reza Rad. Alcune delle modifiche apportate di recente hello in Data Factory potrebbero non essere incluse nella presentazione hello. In modo continuo, si aggiungono ulteriori funzionalità tooAzure Data Factory. In modo continuo, si aggiungono ulteriori funzionalità tooAzure Data Factory. Si verranno incorporare questi aggiornamenti in confronto hello delle tecnologie di integrazione di dati da Microsoft un intervallo di tempo entro l'anno.   

## <a name="activities---faq"></a>Attività - Domande frequenti
### <a name="what-are-hello-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a>Quali sono hello diversi tipi di attività, che è possibile utilizzare in una pipeline di Data Factory?
* [Le attività di spostamento dati](data-factory-data-movement-activities.md) toomove dati.
* [Attività di trasformazione dei dati](data-factory-data-transformation-activities.md) tooprocess/trasformazione dati.

### <a name="when-does-an-activity-run"></a>Quando viene eseguita un'attività?
Hello **disponibilità** impostazione di configurazione nel hello output tabella dati determina l'esecuzione di attività hello. Se vengono specificati i set di dati di input, l'attività hello controlla se vengono soddisfatte tutte le dipendenze di dati di input hello (vale a dire **pronto** stato) prima che siano in esecuzione.

## <a name="copy-activity---faq"></a>Attività di copia - Domande frequenti
### <a name="is-it-better-toohave-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a>È preferibile toohave una pipeline con più attività o una pipeline distinta per ogni attività?
Pipeline dovrebbero toobundle attività correlate. Se i set di dati hello che li connettono non vengono utilizzati da qualsiasi altra attività di fuori della pipeline hello, è possibile mantenere le attività di hello in una pipeline. In questo modo, non è necessario toochain periodi attivi di pipeline in modo che vengano allineati tra loro. Salve, inoltre, l'integrità dei dati nelle tabelle di hello pipeline interna toohello meglio viene mantenuta quando l'aggiornamento della pipeline hello. Aggiornamento della pipeline essenzialmente arresta tutte le attività di hello pipeline hello, rimuoverli e li crea nuovamente. Dalla prospettiva di creazione, potrebbe inoltre essere più facile toosee hello il flusso di dati all'interno di hello correlata le attività in JSON di un file per la pipeline di hello.

### <a name="what-are-hello-supported-data-stores"></a>Quali sono hello supportati archivi dati?
Attività di copia in Data Factory copia dati da un archivio dati di origine dati archivio tooa sink. Data Factory supporta hello seguenti archivi dati. È possibile scrivere dati da qualsiasi origine tooany sink. Fare clic su un toolearn archivio dati come toocopy tooand di dati dall'archivio.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Archivia i dati con * può essere locale o in Azure IaaS e richiedono tooinstall [Gateway di gestione dati](data-factory-data-management-gateway.md) in un computer di IaaS in locale o Azure.

### <a name="what-are-hello-supported-file-formats"></a>Quali sono hello formati di file supportati?
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-hello-copy-operation-performed"></a>In cui viene eseguita l'operazione di copia hello?
Per altre informazioni, vedere la sezione [Spostamento dei dati disponibile a livello globale](data-factory-data-movement-activities.md#global) . In breve, quando è coinvolto un archivio dati locale, operazione di copia hello viene eseguita da hello Gateway di gestione dati nell'ambiente locale. E, quando lo spostamento dei dati di hello è compreso tra due archivi cloud, l'operazione di copia hello viene eseguita in hello area più vicina toohello sink posizione in hello geography stesso.

## <a name="hdinsight-activity---faq"></a>Attività di HDInsight - Domande frequenti
### <a name="what-regions-are-supported-by-hdinsight"></a>Quali aree sono supportate da HDInsight?
Vedere hello sezione di disponibilità a livello geografico nell'articolo seguente hello: o [dettagli prezzi di HDInsight][hdinsight-supported-regions].

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a>Quale area geografica viene usata per un cluster HDInsight su richiesta?
Hello cluster HDInsight su richiesta viene creato in hello stessa area in cui archiviazione hello toobe utilizzato con i cluster di hello specificato esiste.    

### <a name="how-tooassociate-additional-storage-accounts-tooyour-hdinsight-cluster"></a>Come tooassociate aggiuntive gli account di archiviazione cluster HDInsight tooyour?
Se si utilizza un HDInsight Cluster (BYOC - portare il proprio Cluster), vedere hello seguenti argomenti:

* [Uso di un cluster HDInsight con account di archiviazione e metastore alternativi][hdinsight-alternate-storage]
* [Usare account di archiviazione aggiuntivi con HDInsight Hive][hdinsight-alternate-storage-2]

Se si utilizza un cluster su richiesta che viene creato dal servizio Data Factory di hello, specificare l'account di archiviazione aggiuntivi per hello HDInsight servizio collegato in modo che il servizio di Data Factory hello può registrare per conto dell'utente. Nella definizione JSON per il servizio collegato su richiesta hello hello, utilizzare **additionalLinkedServiceNames** gli account di archiviazione alternativo toospecify di proprietà come illustrato nel seguente frammento di codice JSON hello:

```JSON
{
    "name": "MyHDInsightOnDemandLinkedService",
    "properties":
    {
        "type": "HDInsightOnDemandLinkedService",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "LinkedService-SampleData",
            "additionalLinkedServiceNames": [ "otherLinkedServiceName1", "otherLinkedServiceName2" ]
        }
    }
}
```
Nell'esempio hello sopra, otherLinkedServiceName1 e otherLinkedServiceName2 rappresentano servizi collegati, le cui definizioni contengono credenziali hello account di archiviazione alternativo tooaccess esigenze cluster HDInsight.

## <a name="slices---faq"></a>Sezioni - Domande frequenti
### <a name="why-are-my-input-slices-not-in-ready-state"></a>Perché le sezioni di input non sono in stato Pronto?
Un errore comune è l'impostazione non **esterno** proprietà troppo**true** su hello input set di dati quando i dati di input hello è data factory di toohello esterno (non prodotte da data factory di hello).

Nell'esempio seguente di hello, è necessario solo tooset **esterno** tootrue su **dataset1**.  

**DataFactory1** Pipeline 1: dataset1 -&gt; activity1 -&gt; dataset2 -&gt; activity2 -&gt; dataset3 Pipeline 2: dataset3-&gt; activity3 -&gt; dataset4

Se si dispone di un altro data factory di con una pipeline che accetta dataset4 (prodotto dalla pipeline 2 nella data factory, 1), contrassegnare dataset4 come un set di dati esterno perché hello set di dati viene generato da una factory di dati diversi (DataFactory1, non DataFactory2).  

**DataFactory2**    
Pipeline 1: dataset4->activity4->dataset5

Se hello esterno sia correttamente impostata, verificare se i dati di input hello è presente nel percorso di hello specificato nella definizione del set di dati input hello.

### <a name="how-toorun-a-slice-at-another-time-than-midnight-when-hello-slice-is-being-produced-daily"></a>Come una sezione in un secondo momento alla mezzanotte quando sezione hello è siano prodotte giornalmente toorun?
Hello utilizzare **offset** proprietà toospecify hello ora in cui si desidera hello sezione toobe prodotti. Per altre informazioni su questa proprietà, vedere [Disponibilità dei set di dati](data-factory-create-datasets.md#dataset-availability) . Di seguito è riportato un rapido esempio:

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
Inizio delle sezioni giornaliere in **6: 00** anziché a mezzanotte predefinito hello.     

### <a name="how-can-i-rerun-a-slice"></a>Come si riesegue una sezione?
È possibile eseguire di nuovo una sezione in uno dei seguenti modi hello:

* Utilizzare una finestra attività di toorerun monitorare e gestire App o sezione. Per istruzioni, vedere la sezione [Rieseguire finestre attività selezionate](data-factory-monitor-manage-app.md#perform-batch-actions) .   
* Fare clic su **eseguire** nella barra dei comandi hello in hello **sezione dati** pannello sezione hello hello portale di Azure.
* Eseguire **Set AzureRmDataFactorySliceStatus** cmdlet con stato impostato troppo**in attesa** per sezione hello.   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
Vedere [Set AzureRmDataFactorySliceStatus] [ set-azure-datafactory-slice-status] per informazioni dettagliate sui cmdlet di hello.

### <a name="how-long-did-it-take-tooprocess-a-slice"></a>La modalità tempo tooprocess una sezione?
Utilizzare Esplora risorse attività tooknow Monitor e App di gestire il tempo impiegato tooprocess una sezione di dati. Per informazioni dettagliate, vedere la sezione [Activity Window Explorer](data-factory-monitor-manage-app.md#activity-window-explorer) (Esplora finestre attività).

È inoltre possibile eseguire hello seguente in hello portale di Azure:  

1. Fare clic su **set di dati** riquadro hello **DATA FACTORY** pannello per il data factory.
2. Fare clic su set di dati specifico hello in hello **set di dati** blade.
3. Sezione selezionare hello che si è interessati da hello **sezioni recenti** elenco hello **tabella** blade.
4. Fare clic sull'attività hello eseguire da hello **esecuzioni di attività** elenco hello **sezione dati** blade.
5. Fare clic su **proprietà** riquadro hello **Dettagli esecuzione attività** blade.
6. Dovrebbe essere hello **durata** campo con un valore. Questo valore è una porzione di hello tooprocess tempo hello.   

### <a name="how-toostop-a-running-slice"></a>Come toostop una sezione in esecuzione?
Se è necessario pipeline hello toostop l'esecuzione, è possibile utilizzare [Suspend AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) cmdlet. Attualmente, la sospensione di pipeline hello non arresta esecuzioni di sezione hello in corso. Una volta terminato di esecuzioni in corso di hello, non sezioni aggiuntive vengono prelevati.

Se si vuole toostop tutte le esecuzioni hello immediatamente, hello solo modo sarebbe toodelete hello pipeline e crearne uno nuovo. Se si sceglie di pipeline hello toodelete, non occorre toodelete tabelle e i servizi collegati utilizzati dalla pipeline hello.

[create-factory-using-dotnet-sdk]: data-factory-create-data-factories-programmatically.md
[msdn-class-library-reference]: /dotnet/api/microsoft.azure.management.datafactories.models
[msdn-rest-api-reference]: /rest/api/datafactory/

[adf-powershell-reference]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/azurerm.datafactories
[azure-portal]: http://portal.azure.com
[set-azure-datafactory-slice-status]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/set-azurermdatafactoryslicestatus

[adf-pricing-details]: http://go.microsoft.com/fwlink/?LinkId=517777
[hdinsight-supported-regions]: http://azure.microsoft.com/pricing/details/hdinsight/
[hdinsight-alternate-storage]: http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx
[hdinsight-alternate-storage-2]: http://blogs.msdn.com/b/cindygross/archive/2014/05/05/use-additional-storage-accounts-with-hdinsight-hive.aspx
