---
title: Creazione di un'app Web PHP-MySQL in Servizio app di Azure e distribuzione tramite Git
description: Un'esercitazione in cui viene illustrato come creare un'app Web PHP che archivia i dati in MySQL e come utilizzare la distribuzione Git in Azure."
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
ms.openlocfilehash: aa845eb474dbd42ae2c31880690d4ced059eb448
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>Creazione di un'app Web PHP-MySQL in Servizio app di Azure e distribuzione tramite Git
In questa esercitazione viene illustrato come creare un'app Web PHP-MySQL e come distribuirla in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) tramite Git. Si useranno [PHP][install-php], lo strumento da riga di comando MySQL (che fa parte di [MySQL][install-mysql]) e [Git][install-git] installati nel computer. Le istruzioni di questa esercitazione possono essere eseguite in qualsiasi sistema operativo, tra cui Windows, Mac e Linux. Dopo aver completato questa guida, si disporrà dell'app Web PHP/MySQL in esecuzione in Azure.

Si acquisiranno le nozioni seguenti:

* Come creare un'app Web e un database MySQL mediante il [portale di Azure][management-portal]. Poiché PHP è abilitato nelle [app Web di Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) per impostazione predefinita, non è necessario effettuare operazioni particolari per eseguire il codice PHP.
* Pubblicare e ripubblicare l'applicazione in Azure tramite Git.
* Come abilitare l'estensione Compositore e automatizzarne le attività per ogni `git push`.

Seguendo questa esercitazione, verrà creata una semplice app Web di registrazione in PHP, che verrà ospitata nelle app Web. Di seguito è riportata una schermata dell'applicazione completata:

![Sito Web PHP di Azure][running-app]

## <a name="set-up-the-development-environment"></a>Configurare l'ambiente di sviluppo
In questa esercitazione si presuppone che [PHP][install-php], lo strumento da riga di comando MySQL (parte di [MySQL][install-mysql]) e [Git][install-git] siano installati nel computer.

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>Creare un'app Web e configurare la pubblicazione Git
Per creare un'app Web e un database MySQL, attenersi alla procedura seguente:

1. Eseguire l'accesso al [portale di Azure][management-portal].
2. Fare clic sull'icona **Nuovo** .
3. Fare clic su **Visualizza tutto** accanto a **Marketplace**. 
4. Fare clic su **Web e dispositivi mobili**, quindi su **App Web + MySQL**. Fare quindi clic su **Crea**.
5. Immettere un nome valido per il gruppo di risorse.
   
    ![Gruppo di risorse denominato ADF.][resource-group]
6. Immettere i valori per la nuova app Web.
   
    ![Crea app Web][new-web-app]
7. Immettere i valori per il nuovo database e accettare termini e condizioni.
   
    ![Creazione di un nuovo database MySQL][new-mysql-db]
8. Una volta creata l'app Web, verrà visualizzato il pannello del nuovo gruppo di risorse.
9. In **Impostazioni** fare clic su **Distribuzione continua**, poi fare clic su *Configura le impostazioni necessarie*.
   
    ![Configurazione della pubblicazione Git][setup-publishing]
10. Selezionare **Repository Git locale** per l'origine.
    
     ![Impostare i repository Git][setup-repository]
11. Per abilitare la pubblicazione Git, è necessario specificare un nome utente e una password. Prendere nota del nome utente e della password creati. Se è stato configurato un repository Git in precedenza, ignorare questo passaggio.
    
     ![Creazione di credenziali di pubblicazione][credentials]

## <a name="get-remote-mysql-connection-information"></a>Recupero di informazioni sulla connessione remota a MySQL
Per connettersi al database MySQL in esecuzione in App Web, saranno necessarie le informazioni sulla connessione. Per recuperare le informazioni sulla connessione a MySQL, attenersi alla procedura seguente:

1. Dal gruppo di risorse, fare clic sul database:
   
    ![Selezionare il database][select-database]
2. Dalle **Impostazioni** del database, selezionare **Proprietà**.
   
    ![Selezionare le proprietà][select-properties]
3. Prendere nota dei valori di `Database`, `Host`, `User Id` e `Password`.
   
    ![Proprietà nota][note-properties]

## <a name="build-and-test-your-app-locally"></a>Creare e verificare l'applicazione in locale
Una volta creata l'app Web, è possibile sviluppare localmente l'applicazione, quindi distribuirla dopo il test.

L'applicazione di registrazione è una semplice applicazione PHP che consente di registrarsi per un evento specificando il proprio nome e l'indirizzo di posta elettronica. Le informazioni sui registranti precedenti vengono visualizzate in una tabella. Le informazioni sulle registrazioni vengono archiviate in un database MySQL. L'applicazione è costituita da un unico file (copiare e incollare il codice disponibile di seguito):

* **index.php**: consente di visualizzare un modulo per la registrazione e una tabella contenente informazioni sui registranti.

Per creare ed eseguire l'applicazione in locale, attenersi alla procedura seguente. Si noti che per questi passaggi si presuppone che PHP e lo strumento da riga di comando MySQL (parte di MySQL) siano configurati nel computer locale e che l'[estensione PDO per MySQL][pdo-mysql] sia stata abilitata.

1. Connettersi al server MySQL remoto usando i valori di `Data Source`, `User Id`, `Password` e `Database` recuperati in precedenza:
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. Verrà visualizzato il prompt dei comandi MySQL:
   
        mysql>
3. Incollare il comando `CREATE TABLE` seguente per creare la tabella `registration_tbl` nel database:
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. Nella radice della cartella dell'applicazione locale creare il file **index.php** .
5. Aprire il file **index.php** in un editor di testo o in un IDE e aggiungere il codice seguente, quindi completare le necessarie modifiche contrassegnate con commenti `//TODO:`.

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
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
            // DB connection info
            //TODO: Update the values for $host, $user, $pwd, and $db
            //using the values you retrieved earlier from the Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect to database.
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

1. In un terminale passare alla cartella dell'applicazione e digitare il comando seguente:
   
       php -S localhost:8000

A questo punto è possibile passare a **http://localhost:8000/** per testare l'applicazione.

## <a name="publish-your-app"></a>Pubblicare l'app
Dopo aver testato l'app in locale, è possibile pubblicarla su App Web tramite Git. Inizializzare l'archivio Git locale e pubblicare l'applicazione.

> [!NOTE]
> Questi passaggi sono uguali a quelli illustrati nel portale di Azure alla fine della precedente sezione Creare un'app Web e configurare la pubblicazione Git.
> 
> 

1. (Facoltativo) Se l'URL del repository remoto Git è stato dimenticato o smarrito, passare alle proprietà dell'app Web nel Portale di Azure.
2. Aprire GitBash (o un terminale, se Git si trova in `PATH`), passare alla directory radice dell'applicazione ed eseguire i comandi seguenti:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Verrà richiesto di specificare la password creata in precedenza.
   
    ![Push iniziale in Azure tramite Git][git-initial-push]
3. Passare a **http://[nome sito].azurewebsites.net/index.php** per iniziare a usare l'applicazione. Queste informazioni verranno archiviate nel dashboard dell'account:
   
    ![Sito Web PHP di Azure][running-app]

Dopo aver pubblicato l'app, è possibile iniziare ad apportarvi modifiche e ad usare Git per pubblicarle.

## <a name="publish-changes-to-your-app"></a>Pubblicare le modifiche apportate all'app
Per pubblicare le modifiche appportate all'app, attenersi alla procedura seguente:

1. Apportare le modifiche all'app localmente.
2. Aprire GitBash (o un terminale, se Git si trova in `PATH`), passare alla directory radice dell'app e eseguire i comandi seguenti:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Verrà richiesto di specificare la password creata in precedenza.
   
    ![Push delle modifiche del sito apportate in Azure tramite Git][git-change-push]
3. Passare a **http://[nome sito].azurewebsites.net/index.php** per visualizzare l'app e le eventuali modifiche apportate:
   
    ![Sito Web PHP di Azure][running-app]

> [!NOTE]
> Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a>Abilitare l'automazione Composer con l'estensione Composer
Per impostazione predefinita, il processo di distribuzione git nel servizio app non esegue operazioni relative a composer.json, se questo è presente nel progetto PHP. È possibile abilitare l'elaborazione di composer.json durante l'operazione di `git push` abilitando l'estensione Compositore.

1. Nel pannello dell'app Web PHP nel [portale di Azure][management-portal] fare clic su **Strumenti** > **Estensioni**.
   
    ![Impostazioni dell'estensione Compositore][composer-extension-settings]
2. Fare clic su **Aggiungi**, quindi su **Compositore**.
   
    ![Aggiunta dell'estensione Compositore][composer-extension-add]
3. Fare clic su **OK** per accettare le note legali. Fare di nuovo clic su **OK** per aggiungere l'estensione.
   
    Nel pannello **Estensioni installate** è ora visualizzata l'estensione Compositore.  
    ![Visualizzazione dell'estensione Compositore][composer-extension-view]
4. Eseguire ora `git add`, `git commit` e `git push` come nella sezione precedente. Si noterà che ora Composer installa le dipendenze definite in composer.json.
   
    ![Estensione Compositore - Esito positivo][composer-extension-success]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere il [Centro per sviluppatori di PHP](/develop/php/).

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
