---
title: dati aaaMove da HDFS locale | Documenti Microsoft
description: Informazioni su come dati toomove da on-premise HDFS usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a>Spostare dati da HDFS locale con Azure Data Factory
Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un HDFS locale. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.

È possibile copiare i dati dall'archivio dati HDFS tooany supportati sink. Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. Data factory di attualmente supporta solo lo spostamento dei dati da un archivi di dati tooother HDFS locale, ma non per lo spostamento dei dati da altri dati archivi tooan locale HDFS.

> [!NOTE]
> Attività di copia non elimina i file di origine hello dopo che è la destinazione toohello copiati correttamente. Se è necessario toodelete file di origine hello dopo una copia ha esito positivo, creare un file di hello toodelete di attività personalizzata e utilizzare attività hello nella pipeline hello. 

## <a name="enabling-connectivity"></a>Abilitazione della connettività
Servizio Data Factory supporta connessione HDFS tooon locale utilizzando hello Gateway di gestione dati. Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello. Utilizzare hello gateway tooconnect tooHDFS anche se è ospitato in una macchina virtuale IaaS di Azure.

> [!NOTE]
> Hello di assicurarsi che Gateway di gestione dati è possibile accedere troppo**tutti** hello [server dei nomi nodo]: [nome porta nodo] e [server dei nodi di dati]: [porta nodo di dati] del cluster Hadoop hello. La [porta del nodo dei nomi] predefinita è 50070 e la [porta del nodo dati] predefinita è 50075.

Sebbene sia possibile installare un gateway in hello stesso locale macchina o hello macchina virtuale di Azure come hello HDFS, si consiglia di installare gateway hello in un separato macchina/Azure VM IaaS. La presenza del gateway su un computer separato riduce i conflitti di risorse e consente di ottenere prestazioni migliori. Quando si installa il gateway hello in un computer separato, macchina hello deve essere in grado di tooaccess macchina di hello con hello HDFS.

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine HDFS usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio dati HDFS, vedere [esempio JSON: copiare i dati da tooAzure HDFS locale Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) sezione di questo articolo.

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooHDFS:

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Un servizio collegato di collegare una data factory tooa archivio di dati. Creare un servizio collegato di tipo **Hdfs** toolink una data factory di tooyour HDFS locale. Hello nella tabella seguente fornisce una descrizione del servizio specifico tooHDFS collegati gli elementi JSON.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **Hdfs** |Sì |
| Url |URL toohello HDFS |Sì |
| authenticationType |Anonima o Windows. <br><br> toouse **l'autenticazione Kerberos** per connettore HDFS, fare riferimento troppo[in questa sezione](#use-kerberos-authentication-for-hdfs-connector) tooset l'ambiente locale di conseguenza. |Sì |
| userName |Nome utente per l'autenticazione di Windows |Sì (per l'autenticazione di Windows) |
| password |Password per l'autenticazione di Windows |Sì (per l'autenticazione di Windows) |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve usare tooconnect toohello HDFS. |Sì |
| encryptedCredential |[Nuovo AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output delle credenziali di accesso hello. |No |

### <a name="using-anonymous-authentication"></a>Uso dell'autenticazione anonima

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a>Uso dell'autenticazione di Windows

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. sezione Hello typeProperties per set di dati di tipo **FileShare** (che include set di dati HDFS) ha le proprietà seguenti hello

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| folderPath |Cartella toohello percorso. Esempio: `myfolder`<br/><br/>Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello. Ad esempio: per cartella\sottocartella specificare cartella\\\\sottocartella e per d:\cartellaesempio specificare l'unità d:\\\\cartellaesempio.<br/><br/>È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora. |Sì |
| fileName |Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello. Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.<br/><br/>Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato: <br/><br/>Data<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| partitionedBy |partitionedBy può essere utilizzato toospecify un folderPath dinamica, il nome file per i dati della serie temporale. Ad esempio, folderPath con parametri per ogni ora di dati. |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output. |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. I livelli supportati sono **Ottimale** e **Più veloce**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

> [!NOTE]
> filename e fileFilter non possono essere usati contemporaneamente.

### <a name="using-partionedby-property"></a>Uso della proprietà partionedBy
Come indicato nella sezione precedente di hello, è possibile specificare un folderPath dinamico e il nome di dati della serie temporale con hello **partitionedBy** proprietà [funzioni di Data Factory e le variabili di sistema hello](data-factory-functions-variables.md).

toolearn ulteriori informazioni sui set di dati serie ora, la pianificazione e le sezioni, vedere [la creazione di DataSet](data-factory-create-datasets.md), [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md), e [la creazione di pipeline](data-factory-create-pipelines.md) articoli.

#### <a name="sample-1"></a>Esempio 1.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
In questo esempio {Slice} viene sostituito con valore hello della variabile di sistema di Data Factory SliceStart nel formato hello (YYYYMMDDHH) specificato. Hello SliceStart fa riferimento l'ora toostart sezione hello. Hello folderPath è diversa per ogni sezione. Ad esempio: wikisampledataout/wikidatagateway/2014100103 o wikisampledataout/wikidatagateway/2014100104.

#### <a name="sample-2"></a>Esempio 2:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
In questo esempio l'anno, il mese, il giorno e l'ora di SliceStart vengono estratti in variabili separate che vengono usate dalle proprietà folderPath e fileName.

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

Per attività di copia, l'origine è di tipo **FileSystemSource** hello le proprietà seguenti sono disponibile nella sezione typeProperties:

**FileSystemSource** supporta hello le proprietà seguenti:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello. |True, False (valore predefinito) |No |

## <a name="supported-file-and-compression-formats"></a>Formati di file e di compressione supportati
Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a>Esempio JSON: copiare i dati da tooAzure HDFS locale Blob
Questo esempio viene illustrato come toocopy dati da un tooAzure HDFS locale nell'archiviazione Blob. Tuttavia, i dati possono essere copiati **direttamente** tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.  

esempio Hello fornisce definizioni di JSON per hello seguenti entità Data Factory. È possibile utilizzare questi toocreate definizioni una pipeline di dati da HDFS tooAzure nell'archiviazione Blob toocopy utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).

1. Un servizio collegato di tipo [OnPremisesHdfs](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati da un tooan HDFS locale blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

Innanzitutto, configurare il gateway di gestione dati hello. Hello istruzioni hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.

**Servizio collegato HDFS:** in questo esempio viene utilizzata l'autenticazione di Windows di hello. Per i diversi tipi di autenticazione disponibili, vedere la sezione [Proprietà del servizio collegato HDFS](#linked-service-properties) .

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

**Servizio collegato Archiviazione di Azure:**

```JSON
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

**Set di dati di input HDFS:** questo set di dati si riferisce cartella HDFS toohello DataTransfer/UnitTest /. pipeline Hello copia tutti i file hello toohello questa cartella di destinazione.

L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

**Set di dati di output del BLOB di Azure:**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Un'attività di copia in una pipeline con un'origine su file system e un sink BLOB:**

pipeline di Hello contiene un'attività di copia che è configurato toouse questi set di dati di input e output e toorun pianificato ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**FileSystemSource** e **sink** tipo è stato impostato troppo**BlobSink**. query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a>Uso dell'autenticazione Kerberos per il connettore HDFS
Esistono due opzioni tooset backup hello nell'ambiente locale in modo da toouse l'autenticazione Kerberos nel connettore HDFS. È possibile scegliere hello uno meglio si adatta al caso.
* Opzione 1: [aggiungere un computer gateway all'area di autenticazione di Kerberos](#kerberos-join-realm)
* Opzione 2: [Abilitare il trust reciproco tra il dominio di Windows e l'area di autenticazione di Kerberos](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>Opzione 1: aggiungere un computer gateway all'area di autenticazione di Kerberos

#### <a name="requirement"></a>Requisito:

* computer del gateway Hello necessita di autenticazione Kerberos hello toojoin e non può partecipare a qualsiasi dominio di Windows.

#### <a name="how-tooconfigure"></a>Come tooconfigure:

**Nel computer del gateway:**

1.  Eseguire hello **che Ksetup** tooconfigure utilità hello server Kerberos KDC e area di autenticazione.

    computer di Hello deve essere configurato come membro del gruppo di lavoro poiché un'area di autenticazione Kerberos è diversa da un dominio di Windows. Ciò può essere ottenuto impostando l'area di autenticazione Kerberos hello e aggiungendo un server KDC come indicato di seguito. Sostituire *REALM.COM* con la propria area di autenticazione.

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    **Riavviare** macchina hello dopo l'esecuzione di questi 2 comandi.

2.  Verificare la configurazione di hello con **che Ksetup** comando. output di Hello deve essere ad esempio:

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

**In Azure Data Factory:**

* Configurazione connettore di hello HDFS mediante **l'autenticazione di Windows** con Kerberos principale nome e la password tooconnect toohello HDFS origine dati. Controllare la sezione [Proprietà del servizio collegato HDFS](#linked-service-properties) per i dettagli di configurazione.

### <a name="kerberos-mutual-trust"></a>Opzione 2: Abilitare il trust reciproco tra il dominio di Windows e l'area di autenticazione di Kerberos

#### <a name="requirement"></a>Requisito:
*   computer del gateway Hello è necessario aggiungere un dominio Windows.
*   Sono necessarie impostazioni di autorizzazione tooupdate hello controller di dominio.

#### <a name="how-tooconfigure"></a>Come tooconfigure:

> [!NOTE]
> Sostituire area-di autenticazione.com e AD.COM hello segue l'esercitazione con il propria rispettivo area di autenticazione e controller di dominio in base alle esigenze.

**Nel server KDC:**

1.  Modifica configurazione KDC hello in **krb5** toolet file KDC di considerare attendibile il dominio di Windows che fa riferimento toohello seguente modello di configurazione. Per impostazione predefinita, si trova in configurazione hello **/etc/krb5.conf**.

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  **Riavviare** hello servizio KDC dopo la configurazione.

2.  Preparare un'entità denominata  **krbtgt/REALM.COM@AD.COM**  in server KDC con hello comando seguente:

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  Nel file di configurazione del servizio HDFS **hadoop.security.auth_to_local** aggiungere `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.

**Nel controller di dominio:**

1.  Eseguire il seguente hello **che Ksetup** comandi tooadd una voce dell'area di autenticazione:

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  Stabilire relazioni di trust dal dominio di Windows tooKerberos dell'area di autenticazione. [password] è hello per le entità di hello  **krbtgt/REALM.COM@AD.COM** .

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  Selezionare l'algoritmo di crittografia usato in Kerberos.

    1. Passare tooServer Manager > Gestione criteri di gruppo > dominio > oggetti Criteri di gruppo > predefinito o criteri di dominio Active e modifica.

    2. In hello **Editor Gestione criteri di gruppo** finestra popup, andare tooComputer configurazione > Criteri > Impostazioni di Windows > Impostazioni di sicurezza > Criteri locali > Opzioni di sicurezza e configurare **rete sicurezza: configurare i tipi di crittografia consentiti per Kerberos**.

    3. Algoritmo di crittografia hello selezionare da toouse tooKDC quando esegue la connessione. In genere, è possibile selezionare semplicemente tutte le opzioni di hello.

        ![Configurare i tipi di crittografia per Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. Utilizzare **che Ksetup** comando toospecify hello crittografia algoritmo toobe utilizzato su hello specifico dell'area di autenticazione.

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  Creare mapping hello tra account di dominio hello e Kerberos dell'entità, in ordine toouse Kerberos dell'entità di dominio di Windows.

    1. Avviare strumenti di amministrazione di hello > **Active Directory Users and Computers**.

    2. Configurare funzionalità avanzate facendo clic su **Visualizza** > **Funzionalità avanzate**.

    3. Individuare hello account toowhich toocreate mapping desiderato e fare doppio clic su tooview **i mapping dei nomi** > fare clic su **nomi Kerberos** scheda.

    4. Aggiungere un'entità dall'area di autenticazione hello.

        ![Eseguire il mapping di sicurezza e identità](media/data-factory-hdfs-connector/map-security-identity.png)

**Nel computer del gateway:**

* Eseguire il seguente hello **che Ksetup** comandi tooadd una voce dell'area di autenticazione.

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

**In Azure Data Factory:**

* Configurazione connettore di hello HDFS mediante **l'autenticazione di Windows** con Account di dominio o l'origine dati di entità Kerberos tooconnect toohello HDFS. Controllare la sezione [Proprietà del servizio collegato HDFS](#linked-service-properties) per i dettagli di configurazione.

> [!NOTE]
> colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).


## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
