---
title: aaaConnect tooAzure DB Cosmos utilizzando gli strumenti di BI analitica | Documenti Microsoft
description: Informazioni su come toouse hello Azure Cosmos DB ODBC driver toocreate tabelle e viste in modo che sia possono visualizzare dati normalizzati in Business Intelligence e dati software analitica.
keywords: ODBC, driver ODBC
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 9967f4e5-4b71-4cd7-8324-221a8c789e6b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: e12a70f7805445f09fac01411e4bfbccc9a29c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-cosmos-db-using-bi-analytics-tools-with-hello-odbc-driver"></a>Connettersi tooAzure Cosmos DB usando gli strumenti di BI analitica con il driver ODBC di hello

Consente di driver ODBC di Azure Cosmos DB Hello tooconnect tooAzure DB Cosmos analitica BI utilizzando strumenti quali SQL Server Integration Services, Power BI Desktop e Tableau in modo da poter analizzare e creare visualizzazioni dei dati di Azure Cosmos DB le soluzioni.

Hello Azure Cosmos DB ODBC driver ODBC 3.8 conforme e supporta la sintassi ANSI SQL-92. Hello driver offre funzionalità avanzate toohelp si renormalize dati nel database di Azure Cosmos. Usa il driver hello, è possibile rappresentare i dati nel database di Azure Cosmos come tabelle e viste. driver Hello consente operazioni di SQL tooperform su tabelle hello e le viste incluse Raggruppa per le query, gli inserimenti, aggiornamenti ed eliminazioni.

## <a name="why-do-i-need-toonormalize-my-data"></a>Perché devo toonormalize dati?
DB Cosmos Azure è un database schemaless, che consente lo sviluppo rapido di applicazioni, consentendo di applicazioni tooiterate i dati del modello in tempo reale hello e non limitarli tooa strict schema. Un singolo database di Azure Cosmos DB può contenere documenti JSON con varie strutture. Questo è molto utile per lo sviluppo rapido di applicazioni, ma quando si desidera tooanalyze e creare report dei dati utilizzando analitica dei dati e strumenti di Business Intelligence, deve toobe bidimensionali spesso dati hello e rispettare tooa specifico schema.

Si tratta in cui è disponibile il driver ODBC hello in. Tramite driver ODBC di hello, è possibile ora rinormalizzato dati nel database di Azure Cosmos in tabelle e viste tooyour dati analitici e di creazione di report è necessario. gli schemi di Hello rinormalizzato non hanno effetto sui dati sottostanti hello e non limitare gli sviluppatori tooadhere toothem, consentono semplicemente si tooleverage conforme a ODBC strumenti tooaccess hello dati. A questo punto il database di Azure Cosmos DB non sarà apprezzato solo dal team di sviluppo, ma anche dagli analisti dei dati.

Ora consente di iniziare con il driver ODBC di hello.

## <a id="install"></a>Passaggio 1: Installare i driver ODBC di Azure Cosmos DB hello

1. Scaricare i driver di hello per l'ambiente:

    * [Microsoft Azure Cosmos DB ODBC 64-bit.msi](https://aka.ms/documentdb-odbc-64x64) per Windows a 64 bit
    * [Microsoft Azure Cosmos DB ODBC 32x64-bit.msi](https://aka.ms/documentdb-odbc-32x64) per Windows a 32 bit in Windows a 64 bit
    * [Microsoft Azure Cosmos DB ODBC 32-bit.msi](https://aka.ms/documentdb-odbc-32x32) per Windows a 32 bit

    Esecuzione hello msi file localmente, quali hello inizia **guidata di installazione di Microsoft Azure Cosmos DB ODBC Driver**. 
2. Completare la procedura guidata installazione hello tramite driver ODBC di hello predefinito tooinstall input hello.
3. Aprire hello **Amministratore origine dati ODBC** app nel computer, è possibile farlo digitare **origini dati ODBC** Windows hello casella di ricerca. 
    È possibile confermare hello driver è stato installato, fare clic su hello **driver** scheda e garantire **Driver ODBC di Microsoft Azure Cosmos DB** è elencato.

    ![Amministrazione origine dati ODBC di Azure Cosmos DB](./media/odbc-driver/odbc-driver.png)

## <a id="connect"></a>Passaggio 2: Connessione database Azure Cosmos DB tooyour

1. Dopo aver [installazione hello Azure Cosmos DB Provider ODBC](#install), in hello **Amministrazione origine dati ODBC** finestra, fare clic su **Aggiungi**. È possibile creare un DSN utente o di sistema. In questo esempio viene creato un DSN utente.
2. In hello **Crea nuova origine dati** selezionare **Driver ODBC di Microsoft Azure Cosmos DB**, quindi fare clic su **fine**.
3. In hello **Azure Cosmos DB ODBC Driver SDN installazione** compilare seguente hello: 

    ![Finestra Azure Cosmos DB ODBC Driver DSN Setup (Configurazione DSN driver ODBC di Azure Cosmos DB)](./media/odbc-driver/odbc-driver-dsn-setup.png)
    - **Nome dell'origine dati**: nome descrittivo per hello DSN ODBC. Questo nome è univoco tooyour Azure Cosmos DB account, quindi assegnare in modo appropriato se si hanno più account.
    - **Descrizione**: una breve descrizione dell'origine dati hello.
    - **Host**: URI dell'account Azure Cosmos DB. È possibile recuperare questo dal Pannello di chiavi di Azure Cosmos DB hello in hello portale di Azure, come illustrato nella seguente schermata hello. 
    - **Tasto**: hello chiave primaria o secondaria, lettura / scrittura o sola lettura dal Pannello di chiavi di Azure Cosmos DB hello in hello portale di Azure, come illustrato nella seguente schermata hello. È consigliabile che utilizzare il tasto di sola lettura hello se hello DSN viene utilizzato per l'elaborazione dati di sola lettura e creazione di report.
    ![Pannello Chiavi di Azure Cosmos DB](./media/odbc-driver/odbc-driver-keys.png)
    - **Crittografare la chiave di accesso per**: selezionare migliore hello in base agli utenti di hello del computer. 
4. Fare clic su hello **Test** toomake pulsante che sia possibile connettersi account Azure Cosmos DB tooyour. 
5. Fare clic su **opzioni avanzate** e hello set seguenti valori:
    - **Eseguire una query coerenza**: hello seleziona [livello di coerenza](consistency-levels.md) per le operazioni. valore predefinito di Hello è sessione.
    - **Numero di tentativi**: hello di numero di volte in cui un'operazione se la richiesta iniziale hello non viene completata a causa di limitazione delle richieste tooservice tooretry.
    - **File di schema**: si dispone di una serie di opzioni.
        - Per impostazione predefinita, se si lascia questa voce è (vuoto), driver hello esegue l'analisi di dati di pagina prima di hello per tutti gli schemi di hello toodetermine raccolte di ciascuna raccolta. L'operazione è definita Mapping raccolta. Senza un file di schema definito, il driver di hello ha tooperform hello analisi per ogni sessione di driver e potrebbe provocare un avvio più di un'applicazione tramite hello DSN. È consigliabile associare sempre un file di schema per un DSN.
        - Se si dispone già di un file di schema (probabilmente uno creato usando hello [Editor schemi](#schema-editor)), è possibile fare clic su **Sfoglia**, passare il file tooyour, fare clic su **salvare**e quindi fare clic su **OK**.
        - Se si desidera toocreate un nuovo schema, fare clic su **OK**, quindi fare clic su **Editor schemi** nella finestra principale di hello. Procedere quindi toohello [Editor schemi](#schema-editor) informazioni. Al momento della creazione nuovo file di schema hello, ricordarsi toohello indietro toogo **opzioni avanzate** file di schema finestra tooinclude hello appena creato.

6. Dopo aver completato e chiudere hello **configurazione DSN di Azure Cosmos DB ODBC Driver** finestra hello nuovo DSN utente viene aggiunto scheda DSN utente toohello.

    ![Nuovo Azure Cosmos DB DSN ODBC nella scheda DSN utente hello](./media/odbc-driver/odbc-driver-user-dsn.png)

## <a id="#collection-mapping"></a>Passaggio 3: Creare una definizione di schema con metodo di mapping insieme hello

Esistono due tipi di metodi di campionamento da utilizzare: il **mapping raccolta** o i **delimitatori di tabella**. Una sessione di campionamento può usare entrambi i metodi, ma ogni raccolta può usarne solo uno specifico. i passaggi di Hello seguenti crea uno schema per i dati di hello in uno o più raccolte con metodo di mapping insieme hello. Questo metodo di campionamento recupera dati hello nella pagina di hello di una struttura di hello toodetermine di raccolta dei dati di hello. Consente di invertire una tabella tooa insieme sul lato ODBC hello. Questo metodo di campionamento è efficace e rapido quando i dati di hello in una raccolta sono omogenei. Se una raccolta contiene eterogenea tipo di dati, si consiglia di usare hello [tabella delimitatori mapping metodo](#table-mapping) che fornisce un metodo di campionamento più affidabile toodetermine hello strutture di dati raccolta hello. 

1. Dopo aver completato i passaggi da 1 a 4 in [Connetti tooyour Azure Cosmos DB database](#connect), fare clic su **Editor schemi** in hello **configurazione DSN di Azure Cosmos DB ODBC Driver** finestra.

    ![Pulsante editor schema nella finestra di installazione di Azure Cosmos DB ODBC Driver DSN hello](./media/odbc-driver/odbc-driver-schema-editor.png)
2. In hello **Editor schemi** finestra, fare clic su **Crea nuovo**.
    Hello **genera Schema** finestra Visualizza tutte le raccolte di hello in hello account Azure Cosmos DB. 
3. Selezionare uno o più toosample raccolte e quindi fare clic su **esempio**. 
4. In hello **visualizzazione Progettazione** sono rappresentati scheda, hello database, schema e tabella. In visualizzazione tabella hello analisi hello Visualizza set di hello di proprietà associate a nomi di colonna hello (nome SQL, nome di origine e così via).
    Per ogni colonna, è possibile modificare nome SQL della colonna hello, tipo SQL hello, lunghezza SQL (se applicabile), scala (se applicabile), precisione (se applicabile) e ammette valori null.
    - È possibile impostare **Nascondi colonna** troppo**true** se si desidera tooexclude tale colonna dai risultati della query. Le colonne contrassegnate Nascondi colonna = true non vengono restituiti per la selezione e proiezione, sebbene siano ancora parte dello schema hello. Ad esempio, è possibile nascondere tutte le proprietà di sistema necessarie hello Azure Cosmos DB a partire da "_".
    - Hello **id** colonna è hello unico campo che non può essere nascosti poiché viene utilizzata come chiave primaria di hello nello schema normalizzato hello. 
5. Dopo aver completato la definizione di schema hello, fare clic su **File** | **salvare**, passare lo schema di hello toohello directory toosave e quindi fare clic su **salvare**.

    Se in futuro hello desideri toouse questo schema con un DSN, aprire finestra di installazione di Azure Cosmos DB ODBC Driver DSN hello (tramite Amministrazione origine dati ODBC hello), fare clic su Opzioni avanzate e quindi nella casella File di Schema hello passare toohello salvata dello schema. Il salvataggio di un tooan di file di schema esistente DSN modifica dati toohello tooscope di hello DSN connessione e la struttura definita dallo schema.

## <a id="table-mapping"></a>Passaggio 4: Creare una definizione di schema delimitatori hello tabella-mapping (metodo)

Esistono due tipi di metodi di campionamento da utilizzare: il **mapping raccolta** o i **delimitatori di tabella**. Una sessione di campionamento può usare entrambi i metodi, ma ogni raccolta può usarne solo uno specifico. 

Hello seguenti passaggi necessari per creare uno schema per i dati di hello in uno o più raccolte utilizzando hello **tabella delimitatori** mapping metodo. È consigliabile usare questo metodo di campionamento quando le raccolte contengono tipi eterogenei di dati. È possibile utilizzare questo hello tooscope metodo di campionamento tooa set di attributi e i valori corrispondenti. Ad esempio, se un documento contiene una proprietà "Type", è possibile definire l'ambito valori toohello di campionamento hello di questa proprietà. il risultato finale Hello di campionamento hello sarebbe un set di tabelle per ognuno dei valori di hello per il tipo è stato specificato. Ad esempio, Tipo = Car produrrà una tabella Car mentre Tipo = Plane produrrà una tabella Plane.

1. Dopo aver completato i passaggi da 1 a 4 in [Connetti tooyour Azure Cosmos DB database](#connect), fare clic su **Editor schemi** nella finestra di installazione di Azure Cosmos DB ODBC Driver DSN hello.
2. In hello **Editor schemi** finestra, fare clic su **Crea nuovo**.
    Hello **genera Schema** finestra Visualizza tutte le raccolte di hello in hello account Azure Cosmos DB. 
3. Selezionare una raccolta in hello **vista di esempio** scheda hello **Mapping definizione** colonna per la raccolta di hello, fare clic su **modifica**. Quindi in hello **Mapping definizione** selezionare **tabella delimitatori** metodo. Quindi hello seguenti:

    a. In hello **attributi** casella, il nome del tipo hello di una proprietà delimitatore. Si tratta di una proprietà del documento che si desidera campionamento hello tooscope, ad esempio, città e premere INVIO. 

    b. Se si vuole solo i valori di toocertain tooscope hello campionamento per attributo hello appena immesso, selezionare l'attributo hello nella casella di selezione di hello, quindi immettere un valore in hello **valore** casella, ad esempio, Seattle, quindi premere INVIO. È possibile continuare a tooadd più valori per gli attributi. Assicurarsi solo che hello corretto attributo viene selezionato quando si immettono valori.

    Ad esempio, se si include un **attributi** valore City e si desidera toolimit tooonly la tabella include le righe con un valore di città di New York e Dubai, immettere City casella attributi hello e New York e quindi Dubai in hello  **I valori** casella.
4. Fare clic su **OK**. 
5. Dopo aver completato le definizioni di mapping hello per le raccolte di hello desiderato toosample, in hello **Editor schemi** finestra, fare clic su **esempio**.
     Per ogni colonna, è possibile modificare nome SQL della colonna hello, tipo SQL hello, lunghezza SQL (se applicabile), scala (se applicabile), precisione (se applicabile) e ammette valori null.
    - È possibile impostare **Nascondi colonna** troppo**true** se si desidera tooexclude tale colonna dai risultati della query. Le colonne contrassegnate Nascondi colonna = true non vengono restituiti per la selezione e proiezione, sebbene siano ancora parte dello schema hello. Ad esempio, è possibile nascondere tutte le proprietà del sistema richiesto Azure Cosmos DB hello a partire da "_".
    - Hello **id** colonna è hello unico campo che non può essere nascosti poiché viene utilizzata come chiave primaria di hello nello schema normalizzato hello. 
6. Dopo aver completato la definizione di schema hello, fare clic su **File** | **salvare**, passare lo schema di hello toohello directory toosave e quindi fare clic su **salvare**.
7. In hello **configurazione DSN di Azure Cosmos DB ODBC Driver** finestra, fare clic su * * Avanzate opzioni * *. Quindi, nel hello **File di Schema** passare il file di schema toohello salvato e fare clic su **OK**. Fare clic su **OK** nuovamente toosave hello DSN. Questo schema consente di risparmiare hello toohello DSN è stato creato. 

## <a name="optional-creating-views"></a>(Facoltativo) Creazione di visualizzazioni
È possibile definire e creare visualizzazioni come parte del processo di campionamento hello. Queste visualizzazioni sono tooSQL equivalente. Sono di sola lettura e sono selezioni hello ambito e le proiezioni di hello che Azure Cosmos DB SQL definiti. 

una visualizzazione dei dati, in hello toocreate **Editor schemi** hello della finestra **le definizioni delle viste** colonna, fare clic su **Aggiungi** nella riga hello del toosample raccolta hello. Quindi in hello **le definizioni delle viste** finestra hello seguenti:
1. Fare clic su **New**, immettere un nome per la visualizzazione di hello, ad esempio, EmployeesfromSeattleView e quindi fare clic su **OK**.
2. In hello **Modifica visualizzazione** finestra, immettere una query di database di Azure Cosmos. Deve trattarsi di una query SQL di Azure Cosmos DB, ad esempio `SELECT c.City, c.EmployeeName, c.Level, c.Age, c.Gender, c.Manager FROM c WHERE c.City = “Seattle”`. Fare clic su **OK**.

È possibile creare un numero illimitato di visualizzazioni. Dopo aver eseguito una definizione di viste hello, è quindi possibile campionare i dati di hello. 

## <a name="step-5-view-your-data-in-bi-tools-such-as-power-bi-desktop"></a>Passaggio 5: Visualizzare i dati in strumenti di BI quali Power BI Desktop

È possibile utilizzare il nuovo tooconnect DSN DocumentADB con qualsiasi strumento conforme a ODBC - questo passaggio semplicemente illustra come tooconnect tooPower BI Desktop e creare una visualizzazione di Power BI.

1. Aprire Power BI Desktop.
2. Fare clic su **Recupera dati**.
3. In hello **recupera dati** finestra, fare clic su **altri** | **ODBC** | **Connetti**.
4. In hello **da ODBC** (finestra), nome dell'origine dati selezionare hello creato e quindi fare clic su **OK**. È possibile lasciare hello **opzioni avanzate** voci vuote.
5. In hello **accedere a un'origine dati tramite un driver ODBC** selezionare **predefinita o personalizzata** e quindi fare clic su **Connetti**. Non è necessario hello tooinclude **credenziali proprietà della stringa di connessione**.
6. In hello **Navigator** finestra, nel riquadro di sinistra hello, espandere database hello, schema hello e quindi selezionare hello tabella. riquadro risultati Hello include dati di hello utilizzando hello schema che è stato creato.
7. toovisualize hello dati in Power BI desktop, selezionare la casella hello davanti al nome della tabella hello e quindi fare clic su **carico**.
8. In Power BI Desktop, selezionare nella hello all'estrema sinistra, scheda dati hello ![Scheda dati in Power BI Desktop](./media/odbc-driver/odbc-driver-data-tab.png) tooconfirm i dati sono stati importati.
9. È ora possibile creare oggetti visivi usando Power BI facendo clic sulla scheda Report hello ![scheda Report in Power BI Desktop](./media/odbc-driver/odbc-driver-report-tab.png), facendo clic su **nuovo Visual**e quindi la personalizzazione del riquadro. Per altre informazioni sulla creazione di visualizzazioni in Power BI Desktop, vedere [Tipi di visualizzazioni in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-visualization-types-for-reports-and-q-and-a/).

## <a name="troubleshooting"></a>Risoluzione dei problemi

Se viene visualizzato il seguente errore hello, assicurarsi di hello **Host** e **chiave di accesso** valori copiato hello portale di Azure in [passaggio 2](#connect) siano corrette, quindi riprovare. Utilizzare hello copia pulsanti toohello diritto di hello **Host** e **chiave di accesso** valori hello toocopy portale Azure hello valori senza errori.

    [HY000]: [Microsoft][Azure Cosmos DB] (401) HTTP 401 Authentication Error: {"code":"Unauthorized","message":"hello input authorization token can't serve hello request. Please check that hello expected payload is built as per hello protocol, and check hello key being used. Server used hello following payload toosign: 'get\ndbs\n\nfri, 20 jan 2017 03:43:55 gmt\n\n'\r\nActivityId: 9acb3c0d-cb31-4b78-ac0a-413c8d33e373"}`

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni su Azure Cosmos DB, vedere [che cos'è Azure Cosmos DB?](introduction.md).
