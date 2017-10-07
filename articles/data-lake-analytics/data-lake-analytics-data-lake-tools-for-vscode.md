---
title: 'Strumenti Azure Data Lake: Usare Strumenti Azure Data Lake per Visual Studio Code | Microsoft Docs'
description: 'Informazioni su come toouse Azure Data Lake Tools per Visual Studio Code toocreate, testare ed eseguire gli script U-SQL. '
Keywords: Percorso di toostorage di caricamento di VScode, strumenti di Azure Data Lake, esecuzione, file di archiviazione locale di debug, eseguire il Debug locale, anteprima locale
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>Usare gli Strumenti Azure Data Lake per Visual Studio Code

Informazioni su come toouse Azure Data Lake Tools per Visual Studio Code (codice di Visual Studio) toocreate, testare ed eseguire gli script U-SQL. informazioni di Hello sono anche incluso in hello video seguente:

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>Prerequisiti

Data Lake Tools può essere installato su piattaforme hello supportate dal codice di Visual Studio. piattaforme supportata Hello includono Windows, Linux e MacOS. diverse piattaforme Hello hanno hello seguenti prerequisiti:

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Aggiornamento 77 o successivo di Java SE Runtime Environment, versione 8](https://java.com/download/manual.jsp). Aggiungere hello java.exe toohello sistema ambiente variabile percorso. Per istruzioni sulla configurazione, vedere [come impostare o modificare una variabile di sistema Path hello?]( https://www.java.com/download/help/path.xml). percorso di Hello è tooC:\Program Files\Java\jdk1.8.0_77\jre\bin simile.
    - [Runtime di .NET Core SDK 1.0.3 o .NET Core 1.1](https://www.microsoft.com/net/download).
    
- Linux (è consigliabile scegliere Ubuntu 14.04 LTS)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx). tooinstall hello codice, immettere hello comando seguente:

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/). 

        - pacchetto di deb hello tooupdate del codice sorgente, immettere hello seguenti comandi:

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - tooinstall Mono, immettere hello comando seguente:

                sudo apt-get install mono-complete

            > [!NOTE] 
            > Mono 4.6 non è supportato. Disinstallare completamente la versione 4.6 prima di installare la versione 4.2.x.  

        - [Aggiornamento 77 o successivo di Java SE Runtime Environment, versione 8](https://java.com/download/manual.jsp). Per istruzioni sull'installazione, vedere hello [Linux a 64 bit di istruzioni di installazione per Java]( https://java.com/en/download/help/linux_x64_install.xml) pagina.
        - [Runtime di .NET Core SDK 1.0.3 o .NET Core 1.1](https://www.microsoft.com/net/download).
- MacOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/). 
    - [Aggiornamento 77 o successivo di Java SE Runtime Environment, versione 8](https://java.com/download/manual.jsp). Per istruzioni sull'installazione, vedere hello [Linux a 64 bit di istruzioni di installazione per Java](https://java.com/en/download/help/mac_install.xml) pagina.
    - [Runtime di .NET Core SDK 1.0.3 o .NET Core 1.1](https://www.microsoft.com/net/download).

## <a name="install-data-lake-tools"></a>Installare gli strumenti di Data Lake

Dopo aver installato i prerequisiti di hello, è possibile installare Data Lake Tools per Visual Studio Code.

**tooinstall Data Lake Tools**

1. Aprire Visual Studio Code.
2. Selezionare Ctrl + P e quindi immettere hello comando seguente:
```
ext install usql-vscode-ext
```
È possibile visualizzare un elenco delle estensioni di codice di Visual Studio, tra cui Una di queste è costituita da **Strumenti Azure Data Lake**.

3. Selezionare **installare** Avanti troppo**Azure Data Lake Tools**. Dopo alcuni secondi, hello **installare** pulsante verrà modificato troppo**Ricarica**.
4. Selezionare **Ricarica** estensione hello tooactivate.
5. Selezionare **OK** tooconfirm. È possibile visualizzare gli strumenti di Azure Data Lake nella hello **estensioni** riquadro.
    ![Riquadro Estensioni di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>Attivare Strumenti Azure Data Lake
Creare un nuovo file .usql o aprire esistente .usql tooactivate hello estensione di file. 

## <a name="connect-tooazure"></a>Connettersi tooAzure

Prima di è possibile compilare ed eseguire gli script U-SQL in Data Lake Analitica, è necessario connettersi tooyour account Azure.

**tooconnect tooAzure**

1.  Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza. 
2.  Immettere **ADL: Login** (ADL: Accedi). informazioni di accesso Hello viene visualizzato in hello **Output** riquadro.

    ![Riquadro comandi di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Informazioni di accesso di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. Selezionare Ctrl + clic sull'URL di account di accesso hello: pagina Web di accesso https://aka.ms/devicelogin tooopen hello. Immettere il codice hello **G567LX42V** nella casella di testo hello e quindi selezionare **continua**.

   ![Codice di accesso da incollare di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  Seguire toosign istruzioni hello dalla pagina Web hello. Quando si è connessi, il nome dell'account di Azure viene visualizzato sulla barra di stato hello nell'angolo inferiore sinistro hello di hello **Visual Studio Code** finestra. 

    > [!NOTE] 
    > Se l'account ha due fattori abilitati, è consigliabile usare l'autenticazione telefonica anziché un PIN.

toosign, immettere il comando hello **ADL: disconnessione**.

## <a name="list-your-data-lake-analytics-accounts"></a>Elencare gli account di Data Lake Analytics personali

connessione di hello tootest, ottenere un elenco di account Data Lake Analitica.

**toolist hello Data Lake Analitica gli account utilizzati per la sottoscrizione di Azure**

1. Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.
2. Immettere **ADL: List Accounts** (ADL: Elenca gli account). gli account Hello appaiano nel hello **Output** riquadro.

## <a name="open-hello-sample-script"></a>Script di esempio hello aperto
Aprire il riquadro comandi hello (Ctrl + MAIUSC + P) e immettere **ADL: aprire uno Script di esempio**. Verrà quindi aperta un'altra istanza di questo esempio. Anche in questa istanza è possibile modificare, configurare e inviare lo script.

## <a name="work-with-u-sql"></a>Uso di U-SQL

È necessario aprire un file U-SQL o una cartella toowork con U-SQL.

**tooopen una cartella per il progetto U-SQL**

1. Il codice di Visual Studio, selezionare hello **File** menu e quindi selezionare **Apri cartella**.
2. Specificare una cartella e quindi scegliere **Seleziona cartella**.
3. Seleziona hello **File** menu e quindi selezionare **New**. Un file senza titolo 1 viene aggiunto il progetto toohello.
4. Immettere hello seguente codice nel file hello senza titolo 1:

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    script Hello crea un file departments.csv con alcuni dati inclusi nella cartella /output hello.

5. Salvare il file hello come **myUSQL.usql** hello aprire cartella. Un file di configurazione adltools_settings.json aggiunto anche toohello progetto.
4. Aprire e configurare adltools_settings.json con hello le proprietà seguenti:

    - Account: un account di Data Lake Analytics sotto la sottoscrizione di Azure.
    - Database: un database nel proprio account. valore predefinito di Hello è **master**.
    - Schema: uno schema nel database. valore predefinito di Hello è **dbo**.
    - Impostazioni facoltative:
        - Priorità: intervallo di priorità hello è 1 too1000 con 1 come priorità più alta hello. valore predefinito di Hello è **1000**.
        - Parallelismo: intervallo di parallelismo hello è compreso tra 1 too150. valore predefinito di Hello è parallelismo di hello massimo consentito nell'account di Azure Data Lake Analitica. 
        
        > [!NOTE] 
        > Se le impostazioni di hello non sono validi, vengono utilizzati i valori predefiniti di hello.

    ![File di configurazione degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    Un calcolo account Data Lake Analitica è necessario toocompile ed eseguire processi U-SQL. È necessario configurare l'account computer hello prima di compilare ed eseguire i processi di U-SQL.
    
Dopo aver salvata la configurazione hello, sulla barra di stato hello nell'angolo inferiore sinistro di hello del file .usql corrispondente hello hello informazioni di schema, database e account. 
 
 
Confrontati tooopening un file, quando si apre una cartella in cui che è possibile:

- Usare un file code-behind. Codice non è supportato in modalità solo file hello.
- Usare un file di configurazione. Quando si apre una cartella, gli script hello nella cartella di lavoro hello condividono un singolo file di configurazione.


Hello script U-SQL viene compilato in modalità remota tramite il servizio Data Lake Analitica hello. Quando si esegue hello **compilare** comando inviato account Data Lake Analitica tooyour hello script U-SQL. Successivamente, codice di Visual Studio riceve il risultato della compilazione hello. A causa di compilazione remoto toohello, codice di Visual Studio richiede informazioni hello tooconnect tooyour Data Lake Analitica account nel file di configurazione hello elencati.

**script toocompile U-SQL**

1. Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza. 
2. Immettere **ADL: Compile Script**. Hello compilazione risultati vengono visualizzati in hello **Output** finestra. È possibile anche fare doppio clic su un file di script e quindi selezionare **ADL: compilare Script** processo toocompile U-SQL. viene visualizzato il risultato della compilazione Hello in hello **Output** riquadro.
 

**script toosubmit U-SQL**

1. Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza. 
2. Immettere **ADL: Submit Job**.  È anche possibile fare clic con il pulsante destro del mouse su un file di script e selezionare **ADL: Invia processo**. 

Dopo aver inviato un processo U-SQL, i log di invio di hello vengono visualizzati in hello **Output** finestra in Visual Studio Code. Se l'invio di hello ha esito positivo, viene visualizzato anche hello processo URL. È possibile aprire URL processo hello in uno stato di processo in tempo reale di web browser tootrack hello.

output di hello tooenable dettagli processo hello, impostare **jobInformationOutputPath** in hello **codice di Visual Studio per hello u-sql_settings.json** file.
 
## <a name="use-a-code-behind-file"></a>Usare un file code-behind

Un file code-behind è un file C# associato a uno script U-SQL. È possibile definire un tooUDO script dedicato, aggregazione definita dall'utente, tipo definito dall'utente e funzioni definite dall'utente nel file code-behind hello. Hello UDO, aggregazione definita dall'utente, tipo definito dall'utente e la funzione definita dall'utente è utilizzabile direttamente nello script di hello senza registrare assembly hello prima. Hello file code-behind viene inserito in hello stessa cartella del relativo file di script U-SQL peering. Se lo script di hello è denominato xxx.usql, denominato codice hello come xxx.usql.cs. Se si elimina manualmente file code-behind hello, funzionalità code-behind hello è disabilitata per lo script U-SQL associato. Per altre informazioni sulla scrittura del codice cliente per lo script U-SQL, vedere [Scrivere e usare il codice personalizzato in U-SQL: funzioni definite dall'utente]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).

codice toosupport, è necessario aprire una cartella di lavoro. 

**un file code-behind toogenerate**

1. Aprire un file di origine. 
2. Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.
3. Immettere **ADL: Generate Code Behind**. Viene creato un file code-behind in hello stessa cartella. 

È anche possibile fare clic con il pulsante destro del mouse su un file di script e selezionare **ADL: Generate Code Behind** (ADL: Genera code-behind). 

toocompile e inviare uno script U-SQL con un file code-behind è hello uguale al file di script con la versione autonoma di hello U-SQL.

Hello due schermate seguenti Mostra un file code-behind e il relativo file di script U-SQL associato:
 
![Code-behind di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![File di script code-behind di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>Usare gli assembly

Per informazioni sullo sviluppo di assembly, vedere [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Sviluppare assembly U-SQL per i processi di Azure Data Lake Analytics).

È possibile utilizzare gli assembly di codice personalizzato tooregister Data Lake Tools nel catalogo dati Lake Analitica hello.

**tooregister un assembly**

È possibile registrare l'assembly hello tramite hello **ADL: registrare Assembly** o **ADL: registrare Assembly tramite la configurazione** comandi.

**tooregister tramite hello ADL: comando registra Assembly**
1.  Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.
2.  Immettere **ADL: Register Assembly** (ADL: Registra assembly). 
3.  Specificare il percorso di assembly locale hello. 
4.  Selezionare un account di Data Lake Analytics.
5.  Selezionare un database.

Risultati: portale hello viene aperto in un browser e Visualizza processo di registrazione assembly hello.  

Un altro hello di tootrigger pratica **ADL: registrare Assembly** comando è file con estensione DLL di hello tooright clic in Esplora File. 

**tooregister hello tuttavia ADL: registrare Assembly tramite il comando di configurazione**
1.  Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.
2.  Immettere **ADL: Register Assembly through Configuration** (ADL: Registra assembly da configurazione). 
3.  Specificare il percorso di assembly locale hello. 
4.  file JSON Hello viene visualizzato. Esaminare e modificare le dipendenze dell'assembly hello e i parametri delle risorse, se necessario. Le istruzioni vengono visualizzate in hello **Output** finestra. tooproceed toohello registrazione dell'assembly, salvare file JSON di hello (Ctrl + S).

![Code-behind di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- Le dipendenze dell'assembly: rileva automaticamente gli strumenti di Azure Data Lake hello DLL se dispone di tutte le dipendenze. dipendenze di Hello vengono visualizzate nel file JSON hello dopo che vengono rilevati. 
>- Risorse: È possibile caricare le risorse DLL (ad esempio, txt, PNG e CSV) come parte della registrazione dell'assembly hello. 

Hello di tootrigger un altro modo **ADL: registrare Assembly tramite la configurazione** è file. dll di hello tooright clic in Esplora File. 

Hello codice U-SQL seguente viene illustrato come toocall un assembly. Nell'esempio hello è il nome dell'assembly hello *test*.

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a>Catalogo dati Lake Analitica hello di accesso

Dopo avere stabilito la connessione tooAzure, è possibile utilizzare hello catalog di passaggi tooaccess hello U-SQL seguente.

**metadati di Azure Data Lake Analitica hello tooaccess**

1.  Premere CTRL+MAIUSC+P e digitare **ADL: List Tables** (ADL: Elenca tabelle).
2.  Selezionare uno degli account Data Lake Analitica hello.
3.  Selezionare uno dei database di Data Lake Analitica hello.
4.  Selezionare uno degli schemi di hello. È possibile visualizzare l'elenco di hello delle tabelle.

## <a name="view-data-lake-analytics-jobs"></a>Visualizzare i processi di Data Lake Analytics

**processi di Data Lake Analitica tooview**
1.  Aprire il riquadro comandi hello (Ctrl + MAIUSC + P) e selezionare **ADL: processo mostra**. 
2.  Selezionare un account di Data Lake Analytics o locale. 
3.  Attendere per l'elenco di processi hello tooappear account hello.
4.  Selezionare un processo dall'elenco di processi, Data Lake Tools apre i dettagli dei processi hello nel portale di Azure hello e visualizza i file di JobInfo hello in Visual Studio Code.

![Tipi di oggetto IntelliSense degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Integrazione di Azure Data Lake Store

È possibile usare i comandi correlati all'archiviazione di Azure Data Lake per:
 - Esplorare le risorse di archiviazione di Azure Data Lake hello. 
 - File di archiviazione di Azure Data Lake hello di anteprima.  
 - Caricare hello direttamente file tooAzure Lake archiviazione dei dati in Visual Studio Code. 

### <a name="list-hello-storage-path"></a>Percorso di archiviazione hello elenco 
È possibile elencare percorso di archiviazione hello tramite tavolozza comando hello o pulsante destro del mouse.

**percorso di archiviazione di hello toolist tramite tavolozza comando hello**

1.  Aprire il riquadro comandi hello (Ctrl + MAIUSC + P) e immettere **ADL: percorso di archiviazione elenco**.

    ![Elencare il percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  Selezionare il modo migliore per elencare il percorso di archiviazione hello. Questo passaggio usa **Enter a path** (Immetti un percorso) come esempio.

    ![Data Lake Tools per Visual Studio Code percorso di archiviazione hello toolist unidirezionale](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- Codice di Visual Studio consente di mantenere percorso visitato ultimo hello ogni account Data Lake Analitica. Ad esempio /tt/ss.
    >- Browser dal percorso radice: percorso radice di elenco hello dall'account Data Lake Analitica selezionato o un percorso locale.
    >- Immettere un percorso: elencare un percorso specificato dall'account di Data Lake Analytics selezionato o un percorso locale.
    
3. Selezionare un account dal percorso locale hello o un account Data Lake Analitica.

    ![Selezionare altro in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. Selezionare **più** toolist ulteriori account Data Lake Analitica e quindi selezionare un account Data Lake Analitica.

    ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  Immettere un percorso di archiviazione di Azure. Ad esempio /output.

    ![Immettere un percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  Risultati: tavolozza di hello comando Visualizza le informazioni di percorso hello in base ai valori immessi.

    ![Risultato dell'inserimento del percorso di archiviazione di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Un modo più pratico percorso relativo di toolist hello è tramite hello fare clic sul menu di scelta rapida.

**percorso di archiviazione hello toolist tramite mouse**

1.  Fare doppio clic su hello percorso stringa tooselect **il percorso di archiviazione elenco**.

       ![Menu di scelta rapida di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. percorso relativo di Hello selezionato viene visualizzato nel riquadro comandi hello.

   ![Percorso relativo selezionato in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  Selezionare un account dal percorso locale hello o un account Data Lake Analitica.

       ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  Risultati: riquadro comandi hello Elenca hello cartelle e file per il percorso corrente hello.

       ![Data Lake Tools per elenco di codice di Visual Studio dal percorso corrente hello](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a>File di archiviazione hello anteprima
È possibile visualizzare l'anteprima di file di archiviazione hello tramite tavolozza comando hello o pulsante destro del mouse.

**file di archiviazione hello toopreview tramite tavolozza comando hello**

1.  Aprire il riquadro comandi hello (Ctrl + MAIUSC + P) e immettere **ADL: File di archiviazione di anteprima**.

       ![Anteprima dei file di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  Selezionare un account dal percorso locale hello o un account Data Lake Analitica.

       ![Elencare l'account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Selezionare **più** toolist ulteriori account Data Lake Analitica e quindi selezionare un account Data Lake Analitica.

       ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  Immettere un file o un percorso di archiviazione di Azure. Ad esempio /output/SearchLog.txt.

       ![Immissione di un file o percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  Risultati: tavolozza di hello comando Visualizza le informazioni di percorso hello in base ai valori immessi.

       ![Risultato del file di anteprima in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**percorso di archiviazione hello toolist tramite mouse**

1.  toopreview un file, fare clic sul percorso del file hello.

   ![Menu di scelta rapida di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  Selezionare un account dal percorso locale hello o un account Data Lake Analitica.

       ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Risultati: Codice di Visual Studio visualizza i risultati di anteprima hello del file hello.

       ![Risultato del file di anteprima in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>Caricare un file 

È possibile caricare file immettendo i comandi di hello **ADL: carica File** o **ADL: carica File tramite la configurazione**.

**file tooupload hello tuttavia ADL: il comando Carica File**
1. Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza o editor di script hello e quindi immettere **carica File**.
2.  hello tooupload file, immettere un percorso locale.

    ![Inserimento di un percorso locale in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. Selezionare uno dei modi hello del percorso di archiviazione hello elenco. Questo passaggio usa **Enter a path** (Immetti un percorso) come esempio.

    ![Elencare il percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- Codice di Visual Studio consente di mantenere percorso visitato ultimo hello ogni account Data Lake Analitica. Ad esempio /tt/ss.
    >- Browser dal percorso radice: percorso radice di elenco hello dall'account Data Lake Analitica selezionato o un percorso locale.
    >- Immettere un percorso: elencare un percorso specificato dall'account di Data Lake Analytics selezionato o un percorso locale.

4. Selezionare un account dal percorso locale hello o un account Data Lake Analitica.

    ![Archiviazione dal menu di scelta rapida in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. Immettere un percorso di archiviazione di Azure. Ad esempio /output.

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. Individuare il percorso di archiviazione di Azure. Selezionare **Choose current folder** (Scegli cartella corrente).

    ![Selezionare una cartella in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  Risultati: hello **Output** finestra viene visualizzato lo stato di caricamento file hello.

       ![Stato di caricamento in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**file tooupload hello tuttavia ADL: caricare File tramite il comando di configurazione**
1.  Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza o editor di script hello e quindi immettere **carica File tramite la configurazione**.
2.  VS Code visualizza un file JSON. È possibile immettere i percorsi di file e caricare più file hello contemporaneamente. Le istruzioni vengono visualizzate in hello **Output** finestra. file di hello il tooproceed tooupload, salvare file JSON di hello (Ctrl + S).

       ![Percorso del file in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  Risultati: hello **Output** finestra viene visualizzato lo stato di caricamento file hello.

       ![Stato di caricamento in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

Menu di scelta rapida nel percorso completo del file hello o percorso del file hello nell'editor di script hello un'altra tooupload modo consiste nell'utilizzare un toostorage file hello. Immettere il percorso di file locale hello e quindi selezionare account hello. Hello **Output** finestra Visualizza lo stato di caricamento hello. 

### <a name="open-azure-storage-explorer"></a>Aprire Azure Storage Explorer
È possibile aprire **Azure Storage Explorer** immettendo il comando hello **ADL: aprire Web Azure Storage Explorer** o selezionarlo dal menu di scelta rapida hello.

**tooopen Esplora archivi Azure**

1. Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.
2. Immettere **aprire Esplora risorse di archiviazione Azure Web** o fare clic su un percorso relativo o il percorso completo di hello nell'editor di script hello e quindi selezionare **aprire Esplora risorse di archiviazione Azure Web**.
3. Selezionare un account di Data Lake Analytics.

Data Lake Tools consente di aprire il percorso di archiviazione di Azure hello hello portale di Azure. È possibile trovare i file di hello di percorso e anteprima hello dal web hello.

### <a name="local-run-and-local-debug-for-windows-users"></a>Esecuzione e debug locale per utenti Windows
Esecuzione locale U-SQL verifica i dati locali e di convalidare lo script in locale, prima che il codice venga pubblicato tooData Lake Analitica. Hello consente di funzionalità di debug locale è toocomplete hello seguenti attività prima che il codice venga inviata Analitica tooData Lake: 
- Eseguire il debug del code-behind di C#. 
- Esaminare il codice hello. 
- Convalidare lo script in locale.

Per istruzioni sull'esecuzione e il debug locali, vedere [Esecuzione locale e debug locale di U-SQL con Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).

## <a name="additional-features"></a>Funzionalità aggiuntive

Data Lake Tools per Visual Studio Code supporta hello seguenti caratteristiche:

-   Completamento automatico di IntelliSense: vengono visualizzati suggerimenti in finestre popup intorno agli elementi, ad esempio parole chiave, metodi e variabili. Icone diverse rappresentano diversi tipi di oggetti hello:

    - Tipo di dati Scala
    - Tipo di dati complesso
    - UDT integrati
    - Raccolta e classi .NET
    - Espressioni C#
    - UDF, UDO e UDAAG di C# integrati 
    - Funzioni di U-SQL
    - Funzione di windowing di U-SQL
 
    ![Tipi di oggetto IntelliSense degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   IntelliSense, completamento automatico sui metadati Data Lake Analitica: Data Lake Tools Scarica hello Data Lake Analitica informazioni sui metadati in locale. funzionalità IntelliSense Hello popola automaticamente gli oggetti, inclusi database hello, schema, tabella, vista, funzione con valori di tabella, procedure e gli assembly c#, dai metadati Data Lake Analitica hello.
 
    ![Metadati IntelliSense degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   Indicatore di errore di IntelliSense: Data Lake Tools sottolinea hello U-SQL e c# per l'elaborazione degli errori. 
-   Caratteristiche salienti di sintassi: Data Lake Tools Usa elementi toodifferentiate colori diversi, ad esempio variabili, le parole chiave, il tipo di dati e funzioni. 

    ![Sintassi in evidenza degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>Passaggi successivi

- Per l'esecuzione e il debug locali di U-SQL con Visual Studio Code, vedere [Esecuzione locale e debug locale di U-SQL con Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).
- Per informazioni introduttive su Data Lake Analytics, vedere [Esercitazione: Introduzione a Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Per informazioni sull'uso degli strumenti di Data Lake per Visual Studio, vedere [Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Per informazioni sullo sviluppo di assembly, vedere [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Sviluppare assembly U-SQL per i processi di Azure Data Lake Analytics).



