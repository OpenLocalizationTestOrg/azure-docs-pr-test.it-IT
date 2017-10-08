---
title: 'Output di Analisi di flusso: opzioni per archiviazione, analisi | Microsoft Docs'
description: Informazioni sulla destinazione di opzioni di output dei dati di Analisi di flusso tra cui Power BI per i risultati dell'analisi.
keywords: trasformazione dei dati, risultati dell'analisi, opzioni di archiviazione dati
services: stream-analytics,documentdb,sql-database,event-hubs,service-bus,storage
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ba6697ac-e90f-4be3-bafd-5cfcf4bd8f1f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 99f8113f0464960e898293397fbe3de90d669857
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-outputs-options-for-storage-analysis"></a>Output di Analisi di flusso: opzioni per archiviazione, analisi
Durante la creazione di un processo di flusso Analitica, prendere in considerazione la modalità di utilizzo di dati risultante hello. Come si visualizzeranno risultati hello del processo di flusso Analitica hello e in cui verrà archiviata?

In ordine tooenable un'ampia gamma di modelli di applicazione, Azure flusso Analitica ha diverse opzioni per l'archiviazione di output e visualizzazione dei risultati dell'analisi. Questo rende l'output del processo tooview semplice e offre flessibilità nell'utilizzo di hello e l'archiviazione di output del processo hello per altri scopi e data warehousing. Qualsiasi output configurato nel processo di hello deve esistere prima hello processo viene avviato e gli eventi di inizio propagazione. Ad esempio, se si utilizza l'archiviazione Blob come output, il processo di hello non creerà un account di archiviazione automaticamente. È necessario che toobe creato dall'utente hello prima dell'avvio del processo ASA hello.

## <a name="azure-data-lake-store"></a>Archivio Azure Data Lake
Analisi di flusso supporta [Archivio Data Lake di Azure](https://azure.microsoft.com/services/data-lake-store/). Questa risorsa di archiviazione consente toostore dati di qualsiasi dimensione, tipo e l'inserimento di velocità per analitica operative ed esplorative. Inoltre, flusso Analitica esigenze toobe autorizzato archivio Data Lake di tooaccess hello. Informazioni dettagliate sulle autorizzazioni e come toosign per hello archivio Data Lake (se necessario) vengono discussi in hello [Data Lake di output articolo](stream-analytics-data-lake-output.md).

### <a name="authorize-an-azure-data-lake-store"></a>Autorizzare un Archivio Azure Data Lake
Se Data Lake archiviazione è stata selezionata come output nel portale di Azure hello, sarà richiesta tooauthorize un archivio connessione tooan esistente Data Lake.  

![Autorizzare Archivio Data Lake](./media/stream-analytics-define-outputs/06-stream-analytics-define-outputs.png)  

Compilare quindi la proprietà hello per hello archivio Data Lake di output come illustrato di seguito:

![Autorizzare Archivio Data Lake](./media/stream-analytics-define-outputs/07-stream-analytics-define-outputs.png)  

tabella Hello riportata di seguito sono elencati i nomi delle proprietà hello e la relativa descrizione necessari per la creazione di un archivio Data Lake di output.

<table>
<tbody>
<tr>
<td><B>NOME PROPRIETÀ</B></td>
<td><B>DESCRIZIONE</B></td>
</tr>
<tr>
<td>Alias di output</td>
<td>Si tratta di un nome descrittivo utilizzato nella query toodirect hello query output toothis archivio Data Lake.</td>
</tr>
<tr>
<td>Nome account</td>
<td>nome Hello di hello account Data Lake archiviazione in cui si invia l'output. Verrà visualizzata con un elenco di account archivio Data Lake toowhich hello utente registrati nel portale di toohello ha accesso a discesa.</td>
</tr>
<tr>
<td>Schema prefisso percorso [<I>facoltativo</I>]</td>
<td>Hello toowrite percorso file del file all'interno di hello specificati Account archivio Data Lake. <BR>{date}, {time}<BR>Esempio 1: folder1/logs/{date}/{time}<BR>Esempio 2: folder1/logs/{date}</td>
</tr>
<tr>
<td>Formato data [<I>facoltativo</I>]</td>
<td>Se il token di data hello viene utilizzato nel percorso di prefisso hello, è possibile selezionare il formato di data hello in cui sono organizzati i file. Esempio: AAAA/MM/GG</td>
</tr>
<tr>
<td>Formato ora [<I>facoltativo</I>]</td>
<td>Se il token di tempo hello viene utilizzato nel percorso di prefisso hello, specificare il formato di ora hello in cui i file sono organizzati. Il valore di hello solo supportato attualmente è HH.</td>
</tr>
<tr>
<td>Formato di serializzazione eventi</td>
<td>Formato di serializzazione per i dati di output. Sono supportati i formati JSON, CSV e Avro.</td>
</tr>
<tr>
<td>Codifica</td>
<td>Se il formato è CSV o JSON, è necessario specificare un formato di codifica. UTF-8 è hello formato di codifica è supportata solo in questo momento.</td>
</tr>
<tr>
<td>Delimitatore</td>
<td>Applicabile solo per la serializzazione CSV. Analisi di flusso supporta una serie di delimitatori comuni per la serializzazione dei dati CSV. I valori supportati sono virgola, punto e virgola, spazio, tabulazione e barra verticale.</td>
</tr>
<tr>
<td>Format</td>
<td>Applicabile solo per la serializzazione JSON. Separato da righe specifica che verrà formattato output di hello con ogni oggetto JSON sia separato da una nuova riga. Matrice specifica che verrà formattato come una matrice di oggetti JSON output di hello.</td>
</tr>
</tbody>
</table>

### <a name="renew-data-lake-store-authorization"></a>Rinnovare l'autorizzazione per Archivio Data Lake
Sarà necessario toore-autenticazione account archivio Data Lake la password è stato modificato dopo il processo di creazione o dell'ultima autenticazione.

![Autorizzare Archivio Data Lake](./media/stream-analytics-define-outputs/08-stream-analytics-define-outputs.png)  

## <a name="sql-database"></a>Database SQL
[database SQL di Azure](https://azure.microsoft.com/services/sql-database/) può essere usato come output per i dati di natura relazionale o per applicazioni che dipendono dal contesto ospitato in un database relazionale. I processi di flusso Analitica scriverà tooan di tabella esistente in un Database di SQL Azure.  Si noti che lo schema di tabella hello deve corrispondere esattamente i campi di hello e i tipi da output del processo. Un [Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/services/sql-data-warehouse/) può anche essere specificato come un output tramite hello SQL Database output anche l'opzione (si tratta di una funzionalità di anteprima). tabella Hello riportata di seguito sono elencati i nomi delle proprietà hello e la relativa descrizione per la creazione di un Database SQL di output.

| Nome proprietà | Descrizione |
| --- | --- |
| Alias di output |Si tratta di un nome descrittivo utilizzato nel database toothis di output di query toodirect hello query. |
| Database |nome Hello del database di hello in cui si invia l'output |
| Server Name |nome del server di Database SQL di Hello |
| Username |nome utente che dispone di accesso toowrite toohello database Hello |
| Password |database di Hello password tooconnect toohello |
| Tabella |nome della tabella Hello in cui verrà scritto l'output di hello. nome della tabella Hello viene fatta distinzione tra maiuscole e minuscole e schema hello di questa tabella deve corrispondere esattamente toohello numero di campi e i tipi generati dall'output del processo. |

> [!NOTE]
> Offerta di Database SQL di Azure hello è attualmente supportato per un output del processo in flusso Analitica. Non è tuttavia supportata una macchina virtuale di Azure che esegue SQL Server con un database collegato. Si tratta dell'oggetto toochange nelle versioni future.
> 
> 

## <a name="blob-storage"></a>Archiviazione BLOB
Archiviazione BLOB offre una soluzione economica e scalabile per archiviare grandi quantità di dati non strutturati nel cloud hello.  Per un'introduzione all'archiviazione Blob di Azure e il relativo utilizzo, vedere la documentazione di hello in [come toouse BLOB](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

tabella Hello riportata di seguito sono elencati i nomi delle proprietà hello e la relativa descrizione per la creazione di un output di blob.

<table>
<tbody>
<tr>
<td>Nome proprietà</td>
<td>Descrizione</td>
</tr>
<tr>
<td>Alias di output</td>
<td>Si tratta di un nome descrittivo usato nell'archiviazione blob query toodirect hello query output toothis.</td>
</tr>
<tr>
<td>Account di archiviazione</td>
<td>nome Hello hello dell'account di archiviazione in cui si invia l'output.</td>
</tr>
<tr>
<td>Chiave dell'account di archiviazione</td>
<td>chiave segreta Hello associata con l'account di archiviazione hello.</td>
</tr>
<tr>
<td>Contenitore di archiviazione</td>
<td>I contenitori forniscono un raggruppamento logico dei blob archiviati nel servizio Blob di Microsoft Azure hello. Quando si carica un toohello blob del servizio Blob, è necessario specificare un contenitore per il blob.</td>
</tr>
<tr>
<td>Schema prefisso percorso [facoltativo]</td>
<td>percorso del file Hello utilizzato toowrite i BLOB nel contenitore specificato hello.<BR>Nel percorso di hello, è possibile scegliere uno o più istanze di segue frequenza hello toospecify 2 variabili che vengono scritti i BLOB hello toouse:<BR>{date}, {time}<BR>Esempio 1: cluster1/logs/{date}/{time}<BR>Esempio 2: cluster1/logs/{date}</td>
</tr>
<tr>
<td>Formato data [facoltativo]</td>
<td>Se il token di data hello viene utilizzato nel percorso di prefisso hello, è possibile selezionare il formato di data hello in cui sono organizzati i file. Esempio: AAAA/MM/GG</td>
</tr>
<tr>
<td>Formato ora [facoltativo]</td>
<td>Se il token di tempo hello viene utilizzato nel percorso di prefisso hello, specificare il formato di ora hello in cui i file sono organizzati. Il valore di hello solo supportato attualmente è HH.</td>
</tr>
<tr>
<td>Formato di serializzazione eventi</td>
<td>Formato di serializzazione per i dati di output.  Sono supportati i formati JSON, CSV e Avro.</td>
</tr>
<tr>
<td>Codifica</td>
<td>Se il formato è CSV o JSON, è necessario specificare un formato di codifica. UTF-8 è hello formato di codifica è supportata solo in questo momento.</td>
</tr>
<tr>
<td>Delimitatore</td>
<td>Applicabile solo per la serializzazione CSV. Analisi di flusso supporta una serie di delimitatori comuni per la serializzazione dei dati CSV. I valori supportati sono virgola, punto e virgola, spazio, tabulazione e barra verticale.</td>
</tr>
<tr>
<td>Format</td>
<td>Applicabile solo per la serializzazione JSON. Separato da righe specifica che verrà formattato output di hello con ogni oggetto JSON sia separato da una nuova riga. Matrice specifica che verrà formattato come una matrice di oggetti JSON output di hello. Questa matrice verrà chiusa solo quando si arresta processo hello o Analitica di flusso è stato spostato toohello successivo intervallo di tempo. In generale, è preferibile toouse riga JSON separati, poiché non richiede una gestione speciale mentre i file di output di hello è ancora scritto.</td>
</tr>
</tbody>
</table>

## <a name="event-hub"></a>Hub eventi
[Hub eventi](https://azure.microsoft.com/services/event-hubs/) è un ingestor di eventi di pubblicazione-sottoscrizione altamente scalabile. Può raccogliere milioni di eventi al secondo.  Un utilizzo di un Hub eventi come output è l'output di hello di un processo di flusso Analitica sarà input hello di un altro processo di streaming.

Esistono alcuni parametri che sono necessari tooconfigure flussi di dati di Hub eventi come output.

| Nome proprietà | Descrizione |
| --- | --- |
| Alias di output |Si tratta di un nome descrittivo utilizzato nella query toodirect hello query output toothis Hub eventi. |
| Spazio dei nomi del bus di servizio |Uno spazio dei nomi Service Bus è un contenitore per un set di entità di messaggistica. Quando si crea un nuovo hub eventi, viene anche creato uno spazio dei nomi del bus di servizio |
| Hub eventi |nome Hello dell'output di Hub eventi |
| Nome criterio hub eventi |criteri di accesso condiviso Hello, che possono essere creati nella scheda Configura dell'Hub eventi hello. Ogni criterio di accesso condiviso ha un nome, autorizzazioni impostate e tasti di scelta |
| Chiave criterio hub eventi |chiave di accesso condiviso Hello utilizzata tooauthenticate accesso toohello Bus di servizio spazio dei nomi |
| Colonna chiave di partizione [facoltativo] |Questa colonna contiene la chiave di partizione hello per l'output di Hub eventi. |
| Formato di serializzazione eventi |Formato di serializzazione per i dati di output.  Sono supportati i formati JSON, CSV e Avro. |
| Codifica |Per CSV e JSON, UTF-8 è hello formato di codifica è supportata solo in questo momento |
| Delimitatore |Applicabile solo per la serializzazione CSV. Analisi di flusso supporta una serie di delimitatori comuni per la serializzazione dei dati in formato CSV. I valori supportati sono virgola, punto e virgola, spazio, tabulazione e barra verticale. |
| Format |Applicabile solo per il tipo JSON. Separato da righe specifica che verrà formattato output di hello con ogni oggetto JSON sia separato da una nuova riga. Matrice specifica che verrà formattato come una matrice di oggetti JSON output di hello. |

## <a name="power-bi"></a>Power BI
[Power BI](https://powerbi.microsoft.com/) utilizzabile come output per un tooprovide processo Analitica di flusso per un'esperienza di visualizzazione completa dei risultati dell'analisi. Questa funzionalità può essere usata per i dashboard operativi, la generazione di report e la creazione di report basati sulle metriche.

### <a name="authorize-a-power-bi-account"></a>Autorizzare un account Power BI
1. Quando Power BI è stata selezionata come output nel portale di Azure hello, sarà possibile tooauthorize richiesto un utente di Power BI esistente o toocreate un nuovo account di Power BI.  
   
   ![Autorizzare l'utente di Power BI](./media/stream-analytics-define-outputs/01-stream-analytics-define-outputs.png)  
2. Creare un nuovo account se non è ancora presente, quindi scegliere Autorizza ora.  Viene visualizzata una schermata simile hello seguente.  
   
   ![Power BI account Azure](./media/stream-analytics-define-outputs/02-stream-analytics-define-outputs.png)  
3. In questo passaggio, fornire il hello o scuola account per autorizzare l'output di hello Power BI. Se non si è già iscritti a Power BI, scegliere Iscriviti ora. Hello account aziendale o dell'istituto di istruzione usato per Power BI potrebbe essere diverso dall'account di sottoscrizione di Azure che si è connessi con hello.

### <a name="configure-hello-power-bi-output-properties"></a>Configurare le proprietà di output di hello Power BI
Dopo aver creato hello Power BI account autenticati, è possibile configurare le proprietà di hello per l'output di Power BI. tabella Hello riportata di seguito è elenco hello di nomi di proprietà e i relativi tooconfigure descrizione l'output di Power BI.

| Nome proprietà | Descrizione |
| --- | --- |
| Alias di output |Si tratta di un nome descrittivo utilizzato nella query toodirect hello query output toothis output di Power BI. |
| Area di lavoro del gruppo |tooenable condivisione dei dati con altri utenti di Power BI è possibile selezionare gruppi all'interno di Power BI account oppure scegliere "Area di lavoro personale" Se non si desidera toowrite tooa gruppo.  L'aggiornamento di un gruppo esistente, è necessario rinnovare l'autenticazione a Power BI hello. |
| Nome del set di dati |Fornire un nome di set di dati che si desidera per Power BI hello output toouse |
| Nome tabella |Specificare un nome di tabella nel set di dati di hello di hello output di Power BI. Attualmente, l’output di Power BI da processi di Analisi di flusso può avere solo una tabella in un set di dati |

Per una panoramica della configurazione di un output di Power BI e i dashboard, vedere hello [Analitica di flusso di Azure e Power BI](stream-analytics-power-bi-dashboard.md) articolo.

> [!NOTE]
> Non creare in modo esplicito hello dataset e nel dashboard di Power BI hello. Hello set di dati e la tabella verrà popolate automaticamente quando viene avviato il processo di hello e hello inizia distribuzione output in Power BI. Si noti che se non genera query processo hello eventuali risultati, il set di dati hello e non verrà creata nella tabella. Occorre essere consapevoli che, se Power BI dispone già di un set di dati e una tabella con hello stesso nome hello uno fornito in questo processo di flusso Analitica, hello i dati esistenti verranno sovrascritti.
> 
> 

### <a name="schema-creation"></a>Creazione dello schema
Azure Analitica flusso crea un set di dati di Power BI e una tabella per conto di utente hello se non ne esiste già. In tutti gli altri casi, la tabella hello viene aggiornata con nuovi valori. Attualmente, è presente una limitazione di hello può esistere solo una tabella all'interno di un set di dati.

### <a name="data-type-conversion-from-asa-toopower-bi"></a>Conversione da tooPower ASA BI tipo di dati
Azure flusso Analitica aggiorna il modello di dati hello in modo dinamico in fase di esecuzione se le modifiche dello schema di output di hello. Vengono rilevate tutte le modifiche di nome di colonna, le modifiche di tipo di colonna e hello aggiunta o rimozione di colonne.

Nella tabella sono incluse le conversioni di tipo di dati hello da [tipi di dati di flusso Analitica](https://msdn.microsoft.com/library/azure/dn835065.aspx) tooPower BIs [tipi Entity Data Model (EDM)](https://powerbi.microsoft.com/documentation/powerbi-developer-walkthrough-push-data/) se un set di dati di POWER BI e una tabella non esiste.


Dall'analisi di flusso | tooPower BI
-----|-----|------------
bigint | Int64
nvarchar(max) | String
datetime | DateTime
float | Double
Matrice di record | Tipo String, valore di tipo Constant "IRecord" o "IArray"

### <a name="schema-update"></a>Aggiornamento dello schema
Flusso Analitica deriva hello schema di modello di dati basato sul primo set di eventi nell'output di hello di hello. In seguito, se necessario, schema del modello di dati hello viene aggiornato tooaccommodate gli eventi in entrata che potrebbero non essere adatto nello schema originale hello.

Hello `SELECT *` query devono essere evitati aggiornare lo schema dinamico tooprevent su più righe. Inoltre toopotential implicazioni sulle prestazioni, potrebbe inoltre causare indeterminacy di tempo per ottenere risultati hello hello. campi esatti Hello necessario visualizzate nel dashboard di Power BI toobe devono essere selezionati. Inoltre, i valori dei dati hello devono essere conformi con hello scelta tipo di dati.


Precedente/Corrente | Int64 | string | DateTime | Double
-----------------|-------|--------|----------|-------
Int64 | Int64 | String | String | Double
Double | Double | string | String | Double
string | String | String | String |  | string | 
DateTime | string | string |  DateTime | String


### <a name="renew-power-bi-authorization"></a>Rinnovare l'autorizzazione di Power BI
Sarà necessario toore-autenticazione account di Power BI, la password è stato modificato dopo il processo di creazione o dell'ultima autenticazione. Multi-Factor Authentication (MFA) è configurata nel tenant di Azure Active Directory (AAD) è necessario anche autorizzazioni di Power BI toorenew ogni 2 settimane. Un sintomo di questo problema è alcun output del processo e un "Esegui autenticazione utente errore" nel log delle operazioni hello:

  ![Errore token di aggiornamento di Power BI](./media/stream-analytics-define-outputs/03-stream-analytics-define-outputs.png)  

tooresolve questo problema, arrestare il processo in esecuzione e passare l'output di Power BI tooyour.  Fare clic sul collegamento "Rinnovo authorization" hello e riavviare il processo dalla perdita di dati di ora ultimo arresto tooavoid hello.

  ![Rinnovo di autorizzazione di Power BI](./media/stream-analytics-define-outputs/04-stream-analytics-define-outputs.png)  

## <a name="table-storage"></a>Archiviazione tabelle
[Archiviazione tabelle di Azure](../storage/common/storage-introduction.md) offre l'archiviazione a disponibilità elevata, altamente scalabile, in modo da un'applicazione può ridimensionare automaticamente la richiesta di toomeet degli utenti. Archiviazione tabelle è archivio o l'attributo chiave NoSQL di Microsoft quale è possibile sfruttare per i dati strutturati con meno vincoli schema hello. Archiviazione tabelle di Azure può essere utilizzato toostore dati per la persistenza e il recupero efficiente.

tabella Hello riportata di seguito sono elencati i nomi delle proprietà hello e la relativa descrizione per la creazione di un output di tabella.

| Nome proprietà | Descrizione |
| --- | --- |
| Alias di output |Si tratta di un nome descrittivo usato nell'archiviazione tabelle query toodirect hello query output toothis. |
| Account di archiviazione |nome Hello hello dell'account di archiviazione in cui si invia l'output. |
| Chiave dell'account di archiviazione |chiave di accesso Hello associata con l'account di archiviazione hello. |
| Nome tabella |nome di Hello della tabella hello. tabella Hello verrà ottenere creata se non esiste. |
| Chiave di partizione |nome Hello hello output colonna contenente hello della chiave di partizione. chiave di partizione Hello è un identificatore univoco per partizione hello all'interno di una tabella specificata e costituisce hello prima parte della chiave primaria di un'entità. È un valore stringa che può essere too1 KB di dimensioni. |
| Chiave di riga |nome Hello hello output contenente hello riga della chiave della colonna. chiave di riga Hello è un identificatore univoco per un'entità all'interno di una determinata partizione. Forma hello seconda parte chiave primaria di un'entità. chiave di riga Hello è un valore stringa che può essere too1 KB di dimensioni. |
| Dimensioni batch |numero di Hello di record per un'operazione batch. In genere predefinito hello è sufficiente per la maggior parte dei processi, vedere toohello [specifica operazione Batch tabella](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx) per ulteriori informazioni su come modificare questa impostazione. |

## <a name="service-bus-queues"></a>Code del bus di servizio
[Code di Service Bus](https://msdn.microsoft.com/library/azure/hh367516.aspx) offrono un First In, tooone di recapito di messaggi FIFO (First Out) o più consumer concorrenti. In genere, i messaggi sono previsti toobe ricevuti ed elaborati dai ricevitori hello in ordine temporale di hello in cui sono stati aggiunti toohello coda e ogni messaggio viene ricevuto ed elaborato da un solo consumer di messaggi.

tabella Hello riportata di seguito sono elencati i nomi delle proprietà hello e la relativa descrizione per la creazione di un coda output.

| Nome proprietà | Descrizione |
| --- | --- |
| Alias di output |Si tratta di un nome descrittivo utilizzato nella query toodirect hello query output toothis coda del Bus di servizio. |
| Spazio dei nomi del bus di servizio |Uno spazio dei nomi Service Bus è un contenitore per un set di entità di messaggistica. |
| Nome coda |nome Hello di hello coda del Bus di servizio. |
| Nome criteri coda |Quando si crea una coda, è anche possibile creare criteri di accesso condiviso nella scheda Configura coda hello. Ogni criterio di accesso condiviso dispone di un nome, delle autorizzazioni impostate, e di tasti di scelta. |
| Chiave criteri coda |chiave di accesso condiviso Hello utilizzata tooauthenticate accesso toohello Bus di servizio spazio dei nomi |
| Formato di serializzazione eventi |Formato di serializzazione per i dati di output.  Sono supportati i formati JSON, CSV e Avro. |
| Codifica |Per CSV e JSON, UTF-8 è hello formato di codifica è supportata solo in questo momento |
| Delimitatore |Applicabile solo per la serializzazione CSV. Analisi di flusso supporta una serie di delimitatori comuni per la serializzazione dei dati in formato CSV. I valori supportati sono virgola, punto e virgola, spazio, tabulazione e barra verticale. |
| Format |Applicabile solo per il tipo JSON. Separato da righe specifica che verrà formattato output di hello con ogni oggetto JSON sia separato da una nuova riga. Matrice specifica che verrà formattato come una matrice di oggetti JSON output di hello. |

## <a name="service-bus-topics"></a>Argomenti del bus di servizio
Anche se le code Service Bus fornisce un metodo di comunicazione tooone dal mittente tooreceiver, [argomenti del Bus di servizio](https://msdn.microsoft.com/library/azure/hh367516.aspx) forniscono una comunicazione forma uno-a-molti.

tabella Hello riportata di seguito sono elencati i nomi delle proprietà hello e la relativa descrizione per la creazione di un output di tabella.

| Nome proprietà | Descrizione |
| --- | --- |
| Alias di output |Si tratta di un nome descrittivo utilizzato nella query toodirect hello query output toothis argomento del Bus di servizio. |
| Spazio dei nomi del bus di servizio |Uno spazio dei nomi Service Bus è un contenitore per un set di entità di messaggistica. Quando si crea un nuovo hub eventi, viene anche creato uno spazio dei nomi del bus di servizio |
| Nome argomento |Gli argomenti sono messaggistica entità, gli hub tooevent simile e code. Si tratta di flussi di eventi toocollect progettato da una serie di diversi dispositivi e servizi. Quando un argomento viene creato, gli viene assegnato un nome specifico. invio di messaggi Hello tooa argomento non sarà disponibile a meno che non viene creata una sottoscrizione, verificare esistono una o più sottoscrizioni in argomento hello |
| Nome criteri argomento |Quando si crea un argomento, è anche possibile creare criteri di accesso condiviso nella scheda Configura argomento hello. Ogni criterio di accesso condiviso ha un nome, autorizzazioni impostate e tasti di scelta |
| Chiave criteri argomento |chiave di accesso condiviso Hello utilizzata tooauthenticate accesso toohello Bus di servizio spazio dei nomi |
| Formato di serializzazione eventi |Formato di serializzazione per i dati di output.  Sono supportati i formati JSON, CSV e Avro. |
| Codifica |Se il formato è CSV o JSON, è necessario specificare un formato di codifica. UTF-8 è hello formato di codifica è supportata solo in questo momento |
| Delimitatore |Applicabile solo per la serializzazione CSV. Analisi di flusso supporta una serie di delimitatori comuni per la serializzazione dei dati in formato CSV. I valori supportati sono virgola, punto e virgola, spazio, tabulazione e barra verticale. |

## <a name="azure-cosmos-db"></a>Azure Cosmos DB
[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) è un servizio di database di documenti NoSQL completamente gestito che offre query e transazioni su dati senza schema, prestazioni prevedibili e affidabili e sviluppo rapido.

Hello sotto i nomi delle proprietà di elenco dettagli hello e la relativa descrizione per la creazione di un database di Azure Cosmos di output.

* **Alias di output** – toorefer un alias per questo output nella query ASA  
* **Nome account** : hello nome o l'URI di hello account Cosmos DB dell'endpoint.  
* **Chiave account** : chiave di accesso condiviso hello per hello Cosmos DB account.  
* **Database** : nome del database DB Cosmos hello.  
* **Modello di nome raccolta** : hello raccolta o il nome relativo modello per hello raccolte toobe utilizzato. formato di nome raccolta Hello può essere costruito utilizzando token {partition} facoltativo hello, in cui le partizioni iniziano da 0. Di seguito sono riportati input di esempio validi:  
  1\) MyCollection: deve essere presente una raccolta denominata "MyCollection".  
  2\) MyCollection{partizione}: devono essere presenti le raccolte "MyCollection0", "MyCollection1", "MyCollection2" e così via.  
* **Chiave di partizione**: valore facoltativo. È necessario solo se si usa un token {partition} nel modello del nome di raccolta. nome di Hello del campo hello in output chiave hello toospecify di eventi utilizzati per il partizionamento dell'output tra raccolte. Per l'output di una singola raccolta si può usare qualsiasi colonna di output arbitraria, ad esempio PartitionId.  
* **ID documento** : valore facoltativo. nome di Hello di hello campo negli eventi di output utilizzato chiave primaria hello toospecify su quali insert o update sono basate le operazioni.  


## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
Sono state introdotte tooStream Analitica, un servizio gestito per lo streaming analitica dei dati di hello Internet delle cose. toolearn ulteriori informazioni su questo servizio, vedere:

* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
