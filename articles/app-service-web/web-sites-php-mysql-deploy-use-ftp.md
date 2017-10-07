---
title: aaaCreate PHP-MySQL web app in Azure App Service e la distribuzione tramite FTP
description: Un'esercitazione che illustra come toocreate PHP web app che archivia i dati in uso e MySQL tooAzure di distribuzione FTP.
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6d9d1de5-5868-48fd-8bad-decb4979cd65
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4d3b56a8ac63d0eba0dc0aec1b62e6d12f601bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Creazione di un'app Web PHP-MySQL in Servizio app di Azure e distribuzione tramite FTP
Questa esercitazione Mostra l'app web toocreate PHP, MySQL e la modalità toodeploy tramite FTP. A tale scopo, si presuppone che nel computer siano installati [PHP][install-php], [MySQL][install-mysql], un server Web e un client FTP. istruzioni di Hello in questa esercitazione possono essere seguite su qualsiasi sistema operativo, tra cui Windows, Mac e Linux. Dopo aver completato questa guida, si disporrà dell'app Web PHP/MySQL in esecuzione in Azure.

Si acquisiranno le nozioni seguenti:

* Come toocreate un'app web e MySQL database utilizzando hello portale di Azure. Poiché per impostazione predefinita, PHP è abilitato nelle App Web, niente di speciale è obbligatorio toorun codice PHP.
* Come toopublish tooAzure applicazione utilizzando FTP.

Seguendo questa esercitazione, verrà creata una semplice app Web di registrazione in PHP, un'applicazione Hello verrà ospitata in un'App Web. Di seguito viene riportata una schermata dell'applicazione hello completata:

![Sito Web PHP di Azure][running-app]

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account, Vai troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Creare un'app Web e configurare la pubblicazione FTP
Seguire questi passaggi toocreate un'app web e un database MySQL:

1. Account di accesso toohello [portale Azure][management-portal].
2. Fare clic su hello **+ nuovo** sull'icona nella parte superiore di hello a sinistra della hello portale di Azure.
   
    ![Creazione di un nuovo sito Web di Azure][new-website]
3. In tipo di ricerca hello **Web app + MySQL** e fare clic su **Web app + MySQL**.
   
    ![Creazione personalizzata di un nuovo sito Web][custom-create]
4. Fare clic su **Crea**. Immettere un nome di servizio app univoco, un nome valido per il gruppo di risorse hello e un nuovo piano di servizio.
   
    ![Gruppo di risorse denominato ADF.][resource-group]
5. Immettere i valori per il nuovo database, tra cui accettano toohello legali.
   
    ![Creazione di un nuovo database MySQL][new-mysql-db]
6. Quando hello web app è stata creata, verrà visualizzato il pannello nuova app servizio hello.
7. Fare clic su **Impostazioni** > **Credenziali di distribuzione**. 
   
    ![Reimpostare le credenziali di distribuzione][set-deployment-credentials]
8. tooenable pubblicazione tramite FTP, è necessario fornire un nome utente e una password. Salvare le credenziali di hello e prendere nota del nome utente hello e la password creata.
   
    ![Creazione di credenziali di pubblicazione][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Creare e verificare l'applicazione in locale
applicazione di registrazione Hello è una semplice applicazione PHP che consente di tooregister per un evento, fornendo il nome e l'indirizzo e-mail. Le informazioni sui registranti precedenti vengono visualizzate in una tabella. Le informazioni sulle registrazioni vengono archiviate in un database MySQL. app Hello è costituita da due file:

* **index.php**: consente di visualizzare un modulo per la registrazione e una tabella contenente informazioni sui registranti.
* **CreateTable.PHP**: Crea tabella di MySQL hello per un'applicazione hello. Questo file verrà utilizzato una volta sola.

toobuild e app hello esecuzione in locale, eseguire le operazioni di hello riportato di seguito. Si noti che questi passaggi presuppongono che si dispone di PHP, MySQL e un server web configurato nel computer locale, e che è stata attivata hello [estensione PDO per MySQL][pdo-mysql].

1. Creare un database MySQL denominato `registration`. È possibile farlo dal prompt dei comandi di MySQL hello con questo comando:
   
        mysql> create database registration;
2. Nella directory radice del server Web creare una cartella denominata `registration` e al suo interno creare due file: uno denominato `createtable.php` e l'altro denominato `index.php`.
3. Aprire hello `createtable.php` file in un editor di testo o un IDE e aggiungere codice hello riportato di seguito. Questo codice sarà utilizzato toocreate hello `registration_tbl` tabella hello `registration` database.
   
        <?php
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
                        id INT NOT NULL AUTO_INCREMENT, 
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
   
   > [!NOTE]
   > È necessario che i valori hello tooupdate per <code>$user</code> e <code>$pwd</code> con il nome utente di MySQL locale e la password.
   > 
   > 
4. Aprire un web browser e passare troppo[http://localhost/registration/createtable.php][localhost-createtable]. Verrà creata hello `registration_tbl` tabella nel database di hello.
5. Aprire hello **index.php** file in un editor di testo o un IDE e aggiungere hello base codice HTML e CSS per la pagina hello (hello codice PHP aggiunto nei passaggi successivi).
   
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
6. All'interno dei tag PHP hello, aggiungere il codice PHP per la connessione database toohello.
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > Nuovamente, sarà necessario valori hello tooupdate per <code>$user</code> e <code>$pwd</code> con il nome utente di MySQL locale e la password.
   > 
   > 
7. Il seguente codice di connessione database hello, aggiungere il codice per l'inserimento di informazioni di registrazione nel database di hello.
   
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
8. Infine, il seguente codice hello precedente, aggiungere il codice per recuperare dati dal database hello.
   
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

È possibile cercare troppo[http://localhost/registration/index.php] [ localhost-index] tootest hello app.

## <a name="get-mysql-and-ftp-connection-information"></a>Recupero di informazioni sulla connessione a MySQL ed FTP
database MySQL tooconnect toohello in cui è in esecuzione in applicazioni Web, sarà necessario hello informazioni di connessione. tooget informazioni di connessione MySQL, seguire questi passaggi:

1. Servizio app hello pannello app web fare clic sul collegamento di gruppo di risorse hello:
   
    ![Selezionare Gruppo di risorse][select-resourcegroup]
2. Il gruppo di risorse, fare clic su database hello:
   
    ![Selezionare il database][select-database]
3. Database hello riepilogo, selezionare **impostazioni** > **proprietà**.
   
    ![Selezionare le proprietà][select-properties]
4. Prendere nota dei valori di hello per `Database`, `Host`, `User Id`, e `Password`.
   
    ![Proprietà nota][note-properties]
5. Dall'app web, fare clic su hello **Scarica profilo di pubblicazione** collegamento hello angolo in basso a destra della pagina hello:
   
    ![Scarica profilo di pubblicazione][download-publish-profile]
6. Aprire hello `.publishsettings` file in un editor XML. 
7. Trovare hello `<publishProfile >` elemento con `publishMethod="FTP"` che ricerca toothis simile:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Prendere nota di hello `publishUrl`, `userName`, e `userPWD` gli attributi.

## <a name="publish-your-app"></a>Pubblicare l'app
Dopo aver testato l'app localmente, è possibile pubblicare app web tooyour tramite FTP. Tuttavia, è necessario innanzitutto informazioni di connessione di database tooupdate hello in un'applicazione hello. Utilizzando le informazioni di connessione database hello ottenuti in precedenza (in hello **le informazioni di connessione FTP e di ottenere MySQL** sezione), aggiornamento hello le seguenti informazioni in **entrambi** hello `createdatabase.php` e `index.php` i file con hello valori appropriati:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

È ora pronto toopublish app tramite FTP.

1. Aprire il client FTP preferito.
2. Immettere hello *parte del nome host* da hello `publishUrl` attributo è indicato in precedenza nel client FTP.
3. Immettere hello `userName` e `userPWD` invariata attributi è indicato in precedenza nel client FTP.
4. Stabilire una connessione.

Dopo avere stabilito la connessione verrà essere in grado di tooupload e scaricare i file in base alle esigenze. Assicurarsi che si sta caricando file toohello radice, ovvero `/site/wwwroot`.

Dopo il caricamento sia `index.php` e `createtable.php`, Sfoglia troppo**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL per un'applicazione hello di tabella, quindi individuare troppo**http://[site nome ].azurewebsites.net/index.php** toobegin utilizzando un'applicazione hello.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).

[install-php]: http://www.php.net/manual/en/install.php
[install-mysql]: http://dev.mysql.com/doc/refman/5.6/en/installing.html
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[localhost-createtable]: http://localhost/tasklist/createtable.php
[localhost-index]: http://localhost/tasklist/index.php
[running-app]: ./media/web-sites-php-mysql-deploy-use-ftp/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-ftp/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-ftp/create_web_mysql.png
[website-details]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/website_details.jpg
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-ftp/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-ftp/select_webapp.png
[set-deployment-credentials]: ./media/web-sites-php-mysql-deploy-use-ftp/set_credentials.png
[portal-ftp-username-password]: ./media/web-sites-php-mysql-deploy-use-ftp/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-ftp/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-ftp/create_wa.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-ftp/select_database.png
[select-resourcegroup]: ./media/web-sites-php-mysql-deploy-use-ftp/select_resourcegroup.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/note-properties.png

[connection-string-info]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/connection_string_info.png
[management-portal]: https://portal.azure.com
[download-publish-profile]: ./media/web-sites-php-mysql-deploy-use-ftp/download_publish_profile_3.png

