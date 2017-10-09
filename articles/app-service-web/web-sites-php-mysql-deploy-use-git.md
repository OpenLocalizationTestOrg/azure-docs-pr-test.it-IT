---
title: aaaCreate PHP-MySQL web app in Azure App Service e la distribuzione usando Git
description: Un'esercitazione che illustra come toocreate PHP web app che archivia i dati di MySQL e utilizzare tooAzure distribuzione Git.
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 9c22946777598cc973cd9dfc8d2a258bd08cc39a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>Creazione di un'app Web PHP-MySQL in Servizio app di Azure e distribuzione tramite Git
Questa esercitazione Mostra l'app web toocreate PHP, MySQL e la modalità toodeploy è troppo[servizio App](http://go.microsoft.com/fwlink/?LinkId=529714) tramite Git. Si utilizzerà [PHP][install-php], lo strumento da riga di comando di MySQL hello (parte di [MySQL][install-mysql]), e [Git] [ install-git] installato nel computer. istruzioni di Hello in questa esercitazione possono essere seguite su qualsiasi sistema operativo, tra cui Windows, Mac e Linux. Dopo aver completato questa guida, si disporrà dell'app Web PHP/MySQL in esecuzione in Azure.

Si acquisiranno le nozioni seguenti:

* Come toocreate un'app web e MySQL database utilizzando hello [portale Azure][management-portal]. Perché PHP è abilitata in [App del servizio Web App](http://go.microsoft.com/fwlink/?LinkId=529714) per impostazione predefinita, niente di speciale è obbligatorio toorun codice PHP.
* Come toopublish e pubblicare nuovamente l'applicazione tooAzure tramite Git.
* Modalità tooenable hello Composer estensione tooautomate Composer attività in ogni `git push`.

Seguendo questa esercitazione, verrà creata una semplice app Web di registrazione in PHP, verrà ospitata l'applicazione Hello nelle App Web. Di seguito viene riportata una schermata dell'applicazione hello completata:

![Sito Web PHP di Azure][running-app]

## <a name="set-up-hello-development-environment"></a>Configurare un ambiente di sviluppo hello
Questa esercitazione presuppone l'esistenza [PHP][install-php], hello lo strumento da riga di comando di MySQL (parte di [MySQL][install-mysql]), e [Git] [ install-git] installato nel computer.

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>Creare un'app Web e configurare la pubblicazione Git
Seguire questi passaggi toocreate un'app web e un database MySQL:

1. Account di accesso toohello [portale Azure][management-portal].
2. Fare clic su hello **New** icona.
3. Fare clic su **vedere tutti** Avanti troppo**Marketplace**. 
4. Fare clic su **Web e dispositivi mobili**, quindi su **App Web + MySQL**. Fare quindi clic su **Crea**.
5. Immettere un nome valido per il gruppo di risorse.
   
    ![Gruppo di risorse denominato ADF.][resource-group]
6. Immettere i valori per la nuova app Web.
   
    ![Crea app Web][new-web-app]
7. Immettere i valori per il nuovo database, tra cui accettano toohello legali.
   
    ![Creazione di un nuovo database MySQL][new-mysql-db]
8. Quando hello web app è stata creata, verrà visualizzato il pannello nuova web app hello.
9. In **Impostazioni** fare clic su **Distribuzione continua**, poi fare clic su *Configura le impostazioni necessarie*.
   
    ![Configurazione della pubblicazione Git][setup-publishing]
10. Selezionare **Git Repository locale** per origine hello.
    
     ![Impostare i repository Git][setup-repository]
11. tooenable Git pubblicazione, è necessario fornire un nome utente e una password. Prendere nota del nome utente hello e la password creata. Se è stato configurato un repository Git in precedenza, ignorare questo passaggio.
    
     ![Creazione di credenziali di pubblicazione][credentials]

## <a name="get-remote-mysql-connection-information"></a>Recupero di informazioni sulla connessione remota a MySQL
database MySQL tooconnect toohello in cui è in esecuzione in applicazioni Web, sarà necessario hello informazioni di connessione. tooget informazioni di connessione MySQL, seguire questi passaggi:

1. Il gruppo di risorse, fare clic su database hello:
   
    ![Selezionare il database][select-database]
2. Da database hello **impostazioni**selezionare **proprietà**.
   
    ![Selezionare le proprietà][select-properties]
3. Prendere nota dei valori di hello per `Database`, `Host`, `User Id`, e `Password`.
   
    ![Proprietà nota][note-properties]

## <a name="build-and-test-your-app-locally"></a>Creare e verificare l'applicazione in locale
Una volta creata l'app Web, è possibile sviluppare localmente l'applicazione, quindi distribuirla dopo il test.

applicazione di registrazione Hello è una semplice applicazione PHP che consente di tooregister per un evento, fornendo il nome e l'indirizzo e-mail. Le informazioni sui registranti precedenti vengono visualizzate in una tabella. Le informazioni sulle registrazioni vengono archiviate in un database MySQL. un'applicazione Hello è costituito da un file (copiare e incollare codice riportato di seguito):

* **index.php**: consente di visualizzare un modulo per la registrazione e una tabella contenente informazioni sui registranti.

toobuild e in locale, un'applicazione hello esecuzione procedura hello riportata di seguito. Si noti che questi passaggi presuppongono che si dispone di hello PHP e MySQL strumento della riga di comando (parte di MySQL) impostare sul computer locale, e che è stata attivata hello [estensione PDO per MySQL][pdo-mysql].

1. Connettersi toohello MySQL server remoto, utilizzando il valore di hello per `Data Source`, `User Id`, `Password`, e `Database` recuperato in precedenza:
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. verranno visualizzati prompt dei comandi di Hello MySQL:
   
        mysql>
3. Incolla in seguito hello `CREATE TABLE` comando toocreate hello `registration_tbl` tabella del database:
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. Nella directory radice della cartella dell'applicazione locale hello creare **index.php** file.
5. Aprire hello **index.php** file in un editor di testo o un IDE e aggiungere hello seguente di codice e le modifiche necessarie hello completa è contrassegnato con `//TODO:` commenti.

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
            // DB connection info
            //TODO: Update hello values for $host, $user, $pwd, and $db
            //using hello values you retrieved earlier from hello Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect toodatabase.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
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
            // Retrieve data
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
        ?>
        </body>
        </html>

1. In un terminal tooyour passare applicazione cartella e il tipo hello comando seguente:
   
       php -S localhost:8000

È possibile cercare troppo**http://localhost:8000/servicemodelsamples/Service /** tootest un'applicazione hello.

## <a name="publish-your-app"></a>Pubblicare l'app
Dopo aver testato l'app localmente, è possibile pubblicare le app tooWeb tramite Git. Verrà inizializzare il repository Git locale e pubblicare un'applicazione hello.

> [!NOTE]
> Questi sono hello stessi passaggi illustrati in hello Set e il portale di Azure alla fine hello hello crea un'app web di pubblicazione Git sezione precedente.
> 
> 

1. (Facoltativo)  Se è stato dimenticato o erroneamente posizionato l'URL remoto repostitory Git, è possibile passare toohello proprietà dell'app web nel portale di Azure hello.
2. Aprire GitBash (o un terminale, se si trova in Git il `PATH`), modificare le directory toohello radice directory dell'applicazione ed eseguire hello seguenti comandi:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Verrà richiesto di hello password creato in precedenza.
   
    ![TooAzure Push iniziale tramite Git][git-initial-push]
3. Sfoglia troppo**http://[site name].azurewebsites.net/index.php** toobegin utilizzando un'applicazione hello (queste informazioni verranno archiviate nel dashboard account):
   
    ![Sito Web PHP di Azure][running-app]

Dopo aver pubblicato l'applicazione, è possibile iniziare a creare tooit modifiche e utilizzare Git toopublish li.

## <a name="publish-changes-tooyour-app"></a>Pubblicare app tooyour modifiche
toopublish modifiche tooyour app, seguire questi passaggi:

1. Rendere l'app tooyour modifiche localmente.
2. Aprire GitBash (o un terminale, it Git è il `PATH`), modificare le directory toohello radice directory dell'app ed eseguire hello seguenti comandi:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Verrà richiesto di hello password creato in precedenza.
   
    ![Push tooAzure di modifiche del sito tramite Git][git-change-push]
3. Sfoglia troppo**http://[site name].azurewebsites.net/index.php** toosee l'app e le eventuali modifiche apportate:
   
    ![Sito Web PHP di Azure][running-app]

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a>Abilitare l'automazione Composer con estensione Composer hello
Per impostazione predefinita, processo di distribuzione git hello nel servizio App non esegue alcuna operazione con composer.json, se presente nel progetto PHP. È possibile abilitare composer.json durante l'elaborazione di `git push` abilitando l'estensione Composer hello.

1. Nel PHP web pannello dell'app in hello [portale di Azure][management-portal], fare clic su **strumenti** > **estensioni**.
   
    ![Impostazioni dell'estensione Compositore][composer-extension-settings]
2. Fare clic su **Aggiungi**, quindi su **Compositore**.
   
    ![Aggiunta dell'estensione Compositore][composer-extension-add]
3. Fare clic su **OK** tooaccept legali. Fare clic su **OK** nuovamente tooadd estensione di hello.
   
    Hello **estensioni installate** pannello verrà visualizzati estensione Composer hello.  
    ![Visualizzazione dell'estensione Compositore][composer-extension-view]
4. A questo punto, eseguire `git add`, `git commit`, e `git push` come nella sezione precedente hello. Si noterà che ora Composer installa le dipendenze definite in composer.json.
   
    ![Estensione Compositore - Esito positivo][composer-extension-success]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: ./media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: ./media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: ./media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: ./media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png
