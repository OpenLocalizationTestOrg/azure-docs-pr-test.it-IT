---
title: Raccogliere log personalizzati in Log Analytics di OMS | Documentazione Microsoft
description: "Log Analytics può raccogliere gli eventi dai file di testo nei computer Windows e Linux.  Questo articolo descrive come definire un nuovo log personalizzato e i dettagli dei record creati nel repository OMS."
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
ms.openlocfilehash: b7f28868e3ffdf95dbe39872f382e7c97eae692c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="custom-logs-in-log-analytics"></a>Log personalizzati in Log Analytics
L'origine dati dei log personalizzati in Log Analytics consente di raccogliere gli eventi dai file di testo nei computer Windows e Linux. Molte applicazioni registrano le informazioni nei file di testo invece di usare servizi di registrazione standard come il registro eventi di Windows o Syslog.  Al termine della raccolta, è possibile analizzare ogni record del log in singoli campi usando la funzionalità [Campi personalizzati](log-analytics-custom-fields.md) di Log Analytics.

![Raccolta di log personalizzati](media/log-analytics-data-sources-custom-logs/overview.png)

I file di log da raccogliere devono soddisfare i criteri seguenti.

- Il log deve avere una sola voce per ogni riga o usare un timestamp che corrisponde a uno dei formati seguenti all'inizio di ogni voce.

    AAAA-MM-GG HH:MM:SS <br>M/G/AAAA HH:MM:SS AM/PM <br>Lun GG,AAAA HH:MM:SS

- Il file di log non deve consentire aggiornamenti circolari in cui il file viene sovrascritto con le nuove voci.
- Il file di log deve usare la codifica ASCII o UTF-8.  Non sono supportati altri formati, ad esempio UTF-16.

>[!NOTE]
>Se sono presenti voci duplicate nel file di log, Log Analytics le raccoglierà.  Tuttavia, i risultati della ricerca non saranno coerenti se i risultati del filtro mostrano più eventi rispetto al numero di risultati.  È importante convalidare il log per determinare se l'applicazione che lo crea è la causa di questo comportamento e indirizzarlo se possibile prima di creare la definizione della raccolta dei log personalizzati.  
>
  
## <a name="defining-a-custom-log"></a>Definizione di un log personalizzato
Usare la procedura seguente per definire un file di log personalizzato.  Scorrere fino alla fine dell'articolo per la procedura dettagliata di un esempio che spiega come aggiungere un log personalizzato.

### <a name="step-1-open-the-custom-log-wizard"></a>Passaggio 1. Aprire la procedura guidata per i log personalizzati
La procedura guidata per i personalizzati viene eseguita nel portale di OMS e consente di definire un nuovo log personalizzato da raccogliere.

1. Nel portale di OMS passare a **Impostazioni**.
2. Fare clic su **Dati**, quindi su **Log personalizzati**.
3. Per impostazione predefinita, viene eseguito automaticamente il push di tutte le modifiche di configurazione in tutti gli agenti.  Per gli agenti Linux, viene inviato un file di configurazione all'agente di raccolta dati Fluentd.  Per modificare questo file manualmente in ogni agente Linux, deselezionare la casella *Applica la configurazione seguente alle macchine virtuali Linux*.
4. Fare clic su **Aggiungi+** per aprire la procedura guidata per i log personalizzati.

### <a name="step-2-upload-and-parse-a-sample-log"></a>Passaggio 2. Caricare e analizzare un log di esempio
Per iniziare, caricare un esempio del log personalizzato.  La procedura guidata analizza e visualizza le voci nel file da convalidare.  Log Analytics usa il delimitatore specificato per identificare tutti i record.

**Nuova riga** è il delimitatore predefinito e viene usato per i file di log con una sola voce per riga.  Se la riga inizia con una data e ora in uno dei formati disponibili, è possibile specificare un delimitatore **Timestamp** che supporta le voci che si estendono su più righe.

Se viene usato un delimitatore Timestamp, la proprietà TimeGenerated di ogni record archiviato in OMS viene popolata con la data/ora specificata per la voce nel file di log.  Se viene usato un delimitatore Nuova riga, TimeGenerated viene popolato con la data e l'ora in cui Log Analytics ha raccolto la voce.

> [!NOTE]
> Al momento, Log Analytics gestisce la data/ora raccolta da un log usando un delimitatore Timestamp come UTC.  Questa impostazione verrà modificata a breve in modo che venga usato il fuso orario dell'agente.
>
>

1. Fare clic su **Sfoglia** e passare a un file di esempio.  In alcuni browser, questo pulsante potrebbe essere denominato **Scegli file** .
2. Fare clic su **Avanti**.
3. La procedura guidata per i log personalizzati carica il file ed elenca i record identificati.
4. Modificare il delimitatore usato per identificare un nuovo record e selezionare il delimitatore che identifica meglio i record nel file di log.
5. Fare clic su **Avanti**.

### <a name="step-3-add-log-collection-paths"></a>Passaggio 3. Aggiungere percorsi di raccolta di log
È necessario definire uno o più percorsi nell'agente in cui è possibile individuare il log personalizzato.  È possibile fornire un percorso specifico e un nome per il file di log oppure specificare un percorso con un carattere jolly per il nome.  Questa opzione è utile per le applicazioni che creano un nuovo file ogni giorno o quando un file raggiunge una determinata dimensione.  È anche possibile fornire più percorsi per un singolo file di log.

Ad esempio, un'applicazione potrebbe creare un file di log ogni giorno con la data inclusa nel nome, come in log20100316.txt. Un modello per questo log potrebbe essere *log\*.txt*, applicabile a qualsiasi file di log in base allo schema di denominazione dell'applicazione.

La tabella seguente fornisce esempi di percorsi validi per specificare file di log diversi.

| Descrizione | Path |
|:--- |:--- |
| Tutti i file in *C:\Logs* con estensione txt nell'agente Windows |C:\Logs\\\*.txt |
| Tutti i file in *C:\Logs* il cui nome inizia con log e aventi un'estensione txt nell'agente Windows |C:\Logs\log\*.txt |
| Tutti i file in */var/log/audit* con estensione txt nell'agente di Linux |/var/log/audit/*.txt |
| Tutti i file in */var/log/audit* con un nome che inizia con log e con l'estensione .txt nell'agente di Linux |/var/log/audit/log\*.txt |

1. Selezionare Windows o Linux per specificare il formato del percorso che verrà aggiunto.
2. Digitare il percorso e fare clic sul pulsante **+** .
3. Ripetere il processo per i percorsi aggiuntivi.

### <a name="step-4-provide-a-name-and-description-for-the-log"></a>Passaggio 4. Specificare un nome e una descrizione per il log
Il nome specificato viene usato per il tipo di log come descritto in precedenza.  Termina sempre con _CL per definirlo come log personalizzato.

1. Digitare un nome per il log.  Il suffisso **\_CL** viene applicato automaticamente.
2. Aggiungere una **Descrizione**facoltativa.
3. Fare clic su **Avanti** per salvare la definizione del log personalizzato.

### <a name="step-5-validate-that-the-custom-logs-are-being-collected"></a>Passaggio 5. Verificare che i log personalizzati vengano raccolti
La visualizzazione dei dati iniziali di un nuovo log personalizzato in Log Analytics potrebbe richiedere fino a un'ora.  La procedura inizia con la raccolta delle voci dai log trovati nel percorso specificato dal punto in cui è stato definito il log personalizzato.  Le voci caricate durante la creazione del log personalizzato non vengono mantenute, ma vengono raccolte le voci già esistenti nei file di log individuati.

Dopo che Log Analytics avvia la raccolta dal log personalizzato, i record vengono resi disponibili con lo strumento di ricerca nei log.  Usare il nome assegnato al log personalizzato come **Tipo** nella query.

> [!NOTE]
> Se la proprietà RawData non è presente nella ricerca, potrebbe essere necessario chiudere e riaprire il browser.
>
>

### <a name="step-6-parse-the-custom-log-entries"></a>Passaggio 6. Analizzare le voci del log personalizzato
L'intera voce di log viene archiviata in una singola proprietà denominata **RawData**.  È probabile che si preferisca separare le diverse parti di informazioni di ogni voce in singole proprietà archiviate nel record.  Per farlo, usare la funzionalità [Campi personalizzati](log-analytics-custom-fields.md) di Log Analytics.

La procedura dettagliata per l'analisi della voce del log personalizzato non viene fornita in questa sede.  Per queste informazioni, vedere la documentazione [Campi personalizzati](log-analytics-custom-fields.md) .

## <a name="disabling-a-custom-log"></a>Disabilitazione di un log personalizzato
Dopo la creazione, la definizione del log personalizzato non può essere rimossa, ma può essere disabilitata rimuovendo tutti i relativi percorsi di raccolta.

1. Nel portale di OMS passare a **Impostazioni**.
2. Fare clic su **Dati**, quindi su **Log personalizzati**.
3. Fare clic su **Dettagli** accanto alla definizione del log personalizzato per disabilitarla.
4. Rimuovere ogni percorso di raccolta della definizione del log personalizzato.

## <a name="data-collection"></a>Raccolta dei dati
Log Analytics raccoglie nuove voci da ogni log personalizzato a intervalli di circa 5 minuti.  L'agente registra la propria posizione in ogni file di log da cui esegue la raccolta.  Se l'agente risulta offline per un certo periodo di tempo, Log Analytics raccoglie le voci dal momento in cui è stato interrotto, anche se le voci sono state create mentre l'agente era offline.

L'intero contenuto della voce di log viene scritto in una singola proprietà denominata **RawData**.  È possibile suddividerla in più proprietà che possono essere analizzate e ricercate separatamente definendo [Campi personalizzati](log-analytics-custom-fields.md) dopo aver creato il log personalizzato.

## <a name="custom-log-record-properties"></a>Proprietà dei record del log personalizzato
Il tipo dei record del log personalizzato corrisponde al nome del log specificato e le proprietà sono indicate nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| TimeGenerated |Data e ora di raccolta del record con Log Analytics.  Se il log usa un delimitatore basato sul tempo, questa proprietà indica la data e l'ora raccolte dalla voce. |
| SourceSystem |Tipo di agente da cui è stato raccolto il record. <br> OpsManager: agente Windows, con connessione diretta o System Center Operations Manager <br> Linux – Tutti gli agenti Linux |
| RawData |Testo completo della voce raccolta. |
| ManagementGroupName |Nome del gruppo di gestione per gli agenti System Center Operations Manager.  Per gli altri agenti, corrisponde ad AOI-\<ID area di lavoro\> |

## <a name="log-searches-with-custom-log-records"></a>Ricerche nei log con i record del log personalizzato
I record dei log personalizzati vengono archiviati nel repository OMS esattamente come i record di qualsiasi altra origine dati.  Hanno un tipo corrispondente al nome fornito quando si definisce il log, quindi è possibile usare la proprietà Tipo nella ricerca per recuperare i record raccolti da un log specifico.

La tabella seguente mostra alcuni esempi di ricerche nei log che recuperano i record dai log personalizzati.

| Query | Descrizione |
|:--- |:--- |
| Type=MyApp_CL |Tutti gli eventi da un log personalizzato denominato MyApp_CL. |
| Type=MyApp_CL Severity_CF=error |Tutti gli eventi di un log personalizzato denominato MyApp_CL con un valore di *error* in un campo personalizzato denominato *Severity_CF*. |

>[!NOTE]
> Se l'area di lavoro è stata aggiornata al [nuovo linguaggio di query di Log Analytics](log-analytics-log-search-upgrade.md), le query precedenti verranno sostituite dalle seguenti.

> | Query | Descrizione |
|:--- |:--- |
| MyApp_CL |Tutti gli eventi da un log personalizzato denominato MyApp_CL. |
| MyApp_CL &#124; where Severity_CF=="error" |Tutti gli eventi di un log personalizzato denominato MyApp_CL con un valore di *error* in un campo personalizzato denominato *Severity_CF*. |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a>Procedura dettagliata di esempio per l'aggiunta di un log personalizzato
La sezione seguente descrive un esempio di creazione di un log personalizzato.  Il log di esempio raccolto ha una singola voce per ogni riga contenente una data e un'ora iniziali seguite da campi delimitati da virgole per il codice, lo stato e il messaggio.  Di seguito sono visualizzate alcune voci di esempio.

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect to database
    2016-03-10 01:31:34 303,Error,Application lost connection to database

### <a name="upload-and-parse-a-sample-log"></a>Caricare e analizzare un log di esempio
Viene fornito uno dei file di log per visualizzare gli eventi che saranno raccolti.  In questo caso Nuova riga è un delimitatore sufficiente.  Se una singola voce nel log può estendersi su più righe, è necessario usare un delimitatore Timestamp.

![Caricare e analizzare un log di esempio](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a>Aggiungere percorsi di raccolta di log
I file di log si trovano in *C:\MyApp\Logs*.  Ogni giorno viene creato un nuovo file con un nome che include la data nel modello *appYYYYMMDD.log*.  Un modello sufficiente per questo registro è *C:\MyApp\Logs\\\*.log*.

![Percorso di raccolta di log](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-the-log"></a>Specificare un nome e una descrizione per il log
Viene usato il nome *MyApp_CL* e viene digitata una **descrizione**.

![Nome del log](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-the-custom-logs-are-being-collected"></a>Verificare che i log personalizzati vengano raccolti
Viene usata una query *Type=MyApp_CL* per restituire tutti i record dal log raccolto.

![Query di log senza campi personalizzati](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-the-custom-log-entries"></a>Analizzare le voci del log personalizzato
Viene usato Campi personalizzati per definire i campi *EventTime*, *Code*, *Status* e *Message* ed è possibile osservare la differenza nei record restituiti dalla query.

![Query di log con campi personalizzati](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a>Passaggi successivi
* Usare [Campi personalizzati](log-analytics-custom-fields.md) per analizzare le voci del log personalizzato nei singoli campi.
* Informazioni sulle [ricerche nei log](log-analytics-log-searches.md) per analizzare i dati raccolti dalle origini dati e dalle soluzioni.
