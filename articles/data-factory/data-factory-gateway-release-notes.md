---
title: note sulla aaaRelease per Gateway di gestione dati | Documenti Microsoft
description: Note sulla versione di Gateway di gestione dati
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a>Note sulla versione di Gateway di gestione dati
Una delle sfide hello per l'integrazione di dati più recenti è toomove dati tooand da toocloud locale. Data Factory rende l'integrazione con i Gateway di gestione dati, ovvero un agente che è possibile installare lo spostamento di dati locale tooenable ibrido.

Vedere i seguenti articoli per informazioni dettagliate su Gateway di gestione dati hello e come toouse è:

*  [Gateway di gestione dati](data-factory-data-management-gateway.md)
*  [Spostare dati tra un ambiente locale e il cloud mediante Azure Data Factory](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a>VERSIONE CORRENTE (2.10.6347.7)

### <a name="enhancements-"></a>Miglioramenti
- È possibile aggiungere bus di servizio toowhitelist le voci DNS anziché whitelist tutti gli indirizzi IP di Azure da un firewall (se necessario). È possibile trovare la rispettiva voce DNS nel portale di Azure (Data Factory -> "Creare e distribuire" -> "Gateway" -> "serviceUrls" (in JSON)
- Il connettore HDFS supporta ora il certificato pubblico autofirmato, consentendo di saltare la convalida SSL.
- Problema risolto: Problema con gateway offline durante l'aggiornamento (in scadenza inclinazione tooclock)



## <a name="earlier-versions"></a>Versioni precedenti

## <a name="2963132"></a>2.9.6313.2
### <a name="enhancements-"></a>Miglioramenti
-   È possibile aggiungere toowhitelist le voci DNS Service Bus anziché whitelist tutti gli indirizzi IP di Azure da un firewall (se necessario). Altri dettagli sono disponibili qui.
-   È ora possibile copiare dati da e verso un blob in blocchi singolo backup too4.75 TB, ovvero dimensioni hello massimo supportato di blob in blocchi. Il limite precedente era di 195 GB.
-   Corretto: problema relativo alla memoria esaurita durante la decompressione di alcuni file di piccole dimensioni durante l'attività di copia.
-   Problema risolto: Indice fuori problema intervallo durante la copia da DB documento tooan SQL Server locale con funzionalità idempotenza.
-   Corretto: lo script di pulizia di SQL non funziona con l'istanza locale di SQL Server dalla Copia guidata.
-   Problema risolto: Nome della colonna con lo spazio alla fine di hello non funziona nell'attività di copia.

## <a name="28662833"></a>2.8.66283.3
### <a name="enhancements-"></a>Miglioramenti
- Corretto: problema relativo alle credenziali mancanti al riavvio del computer gateway.
- Corretto: problema relativo alla registrazione durante il ripristino del gateway tramite un file di backup.


## <a name="2762401"></a>2.7.6240.1
### <a name="enhancements-"></a>Miglioramenti
- Corretto: lettura non corretta del valore Null decimale da Oracle come origine.

## <a name="2661922"></a>2.6.6192.2
### <a name="whats-new"></a>Novità
- Gli utenti possono fornire commenti e suggerimenti sull'esperienza di registrazione del gateway.
- Supporta il nuovo formato di compressione ZIP (Deflate)

### <a name="enhancements-"></a>Miglioramenti
- Miglioramento delle prestazioni per Oracle Sink, origine HDFS.
- Correzione di bug per l'aggiornamento automatico del gateway, capacità di elaborazione parallela del gateway.


## <a name="2561641"></a>2.5.6164.1
### <a name="enhancements"></a>Miglioramenti
- Migliore e più affidabile Gateway registrazione esperienza-ora è possibile monitorare lo stato di avanzamento durante il processo di registrazione Gateway hello, che rende la registrazione di hello esperienza più reattiva.
- Miglioramento Gateway ripristino configurazione di processo, è comunque possibile ripristinare i gateway anche se i file di backup gateway hello con questo aggiornamento non si dispone. In questo caso è necessario tooreset le credenziali di servizio collegato nel portale.
- Correzione di bug.

## <a name="2461511"></a>2.4.6151.1

### <a name="whats-new"></a>Novità

- È ora possibile archiviare localmente le credenziali dell'origine dati. Hello credenziali vengono crittografate. le credenziali dell'origine dati Hello possono essere ripristinate e ripristino i file di backup hello che possono essere esportati da hello locale tutti i Gateway esistente.

### <a name="enhancements-"></a>Miglioramenti

- Esperienza di registrazione gateway migliorata e più affidabile.
- Supporta il rilevamento automatico della configurazione QuoteChar di formato di testo in copia guidata e migliorare hello accuratezza di rilevamento di formato generale.

## <a name="2361002"></a>2.3.6100.2

- Support del rilevamento automatico di firstRowAsHeader e SkipLineCount nella copia guidata per i file di testo in HDFS e nel file system locale.
- Migliorare la stabilità di hello della connessione di rete tra i gateway e Bus di servizio
- Alcune correzioni di bug


## <a name="2260721"></a>2.2.6072.1

*  Supporta l'impostazione proxy HTTP per l'utilizzo di gateway hello hello Gateway Configuration Manager. Se configurato, l'accesso tramite proxy HTTP è disponibile per il BLOB di Azure, le tabelle di Azure, Azure Data Lake e Document DB.
*  Intestazione supporta gestione TextFormat quando si copiano dati dal File System locale tooAzure Blob, archivio Azure Data Lake e HDFS in locale.
*  Supporta la copia dei dati da Blob di accodamento e Blob di pagine insieme hello già supportati Blob in blocchi.
*  Introduce un nuovo stato del gateway **Online (limitato)**, che indica che le funzionalità principali di hello del gateway hello funziona ad eccezione di supporto delle operazioni interattive hello per la copia guidata.
*  Migliora l'affidabilità di hello di registrazione del gateway mediante la chiave di registrazione.

## <a name="216040"></a>2.1.6040.

*  Driver DB2 è incluso nel pacchetto di installazione di gateway hello ora. Non è necessario tooinstall è separatamente.
*  Driver DB2 supporta ora z/OS e DB2 per i (AS / 400) insieme a piattaforme di hello già supportate (Windows, Linux e Unix).
*  Supporta l'uso di Azure Cosmos DB come origine o destinazione per gli archivi dati locali.
*  Supporta la copia di archiviazione dei dati blob da/toocold/hot insieme hello già supportati account di archiviazione generico.
*  Consente di tooconnect tooon locale SQL Server tramite il gateway con privilegi di accesso remoto.  

## <a name="2060131"></a>2.0.6013.1

*  È possibile selezionare hello lingua toobe utilizzato da un gateway durante l'installazione manuale.

*  Quando il gateway non funziona come previsto, è possibile scegliere toosend registri del gateway di ultimi sette giorni tooMicrosoft toofacilitate risoluzione dei problemi di rilascio hello. Se il gateway non è connesso toohello servizio cloud, è possibile scegliere toosave e archiviare i registri del gateway.  

*  Miglioramenti all'interfaccia utente per la gestione della configurazione gateway:

    *  Rendere più visibile nella scheda Home di hello lo stato del gateway.

    *  Controlli riorganizzati e semplificati.

    *  È possibile copiare dati da un archivio utilizzando hello [strumento anteprima senza codice copia](data-factory-copy-data-wizard-tutorial.md). Per informazioni generiche su questa funzionalità, vedere [Copia di staging](data-factory-copy-activity-performance.md#staged-copy) .
*  È possibile utilizzare dati tooingress Gateway di gestione dati direttamente da un database di SQL Server locale in Azure Machine Learning.

*  Miglioramenti delle prestazioni

    * Prestazioni di visualizzazione migliorate dello schema e dell'anteprima in SQL Server nello strumento di anteprima della copia senza codice.

## <a name="11259531"></a>1.12.5953.1

*  Correzioni di bug

## <a name="11159181"></a>1.11.5918.1

*  Dimensione massima del registro eventi del gateway hello è stato aumentato da 1 MB too40 MB.

*  Nel caso in cui sia necessario un riavvio durante l'aggiornamento automatico del gateway, viene visualizzata una finestra di dialogo di avviso. È possibile scegliere toorestart destra quindi o versione successiva.

*  In caso di errore dell'aggiornamento automatico, il programma di installazione del gateway ritenta l'aggiornamento automatico al massimo tre volte.

*  Miglioramenti delle prestazioni

    * È possibile migliorare le prestazioni in caso di caricamento di tabelle di grandi dimensioni dal server locale in uno scenario di copia senza codice.

*  Correzioni di bug

## <a name="11058921"></a>1.10.5892.1

*  Miglioramenti delle prestazioni

*  Correzioni di bug

## <a name="1958652"></a>1.9.5865.2

*  Funzionalità di aggiornamento automatico senza intervento dell'utente
*  Nuova icona dell'area di notifica con indicatori di stato del gateway
*  Capacità troppo "Aggiorna" da client hello
*  Ora pianificazione dell'aggiornamento tooset possibilità
*  Script di PowerShell per attivare o disattivare l'aggiornamento automatico
*  Supporto per il formato JSON  
*  Miglioramenti delle prestazioni
*  Correzioni di bug

## <a name="1858221"></a>1.8.5822.1

*  Miglioramento dell'esperienza di risoluzione dei problemi
*  Miglioramenti delle prestazioni
*  Correzioni di bug

### <a name="1757951"></a>1.7.5795.1

*  Miglioramenti delle prestazioni
*  Correzioni di bug

### <a name="1757641"></a>1.7.5764.1

*  Miglioramenti delle prestazioni
*  Correzioni di bug

### <a name="1657351"></a>1.6.5735.1

*  Supporto di origine/sink HDFS in locale
*  Miglioramenti delle prestazioni
*  Correzioni di bug

### <a name="1656961"></a>1.6.5696.1

*  Miglioramenti delle prestazioni
*  Correzioni di bug

### <a name="1656761"></a>1.6.5676.1

*  Supporto degli strumenti di diagnostica in Gestione configurazione
*  Supporto delle colonne di tabella per le origini dati tabulari per Data factory di Azure
*  Supporto di SQL DW per Data factory di Azure
*  Supporto dell'isolamento in BlobSource e FileSource per Data factory di Azure
*  Supporto di CopyBehavior – MergeFiles, PreserveHierarchy e FlattenHierarchy in BlobSink e FileSink con copia binaria per Data Factory di Azure
*  Supporto dello stato di avanzamento della creazione di report per l'attività di copia per Data factory di Azure
*  Supporto della convalida della connettività dell'origine dati per Data factory di Azure
*  Correzioni di bug

### <a name="1656721"></a>1.6.5672.1

*  Supporto del nome di tabella per l'origine dati ODBC per Data factory di Azure
*  Miglioramenti delle prestazioni
*  Correzioni di bug

### <a name="1656581"></a>1.6.5658.1

*  Supporto del sink dei file per Data factory di Azure
*  Supporto del mantenimento della gerarchia nella copia binaria per Data factory di Azure
*  Supporto dell'idempotenza dell'attività di copia per Data factory di Azure
*  Correzioni di bug

### <a name="1656401"></a>1.6.5640.1

*  Supporto di altre 3 origini dati per Data factory di Azure (ODBC, OData, HDFS)
*  Supporto delle virgolette nel parser CSV per Data factory di Azure
*  Supporto della compressione (BZip2)
*  Correzioni di bug

### <a name="1556121"></a>1.5.5612.1

*  Supporto di cinque database relazionali per Data Factory di Azure (MySQL, PostgreSQL, DB2, Teradata e Sybase)
*  Supporto della compressione (Gzip e Deflate)
*  Miglioramenti delle prestazioni
*  Correzioni di bug

### <a name="1455491"></a>1.4.5549.1

*  Aggiunta del supporto dell'origine dati Oracle per Data factory di Azure
*  Miglioramenti delle prestazioni
*  Correzioni di bug

### <a name="1454921"></a>1.4.5492.1

*  File binario unificato che supporta il servizio Data factory di Microsoft Azure e il servizio Power BI di Office 365
*  Ridefinire il processo di registrazione e l'interfaccia utente di configurazione hello
*  Data Factory di Azure: supporto di ingresso e uscita in Azure per l'origine dati SQL Server

### <a name="1253031"></a>1.2.5303.1

*  Correggere timeout problema toosupport più connessioni a origini dati richiede molto tempo.

### <a name="1155268"></a>1.1.5526.8

*  Richiede .NET Framework 4.5.1 come prerequisito durante l'installazione.

### <a name="1051442"></a>1.0.5144.2

*  Nessuna modifica che interessi gli scenari di Data factory di Azure.
