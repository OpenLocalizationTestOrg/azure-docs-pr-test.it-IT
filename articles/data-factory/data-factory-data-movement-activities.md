---
title: "dati aaaMove tramite attività di copia | Documenti Microsoft"
description: "Informazioni sullo spostamento di dati in pipeline di Data Factory: migrazione di dati tra archivi cloud e tra archivi locali e cloud. Usare l'attività di copia."
keywords: copiare dati, spostamento di dati, migrazione di dati, trasferire dati
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 67543a20-b7d5-4d19-8b5e-af4c1fd7bc75
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 29b74154b9006795ead3b0ee9638a3dbf2c5d831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-by-using-copy-activity"></a>Spostare dati con l'attività di copia
## <a name="overview"></a>Panoramica
In Data Factory di Azure, è possibile utilizzare dati di attività di copia toocopy tra sedi locali e cloud archivi dati. Dopo aver copiato i dati di hello, può essere ulteriormente trasformato e analizzato. È anche possibile utilizzare trasformazione toopublish attività di copia e i risultati dell'analisi per business intelligence (BI) e il consumo di applicazione.

![Ruolo dell'attività di copia](media/data-factory-data-movement-activities/copy-activity.png)

L'attività di copia è un servizio [disponibile a livello globale](#global)sicuro, affidabile e scalabile. Questo articolo fornisce informazioni dettagliate sullo spostamento dei dati in Data factory e sull'attività di copia.

Prima di tutto, verrà illustrato come avviene la migrazione dei dati tra due archivi dati cloud e tra un archivio dati locale e un archivio dati cloud.

> [!NOTE]
> in generale, vedere toolearn sulle attività [informazioni sulle pipeline e attività](data-factory-create-pipelines.md).
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a>Copiare dati tra due archivi dati cloud
Quando gli archivi di dati di origine e sink sono nel cloud hello, attività di copia passa attraverso hello seguente dati toocopy fasi dal sink di toohello origine hello. servizio Hello che consente di creare attività di copia:

1. Legge i dati dall'archivio dati di origine hello.
2. Esegue la serializzazione/deserializzazione, compressione/decompressione, il mapping di colonne e la conversione dei tipi. Esegue queste operazioni in base alle configurazioni di hello del set di dati input hello, set di dati di output e attività di copia.
3. Scrive l'archivio dati di destinazione toohello di dati.

servizio Hello sceglie automaticamente lo spostamento dei dati di hello area ottimale tooperform hello. Quest'area è in genere hello uno più vicino toohello sink archivio dati.

![Copia da cloud a cloud](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Copiare dati tra un archivio dati locale e un archivio dati cloud
toosecurely spostare i dati tra un archivio dati locale e un archivio dati cloud, installare il Gateway di gestione dati nel computer locale. Il Gateway di gestione dati è un agente che consente lo spostamento e l'elaborazione ibridi dei dati. È possibile installarlo in hello stesso computer come archiviano i dati hello stesso o in un computer separato che dispone di accesso ai dati toohello archivio.

In questo scenario, il Gateway di gestione di dati esegue hello. serializzazione/deserializzazione, compressione/decompressione, mapping colonne e conversione di tipi. Dati non transita attraverso hello servizio Azure Data Factory. In alternativa, Gateway di gestione dati scrive direttamente hello dati toohello destinazione archivio.

![Copia da locale a cloud](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

Per un'introduzione e una procedura dettagliata, vedere [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) . Per informazioni dettagliate sull'agente, vedere [Gateway di gestione dati](data-factory-data-management-gateway.md) .

È inoltre possibile spostare i dati da / toosupported gli archivi dati di cui sono ospitati nelle macchine virtuali IaaS di Azure (VM) tramite il Gateway di gestione di dati. In questo caso, è possibile installare il Gateway di gestione di dati in hello stessa macchina virtuale come archiviano i dati hello stesso o in una macchina virtuale separata che dispone di accesso ai dati toohello archivio.

## <a name="supported-data-stores-and-formats"></a>Archivi dati e formati supportati
Attività di copia in Data Factory copia dati da un archivio dati di origine dati archivio tooa sink. Data Factory supporta hello seguenti archivi dati. È possibile scrivere dati da qualsiasi origine tooany sink. Fare clic su un toolearn archivio dati come toocopy tooand di dati dall'archivio.

> [!NOTE] 
> Se è necessario toomove i dati in o da un archivio dati che non supporta attività di copia, utilizzare un **attività personalizzata** in Data Factory con la logica personalizzata per la copia o spostamento di dati. Per i dettagli sulla creazione e l'uso di un'attività personalizzata, vedere l'articolo [Usare attività personalizzate in una pipeline di Azure Data Factory](data-factory-use-custom-activities.md).

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Archivia i dati con * può essere locale o in Azure IaaS e richiedono tooinstall [Gateway di gestione dati](data-factory-data-management-gateway.md) in un computer di IaaS in locale o Azure.

### <a name="supported-file-formats"></a>Formati di file supportati
È possibile utilizzare anche attività di copia**copiare i file come-è** tra archivi due dati basati su file, è possibile ignorare hello [formattare sezione](data-factory-create-datasets.md) in hello input sia le definizioni di set di dati di output. dati Hello viene copiati in modo efficiente senza qualsiasi serializzazione/deserializzazione.

Attività di copia inoltre legge e scrive toofiles in formati specificati: **JSON, testo, Avro, ORC e Parquet**e codec di compressione **GZip, Deflate, BZip2 e ZipDeflate** sono supportati. Vedere [Formati di compressione e file supportati](data-factory-supported-file-and-compression-formats.md) per i dettagli.

Ad esempio, è possibile eseguire seguente hello Copia attività:

* Copiare i dati nel Server SQL locale e scrivere archivio Data Lake di tooAzure nel formato ORC.
* Copia i file in formato testo (CSV) dal File System di on-premise e scrivere tooAzure Blob nel formato Avro.
* Copiare i file compressi dal File System di on-premise e decomprimere quindi inserite archivio tooAzure Data Lake.
* Copiare i dati in formato testo compresso (CSV) GZip da Blob di Azure e scrivere tooAzure Database SQL.

## <a name="global"></a>Spostamento dei dati disponibile a livello globale
Data Factory di Azure è disponibile solo in aree di Stati Uniti occidentali, Stati Uniti orientali ed Europa settentrionale hello. Tuttavia, hello servizio che consente di creare attività di copia è disponibile a livello globale in hello seguendo le aree e aree geografiche. topologia disponibili globalmente Hello garantisce lo spostamento dei dati efficiente che consente di evitare in genere hop tra aree. Per la disponibilità del servizio Data Factory e lo spostamento dei dati in un'area, vedere [Servizi in base all'area](https://azure.microsoft.com/regions/#services) .

### <a name="copy-data-between-cloud-data-stores"></a>Copiare dati tra archivi dati cloud
Quando gli archivi di dati di origine e sink sono nel cloud hello, Data Factory utilizza una distribuzione del servizio nell'area di hello sink toohello più vicino in hello stessi dati di hello toomove geography. Fare riferimento toohello per il mapping nella tabella seguente:

| Geography di archivi dati di destinazione hello | Area dell'archivio dati di destinazione hello | Area usata per lo spostamento dei dati |
|:--- |:--- |:--- |
| Stati Uniti | Stati Uniti orientali | Stati Uniti orientali |
| &nbsp; | Stati Uniti orientali 2 | Stati Uniti orientali 2 |
| &nbsp; | Stati Uniti centrali | Stati Uniti centrali |
| &nbsp; | Stati Uniti centro-settentrionali | Stati Uniti centro-settentrionali |
| &nbsp; | Stati Uniti centro-meridionali | Stati Uniti centro-meridionali |
| &nbsp; | Stati Uniti centro-occidentali | Stati Uniti centro-occidentali |
| &nbsp; | Stati Uniti occidentali | Stati Uniti occidentali |
| &nbsp; | Stati Uniti occidentali 2 | Stati Uniti occidentali |
| Canada | Canada orientale | Canada centrale |
| &nbsp; | Canada centrale | Canada centrale |
| Brasile | Brasile meridionale | Brasile meridionale |
| Europa | Europa settentrionale | Europa settentrionale |
| &nbsp; | Europa occidentale | Europa occidentale |
| Regno Unito | Regno Unito occidentale | Regno Unito meridionale |
| &nbsp; | Regno Unito meridionale | Regno Unito meridionale |
| Asia/Pacifico | Asia sudorientale | Asia sudorientale |
| &nbsp; | Asia orientale | Asia sudorientale |
| Australia | Australia orientale | Australia orientale |
| &nbsp; | Australia sudorientale | Australia sudorientale |
| Giappone | Giappone orientale | Giappone orientale |
| &nbsp; | Giappone occidentale | Giappone orientale |
| India | India centrale | India centrale |
| &nbsp; | India occidentale | India centrale |
| &nbsp; | India meridionale | India centrale |

In alternativa, è possibile indicare in modo esplicito area hello della Data Factory servizio toobe utilizzati tooperform hello copia specificando `executionLocation` proprietà nelle attività di copia `typeProperties`. I valori supportati per questa proprietà sono elencati nella colonna **Area usata per lo spostamento dei dati** precedente. Si noti come che i dati passa attraverso tale area nel transito hello durante la copia. Ad esempio, toocopy tra Azure archivia in Corea, è possibile specificare `"executionLocation": "Japan East"` tooroute tramite area Giappone (vedere [JSON di esempio](#by-using-json-scripts) come riferimento).

> [!NOTE]
> Se l'area hello di hello archivio dati di destinazione non è presente nell'elenco precedente o non rilevabili, per impostazione predefinita attività di copia ha esito negativo anziché passare attraverso un'area alternativa, a meno che non `executionLocation` specificato. verrà espanso l'elenco di regioni Hello è supportato nel tempo.
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Copiare dati tra un archivio dati locale e un archivio dati cloud
Quando i dati vengono copiati da archivi locali (o macchina virtuale Azure/IaaS) ad archivi cloud, lo spostamento dei dati viene eseguito dal [Gateway di gestione dati](data-factory-data-management-gateway.md) su un computer locale o una macchina virtuale. Hello non del flusso di dati tramite il servizio di hello in cloud hello, a meno che non si utilizza hello [staging copia](data-factory-copy-activity-performance.md#staged-copy) funzionalità. In questo caso, i dati passano attraverso hello archiviazione Blob di Azure di gestione temporanea prima che vengano scritti nell'archivio dati di hello sink.

## <a name="create-a-pipeline-with-copy-activity"></a>Creare una pipeline con attività di copia
È possibile creare una pipeline con l'attività di copia in alcuni modi:

### <a name="by-using-hello-copy-wizard"></a>Tramite Copia guidata hello
Hello Data Factory Copia guidata consente di toocreate una pipeline con attività di copia. Questa pipeline consente toocopy dati da origini supportate toodestinations *senza scrivere JSON* le definizioni per i servizi collegati, i set di dati e pipeline. Vedere [Data Factory Copia guidata](data-factory-copy-wizard.md) per informazioni dettagliate sulla procedura guidata hello.  

### <a name="by-using-json-scripts"></a>Con gli script JSON
È possibile utilizzare Editor delle Data Factory in hello portale di Azure, Visual Studio o Azure PowerShell toocreate una definizione JSON per una pipeline (utilizzando l'attività di copia). Quindi, è possibile distribuire la pipeline hello toocreate in Data Factory. Per un'esercitazione con istruzioni dettagliate, vedere [Esercitazione: Copiare dati da un archivio BLOB al database SQL usando Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .    

Per tutti i tipi di attività sono disponibili proprietà JSON come nome, descrizione, tabelle di input e output e criteri. Le proprietà disponibili in hello `typeProperties` sezione dell'attività hello variano in base a ogni tipo di attività.

Per attività di copia, hello `typeProperties` sezione varia a seconda dei tipi di hello delle origini e sink. Fare clic su un'origine/sink di hello [origini e sink supportati](#supported-data-stores-and-formats) toolearn sezione sulle proprietà del tipo che supporta attività di copia per l'archivio dati.

Di seguito è riportata una definizione JSON di esempio:

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputBlobTable"
          }
        ],
        "outputs": [
          {
            "name": "OutputSQLTable"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          },
          "executionLocation": "Japan East"          
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
}
```
pianificazione Hello è definito in hello output di set di dati determina l'esecuzione di attività hello (ad esempio: **giornaliero**, frequenza come **giorno**e l'intervallo come **1**). Hello attività Copia i dati da un set di dati di input (**origine**) set di dati di output tooan (**sink**).

È possibile specificare più di un set di dati input tooCopy attività. Sono utilizzati tooverify hello dipendenze prima di eseguire attività hello. Tuttavia, solo i dati di hello dal primo set di dati hello sono copiato toohello dataset di destinazione. Per altre informazioni, vedere [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md).  

## <a name="performance-and-tuning"></a>Prestazioni e ottimizzazione
Vedere hello [ottimizzazione Guida e alle prestazioni di attività di copia](data-factory-copy-activity-performance.md), che descrive i fattori principali che influiscono sulle prestazioni di hello spostamento dei dati (attività di copia) in Azure Data Factory. Inoltre, elenca hello osservata le prestazioni durante il test interno e vengono illustrati vari modi toooptimize hello rendimento attività di copia.

## <a name="fault-tolerance"></a>Tolleranza di errore
Per impostazione predefinita, l'attività di copia verrà interrotta la copia di dati e restituire un errore quando rilevano dati incompatibili tra origine e sink; Sebbene sia possibile configurare in modo esplicito tooskip e le righe non compatibile di log hello e copia solo tali copia di dati compatibili toomake hello ha avuto esito positivo. Vedere hello [tolleranza di errore delle attività di copia](data-factory-copy-activity-fault-tolerance.md) ulteriori dettagli.

## <a name="security-considerations"></a>Considerazioni relative alla sicurezza
Vedere hello [considerazioni sulla sicurezza](data-factory-data-movement-security-considerations.md), che descrive l'infrastruttura di sicurezza che i servizi lo spostamento dei dati in Azure Data Factory utilizzare toosecure i dati.

## <a name="scheduling-and-sequential-copy"></a>Pianificazione e copia sequenziale
Vedere [Pianificazione ed esecuzione con Data Factory](data-factory-scheduling-and-execution.md) per informazioni dettagliate sul funzionamento della pianificazione e dell'esecuzione in Data Factory. È possibile toorun più operazioni di copia uno dopo l'altro in modo sequenziale o ordinato. Vedere hello [copiare in sequenza](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) sezione.

## <a name="type-conversions"></a>Conversioni di tipi
Gli archivi dati provengono tutti da uno specifico sistema di tipi nativo. Attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi:

1. Convertire dal tipo .NET tooa tipi di origine nativa.
2. Convertire un tipo di sink native tooa tipo .NET.

mapping di Hello da un tipo .NET di tipo nativo del sistema tooa per un archivio dati è hello rispettivi dati archivio dell'articolo. (Fare clic sul collegamento di specifiche hello in hello [supportati archivi dati](#supported-data-stores) tabella). È possibile utilizzare questi tipi di mapping toodetermine appropriato durante la creazione delle tabelle, in modo che l'attività di copia esegue conversioni di destra hello.

## <a name="next-steps"></a>Passaggi successivi
* vedere toolearn sulle attività di copia più, hello [copiare i dati da tooAzure di archiviazione Blob di Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* toolearn sullo spostamento dei dati da un locale archivio tooa cloud dati archivio dati, vedere [spostare i dati da archivi di dati locali toocloud](data-factory-move-data-between-onprem-and-cloud.md).
