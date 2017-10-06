---
title: dati BLOB di archiviazione di Azure in archivio Data Lake aaaCopy | Documenti Microsoft
description: Utilizzare i dati di toocopy strumento AdlCopy dall'archivio di Azure archiviazione BLOB tooData Lake
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a>Copiare i dati da un archivio Azure archiviazione BLOB tooData Lake
> [!div class="op_single_selector"]
> * [Con DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Con AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Archivio Azure Data Lake fornisce uno strumento da riga di comando, [AdlCopy](http://aka.ms/downloadadlcopy), dati toocopy hello seguenti origini:

* Dal BLOB di Archiviazione di Azure a Data Lake Store. Non è possibile utilizzare AdlCopy toocopy dati dall'archivio Data Lake tooAzure archiviazione BLOB.
* Tra due account di Azure Data Lake Store.

Inoltre, è possibile utilizzare lo strumento AdlCopy hello in due modalità diverse:

* **Autonomo**, in cui lo strumento hello utilizza attività hello tooperform risorse di archivio Data Lake.
* **Utilizzo di un account Data Lake Analitica**, in cui unità hello assegnata account Data Lake Analitica tooyour sono utilizzati tooperform hello operazione di copia. È possibile toouse questa opzione quando si esaminano le attività di copia hello tooperform in modo prevedibile.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **BLOB di Archiviazione di Azure** con alcuni dati.
* **Un account Azure Data Lake Store**. Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)
* **(Facoltativo) dell'account Azure Data Lake Analitica** -vedere [Guida introduttiva di Azure Data Lake Analitica](../data-lake-analytics/data-lake-analytics-get-started-portal.md) per istruzioni su come toocreate una Data Lake archivio account.
* **Lo strumento AdlCopy**. Installare lo strumento AdlCopy hello da [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).

## <a name="syntax-of-hello-adlcopy-tool"></a>Sintassi dello strumento AdlCopy hello
Utilizzare hello segue sintassi toowork con lo strumento AdlCopy hello

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

parametri di Hello nella sintassi hello sono descritti di seguito:

| Opzione | Descrizione |
| --- | --- |
| Sorgente |Specifica il percorso di hello hello dei dati di origine nel blob di archiviazione di Azure hello. Hello origine può essere un contenitore blob, un blob o un altro account archivio Data Lake. |
| Dest |Specifica hello archivio Data Lake destinazione toocopy per. |
| SourceKey |Specifica una chiave di accesso di archiviazione di hello per l'origine blob di archiviazione di Azure hello. Ciò è necessario solo se l'origine di hello è un contenitore blob o un blob. |
| Account |**Facoltativo**. Usare questo processo di copia hello toorun account Azure Data Lake Analitica toouse. Se si utilizza l'opzione /Account hello nella sintassi hello ma non si specifica un account Data Lake Analitica, AdlCopy utilizza un processo di hello toorun account predefinito. Inoltre, se si utilizza questa opzione, è necessario aggiungere origine hello (Blob di archiviazione di Azure) e destinazione (archivio Azure Data Lake) come origini dati per l'account Data Lake Analitica. |
| Unità |Specifica il numero di hello di unità Data Lake Analitica che verrà utilizzato per il processo di copia hello. Questa opzione è obbligatoria se si utilizza hello **/Account** opzione account Data Lake Analitica di hello toospecify. |
| Modello |Specifica un criterio di espressione regolare che indica quale toocopy BLOB o i file. AdlCopy usa la corrispondenza tra maiuscole e minuscole. modello predefinito di Hello utilizzato quando non viene specificato alcun criterio è toocopy tutti gli elementi. Non è consentito specificare più criteri file. |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a>Utilizzare i dati di toocopy AdlCopy (come file autonomo) di un blob di archiviazione di Azure
1. Aprire un prompt dei comandi e passare toohello directory in cui AdlCopy è installato, in genere `%HOMEPATH%\Documents\adlcopy`.
2. Eseguire hello successivo comando toocopy un blob specifico da hello origine contenitore tooa archivio Data Lake:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    ad esempio:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] sintassi di Hello precedente specifica hello file toobe tooa copiati cartella account archivio Data Lake hello. Strumento AdlCopy crea una cartella se il nome di cartella specificato hello non esiste.

    Sarà richiesto tooenter credenziali hello per hello sottoscrizione di Azure in cui si dispone di account archivio Data Lake. Verrà visualizzato un esempio di toohello simile output:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. È inoltre possibile copiare tutti i BLOB hello dall'account archivio Data Lake toohello di un contenitore utilizzando hello comando seguente:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    ad esempio:

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a>Considerazioni sulle prestazioni

Se si copia da un account di archiviazione Blob di Azure, possono essere limitate durante la copia sul lato di archiviazione blob di hello. Si riducono le prestazioni di hello del processo di copia. toolearn ulteriori informazioni sui limiti di hello dell'archiviazione Blob di Azure, vedere i limiti di archiviazione di Azure in [sottoscrizione di Azure e limiti dei servizi](../azure-subscription-service-limits.md).

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a>Utilizzare i dati di toocopy AdlCopy (come file autonomo) di un altro account archivio Data Lake
È inoltre possibile utilizzare dati toocopy AdlCopy tra due account archivio Data Lake.

1. Aprire un prompt dei comandi e passare toohello directory in cui AdlCopy è installato, in genere `%HOMEPATH%\Documents\adlcopy`.
2. Eseguire hello successivo comando toocopy un file specifico da un archivio Data Lake account tooanother.

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    ad esempio:

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > sintassi di Hello precedente specifica hello file toobe tooa copiati cartella account archivio Data Lake di destinazione hello. Strumento AdlCopy crea una cartella se il nome di cartella specificato hello non esiste.
   >
   >

    Sarà richiesto tooenter credenziali hello per hello sottoscrizione di Azure in cui si dispone di account archivio Data Lake. Verrà visualizzato un esempio di toohello simile output:

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. Hello comando seguente copia tutti i file da una cartella nella cartella tooa account hello origine archivio Data Lake nella destinazione hello account archivio Data Lake.

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a>Considerazioni sulle prestazioni

Quando si utilizza AdlCopy come strumento autonomo, copia hello viene eseguito su condiviso, le risorse gestite di Azure. prestazioni Hello che è possibile che venga visualizzato in questo ambiente dipendono dal carico del sistema e le risorse disponibili. Questa modalità è più adatta ai trasferimenti di piccole dimensioni eseguiti ad hoc. Nessun parametro necessario toobe ottimizzati quando si utilizza AdlCopy come strumento autonomo.

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a>Utilizzare i dati toocopy AdlCopy (con l'account Data Lake Analitica)
È inoltre possibile utilizzare il Analitica Lake dati account tooData Lake archivio BLOB di hello toorun dati toocopy del processo AdlCopy dall'archiviazione di Azure. Questa opzione viene utilizzata in genere quando toobe dati hello spostato è compreso nell'intervallo di hello di gigabyte e terabyte e si desidera la velocità effettiva prevedibile e migliori prestazioni.

toouse che account Data Lake Analitica con toocopy AdlCopy da un Blob di archiviazione di Azure, origine hello (Blob di archiviazione di Azure) deve essere aggiunto come un'origine dati per l'account Data Lake Analitica. Per istruzioni sull'aggiunta di account Data Lake Analitica tooyour origini di dati aggiuntivi, vedere [gestire Data Lake Analitica account origini dati](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).

> [!NOTE]
> Se si copia da un account archivio Azure Data Lake come origine di hello usando un account Data Lake Analitica, non è necessario tooassociate hello account archivio Data Lake con hello account Data Lake Analitica. Hello requisito tooassociate hello origine store con account Data Lake Analitica hello è solo quando l'origine hello è un account di archiviazione di Azure.
>
>

Eseguire i seguenti toocopy comando da un account archivio Data Lake di archiviazione di Azure blob tooa utilizzando account Data Lake Analitica hello:

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

ad esempio:

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

Analogamente, l'esecuzione dopo toocopy comando da un account di archiviazione di Azure blob tooa archivio Data Lake utilizzando account Data Lake Analitica hello:

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a>Considerazioni sulle prestazioni

Quando si copiano dati nell'intervallo di hello di terabyte, l'uso di AdlCopy con il proprio account Azure Data Lake Analitica offre prestazioni migliori e più prevedibile. il parametro Hello che verranno ottimizzato è il numero di hello di Azure Data Lake Analitica unità toouse per il processo di copia hello. Aumentare il numero di hello unità migliorano le prestazioni di hello del processo di copia. Ogni toobe file copiato è possibile utilizzare un'unità massima. Specifica di più unità di numero hello di file da copiare non migliorano le prestazioni.

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a>Utilizzare i dati di toocopy AdlCopy utilizzando criteri di ricerca
In questa sezione viene illustrato come toouse AdlCopy toocopy dati da un'origine (nell'esempio riportato di seguito è usare Blob di archiviazione di Azure) tooa account archivio Data Lake di destinazione utilizzando criteri di ricerca. Ad esempio, è possibile utilizzare passaggi hello sotto toocopy tutti i file con estensione csv dalla destinazione toohello blob di origine hello.

1. Aprire un prompt dei comandi e passare toohello directory in cui AdlCopy è installato, in genere `%HOMEPATH%\Documents\adlcopy`.
2. Eseguire hello successivo comando toocopy tutti i file con estensione CSV da un blob specifico da hello origine contenitore tooa archivio Data Lake:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    ad esempio:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a>Fatturazione
* Se si utilizza lo strumento AdlCopy hello come autonomo che verrà fatturato per i costi di uscita per lo spostamento di dati, se non è in origine hello account di archiviazione Azure hello stessa area come hello archivio Data Lake.
* Se si utilizza lo strumento AdlCopy hello con il Analitica Lake dati account standard [Data Lake Analitica tariffe di fatturazione](https://azure.microsoft.com/pricing/details/data-lake-analytics/) verranno applicate.

## <a name="considerations-for-using-adlcopy"></a>Considerazioni sull'uso di AdlCopy
* AdlCopy (per la versione 1.0.5) supporta la copia dei dati da origini che collettivamente contengono migliaia di file e cartelle. Tuttavia, se si verificano problemi con la copia di un set di dati di grandi dimensioni, è possibile distribuire file e cartelle hello in sottocartelle diverse e utilizzare invece le sottocartelle di hello percorso toothose come origine di hello.

## <a name="performance-considerations-for-using-adlcopy"></a>Considerazioni sulle prestazioni per l'uso di AdlCopy

AdlCopy supporta la copia dei dati che contengono migliaia di file e cartelle. Tuttavia, se si verificano problemi con la copia di un set di dati di grandi dimensioni, è possibile distribuire hello file e cartelle in sottocartelle più piccoli. AdlCopy è stato creato per copie ad hoc. Se si siano tentando di toocopy dati in modo ricorrente, è consigliabile utilizzare [Data Factory di Azure](../data-factory/data-factory-azure-datalake-connector.md) che fornisce la gestione completa per le operazioni di copia hello.

## <a name="release-notes"></a>Note sulla versione
* 1.0.13 - se si copiano dati toohello stesso account archivio Azure Data Lake tra adlcopy più comandi, non è necessario tooreenter le credenziali per ogni esecuzione di più. Adlcopy memorizza ora nella cache queste informazioni tra le diverse esecuzioni.

## <a name="next-steps"></a>Passaggi successivi
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
* [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usare Azure HDInsight con Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
