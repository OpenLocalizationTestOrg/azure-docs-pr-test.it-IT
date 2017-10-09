---
title: App web aaaCreating con pallone in Azure
description: Un'esercitazione che illustra toorunning un'app web Python in Azure.
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a>Creazione di app Web con Flask in Azure
In questa esercitazione descrive la modalità di avvio in esecuzione Python in tooget [App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).  Le app Web di Azure offrono hosting gratuito limitato e capacità di distribuzione rapida, oltre alla possibilità di utilizzare Python!  Aumento delle dimensioni dell'app, è possibile passare toopaid hosting ed è inoltre possibile integrare con tutte hello altri servizi di Azure.

Si creerà un'applicazione tramite un framework web pallone hello (vedere le versioni di questa esercitazione per [Django](web-sites-python-create-deploy-django-app.md) e [Bottle](web-sites-python-create-deploy-bottle-app.md)).  Si crea sito Web di hello dalla raccolta di Azure hello, configurare la distribuzione Git e clonare il repository hello in locale.  Quindi verrà eseguito in locale un'applicazione hello, apportare modifiche, eseguire il commit e inviarli tooAzure.  Hello esercitazione viene illustrato come toodo da Windows o Mac o Linux.

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
Se non è già installato Python 2.7 o 3.4 (32 bit), si consiglia di installare [Azure SDK per Python 2.7] o [Azure SDK per Python 3.4] mediante Installazione guidata piattaforma Web.  Versione a 32 bit hello di Python, setuptools, pip, virtualenv e così via (32 bit Python è ciò che viene installato nei computer host di Azure hello) vengono installati.  In alternativa, è possibile ottenere Python da [python.org].

Per Git, è consigliabile [Git per Windows] o [GitHub per Windows].  Se si utilizza Visual Studio, è possibile utilizzare il supporto di Git hello integrato.

È inoltre consigliabile installare [Python Tools 2.2 per Visual Studio].  Questa operazione è facoltativa, ma se dispone di [Visual Studio], tra cui hello liberare Visual Studio Community 2013 o Visual Studio Express 2013 per Web, quindi si riceverà un ottimo dell'IDE Python.

### <a name="maclinux"></a>Mac/Linux
È necessario avere già installato Python e Git, ma assicurarsi di disporre di Python 2.7 o 3.4.

## <a name="web-app-create-on-hello-azure-portal"></a>Creare app Web nel portale di Azure hello
primo passaggio nella creazione dell'applicazione Hello è toocreate hello web app tramite hello [portale Azure](https://portal.azure.com). 

1. Accedere al portale di Azure hello e fare clic su hello **NEW** pulsante nell'angolo inferiore sinistro di hello. 
2. Fare clic su **Web e dispositivi mobili**.
3. Nella casella di ricerca hello, digitare "python".
4. Nei risultati della ricerca hello, selezionare **pallone**, quindi fare clic su **crea**.
5. Configurare hello nuova pallone app, ad esempio la creazione di un nuovo piano di servizio App e un nuovo gruppo di risorse per tale. Fare quindi clic su **Crea**.
6. Configurare la pubblicazione Git per l'app web appena creato seguendo le istruzioni di hello in [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Informazioni generali sull'applicazione
### <a name="git-repository-contents"></a>Contenuti del repository Git
Di seguito è riportata una panoramica dei file hello che si trova nell'archivio Git iniziale hello, che è possibile clonare nella sezione successiva hello.

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

Origini principali per l'applicazione hello.  È composta da 3 pagine (indice, informazioni su, contatti) con un layout master.  Il contenuto statico e gli script includono bootstrap, jquery, modernizr e respond.

    \runserver.py

Supporto del server di sviluppo locale. Utilizzare questa applicazione hello toorun localmente.

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

File di progetto da utilizzare con [Python Tools per Visual Studio].

    \ptvs_virtualenv_proxy.py

Proxy IIS per ambienti virtuali e supporto del debug remoto PTVS.

    \requirements.txt

Pacchetti esterni necessari da parte di questa applicazione. script di distribuzione Hello verrà pip pacchetti hello installazione elencati in questo file.

    \web.2.7.config
    \web.3.4.config

File di configurazione IIS.  script di distribuzione Hello verrà utilizzata web.x.y.config appropriato hello e copiarlo come Web. config.

### <a name="optional-files---customizing-deployment"></a>File facoltativi - Personalizzazione della distribuzione
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>File facoltativi - Runtime Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Altri file sul server
Alcuni file esistano nel server di hello ma non vengono aggiunti i repository git toohello.  Vengono creati tramite script di distribuzione hello.

    \web.config

File di configurazione IIS.  Creato da web.x.y.config per ogni distribuzione.

    \env\

Ambiente virtuale Python.  Se un ambiente virtuale compatibile non esiste già nell'applicazione hello, creato durante la distribuzione.  I pacchetti elencati in requirements.txt sono pip installato, ma pip ignorerà l'installazione se sono già installati i pacchetti hello.

Hello accanto 3 sezioni descrivono come tooproceed con hello web lo sviluppo di app in ambienti diversi 3:

* Windows, con Python Tools per Visual Studio
* Windows, con la riga di comando
* Mac/Linux, con la riga di comando

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Sviluppo di siti Web - Windows - Python Tools per Visual Studio
### <a name="clone-hello-repository"></a>Repository di hello clone
In primo luogo, clonare il repository hello utilizzando URL hello fornito nel portale di Azure hello. Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).

Aprire il file di soluzione hello (con estensione sln) che è incluso nella directory radice del repository hello hello.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a>Creare l'ambiente virtuale
A questo punto verrà creato un ambiente virtuale per lo sviluppo locale.  Fare clic con il pulsante destro del mouse su **Python Environments** (Ambienti Python) e selezionare **Add Virtual Environment...** (Aggiungi ambiente virtuale...).

* Assicurarsi che il nome di hello dell'ambiente hello `env`.
* Selezionare l'interprete base hello.  Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (runtime.txt o hello **le impostazioni dell'applicazione** pannello dell'app web nel portale di Azure hello).
* Verificare che sia selezionata hello opzione toodownload e installare i pacchetti.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

Fare clic su **Crea**.  Questo verrà crea ambiente virtuale hello e installare le dipendenze elencate in requirements.txt.

### <a name="run-using-development-server"></a>Eseguire mediante il server di sviluppo
Premere F5 toostart debug e il browser verrà aperto automaticamente pagina toohello in esecuzione in locale.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

È possibile impostare i punti di interruzione in origini hello, utilizzare le finestre Espressioni di controllo hello e così via.  Vedere hello [Python Tools per la documentazione di Visual Studio] per ulteriori informazioni su hello varie funzionalità.

### <a name="make-changes"></a>Apportare modifiche
Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.

Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a>Installare altri pacchetti
L'applicazione potrebbe avere dipendenze oltre Python e Flask.

È possibile installare altri pacchetti utilizzando pip.  tooinstall un pacchetto, fare clic su ambiente virtuale hello e selezionare **Installa pacchetto Python**.

Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi di Azure, immettere `azure`:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

Fare clic sull'ambiente virtuale hello e selezionare **generare requirements.txt** tooupdate requirements.txt.

Quindi, eseguire il commit del repository Git di hello modifiche toorequirements.txt toohello.

### <a name="deploy-tooazure"></a>Distribuire tooAzure
tootrigger una distribuzione, fare clic su **sincronizzazione** o **Push**.  La sincronizzazione esegue sia il push che il pull.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

prima distribuzione Hello richiederà del tempo, come verrà creato un ambiente virtuale, pacchetti di installazione e così via.

Visual Studio non viene visualizzato lo stato di hello della distribuzione hello.  Se si desidera l'output di hello tooreview, vedere la sezione hello [Troubleshooting - distribuzione](#troubleshooting-deployment).

Sfoglia toohello URL Azure tooview le modifiche.

## <a name="web-app-development---windows---command-line"></a>Sviluppo di siti Web - Windows - Riga di comando
### <a name="clone-hello-repository"></a>Repository di hello clone
In primo luogo, clonare il repository di hello tramite URL hello fornito nel portale di Azure hello e aggiungere hello Azure repository come remota. Per ulteriori informazioni, vedere [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Creare l'ambiente virtuale
Si creerà un nuovo ambiente virtuale per scopi di sviluppo (non aggiungerlo toohello repository).  Gli ambienti virtuali in Python non sono rilocabile, pertanto ogni sviluppatore che lavora in un'applicazione hello creerà i propri localmente.

Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (runtime.txt o hello **le impostazioni dell'applicazione** pannello dell'app web nel portale di Azure hello).

Per Python 2.7:

    c:\python27\python.exe -m virtualenv env

Per Python 3.4:

    c:\python34\python.exe -m venv env

Installare tutti i pacchetti esterni richiesti dall'applicazione. È possibile utilizzare file requirements.txt hello radice hello pacchetti hello tooinstall del repository hello nell'ambiente virtuale:

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>Eseguire mediante il server di sviluppo
È possibile avviare un'applicazione hello in un server di sviluppo con hello comando seguente:

    env\scripts\python runserver.py

console Hello verrà visualizzato l'URL di hello e server hello porte in ascolto:

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

Quindi, aprire l'URL di web browser toothat.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a>Apportare modifiche
Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.

Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Installare altri pacchetti
L'applicazione potrebbe avere dipendenze oltre Python e Flask.

È possibile installare altri pacchetti utilizzando pip.  Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi Azure, digitare:

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
Si creerà un nuovo ambiente virtuale per scopi di sviluppo (non aggiungerlo toohello repository).  Gli ambienti virtuali in Python non sono rilocabile, pertanto ogni sviluppatore che lavora in un'applicazione hello creerà i propri localmente.

Assicurarsi che toouse hello stessa versione di Python selezionato per l'app web (runtime.txt o hello **le impostazioni dell'applicazione** pannello dell'app web nel portale di Azure hello).

Per Python 2.7:

    python -m virtualenv env

Per Python 3.4:

    python -m venv env
o pyvenv env

Installare tutti i pacchetti esterni richiesti dall'applicazione. È possibile utilizzare file requirements.txt hello radice hello pacchetti hello tooinstall del repository hello nell'ambiente virtuale:

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>Eseguire mediante il server di sviluppo
È possibile avviare un'applicazione hello in un server di sviluppo con hello comando seguente:

    env/bin/python runserver.py

console Hello verrà visualizzato l'URL di hello e server hello porte in ascolto:

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

Quindi, aprire l'URL di web browser toothat.

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a>Apportare modifiche
Ora è possibile provare ad apportare modifiche toohello applicazione origini e/o modelli.

Dopo aver verificato le modifiche, eseguirne il commit del repository Git toohello:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Installare altri pacchetti
L'applicazione potrebbe avere dipendenze oltre Python e Flask.

È possibile installare altri pacchetti utilizzando pip.  Ad esempio, tooinstall hello Azure SDK per Python, che consente di accedere tooAzure archiviazione, bus di servizio e altri servizi Azure, digitare:

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

## <a name="next-steps"></a>Passaggi successivi
Seguire questi toolearn collegamenti ulteriori sui pallone e gli strumenti Python per Visual Studio: 

* [Documentazione di Flask]
* [Python Tools per la documentazione di Visual Studio]

Per informazioni sull'uso di Archiviazione tabelle di Azure e MongoDB:

* [Flask e MongoDB in Azure con Python Tools per Visual Studio]
* [Flask e archiviazione tabelle di Azure con Python Tools per Visual Studio]

Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori Python](/develop/python/).

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Flask e MongoDB in Azure con Python Tools per Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask e archiviazione tabelle di Azure con Python Tools per Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

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
[Documentazione di Flask]: http://flask.pocoo.org/ 

