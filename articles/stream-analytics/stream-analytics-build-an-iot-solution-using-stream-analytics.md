---
title: una soluzione IoT tramite flusso Analitica aaaBuild | Documenti Microsoft
description: Guida introduttiva di esercitazione per hello soluzione IoT Analitica di flusso di uno scenario casello
keywords: soluzione IOT, funzioni finestra
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a>Compilare una soluzione IoT con Analisi di flusso
## <a name="introduction"></a>Introduzione
In questa esercitazione si apprenderà come informazioni in tempo reale toouse Azure flusso Analitica tooget dai dati. Gli sviluppatori possono combinare facilmente flussi di dati, ad esempio fare clic su flussi, registri e gli eventi generati dal dispositivo, con record cronologici o ottenere informazioni aziendali accurate tooderive dati di riferimento. Come un servizio di calcolo di flusso in tempo reale completamente gestito che è ospitato in Microsoft Azure, Azure flusso Analitica fornisce resilienza predefinita, bassa latenza e la scalabilità tooget operativi in pochi minuti.

Dopo aver completato questa esercitazione, si sarà in grado di:

* Acquisire familiarità con il portale di Azure flusso Analitica hello.
* Configurare e distribuire un processo di flusso.
* Esprimere i reali problemi e risolverli utilizzando il linguaggio di query di hello Analitica di flusso.
* Sviluppare in tutta sicurezza soluzioni di streaming per i clienti usando Analisi di flusso.
* Utilizzare hello monitoraggio e registrazione esperienza tootroubleshoot problemi.

## <a name="prerequisites"></a>Prerequisiti
Si sarà necessario hello seguenti prerequisiti toocomplete questa esercitazione:

* versione più recente di Hello di [Azure PowerShell](/powershell/azure/overview)
* Visual Studio 2017, 2015, o libera hello [Community di Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)
* Una [sottoscrizione di Azure](https://azure.microsoft.com/pricing/free-trial/)
* Privilegi amministrativi nel computer di hello
* Il download di [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) da Microsoft Download Center hello
* Facoltativo: Codice sorgente per generazione di eventi TollApp hello in [GitHub](https://aka.ms/azure-stream-analytics-toll-source)

## <a name="scenario-introduction-hello-toll"></a>Presentazione dello scenario: il casello
Un casello rappresenta una situazione piuttosto comune. Si verificano tali in molte autostrade, ponti e tunnel tra HelloWorld. Ogni barriera è costituita da più caselli. In stand manuale, non è arrestare toopay hello casello tooan supervisore. In stand automatizzati, un sensore all'inizio di ogni tipo analizza una scheda RFID che viene apposta toohello parabrezza del veicolo di quello passato casello hello. È facile toovisualize passaggio di hello dei veicoli attraverso il casello come un flusso di eventi su cui è possibile eseguire operazioni interessanti.

![Immagine di automobili ai caselli](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a>Dati di ingresso
Questa esercitazione utilizza due flussi di dati. Sensori installato in entrata hello e uscita di casello hello produrre primo flusso hello. secondo flusso Hello è un set di dati statici della ricerca con i dati di registrazione veicolo.

### <a name="entry-data-stream"></a>Flusso di dati di ingresso
flusso di dati di Hello voce contiene informazioni su automobili in arrivo casello.

| ID casello | Tempo ingresso | Targa | Stato | Casa automobilistica | Modello | Tipo veicolo | Peso veicolo | Casello | Tag |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 |2014-09-10 12:01:00.000 |JNB 7001 |NY |Honda |CRV |1 |0 |7 | |
| 1 |2014-09-10 12:02:00.000 |YXZ 1001 |NY |Toyota |Camry |1 |0 |4 |123456789 |
| 3 |2014-09-10 12:02:00.000 |ABC 1004 |CT |Ford |Taurus |1 |0 |5 |456789123 |
| 2 |2014-09-10 12:03:00.000 |XYZ 1003 |CT |Toyota |Corolla |1 |0 |4 | |
| 1 |2014-09-10 12:03:00.000 |BNJ 1007 |NY |Honda |CRV |1 |0 |5 |789123456 |
| 2 |2014-09-10 12:05:00.000 |CDE 1007 |NJ |Toyota |4x4 |1 |0 |6 |321987654 |

Di seguito è riportata una breve descrizione delle colonne di hello:

| Colonna | Descrizione |
| --- | --- |
| ID casello |Hello casello stand ID che identifica in modo univoco un casello |
| Tempo ingresso |Hello data e ora della voce di hello veicolo toohello casello in formato UTC |
| Targa |numero di targa Hello del veicolo hello |
| Stato |Stato degli Stati Uniti |
| Casa automobilistica |produttore Hello dell'automobile hello |
| Modello |numero di automobili hello modello Hello |
| Tipo veicolo |1 per autovetture o 2 per veicoli commerciali |
| Peso veicolo |Peso del veicolo in tonnellate, 0 per veicoli passeggeri |
| Casello |valore casello Hello in dollari USA |
| Tag |Hello e-Tag su automobile hello che automatizza il pagamento; spazio vuoto in cui il pagamento hello è stato eseguito manualmente |

### <a name="exit-data-stream"></a>Flusso di dati di uscita
flusso di dati di uscita Hello contiene informazioni su automobili lasciando casello hello.

| **ID casello** | **Tempo ingresso** | **Targa** |
| --- | --- | --- |
| 1 |2014-09-10T12:03:00.0000000Z |JNB 7001 |
| 1 |2014-09-10T12:03:00.0000000Z |YXZ 1001 |
| 3 |2014-09-10T12:04:00.0000000Z |ABC 1004 |
| 2 |2014-09-10T12:07:00.0000000Z |XYZ 1003 |
| 1 |2014-09-10T12:08:00.0000000Z |BNJ 1007 |
| 2 |2014-09-10T12:07:00.0000000Z |CDE 1007 |

Di seguito è riportata una breve descrizione delle colonne di hello:

| Colonna | Descrizione |
| --- | --- |
| ID casello |Hello casello stand ID che identifica in modo univoco un casello |
| Tempo ingresso |Hello data e ora di uscita del veicolo hello da casello in formato UTC |
| Targa |numero di targa Hello del veicolo hello |

### <a name="commercial-vehicle-registration-data"></a>Dati di registrazione di veicoli commerciali
esercitazione Hello utilizza uno snapshot statico di un database di registrazione del veicolo commerciale.

| Targa | ID registrazione | Scaduto |
| --- | --- | --- |
| SVT 6023 |285429838 |1 |
| XLZ 3463 |362715656 |0 |
| BAC 1005 |876133137 |1 |
| RIV 8632 |992711956 |0 |
| SNY 7188 |592133890 |0 |
| ELH 9896 |678427724 |1 |

Di seguito è riportata una breve descrizione delle colonne di hello:

| Colonna | Descrizione |
| --- | --- |
| Targa |numero di targa Hello del veicolo hello |
| ID registrazione |ID di registrazione del veicolo Hello |
| Scaduto |lo stato della registrazione del veicolo hello Hello: 0 se la registrazione di veicolo è attiva, 1 se la registrazione è scaduta |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a>Configurare l'ambiente hello per Analitica di flusso di Azure
toocomplete questa esercitazione, è necessaria una sottoscrizione di Microsoft Azure. Microsoft offre la possibilità di scegliere una versione di valutazione gratuita per i servizi Microsoft Azure.

Se non si ha un account Azure, è possibile [richiedere una versione di valutazione gratuita](http://azure.microsoft.com/pricing/free-trial/).

> [!NOTE]
> toosign iscrizione a una versione di valutazione gratuita, è necessario un dispositivo mobile in grado di ricevere messaggi di testo e una carta di credito valida.
> 
> 

Assicurarsi di hello toofollow i passaggi nella sezione "Pulire l'account di Azure" hello alla fine di hello di questo articolo in modo che è possibile usare hello meglio il credito Azure.

## <a name="provision-azure-resources-required-for-hello-tutorial"></a>Eseguire il provisioning di risorse di Azure necessari per hello esercitazione
Questa esercitazione richiede due eventi hub tooreceive *voce* e *uscire* flussi di dati. Database SQL di Azure genera risultati hello dei processi di flusso Analitica hello. In Archiviazione di Azure vengono memorizzati i dati di riferimento di registrazione dei veicoli.

È possibile utilizzare hello Setup.ps1 script nella cartella TollApp hello in GitHub toocreate tutte le risorse necessarie. Interesse hello di tempo, è consigliabile che viene eseguito. Se si desidera toolearn ulteriori informazioni sulla modalità tooconfigure alle risorse nel portale di Azure hello fare riferimento toohello appendice di "Configurazione delle risorse di esercitazione nel portale di Azure".

Scaricare e salvare hello supporto [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) cartella e file.

Aprire una finestra di **Microsoft Azure PowerShell***come amministratore*. Se non si dispone ancora di Azure PowerShell, seguire le istruzioni hello [installare e configurare Azure PowerShell](/powershell/azure/overview) tooinstall è.

Poiché Windows blocca automaticamente con estensione ps1,. dll e file .exe, criteri di esecuzione tooset hello è necessario prima di eseguire script hello. Assicurarsi che la finestra di Azure PowerShell hello è in esecuzione *come amministratore*. Eseguire **Set-ExecutionPolicy unrestricted**. Quando richiesto, digitare **Y**.

![Screenshot di "Set-ExecutionPolicy unrestricted" in esecuzione nella finestra di Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

Eseguire **Get-ExecutionPolicy** toomake assicurarsi che il comando hello sia stato risolto.

![Screenshot di "Get-ExecutionPolicy" in esecuzione nella finestra di Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

Passare toohello directory con gli script hello e applicazione del generatore.

![Schermata di "cd .\TollApp\TollApp" in esecuzione nella finestra di Azure PowerShell hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

Tipo **.\\ Setup.ps1** tooset un account di Azure, creare e configurare tutte le risorse necessarie e avviare gli eventi toogenerate. script Hello preleva in modo casuale dalla toocreate una regione di risorse. tooexplicitly specificare un'area, è possibile passare hello **-percorso** parametro come hello di esempio seguente:

**.\\Setup.ps1 -location "Stati Uniti centrali"**

![Schermata della pagina hello Accedi Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

script Hello apre hello **Accedi** pagina per Microsoft Azure. Immettere le credenziali dell'account.

> [!NOTE]
> Se l'account ha accesso toomultiple sottoscrizioni, sarà nome della sottoscrizione hello tooenter frequenti che si desidera toouse per esercitazione hello.
> 
> 

script Hello può richiedere diversi minuti toorun. Dopo il suo completamento, output di hello dovrebbe essere simile hello seguente schermata.

![Schermata di output dello script hello nella finestra di Azure PowerShell hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

Si verifica anche un'altra finestra che è simile toohello seguente schermata. Questa applicazione è l'invio di eventi tooAzure hub eventi, ovvero esercitazione hello toorun obbligatorio. In tal caso, non arrestare l'applicazione hello o chiudere questa finestra finché non viene completata l'esercitazione hello.

![Screenshot dell'invio dei dati dell'hub eventi](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

Si deve essere in grado di toosee le risorse nel portale di Azure a questo punto. Andare troppo<https://portal.azure.com>e accedere con le credenziali dell'account. Si noti che attualmente alcune funzionalità utilizza portale classico hello. Questi passaggi saranno indicati con chiarezza.

### <a name="azure-event-hubs"></a>Hub eventi di Azure
Nel portale di Azure hello, fare clic su **più servizi** nella parte inferiore di hello del riquadro sinistro di gestione di hello. Tipo **hub eventi** in hello campo fornito e fare clic su **hub eventi**. Verrà avviata un nuova hello di toodisplay finestra browser **BUS di servizio** area hello **portale classico**. Qui è possibile visualizzare hello Hub eventi creati da hello Setup.ps1 script.

![Bus di servizio](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

Fare clic su hello che inizia con *tolldata*. Fare clic su hello **hub eventi** scheda. Vengono visualizzati due Hub eventi denominati *entry* ed *exit* creati in questo spazio dei nomi.

![Scheda di hub di eventi nel portale classico hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a>Contenitore Archiviazione di Azure
1. Tornare toohello scheda nel portale di tooAzure aprire browser. Fare clic su **archiviazione** sul lato sinistro di hello toosee portale Azure hello Azure contenitore di archiviazione utilizzato nell'esercitazione hello hello.
   
    ![Voce di menu Archiviazione](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. Fare clic su hello uno che iniziano con *tolldata*. Fare clic su hello **contenitori** contenitore hello creato toosee di scheda.
   
    ![Scheda contenitori hello portale di Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. Fare clic su hello **tolldata** hello toosee contenitore caricato il file JSON che contiene i dati di registrazione vehicle.
   
    ![Schermata del file di registration.json hello nel contenitore di hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a>Database SQL di Azure
1. Nella scheda prima hello, che è stato aperto nel browser hello tornare indietro toohello portale di Azure. Fare clic su **database SQL** sul lato sinistro di hello toosee portale Azure hello database SQL a cui verrà utilizzato nell'esercitazione hello e fare clic su hello **tolldatadb**.
   
    ![Schermata di hello creato il database SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. Nome del server hello copia senza numero di porta hello (*servername*. database.windows.net, ad esempio).
    ![Schermata di hello creato il database di database SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)

## <a name="connect-toohello-database-from-visual-studio"></a>La connessione a database toohello da Visual Studio
Utilizzare Visual Studio tooaccess risultati della query nel database di output di hello.

La connessione a database SQL di toohello (destinazione hello) da Visual Studio:

1. Aprire Visual Studio e quindi fare clic su **strumenti** > **connettersi tooDatabase**.
2. Se richiesto, selezionare **Microsoft SQL Server** come origine dati.
   
    ![Finestra di dialogo Modifica origine dati](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. In hello **nome Server** campo, incollare il nome hello copiato nella sezione precedente hello dal portale di Azure hello (vale a dire *servername*. database.windows.net).
4. Selezionare **Usa autenticazione di SQL Server**.
5. Immettere **tolladmin** in hello **nome utente** campo e **123toll!** in hello **Password** campo.
6. Fare clic su **selezionare o immettere un nome di database**e selezionare **TollDataDB** come database hello.
   
    ![Finestra di dialogo Aggiungi connessione](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. Fare clic su **OK**.
8. Aprire Esplora server.
   
    ![Esplora server](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. Vedere quattro tabelle nel database TollDataDB hello.
   
    ![Tabelle nel database TollDataDB hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a>Generatore di eventi: progetto di esempio TollApp
Hello script di PowerShell viene avviato automaticamente toosend eventi utilizzando programma dell'applicazione di esempio TollApp hello. Non è necessario tooperform eventuali passaggi aggiuntivi.

Tuttavia, se si è interessati nei dettagli di implementazione, è possibile trovare il codice sorgente hello di hello applicazione TollApp in GitHub [esempi/TollApp](https://aka.ms/azure-stream-analytics-toll-source).

![Screenshot del codice di esempio visualizzato in Visual Studio](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a>Creare un processo di Analisi di flusso.
1. Nel portale di Azure hello, fare clic su hello segno verde nell'angolo superiore sinistro hello di hello pagina toocreate un nuovo processo di flusso Analitica. Selezionare **Intelligence e analisi** e quindi fare clic su **Processo di Analisi di flusso**.
   
    ![New button](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. Specificare un nome di processo, convalidare la sottoscrizione di hello sia corretto e quindi creare un nuovo gruppo di risorse in hello stessa area hello archiviazione hub di eventi (valore predefinito è Stati Uniti del centro per script hello).
3. Fare clic su **Pin toodashboard** e quindi **crea** nella parte inferiore di hello della pagina hello.
   
    ![Opzione Crea processo di Analisi di flusso](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a>Definire le origini di input
1. processo Hello creare e aprire una pagina di hello del processo. In alternativa, è possibile scegliere hello processo analitica nel dashboard del portale hello creato.

2. Fare clic su hello **input** scheda toodefine hello origine dati.
   
    ![scheda input Hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. Fare clic su **AGGIUNGERE UN INPUT**.
   
    ![Aggiungi un'opzione di Input Hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. Immettere **EntryStream** come **ALIAS DI INPUT**.
5. Il tipo di origine è **flusso di dati**
6. L'origine è **hub eventi**.
7. **Spazio dei nomi di Service bus** deve essere hello TollData hello elenco a discesa.
8. **Nome dell'hub eventi** deve essere impostato troppo**voce**.
9. **Nome criterio hub eventi*è **RootManageSharedAccessKey** (valore predefinito di hello).
10. Selezionare **JSON** per **FORMATO DI SERIALIZZAZIONE EVENTI** e **UTF8** per **CODIFICA**.
   
    Le impostazioni vengono visualizzate in questo modo:
   
    ![Impostazioni dell'hub eventi](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. Fare clic su **crea** nella parte inferiore di hello della creazione guidata hello pagina toofinish hello.
    
    Una volta creato il flusso di voce hello, si seguirà hello stesso flusso di uscita hello di toocreate passaggi. Essere valori tooenter che come nella seguente schermata hello.
    
    ![Impostazioni per il flusso di uscita hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    Sono stati definiti due flussi di input:
    
    ![Flussi di input definiti in hello portale di Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    Si aggiungeranno quindi input di dati di riferimento per i file blob hello che contiene dati di registrazione dell'automobile.
11. Fare clic su **aggiungere**, quindi seguire hello stesso processo per gli input flusso hello, ma si seleziona **dati di riferimento** anziché **flusso di dati** hello e **Alias di Input**  è **registrazione**.

12. account di archiviazione che inizia con **tolldata**. nome del contenitore Hello debba essere **tolldata**, hello e **il modello del percorso** deve essere **registration.json**. Il nome file fa distinzione tra maiuscole e minuscole e deve contenere solo **lettere minuscole**.
    
    ![Impostazioni dell'archivio BLOB](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. Fare clic su **crea** guidata hello toofinish.

Ora sono definiti tutti gli input.

## <a name="define-output"></a>Definire l'output
1. Nel riquadro Panoramica processo flusso Analitica hello selezionare **output**.
   
    ![scheda Output di Hello e l'opzione "Aggiungere un output"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. Fare clic su **Aggiungi**.
3. Set hello **alias di Output** too'output' e quindi **Sink** troppo**database SQL**.
3. Selezionare Nome hello del server che è stato utilizzato nella sezione "Connect tooDatabase da Visual Studio" dell'articolo hello hello. nome del database Hello **TollDataDB**.
4. Immettere **tolladmin** in hello **USERNAME** campo **123toll!** in hello **PASSWORD** , campo e **TollDataRefJoin** in hello **tabella** campo.
   
    ![Impostazioni del database SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. Fare clic su **Crea**.

## <a name="azure-stream-analytics-query"></a>Query di analisi di flusso di Azure
Hello **QUERY** scheda contiene una query SQL che trasformazioni hello dati in arrivo.

![Aggiunta di una query scheda Query toohello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

In questa esercitazione tenta tooanswer diverse domande aziendali che sono correlate dati tootoll e costrutti Analitica flusso esegue una query che possono essere usate in Azure flusso Analitica tooprovide una risposta pertinente.

Prima di iniziare il primo processo di flusso Analitica, vediamo alcuni scenari e la sintassi di query hello.

## <a name="introduction-tooazure-stream-analytics-query-language"></a>Introduzione tooAzure linguaggio di query Analitica di flusso
- - -
Si supponga che è necessario numero hello toocount dei veicoli che immette un casello. Poiché si tratta di un flusso continuo di eventi, occorre toodefine un "periodo di tempo." È opportuno modificare toobe domanda hello "quanti veicoli immettere un casello ogni tre minuti?". Si tratta di hello tooas comunemente noti a cascata di conteggio.

Diamo un'occhiata query Azure flusso Analitica hello che risponda a questa domanda:

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

Come si può notare, Analitica di flusso di Azure Usa un linguaggio di query che è simile a SQL e aggiunge alcune estensioni toospecify ora aspetti delle query hello.

Per ulteriori dettagli, fare riferimento a [gestione del tempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) e [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) costrutti utilizzati nella query hello da MSDN.

## <a name="testing-azure-stream-analytics-queries"></a>Eseguire i test delle query di analisi di flusso di Azure
Ora che è stato scritto della prima query Analitica di flusso di Azure, è possibile tootest ora utilizzando i file di dati di esempio che si trovano nella cartella TollApp nel seguente percorso hello:

**..\\TollApp\\TollApp\\Data**

Questa cartella contiene i seguenti file hello:

* Entry.json
* Exit.json
* registration.json

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a>Domanda 1: Numero di veicoli che entrano in un casello
1. Aprire hello portale di Azure e processo Analitica di flusso di Azure andare tooyour creato. Fare clic su hello **QUERY** scheda e incollare query dalla sezione precedente hello.

2. toovalidate questa query nei dati di esempio, caricare i dati in input EntryStream facendo hello hello hello... simbolo e selezionando **caricare i dati di esempio dal file**.

    ![Schermata del file Entry.json hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. Nel riquadro di hello che viene visualizzato il file hello selezionare (Entry.json) nel computer locale e fare clic su **OK**. Hello **Test** icona verrà accende ed essere selezionabile.
   
    ![Schermata del file Entry.json hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. Verificare che l'output di hello di query hello è come previsto:
   
    ![Risultati del test di hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a>Domanda 2: Tempo totale di Report per ogni toopass car tramite casello hello
tempo medio di Hello necessaria per un toopass car tramite casello hello consente l'efficienza di hello tooassess del processo di hello e analisi utilizzo software hello.

tempo totale di hello toofind, è necessario toojoin hello EntryTime flusso flusso ExitTime hello. Verrà aggiunta flussi hello in colonne TollId e LicencePlate. Hello **JOIN** operatore richiede flessibilità temporale toospecify che descrive il tempo accettabile di hello differenza tra hello unita in join gli eventi. Si utilizzerà **DATEDIFF** funzione toospecify che gli eventi devono essere non più di 15 minuti da altra. Verrà inoltre applicato hello **DATEDIFF** tooexit funzione e la voce volte toocompute hello tempo effettivo di un'automobile trascorre nella hello verde stazione. Si noti la differenza hello dell'utilizzo di hello del **DATEDIFF** quando viene usato un **selezionare** istruzione piuttosto che un **JOIN** condizione.

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. tootest questa query, query di aggiornamento hello in hello **QUERY** per processo hello. Aggiungere il file di test hello per **ExitStream** come **EntryStream** è stato immesso in precedenza.
   
2. Fare clic su **Test**.

3. Selezionare una casella di controllo tootest hello query e visualizzare hello output di hello:
   
    ![Output del test di hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a>Domanda 3: Report di tutti i veicoli commerciali con registrazione scaduta
Analitica di flusso di Azure è possibile utilizzare snapshot statici dei dati toojoin con flussi di dati temporali. toodemonstrate questa funzionalità, utilizzare hello domanda di esempio seguente.

Se un veicolo commerciale è registrato con società toll hello, può passare attraverso casello hello senza essere fermato per l'ispezione. Utilizzare tutti i veicoli commerciali scaduti registrazioni tooidentify tabella di ricerca registrazione veicolo commerciale.

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

tootest una query utilizzando i dati di riferimento, è necessario toodefine un'origine di input per i dati di riferimento hello, che è già stata eseguita.

tootest questa query, query hello Incolla in hello **QUERY** scheda, fare clic su **Test**e specificare le origini di input hello due registrazione hello dati di esempio e fare clic su **Test**.  
   
![Output del test di hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a>Avviare il processo di flusso Analitica hello
È ora toofinish hello configurazione e avvio hello processo timer. Salvare la query hello dalla domanda 3, che viene prodotto un output che corrispondenze hello dello schema di hello **TollDataRefJoin** tabella di output.

Processo passare toohello **DASHBOARD**, fare clic su **avviare**.

![Schermata del pulsante Start hello in dashboard processo hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

In hello finestra di dialogo che consente di aprire, modificare hello **avviare OUTPUT** troppo tempo**ora personalizzato**. Modifica hello ora tooone ora prima hello ora corrente. Questa modifica assicura che tutti gli eventi provenienti dall'hub di eventi hello vengono elaborati dopo l'avvio di eventi di hello toogenerate all'inizio di hello di esercitazione hello. Fare clic su hello **avviare** processo hello toostart di pulsante.

![Selezione dell'ora personalizzata](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

Avvio del processo di hello può richiedere alcuni minuti. È possibile visualizzare lo stato di hello nella pagina di primo livello hello per Analitica di flusso.

![Schermata di stato hello del processo di hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a>Controllare i risultati in Visual Studio
1. Aprire Esplora Server Visual Studio e fare doppio clic su hello **TollDataRefJoin** tabella.
2. Fare clic su **Mostra dati tabella** toosee output di hello del processo.
   
    ![Selezione di "Mostra dati tabella" in Esplora server](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a>Scalabilità orizzontale dei processi di Analisi di flusso di Azure
È progettato Azure Analitica flusso tooelastically ridimensionare in modo che possa gestire una grande quantità di dati. query di Hello Analitica di flusso di Azure è possibile utilizzare un **PARTITION BY** sistema di hello tootell clausola che questo passaggio verrà scalabilità orizzontale. **PartitionId** è una colonna speciale che hello sistema aggiunge l'ID di partizione hello toomatch dell'input hello (hub di eventi).

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. Interruzione processo corrente di hello, query di aggiornamento hello in hello **QUERY** scheda e aprire hello **impostazioni** ingranaggio in dashboard processo hello. Fare clic su **Scale**.
   
    **UNITÀ di STREAMING** definire quantità hello di potenza di calcolo che hello processo può ricevere.
2. Modifica hello elenco a discesa da 1 da 6.
   
    ![Screenshot della selezione di sei unità di streaming](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. Passare toohello **output** scheda e modificare il nome di hello della tabella SQL hello troppo**TollDataTumblingCountPartitioned**.

Se si avvia il processo di hello a questo punto, Azure flusso Analitica può distribuire il lavoro su più risorse di calcolo e migliorare la velocità effettiva. Si noti che TollApp applicazione hello è anche l'invio di eventi partizionati in base al TollId.

## <a name="monitor"></a>Monitorare
Hello **monitoraggio** area contenente le statistiche sull'esecuzione del processo hello. Prima volta che la configurazione è necessaria l'account di archiviazione toouse hello in hello stessa regione (nome casello come hello resto di questo documento).   

![Screenshot di monitoraggio](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

È possibile accedere a **log attività** dal dashboard processo hello **impostazioni** nonché l'area.


## <a name="conclusion"></a>Conclusioni
In questa esercitazione, è stato introdotto il servizio di Analitica di flusso di Azure toohello. Illustrato come tooconfigure input e output per hello processo flusso Analitica. Uno scenario casello dati hello esercitazione hello illustrati tipi comuni di problemi che si verificano nello spazio di hello dei dati in movimento e come può essere risolto con query SQL semplice in Azure flusso Analitica. esercitazione Hello descritto SQL costrutti di estensione per l'utilizzo di dati temporali. È stato illustrato come flussi di dati toojoin, come flusso di dati di hello tooenrich con dati di riferimento statici e come tooscale out una velocità effettiva superiore tooachieve query.

Anche se questa esercitazione offre una buona introduzione, non può ritenersi completa. È possibile trovare ulteriori modelli di query utilizzando linguaggio SAQL hello [esempi per modelli di utilizzo comune flusso Analitica Query](stream-analytics-stream-analytics-query-patterns.md).
Fare riferimento toohello [documentazione in linea](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn ulteriori informazioni sulla Analitica di flusso di Azure.

## <a name="clean-up-your-azure-account"></a>Eseguire la pulizia dell'account Azure
1. Arrestare il processo di flusso Analitica hello in hello portale di Azure.
   
    Hello Setup.ps1 script crea due hub di eventi e un database SQL. Hello seguendo la Guida di istruzioni che pulire le risorse al fine di hello dell'esercitazione hello.
2. In una finestra di PowerShell, digitare **.\\ Cleanup.ps1** script hello toostart che elimina le risorse utilizzate nell'esercitazione hello.
   
   > [!NOTE]
   > Le risorse sono identificate in base al nome hello. Assicurarsi di controllare attentamente ogni elemento prima di confermarne la rimozione.
   > 
   > 


