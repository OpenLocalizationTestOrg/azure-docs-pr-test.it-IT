---
title: aaaCreate un SQL PHP app web e distribuire tooAzure servizio App tramite Git
description: Un'esercitazione che illustra come toocreate PHP web app che archivia i dati in Database SQL di Azure e utilizzare tooAzure distribuzione Git servizio App.
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aaacb2fe0787bbcdafa72871912e8d08792be29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a>Creare un'app web SQL PHP e distribuire tooAzure servizio App tramite Git
Questa esercitazione viene illustrato come toocreate PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) che si connette tooAzure Database SQL e come toodeploy tramite Git. Questa esercitazione presuppone l'esistenza [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server per PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), e [Git] [ install-git] installato nel computer. Dopo aver completato questa guida, si disporrà di un'app Web PHP-MySQL in esecuzione in Azure.

> [!NOTE]
> È possibile installare e configurare Microsoft Drivers hello, SQL Server Express e PHP per SQL Server per PHP con hello [installazione guidata piattaforma Web di Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

Si acquisiranno le nozioni seguenti:

* Come toocreate di Azure web app e un Database SQL tramite hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715). Poiché per impostazione predefinita, PHP è abilitata nell'App del servizio Web App, niente di speciale è obbligatorio toorun codice PHP.
* Come toopublish e pubblicare nuovamente l'applicazione tooAzure tramite Git.

Seguendo questa esercitazione, verrà creata una semplice applicazione Web di registrazione in PHP, un'applicazione Hello verrà ospitata in un sito Web di Azure. Di seguito viene riportata una schermata dell'applicazione hello completata:

![Sito Web PHP di Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Creare un'app Web di Azure e configurare la pubblicazione Git
Seguire questi toocreate passaggi un'app web di Azure e un Database SQL:

1. Accedi toohello [portale Azure](https://portal.azure.com/).
2. Aprire hello Azure Marketplace facendo hello **New** sull'icona nella parte superiore di hello a sinistra della dashboard hello, fare clic su **Seleziona tutto** tooMarketplace avanti e selezionando **Web e dispositivi mobili**.
3. Nel Marketplace hello, selezionare **Web e dispositivi mobili**.
4. Fare clic su hello **Web app + SQL** icona.
5. Dopo aver letto descrizione hello di app Web hello + SQL app, selezionare **crea**.
6. Fare clic su ogni parte (**gruppo di risorse**, **App Web**, **Database**, e **sottoscrizione**) e immettere o selezionare i valori per hello richiesto campi:
   
   * Immettere un nome di URL a scelta.    
   * Configurare le credenziali del server di database.
   * Selezionare hello area più vicina tooyou
     
     ![configurazione dell'app](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Al termine definizione hello web app, fare clic su **crea**.
   
    Quando hello web app è stata creata, hello **notifiche** pulsante farà lampeggiare una verde **successo** e hello tooshow aprire Pannello gruppo di risorse sia hello web app e hello SQL database nel gruppo di hello.
8. Fare clic sull'icona dell'app web hello nel pannello hello risorsa gruppo blade tooopen hello dell'app web.
   
    ![Gruppo di risorse per app Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. In **Impostazioni** fare clic su **Distribuzione continua** > **Configurare le impostazioni necessarie**. Selezionare **Archivio Git locale** e fare clic su **OK**.
   
    ![Posizione del codice](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Se in precedenza non è stato configurato un repository Git, è necessario fornire nome utente e password. toodo, fare clic su **impostazioni** > **le credenziali di distribuzione** nel pannello dell'app web hello.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. In **impostazioni** fare clic su **proprietà** toosee hello Git URL remoto è necessario toouse toodeploy app PHP in un secondo momento.

## <a name="get-sql-database-connection-information"></a>Recuperare le informazioni sulla connessione al database SQL
istanza del Database SQL toohello tooconnect che è collegato tooyour web app, sarà necessario hello informazioni di connessione, specificato al momento della creazione del database hello. hello tooget informazioni di connessione al Database SQL, seguire questi passaggi:

1. Nel pannello del gruppo di risorse hello, fare clic sull'icona del database SQL di hello.
2. Nel pannello del database SQL di hello, fare clic su **impostazioni** > **proprietà**, quindi fare clic su **Mostra le stringhe di connessione di database**. 
   
    ![Visualizzazione delle proprietà database](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. Da hello **PHP** sezione della finestra di dialogo risultante hello, prendere nota dei valori di hello per `Server`, `SQL Database`, e `User Name`. Utilizzare questi valori in un secondo momento quando la pubblicazione del tooAzure di app web PHP servizio App.

## <a name="build-and-test-your-application-locally"></a>Creazione e test dell'applicazione in locale
applicazione di registrazione Hello è una semplice applicazione PHP che consente di tooregister per un evento, fornendo il nome e l'indirizzo e-mail. Le informazioni sui registranti precedenti vengono visualizzate in una tabella. Le informazioni sulle registrazioni vengono archiviate in un'istanza del database SQL. un'applicazione Hello è costituito da due file (copiare e incollare codice riportato di seguito):

* **index.php**: consente di visualizzare un modulo per la registrazione e una tabella contenente informazioni sui registranti.
* **CreateTable.PHP**: Crea tabella di Database SQL di hello per un'applicazione hello. Questo file verrà utilizzato una volta sola.

in locale, un'applicazione hello toorun procedura hello riportata di seguito. Si noti che questi passaggi presuppongono che si dispone di PHP e SQL Server Express impostare sul computer locale e che è stata attivata hello [estensione PDO per SQL Server][pdo-sqlsrv].

1. Creare un database di SQL Server denominato `registration`. È possibile farlo da hello `sqlcmd` prompt dei comandi con questi comandi:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. Nella directory radice dell'applicazione creare due file: uno denominato `createtable.php` e l'altro denominato `index.php`.
3. Aprire hello `createtable.php` file in un editor di testo o un IDE e aggiungere codice hello riportato di seguito. Questo codice sarà utilizzato toocreate hello `registration_tbl` tabella hello `registration` database.
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    Si noti che sono necessari valori hello tooupdate per <code>$user</code> e <code>$pwd</code> con il nome utente di SQL Server locale e la password.
4. In un terminal alla directory radice hello di hello di tipo applicazione hello comando seguente:
   
        php -S localhost:8000
5. Aprire un web browser e passare troppo**http://localhost:8000/createtable.php**. Verrà creata hello `registration_tbl` tabella nel database di hello.
6. Aprire hello **index.php** file in un editor di testo o un IDE e aggiungere hello base codice HTML e CSS per la pagina hello (hello codice PHP aggiunto nei passaggi successivi).
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. All'interno dei tag PHP hello, aggiungere il codice PHP per la connessione database toohello.
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    Nuovamente, sarà necessario valori hello tooupdate per <code>$user</code> e <code>$pwd</code> con il nome utente di MySQL locale e la password.
8. Il seguente codice di connessione database hello, aggiungere il codice per l'inserimento di informazioni di registrazione nel database di hello.
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. Infine, il seguente codice hello precedente, aggiungere il codice per recuperare dati dal database hello.
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

È possibile cercare troppo**http://localhost:8000/index.php** tootest un'applicazione hello.

## <a name="publish-your-application"></a>Pubblicare l'applicazione
Dopo aver testato l'applicazione localmente, è possibile pubblicare App Web del servizio tooApp tramite Git. Tuttavia, è necessario innanzitutto informazioni di connessione di database tooupdate hello in un'applicazione hello. Utilizzando le informazioni di connessione database hello ottenuti in precedenza (in hello **informazioni di connessione di Database SQL di ottenere** sezione), aggiornamento hello le seguenti informazioni in **entrambi** hello `createdatabase.php` e `index.php` i file con hello valori appropriati:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> In hello <code>$host</code>, il valore di hello del Server deve essere preceduto da <code>tcp:</code>.
> 
> 

A questo punto, si sono pronti tooset la pubblicazione Git e pubblica un'applicazione hello.

> [!NOTE]
> Si tratta di hello stessi passaggi indicati alla fine hello hello **creare un'app web di Azure e impostare la pubblicazione Git** sezione precedente.
> 
> 

1. Aprire GitBash (o un terminale, se si trova in Git il `PATH`), cambiare directory radice toohello di directory dell'applicazione (hello **registrazione** directory), e hello esecuzione seguenti comandi:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Verrà richiesto di hello password creato in precedenza.
2. Sfoglia troppo**http://[web app name].azurewebsites.net/createtable.php** toocreate tabella del database SQL di hello per un'applicazione hello.
3. Sfoglia troppo**http://[web app name].azurewebsites.net/index.php** toobegin utilizzando un'applicazione hello.

Dopo aver pubblicato l'applicazione, è possibile iniziare a creare tooit modifiche e utilizzare Git toopublish li. 

## <a name="publish-changes-tooyour-application"></a>Pubblicare l'applicazione di modifiche tooyour
toopublish cambia tooapplication, seguire questi passaggi:

1. Apportare modifiche tooyour applicazione localmente.
2. Aprire GitBash (o un terminale, it Git è nel `PATH`), modificare le directory toohello radice directory dell'applicazione ed eseguire hello seguenti comandi:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Verrà richiesto di hello password creato in precedenza.
3. Sfoglia troppo**http://[web app name].azurewebsites.net/index.php** toosee le modifiche.

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

