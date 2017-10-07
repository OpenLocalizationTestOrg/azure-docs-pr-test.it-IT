---
title: App web aaaCreating con Django in Azure
description: Un'esercitazione che illustra toorunning un'app web Python nelle App Web di servizio App di Azure.
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a>Creazione di app Web con Django
Questa esercitazione viene descritto come tooget ha avviato l'esecuzione Python [App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714). Le app Web di Azure offrono hosting gratuito limitato e capacità di distribuzione rapida, oltre alla possibilità di utilizzare Python! Aumento delle dimensioni dell'app, è possibile passare toopaid hosting ed è inoltre possibile integrare con tutte hello altri servizi di Azure.

Si creerà un'applicazione tramite un framework web Django hello (vedere le versioni di questa esercitazione per [pallone](web-sites-python-create-deploy-flask-app.md) e [Bottle](web-sites-python-create-deploy-bottle-app.md)). Si crea app web hello da hello Azure Marketplace, configurare la distribuzione Git e clonare il repository hello in locale. Quindi verrà eseguito in locale un'applicazione hello, apportare modifiche, eseguire il commit e inviarli tooAzure. Hello esercitazione viene illustrato come toodo da Windows o Mac o Linux.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
* Windows, Mac o Linux
* Python 2.7 o 3.4
* setuptools, pip, virtualenv (solo Python 2.7)
* Git
* [Python Tools per Visual Studio][Python Tools per Visual Studio] (PTVS) - Nota: non è obbligatorio

**Nota**: la pubblicazione TFS non è attualmente supportata per progetti Python.

### <a name="windows"></a>Windows
Se non è già installato Python 2.7 o 3.4 (32 bit), si consiglia di installare [Azure SDK per Python 2.7] o [Azure SDK per Python 3.4] mediante Installazione guidata piattaforma Web. Versione a 32 bit hello di Python, setuptools, pip, virtualenv e così via (32 bit Python è ciò che viene installato nei computer host di Azure hello) vengono installati. In alternativa, è possibile ottenere Python da [python.org].

Per Git, è consigliabile [Git per Windows] o [GitHub per Windows]. Se si utilizza Visual Studio, è possibile utilizzare il supporto di Git hello integrato.

È inoltre consigliabile installare [Python Tools 2.2 per Visual Studio]. Questa operazione è facoltativa, ma se dispone di [Visual Studio], tra cui hello liberare Visual Studio Community 2013 o Visual Studio Express 2013 per Web, quindi si riceverà un ottimo dell'IDE Python.

### <a name="maclinux"></a>Mac/Linux
È necessario avere già installato Python e Git, ma assicurarsi di disporre di Python 2.7 o 3.4.

## <a name="web-app-creation-on-portal"></a>Creazione delle app Web sul portale
primo passaggio nella creazione dell'applicazione Hello è toocreate hello web app tramite hello [portale Azure](https://portal.azure.com).

1. Accedere al portale di Azure hello e fare clic su hello **NEW** pulsante nell'angolo inferiore sinistro di hello.
2. Nella casella di ricerca hello, digitare "python".
3. Nei risultati della ricerca hello, selezionare **Django** (pubblicato da PTVS), quindi fare clic su **crea**.
4. Configurare hello nuova Django app, ad esempio la creazione di un nuovo piano di servizio App e un nuovo gruppo di risorse per tale. Fare quindi clic su **Crea**.
5. Configurare la pubblicazione Git per l'app web appena creato seguendo le istruzioni di hello in [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Informazioni generali sull'applicazione
### <a name="git-repository-contents"></a>Contenuti del repository Git
Di seguito è riportata una panoramica dei file hello che si trova nell'archivio Git iniziale hello, che è possibile clonare nella sezione successiva hello.

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

Origini principali per l'applicazione hello. È composta da 3 pagine (indice, informazioni su, contatti) con un layout master. Il contenuto statico e gli script includono bootstrap, jquery, modernizr e respond.

    \manage.py

Gestione locale e supporto serve di sviluppo. Utilizzare questa applicazione hello toorun localmente, la sincronizzazione database hello e così via.

    \db.sqlite3

Database predefinito. Include le tabelle necessarie hello per toorun applicazione hello, ma non contiene tutti gli utenti (sincronizzazione hello database toocreate un utente).

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

File di progetto da utilizzare con [Python Tools per Visual Studio].

    \ptvs_virtualenv_proxy.py

Proxy IIS per ambienti virtuali e supporto del debug remoto PTVS.

    \requirements.txt

Pacchetti esterni necessari da parte di questa applicazione. script di distribuzione Hello verrà pip pacchetti hello installazione elencati in questo file.

    \web.2.7.config
    \web.3.4.config

File di configurazione IIS. script di distribuzione Hello verrà utilizzata web.x.y.config appropriato hello e copiarlo come Web. config.

### <a name="optional-files---customizing-deployment"></a>File facoltativi - Personalizzazione della distribuzione
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>File facoltativi - Runtime Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Altri file sul server
Alcuni file esistano nel server di hello ma non vengono aggiunti i repository git toohello. Vengono creati tramite script di distribuzione hello.

    \web.config

File di configurazione IIS. Creato da web.x.y.config per ogni distribuzione.

    \env\

Ambiente virtuale Python. Se un ambiente virtuale compatibile non esiste già nell'applicazione web hello, creato durante la distribuzione. I pacchetti elencati in requirements.txt sono pip installato, ma pip ignorerà l'installazione se sono già installati i pacchetti hello.

Hello accanto 3 sezioni descrivono come tooproceed con hello web lo sviluppo di app in ambienti diversi 3:

* Windows, con Python Tools per Visual Studio
* Windows, con la riga di comando
* Mac/Linux, con la riga di comando

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Sviluppo di siti Web - Windows - Python Tools per Visual Studio
### <a name="clone-hello-repository"></a>Repository di hello clone
In primo luogo, clonare il repository hello utilizzando URL hello fornito nel portale di Azure hello. Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).

Aprire il file di soluzione hello (con estensione sln) che è incluso nella directory radice del repository hello hello.

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a>Creare l'ambiente virtuale
A questo punto verrà creato un ambiente virtuale per lo sviluppo locale. Fare clic con il pulsante destro del mouse su **Python Environments** (Ambienti Python) e selezionare **Add Virtual Environment...** (Aggiungi ambiente virtuale...).

* Assicurarsi che il nome di hello dell'ambiente hello `env`.
* Selezionare l'interprete base hello. Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (runtime.txt o hello **le impostazioni dell'applicazione** pannello dell'app web nel portale di Azure hello).
* Verificare che sia selezionata hello opzione toodownload e installare i pacchetti.

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

Fare clic su **Crea**. Questo verrà crea ambiente virtuale hello e installare le dipendenze elencate in requirements.txt.

### <a name="create-a-superuser"></a>Creare un superuser
database Hello incluso in un'applicazione hello non dispone di un utente avanzato definito. Ordine toouse hello Accedi funzionalità di un'applicazione hello o dell'interfaccia di amministrazione di hello Django (se si decide di tooenable è), è necessario toocreate un utente avanzato.

Eseguire questo dalla hello della riga di comando dalla cartella del progetto:

    env\scripts\python manage.py createsuperuser

Seguire il nome utente hello di hello prompt tooset, password e così via.

### <a name="run-using-development-server"></a>Eseguire mediante il server di sviluppo
Premere F5 toostart debug e il browser verrà aperto automaticamente pagina toohello in esecuzione in locale.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

È possibile impostare i punti di interruzione in origini hello, utilizzare le finestre Espressioni di controllo hello e così via. Vedere hello [Python Tools per la documentazione di Visual Studio] per ulteriori informazioni su hello varie funzionalità.

### <a name="make-changes"></a>Apportare modifiche
Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.

Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a>Installare altri pacchetti
È possibile che l'applicazione disponga di dipendenze oltre a Python e Django.

È possibile installare altri pacchetti utilizzando pip. tooinstall un pacchetto, fare clic su ambiente virtuale hello e selezionare **Installa pacchetto Python**.

Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi di Azure, immettere `azure`:

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

Fare clic sull'ambiente virtuale hello e selezionare **generare requirements.txt** tooupdate requirements.txt.

Quindi, eseguire il commit del repository Git di hello modifiche toorequirements.txt toohello.

### <a name="deploy-tooazure"></a>Distribuire tooAzure
tootrigger una distribuzione, fare clic su **sincronizzazione** o **Push**. La sincronizzazione esegue sia il push che il pull.

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

prima distribuzione Hello richiederà del tempo, come verrà creato un ambiente virtuale, pacchetti di installazione e così via.

Visual Studio non viene visualizzato lo stato di hello della distribuzione hello. Se si desidera l'output di hello tooreview, vedere la sezione hello [Troubleshooting - distribuzione](#troubleshooting-deployment).

Sfoglia toohello URL Azure tooview le modifiche.

## <a name="web-app-development---windows---command-line"></a>Sviluppo di siti Web - Windows - Riga di comando
### <a name="clone-hello-repository"></a>Repository di hello clone
In primo luogo, clonare il repository di hello tramite URL hello fornito nel portale di Azure hello e aggiungere hello Azure repository come remota. Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a>Creare l'ambiente virtuale
Si creerà un nuovo ambiente virtuale per scopi di sviluppo (non aggiungerlo toohello repository). Gli ambienti virtuali in Python non sono rilocabile, pertanto ogni sviluppatore che lavora in un'applicazione hello creerà i propri localmente.

Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (nel pannello Impostazioni applicazione runtime.txt o hello dell'app web nel portale di Azure hello).

Per Python 2.7:

    c:\python27\python.exe -m virtualenv env

Per Python 3.4:

    c:\python34\python.exe -m venv env

Installare tutti i pacchetti esterni richiesti dall'applicazione. È possibile utilizzare file requirements.txt hello radice hello pacchetti hello tooinstall del repository hello nell'ambiente virtuale:

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a>Creare un superuser
database Hello incluso in un'applicazione hello non dispone di un utente avanzato definito. Ordine toouse hello Accedi funzionalità di un'applicazione hello o dell'interfaccia di amministrazione di hello Django (se si decide di tooenable è), è necessario toocreate un utente avanzato.

Eseguire questo dalla hello della riga di comando dalla cartella del progetto:

    env\scripts\python manage.py createsuperuser

Seguire il nome utente hello di hello prompt tooset, password e così via.

### <a name="run-using-development-server"></a>Eseguire mediante il server di sviluppo
È possibile avviare un'applicazione hello in un server di sviluppo con hello comando seguente:

    env\scripts\python manage.py runserver

console Hello verrà visualizzato l'URL di hello e server hello porte in ascolto:

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

Quindi, aprire l'URL di web browser toothat.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a>Apportare modifiche
Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.

Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Installare altri pacchetti
È possibile che l'applicazione disponga di dipendenze oltre a Python e Django.

È possibile installare altri pacchetti utilizzando pip. Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi Azure, digitare:

    env\scripts\pip install azure

Verificare che tooupdate requirements.txt:

    env\scripts\pip freeze > requirements.txt

Eseguire il commit delle modifiche hello:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Distribuire tooAzure
una distribuzione tootrigger, hello push modifica tooAzure:

    git push azure master

Verrà visualizzato un output di hello dello script di distribuzione hello, inclusa la creazione di un ambiente virtuale, installazione dei pacchetti, la creazione di Web. config.

Sfoglia toohello URL Azure tooview le modifiche.

## <a name="web-app-development---maclinux---command-line"></a>Sviluppo del sito Web - Mac/Linux - Riga di comando
### <a name="clone-hello-repository"></a>Repository di hello clone
In primo luogo, clonare il repository di hello tramite URL hello fornito nel portale di Azure hello e aggiungere hello Azure repository come remota. Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a>Creare l'ambiente virtuale
Si creerà un nuovo ambiente virtuale per scopi di sviluppo (non aggiungerlo toohello repository). Gli ambienti virtuali in Python non sono rilocabile, pertanto ogni sviluppatore che lavora in un'applicazione hello creerà i propri localmente.

Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (nel pannello Impostazioni applicazione runtime.txt o hello dell'app web nel portale di Azure hello).

Per Python 2.7:

    python -m virtualenv env

Per Python 3.4:

    python -m venv env

oppure

    pyvenv env

Installare tutti i pacchetti esterni richiesti dall'applicazione. È possibile utilizzare file requirements.txt hello radice hello pacchetti hello tooinstall del repository hello nell'ambiente virtuale:

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a>Creare un superuser
database Hello incluso in un'applicazione hello non dispone di un utente avanzato definito. Ordine toouse hello Accedi funzionalità di un'applicazione hello o dell'interfaccia di amministrazione di hello Django (se si decide di tooenable è), è necessario toocreate un utente avanzato.

Eseguire questo dalla hello della riga di comando dalla cartella del progetto:

    env/bin/python manage.py createsuperuser

Seguire il nome utente hello di hello prompt tooset, password e così via.

### <a name="run-using-development-server"></a>Eseguire mediante il server di sviluppo
È possibile avviare un'applicazione hello in un server di sviluppo con hello comando seguente:

    env/bin/python manage.py runserver

console Hello verrà visualizzato l'URL di hello e server hello porte in ascolto:

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

Quindi, aprire l'URL di web browser toothat.

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a>Apportare modifiche
Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.

Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Installare altri pacchetti
È possibile che l'applicazione disponga di dipendenze oltre a Python e Django.

È possibile installare altri pacchetti utilizzando pip. Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi Azure, digitare:

    env/bin/pip install azure

Verificare che tooupdate requirements.txt:

    env/bin/pip freeze > requirements.txt

Eseguire il commit delle modifiche hello:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Distribuire tooAzure
una distribuzione tootrigger, hello push modifica tooAzure:

    git push azure master

Verrà visualizzato un output di hello dello script di distribuzione hello, inclusa la creazione di un ambiente virtuale, installazione dei pacchetti, la creazione di Web. config.

Sfoglia toohello URL Azure tooview le modifiche.

## <a name="troubleshooting---package-installation"></a>Risoluzione dei problemi - Installazione dei pacchetti
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Risoluzione dei problemi - Ambiente virtuale
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a>Risoluzione dei problemi - File statici
Django esiste il concetto di hello di raccolta dei file statici. Questo accetta tutti i file statici hello dal percorso originale e li copia tooa unica cartella. Per questa applicazione, vengono copiati troppo`/static`.

Tale operazione viene eseguita perché i file statici possono provenire da Django diversi. Ad esempio, i file statici hello dalle interfacce di amministrazione di hello Django si trovano in una sottocartella della libreria Django nell'ambiente virtuale hello. I file statici definiti da questa applicazione si trovano in `/app/static`. Quando si usano più framework Django, i file statici saranno ubicati in più punti.

Quando si esegue un'applicazione hello in modalità di debug, un'applicazione hello fornisce i file statici hello nei percorsi originali.

Quando si esegue un'applicazione hello in modalità di rilascio, applicazione di hello esegue **non** utilizzati file statici hello. È responsabilità di hello di hello tooserve hello dei file server web. Per questa applicazione, IIS servirà hello file statici `/static`.

raccolta di Hello dei file statici viene eseguita automaticamente come file di parte dello script di distribuzione hello, cancellazione raccolti in precedenza. Ciò significa hello raccolta viene eseguita in tutte le distribuzioni, rallentando di distribuzione, ma garantisce che i file obsoleti non saranno disponibili, evitare un potenziale problema di sicurezza.

Se si desidera tooskip raccolta dei file statici per l'applicazione Django:

    \.skipDjango

Sarà necessaria insieme hello toodo manualmente nel computer locale:

    env\scripts\python manage.py collectstatic

Quindi rimuovere hello `\static` cartella `.gitignore` e aggiungerlo repository Git toohello.

## <a name="troubleshooting---settings"></a>Risoluzione dei problemi - Impostazioni
Varie impostazioni per un'applicazione hello possono essere modificate in `DjangoWebProject/settings.py`.

La modalità di debug è abilitata per la comodità dello sviluppatore. Uno degli effetti collaterali nice di che è che sarà in grado di toosee immagini e altri contenuti statici durante l'esecuzione in locale, senza che sia file statici toocollect.

modalità di debug toodisable:

    DEBUG = False

Quando il debug è disabilitato, hello valore per `ALLOWED_HOSTS` toobe esigenze aggiornato nome host di Azure di tooinclude hello. ad esempio:

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

tooenable o qualsiasi:

    ALLOWED_HOSTS = (
        '*',
    )

In pratica, è opportuno toodo qualcosa toodeal più complesse con il passaggio tra debug e rilascio modalità e ottenere il nome host hello.

È possibile impostare le variabili di ambiente tramite il portale di Azure hello **configura** pagina hello **impostazioni app** sezione.  Questo può essere utile per impostare i valori non è possibile tooappear nelle origini hello (le stringhe di connessione, le password e così via) o che si desidera tooset in modo diverso tra Azure e nel computer locale. In `settings.py`, è possibile eseguire una query utilizzando le variabili di ambiente hello `os.getenv`.

## <a name="using-a-database"></a>Utilizzo di un database
database Hello è incluso in un'applicazione hello è un database sqlite. Si tratta di un toouse database predefinito semplice e utile per lo sviluppo, poiché non richiede quasi alcuna installazione. database di Hello è archiviato nel file db.sqlite3 hello nella cartella di progetto hello.

Azure offre servizi di database che sono di facile toouse da un'applicazione Django. Esercitazioni per l'utilizzo di [Database SQL] e [MySQL] da un'applicazione Django Mostra passaggi hello servizio di database hello toocreate necessario, modificare le impostazioni di database hello in `DjangoWebProject/settings.py`, hello e le librerie necessarie tooinstall.

Naturalmente, se si preferiscono toomanage i server di database, è possibile eseguire utilizzando Windows o Linux macchine virtuali in esecuzione in Azure.

## <a name="django-admin-interface"></a>Interfaccia di amministrazione di Django
Una volta avviata la creazione dei modelli, è opportuno database hello toopopulate con alcuni dati. Un modo semplice toodo aggiungere e modificare in modo interattivo il contenuto è l'interfaccia di amministrazione di toouse hello Django.

commento di codice Hello per interfaccia di amministrazione di hello in origini dell'applicazione hello, ma è contrassegnato chiaramente in modo è possibile abilitare facilmente il (ricerca di 'admin').

Dopo averlo abilitato, sincronizzare database hello, eseguire un'applicazione hello e passare troppo`/admin`.

## <a name="next-steps"></a>Passaggi successivi
Seguire questi toolearn collegamenti ulteriori sui Django e gli strumenti Python per Visual Studio:

* [Documentazione di Django]
* [Python Tools per la documentazione di Visual Studio]

Per informazioni sull'utilizzo di Database SQL e MySQL:

* [Django e MySQL in Azure con Python Tools per Visual Studio]
* [Django e database SQL in Azure con Python Tools per Visual Studio]

Per ulteriori informazioni, vedere hello [Centro per sviluppatori Python](/develop/python/).

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Django e MySQL in Azure con Python Tools per Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django e database SQL in Azure con Python Tools per Visual Studio]: web-sites-python-ptvs-django-sql.md
[Database SQL]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

<!--External Link references-->
[Azure SDK per Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK per Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git per Windows]: http://msysgit.github.io/
[GitHub per Windows]: https://windows.github.com/
[Python Tools per Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Python Tools per la documentazione di Visual Studio]: http://aka.ms/ptvsdocs
[Documentazione di Django]: https://www.djangoproject.com/
