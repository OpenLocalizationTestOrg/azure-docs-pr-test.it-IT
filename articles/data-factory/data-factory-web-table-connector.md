---
title: aaaMove dati dalla tabella di Web usando Azure Data Factory | Documenti Microsoft
description: Informazioni su come pagine di dati toomove da una tabella in un sito Web usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a>Spostare i dati da un'origine tabella Web con Azure Data Factory
In questo articolo descrive come toouse hello attività di copia dei dati toomove Data Factory di Azure da una tabella in una pagina Web di tooa supportato archivio dati sink. In questo articolo si basa su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo che presenta una panoramica generale di spostamento dei dati con l'elenco di attività e hello copia di archivi dati supportata come origine/sink.

Data factory di attualmente supporta solo lo spostamento dei dati da un server di dati Web tabella tooother Archivia, ma non lo spostamento dei dati da altri dati archivia tooa Web tabella di destinazione.

> [!IMPORTANT]
> Questo connettore Web attualmente supporta soltanto l'estrazione del contenuto della tabella da una pagina HTML. tooretrieve dei dati da un endpoint HTTP/s, utilizzare [connettore HTTP](data-factory-http-connector.md) invece.

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API. 

- toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati. 
- È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. 
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per un esempio con le definizioni di JSON per le entità Data Factory toocopy utilizzati dati da una tabella web, vedere [esempio JSON: copiare i dati dalla tabella di Web tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che siano utilizzati toodefine Data Factory entità specifiche tooa Web tabella:

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente fornisce una descrizione del servizio specifico tooWeb collegati gli elementi JSON.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **Web** |Sì |
| Url |Origine di URL toohello Web |Sì |
| authenticationType |Anonimo. |Sì |

### <a name="using-anonymous-authentication"></a>Uso dell'autenticazione anonima

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. sezione Hello typeProperties per set di dati di tipo **tabella Web** ha hello seguenti proprietà

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type |tipo di set di dati hello. deve essere impostato troppo**tabella Web** |Sì |
| path |Una risorsa relativa di URL toohello che contiene la tabella hello. |No. Quando non viene specificato alcun percorso, viene utilizzato solo URL hello specificato nella definizione di servizio collegato hello. |
| index |indice di Hello della tabella hello nella risorsa hello. Vedere [indice Get di una tabella in una pagina HTML](#get-index-of-a-table-in-an-html-page) sezione per indice toogetting passaggi di una tabella in una pagina HTML. |Sì |

**Esempio:**

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

Attualmente, quando origine hello in attività di copia è di tipo **WebSource**, non sono supportate proprietà aggiuntive.


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a>Esempio JSON: copiare i dati dalla tabella di Web tooAzure Blob
Hello nel seguente esempio viene illustrato:

1. Un servizio collegato di tipo [Web](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [WebTable](#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [WebSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati da un tooan tabella Web blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

Hello seguente esempio mostra come blob di dati di toocopy da un tooan tabella Web Azure. Tuttavia, i dati possono essere copiati direttamente tooany di hello sink hello dichiarato nella [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo usando hello attività di copia in Azure Data Factory.

**Servizio collegato Web** in questo esempio utilizza hello Web collegato del servizio con l'autenticazione anonima. Per i diversi tipi di autenticazione disponibili, vedere la sezione [Servizio collegato Web](#linked-service-properties) .

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

**Servizio collegato Archiviazione di Azure**

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**Set di dati della tabella Web input** impostazione **esterno** troppo**true** informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività in hello factory di dati.

> [!NOTE]
> Vedere [indice Get di una tabella in una pagina HTML](#get-index-of-a-table-in-an-html-page) sezione per indice toogetting passaggi di una tabella in una pagina HTML.  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


**Set di dati di output del BLOB di Azure**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



**Pipeline con attività di copia**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**WebSource** e **sink** tipo è stato impostato troppo**BlobSink**.

Vedere [le proprietà del tipo WebSource](#copy-activity-type-properties) per elenco hello delle proprietà supportate da hello WebSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="get-index-of-a-table-in-an-html-page"></a>Ottenere l'indice di una tabella in una pagina HTML
1. Avviare **Excel 2016** e passare toohello **dati** scheda.  
2. Fare clic su **nuova Query** sulla barra degli strumenti hello, scegliere troppo**da altre origini** e fare clic su **da Web**.

    ![Menu di Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. In hello **da Web** finestra di dialogo immettere **URL** che verrebbe utilizzato nel collegamento formato JSON del servizio (ad esempio: https://en.wikipedia.org/wiki/) insieme al percorso desiderato per set di dati hello (ad esempio: AFI % 27s_100_Years... 100_Movies), fare clic su **OK**.

    ![Finestra di dialogo Da Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    URL usato in questo esempio: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies
4. Se viene visualizzato **contenuto Web di accesso** la finestra di dialogo, a destra selezionare hello **URL**, **autenticazione**, fare clic su **Connetti**.

   ![Finestra di dialogo Accedi a contenuto Web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. Fare clic su un **tabella** elemento contenuto toosee della visualizzazione albero hello dalla tabella hello e quindi fare clic su **modifica** pulsante nella parte inferiore di hello.  

   ![Finestra di dialogo Strumento di spostamento](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. In hello **Editor di Query** finestra, fare clic su **Editor avanzato** sulla barra degli strumenti hello.

    ![Pulsante Editor avanzato](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. Nella finestra di dialogo Editor avanzato hello, hello numero accanto troppo "Source" è indice di hello.

    ![Editor avanzato - Indice](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

Se si utilizza Excel 2013, utilizzare [Microsoft Power Query per Excel](https://www.microsoft.com/download/details.aspx?id=39379) indice hello tooget. Vedere [pagina web di connessione tooa](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) articolo per informazioni dettagliate. Hello passaggi sono simili se si utilizza [Microsoft Power BI per Desktop](https://powerbi.microsoft.com/desktop/).

> [!NOTE]
> colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
