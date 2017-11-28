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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="08dbf-103">Creazione di un'app Web PHP-MySQL in Servizio app di Azure e distribuzione tramite FTP</span><span class="sxs-lookup"><span data-stu-id="08dbf-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="08dbf-104">Questa esercitazione Mostra l'app web toocreate PHP, MySQL e la modalità toodeploy tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="08dbf-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it using FTP.</span></span> <span data-ttu-id="08dbf-105">A tale scopo, si presuppone che nel computer siano installati [PHP][install-php], [MySQL][install-mysql], un server Web e un client FTP.</span><span class="sxs-lookup"><span data-stu-id="08dbf-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="08dbf-106">istruzioni di Hello in questa esercitazione possono essere seguite su qualsiasi sistema operativo, tra cui Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="08dbf-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="08dbf-107">Dopo aver completato questa guida, si disporrà dell'app Web PHP/MySQL in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="08dbf-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="08dbf-108">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="08dbf-108">You will learn:</span></span>

* <span data-ttu-id="08dbf-109">Come toocreate un'app web e MySQL database utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="08dbf-109">How toocreate a web app and a MySQL database using hello Azure Portal.</span></span> <span data-ttu-id="08dbf-110">Poiché per impostazione predefinita, PHP è abilitato nelle App Web, niente di speciale è obbligatorio toorun codice PHP.</span><span class="sxs-lookup"><span data-stu-id="08dbf-110">Because PHP is enabled in Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="08dbf-111">Come toopublish tooAzure applicazione utilizzando FTP.</span><span class="sxs-lookup"><span data-stu-id="08dbf-111">How toopublish your application tooAzure using FTP.</span></span>

<span data-ttu-id="08dbf-112">Seguendo questa esercitazione, verrà creata una semplice app Web di registrazione in PHP,</span><span class="sxs-lookup"><span data-stu-id="08dbf-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="08dbf-113">un'applicazione Hello verrà ospitata in un'App Web.</span><span class="sxs-lookup"><span data-stu-id="08dbf-113">hello application will be hosted in a Web App.</span></span> <span data-ttu-id="08dbf-114">Di seguito viene riportata una schermata dell'applicazione hello completata:</span><span class="sxs-lookup"><span data-stu-id="08dbf-114">A screenshot of hello completed application is below:</span></span>

![Sito Web PHP di Azure][running-app]

> [!NOTE]
> <span data-ttu-id="08dbf-116">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account, Vai troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="08dbf-116">If you want tooget started with Azure App Service before signing up for an account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="08dbf-117">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="08dbf-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="08dbf-118">Creare un'app Web e configurare la pubblicazione FTP</span><span class="sxs-lookup"><span data-stu-id="08dbf-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="08dbf-119">Seguire questi passaggi toocreate un'app web e un database MySQL:</span><span class="sxs-lookup"><span data-stu-id="08dbf-119">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="08dbf-120">Account di accesso toohello [portale Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="08dbf-120">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="08dbf-121">Fare clic su hello **+ nuovo** sull'icona nella parte superiore di hello a sinistra della hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="08dbf-121">Click hello **+ New** icon on hello top left of hello Azure Portal.</span></span>
   
    ![Creazione di un nuovo sito Web di Azure][new-website]
3. <span data-ttu-id="08dbf-123">In tipo di ricerca hello **Web app + MySQL** e fare clic su **Web app + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="08dbf-123">In hello search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Creazione personalizzata di un nuovo sito Web][custom-create]
4. <span data-ttu-id="08dbf-125">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="08dbf-125">Click **Create**.</span></span> <span data-ttu-id="08dbf-126">Immettere un nome di servizio app univoco, un nome valido per il gruppo di risorse hello e un nuovo piano di servizio.</span><span class="sxs-lookup"><span data-stu-id="08dbf-126">Enter a unique app service name, a valid name for hello resource group and a new service plan.</span></span>
   
    ![Gruppo di risorse denominato ADF.][resource-group]
5. <span data-ttu-id="08dbf-128">Immettere i valori per il nuovo database, tra cui accettano toohello legali.</span><span class="sxs-lookup"><span data-stu-id="08dbf-128">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Creazione di un nuovo database MySQL][new-mysql-db]
6. <span data-ttu-id="08dbf-130">Quando hello web app è stata creata, verrà visualizzato il pannello nuova app servizio hello.</span><span class="sxs-lookup"><span data-stu-id="08dbf-130">When hello web app has been created, you will see hello new app service blade.</span></span>
7. <span data-ttu-id="08dbf-131">Fare clic su **Impostazioni** > **Credenziali di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="08dbf-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Reimpostare le credenziali di distribuzione][set-deployment-credentials]
8. <span data-ttu-id="08dbf-133">tooenable pubblicazione tramite FTP, è necessario fornire un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="08dbf-133">tooenable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="08dbf-134">Salvare le credenziali di hello e prendere nota del nome utente hello e la password creata.</span><span class="sxs-lookup"><span data-stu-id="08dbf-134">Save hello credentials and make a note of hello user name and password you create.</span></span>
   
    ![Creazione di credenziali di pubblicazione][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="08dbf-136">Creare e verificare l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="08dbf-136">Build and test your app locally</span></span>
<span data-ttu-id="08dbf-137">applicazione di registrazione Hello è una semplice applicazione PHP che consente di tooregister per un evento, fornendo il nome e l'indirizzo e-mail.</span><span class="sxs-lookup"><span data-stu-id="08dbf-137">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="08dbf-138">Le informazioni sui registranti precedenti vengono visualizzate in una tabella.</span><span class="sxs-lookup"><span data-stu-id="08dbf-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="08dbf-139">Le informazioni sulle registrazioni vengono archiviate in un database MySQL.</span><span class="sxs-lookup"><span data-stu-id="08dbf-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="08dbf-140">app Hello è costituita da due file:</span><span class="sxs-lookup"><span data-stu-id="08dbf-140">hello app consists of two files:</span></span>

* <span data-ttu-id="08dbf-141">**index.php**: consente di visualizzare un modulo per la registrazione e una tabella contenente informazioni sui registranti.</span><span class="sxs-lookup"><span data-stu-id="08dbf-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="08dbf-142">**CreateTable.PHP**: Crea tabella di MySQL hello per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="08dbf-142">**createtable.php**: Creates hello MySQL table for hello application.</span></span> <span data-ttu-id="08dbf-143">Questo file verrà utilizzato una volta sola.</span><span class="sxs-lookup"><span data-stu-id="08dbf-143">This file will only be used once.</span></span>

<span data-ttu-id="08dbf-144">toobuild e app hello esecuzione in locale, eseguire le operazioni di hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="08dbf-144">toobuild and run hello app locally, follow hello steps below.</span></span> <span data-ttu-id="08dbf-145">Si noti che questi passaggi presuppongono che si dispone di PHP, MySQL e un server web configurato nel computer locale, e che è stata attivata hello [estensione PDO per MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="08dbf-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="08dbf-146">Creare un database MySQL denominato `registration`.</span><span class="sxs-lookup"><span data-stu-id="08dbf-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="08dbf-147">È possibile farlo dal prompt dei comandi di MySQL hello con questo comando:</span><span class="sxs-lookup"><span data-stu-id="08dbf-147">You can do this from hello MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="08dbf-148">Nella directory radice del server Web creare una cartella denominata `registration` e al suo interno creare due file: uno denominato `createtable.php` e l'altro denominato `index.php`.</span><span class="sxs-lookup"><span data-stu-id="08dbf-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="08dbf-149">Aprire hello `createtable.php` file in un editor di testo o un IDE e aggiungere codice hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="08dbf-149">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="08dbf-150">Questo codice sarà utilizzato toocreate hello `registration_tbl` tabella hello `registration` database.</span><span class="sxs-lookup"><span data-stu-id="08dbf-150">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
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
   > <span data-ttu-id="08dbf-151">È necessario che i valori hello tooupdate per <code>$user</code> e <code>$pwd</code> con il nome utente di MySQL locale e la password.</span><span class="sxs-lookup"><span data-stu-id="08dbf-151">You will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="08dbf-152">Aprire un web browser e passare troppo[http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="08dbf-152">Open a web browser and browse too[http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="08dbf-153">Verrà creata hello `registration_tbl` tabella nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="08dbf-153">This will create hello `registration_tbl` table in hello database.</span></span>
5. <span data-ttu-id="08dbf-154">Aprire hello **index.php** file in un editor di testo o un IDE e aggiungere hello base codice HTML e CSS per la pagina hello (hello codice PHP aggiunto nei passaggi successivi).</span><span class="sxs-lookup"><span data-stu-id="08dbf-154">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="08dbf-155">All'interno dei tag PHP hello, aggiungere il codice PHP per la connessione database toohello.</span><span class="sxs-lookup"><span data-stu-id="08dbf-155">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
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
   > <span data-ttu-id="08dbf-156">Nuovamente, sarà necessario valori hello tooupdate per <code>$user</code> e <code>$pwd</code> con il nome utente di MySQL locale e la password.</span><span class="sxs-lookup"><span data-stu-id="08dbf-156">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="08dbf-157">Il seguente codice di connessione database hello, aggiungere il codice per l'inserimento di informazioni di registrazione nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="08dbf-157">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
8. <span data-ttu-id="08dbf-158">Infine, il seguente codice hello precedente, aggiungere il codice per recuperare dati dal database hello.</span><span class="sxs-lookup"><span data-stu-id="08dbf-158">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="08dbf-159">È possibile cercare troppo[http://localhost/registration/index.php] [ localhost-index] tootest hello app.</span><span class="sxs-lookup"><span data-stu-id="08dbf-159">You can now browse too[http://localhost/registration/index.php][localhost-index] tootest hello app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="08dbf-160">Recupero di informazioni sulla connessione a MySQL ed FTP</span><span class="sxs-lookup"><span data-stu-id="08dbf-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="08dbf-161">database MySQL tooconnect toohello in cui è in esecuzione in applicazioni Web, sarà necessario hello informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="08dbf-161">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="08dbf-162">tooget informazioni di connessione MySQL, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="08dbf-162">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="08dbf-163">Servizio app hello pannello app web fare clic sul collegamento di gruppo di risorse hello:</span><span class="sxs-lookup"><span data-stu-id="08dbf-163">From hello app service web app blade click on hello resource group link:</span></span>
   
    ![Selezionare Gruppo di risorse][select-resourcegroup]
2. <span data-ttu-id="08dbf-165">Il gruppo di risorse, fare clic su database hello:</span><span class="sxs-lookup"><span data-stu-id="08dbf-165">From your resource group, click hello database:</span></span>
   
    ![Selezionare il database][select-database]
3. <span data-ttu-id="08dbf-167">Database hello riepilogo, selezionare **impostazioni** > **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="08dbf-167">From hello database summary, select **Settings** > **Properties**.</span></span>
   
    ![Selezionare le proprietà][select-properties]
4. <span data-ttu-id="08dbf-169">Prendere nota dei valori di hello per `Database`, `Host`, `User Id`, e `Password`.</span><span class="sxs-lookup"><span data-stu-id="08dbf-169">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Proprietà nota][note-properties]
5. <span data-ttu-id="08dbf-171">Dall'app web, fare clic su hello **Scarica profilo di pubblicazione** collegamento hello angolo in basso a destra della pagina hello:</span><span class="sxs-lookup"><span data-stu-id="08dbf-171">From your web app, click hello **Download publish profile** link at hello bottom right corner of hello page:</span></span>
   
    ![Scarica profilo di pubblicazione][download-publish-profile]
6. <span data-ttu-id="08dbf-173">Aprire hello `.publishsettings` file in un editor XML.</span><span class="sxs-lookup"><span data-stu-id="08dbf-173">Open hello `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="08dbf-174">Trovare hello `<publishProfile >` elemento con `publishMethod="FTP"` che ricerca toothis simile:</span><span class="sxs-lookup"><span data-stu-id="08dbf-174">Find hello `<publishProfile >` element with `publishMethod="FTP"` that looks similar toothis:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="08dbf-175">Prendere nota di hello `publishUrl`, `userName`, e `userPWD` gli attributi.</span><span class="sxs-lookup"><span data-stu-id="08dbf-175">Make note of hello `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="08dbf-176">Pubblicare l'app</span><span class="sxs-lookup"><span data-stu-id="08dbf-176">Publish your app</span></span>
<span data-ttu-id="08dbf-177">Dopo aver testato l'app localmente, è possibile pubblicare app web tooyour tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="08dbf-177">After you have tested your app locally, you can publish it tooyour web app using FTP.</span></span> <span data-ttu-id="08dbf-178">Tuttavia, è necessario innanzitutto informazioni di connessione di database tooupdate hello in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="08dbf-178">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="08dbf-179">Utilizzando le informazioni di connessione database hello ottenuti in precedenza (in hello **le informazioni di connessione FTP e di ottenere MySQL** sezione), aggiornamento hello le seguenti informazioni in **entrambi** hello `createdatabase.php` e `index.php` i file con hello valori appropriati:</span><span class="sxs-lookup"><span data-stu-id="08dbf-179">Using hello database connection information you obtained earlier (in hello **Get MySQL and FTP connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="08dbf-180">È ora pronto toopublish app tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="08dbf-180">Now you are ready toopublish your app using FTP.</span></span>

1. <span data-ttu-id="08dbf-181">Aprire il client FTP preferito.</span><span class="sxs-lookup"><span data-stu-id="08dbf-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="08dbf-182">Immettere hello *parte del nome host* da hello `publishUrl` attributo è indicato in precedenza nel client FTP.</span><span class="sxs-lookup"><span data-stu-id="08dbf-182">Enter hello *host name portion* from hello `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="08dbf-183">Immettere hello `userName` e `userPWD` invariata attributi è indicato in precedenza nel client FTP.</span><span class="sxs-lookup"><span data-stu-id="08dbf-183">Enter hello `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="08dbf-184">Stabilire una connessione.</span><span class="sxs-lookup"><span data-stu-id="08dbf-184">Establish a connection.</span></span>

<span data-ttu-id="08dbf-185">Dopo avere stabilito la connessione verrà essere in grado di tooupload e scaricare i file in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="08dbf-185">After you have connected you will be able tooupload and download files as needed.</span></span> <span data-ttu-id="08dbf-186">Assicurarsi che si sta caricando file toohello radice, ovvero `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="08dbf-186">Be sure that you are uploading files toohello root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="08dbf-187">Dopo il caricamento sia `index.php` e `createtable.php`, Sfoglia troppo**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL per un'applicazione hello di tabella, quindi individuare troppo**http://[site nome ].azurewebsites.net/index.php** toobegin utilizzando un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="08dbf-187">After uploading both `index.php` and `createtable.php`, browse too**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL table for hello application, then browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08dbf-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08dbf-188">Next steps</span></span>
<span data-ttu-id="08dbf-189">Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="08dbf-189">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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

