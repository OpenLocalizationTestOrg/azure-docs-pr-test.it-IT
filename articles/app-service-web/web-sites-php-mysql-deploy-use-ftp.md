---
title: Creazione di un'app Web PHP-MySQL in Servizio app di Azure e distribuzione tramite FTP
description: Esercitazione che illustra come creare un'app Web PHP che archivia i dati in MySQL e come usare la distribuzione FTP in Azure."
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
ms.openlocfilehash: d428dffc6b810a692be0ec39a5f9cca05f5439e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Creazione di un'app Web PHP-MySQL in Servizio app di Azure e distribuzione tramite FTP
Questa esercitazione illustra come creare un'app Web di Azure PHP-MySQL e distribuirla tramite FTP. A tale scopo, si presuppone che nel computer siano installati [PHP][install-php], [MySQL][install-mysql], un server Web e un client FTP. Le istruzioni di questa esercitazione possono essere eseguite in qualsiasi sistema operativo, tra cui Windows, Mac e Linux. Dopo aver completato questa guida, si disporrà dell'app Web PHP/MySQL in esecuzione in Azure.

Si acquisiranno le nozioni seguenti:

* Creare un'app Web e un database MySQL mediante il portale di Azure. Poiché PHP è abilitato in App Web di Azure per impostazione predefinita, non è necessario completare operazioni speciali per eseguire il codice PHP.
* Pubblicare l'applicazione in Azure tramite FTP.

Seguendo questa esercitazione, verrà creata una semplice app Web di registrazione in PHP, ospitata in un'app Web. Di seguito è riportata una schermata dell'applicazione completata:

![Sito Web PHP di Azure][running-app]

> [!NOTE]
> Per iniziare a utilizzare Servizio app di Azureprima di registrare un account di Azure, andare alla pagina di [prova di Servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare immediatamente un'app Web temporanea in Servizio app. Non è necessario fornire una carta di credito né impegnarsi in alcun modo. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Creare un'app Web e configurare la pubblicazione FTP
Per creare un'app Web e un database MySQL, attenersi alla procedura seguente:

1. Eseguire l'accesso al [portale di Azure][management-portal].
2. Fare clic sull'icona **+Nuovo** nella parte superiore sinistra del portale di Azure.
   
    ![Creazione di un nuovo sito Web di Azure][new-website]
3. Nella casella di ricerca digitare **App Web e MySQL** e fare clic su **App Web e MySQL**.
   
    ![Creazione personalizzata di un nuovo sito Web][custom-create]
4. Fare clic su **Create**. Immettere un nome di servizio app univoco, un nome valido per il gruppo di risorse e un nuovo piano di servizio.
   
    ![Gruppo di risorse denominato ADF.][resource-group]
5. Immettere i valori per il nuovo database e accettare termini e condizioni.
   
    ![Creazione di un nuovo database MySQL][new-mysql-db]
6. Una volta creata l'app Web, verrà visualizzato il pannello del nuovo servizio app.
7. Fare clic su **Impostazioni** > **Credenziali di distribuzione**. 
   
    ![Reimpostare le credenziali di distribuzione][set-deployment-credentials]
8. Per abilitare la pubblicazione FTP è necessario specificare un nome utente e una password. Salvare le credenziali e prendere nota del nome utente e della password creati.
   
    ![Creazione di credenziali di pubblicazione][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Creare e verificare l'applicazione in locale
L'applicazione di registrazione è una semplice applicazione PHP che consente di registrarsi per un evento specificando il proprio nome e l'indirizzo di posta elettronica. Le informazioni sui registranti precedenti vengono visualizzate in una tabella. Le informazioni sulle registrazioni vengono archiviate in un database MySQL. L'applicazione è costituita da due file:

* **index.php**: consente di visualizzare un modulo per la registrazione e una tabella contenente informazioni sui registranti.
* **createtable.php**: consente di creare la tabella MySQL per l'applicazione. Questo file verrà utilizzato una volta sola.

Per creare ed eseguire l'app in locale, attenersi alla procedura seguente. Si noti che per questi passaggi si presuppone che nel computer locale siano già stati configurati PHP, MySQL e un server Web e che sia stata abilitata l'[estensione PDO per MySQL][pdo-mysql].

1. Creare un database MySQL denominato `registration`. A tale scopo, immettere al prompt dei comandi MySQL il comando seguente:
   
        mysql> create database registration;
2. Nella directory radice del server Web creare una cartella denominata `registration` e al suo interno creare due file: uno denominato `createtable.php` e l'altro denominato `index.php`.
3. Aprire il file `createtable.php` in un editor di testo o IDE e aggiungere il codice seguente. Questo codice verrà usato per creare la tabella `registration_tbl` nel database `registration`.
   
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
   > È necessario aggiornare i valori per <code>$user</code> e <code>$pwd</code> con il nome utente di MySQL locale e la password.
   > 
   > 
4. Aprire un Web browser e passare a [http://localhost/registration/createtable.php][localhost-createtable]. Verrà creata la tabella `registration_tbl` nel database.
5. Aprire il file **index.php** in un editor di testo o IDE e aggiungere il codice HTML e CSS di base per la pagina (il codice PHP verrà aggiunto nei passaggi successivi).
   
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
   
        ?>
        </body>
        </html>
6. All'interno dei tag PHP, aggiungere il codice PHP per la connessione al database.
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > Nuovamente, sarà necessario aggiornare i valori per <code>$user</code> e <code>$pwd</code> con il nome utente di MySQL locale e la password.
   > 
   > 
7. Dopo il codice di connessione al database, aggiungere il codice per l'inserimento delle informazioni di registrazione nel database.
   
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
8. Infine, dopo il codice sopra riportato, aggiungere il codice per recuperare i dati dal database.
   
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

A questo punto è possibile passare a [http://localhost/registration/index.php][localhost-index] per testare l'applicazione.

## <a name="get-mysql-and-ftp-connection-information"></a>Recupero di informazioni sulla connessione a MySQL ed FTP
Per connettersi al database MySQL in esecuzione in App Web, saranno necessarie le informazioni sulla connessione. Per recuperare le informazioni sulla connessione a MySQL, attenersi alla procedura seguente:

1. Nel pannello dell'app Web del servizio app fare clic sul collegamento Gruppo di risorse:
   
    ![Selezionare Gruppo di risorse][select-resourcegroup]
2. Dal gruppo di risorse, fare clic sul database:
   
    ![Selezionare il database][select-database]
3. Nel riepilogo del database selezionare **Impostazioni** > **Proprietà**.
   
    ![Selezionare le proprietà][select-properties]
4. Prendere nota dei valori di `Database`, `Host`, `User Id` e `Password`.
   
    ![Proprietà nota][note-properties]
5. Dall'app Web fare clic sul collegamento **Scarica profilo di pubblicazione** nell'angolo in basso a destra della pagina:
   
    ![Scarica profilo di pubblicazione][download-publish-profile]
6. Aprire il file `.publishsettings` in un editor XML. 
7. Trovare l'elemento `<publishProfile >` con `publishMethod="FTP"` che abbia un aspetto simile al seguente:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Prendere nota degli attributi `publishUrl`, `userName` e `userPWD`.

## <a name="publish-your-app"></a>Pubblicare l'app
Dopo aver verificato l'app in locale è possibile pubblicarla nell'app Web tramite FTP. È tuttavia necessario aggiornare innanzitutto le informazioni di connessione al database nell'applicazione. Usando le informazioni di connessione al database ottenute in precedenza (nella sezione **Recuperare le informazioni sulla connessione a MySQL ed FTP**) aggiornare le informazioni seguenti in **entrambi** i file `createdatabase.php` e `index.php` con i valori appropriati:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

A questo punto è possibile pubblicare l'app tramite FTP.

1. Aprire il client FTP preferito.
2. Immettere nel client FTP la *parte di nome host* dell'attributo `publishUrl` precedentemente annotato.
3. Immettere gli attributi `userName` e `userPWD` precedentemente annotati, senza modifiche, nel client FTP.
4. Stabilire una connessione.

Dopo aver effettuato la connessione si sarà in grado di caricare e scaricare i file in base alle proprie esigenze. Assicurarsi di caricare i file nella directory radice, ossia `/site/wwwroot`.

Dopo aver caricato `index.php` e `createtable.php`, passare a **http://[nome sito].azurewebsites.net/createtable.php** per creare la tabella MySQL per l'applicazione, quindi passare a **http://[nome sito].azurewebsites.net/index.php** per iniziare a usare l'applicazione.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere il [Centro per sviluppatori di PHP](/develop/php/).

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

