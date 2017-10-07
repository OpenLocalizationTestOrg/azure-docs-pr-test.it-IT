---
title: "Attività aaaCopy ottimizzazione Guida e alle prestazioni | Documenti Microsoft"
description: "Informazioni sui fattori che influiscono sulle prestazioni di hello di trasferimento dei dati in Data Factory di Azure quando si utilizza l'attività di copia."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 4b9a6a4f-8cf5-4e0a-a06f-8133a2b7bc58
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jingwang
ms.openlocfilehash: b0fb5a76c34752d07e8ddfffbb799a05fb5d6be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-activity-performance-and-tuning-guide"></a>Guida alle prestazioni dell'attività di copia e all'ottimizzazione
L'attività di copia di Azure Data Factory offre una soluzione di caricamento dei dati di primo livello in quanto a sicurezza, affidabilità e prestazioni. Consente di toocopy decine di terabyte di dati ogni giorno in un'ampia varietà di cloud e archivi dati locali. Velocissime dati prestazioni di caricamento sono tooensure chiave, è possibile concentrarsi sul problema di "big data" hello core: compilazione di soluzioni avanzate analitica e recupero approfondite da tutti i dati.

Azure offre un set di livello aziendale soluzioni warehouse dati e archiviazione di dati e attività di copia offre un caricamento esperienza semplice tooconfigure e set di backup di dati altamente ottimizzati. Con un'unica attività di copia, è possibile ottenere:

* Caricamento dei dati in **Azure SQL Data Warehouse** a **1,2 GBps**. Per la procedura dettagliata con un caso d'uso, vedere [Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md).
* Caricamento dei dati nell'**Archiviazione BLOB di Azure** a **1 GBps**
* Caricamento dei dati in **Azure Data Lake Store** a **1 GBps**

L'articolo illustra:

* [Numeri di riferimento relativi alle prestazioni](#performance-reference) per supportati i toohelp dati archivi di origine e sink piano al progetto.
* Funzionalità che è possibile migliorare la velocità effettiva copia in diversi scenari, tra cui di hello [cloud unità lo spostamento dei dati](#cloud-data-movement-units), [parallela copia](#parallel-copy), e [staging copia](#staged-copy);
* [Indicazioni di ottimizzazione delle prestazioni](#performance-tuning-steps) su come tootune hello hello e prestazioni fattori chiave che possono influire sulla copia delle prestazioni.

> [!NOTE]
> Se non si ha familiarità con l'attività di copia in generale, vedere [Spostare dati con l'attività di copia](data-factory-data-movement-activities.md) prima di continuare a leggere l'articolo.
>

## <a name="performance-reference"></a>Informazioni di riferimento sulle prestazioni

Come riferimento, sotto la tabella Mostra numero di velocità effettiva copia hello in MBps per hello assegnato in base a test interni coppie di origine e sink. A scopo di confronto, viene illustrato anche in che modo le diverse impostazioni di [unità di spostamento dati cloud](#cloud-data-movement-units) o la [scalabilità di Gateway di gestione dati](data-factory-data-management-gateway-high-availability-scalability.md) (nodi gateway multipli) possono favorire le prestazioni di copia.

![Matrice delle prestazioni](./media/data-factory-copy-activity-performance/CopyPerfRef.png)


**Toonote punti:**
* Velocità effettiva viene calcolata utilizzando la formula seguente hello: [dimensioni dei dati letti dall'origine] / [Durata esecuzione attività di copia].
* numeri di riferimento relativi alle prestazioni Hello nella tabella hello misurati utilizzando [TPC-H](http://www.tpc.org/tpch/) set di dati di esecuzione dell'attività sola copia.
* In archivi dati di Azure, hello origine e sink presenti hello stessa area di Azure.
* Per la copia ibrida tra sedi locali e cloud archivi dati, ogni nodo gateway era in esecuzione in un computer che è stato separato dal hello dati archivio locale con sotto specifica. Durante l'esecuzione di una singola attività nel gateway, l'operazione di copia hello utilizzata solo una piccola parte della CPU, memoria o larghezza di banda di rete del computer di test hello. Vedere [Considerazioni su Gateway di gestione dati](#considerations-for-data-management-gateway).
    <table>
    <tr>
        <td>CPU</td>
        <td>Intel Xeon E5-2660 v2 da 32 core a 2,20 GHz</td>
    </tr>
    <tr>
        <td>Memoria</td>
        <td>128 GB</td>
    </tr>
    <tr>
        <td>Rete</td>
        <td>Interfaccia Internet: 10 Gbps, interfaccia Intranet: 40 Gbps</td>
    </tr>
    </table>


> [!TIP]
> È possibile ottenere una velocità effettiva mediante l'utilizzo di più unità di spostamento dei dati (DMUs) di hello predefinito massimo DMUs, ovvero 32 per eseguire un'attività di copia da cloud a cloud. Ad esempio, con 100 unità di spostamento dati è possibile copiare i dati dal BLOB di Azure in Azure Data Lake Store a **1,0 GB al secondo**. Vedere hello [unità lo spostamento dei dati Cloud](#cloud-data-movement-units) sezione per informazioni dettagliate su questa funzionalità e hello scenario è supportato. Contatto [supporto tecnico di Azure](https://azure.microsoft.com/support/) toorequest DMUs altre.

## <a name="parallel-copy"></a>Copia parallela
È possibile leggere dati da hello di origine o destinazione toohello dati scrivere **in parallelo all'interno di un'attività di copia eseguire**. Questa funzionalità migliora la velocità effettiva di hello di un'operazione di copia e riduce hello tempo toomove dati.

Questa impostazione è diversa da hello **concorrenza** proprietà nella definizione di attività hello. Hello **concorrenza** proprietà determina il numero di hello di **esegue attività di copia simultanea** tooprocess dati da windows attività differenti (1 too2 AM AM, STO too3 AM 2, 3 AM too4 e così via). Questa funzionalità è utile quando si esegue un caricamento cronologico. funzionalità di copia parallela Hello applica tooa **singola esecuzione dell'attività**.

Verrà ora esaminato uno scenario di esempio. Nell'esempio seguente di hello, più sezioni da hello ultimi necessitano toobe elaborati. Data Factory esegue un'istanza dell'attività di copia, ovvero un'esecuzione attività, per ogni sezione:

* sezione di dati Hello dal primo periodo di attività hello (1 too2 AM AM) = = > esecuzione di attività 1
* sezione di dati Hello dalla seconda finestra dell'attività hello (2 AM too3 AM) = = > eseguire l'attività 2
* sezione di dati Hello dalla seconda finestra dell'attività hello (3 AM too4 AM) = = > esecuzione di attività 3

e così via.

In questo esempio, quando hello **concorrenza** too2, viene impostato **attività eseguita 1** e **attività eseguita 2** copiare i dati da due finestre attività **contemporaneamente**  tooimprove prestazioni lo spostamento dei dati. Tuttavia, se più file sono associati con 1 di esecuzione dell'attività, il servizio di spostamento dati hello copia file da hello origine toohello destinazione un file alla volta.

### <a name="cloud-data-movement-units"></a>Unità di spostamento dati cloud
Oggetto **unità lo spostamento dei dati di cloud (DMU)** è una misura che rappresenta la potenza hello (una combinazione di CPU, memoria e di allocazione delle risorse di rete) di una singola unità nella Data Factory. Una unità di spostamento dati può essere usata in un'operazione di copia da cloud a cloud, ma non in una copia ibrida.

Per impostazione predefinita, Data Factory viene utilizzata una tooperform DMU singolo cloud eseguire una singola attività di copia. toooverride questa impostazione predefinita, specificare un valore per hello **cloudDataMovementUnits** proprietà come indicato di seguito. Per informazioni sul livello di hello miglioramento delle prestazioni è possibile che venga visualizzato quando si configurano più unità per una copia specifica origine e il sink, vedere hello [di riferimento delle prestazioni](#performance-reference).

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "cloudDataMovementUnits": 32
        }
    }
]
```
Hello **i valori consentiti** per hello **cloudDataMovementUnits** proprietà sono 1 (impostazione predefinita), 2, 4, 8, 16, 32. Hello **numero effettivo di cloud DMUs** che l'operazione di copia hello viene utilizzato in fase di esecuzione è uguale tooor minore hello configurato, a seconda del modello di dati.

> [!NOTE]
> Se sono necessarie più unità di spostamento dati cloud per aumentare la velocità effettiva, contattare il [supporto di Azure](https://azure.microsoft.com/support/). L'impostazione di 8 e versioni successive attualmente funziona solo quando si **copiare più file da Blob archivio Data Lake/archiviazione/Amazon S3/cloud FTP/cloud SFTP tooBlob storage/archivio Data Lake/Azure SQL Database**.
>

### <a name="parallelcopies"></a>parallelCopies
È possibile utilizzare hello **parallelCopies** parallelismo hello tooindicate di proprietà che si desidera toouse attività di copia. È possibile pensare di questa proprietà come numero massimo di hello di thread all'interno delle attività di copia di lettura dall'origine o la scrittura tooyour sink gli archivi dati in parallelo.

Per eseguire ogni attività di copia, Data Factory determina il numero di hello di parallelo copie toouse toocopy dati dall'archivio dati di origine hello e toohello archivio dati di destinazione. numero di copie parallele che utilizza predefinito Hello dipende dal tipo di hello di origine e sink in uso.  

| Origine e sink | Numero predefinito di copie parallele determinato dal servizio |
| --- | --- |
| Copia di dati tra archivi basati su file, come archiviazione BLOB, Data Lake Store, Amazon S3, un file system locale, un HDFS locale |Tra 1 e 32. Dipende dalla dimensione hello del file hello e numero di hello cloud lo spostamento delle unità di dati (DMUs) toocopy utilizzati dati tra due archivi di dati di cloud o configurazione fisica di hello di hello computer Gateway utilizzato per una copia ibrida (tooor di toocopy dati da un archivio dati locale ). |
| Copia i dati da **archiviazione tabelle tooAzure di archiviare i dati di origine** |4 |
| Tutte le altre coppie di origine e sink |1 |

In genere, il comportamento predefinito di hello dovrebbe offrire la migliore velocità effettiva di hello. Tuttavia, hello toocontrol carico nei computer che ospitano l'archivi dati o le prestazioni della copia tootune, è possibile scegliere di valore predefinito di toooverride hello e specificare un valore per hello **parallelCopies** proprietà. il valore di Hello deve essere compreso tra 1 e 32 (inclusi). In fase di esecuzione per prestazioni ottimali hello, attività di copia viene utilizzato un valore che è minore o uguale toohello valore impostato.

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "parallelCopies": 8
        }
    }
]
```
Toonote punti:

* Quando si copiano dati tra archivi basati su file, hello **parallelCopies** determinare parallelismo hello a livello di file hello. suddivisione in blocchi Hello all'interno di un singolo file accadrebbe sotto automatico e trasparente ed è concepita toouse hello migliore Adatta dimensioni del blocco per un archivio dati di origine specificata di tipo tooload in parallelo e ortogonali tooparallelCopies. numero effettivo di Hello copie parallelo è non più di numero hello file hello dati lo spostamento del servizio Usa per operazione di copia hello in fase di esecuzione. Se il comportamento di copia hello è **mergeFile**, attività di copia non è possibile trarre vantaggio dal parallelismo a livello di file.
* Quando si specifica un valore per hello **parallelCopies** proprietà, considerare l'aumento del carico hello sul archivi di dati di origine e sink e toogateway se è una copia ibrida. Questo errore si verifica soprattutto quando si dispone di più attività o esecuzioni simultanee di hello stesse attività eseguite su hello allo stesso archivio dati. Se si nota che l'archivio dati hello o Gateway viene sovraccaricato con carico hello, ridurre hello **parallelCopies** carico hello toorelieve di valore.
* Quando si copiano dati da archivi che non sono toostores basata su file che sono basate su file, il servizio di spostamento dati hello Ignora hello **parallelCopies** proprietà. Anche se viene specificato, in questo caso il parallelismo non viene applicato.

> [!NOTE]
> È necessario utilizzare hello toouse 1.11 o versione successiva versione di Gateway di gestione dati **parallelCopies** funzionalità quando si esegue una copia ibrida.
>
>

toobetter utilizzare queste due proprietà e tooenhance la velocità effettiva lo spostamento dei dati, vedere hello [casi di utilizzo di esempio](#case-study-use-parallel-copy). Non è necessario tooconfigure **parallelCopies** tootake vantaggio del comportamento predefinito di hello. Se si esegue la configurazione e il valore di **parallelCopies** è troppo basso, è possibile che più unità di spostamento dati cloud non vengano utilizzate appieno.  

### <a name="billing-impact"></a>Impatto della fatturazione
Ha **importante** tooremember che vengono addebitati in base al tempo totale di hello dell'operazione di copia hello. Se un processo di copia utilizzato tootake un'ora con l'unità di un cloud e ha ora 15 minuti con quattro unità cloud, hello generale rimane costi quasi hello stesso. Si prenda ad esempio un utilizzo di quattro unità cloud. la prima unità cloud di Hello impiega 10 minuti, hello terzo, 5 minuti, hello secondo, 10 minuti e hello quarto, 5 minuti, in esecuzione un'attività di copia. Viene addebitato per volta (lo spostamento dei dati) di hello copia totale, ovvero 10 + 10 + 5 + 5 = 30 minuti. L'uso di **parallelCopies** non influisce sulla fatturazione.

## <a name="staged-copy"></a>copia di staging
Quando si copiano dati da un archivio dati di origine dati archivio tooa sink, è possibile scegliere l'archiviazione Blob toouse come archivio di gestione temporanea provvisorio. Gestione temporanea è particolarmente utile nei seguenti casi hello:

1. **Si desidera tooingest dati da diversi archivi dati in SQL Data Warehouse tramite PolyBase**. SQL Data Warehouse utilizza PolyBase come tooload un meccanismo di velocità effettiva elevata una grande quantità di dati in SQL Data Warehouse. Tuttavia, i dati di origine hello devono essere nell'archiviazione Blob e deve soddisfare i criteri aggiuntivi. Quando si caricano dati da un archivio dati non BLOB, è possibile attivare la copia di dati tramite un archivio BLOB di staging provvisorio. In tal caso, Data Factory esegue hello necessario tooensure di trasformazioni di dati che soddisfi i requisiti di hello di PolyBase. Quindi, Usa dati tooload PolyBase in SQL Data Warehouse. Per ulteriori informazioni, vedere [dati tooload usare PolyBase in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse). Per la procedura dettagliata con un caso d'uso, vedere [Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md).
2. **In alcuni casi occorre un po' di tempo tooperform lo spostamento di dati un ibrido (vale a dire toocopy tra un archivio dati locale e un archivio dati cloud) su una connessione di rete lenta**. tooimprove prestazioni, è possibile comprimere i dati in locale in modo che richiede meno tempo archiviano dati di gestione temporanea toohello toomove dati nel cloud hello hello. È quindi possibile decomprimere i dati di hello nell'archivio di gestione temporanea prima di caricarli nell'archivio dati di destinazione hello hello.
3. **Non si desidera tooopen porte diverso da porta 80 e la porta 443 nel firewall, a causa dei criteri IT aziendali**. Ad esempio, quando si copiano dati da un sink di Database SQL di Azure locale dati archivio tooan o un sink di Azure SQL Data Warehouse, è necessario tooactivate le comunicazioni TCP in uscita sulla porta 1433 per hello Windows firewall e del firewall aziendale. In questo scenario, sfruttare i vantaggi hello gateway toofirst copia tooa Blob archiviazione gestione temporanea dell'istanza di dati tramite HTTP o HTTPS sulla porta 443. Quindi, è possibile caricare i dati di hello in Database SQL o SQL Data Warehouse di gestione temporanea di archiviazione Blob. In questo flusso non è necessario tooenable porta 1433.

### <a name="how-staged-copy-works"></a>Come funziona la copia di staging
Quando si attiva hello funzionalità di gestione temporanea, i primi dati hello viene copiati dal hello origine dati archivio toohello archivio dati di gestione temporanea (modalità). Successivamente, i dati di hello vengono copiati dal hello dati archivio toohello sink dati archivio di gestione temporanea. Data Factory gestisce automaticamente il flusso di hello in due fasi per l'utente. Data Factory elimina anche i dati temporanei da gestione temporanea di archiviazione dopo aver completato lo spostamento dei dati di hello hello.

In caso di copia hello cloud (dati di origine e sink archivi sono nel cloud hello), non viene usato gateway. servizio Data Factory Hello esegue operazioni di copia hello.

![Copia di staging: scenario cloud](media/data-factory-copy-activity-performance/staged-copy-cloud-scenario.png)

In caso di copia ibrida hello (origine si trova in locale e il sink è nel cloud hello), gateway hello sposta dati dai dati di origine hello archiviano tooa archivio dati di gestione temporanea. Servizio Data Factory consente di spostare dati da dati di gestione temporanea hello toohello archiviano dati sink. Copia di dati da un tooan di archivio dati cloud locali archivio dati tramite gestione temporanea è supportato anche con flusso hello invertita.

![Copia di staging: scenario ibrido](media/data-factory-copy-activity-performance/staged-copy-hybrid-scenario.png)

Quando si attiva lo spostamento dei dati tramite un archivio di gestione temporanea, è possibile specificare se si desidera toobe dati hello compressi prima di passare dati dall'origine hello dati archiviano tooan provvisorio o archivio dati di gestione temporanea e quindi decompressi prima di spostare dati da un provvisorio o dati di gestione temporanea archiviano toohello sink dati.

Attualmente non è possibile copiare dati tra due archivi dati locali usando un archivio di staging. È probabile che non appena questo toobe opzione disponibile.

### <a name="configuration"></a>Configurazione
Configurare hello **enableStaging** impostazione nell'attività di copia toospecify se si desidera toobe dati hello gestione temporanea nell'archiviazione Blob prima di caricarli in un archivio dati di destinazione. Quando si imposta **enableStaging** tooTRUE, specificare hello proprietà aggiuntive elencate nella tabella riportata di seguito hello. Se non si dispone di uno, è necessario anche toocreate una risorsa di archiviazione di Azure o l'archiviazione condivisa servizio collegato alla firma di accesso per la gestione temporanea.

| Proprietà | Descrizione | Valore predefinito | Obbligatorio |
| --- | --- | --- | --- |
| **enableStaging** |Specificare se si desidera toocopy dati tramite un provvisorio archivio di gestione temporanea. |False |No |
| **linkedServiceName** |Specificare il nome di hello di un [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) servizio, che fa riferimento istanza toohello di spazio di archiviazione utilizzato come archivio di gestione temporanea provvisorio collegato. <br/><br/> È possibile utilizzare l'archiviazione dati tooload una firma di accesso condiviso in SQL Data Warehouse tramite PolyBase. Può essere usata in tutti gli altri scenari. |N/D |Sì, quando **enableStaging** è impostato tooTRUE |
| **path** |Specificare percorso di archiviazione Blob hello di visualizzare i dati di gestione temporanea hello toocontain. Se non si specifica un percorso, il servizio di hello crea un contenitore toostore temporanea di dati. <br/><br/> Specificare un percorso solo se si utilizza l'archiviazione con una firma di accesso condiviso, o si richiede dati temporanei toobe in una posizione specifica. |N/D |No |
| **enableCompression** |Specifica se è necessario comprimere i dati prima che venga copiato toohello destinazione. Questa impostazione consente di ridurre il volume di hello di dati trasferiti. |False |No |

Di seguito è riportato un esempio della definizione attività di copia con proprietà hello descritte nella tabella precedente hello:

```json
"activities":[  
{
    "name": "Sample copy activity",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDBOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlSink"
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob",
            "path": "stagingcontainer/path",
            "enableCompression": true
        }
    }
}
]
```

### <a name="billing-impact"></a>Impatto della fatturazione
I costi addebitati si basano su due passaggi: durata della copia e tipo di copia.

* Quando si utilizza Gestione temporanea durante una copia su cloud (copia di dati da un archivio dati cloud dati archivio tooanother cloud), vengono addebitati hello [somma della durata di copia per i passaggi 1 e 2] x [prezzo unitario di copia cloud].
* Quando si utilizza Gestione temporanea durante una copia ibrida (copia di dati da un archivio dati locale dati archivio tooa cloud), vengono addebitati i [durata copia ibrida] x [prezzo unitario di copia ibrida] + [cloud copia durata] x [prezzo unitario di copia cloud].

## <a name="performance-tuning-steps"></a>Procedura di ottimizzazione delle prestazioni
Si consiglia di eseguire la procedura seguente prestazioni hello tootune del servizio Data Factory con attività di copia:

1. **Stabilire una baseline**. Durante la fase di sviluppo hello, testare la pipeline con attività di copia su un campione di dati rappresentativo. È possibile utilizzare Data Factory hello [sezionamento modello](data-factory-scheduling-and-execution.md) quantità hello toolimit si lavora con dati.

   Raccogliere il tempo di esecuzione e le caratteristiche di prestazioni tramite hello **monitoraggio e gestione App**. Scegliere **Monitoraggio e gestione** nella home page di Data Factory. Nella visualizzazione ad albero di hello, scegliere hello **set di dati di output**. In hello **attività Windows** scegliere hello eseguire attività di copia. **Attività Windows** Elenca la durata di attività di copia hello e dimensione hello dati hello che viene copiato. velocità effettiva di Hello è elencata nella **attività finestra Esplora**. toolearn ulteriori informazioni sull'applicazione hello, vedere [Monitor e gestire le pipeline di Data Factory di Azure tramite hello monitoraggio e gestione App](data-factory-monitor-manage-app.md).

   ![Dettagli esecuzione attività](./media/data-factory-copy-activity-performance/mmapp-activity-run-details.png)

   Più avanti in articolo hello, è possibile confrontare le prestazioni di hello e la configurazione del scenario tooCopy attività [di riferimento delle prestazioni](#performance-reference) dai nostri test.
2. **Diagnosticare e ottimizzare le prestazioni**. Se le prestazioni di hello che è osservare non soddisfano le aspettative, è necessario tooidentify eventuali colli di bottiglia. Quindi, ottimizzare le prestazioni tooremove o ridurre l'effetto di hello di colli di bottiglia. Una descrizione completa della diagnosi delle prestazioni esula dall'ambito di hello di questo articolo, ma di seguito sono riportate alcune considerazioni comuni:

   * Funzionalità per le prestazioni:
     * [Copia parallela](#parallel-copy)
     * [Unità di spostamento dati cloud](#cloud-data-movement-units)
     * [Copia di staging](#staged-copy)
     * [Scalabilità di Gateway di gestione dati](data-factory-data-management-gateway-high-availability-scalability.md)
   * [Gateway di gestione dati](#considerations-for-data-management-gateway)
   * [Origine](#considerations-for-the-source)
   * [Sink](#considerations-for-the-sink)
   * [Serializzazione e deserializzazione](#considerations-for-serialization-and-deserialization)
   * [Compressione](#considerations-for-compression)
   * [Mapping di colonne](#considerations-for-column-mapping)
   * [Altre considerazioni](#other-considerations)
3. **Espandere hello configurazione tooyour intero set di dati**. Quando si è soddisfatti dei risultati dell'esecuzione hello e prestazioni, è possibile espandere definizione hello e toocover periodo attivo di pipeline l'intero set di dati.

## <a name="considerations-for-data-management-gateway"></a>Considerazioni su Gateway di gestione dati
**Installazione del gateway**: È consigliabile usare un Gateway di gestione dati di toohost computer dedicato. Vedere [Considerazioni sull'uso di Gateway di gestione dati](data-factory-data-management-gateway.md#considerations-for-using-gateway).  

**Monitoraggio di gateway e la scalabilità verticale/orizzontale**: un singolo gateway logico con uno o più nodi gateway può essere utilizzato più attività di copia viene eseguito nel hello stesso tempo contemporaneamente. È possibile visualizzare snapshot tempo quasi reale di utilizzo delle risorse (CPU, memoria, network(in/out) e così via) nel computer gateway, nonché il numero di hello di processi simultanei in esecuzione e limite di hello portale di Azure, vedere [gateway monitoraggio nel portale di hello](data-factory-data-management-gateway.md#monitor-gateway-in-the-portal). Se è necessario pesante nello spostamento dei dati ibrido con un numero elevato di sequenze di attività simultanee di copia o con volume elevato di dati toocopy, prendere in considerazione troppo[scalabilità verticale e scalabilità gateway](data-factory-data-management-gateway-high-availability-scalability.md#scale-considerations) così come toobetter utilizzare la risorsa o copiare ulteriori risorse tooempower di tooprovision. 

## <a name="considerations-for-hello-source"></a>Considerazioni per l'origine hello
### <a name="general"></a>Generale
Assicurarsi che hello archivio dati sottostante non viene sovraccaricato di altri carichi di lavoro che sono in esecuzione su o su di essa.

Per gli archivi di dati di Microsoft, vedere [di monitoraggio e ottimizzazione argomenti](#performance-reference) che sono specifici toodata archivi e consentono di comprendere dati memorizzare le caratteristiche di prestazioni, ridurre al minimo i tempi di risposta e ottimizzare la velocità effettiva.

Se si copiano dati da tooSQL di archiviazione Blob del Data Warehouse, è consigliabile utilizzare **PolyBase** tooboost prestazioni. Vedere [dati tooload usare PolyBase in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) per informazioni dettagliate. Per la procedura dettagliata con un caso d'uso, vedere [Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md).

### <a name="file-based-data-stores"></a>Archivi dati basati su file
*Inclusi archiviazione BLOB, Data Lake Store, Amazon S3, file system locali e HDFS locale*

* **Dimensioni medie dei file e numero medio di file**: l'attività di copia trasferisce i dati procedendo un file alla volta. Con hello stessa quantità di dati toobe spostato, hello velocità effettiva complessiva è minore, se i dati di hello è costituito da molti piccoli file anziché di alcuni file di grandi dimensioni a causa di toohello fase bootstrap per ogni file. Pertanto, se possibile, combinare piccoli file in più grandi file toogain una velocità effettiva.
* **File di formato e la compressione**: per prestazioni più elevate tooimprove modi, vedere hello [considerazioni per la serializzazione e deserializzazione](#considerations-for-serialization-and-deserialization) e [considerazioni per la compressione](#considerations-for-compression) sezioni.
* Per hello **locale del file system** scenario, in cui **Gateway di gestione dati** è obbligatorio, vedere hello [considerazioni per Gateway di gestione dati](#considerations-for-data-management-gateway) sezione.

### <a name="relational-data-stores"></a>Archivi dati relazionali
*Inclusi database SQL, SQL Data Warehouse, Amazon Redshift, database SQL Server e database Oracle, MySQL, DB2, Teradata, Sybase e PostgreSQL*

* **Modello di dati**: lo schema di tabella influisce sulla velocità effettiva di copia. Toocopy hello stessa quantità di dati di grandi dimensioni offre prestazioni migliori di dimensioni della riga di piccole dimensioni. motivo di Hello è che il database hello in modo più efficiente possibile recuperare un minor numero di batch di dati che contengono meno righe.
* **Query o stored procedure**: ottimizzare logica hello di query di hello o stored procedure specificata nei dati di hello attività di copia origine toofetch in modo più efficiente.
* Per **database relazionali locale**, ad esempio SQL Server e Oracle, che richiedono l'uso di hello di **Gateway di gestione dati**, vedere hello [considerazioni per il Gateway di gestione dati](#considerations-on-data-management-gateway) sezione.

## <a name="considerations-for-hello-sink"></a>Considerazioni per il sink hello
### <a name="general"></a>Generale
Assicurarsi che hello archivio dati sottostante non viene sovraccaricato di altri carichi di lavoro che sono in esecuzione su o su di essa.

Per gli archivi di dati di Microsoft, fare riferimento troppo[di monitoraggio e ottimizzazione argomenti](#performance-reference) che sono archivi toodata specifico. Questi argomenti consentono di comprendere le caratteristiche di prestazioni archivio dati e la modalità di tempi di risposta toominimize e ottimizzare la velocità effettiva.

Se si copiano dati da **nell'archiviazione Blob** troppo**SQL Data Warehouse**, è consigliabile utilizzare **PolyBase** tooboost prestazioni. Vedere [dati tooload usare PolyBase in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) per informazioni dettagliate. Per la procedura dettagliata con un caso d'uso, vedere [Caricare 1 TB di dati in Azure SQL Data Warehouse in meno di 15 minuti con Azure Data Factory](data-factory-load-sql-data-warehouse.md).

### <a name="file-based-data-stores"></a>Archivi dati basati su file
*Inclusi archiviazione BLOB, Data Lake Store, Amazon S3, file system locali e HDFS locale*

* **Copiare il comportamento**: se si copiano dati da un archivio dati diverso basato su file, attività di copia sono disponibili tre opzioni tramite hello **copyBehavior** proprietà. mantenere la gerarchia, rendere flat la gerarchia e unire i file. Mantenimento o rendere flat gerarchia presenta un overhead di prestazioni senza alcuna, ma l'unione di file provoca tooincrease overhead delle prestazioni.
* **File di formato e la compressione**: hello vedere [considerazioni per la serializzazione e deserializzazione](#considerations-for-serialization-and-deserialization) e [considerazioni per la compressione](#considerations-for-compression) sezioni per le prestazioni di altre modalità tooimprove .
* **Archivio BLOB**: attualmente l'archivio BLOB supporta solo i BLOB in blocchi per l'ottimizzazione della velocità effettiva e del trasferimento dati.
* Per **locale file System** scenari che richiedono l'uso di hello di **Gateway di gestione dati**, vedere hello [considerazioni per Gateway di gestione dati](#considerations-for-data-management-gateway) sezione.

### <a name="relational-data-stores"></a>Archivi dati relazionali
*Inclusi database SQL, SQL Data Warehouse, database SQL Server e database Oracle*

* **Copiare il comportamento**: a seconda delle proprietà hello sono stati impostati per **sqlSink**, attività di copia scrive i database di destinazione toohello dati in modi diversi.
  * Per impostazione predefinita, utilizza servizio di hello dati lo spostamento dei dati di tooinsert hello API della copia Bulk in modalità di aggiunta, che fornisce hello prestazioni ottimali.
  * Se si configura una stored procedure nel sink hello, database di hello applica una riga di dati hello alla volta anziché come un caricamento bulk. e le prestazioni ne risentono notevolmente. Se il set di dati è grande, quando applicabile, valutare se passare hello toousing **sqlWriterCleanupScript** proprietà.
  * Se si configura hello **sqlWriterCleanupScript** eseguire proprietà per ogni attività di copia, trigger servizio hello hello script e quindi utilizzare dati hello tooinsert API della copia Bulk di hello. Ad esempio, toooverwrite hello intera tabella con dati più recenti di hello, è possibile specificare un toofirst script elimina tutti i record prima che nuovi dati di caricamento bulk hello dall'origine hello.
* **Modello di dati e dimensioni batch**:
  * Lo schema di tabella influisce sulla velocità effettiva di copia. toocopy hello stessa quantità di dati di grandi dimensioni offre prestazioni migliori rispetto alla dimensione di una riga piccola perché il database di hello in modo più efficiente possibile eseguire il commit un minor numero di batch di dati.
  * L'attività di copia inserisce i dati in una serie di batch. È possibile impostare il numero di hello di righe in un batch utilizzando hello **viene raggiunto writeBatchSize** proprietà. Se i dati includono le righe di piccole dimensioni, è possibile impostare hello **viene raggiunto writeBatchSize** proprietà con una maggiore toobenefit valore da un overhead minore di batch e una velocità effettiva. Se le dimensioni di riga hello dei dati sono grande, prestare attenzione quando si aumenta **viene raggiunto writeBatchSize**. Un valore elevato potrebbe causare l'errore di copia tooa tramite overload database hello.
* Per **database relazionali locale** , ad esempio SQL Server e Oracle, che richiedono l'uso di hello di **Gateway di gestione dati**, vedere hello [considerazioni per il Gateway di gestione dati](#considerations-for-data-management-gateway) sezione.

### <a name="nosql-stores"></a>Archivi NoSQL
*Inclusi gli archivi tabelle e Azure Cosmos DB*

* Per gli **archivi tabelle**:
  * **Partizione**: scrittura di partizioni di dati toointerleaved notevolmente le prestazioni risultano inferiori. Ordinare i dati di origine dalla chiave di partizione in modo che i dati di hello viene inseriti in modo efficiente una partizione dopo l'altro, oppure regolare hello logica toowrite hello tooa singola partizione di dati.
* Per **Azure Cosmos DB**:
  * **Dimensione batch**: hello **viene raggiunto writeBatchSize** proprietà imposta il numero di hello di richieste in parallelo dei documenti toocreate toohello DB Cosmos Azure del servizio. È possibile prevedere prestazioni migliori quando si aumenta **viene raggiunto writeBatchSize** perché altre richieste in parallelo vengono inviate tooAzure DB Cosmos. Tuttavia, controllare la limitazione delle richieste quando si scrittura tooAzure DB Cosmos (messaggio di errore hello è "Richiesta frequenza è di grandi dimensioni"). Vari fattori possono causare la limitazione delle richieste, tra cui dimensioni del documento, numero hello di termini nei documenti di hello e hello criteri di indicizzazione della raccolta di destinazione. tooachieve una velocità effettiva copia, è consigliabile utilizzare una raccolta migliore, ad esempio, S3.

## <a name="considerations-for-serialization-and-deserialization"></a>Considerazioni sulla serializzazione e deserializzazione
Serializzazione e deserializzazione possono verificarsi quando il set di dati di input o il set di dati di output è costituito da un file. Per informazioni dettagliate sui formati di file supportati dall'attività di copia vedere [File supportati e formati di compressione](data-factory-supported-file-and-compression-formats.md).

**Comportamento di copia**:

* Copia di file tra archivi dati basati su file:
  * Quando i set di dati di input e output che prevedono non hello stesso o impostazioni del file di formato, il servizio di spostamento dati hello esegue una copia binaria senza la serializzazione o deserializzazione. Vedrai uno scenario di toohello maggiore velocità effettiva rispetto, in cui hello impostazioni di formato di file di origine e sink sono diverse tra loro.
  * Quando l'input e output set di dati di entrambi sono in formato testo e codifica hello solo il tipo è diverso, il servizio di spostamento dati hello esegue solo la conversione di codifica. Non esegue qualsiasi serializzazione e la deserializzazione, che provoca un sovraccarico delle prestazioni rispetto copia binaria tooa.
  * Quando l'input e output set di dati sia diversi formati di file o configurazioni diverse, come delimitatori, hello servizio di spostamento dati deserializza toostream dati di origine, trasformazione e quindi eseguirne la serializzazione in formato di output di hello che è indicato. Questa operazione comporta un sovraccarico prestazioni molto più significativo rispetto tooother scenari.
* Quando si copiano i file per/da un archivio dati che non è basata su file (ad esempio, da un archivio relazionale tooa store basate su file), passaggio di serializzazione o deserializzazione di hello è obbligatorio. Questo passaggio comporta un notevole overhead delle prestazioni.

**Formato di file**: formato scelto per il file hello potrebbe influire sulle prestazioni di copia. Ad esempio, Avro è un formato binario compresso che archivia i metadati con i dati. Include un ampio supporto nell'ecosistema di hello Hadoop per l'elaborazione e l'esecuzione di query. È tuttavia più costoso per la serializzazione e la deserializzazione, determinando una velocità effettiva copia inferiore rispetto a tootext formato Avro. Effettuare la selezione del formato di file in tutta l'elaborazione del flusso olistico hello. Iniziare con il modulo hello vengono memorizzati in, archivi dati di origine toobe estratti da sistemi esterni. formato migliore di Hello per l'archiviazione, elaborazione analitica e l'esecuzione di query; e il relativo formato dati hello devono essere esportati nel data mart per strumenti di report e visualizzazioni. Talvolta un formato di file che non sia ottimale per leggere e scrivere prestazioni potrebbe essere una scelta ottimale quando si considera hello complessiva analitici processo.

## <a name="considerations-for-compression"></a>Considerazioni sulla compressione
Quando il set di dati di input o output è un file, è possibile impostare la compressione tooperform attività di copia o la decompressione durante la scrittura di destinazione toohello dei dati. La scelta della compressione comporta un compromesso tra input/output (I/O) e CPU. Le risorse di calcolo la compressione dei dati hello comporta costi aggiuntivi in. ma riduce l'I/O di rete e l'archiviazione. A seconda dei dati, si potrebbe riscontrare un aumento della velocità effettiva di copia complessiva.

**Codec**: l'attività di copia supporta i tipi di compressione gzip, bzip2 e Deflate. Azure HDInsight può utilizzare tutti e tre i tipi per l'elaborazione. Ogni codec di compressione presenta dei vantaggi. Ad esempio, bzip2 con velocità effettiva copia più bassa hello, ma si otterrà hello Hive query prestazioni ottimali con bzip2 poiché dividerlo per l'elaborazione. Gzip è l'opzione di hello più bilanciato e viene utilizzato spesso hello. Scegliere i codec hello che meglio si adatta allo scenario end-to-end.

**Livello**: per ogni codec di compressione è possibile scegliere tra due opzioni, la compressione più veloce e la compressione ottimale. Hello più rapido compresso opzione comprime hello dati più rapidamente possibile, anche se non viene compresso in modo ottimale file risultante hello. Hello opzione compresso in modo ottimale impiega più tempo alla compressione e produce una quantità minima di dati. È possibile testare entrambi toosee opzioni che fornisce migliori prestazioni complessive nel case.

**Una considerazione importante**: toocopy una grande quantità di dati tra un archivio locale e cloud hello, considerare l'utilizzo dell'archiviazione blob provvisorio con la compressione. Utilizzo dell'archiviazione provvisorio risulta utile quando hello di banda di rete aziendale e i servizi di Azure è fattore limitante hello e si desidera che il set di dati di input hello ed entrambi toobe set di dati di output in formato non compresso. In particolare, è possibile dividere un'attività di copia singola in due attività di copia. Hello prima attività Copia da provvisorio tooan di origine hello o blob di gestione temporanea in formato compresso. attività di copia secondo Hello copia i dati compresso hello dalla gestione temporanea e quindi decomprime mentre scrive toohello sink.

## <a name="considerations-for-column-mapping"></a>Considerazioni sul mapping di colonne
È possibile impostare hello **columnMappings** proprietà nell'attività di copia toomap tutti o un sottoinsieme di hello colonne di output toohello colonne di input. Dopo il servizio di spostamento dati hello legge i dati di hello dall'origine hello, è necessario il mapping di colonne tooperform sui dati hello prima che vengano scritte hello dati toohello sink. Questa ulteriore elaborazione riduce la velocità effettiva di copia.

Se l'archivio dati di origine è disponibile per query, se si tratta di un archivio relazionale come Database SQL o SQL Server o se è un archivio NoSQL come archiviazione tabelle o database Cosmos di Azure, si consideri ad esempio inserendo hello colonna filtro e il riordino degli logica toohello **query**  proprietà anziché i mapping della colonna. In questo modo, la proiezione hello si verifica quando il servizio di spostamento dati hello legge l'archivio dati dai dati di origine hello, in cui è molto più efficiente.

## <a name="other-considerations"></a>Altre considerazioni
Se hello le dimensioni dei dati che si desidera toocopy è di grandi dimensioni, è possibile modificare i dati della regola business toofurther partizione hello utilizzando hello meccanismo di sezionamento in Data Factory. Pianificare il tempo di attività di copia toorun più frequentemente eseguire delle dimensioni dei dati hello tooreduce per ogni attività di copia.

Essere attenzione hello numerosi set di dati e attività di copia richiedendo Data Factory tooconnector toohello stesso archivio dati in hello stesso tempo. Numero di processi simultanei copia potrebbe limitare un archivio dati e comportare prestazioni toodegraded, copiare i tentativi interni di processo e in alcuni casi, gli errori di esecuzione.

## <a name="sample-scenario-copy-from-an-on-premises-sql-server-tooblob-storage"></a>Scenario di esempio: copia da un archivio di tooBlob di SQL Server locale
**Scenario**: una pipeline viene compilata toocopy dati da un archivio di tooBlob on-premise SQL Server in formato CSV. toomake hello più velocemente il processo di copia, i file CSV hello devono essere compresso nel formato bzip2.

**Test e analisi**: velocità effettiva di hello delle attività di copia è minore di 2 MBps, che è molto più lente rispetto benchmark delle prestazioni hello.

**Analisi delle prestazioni e ottimizzazione**: tootroubleshoot hello problema di prestazioni, si esaminerà come dati hello vengono elaborati e spostati.

1. **Leggere dati**: Gateway apre tooSQL una connessione Server e invia hello query. SQL Server risponde inviando tooGateway di flusso di dati di hello tramite intranet hello.
2. **La serializzazione e comprimere i dati**: Gateway serializza formato tooCSV flusso di dati hello e comprime hello tooa bzip2 flusso dei dati.
3. **Scrivere dati**: Gateway carica archiviazione tooBlob di hello bzip2 flusso tramite hello Internet.

Come si può notare, i dati di hello vengono elaborati e spostati in modo sequenziale streaming: SQL Server > LAN > Gateway > WAN > nell'archiviazione Blob. **Hello prestazioni complessive viene gestita dalla velocità effettiva minima di hello attraverso la pipeline hello**.

![Flusso di dati](./media/data-factory-copy-activity-performance/case-study-pic-1.png)

Uno o più dei seguenti fattori hello potrebbe causare colli di bottiglia delle prestazioni hello:

* **Origine**: SQL Server ha di per sé una velocità effettiva bassa a causa dei carichi elevati.
* **Gateway di gestione dati**:
  * **LAN**: Gateway si trova lontano dal computer di SQL Server hello e dispone di una connessione con larghezza di banda ridotta.
  * **Gateway**: Gateway ha raggiunto il hello tooperform limitazioni di carico seguenti operazioni:
    * **Serializzazione**: serializzazione tooCSV flusso di dati hello formato è lento della velocità effettiva.
    * **Compressione**: si è scelto un codec di compressione lenta, ad esempio bzip2 a 2,8 Mbps con core i7.
  * **WAN**: larghezza di banda di hello tra la rete aziendale hello e i servizi di Azure è basso (ad esempio T1 = 1,544 kbps; T2 = 6,312 kbps).
* **Sink**: l'archivio BLOB ha una velocità effettiva bassa. Questo scenario è poco probabile perché il relativo contratto di servizio garantisce un minimo di 60 Mbps.

In questo caso, la compressione dei dati bzip2 potrebbe rallentare pipeline intera hello. Cambio codec di compressione gzip tooa potrebbe facilitano il collo di bottiglia.

## <a name="sample-scenarios-use-parallel-copy"></a>Scenari di esempio: usare la copia parallela
**Scenario di ricerca per categorie:** copiare i file di 1 MB 1.000 da archiviazione tooBlob nel file system hello in locale.

**Analisi e regolazione delle prestazioni**: per un esempio, se è stato installato un gateway in un computer quad-core, Data Factory utilizza 16 copie parallelo toomove file dall'archiviazione tooBlob nel file system hello contemporaneamente. L'esecuzione parallela deve garantire una velocità effettiva elevata. È anche possibile specificare esplicitamente conteggio copie parallelo hello. Quando si copiano molti file di piccole dimensioni, le copie parallele migliorano notevolmente la velocità effettiva garantendo un uso più efficiente delle risorse.

![Scenario 1](./media/data-factory-copy-activity-performance/scenario-1.png)

**Scenario II**: copiare 20 BLOB di 500 MB da archiviazione di Blob tooData Lake archivio Analitica e ottimizzare le prestazioni.

**Analisi e regolazione delle prestazioni**: In questo scenario, Data Factory copia dati hello da un archivio Blob archiviazione tooData Lake tramite una singola copia (**parallelCopies** impostare too1) e le unità di spostamento di dati singolo cloud. Hello velocità effettiva è osservare verrà essere Chiudi toothat descritto in hello [sezione di riferimento delle prestazioni](#performance-reference).   

![Scenario 2](./media/data-factory-copy-activity-performance/scenario-2.png)

**Scenario III**: i singoli file hanno grandi dimensioni e il volume totale molto elevato.

**Analisi e ottimizzazione delle prestazioni**: aumento **parallelCopies** non ottenere migliori prestazioni di copia a causa delle limitazioni delle risorse hello di DMU una singolo cloud. Al contrario, è necessario specificare più cloud DMUs tooget spostamento dei dati di altre risorse tooperform hello. Non si specifica un valore per hello **parallelCopies** proprietà. Data Factory gestisce il parallelismo hello. In questo caso, se si imposta **cloudDataMovementUnits** si verifica di too4, una velocità effettiva di circa quattro volte.

![Scenario 3](./media/data-factory-copy-activity-performance/scenario-3.png)

## <a name="reference"></a>riferimento
Ecco il monitoraggio delle prestazioni e ottimizzazione di riferimenti per alcuni archivi dati hello è supportato:

* Archiviazione di Azure, inclusi archivi BLOB e archivi tabelle: [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../storage/common/storage-scalability-targets.md) ed [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](../storage/common/storage-performance-checklist.md)
* Database SQL di Azure: È possibile [monitorare le prestazioni di hello](../sql-database/sql-database-single-database-monitor.md) e verificare la percentuale di hello database transaction unit (DTU)
* Azure SQL Data Warehouse: la funzionalità viene misurata in unità data warehouse (DWU). Vedere in proposito [Gestire la potenza di calcolo in Azure SQL Data Warehouse (Panoramica)](../sql-data-warehouse/sql-data-warehouse-manage-compute-overview.md)
* Azure Cosmos DB: [livelli di prestazioni in Azure Cosmos DB](../documentdb/documentdb-performance-levels.md)
* SQL Server locale: [Monitoraggio e ottimizzazione delle prestazioni](https://msdn.microsoft.com/library/ms189081.aspx)
* File server locale: [Performance Tuning for File Servers](https://msdn.microsoft.com/library/dn567661.aspx)
