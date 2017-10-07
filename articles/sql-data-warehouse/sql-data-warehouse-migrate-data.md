---
title: aaaMigrate il tooSQL di dati Data Warehouse | Documenti Microsoft
description: Suggerimenti per la migrazione del tooAzure di dati SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a>Eseguire la migrazione dei dati
È possibile spostare dati da differenti origini a SQL Data Warehouse con diversi strumenti,  Copia file ADF SSIS e bcp può tutti tooachieve usato questo obiettivo. Tuttavia, man mano che aumenta la quantità hello di dati è necessario considerare suddivisione migrazione dei dati hello in passaggi. Ciò consente hello opportunità toooptimize ogni passaggio sia per le prestazioni e per la resilienza tooensure una migrazione dei dati uniforme.

In questo articolo viene innanzitutto gli scenari di migrazione semplice hello di copia file ADF SSIS e bcp. Quindi approfondire in modalità migrazione hello può essere ottimizzata.

## <a name="azure-data-factory-adf-copy"></a>ADF Copy
[ADF Copy][ADF Copy] fa parte di [Azure Data Factory][Azure Data Factory]. È possibile utilizzare Copia ADF tooexport tooflat dei file di dati che risiedono nell'archiviazione locale, file flat tooremote contenute nell'archiviazione blob di Azure o direttamente in SQL Data Warehouse.

Se i dati viene avviato in file flat, quindi è necessario innanzitutto tootransfer il blob di archiviazione tooAzure prima dell'avvio di un carico in SQL Data Warehouse. Una volta hello dati vengono trasferiti nell'archiviazione blob di Azure è possibile scegliere toouse [copia ADF] [ ADF Copy] nuovamente i dati hello toopush in SQL Data Warehouse.

PolyBase offre inoltre un'opzione di ad alte prestazioni per il caricamento dei dati di hello. Questo non significa però che debbano essere usati due strumenti anziché uno. Se è necessario ottenere prestazioni ottimali hello, usare PolyBase. Se si desidera un'esperienza singolo strumento (e i dati di hello non sono larga) ADF è la risposta.


> 
> 

Head su toohello articolo per alcuni elevate seguente [esempi ADF][ADF samples].

## <a name="integration-services"></a>Integration Services
Integration Services (SSIS) è uno strumento sofisticato e flessibile di Extract Transform and Load (ETL) che supporta flussi di lavoro complessi, la trasformazione dei dati e diverse opzioni di caricamento dei dati. Utilizzare SSIS toosimply trasferimento dati tooAzure o come parte di una migrazione più ampia.

> [!NOTE]
> SSIS è possibile esportare tooUTF-8 senza hello ordine dei byte nel file hello. Ciò è necessario utilizzare hello derivato colonna componente tooconvert hello dati di tipo carattere tooconfigure hello flusso toouse hello 65001 UTF-8 codice pagina di dati. Una volta colonne hello sono state convertite, scrivere hello dati toohello file flat destinazione adapter assicurandosi che 65001 è stata selezionata anche come pagina di codice hello per file hello.
> 
> 

SSIS si connette tooSQL Data Warehouse come connessione tooa distribuzione di SQL Server. Tuttavia, le connessioni saranno necessario toobe utilizzando una gestione connessione ADO.NET. Inoltre è necessario tooconfigure hello "Utilizzare inserimento bulk quando disponibili" velocità effettiva toomaximize impostazione. Consultare toohello [adattatore di destinazione ADO.NET] [ ADO.NET destination adapter] toolearn articolo informazioni su questa proprietà

> [!NOTE]
> Connessione tooAzure SQL Data Warehouse mediante OLEDB non è supportata.
> 
> 

Inoltre, vi è sempre hello possibilità che un pacchetto potrebbe non riuscire a causa di problemi di rete o toothrottling. Progettazione pacchetti in modo possano essere ripresi nel punto di hello di errore, senza il rollforward di lavoro completate prima errore hello.

Per ulteriori informazioni consultare hello [documentazione SSIS][SSIS documentation].

## <a name="bcp"></a>bcp
L'utilità della riga di comando bcp è progettata per l'importazione e l'esportazione di dati di file flat. Durante l'esportazione di dati possono essere eseguite trasformazioni. trasformazioni semplice tooperform utilizzano tooselect una query e trasformare i dati di hello. Una volta esportato, file flat hello possono quindi essere caricati direttamente nel database di SQL Data Warehouse di hello destinazione hello.

> [!NOTE]
> È spesso un hello tooencapsulate consigliabile esportano le trasformazioni utilizzate durante i dati in una vista nel sistema di origine hello. Ciò garantisce che la logica di hello viene mantenuta e processo hello è ripetibile.
> 
> 

I vantaggi derivanti dall'uso dell'utilità bcp sono i seguenti:

* Semplicità. i comandi bcp sono toobuild semplice ed eseguire
* Possibilità di riavviare il processo di caricamento. Una volta esportato hello carico può essere eseguita qualsiasi numero di volte

Le limitazioni dell'utilità bcp sono le seguenti:

* Funziona solo con file flat tabulari. Non funziona ad esempio con file XML o JSON.
* Funzionalità di trasformazione dei dati sono toohello limitato solo fase di esportazione e semplici
* bcp non è stato adattato toobe affidabili durante il caricamento dei dati su hello internet. Qualsiasi instabilità della rete può causare un errore di caricamento.
* utilità bcp si basa sullo schema di hello presente carico toohello precedente del database di destinazione hello

Per ulteriori informazioni, vedere [utilizzare dati tooload bcp in SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].

## <a name="optimizing-data-migration"></a>Ottimizzazione della migrazione dei dati
Un processo di migrazione di dati SQLDW può essere suddiviso in modo efficace in tre passaggi discreti:

1. Esportazione dei dati di origine
2. Trasferimento di dati tooAzure
3. Caricare nel database di hello destinazione SQLDW

Ogni passaggio può essere ottimizzato singolarmente toocreate un processo di migrazione affidabile, nuovamente avviato e resiliente che ottimizza le prestazioni a ogni passaggio.

## <a name="optimizing-data-load"></a>Ottimizzazione del caricamento dei dati
Esaminando questi elementi in ordine inverso per un momento; dati tooload modo più veloci di Hello sono tramite PolyBase. Ottimizzazione di un processo di caricamento PolyBase posizionato prerequisiti hello passaggi precedenti, pertanto è migliore toounderstand questo iniziale. Sono:

1. Codifica dei file di dati
2. Formato dei file di dati
3. Percorso dei file di dati

### <a name="encoding"></a>Codifica
PolyBase richiede toobe i file di dati UTF-8 o UTF-16FE. 



### <a name="format-of-data-files"></a>Formato dei file di dati
PolyBase impone un carattere di terminazione di riga fisso \n o una nuova riga. I file di dati devono essere conforme toothis standard. Non esistono restrizioni per i caratteri di terminazione di colonna o stringa.

Sarà necessario toodefine ogni colonna nel file hello come parte della tabella esterna in PolyBase. Assicurarsi che tutte le colonne esportate sono obbligatori e che i tipi di hello conforme standard toohello richiesto.

Fare riferimento toohello [eseguire la migrazione dello schema] articolo per informazioni dettagliate sui tipi di dati supportati.

### <a name="location-of-data-files"></a>Percorso dei file di dati
SQL Data Warehouse usa esclusivamente dati di PolyBase tooload dall'archiviazione Blob di Azure. Di conseguenza, i dati di hello devono innanzitutto trasferiti nell'archiviazione blob.

## <a name="optimizing-data-transfer"></a>Ottimizzazione del trasferimento dei dati
Una delle parti di più lente hello della migrazione dei dati è il trasferimento di hello di hello tooAzure di dati. Non solo la larghezza di banda di rete può costituire un problema, ma anche l'affidabilità della rete può gravemente compromettere lo stato di avanzamento. Per impostazione predefinita la migrazione dei dati tooAzure è su internet hello così probabilità di errori di trasferimento che si verificano ragionevolmente probabilmente hello. Tuttavia, questi errori possono richiedere toobe dati inviati di nuovo in tutto o in parte.

Per fortuna sono diverse velocità di opzioni tooimprove hello e resilienza di questo processo:

### <a name="expressrouteexpressroute"></a>[ExpressRoute][ExpressRoute]
È possibile utilizzare tooconsider [ExpressRoute] [ ExpressRoute] toospeed di trasferimento hello. [ExpressRoute] [ ExpressRoute] fornisce con un tooAzure di stabilire una connessione privata in modo da non superare connessione hello hello rete internet pubblica. Non si tratta di un passaggio obbligatorio. Tuttavia, determina un miglioramento della velocità effettiva quando si tooAzure dati da un locale o funzionalità di condivisione percorso.

vantaggi dell'utilizzo di Hello [ExpressRoute] [ ExpressRoute] sono:

1. Maggiore affidabilità
2. Maggiore velocità di rete
3. Minore latenza di rete
4. Maggiore sicurezza di rete

[ExpressRoute] [ ExpressRoute] è utile per il numero di scenari; hello non appena la migrazione.

Per altre informazioni Per ulteriori informazioni e i prezzi, visitare hello [documentazione di ExpressRoute][ExpressRoute documentation].

### <a name="azure-import-and-export-service"></a>Servizio Importazione/Esportazione di Azure
Hello servizio di esportazione e importazione di Azure è un processo di trasferimento di dati progettato per trasferimenti grandi dimensioni (GB + +) toomassive (TB + +) dei dati in Azure. Comporta la scrittura di toodisks i dati e il loro trasferimento tooan data center di Azure. contenuto del disco Hello verrà quindi caricato nel BLOB di archiviazione di Azure per conto dell'utente.

Una panoramica del processo di esportazione importazione hello è come segue:

1. Configurare una data di archiviazione Blob di Azure contenitore tooreceive hello
2. Esportare l'archiviazione dei dati toolocal
3. Copiare hello dati too3.5 pollice SATA II/III unità disco rigido utilizzando hello [strumento di importazione/esportazione di Azure]
4. Creare un processo di importazione utilizzando hello importazione di Azure e il servizio di esportazione che fornisce file journal hello prodotti da hello [strumento di importazione/esportazione di Azure]
5. Spedire i dischi di hello del nominato data center di Azure
6. I dati vengono trasferiti tooyour contenitore di archiviazione Blob di Azure
7. Caricare i dati di hello in SQLDW con PolyBase

### <a name="azcopyazcopy-utility"></a>Utilità [AZCopy][AZCopy]
Hello [AZCopy][AZCopy] utilità è un ottimo strumento per ottenere i dati trasferiti nel BLOB di archiviazione Azure. È progettato per piccole (MB + +) toovery grandi dimensioni (GB + +) trasferimenti di dati. [AZCopy] è stato progettato tooprovide resilienti una velocità effettiva ottimale quando il trasferimento di dati tooAzure e pertanto è la scelta ideale per la fase di trasferimento dei dati hello. Una volta trasferiti, è possibile caricare i dati di hello usando PolyBase in SQL Data Warehouse. È anche possibile incorporare AZCopy nei pacchetti SSIS usando un'attività "Execute Process".

toouse AZCopy sarà anche necessario toodownload e installarlo prima. Sono disponibili una [versione di produzione][production version] e una [versione di anteprima][preview version].

tooupload un file dal file system che è necessario un comando simile hello uno di seguito:

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

Segue un riepilogo generale del processo:

1. Configurare un dati di hello tooreceive del contenitore di blob di archiviazione di Azure
2. Esportare l'archiviazione dei dati toolocal
3. I dati nel contenitore di archiviazione Blob di Azure hello AZCopy
4. Caricare i dati di hello in SQL Data Warehouse tramite PolyBase

Documentazione completa disponibile: [AZCopy][AZCopy].

## <a name="optimizing-data-export"></a>Ottimizzazione dell'esportazione dei dati
Inoltre tooensuring che esportazione hello conforme requisiti toohello disposti da PolyBase è anche possibile cercare esportazione hello toooptimize hello processo di data tooimprove hello ulteriormente.



### <a name="data-compression"></a>Compressione dei dati
PolyBase è in grado di leggere i dati compressi in file gzip. Se si è in grado di toocompress toogzip dei file di dati, quindi si verrà ridurre hello dati caduti rete hello.

### <a name="multiple-files"></a>File multipli
Suddividere le tabelle di grandi dimensioni in più file non solo consente di tooimprove esportare velocità, consente inoltre con trasferimento re-startability e la gestibilità complessiva dei dati di hello una volta nell'archiviazione blob di Azure di hello hello. Una delle numerose funzionalità interessante di PolyBase è che verrà letto tutti hello hello file all'interno di una cartella e considerarla come una tabella. È pertanto un file di hello buona tooisolate per ogni tabella nella relativa cartella.

PolyBase supporta anche una funzionalità nota come "attraversamento di cartelle ricorsivo". È possibile utilizzare questa funzionalità toofurther migliorare organizzazione hello di tooimprove i dati esportati la gestione dei dati.

toolearn più sul caricamento dei dati con PolyBase, vedere [dati tooload usare PolyBase in SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulla migrazione, vedere [eseguire la migrazione del Data Warehouse di tooSQL soluzione][Migrate your solution tooSQL Data Warehouse].
Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
