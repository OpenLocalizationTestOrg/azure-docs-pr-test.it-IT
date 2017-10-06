---
title: note sulla versione Analitica aaaStream | Documenti Microsoft
description: Note sulla versione di analisi di flusso
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e59f893-cd2c-43fb-9eca-c146ce637203
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/03/2017
ms.author: jeffstok
ms.openlocfilehash: 1426ebc260be19fbde60518b25501fe53d908d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-release-notes"></a>Note sulla versione di analisi di flusso

## <a name="notes-for-06142017-update-of-stream-analytics-tools-for-visual-studio"></a>Note per la versione 14/06/2017 di Strumenti di Analisi di flusso per Visual Studio
Questo aggiornamento è per gli Strumenti di Visual Studio. Questa versione include nuove funzionalità seguenti hello.

| Titolo | Descrizione |
| --- | --- |
| Supporto per l'editor dello script Java |È possibile utilizzare l'esperienza di editor di script hello java native dopo la creazione di funzioni di script java.|
| Visualizzare il messaggio di errore di runtime del processo | Se sono presenti errori di runtime durante l'esecuzione del processo, è possibile visualizzarli nella scheda errori hello modificando l'intervallo di tempo visualizzato hello. Per impostazione predefinita Mostra messaggi di errore hello per ultimi 30 minuti. |
| Supporto CSV e Avro per l'input di test locale | Oltre a JSON, ora è possibile usare il formato file CSV e Avro per l'input di test locale.|

## <a name="notes-for-05032017-update-of-stream-analytics"></a>Note sulla versione 03/05/2017 dell'aggiornamento di Analisi di flusso
Questo aggiornamento è relativo al rilascio della documentazione sulla risoluzione dei problemi.

Hello [risoluzione dei problemi guida](stream-analytics-troubleshooting-guide.md) e altri documenti sono stati rilasciati. Esaminare il contenuto. Commenti e suggerimenti sono apprezzati.

## <a name="notes-for-04242017-update-of-stream-analytics-tools-for-visual-studio"></a>Note per la versione 24/04/2017 di Strumenti di Analisi di flusso per Visual Studio
Questo aggiornamento è per gli Strumenti di Visual Studio. Questa versione include nuove funzionalità seguenti hello.

| Titolo | Descrizione |
| --- | --- |
| Visualizzare il risultato del test locale in Visual Studio | risultato dell'output di hello locale tooview hello test, premere INVIO nella finestra di console output di hello o chiuderlo. risultato Hello è visualizzato in una finestra in Visual Studio in formato tabella. |
| Risultato locale dell'output in formato JSON | Quando si esegue un test locale, verrà generato il risultato di output di hello come formati di file JSON e CSV. |
| Visualizzare dati di input/output di archiviazione della tabella/BLOB | Facendo doppio clic su un'archiviazione blob o tabella di input/output nella visualizzazione processi hello, è possibile visualizzare in Anteprima dati hello all'interno di Visual Studio in modo molto semplice. |
| Visualizzare messaggio di errore per input/output | Se sono presenti input o output di un processo correlato tooyou runtime e gli errori, verrà visualizzato nel diagramma di processo hello in cui è possibile passare il mouse su tale messaggio di errore dettagliato toosee hello.|


## <a name="notes-for-02012017-release-of-stream-analytics"></a>Note per la versione 01/02/2017 di Analisi di flusso
Questa versione contiene hello dopo l'aggiornamento.

| Titolo | Descrizione |
| --- | --- |
| Introduzione alle funzioni JavaScript definite dall'utente (UDF) |Le [funzioni Java definite dall'utente](stream-analytics-javascript-user-defined-functions.md) sono ora disponibili per una maggiore flessibilità nella creazione di query. |
| Introduzione agli strumenti per Visual Studio e analisi di flusso |Gli [strumenti per Visual Studio](stream-analytics-tools-for-visual-studio.md) sono ora disponibili per il debug e per le utility. |
| Abilitare la registrazione diagnostica |La [registrazione diagnostica](stream-analytics-job-diagnostic-logs.md) è ora disponibile per altre opzioni di risoluzione dei problemi. |
| Introduzione alle funzioni geospaziali |Le [funzioni geospaziali](http://msdn.microsoft.com/library/mt778980(Azure.100).aspx) sono ora disponibili a livello generale. |

## <a name="notes-for-04152016-release-of-stream-analytics"></a>Note per la versione 15/04/2016 di Analisi di flusso
Questa versione contiene hello dopo l'aggiornamento.

| Titolo | Descrizione |
| --- | --- |
| Disponibilità generale per gli output di Power BI |[Gli output di Power BI](stream-analytics-power-bi-dashboard.md) sono ora disponibili a livello generale. scadenza di autorizzazione Hello 90 giorni per Power BI è stato rimosso. Per altre informazioni sugli scenari in cui autorizzazione deve toobe rinnovato vedere hello [rinnovare l'autorizzazione](stream-analytics-power-bi-dashboard.md#renew-authorization) sezione di creazione di un dashboard di Power BI. |

## <a name="notes-for-03032016-release-of-stream-analytics"></a>Note per la versione 03/03/2016 di Analisi di flusso
Questa versione contiene hello dopo l'aggiornamento.

| Titolo | Descrizione |
| --- | --- |
| Nuovi elementi del linguaggio di query di Analisi di flusso |Ora SAQL ha [GetType](https://msdn.microsoft.com/library/azure/mt643890.aspx "Pagina MSDN su GetType"), [TRY_CAST](https://msdn.microsoft.com/library/azure/mt643735.aspx "Pagina MSDN su TRY_CAST") e [REGEXMATCH](https://msdn.microsoft.com/library/azure/mt643891.aspx "Pagina MSDN su REGEXMATCH"). |

## <a name="notes-for-12102015-release-of-stream-analytics"></a>Note per la versione 10/12/2015 di Analisi di flusso
Questa versione contiene hello dopo l'aggiornamento.

| Titolo | Descrizione |
| --- | --- |
| Aggiornamento della versione dell'API REST |versione dell'API REST Hello è stato aggiornato too2015-10-01. I dettagli sono disponibili su MSDN nella sezione di [riferimento dell'API REST di gestione di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn835031.aspx) e [Integrazione di Machine Learning in Analisi di flusso](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md). |
| Integrazione con Azure Machine Learning |Questa versione offre il supporto per le funzioni definite dall'utente di Azure Machine Learning. Vedere hello [esercitazione](stream-analytics-machine-learning-integration-tutorial.md) per ulteriori informazioni, nonché hello [annuncio sul blog generale](http://blogs.technet.com/b/machinelearning/archive/2015/12/10/apply-azure-ml-as-a-function-in-azure-stream-analytics.aspx). |

## <a name="notes-for-11122015-release-of-stream-analytics"></a>Note per la versione 12/11/2015 di Analisi di flusso
Questa versione contiene hello dopo l'aggiornamento.

| Titolo | Descrizione |
| --- | --- |
| Nuovo comportamento di SELECT |Selezionare in Analitica di flusso è stato esteso tooallow * come una funzione di accesso di un record annidato. Per altre informazioni, vedere [http://msdn.microsoft.com/library/mt622759.aspx](http://msdn.microsoft.com/library/mt622759.aspx "Tipi di dati complessi"). |

## <a name="notes-for-10222015-release-of-stream-analytics"></a>Note per la versione 22/10/2015 di Analisi di flusso
Questa versione contiene hello dopo gli aggiornamenti.

| Titolo | Descrizione |
| --- | --- |
| Funzionalità del linguaggio di query aggiuntive |Flusso Analitica ha espanso il linguaggio di query hello includendo hello seguenti caratteristiche: [ABS](https://msdn.microsoft.com/library/azure/mt574054.aspx), [CEILING](https://msdn.microsoft.com/library/azure/mt605286.aspx), [EXP](https://msdn.microsoft.com/library/azure/mt605289.aspx), [FLOOR](https://msdn.microsoft.com/library/azure/mt605240.aspx), [POWER](https://msdn.microsoft.com/library/azure/mt605287.aspx), [SIGN](https://msdn.microsoft.com/library/azure/mt605290.aspx), [quadrato](https://msdn.microsoft.com/library/azure/mt605288.aspx), e [SQRT](https://msdn.microsoft.com/library/azure/mt605238.aspx). |
| Rimuovere le limitazioni di aggregazione |Questa versione consente di rimuovere la limitazione di hello di 15 aggregazioni in una query. Non è disponibile alcun toohello limita il numero di aggregazioni per ogni query. |
| Nuova funzionalità GROUP BY di System.Timestamp |Hello [GROUP BY](https://msdn.microsoft.com/library/azure/dn835023.aspx) funzione consente ora per entrambi window_type o [timestamp](https://msdn.microsoft.com/library/azure/mt598501.aspx). |
| OFFSET aggiunto per le finestre a cascata e di salto. |Per impostazione predefinita, le finestre [a cascata](https://msdn.microsoft.com/library/azure/dn835055.aspx) e [di salto](https://msdn.microsoft.com/library/azure/dn835041.aspx) sono allineate rispetto al tempo zero (1/1/0001 12:00:00 AM UTC). il parametro (facoltativo) nuovo 'offsetsize' Hello consente di specificare un offset personalizzato (o allineamento). |

## <a name="notes-for-09292015-release-of-stream-analytics"></a>Note per la versione 29/09/2015 di Analisi di flusso
Questa versione contiene hello dopo gli aggiornamenti.

| Titolo | Descrizione |
| --- | --- |
| Anteprima pubblica di Azure IoT Suite |Flusso Analitica è incluso in anteprima pubblica di hello Azure IoT Suite hello. |
| Integrazione del portale di Azure |In presenza di toocontinued aggiunta nel portale di gestione di Azure hello, flusso Analitica è ora integrato in hello [portale Azure](https://azure.microsoft.com/overview/preview-portal/). Si noti che la funzionalità di flusso Analitica nel portale di anteprima hello è attualmente un sottoinsieme delle funzionalità di hello offerte nel portale di gestione di Azure hello senza supporto per il test delle query nel browser, che configurazione e la visualizzazione di creazione di nuovi tooor di output Power BI risorse di input e outpue nelle sottoscrizioni si ha accesso a. |
| Supporto per l'output Cosmos DB |I processi di flusso Analitica possono ora restituire troppo[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/). |
| Supporto per l'input dell'hub IoT |I processi di analisi di flusso sono ora in grado di acquisire dati dagli hub IoT. |
| TIMESTAMP BY per eventi eterogenei |Quando un unico flusso di dati contiene più tipi di evento con timestamp in campi diversi, è ora possibile usare [TIMESTAMP BY](http://msdn.microsoft.com/library/mt573293.aspx) con i campi di espressioni toospecify timestamp diverso per ogni case. |

## <a name="notes-for-09102015-release-of-stream-analytics"></a>Note per la versione 10/09/2015 di Analisi di flusso
Questa versione contiene hello dopo gli aggiornamenti.

| Titolo | Descrizione |
| --- | --- |
| Supporto per i gruppi PowerBI |condivisione di dati con altri utenti di Power BI, Analitica flusso processi ora è possono scrivere troppo tooenable[gruppi di Power BI](stream-analytics-define-outputs.md#power-bi) all'interno dell'account di Power BI. |

## <a name="notes-for-08202015-release-of-stream-analytics"></a>Note per la versione 20/08/2015 di Analisi di flusso
Questa versione contiene hello dopo gli aggiornamenti.

| Titolo | Descrizione |
| --- | --- |
| Aggiunta funzione LAST |Hello [ultimo](http://msdn.microsoft.com/library/mt421186.aspx) funzione è ora disponibile nei processi di flusso Analitica, consentendo tooretrieve hello dell'evento più recente in un flusso di eventi all'interno di un intervallo di tempo specificato. |
| Nuove funzioni di matrice |Ora sono disponibili le funzioni di matrice [GetArrayElement](http://msdn.microsoft.com/library/mt270218.aspx), [GetArrayElements](http://msdn.microsoft.com/library/mt298451.aspx) e [GetArrayLength](http://msdn.microsoft.com/library/mt270226.aspx). |
| Nuove funzioni di record |Le funzioni di record [GetRecordProperties](http://msdn.microsoft.com/library/mt270221.aspx) e [GetRecordPropertyValue](http://msdn.microsoft.com/library/mt270220.aspx) sono ora disponibili. |

## <a name="notes-for-07302015-release-of-stream-analytics"></a>Note per la versione del 30/07/2015 di Analisi di flusso
Questa versione contiene hello dopo gli aggiornamenti.

| Titolo | Descrizione |
| --- | --- |
| ID organizzazione di Power BI separato dall'ID di Azure |Questa funzionalità abilita l' [output di Power BI](stream-analytics-power-bi-dashboard.md) per i processi ASA in qualsiasi tipo di account di Azure (Live ID o ID organizzazione). Inoltre, è possibile disporre di un ID organizzazione per l'account Azure e utilizzarne uno diverso per l'autorizzazione dell'output di Power BI. |
| Supporto per l'output di code del bus di servizio |Gli output di [code del bus di servizio](stream-analytics-define-outputs.md#service-bus-queues) sono ora disponibili nei processi di Analisi di flusso. |
| Supporto per l'output di argomenti del bus di servizio |Gli output di [argomenti del bus di servizio](stream-analytics-define-outputs.md#service-bus-topics) sono ora disponibili nei processi di Analisi di flusso. |

## <a name="notes-for-07092015-release-of-stream-analytics"></a>Note per la versione 09/07/2015 di Analisi di flusso
Questa versione contiene hello dopo gli aggiornamenti.

| Titolo | Descrizione |
| --- | --- |
| Partizionamento output BLOB personalizzato |Output di archiviazione BLOB ne consentono una frequenza di hello toospecify opzione di output BLOB vengono scritti e struttura di data percorso cartella di output di hello struttura e il formato di hello. |

## <a name="notes-for-05032015-release-of-stream-analytics"></a>Note per la versione 03/05/2015 di Analisi di flusso
Questa versione contiene hello dopo gli aggiornamenti.

| Titolo | Descrizione |
| --- | --- |
| Aumento del valore massimo per Finestra di tolleranza elementi non in ordine |dimensione massima di Hello per la finestra di tolleranza ordine hello è ora 59:59 (mm: ss) |
| Formato di output JSON: Separato da righe o matrice |Ora è disponibile un'opzione per l'output tooBlob archiviazione o Hub eventi toooutput come una matrice di oggetti JSON o separando oggetti JSON con una nuova riga. |

## <a name="notes-for-04162015-release-of-stream-analytics"></a>Note per la versione 16/04/2015 di Analisi di flusso
| Titolo | Descrizione |
| --- | --- |
| Ritardo nella configurazione dell'account di archiviazione di Azure |Quando si crea un processo di flusso Analitica in un'area per hello prima volta, si toocreate richiesto un nuovo account di archiviazione o specificare un account esistente per il monitoraggio dei processi di flusso Analitica in tale area. Scadenza toolatency nella configurazione del monitoraggio, la creazione di un altro processo di flusso Analitica nella stessa area entro 30 minuti richiederà hello specifica di un secondo account di archiviazione anziché mostrare hello hello configurata di recente in archiviazione di monitoraggio hello Elenco a discesa dell'account. tooavoid la creazione di un account di archiviazione non necessario, attendere 30 minuti dopo la creazione di un processo in un'area per hello prima volta prima del provisioning di processi aggiuntivi in tale area. |
| Aggiornamento dei processi |In questo momento, Analitica flusso non supporta le modifiche in tempo reale toohello definizione o la configurazione di un processo in esecuzione. In ordine toochange hello input, output, query, la scala o configurazione di un processo in esecuzione, è necessario prima interrompere il processo di hello. |
| Tipi di dati dedotti da origine di input |Se non viene utilizzata un'istruzione CREATE TABLE, tipo di input hello è derivato dal formato di input, ad esempio tutti i campi da file CSV sono costituiti da stringa. Campi necessità toobe convertito in modo esplicito toohello tipo corretto utilizzo di funzione CAST hello in errori di mancata corrispondenza di tipo tooavoid ordine. |
| I campi mancanti sono generati come valori null |Riferimento a un campo che non è presente nell'origine di input hello determinerà i valori null nell'evento di output di hello. |
| Le istruzioni WITH devono precedere le istruzioni SELECT |Nella query, le istruzioni SELECT devono seguire le sottoquery definite nelle istruzioni WITH. |
| Problema relativo a memoria insufficiente |Riavviare i processi di streaming Analitica con una tolleranza di grandi dimensioni per gli eventi in ordine e/o di gestione di che una grande quantità di stato potrebbe essere toorun processo hello dalla memoria, risultante in un processo di query complesse. Hello start e stop operazioni saranno visibili nei log di operazione del processo di hello. tooavoid questo comportamento, query hello scala out tra più partizioni. In una versione futura questa limitazione verrà risolta riducendo le prestazioni dei processi interessati anziché causandone il riavvio. |
| Input blob di grandi dimensioni senza timestamp payload possono causare problemi relativi a memoria insufficiente |Utilizzo di file dall'archiviazione Blob di grandi dimensioni può causare toocrash i processi di flusso Analitica se un campo di data e ora non viene specificato tramite TIMESTAMP BY. tooavoid questo problema, mantenere ogni blob inferiori a 10MB di dimensioni. |
| Limitazione del volume di eventi del database SQL |Quando si utilizza il Database SQL come una destinazione di output, volumi molto elevati di dati di output potrebbe essere hello Analitica flusso processo tootime out. Questo problema, ovvero tooresolve aggregazioni o operatori di filtro per ridurre il volume di output di hello oppure scegliere invece archiviazione Blob di Azure o hub eventi come una destinazione di output. |
| I dataset PowerBI possono contenere solo una tabella |PowerBI non supporta più di una tabella in un dato dataset. |

## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
