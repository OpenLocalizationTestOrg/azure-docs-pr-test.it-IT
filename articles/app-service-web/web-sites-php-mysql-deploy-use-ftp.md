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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="f3462-103">Creazione di un'app Web PHP-MySQL in Servizio app di Azure e distribuzione tramite FTP</span><span class="sxs-lookup"><span data-stu-id="f3462-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="f3462-104">Questa esercitazione illustra come creare un'app Web di Azure PHP-MySQL e distribuirla tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="f3462-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span></span> <span data-ttu-id="f3462-105">A tale scopo, si presuppone che nel computer siano installati [PHP][install-php], [MySQL][install-mysql], un server Web e un client FTP.</span><span class="sxs-lookup"><span data-stu-id="f3462-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="f3462-106">Le istruzioni di questa esercitazione possono essere eseguite in qualsiasi sistema operativo, tra cui Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="f3462-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="f3462-107">Dopo aver completato questa guida, si disporrà dell'app Web PHP/MySQL in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="f3462-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="f3462-108">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f3462-108">You will learn:</span></span>

* <span data-ttu-id="f3462-109">Creare un'app Web e un database MySQL mediante il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3462-109">How to create a web app and a MySQL database using the Azure Portal.</span></span> <span data-ttu-id="f3462-110">Poiché PHP è abilitato in App Web di Azure per impostazione predefinita, non è necessario completare operazioni speciali per eseguire il codice PHP.</span><span class="sxs-lookup"><span data-stu-id="f3462-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="f3462-111">Pubblicare l'applicazione in Azure tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="f3462-111">How to publish your application to Azure using FTP.</span></span>

<span data-ttu-id="f3462-112">Seguendo questa esercitazione, verrà creata una semplice app Web di registrazione in PHP,</span><span class="sxs-lookup"><span data-stu-id="f3462-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="f3462-113">ospitata in un'app Web.</span><span class="sxs-lookup"><span data-stu-id="f3462-113">The application will be hosted in a Web App.</span></span> <span data-ttu-id="f3462-114">Di seguito è riportata una schermata dell'applicazione completata:</span><span class="sxs-lookup"><span data-stu-id="f3462-114">A screenshot of the completed application is below:</span></span>

![Sito Web PHP di Azure][running-app]

> [!NOTE]
> <span data-ttu-id="f3462-116">Per iniziare a utilizzare Servizio app di Azureprima di registrare un account di Azure, andare alla pagina di [prova di Servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare immediatamente un'app Web temporanea in Servizio app.</span><span class="sxs-lookup"><span data-stu-id="f3462-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f3462-117">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="f3462-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="f3462-118">Creare un'app Web e configurare la pubblicazione FTP</span><span class="sxs-lookup"><span data-stu-id="f3462-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="f3462-119">Per creare un'app Web e un database MySQL, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f3462-119">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="f3462-120">Eseguire l'accesso al [portale di Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="f3462-120">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="f3462-121">Fare clic sull'icona **+Nuovo** nella parte superiore sinistra del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3462-121">Click the **+ New** icon on the top left of the Azure Portal.</span></span>
   
    ![Creazione di un nuovo sito Web di Azure][new-website]
3. <span data-ttu-id="f3462-123">Nella casella di ricerca digitare **App Web e MySQL** e fare clic su **App Web e MySQL**.</span><span class="sxs-lookup"><span data-stu-id="f3462-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Creazione personalizzata di un nuovo sito Web][custom-create]
4. <span data-ttu-id="f3462-125">Fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="f3462-125">Click **Create**.</span></span> <span data-ttu-id="f3462-126">Immettere un nome di servizio app univoco, un nome valido per il gruppo di risorse e un nuovo piano di servizio.</span><span class="sxs-lookup"><span data-stu-id="f3462-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span></span>
   
    ![Gruppo di risorse denominato ADF.][resource-group]
5. <span data-ttu-id="f3462-128">Immettere i valori per il nuovo database e accettare termini e condizioni.</span><span class="sxs-lookup"><span data-stu-id="f3462-128">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Creazione di un nuovo database MySQL][new-mysql-db]
6. <span data-ttu-id="f3462-130">Una volta creata l'app Web, verrà visualizzato il pannello del nuovo servizio app.</span><span class="sxs-lookup"><span data-stu-id="f3462-130">When the web app has been created, you will see the new app service blade.</span></span>
7. <span data-ttu-id="f3462-131">Fare clic su **Impostazioni** > **Credenziali di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="f3462-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Reimpostare le credenziali di distribuzione][set-deployment-credentials]
8. <span data-ttu-id="f3462-133">Per abilitare la pubblicazione FTP è necessario specificare un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="f3462-133">To enable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="f3462-134">Salvare le credenziali e prendere nota del nome utente e della password creati.</span><span class="sxs-lookup"><span data-stu-id="f3462-134">Save the credentials and make a note of the user name and password you create.</span></span>
   
    ![Creazione di credenziali di pubblicazione][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="f3462-136">Creare e verificare l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="f3462-136">Build and test your app locally</span></span>
<span data-ttu-id="f3462-137">L'applicazione di registrazione è una semplice applicazione PHP che consente di registrarsi per un evento specificando il proprio nome e l'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="f3462-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="f3462-138">Le informazioni sui registranti precedenti vengono visualizzate in una tabella.</span><span class="sxs-lookup"><span data-stu-id="f3462-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="f3462-139">Le informazioni sulle registrazioni vengono archiviate in un database MySQL.</span><span class="sxs-lookup"><span data-stu-id="f3462-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="f3462-140">L'applicazione è costituita da due file:</span><span class="sxs-lookup"><span data-stu-id="f3462-140">The app consists of two files:</span></span>

* <span data-ttu-id="f3462-141">**index.php**: consente di visualizzare un modulo per la registrazione e una tabella contenente informazioni sui registranti.</span><span class="sxs-lookup"><span data-stu-id="f3462-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="f3462-142">**createtable.php**: consente di creare la tabella MySQL per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3462-142">**createtable.php**: Creates the MySQL table for the application.</span></span> <span data-ttu-id="f3462-143">Questo file verrà utilizzato una volta sola.</span><span class="sxs-lookup"><span data-stu-id="f3462-143">This file will only be used once.</span></span>

<span data-ttu-id="f3462-144">Per creare ed eseguire l'app in locale, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="f3462-144">To build and run the app locally, follow the steps below.</span></span> <span data-ttu-id="f3462-145">Si noti che per questi passaggi si presuppone che nel computer locale siano già stati configurati PHP, MySQL e un server Web e che sia stata abilitata l'[estensione PDO per MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="f3462-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="f3462-146">Creare un database MySQL denominato `registration`.</span><span class="sxs-lookup"><span data-stu-id="f3462-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="f3462-147">A tale scopo, immettere al prompt dei comandi MySQL il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f3462-147">You can do this from the MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="f3462-148">Nella directory radice del server Web creare una cartella denominata `registration` e al suo interno creare due file: uno denominato `createtable.php` e l'altro denominato `index.php`.</span><span class="sxs-lookup"><span data-stu-id="f3462-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="f3462-149">Aprire il file `createtable.php` in un editor di testo o IDE e aggiungere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="f3462-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="f3462-150">Questo codice verrà usato per creare la tabella `registration_tbl` nel database `registration`.</span><span class="sxs-lookup"><span data-stu-id="f3462-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
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
   > <span data-ttu-id="f3462-151">È necessario aggiornare i valori per <code>$user</code> e <code>$pwd</code> con il nome utente di MySQL locale e la password.</span><span class="sxs-lookup"><span data-stu-id="f3462-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="f3462-152">Aprire un Web browser e passare a [http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="f3462-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="f3462-153">Verrà creata la tabella `registration_tbl` nel database.</span><span class="sxs-lookup"><span data-stu-id="f3462-153">This will create the `registration_tbl` table in the database.</span></span>
5. <span data-ttu-id="f3462-154">Aprire il file **index.php** in un editor di testo o IDE e aggiungere il codice HTML e CSS di base per la pagina (il codice PHP verrà aggiunto nei passaggi successivi).</span><span class="sxs-lookup"><span data-stu-id="f3462-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="f3462-155">All'interno dei tag PHP, aggiungere il codice PHP per la connessione al database.</span><span class="sxs-lookup"><span data-stu-id="f3462-155">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
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
   > <span data-ttu-id="f3462-156">Nuovamente, sarà necessario aggiornare i valori per <code>$user</code> e <code>$pwd</code> con il nome utente di MySQL locale e la password.</span><span class="sxs-lookup"><span data-stu-id="f3462-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="f3462-157">Dopo il codice di connessione al database, aggiungere il codice per l'inserimento delle informazioni di registrazione nel database.</span><span class="sxs-lookup"><span data-stu-id="f3462-157">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
8. <span data-ttu-id="f3462-158">Infine, dopo il codice sopra riportato, aggiungere il codice per recuperare i dati dal database.</span><span class="sxs-lookup"><span data-stu-id="f3462-158">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="f3462-159">A questo punto è possibile passare a [http://localhost/registration/index.php][localhost-index] per testare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3462-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="f3462-160">Recupero di informazioni sulla connessione a MySQL ed FTP</span><span class="sxs-lookup"><span data-stu-id="f3462-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="f3462-161">Per connettersi al database MySQL in esecuzione in App Web, saranno necessarie le informazioni sulla connessione.</span><span class="sxs-lookup"><span data-stu-id="f3462-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="f3462-162">Per recuperare le informazioni sulla connessione a MySQL, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f3462-162">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="f3462-163">Nel pannello dell'app Web del servizio app fare clic sul collegamento Gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="f3462-163">From the app service web app blade click on the resource group link:</span></span>
   
    ![Selezionare Gruppo di risorse][select-resourcegroup]
2. <span data-ttu-id="f3462-165">Dal gruppo di risorse, fare clic sul database:</span><span class="sxs-lookup"><span data-stu-id="f3462-165">From your resource group, click the database:</span></span>
   
    ![Selezionare il database][select-database]
3. <span data-ttu-id="f3462-167">Nel riepilogo del database selezionare **Impostazioni** > **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="f3462-167">From the database summary, select **Settings** > **Properties**.</span></span>
   
    ![Selezionare le proprietà][select-properties]
4. <span data-ttu-id="f3462-169">Prendere nota dei valori di `Database`, `Host`, `User Id` e `Password`.</span><span class="sxs-lookup"><span data-stu-id="f3462-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Proprietà nota][note-properties]
5. <span data-ttu-id="f3462-171">Dall'app Web fare clic sul collegamento **Scarica profilo di pubblicazione** nell'angolo in basso a destra della pagina:</span><span class="sxs-lookup"><span data-stu-id="f3462-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span></span>
   
    ![Scarica profilo di pubblicazione][download-publish-profile]
6. <span data-ttu-id="f3462-173">Aprire il file `.publishsettings` in un editor XML.</span><span class="sxs-lookup"><span data-stu-id="f3462-173">Open the `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="f3462-174">Trovare l'elemento `<publishProfile >` con `publishMethod="FTP"` che abbia un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f3462-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="f3462-175">Prendere nota degli attributi `publishUrl`, `userName` e `userPWD`.</span><span class="sxs-lookup"><span data-stu-id="f3462-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="f3462-176">Pubblicare l'app</span><span class="sxs-lookup"><span data-stu-id="f3462-176">Publish your app</span></span>
<span data-ttu-id="f3462-177">Dopo aver verificato l'app in locale è possibile pubblicarla nell'app Web tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="f3462-177">After you have tested your app locally, you can publish it to your web app using FTP.</span></span> <span data-ttu-id="f3462-178">È tuttavia necessario aggiornare innanzitutto le informazioni di connessione al database nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3462-178">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="f3462-179">Usando le informazioni di connessione al database ottenute in precedenza (nella sezione **Recuperare le informazioni sulla connessione a MySQL ed FTP**) aggiornare le informazioni seguenti in **entrambi** i file `createdatabase.php` e `index.php` con i valori appropriati:</span><span class="sxs-lookup"><span data-stu-id="f3462-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="f3462-180">A questo punto è possibile pubblicare l'app tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="f3462-180">Now you are ready to publish your app using FTP.</span></span>

1. <span data-ttu-id="f3462-181">Aprire il client FTP preferito.</span><span class="sxs-lookup"><span data-stu-id="f3462-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="f3462-182">Immettere nel client FTP la *parte di nome host* dell'attributo `publishUrl` precedentemente annotato.</span><span class="sxs-lookup"><span data-stu-id="f3462-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="f3462-183">Immettere gli attributi `userName` e `userPWD` precedentemente annotati, senza modifiche, nel client FTP.</span><span class="sxs-lookup"><span data-stu-id="f3462-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="f3462-184">Stabilire una connessione.</span><span class="sxs-lookup"><span data-stu-id="f3462-184">Establish a connection.</span></span>

<span data-ttu-id="f3462-185">Dopo aver effettuato la connessione si sarà in grado di caricare e scaricare i file in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="f3462-185">After you have connected you will be able to upload and download files as needed.</span></span> <span data-ttu-id="f3462-186">Assicurarsi di caricare i file nella directory radice, ossia `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="f3462-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="f3462-187">Dopo aver caricato `index.php` e `createtable.php`, passare a **http://[nome sito].azurewebsites.net/createtable.php** per creare la tabella MySQL per l'applicazione, quindi passare a **http://[nome sito].azurewebsites.net/index.php** per iniziare a usare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3462-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3462-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f3462-188">Next steps</span></span>
<span data-ttu-id="f3462-189">Per ulteriori informazioni, vedere il [Centro per sviluppatori di PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f3462-189">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

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

