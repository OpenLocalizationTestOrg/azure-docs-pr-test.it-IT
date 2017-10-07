---
title: aaaMove dati da un tooSQL di SQL Server on-premise Azure con Data Factory di Azure | Documenti Microsoft
description: "Consente di impostare una pipeline ADF che riunisce due attività di migrazione di dati che spostano i dati su base giornaliera insieme tra i database locali e nel cloud hello."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a>Spostare i dati da un tooSQL di server SQL Azure con Data Factory di Azure in locale
Questo argomento viene illustrato come toomove dati da un tooa di Database di SQL Server on-premise Database di SQL Azure tramite archiviazione Blob di Azure utilizzando hello Azure Data Factory (ADF).

Per una tabella che riepiloga le varie opzioni per lo spostamento dati tooan Database SQL di Azure, vedere [spostare dati tooan Database SQL di Azure per Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).

## <a name="intro"></a>Introduzione: Che cos'è Azure Data factory e quando deve essere utilizzato toomigrate dati?
Data Factory di Azure è un servizio di integrazione di dati basato su cloud completamente gestito che Orchestra e automatizza lo spostamento di hello e trasformazione dei dati. concetto chiave Hello modello ADF hello è pipeline. Una pipeline è un raggruppamento logico delle attività, ognuna delle quali definisce hello azioni tooperform sui dati hello contenuti nel set di dati. Servizi collegati sono le informazioni di hello toodefine utilizzati necessarie per le risorse di dati di Data Factory tooconnect toohello.

Con Azure Data factory, i servizi di elaborazione dei dati esistenti possono essere composte in pipeline di dati che sono gestiti e a disponibilità elevata nel cloud hello. Queste pipeline di dati possono essere pianificati tooingest, preparare, trasformare, analizzare e pubblicare i dati e file ADF gestisce e gestisce dati complessi hello e dipendenze di elaborazione. Le soluzioni possono essere cloud hello rapidamente compilato e distribuito in, la connessione a un numero crescente di on-premise e origini dati cloud.

Considerare l'uso di ADF:

* Quando dati esigenze toobe continuamente la migrazione in uno scenario ibrido che consente di accedere sia in locale e risorse cloud
* Quando viene sottoposto a transazione dati hello o esigenze toobe modificato o dispone di logica di business aggiunto tooit quando viene eseguita la migrazione.

ADF consente hello pianificazione e monitoraggio dei processi utilizzando semplici script JSON che gestiscono lo spostamento di hello dei dati su base periodica. ADF dispone anche di altre funzionalità quali il supporto di operazioni complesse. Per ulteriori informazioni sulla data factory di AZURE, vedere la documentazione di hello in [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).

## <a name="scenario"></a>Hello Scenario
Si configura una pipeline ADF che compone due attività di migrazione dei dati. Insieme passano dati su base giornaliera tra un database SQL locale e un Database di SQL Azure nel cloud hello. Hello due attività sono:

* copiare i dati da un tooan di database di SQL Server on-premise account di archiviazione Blob di Azure
* copiare i dati da tooan account di archiviazione Blob di Azure hello Database SQL di Azure.

> [!NOTE]
> eseguire i passaggi illustrati di seguito sono state adattate da hello dettagliate esercitazione fornito dal team ADF hello Hello: [spostare dati tra origini locali e cloud con Gateway di gestione dati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) fa riferimento a toohello sezioni rilevanti dell'argomento vengono forniti quando appropriato.
>
>

## <a name="prereqs"></a>Prerequisiti
Il tutorial presuppone:

* Una **sottoscrizione di Azure**. Se non si ha una sottoscrizione, è possibile iscriversi per provare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Un **account di archiviazione Azure**. Utilizzare un account di archiviazione di Azure per archiviare i dati di hello in questa esercitazione. Se non si dispone di un account di archiviazione di Azure, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo. Dopo aver creato l'account di archiviazione hello, è necessario account hello tooobtain chiave utilizzata l'archiviazione di hello tooaccess. Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Accesso tooan **Database SQL di Azure**. Se è necessario impostare un Database SQL di Azure, hello tpoic [Guida introduttiva a Database SQL di Microsoft Azure ](../sql-database/sql-database-get-started.md) fornisce informazioni su come tooprovision una nuova istanza di un Database di SQL Azure.
* Installazione e configurazione di **Azure PowerShell** in locale. Per istruzioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

> [!NOTE]
> Questa procedura utilizza hello [portale di Azure](https://portal.azure.com/).
>
>

## <a name="upload-data"></a>Caricamento hello dati tooyour SQL Server locale
Utilizziamo hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate processo di migrazione hello. Hello NYC Taxi set di dati è disponibile, come indicato in questo post, nell'archiviazione blob di Azure [NYC Taxi dati](http://www.andresmh.com/nyctaxitrips/). dati Hello dispone di due file, file di trip_data.csv hello, che contiene i dettagli di andata e ritorno, e file di trip_far.csv hello, che contiene i dettagli della tariffa di hello pagata per ogni itinerario. Un esempio e una descrizione di questi file sono inclusi in [Descrizione del set di dati relativo alle corse dei taxi di NYC](machine-learning-data-science-process-sql-walkthrough.md#dataset).

È possibile adattare hello procedura qui tooa set di dati personalizzati o seguire i passaggi di hello, come descritto utilizzando hello NYC Taxi set di dati. hello tooupload NYC Taxi set di dati nel database di SQL Server locale, attenersi alla procedura hello [importazione Bulk dei dati nel Database di SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload). Queste istruzioni sono valide per un Server SQL in una macchina virtuale di Azure, ma procedure hello per il caricamento toohello on-premise SQL Server è hello stesso.

## <a name="create-adf"></a> Creare un data factory di Azure
istruzioni per la creazione di una nuova Data Factory di Azure e un gruppo di risorse in hello Hello [portale di Azure](https://portal.azure.com/) forniti [creare una Data Factory di Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory). Nome hello nuova ADF istanza *adfdsp* e nome gruppo di risorse di hello creato *adfdsprg*.

## <a name="install-and-configure-up-hello-data-management-gateway"></a>Installare e configurare il backup hello Gateway di gestione dati
tooenable le pipeline in toowork un factory di dati di Azure con un Server SQL locale, è necessario tooadd come una data factory toohello servizio collegato. toocreate un servizio collegato per un Server SQL locale, è necessario:

* scaricare e installare il Gateway di gestione dati Microsoft nel computer locale hello.
* configurare il servizio collegato hello per gateway di hello locale dati origine toouse hello.

Hello Gateway di gestione dati serializza e deserializza i dati di origine e sink hello computer hello in cui è ospitato.

Per le istruzioni di configurazione e i dettagli sul Gateway di gestione dati, vedere [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)

## <a name="adflinkedservices"></a>Creare servizi collegati tooconnect toohello risorse di dati
Un servizio collegato definisce informazioni di hello necessarie per la risorsa di Azure Data Factory tooconnect tooa dati. viene fornita la procedura dettagliata per la creazione di servizi collegati Hello in [creare i servizi collegati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).

Sono disponibili tre risorse in questo scenario per il quale sono necessari servizi collegati.

1. [Servizio collegato per SQL Server locale](#adf-linked-service-onprem-sql)
2. [Servizio collegato per archiviazione BLOB di Azure](#adf-linked-service-blob-store)
3. [Servizio collegato per il database SQL Azure](#adf-linked-service-azure-sql)

### <a name="adf-linked-service-onprem-sql"></a>Servizio collegato per il database SQL Server locale
servizio collegato hello toocreate per hello locale SQL Server:

* Fare clic su hello **archivio dati** nella pagina di destinazione ADF hello nel portale classico di Azure
* Selezionare **SQL** e immettere hello *username* e *password* le credenziali per hello on-premise SQL Server. È necessario tooenter hello servername come un **servername completo barra rovesciata nome dell'istanza (nomeserver\nomeistanza)**. Servizio collegato hello nome *adfonpremsql*.

### <a name="adf-linked-service-blob-store"></a>Servizi collegati per BLOB
toocreate hello servizio collegato per l'account di archiviazione Blob di Azure hello:

* Fare clic su hello **archivio dati** nella pagina di destinazione ADF hello nel portale classico di Azure
* selezionare **Account di archiviazione di Azure**
* Immettere hello archiviazione Blob di Azure contenitore chiave e il nome dell'account. Hello Nome servizio collegato *adfds*.

### <a name="adf-linked-service-azure-sql"></a>Servizio collegato per il database SQL Azure
toocreate hello servizio collegato per hello Database SQL di Azure:

* Fare clic su hello **archivio dati** nella pagina di destinazione ADF hello nel portale classico di Azure
* Selezionare **SQL Azure** e immettere hello *username* e *password* le credenziali per hello Database SQL di Azure. Hello *username* deve essere specificato come  *user@servername* .   

## <a name="adf-tables"></a>Definire e creare tabelle toospecify come tooaccess hello set di dati
Creare tabelle che specificano struttura hello, posizione e la disponibilità dei set di dati hello con hello procedure basato su script. File JSON vengono usati toodefine hello tabelle. Per ulteriori informazioni sulla struttura hello di questi file, vedere [set di dati](../data-factory/data-factory-create-datasets.md).

> [!NOTE]
> È consigliabile eseguire hello `Add-AzureAccount` cmdlet prima di eseguire hello [New AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm cmdlet che hello sottoscrizione di Azure a destra è selezionata per l'esecuzione del comando hello. Per la documentazione di questo cmdlet, vedere [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).
>
>

le definizioni di basato su JSON di Hello nelle tabelle di hello utilizzare hello seguenti nomi:

* Hello **nome tabella** hello on-premise SQL server è *nyctaxi_data*
* Hello **nome contenitore** in hello archiviazione Blob di Azure è l'account *containername*  

Per questa pipeline ADF sono necessarie tre definizioni di tabella:

1. [Tabella SQL locale](#adf-table-onprem-sql)
2. [Tabella BLOB ](#adf-table-blob-store)
3. [Tabella SQL Azure](#adf-table-azure-sql)

> [!NOTE]
> Queste procedure utilizzano toodefine Azure PowerShell e creare hello attività ADF. Tuttavia, queste attività possono inoltre essere eseguite utilizzando hello portale di Azure. Per informazioni dettagliate, vedere [Creare set di dati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).
>
>

### <a name="adf-table-onprem-sql"></a>Tabella SQL locale
definizione della tabella Hello per hello on-premise SQL Server specificato nel seguente file JSON hello:

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

non sono inclusi i nomi di colonna Hello. È possibile selezionare i nomi di colonna hello Sub includendoli qui (per dettagli, vedere hello [documentazione ADF](../data-factory/data-factory-data-movement-activities.md) argomento.

Copiare definizione JSON hello della tabella hello in un file denominato *onpremtabledef.json* file e salvarlo tooa percorso noto (di seguito si presuppone che toobe *C:\temp\onpremtabledef.json*). Creare tabella hello in ADF con hello cmdlet di Azure PowerShell seguente:

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a>Tabella BLOB
Definizione per la tabella hello per hello output blob si trova nella seguente hello (esegue il mapping dei dati di caricamento hello dal blob tooAzure locale):

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

Copiare definizione JSON hello della tabella hello in un file denominato *bloboutputtabledef.json* file e salvarlo tooa percorso noto (di seguito si presuppone che toobe *C:\temp\bloboutputtabledef.json*). Creare tabella hello in ADF con hello cmdlet di Azure PowerShell seguente:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sq"></a>Tabella SQL Azure
Definizione di tabella hello per SQL Azure di output di hello è seguito hello (questo schema Associa dati hello provenienti dal blob hello):

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

Copiare definizione JSON hello della tabella hello in un file denominato *AzureSqlTable.json* file e salvarlo tooa percorso noto (di seguito si presuppone che toobe *C:\temp\AzureSqlTable.json*). Creare tabella hello in ADF con hello cmdlet di Azure PowerShell seguente:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a>Definire e creare pipeline hello
Specificare le attività di hello appartenenti toohello della pipeline e creare pipeline hello con hello procedure basato su script. Un file JSON è toodefine usate le proprietà della pipeline di hello.

* Hello script si presuppone che hello **nome pipeline** è *AMLDSProcessPipeline*.
* Si noti inoltre che è impostata la periodicità hello di hello pipeline toobe eseguito su ogni giorno base e utilizzare hello tempo di esecuzione predefinito per il processo di hello (12 am UTC).

> [!NOTE]
> Hello procedure riportate di seguito utilizzano toodefine Azure PowerShell e creare pipeline ADF hello. Tuttavia, questa attività può inoltre essere eseguita tramite il portale di Azure. Per informazioni dettagliate, vedere [Creare una pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).
>
>

Utilizzo di definizioni di tabella hello fornito in precedenza, definizione di pipeline hello per hello che ADF viene specificata come segue:

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

Copiare questa definizione JSON della pipeline hello in un file denominato *pipelinedef.json* file e salvarlo tooa percorso noto (di seguito si presuppone che toobe *C:\temp\pipelinedef.json*). Creare pipeline hello in ADF con hello cmdlet di Azure PowerShell seguente:

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

Confermare che è possibile visualizzare pipeline hello in hello ADF nel portale di Azure classico hello visualizzati come riportato di seguito (quando si fa clic su diagramma hello)

![Pipeline ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <a name="adf-pipeline-start"></a>Avviare hello Pipeline
è possibile eseguire pipeline Hello utilizzando hello comando seguente:

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

Hello *startdate* e *enddate* i valori di parametro devono toobe sostituito con date effettive di hello tra i quali si desidera toorun pipeline hello.

Una volta che viene eseguita la pipeline hello, si dovrebbe essere in grado di toosee hello dati visualizzati nel contenitore hello selezionati per il blob hello, un file per ogni giorno.

Si noti che non è stato sfruttato funzionalità hello fornita dai dati toopipe ADF in modo incrementale. Per ulteriori informazioni su come toodo questa e altre funzionalità fornite da Azure Data factory, vedere hello [documentazione ADF](https://azure.microsoft.com/services/data-factory/).
