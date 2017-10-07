---
title: aaaDjango e MySQL in Azure con Python Tools 2.2 per Visual Studio
description: Informazioni su come toouse hello Python Tools per Visual Studio toocreate un'app web Django che archivia i dati in un'istanza di database MySQL e distribuirlo tooAzure App del servizio Web App.
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a>Django e MySQL in Azure con Python Tools 2.2 per Visual Studio
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

In questa esercitazione si utilizzerà [Python Tools per Visual Studio](https://www.visualstudio.com/vs/python) toocreate una semplice app web utilizzando uno dei modelli di esempio hello PTVS esegue il polling. Si apprenderà come toouse ospitato un servizio MySQL in Azure e come tooconfigure hello web app toouse MySQL come toopublish hello app web troppo[App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

> [!NOTE]
> Hello informazioni contenute in questa esercitazione sono disponibili anche in hello video seguente:
> 
> [PTVS 2.1: Django app with MySQL][video] (PTVS 2.1: app Django con MySQL)
> 
> 

Vedere hello [Centro per sviluppatori Python] per ulteriori articoli che coprono lo sviluppo di App del servizio Web App di Azure con PTVS utilizzando Bottle pallone e Django web Framework, con i servizi di archiviazione tabelle di Azure, MySQL e SQL Database. Durante questo articolo è incentrato sul servizio App, i passaggi di hello sono simili durante lo sviluppo di [servizi Cloud di Azure].

## <a name="prerequisites"></a>Prerequisiti
* Visual Studio 2015
* [Python 2.7 a 32 bit] o [Python 3.4 a 32 bit]
* [Python Tools 2.2 per Visual Studio]
* [Python Tools 2.2 per Visual Studio esempi VSIX]
* [Strumenti di Azure SDK per Visual Studio 2015]
* Django 1.9 o versione successiva

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="create-hello-project"></a>Creare hello progetto
In questa sezione verrà creato un progetto di Visual Studio usando un modello di esempio. Verrà creato un ambiente virtuale e verranno installati i pacchetti necessari. Si creerà un database locale usando sqlite, Quindi viene eseguita un'applicazione hello in locale.

1. In Visual Studio selezionare **File**, **Nuovo progetto**.
2. modelli di progetto da hello Hello [Python Tools 2.2 per Visual Studio esempi VSIX] sono disponibili in **Python**, **esempi**. Selezionare **progetto Web di polling Django** e fare clic su OK toocreate hello progetto.
   
    ![Finestra di dialogo Nuovo progetto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. Sarà richiesto tooinstall i pacchetti esterni. Selezionare **Installa in un ambiente virtuale**.
   
    ![Finestra di dialogo dei pacchetti esterni](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. Selezionare **Python 2.7** o **Python 3.4** come interprete base hello.
   
    ![Finestra di dialogo Aggiungi ambiente virtuale](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. In **Esplora**, fare clic sul nodo del progetto hello e selezionare **Python**, quindi selezionare **Django eseguire la migrazione**.  Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).
6. Questo verrà aprire una Console di gestione Django e creare un database sqlite nella cartella di progetto hello. Seguire hello richieste toocreate un utente.
7. Verificare che l'applicazione hello funzioni premendo `F5`.
8. Fare clic su **Accedi** hello barra di spostamento superiore hello.
   
    ![Barra di spostamento di Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. Immettere le credenziali di hello per utente hello creato quando è possibile sincronizzare database hello.
   
    ![Form di accesso](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. Fare clic su **Create Sample Polls**.
    
     ![Create Sample Polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. Fare clic su un sondaggio e votare.
    
     ![Votazione nei poll di esempio](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a>Creare un database MySQL
Per il database di hello, si creerà un database di hosting MySQL di ClearDB in Azure.

In alternativa, è possibile creare una propria macchina virtuale in esecuzione in Azure, quindi installare e amministrare MySQL manualmente.

Per creare un database con un piano gratuito, attenersi alla procedura seguente.

1. Accedi toohello [portale Azure].
2. Nella parte superiore del riquadro di spostamento hello hello, fare clic su **NEW**, quindi fare clic su **dati e archiviazione**, quindi fare clic su **MySQL Database**.
3. Configurare il nuovo database di MySQL hello creando un nuovo gruppo di risorse e selezionare hello percorso appropriato per tale.
4. Una volta creato il database di MySQL hello, fare clic su **proprietà** nel pannello database hello.
5. Utilizzare il valore hello copia pulsante tooput hello di **stringa di connessione** negli Appunti hello.

## <a name="configure-hello-project"></a>Configurare hello progetto
In questa sezione, è possibile configurare i database web app toouse hello MySQL che appena creato. Verrà installato anche database di MySQL toouse obbligatorio Python pacchetti aggiuntivi con Django. Quindi, puoi eseguire app web hello in locale.

1. In Visual Studio, aprire **settings.py**, da hello *ProjectName* cartella. Incollare temporaneamente la stringa di connessione hello nell'editor di hello. stringa di connessione Hello è nel formato seguente:
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    Database predefinito di modifica hello **motore** toouse MySQL e set hello valori per **nome**, **utente**, **PASSWORD** e  **HOST** da hello **CONNECTIONSTRING**.
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. In Esplora soluzioni in **ambienti Python**, fare clic su ambiente virtuale hello e selezionare **Installa pacchetto Python**.
3. Installare il pacchetto di hello `mysqlclient` utilizzando **pip**.
   
    ![Finestra di dialogo per l'installazione del pacchetto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. In **Esplora**, fare clic sul nodo del progetto hello e selezionare **Python**, quindi selezionare **Django eseguire la migrazione**.  Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).
   
    Per creare tabelle hello di database MySQL hello creato nella sezione precedente hello. Seguire hello richieste toocreate un utente, che non dispone di utente hello toomatch nel database sqlite hello creato nella prima sezione di hello di questo articolo.
5. Eseguire un'applicazione hello con `F5`. Esegue il polling creati con **creare sondaggi esempio** e hello i dati inviati dal voto verranno serializzati nel database di MySQL hello.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Pubblicare hello web app tooAzure servizio App
Hello Azure .NET SDK fornisce un modo semplice di toodeploy il tooAzure app web del servizio App.

1. In **Esplora**, fare clic sul nodo del progetto hello e selezionare **pubblica**.
   
    ![Finestra di dialogo Pubblica sito Web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. Fare clic su **Servizio app di Microsoft Azure**.
3. Fare clic su **New** toocreate una nuova app web.
4. Compilare hello seguente i campi e fare clic su **crea**:
   
   * **Nome dell'app Web**
   * **Piano di servizio app**
   * **Gruppo di risorse**
   * **Area**
   * Lasciare **server di Database** impostare troppo**alcun database**
5. Accettare tutte le altre impostazioni predefinite e fare clic su **Pubblica**.
6. Web browser verrà aperto automaticamente toohello pubblicato web app. Dovrebbe essere funzionante di hello web app come previsto, utilizzando hello **MySQL** database ospitato in Azure.
   
    ![Web browser](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    Congratulazioni. È stato pubblicato correttamente il tooAzure app web basate su MySQL.

## <a name="next-steps"></a>Passaggi successivi
Seguire questi toolearn collegamenti ulteriori informazioni sugli strumenti Python per Visual Studio, Django e MySQL.

* [Documentazione di Python Tools per Visual Studio]
  * [Progetti Web]
  * [Progetti servizio cloud]
  * [Debug remoto in Microsoft Azure]
* [Documentazione di Django]
* [MySQL]

Per ulteriori informazioni, vedere hello [Centro per sviluppatori Python](/develop/python/).

<!--Link references-->

[Centro per sviluppatori Python]: /develop/python/
[servizi Cloud di Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[portale Azure]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 per Visual Studio esempi VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Strumenti di Azure SDK per Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentazione di Python Tools per Visual Studio]: http://aka.ms/ptvsdocs
[Debug remoto in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Progetti Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Progetti servizio cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentazione di Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
