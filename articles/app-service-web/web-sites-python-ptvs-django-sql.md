---
title: aaaDjango e Database SQL in Azure con Python Tools 2.2 per Visual Studio
description: Informazioni su come toouse hello Python Tools per Visual Studio toocreate un'app web Django che archivia i dati in un'istanza del database SQL e distribuirlo tooAzure App del servizio Web App.
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Django e database SQL in Azure con Python Tools 2.2 per Visual Studio
In questa esercitazione si userà [Python Tools per Visual Studio] toocreate una semplice app web utilizzando uno dei modelli di esempio hello PTVS esegue il polling. Questa esercitazione è anche disponibile in formato [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).

Si apprenderà come toouse un database SQL ospitato in Azure, come tooconfigure hello web app toouse un database SQL e come toopublish hello app web troppo[App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

Vedere hello [Centro per sviluppatori Python] per ulteriori articoli che coprono lo sviluppo di App del servizio Web App di Azure con PTVS utilizzando Bottle pallone e Django web Framework, con i servizi di archiviazione tabelle di Azure, MySQL e Database SQL. Durante questo articolo è incentrato sul servizio App, i passaggi di hello sono simili durante lo sviluppo di [servizi Cloud di Azure].

## <a name="prerequisites"></a>Prerequisiti
* Visual Studio 2015
* [Python 2.7 a 32 bit]
* [Python Tools 2.2 per Visual Studio]
* [Python Tools 2.2 per Visual Studio esempi VSIX]
* [Strumenti di Azure SDK per Visual Studio 2015]
* Django 1.9 o versione successiva

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
>
>

## <a name="create-hello-project"></a>Creare hello progetto
In questa sezione verrà creato un progetto di Visual Studio usando un modello di esempio. Verrà creato un ambiente virtuale e verranno installati i pacchetti necessari. Si creerà un database locale usando sqlite, Quindi viene eseguito localmente hello web app.

1. In Visual Studio selezionare **File**, **Nuovo progetto**.
2. modelli di progetto da hello Hello [Python Tools 2.2 per Visual Studio esempi VSIX] sono disponibili in **Python**, **esempi**. Selezionare **progetto Web di polling Django** e fare clic su OK toocreate hello progetto.

     ![Finestra di dialogo Nuovo progetto](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. Sarà richiesto tooinstall i pacchetti esterni. Selezionare **Installa in un ambiente virtuale**.

     ![Finestra di dialogo dei pacchetti esterni](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Selezionare **Python 2.7** come interprete base hello.

     ![Finestra di dialogo Aggiungi ambiente virtuale](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. In **Esplora**, fare clic sul nodo del progetto hello e selezionare **Python**, quindi selezionare **Django eseguire la migrazione**.  Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).
6. Questo verrà aprire una Console di gestione Django e creare un database sqlite nella cartella di progetto hello. Seguire hello richieste toocreate un utente.
7. Verificare che l'applicazione hello funzioni premendo <kbd>F5</kbd>.
8. Fare clic su **Accedi** hello barra di spostamento superiore hello.

     ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Immettere le credenziali di hello per utente hello creato quando è possibile sincronizzare database hello.

     ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. Fare clic su **Create Sample Polls**.

      ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Fare clic su un sondaggio e votare.

      ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>Creare un database SQL
Per il database di hello, si creerà un database SQL di Azure.

Per creare un database, seguire questa procedura.

1. Accedere al hello [portale Azure].
2. Nella parte inferiore di hello del riquadro di spostamento hello, fare clic su **NEW**. Fare clic su **Dati e archiviazione** > **Database SQL**.
3. Configurare hello Nuovo Database SQL tramite la creazione di un nuovo gruppo di risorse e selezionare hello posizione appropriata per tale.
4. Una volta creato hello Database SQL, fare clic su **aperta in Visual Studio** nel pannello database hello.
5. Fare clic su **Configura firewall**.
6. In hello **le impostazioni del Firewall** pannello, aggiungere una regola firewall con **IP iniziale** e **IP finale** impostare l'indirizzo IP pubblico toohello del computer di sviluppo. Fare clic su **Salva**.

   In questo modo i server di database di connessioni toohello dal computer di sviluppo.
7. Nel pannello database hello, fare clic su **proprietà**, quindi fare clic su **Mostra le stringhe di connessione di database**.
8. Utilizzare il valore hello copia pulsante tooput hello di **ADO.NET** negli Appunti hello.

## <a name="configure-hello-project"></a>Configurare hello progetto
In questa sezione, è possibile configurare il database SQL di hello di web app toouse che appena creato. È inoltre verrà installato il database SQL toouse obbligatorio Python pacchetti aggiuntivi con Django. Quindi viene eseguito localmente hello web app.

1. In Visual Studio, aprire **settings.py**, da hello *ProjectName* cartella. Incollare temporaneamente la stringa di connessione hello nell'editor di hello. stringa di connessione Hello è nel formato seguente:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Modifica definizione hello `DATABASES` valori hello toouse precedenti.

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. In Esplora soluzioni in **ambienti Python**, fare clic su ambiente virtuale hello e selezionare **Installa pacchetto Python**.
2. Installare il pacchetto di hello `pyodbc` utilizzando **pip**.

     ![Finestra di dialogo per l'installazione del pacchetto](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Installare il pacchetto di hello `django-pyodbc-azure` utilizzando **pip**.

     ![Finestra di dialogo per l'installazione del pacchetto](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. In **Esplora**, fare clic sul nodo del progetto hello e selezionare **Python**, quindi selezionare **Django eseguire la migrazione**.  Selezionare quindi **Django Create Superuser**(Creazione SuperUser Django).

   Per creare tabelle hello per il database SQL hello creati nella sezione precedente hello. Seguire hello richieste toocreate un utente, che non dispone di utente hello toomatch nel database sqlite hello creato nella prima sezione hello.
5. Eseguire un'applicazione hello con `F5`. Esegue il polling creati con **creare sondaggi esempio** e hello i dati inviati dal voto verranno serializzati nel database SQL di hello.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Pubblicare hello web app tooAzure servizio App
Hello Azure .NET SDK fornisce toodeploy un modo semplice il tooAzure di app web App del servizio Web App web.

1. In **Esplora**, fare clic sul nodo del progetto hello e selezionare **pubblica**.

     ![Finestra di dialogo Pubblica sito Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. Fare clic su **App Web di Microsoft Azure**.
3. Fare clic su **New** toocreate una nuova app web.
4. Compilare hello seguente i campi e fare clic su **crea**.

   * **Nome dell'app Web**
   * **Piano di servizio app**
   * **Gruppo di risorse**
   * **Area**
   * Lasciare **server di Database** impostare troppo**alcun database**
5. Accettare tutte le altre impostazioni predefinite e fare clic su **Pubblica**.
6. Web browser verrà aperto automaticamente toohello pubblicato web app. Dovrebbe essere funzionante di hello web app come previsto, utilizzando hello **SQL** database ospitato in Azure.

   Congratulazioni.

     ![Web browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Passaggi successivi
Seguire questi toolearn collegamenti ulteriori informazioni sugli strumenti Python per Visual Studio, Django e Database SQL.

* [Documentazione di Python Tools per Visual Studio]
  * [Progetti Web]
  * [Progetti servizio cloud]
  * [Debug remoto in Microsoft Azure]
* [Documentazione di Django]
* [Database SQL]

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Centro per sviluppatori Python]: /develop/python/
[servizi Cloud di Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[portale Azure]: https://portal.azure.com
[Python Tools per Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 per Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 per Visual Studio esempi VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Strumenti di Azure SDK per Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 a 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Documentazione di Python Tools per Visual Studio]: http://aka.ms/ptvsdocs
[Debug remoto in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Progetti Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Progetti servizio cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentazione di Django]: https://www.djangoproject.com/
[Database SQL]: /documentation/services/sql-database/
