---
title: Registra aaaCollect personalizzato in OMS Log Analitica | Documenti Microsoft
description: "Log Analytics può raccogliere gli eventi dai file di testo nei computer Windows e Linux.  In questo articolo viene descritto come toodefine un nuovo log personalizzato e i dettagli del record di hello che ha creato nel repository OMS hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: aca7f6bb-6f53-4fd4-a45c-93f12ead4ae1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: a75d058c371fecf7c43690a797d4e650c1570317
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-logs-in-log-analytics"></a>Log personalizzati in Log Analytics
origine dei dati di log personalizzati Hello in Log Analitica consente toocollect eventi dai file di testo nei computer Windows e Linux. Molte applicazioni log file di informazioni tootext anziché i servizi di registrazione standard, ad esempio il registro eventi di Windows o Syslog.  Una volta raccolti, è possibile analizzare ogni record di log hello nei campi tooindividual utilizzando hello [campi personalizzati](log-analytics-custom-fields.md) funzionalità di Log Analitica.

![Raccolta di log personalizzati](media/log-analytics-data-sources-custom-logs/overview.png)

Hello toobe di file di log raccolti deve corrispondere hello seguenti criteri.

- log Hello deve avere una sola voce per ogni riga o utilizzare un timestamp corrispondente uno dei seguenti hello formati all'inizio di hello di ciascuna voce.

    AAAA-MM-GG HH:MM:SS <br>M/G/AAAA HH:MM:SS AM/PM <br>Lun GG,AAAA HH:MM:SS

- file di log Hello deve consentire aggiornamenti circolari non in file hello viene sovrascritto con le nuove voci.
- file di log Hello deve usare la codifica ASCII o UTF-8.  Non sono supportati altri formati, ad esempio UTF-16.

>[!NOTE]
>Se sono presenti voci duplicate nel file di log hello, Log Analitica raccoglierà tali.  Tuttavia, i risultati della ricerca hello risulterà incoerente in cui i risultati del filtro hello mostrano ulteriori eventi di conteggio risultati hello.  Sarà importante convalidare hello log toodetermine se a causa di un'applicazione hello che l'ha creato questo comportamento e risolverlo prima di creare una definizione di raccolta log personalizzati hello se possibile.  
>
  
## <a name="defining-a-custom-log"></a>Definizione di un log personalizzato
Utilizzare hello seguendo procedure toodefine un file di log personalizzato.  Scorrere toohello fine di questo articolo per una procedura dettagliata di un esempio di aggiunta di un log personalizzato.

### <a name="step-1-open-hello-custom-log-wizard"></a>Passaggio 1. Aprire una creazione guidata Registro personalizzata hello
Creazione guidata Registro personalizzata Hello viene eseguita nel portale OMS hello e consente di toodefine un nuovo toocollect log personalizzato.

1. Nel portale OMS hello, andare troppo**impostazioni**.
2. Fare clic su **Dati**, quindi su **Log personalizzati**.
3. Per impostazione predefinita, tutte le modifiche di configurazione vengono automaticamente spostate tooall agenti.  Per gli agenti Linux, un file di configurazione viene inviato l'agente di raccolta dati Fluentd toohello.  Se si desidera toomodify questo file manualmente in ogni agente Linux, quindi deselezionare la casella di hello *Apply below macchine Linux di configurazione toomy*.
4. Fare clic su **Aggiungi +** tooopen hello guidata Log personalizzato.

### <a name="step-2-upload-and-parse-a-sample-log"></a>Passaggio 2. Caricare e analizzare un log di esempio
È innanzitutto necessario caricare un esempio di log personalizzato hello.  Hello verrà analizzare e visualizzare le voci di hello in questo file per si toovalidate.  Log Analitica utilizzerà il delimitatore di hello specificare tooidentify ogni record.

**Nuova riga** è il delimitatore predefinito hello e viene utilizzata per i file di log che hanno una singola voce per ogni riga.  Se la riga hello inizia con una data e ora in uno dei formati disponibili hello, quindi è possibile specificare un **Timestamp** delimitatore che supporta le voci che si estendono su più righe.

Se viene utilizzato un delimitatore di timestamp, proprietà TimeGenerated hello di ogni record archiviati in OMS verrà popolato con hello data/ora specificato per tale voce nel file di log hello.  Se viene utilizzato un delimitatore di nuova riga, TimeGenerated viene popolato con data e ora che Analitica Log raccolti voce hello.

> [!NOTE]
> Log Analitica considera attualmente hello data/ora raccolto da un file registro utilizzando un delimitatore di timestamp come UTC.  Non appena sarà modificato toouse hello fuso orario su agente hello.
>
>

1. Fare clic su **Sfoglia** e individuare il file di esempio tooa.  In alcuni browser, questo pulsante potrebbe essere denominato **Scegli file** .
2. Fare clic su **Avanti**.
3. Creazione guidata Registro personalizzata Hello caricherà hello file ed elenco hello record che identifica.
4. Modificare il delimitatore hello è tooidentify utilizzato un nuovo record e delimitatore selezionare hello che identifica meglio record hello nel file di log.
5. Fare clic su **Avanti**.

### <a name="step-3-add-log-collection-paths"></a>Passaggio 3. Aggiungere percorsi di raccolta di log
È necessario definire uno o più percorsi nell'agente hello in cui si possono individuare i log personalizzati hello.  È possibile fornire un percorso specifico e un nome per il file di log hello oppure è possibile specificare un percorso con un carattere jolly per nome hello.  Questa opzione è utile per le applicazioni che creano un nuovo file ogni giorno o quando un file raggiunge una determinata dimensione.  È anche possibile fornire più percorsi per un singolo file di log.

Ad esempio, un'applicazione potrebbe creare un file di log ogni giorno con data hello inclusa nel nome hello come log20100316.txt. Potrebbe essere un modello per questo tipo di un log *log\*. txt* che verrebbe applicata tooany file di log dopo l'applicazione hello di schema di denominazione.

Hello nella tabella seguente vengono forniti esempi di modelli validi toospecify diversi file di log.

| Descrizione | Path |
|:--- |:--- |
| Tutti i file in *C:\Logs* con estensione txt nell'agente Windows |C:\Logs\\\*.txt |
| Tutti i file in *C:\Logs* il cui nome inizia con log e aventi un'estensione txt nell'agente Windows |C:\Logs\log\*.txt |
| Tutti i file in */var/log/audit* con estensione txt nell'agente di Linux |/var/log/audit/*.txt |
| Tutti i file in */var/log/audit* con un nome che inizia con log e con l'estensione .txt nell'agente di Linux |/var/log/audit/log\*.txt |

1. Selezionare toospecify Windows o Linux, il formato di percorso si sta aggiungendo.
2. Digitare il percorso di hello e fare clic su hello  **+**  pulsante.
3. Ripetere il processo di hello per tutti i percorsi aggiuntivi.

### <a name="step-4-provide-a-name-and-description-for-hello-log"></a>Passaggio 4. Specificare un nome e una descrizione per il log di hello
Hello nome specificato dall'utente da utilizzare per il tipo di log hello come descritto in precedenza.  Sempre terminerà con _CL toodistinguish, come un log personalizzato.

1. Digitare un nome per il log di hello.  Hello  **\_CL** suffisso viene fornito automaticamente.
2. Aggiungere una **Descrizione**facoltativa.
3. Fare clic su **Avanti** definizione di toosave hello log personalizzato.

### <a name="step-5-validate-that-hello-custom-logs-are-being-collected"></a>Passaggio 5. Convalida che vengono raccolti i log personalizzati hello
Potrebbe richiedere fino a ora tooan per i dati iniziali hello un tooappear nuovo log personalizzato nel Log Analitica.  Verrà avviata la raccolta di voci da hello i log disponibili nel percorso hello specificato dal punto di hello che è definito hello log personalizzato.  Non manterrà le voci di hello caricato durante la creazione di log personalizzato hello, ma verranno raccolte le voci già esistenti nei file di log hello che viene individuato.

Log Analitica inizia a raccogliere dati dal log personalizzato hello, i relativi record sarà disponibili con una ricerca di Log.  Utilizza il nome di hello assegnato log personalizzato di hello come hello **tipo** nella query.

> [!NOTE]
> Se non è presente ricerca hello hello RawData proprietà, è possibile necessario tooclose e riaprire il browser.
>
>

### <a name="step-6-parse-hello-custom-log-entries"></a>Passaggio 6. Analizzare le voci di log personalizzato hello
voce del registro intera Hello verrà archiviati in una singola proprietà denominata **RawData**.  È probabile che si desideri tooseparate hello dei diversi componenti di informazioni in ogni voce in singole proprietà archiviata nel record di hello.  Eseguire questa operazione utilizzando hello [campi personalizzati](log-analytics-custom-fields.md) funzionalità di Log Analitica.

I passaggi dettagliati per l'analisi di voce di log personalizzata hello non sono forniti di seguito.  Consultare toohello [campi personalizzati](log-analytics-custom-fields.md) documentazione relativa a queste informazioni.

## <a name="disabling-a-custom-log"></a>Disabilitazione di un log personalizzato
Dopo la creazione, la definizione del log personalizzato non può essere rimossa, ma può essere disabilitata rimuovendo tutti i relativi percorsi di raccolta.

1. Nel portale OMS hello, andare troppo**impostazioni**.
2. Fare clic su **Dati**, quindi su **Log personalizzati**.
3. Fare clic su **dettagli** Avanti toohello log personalizzato definizione toodisable.
4. Eliminare i percorsi di hello insieme per la definizione di log personalizzato hello.

## <a name="data-collection"></a>Raccolta dei dati
Log Analytics raccoglie nuove voci da ogni log personalizzato a intervalli di circa 5 minuti.  agente Hello registrerà al suo posto in ogni file di log raccolti da.  Se l'agente di hello passa alla modalità offline per un periodo di tempo, quindi Log Analitica raccoglierà voci dall'ultima libero, anche se sono stati creati i movimenti mentre hello agent era offline.

Hello scritto intero contenuto della voce di log hello è tooa singola proprietà denominata **RawData**.  È possibile analizzare questa in più proprietà che possono essere analizzate e ricerca separatamente definendo [campi personalizzati](log-analytics-custom-fields.md) dopo la creazione di log personalizzato hello.

## <a name="custom-log-record-properties"></a>Proprietà dei record del log personalizzato
I record di log personalizzato dispone di un tipo con il nome di registro hello che viene fornita e hello proprietà hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| TimeGenerated |Data e ora di hello record sono stati raccolti da Log Analitica.  Se il log di hello utilizza un delimitatore di limiti di tempo viene ora hello raccolto dalla voce hello. |
| SourceSystem |Tipo di agente hello record sono stati raccolti da. <br> OpsManager: agente Windows, con connessione diretta o System Center Operations Manager <br> Linux – Tutti gli agenti Linux |
| RawData |Full-text di hello raccolti voce. |
| ManagementGroupName |Nome del gruppo di gestione di hello per gli agenti di gestione di System Center Operations.  Per gli altri agenti, corrisponde ad AOI-\<ID area di lavoro\> |

## <a name="log-searches-with-custom-log-records"></a>Ricerche nei log con i record del log personalizzato
Record di log personalizzati vengono archiviati nel repository OMS hello come record di qualsiasi altra origine dati.  È necessario un tipo corrispondente nome hello fornito quando si definisce il log di hello, pertanto è possibile utilizzare la proprietà di tipo hello nei record tooretrieve ricerca raccolti da un log specifico.

Hello nella tabella seguente vengono forniti esempi di ricerche nei log che recuperano i record di log personalizzati.

| Query | Descrizione |
|:--- |:--- |
| Type=MyApp_CL |Tutti gli eventi da un log personalizzato denominato MyApp_CL. |
| Type=MyApp_CL Severity_CF=error |Tutti gli eventi di un log personalizzato denominato MyApp_CL con un valore di *error* in un campo personalizzato denominato *Severity_CF*. |

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.

> | Query | Descrizione |
|:--- |:--- |
| MyApp_CL |Tutti gli eventi da un log personalizzato denominato MyApp_CL. |
| MyApp_CL &#124; where Severity_CF=="error" |Tutti gli eventi di un log personalizzato denominato MyApp_CL con un valore di *error* in un campo personalizzato denominato *Severity_CF*. |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a>Procedura dettagliata di esempio per l'aggiunta di un log personalizzato
Hello nella sezione seguente viene illustrato un esempio di creazione di un log personalizzato.  log di esempio Hello raccolti dispone di una singola voce per ogni riga a partire da una data e ora e quindi delimitato da virgole di campi per codice di stato e il messaggio.  Di seguito sono visualizzate alcune voci di esempio.

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect toodatabase
    2016-03-10 01:31:34 303,Error,Application lost connection toodatabase

### <a name="upload-and-parse-a-sample-log"></a>Caricare e analizzare un log di esempio
È fornire uno dei file di log hello e possono visualizzare gli eventi di hello che vogliono raccogliere.  In questo caso Nuova riga è un delimitatore sufficiente.  Se una singola voce nel log di hello potrebbe estendersi su più righe tuttavia, un delimitatore di timestamp necessario toobe utilizzato.

![Caricare e analizzare un log di esempio](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a>Aggiungere percorsi di raccolta di log
i file di log Hello saranno posizionati *C:\MyApp\Logs*.  Verrà creato un nuovo file ogni giorno con un nome che include data hello nel modello hello *appYYYYMMDD.log*.  Un modello sufficiente per questo registro è *C:\MyApp\Logs\\\*.log*.

![Percorso di raccolta di log](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-hello-log"></a>Specificare un nome e una descrizione per il log di hello
Viene usato il nome *MyApp_CL* e viene digitata una **descrizione**.

![Nome del log](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-hello-custom-logs-are-being-collected"></a>Convalida che vengono raccolti i log personalizzati hello
Viene utilizzata una query di *tipo = MyApp_CL* tooreturn tutti i record dal log raccolti hello.

![Query di log senza campi personalizzati](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-hello-custom-log-entries"></a>Analizzare le voci di log personalizzato hello
Utilizziamo hello toodefine campi personalizzati *EventTime*, *codice*, *stato*, e *messaggio* campi e si noterà differenza hello hello record restituiti dalla query hello.

![Query di log con campi personalizzati](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare [campi personalizzati](log-analytics-custom-fields.md) voci hello tooparse nel registro eventi personalizzato hello in tooindividual campi.
* Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni.
