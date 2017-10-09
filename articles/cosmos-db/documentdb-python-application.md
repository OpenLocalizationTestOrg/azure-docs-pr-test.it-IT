---
title: esercitazione di applicazione web pallone aaaPython per Azure Cosmos DB | Documenti Microsoft
description: Esaminare un'esercitazione database sull'uso di Azure Cosmos DB toostore e accedere ai dati da un'applicazione web di Python pallone ospitato in Azure. Trovare soluzioni di sviluppo dell'applicazione.
keywords: Sviluppo di applicazioni, Python Flask, applicazione Web Python, sviluppo Web Python
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a>Creare un'applicazione Web Python Flask con Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.JS](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

In questa esercitazione Mostra come toouse Azure Cosmos DB toostore e accedere ai dati da un Python web applicazione ospitata in Azure e si presuppongono di aver esperienza precedente usando Python e siti Web di Azure.

In questa esercitazione del database vengono trattati i seguenti argomenti:

1. Creazione e provisioning di un account Cosmos DB.
2. Creazione di un'applicazione Python Flask.
3. Connessione tooand utilizzando Cosmos DB dall'applicazione web.
4. Distribuzione hello tooAzure di applicazione web.

Seguendo questa esercitazione, si creerà una semplice applicazione di voto che consente di toovote per un sondaggio.

![Cattura di schermata dell'applicazione di voto hello creata da questa esercitazione database](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a>Prerequisiti per l'esercitazione del database
Prima di seguire le istruzioni di hello in questo articolo, è necessario assicurarsi di aver installato quanto segue hello:

* Un account Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
 
    OPPURE 

    Un'installazione locale di hello [emulatore di Azure Cosmos DB](local-emulator.md).
* [Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).  
* [Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).  
* [Microsoft Azure SDK per Python 2.7](https://azure.microsoft.com/downloads/). 
* [Python 2.7.13](https://www.python.org/downloads/windows/). 

> [!IMPORTANT]
> Se si sta installando Python 2.7 hello per la prima volta, assicurarsi che nella schermata di Python personalizzare 2.7.13 hello, selezionare **aggiungere python.exe tooPath**.
> 
> ![Cattura di schermata della schermata di Python personalizzare 2.7.11 hello, in cui è necessario tooselect Aggiungi python.exe tooPath](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* [Compilatore Microsoft Visual C++ per Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a>Passaggio 1: Creare un account del database di Azure Cosmos DB
Creare prima di tutto un account Cosmos DB. Se è già un account o se si utilizza hello Azure Cosmos DB emulatore per questa esercitazione, è possibile ignorare troppo[passaggio 2: creare una nuova applicazione web Python pallone](#step-2-create-a-new-python-flask-web-application).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
È ora verrà illustrata la modalità messa a terra toocreate una nuova applicazione web di Python pallone da hello.

## <a name="step-2-create-a-new-python-flask-web-application"></a>Passaggio 2: Creare una nuova applicazione Web Python Flask
1. In Visual Studio, su hello **File** menu, scegliere troppo**New**e quindi fare clic su **progetto**.
   
    Hello **nuovo progetto** viene visualizzata la finestra di dialogo.
2. Nel riquadro sinistro hello espandere **modelli** e quindi **Python**, quindi fare clic su **Web**. 
3. Selezionare **progetto Web pallone** nel riquadro centrale hello, quindi nell'hello **nome** digitare **esercitazione**e quindi fare clic su **OK**. Tenere presente che i nomi di pacchetto di Python devono essere tutti in lettere minuscole, come descritto in hello [Guida di stile per il codice Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).
   
    Per tali nuovi tooPython pallone, è un framework di sviluppo di applicazioni web che consente di compilare applicazioni web in Python più velocemente.
   
    ![Cattura di schermata della finestra Nuovo progetto hello in Visual Studio con Python evidenziato nella finestra di sinistra, Python pallone Web progetto selezionato in intermedio hello ed esercitazione nome hello nella casella Nome hello hello](./media/documentdb-python-application/image9.png)
4. In hello **Python Tools per Visual Studio** finestra, fare clic su **installare in un ambiente virtuale**. 
   
    ![Cattura di schermata dell'esercitazione database hello - Python Tools per la finestra di Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. In hello **aggiungere ambiente virtuale** finestra, è possibile accettare le impostazioni predefinite hello e utilizzare Python 2.7 ambiente base hello PyDocumentDB supporta attualmente Python 3. x e quindi fare clic su **crea**. Viene impostata l'ambiente virtuale di Python hello necessario per il progetto.
   
    ![Cattura di schermata dell'esercitazione database hello - Python Tools per la finestra di Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    Visualizza finestra di output di Hello `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` quando ambiente hello è stato installato correttamente.

## <a name="step-3-modify-hello-python-flask-web-application"></a>Passaggio 3: Modificare un'applicazione web Python pallone hello
### <a name="add-hello-python-flask-packages-tooyour-project"></a>Aggiungere hello Python pallone pacchetti tooyour progetto
Una volta configurato il progetto, è necessario tooadd hello necessario pallone pacchetti tooyour progetto, inclusi pydocumentdb, pacchetto di Python hello per DocumentDB.

1. In Esplora soluzioni, aprire il file hello denominato **requirements.txt** e sostituire il contenuto di hello con hello seguente:
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. Salvare hello **requirements.txt** file. 
3. In Esplora soluzioni fare clic con il pulsante destro del mouse su **env** e scegliere **Install from requirements.txt**.
   
    ![Cattura di schermata che mostra env (Python 2.7) selezionato con l'installazione da requirements.txt evidenziato nell'elenco di hello](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    Al termine dell'installazione, finestra di output di hello Visualizza seguente hello:
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > In rari casi, è possibile visualizzare un errore nella finestra di output di hello. In tal caso, controllare se l'errore hello è toocleanup correlati. Talvolta pulizia hello ha esito negativo, ma sarà comunque possibile eseguire installazione di hello (scorrere verso l'alto tooverify finestra output di hello questo). È possibile verificare l'installazione da [ambiente virtuale di verifica hello](#verify-the-virtual-environment). Se hello installazione non è riuscita ma hello verifica ha esito positivo, è toocontinue OK.
   > 
   > 

### <a name="verify-hello-virtual-environment"></a>Verificare l'ambiente virtuale hello
È importante verificare che tutto sia installato correttamente.

1. Compilare la soluzione hello premendo **Ctrl**+**MAIUSC**+**B**.
2. Al termine della compilazione hello, avviare il sito Web di hello premendo **F5**. Verrà avviato il server di sviluppo pallone hello e avvia il browser web. Dovrebbe essere hello dopo.
   
    ![Hello Python pallone progetto web vuoto sviluppo visualizzato in un browser](./media/documentdb-python-application/image12.png)
3. Arrestare il debug del sito Web hello premendo **MAIUSC**+**F5** in Visual Studio.

### <a name="create-database-collection-and-document-definitions"></a>Creare definizioni di database, raccolta e documento
Ora viene creata l'applicazione di voto aggiungendo nuovi file e aggiornandone altri.

1. In Esplora soluzioni fare doppio clic su hello **esercitazione** del progetto, fare clic su **Aggiungi**, quindi fare clic su **nuovo elemento**. Selezionare **File Python vuoto** e nome file di hello **forms.py**.  
2. Aggiungere i seguenti file di codice toohello forms.py hello e quindi salvare il file hello.

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a>Aggiungere tooviews.py importazioni hello richiesto
1. In Esplora soluzioni espandere hello **esercitazione** cartella e aprire hello **views.py** file. 
2. Aggiungere hello dopo l'importazione istruzioni toohello cima hello **views.py** file, quindi salvare il file hello. Questi importare Cosmos DB PythonSDK e hello pacchetti pallone.
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a>Creare il database, la raccolta e il documento
* Ancora in **views.py**, aggiungere hello successivo toohello codice alla fine del file hello. Questo si occupa di creazione del database hello utilizzato dal modulo hello. Non eliminare il codice esistente in hello **views.py**. Consente di accodare questo fine toohello.

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a>Leggere il database, la raccolta e il documento e inviare il form
* Ancora in **views.py**, aggiungere hello successivo toohello codice alla fine del file hello. Questo si occupa della configurazione di modulo hello, la lettura di documenti, raccolta e database hello. Non eliminare il codice esistente in hello **views.py**. Consente di accodare questo fine toohello.

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a>Creare hello file HTML
1. In Esplora soluzioni, in hello **esercitazione** cartella, a destra fare clic su hello **modelli** cartella, fare clic su **Aggiungi**, quindi fare clic su **nuovo elemento**. 
2. Selezionare **pagina HTML**e quindi nella casella digitare nome di hello **create.html**. 
3. Ripetere i passaggi 1 e 2 toocreate due altri file HTML: results.html e vote.html.
4. Aggiungere hello seguente codice troppo**create.html** in hello `<body>` elemento. Consente di visualizzare un messaggio che comunica l'avvenuta creazione di un nuovo database, di una raccolta e di un documento.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. Aggiungere hello seguente codice troppo**results.html** in hello `<body`> elemento. Visualizza risultati hello di polling hello.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. Aggiungere hello seguente codice troppo**vote.html** in hello `<body`> elemento. Visualizza il polling di hello e accetta hello voti. Registrazione voti hello, controllo hello viene passato tramite tooviews.py in cui verrà riconoscere hello voto cast e aggiungere il documento hello conseguenza.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. In hello **modelli** Sostituisci hello contenuto della cartella **index.html** con seguenti hello. Funge da hello pagina per l'applicazione di destinazione.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a>Aggiungere un file di configurazione e modificare hello \_ \_init\_\_. py.
1. In Esplora soluzioni fare doppio clic su hello **esercitazione** del progetto, fare clic su **Aggiungi**, fare clic su **nuovo elemento**selezionare **File Python vuoto**e quindi file con nome hello **config.py**. Questo file config è necessario per i moduli in Flask. È possibile utilizzarlo tooprovide anche una chiave privata. Tale chiave non sarà tuttavia necessaria per questa esercitazione.
2. Aggiungere il seguente hello tooconfig.py di codice, è necessario valori hello tooalter di **DOCUMENTDB\_HOST** e **DOCUMENTDB\_chiave** nel passaggio successivo hello.
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. In hello [portale di Azure](https://portal.azure.com/), passare toohello **chiavi** pannello facendo **Sfoglia**, **gli account di Azure Cosmos DB**, fare doppio clic sul nome hello di hello toouse dell'account e quindi fare clic su hello **chiavi** pulsante hello **Essentials** area. In hello **chiavi** blade, hello copia **URI** valore e incollarlo in hello **config.py** file, come valore hello hello **DOCUMENTDB\_HOST**  proprietà. 
4. Nel portale di Azure in hello hello **chiavi** pannello hello copia valore hello **chiave primaria** o hello **chiave secondaria**e incollarlo in hello **config.py**  file, come valore hello hello **DOCUMENTDB\_chiave** proprietà.
5. In hello  **\_ \_init\_\_py** file, aggiungere hello successiva riga. 
   
        app.config.from_object('config')
   
    In modo che il contenuto del file hello hello è:
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. Dopo avere aggiunto tutti i file hello, Esplora soluzioni dovrebbe essere simile al seguente:
   
    ![Cattura di schermata della finestra Esplora soluzioni di Visual Studio hello](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a>Passaggio 4: Esecuzione dell'applicazione Web in locale
1. Compilare la soluzione hello premendo **Ctrl**+**MAIUSC**+**B**.
2. Al termine della compilazione hello, avviare il sito Web di hello premendo **F5**. Esempio hello dovrebbe sullo schermo.
   
    ![Cattura di schermata della hello Python + Cosmos DB voto applicazione Azure visualizzata in un web browser](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. Fare clic su **creazione e la cancellazione hello voto Database** database hello toogenerate.
   
    ![Cattura di schermata della hello crea una pagina dell'applicazione web hello-informazioni sullo sviluppo](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. Fare quindi clic su **Voto** e selezionare un'opzione.
   
    ![Cattura di schermata dell'applicazione web hello una domanda voto poste](./media/documentdb-python-application/cosmos-db-vote.png)
5. Per ogni voto che si esegue il cast, incrementa il numero appropriato di hello.
   
    ![Cattura di schermata dei risultati della pagina di voto hello illustrato hello](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. Arrestare il debug di progetti hello premendo MAIUSC + F5.

## <a name="step-5-deploy-hello-web-application-tooazure"></a>Passaggio 5: Distribuire hello web applicazione tooAzure
Dopo aver creato un'applicazione completa hello funziona correttamente con DB Cosmos, verrà toodeploy questo tooAzure.

1. Progetto hello pulsante destro del mouse in Esplora soluzioni (assicurarsi che non si è ancora in esecuzione, in locale) e selezionare **pubblica**.  
   
     ![Cattura di schermata dell'esercitazione hello selezionato in Esplora soluzioni, con l'opzione pubblica hello evidenziato](./media/documentdb-python-application/image20.png)
2. In hello **pubblica** nella finestra di dialogo **servizio App di Microsoft Azure**selezionare **Crea nuovo**, quindi fare clic su **pubblica**.
   
    ![Cattura di schermata della finestra di hello pubblica sul Web con Microsoft Azure App Service evidenziato](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. In hello **Crea servizio App** finestra di dialogo immettere il nome di hello per le app web con il **sottoscrizione**, **gruppo di risorse**, e **piano di servizio App** , quindi fare clic su **crea**.
   
    ![Cattura di schermata della finestra di hello finestra App Web di Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. Dopo alcuni secondi, Visual Studio completerà la pubblicazione del servizio app e avvierà un browser in cui sarà possibile osservare il proprio lavoro in esecuzione in Azure.

    ![Cattura di schermata della finestra di hello finestra App Web di Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se si tratta di hello prima applicazione Python è stato eseguito nel computer, verificare che segue hello nella variabile di percorso sono inclusi cartelle (o percorsi di installazione equivalente hello):

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

Se si riceve un errore nella pagina del voto e si nome progetto diverso da **esercitazione**, assicurarsi che  **\_ \_init\_\_py** riferimenti hello Nome progetto corretto nella riga hello: `import tutorial.view`.

## <a name="next-steps"></a>Passaggi successivi
Congratulazioni. Solo avere completato la prima applicazione web di Python usando DB Cosmos e pubblicarlo tooAzure.

Questo argomento viene aggiornato e migliorato spesso in base al feedback degli utenti.  Una volta completati esercitazione hello utilizzando hello voto pulsanti hello superiore e inferiore di questa pagina ed essere tooinclude che commenti e suggerimenti su quali miglioramenti si desidera toosee apportate. Se desideri toocontact direttamente, ritieni libero tooinclude posta nei commenti.

applicazione web tooyour con funzionalità aggiuntive di tooadd, revisione hello API disponibili in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).

Per ulteriori informazioni su Azure, Visual Studio e Python, vedere hello [Centro per sviluppatori Python](https://azure.microsoft.com/develop/python/). 

Per ulteriori esercitazioni pallone Python, vedere [hello pallone Mega-esercitazione, Part i: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
