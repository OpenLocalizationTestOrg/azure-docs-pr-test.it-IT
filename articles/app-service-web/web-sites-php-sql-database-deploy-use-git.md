---
title: Creare un'app Web PHP-SQL e distribuire in Azure App Service tramite Git
description: Un'esercitazione che illustra come creare un'app Web PHP che archivia i dati nel database SQL di Azure e come usare la distribuzione Git nel servizio app di Azure.
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
ms.openlocfilehash: 0baa3eced3824fec0907ca937c594f127a2bdf8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-to-azure-app-service-using-git"></a><span data-ttu-id="06504-103">Creare un'app Web PHP-SQL e distribuire in Azure App Service tramite Git</span><span class="sxs-lookup"><span data-stu-id="06504-103">Create a PHP-SQL web app and deploy to Azure App Service using Git</span></span>
<span data-ttu-id="06504-104">Questa esercitazione illustra come creare nel [servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) un'app Web PHP che si connette al database SQL di Azure e come distribuirla tramite Git.</span><span class="sxs-lookup"><span data-stu-id="06504-104">This tutorial shows you how to create a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects to Azure SQL Database and how to deploy it using Git.</span></span> <span data-ttu-id="06504-105">In questa esercitazione si presuppone che nel computer siano installati [PHP][install-php], [SQL Server Express][install-SQLExpress], i [driver Microsoft per SQL Server per PHP](http://www.microsoft.com/download/en/details.aspx?id=20098) e [Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="06504-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], the [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="06504-106">Dopo aver completato questa guida, si disporrà di un'app Web PHP-MySQL in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="06504-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="06504-107">Per installare e configurare PHP, SQL Server Express e i driver Microsoft per SQL Server per PHP, è possibile usare l' [Installazione guidata piattaforma Web Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="06504-107">You can install and configure PHP, SQL Server Express, and the Microsoft Drivers for SQL Server for PHP using the [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="06504-108">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="06504-108">You will learn:</span></span>

* <span data-ttu-id="06504-109">Creare un'app Web di Azure e un database SQL usando il [portale di Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="06504-109">How to create an Azure web app and a SQL Database using the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="06504-110">Poiché PHP è abilitato nelle app Web di Servizio app di Azure per impostazione predefinita, non è necessario effettuare operazioni particolari per eseguire il codice PHP.</span><span class="sxs-lookup"><span data-stu-id="06504-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="06504-111">Pubblicare e ripubblicare l'applicazione in Azure tramite Git.</span><span class="sxs-lookup"><span data-stu-id="06504-111">How to publish and re-publish your application to Azure using Git.</span></span>

<span data-ttu-id="06504-112">Seguendo questa esercitazione, verrà creata una semplice applicazione Web di registrazione in PHP,</span><span class="sxs-lookup"><span data-stu-id="06504-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="06504-113">ospitata in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="06504-113">The application will be hosted in an Azure Website.</span></span> <span data-ttu-id="06504-114">Di seguito è riportata una schermata dell'applicazione completata:</span><span class="sxs-lookup"><span data-stu-id="06504-114">A screenshot of the completed application is below:</span></span>

![Sito Web PHP di Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="06504-116">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="06504-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="06504-117">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="06504-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="06504-118">Creare un'app Web di Azure e configurare la pubblicazione Git</span><span class="sxs-lookup"><span data-stu-id="06504-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="06504-119">Per creare un'app Web di Azure e un database SQL, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="06504-119">Follow these steps to create an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="06504-120">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="06504-120">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="06504-121">Aprire Azure Marketplace facendo clic sull'icona **Nuovo** in alto a sinistra nel dashboard, fare clic su **Seleziona tutto** accanto a Marketplace e quindi selezionare **Web e dispositivi mobili**.</span><span class="sxs-lookup"><span data-stu-id="06504-121">Open the Azure Marketplace by clicking the **New** icon on the top left of the dashboard, click on **Select All** next to Marketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="06504-122">Nel Marketplace selezionare **Web e dispositivi mobili**.</span><span class="sxs-lookup"><span data-stu-id="06504-122">In the Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="06504-123">Fare clic sull'icona **Web app + SQL** .</span><span class="sxs-lookup"><span data-stu-id="06504-123">Click the **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="06504-124">Dopo aver letto la descrizione dell'app Web e dell'SQL, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="06504-124">After reading the description of the Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="06504-125">Fare clic sulle singole parti, **Gruppo di risorse**, **App Web**, **Database** e **Sottoscrizione** e immettere o selezionare i valori per i campi obbligatori:</span><span class="sxs-lookup"><span data-stu-id="06504-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for the required fields:</span></span>
   
   * <span data-ttu-id="06504-126">Immettere un nome di URL a scelta.</span><span class="sxs-lookup"><span data-stu-id="06504-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="06504-127">Configurare le credenziali del server di database.</span><span class="sxs-lookup"><span data-stu-id="06504-127">Configure database server credentials</span></span>
   * <span data-ttu-id="06504-128">Selezionare l'area più vicina.</span><span class="sxs-lookup"><span data-stu-id="06504-128">Select the region closest to you</span></span>
     
     ![configurazione dell'app](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="06504-130">Al termine della definizione dell'app Web, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="06504-130">When finished defining the web app, click **Create**.</span></span>
   
    <span data-ttu-id="06504-131">Quando l'app Web viene creata, nel pulsante **Notifiche** lampeggia in verde il testo **OPERAZIONE RIUSCITA** e il pannello del gruppo di risorse si apre per visualizzare sia l'app Web sia il database SQL presenti nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="06504-131">When the web app has been created, the **Notifications** button will flash a green **SUCCESS** and the resource group blade open to show both the web app and the SQL database in the group.</span></span>
8. <span data-ttu-id="06504-132">Fare clic sull'icona dell'app Web nel pannello del gruppo di risorse per aprire il pannello dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="06504-132">Click the web app's icon in the resource group blade to open the web app's blade.</span></span>
   
    ![Gruppo di risorse per app Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="06504-134">In **Impostazioni** fare clic su **Distribuzione continua** > **Configurare le impostazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="06504-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="06504-135">Selezionare **Archivio Git locale** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="06504-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![Posizione del codice](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="06504-137">Se in precedenza non è stato configurato un repository Git, è necessario fornire nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="06504-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="06504-138">A tale scopo, fare clic su **Impostazioni** > **Credenziali per la distribuzione** nel pannello dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="06504-138">To do this, click **Settings** > **Deployment credentials** in the web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="06504-139">In **Impostazioni** fare clic su **Proprietà** per visualizzare l'URL Git remoto da usare per distribuire l'app PHP in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="06504-139">In **Settings** click on **Properties** to see the Git remote URL you need to use to deploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="06504-140">Recuperare le informazioni sulla connessione al database SQL</span><span class="sxs-lookup"><span data-stu-id="06504-140">Get SQL Database connection information</span></span>
<span data-ttu-id="06504-141">Per connettersi all'istanza del database SQL collegata all'app Web, saranno necessarie le informazioni di connessione specificate durante la creazione del database.</span><span class="sxs-lookup"><span data-stu-id="06504-141">To connect to the SQL Database instance that is linked to your web app, your will need the connection information, which you specified when you created the database.</span></span> <span data-ttu-id="06504-142">Per ottenere le informazioni di connessione al database SQL, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="06504-142">To get the SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="06504-143">Tornando nel pannello del gruppo di risorse, fare clic sull'icona del database SQL.</span><span class="sxs-lookup"><span data-stu-id="06504-143">Back in the resource group's blade, click the SQL database's icon.</span></span>
2. <span data-ttu-id="06504-144">Nel pannello del database SQL fare clic su **Impostazioni** > **Proprietà** e quindi su **Mostra stringhe di connessione del database**.</span><span class="sxs-lookup"><span data-stu-id="06504-144">In the SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Visualizzazione delle proprietà database](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="06504-146">Nella sezione **PHP** della finestra di dialogo risultante prendere nota dei valori per `Server`, `SQL Database` e `User Name`.</span><span class="sxs-lookup"><span data-stu-id="06504-146">From the **PHP** section of the resulting dialog, make note of the values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="06504-147">Si useranno questi valori successivamente, al momento di pubblicare l'app Web PHP nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="06504-147">You will use these values later when publishing your PHP web app to Azure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="06504-148">Creazione e test dell'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="06504-148">Build and test your application locally</span></span>
<span data-ttu-id="06504-149">L'applicazione di registrazione è una semplice applicazione PHP che consente di registrarsi per un evento specificando il proprio nome e l'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="06504-149">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="06504-150">Le informazioni sui registranti precedenti vengono visualizzate in una tabella.</span><span class="sxs-lookup"><span data-stu-id="06504-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="06504-151">Le informazioni sulle registrazioni vengono archiviate in un'istanza del database SQL.</span><span class="sxs-lookup"><span data-stu-id="06504-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="06504-152">L'applicazione è costituita da due file (copiare e incollare il codice disponibile di seguito):</span><span class="sxs-lookup"><span data-stu-id="06504-152">The application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="06504-153">**index.php**: consente di visualizzare un modulo per la registrazione e una tabella contenente informazioni sui registranti.</span><span class="sxs-lookup"><span data-stu-id="06504-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="06504-154">**createtable.php**: consente di creare la tabella di database SQL per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06504-154">**createtable.php**: Creates the SQL Database table for the application.</span></span> <span data-ttu-id="06504-155">Questo file verrà utilizzato una volta sola.</span><span class="sxs-lookup"><span data-stu-id="06504-155">This file will only be used once.</span></span>

<span data-ttu-id="06504-156">Per eseguire l'applicazione in locale, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="06504-156">To run the application locally, follow the steps below.</span></span> <span data-ttu-id="06504-157">Si noti che per questi passaggi si presuppone che nel computer locale siano già stati configurati PHP e SQL Server Express e che sia stata abilitata l'[estensione PDO per SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="06504-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled the [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="06504-158">Creare un database di SQL Server denominato `registration`.</span><span class="sxs-lookup"><span data-stu-id="06504-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="06504-159">A tale scopo, immettere nel prompt dei comandi `sqlcmd` i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="06504-159">You can do this from the `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="06504-160">Nella directory radice dell'applicazione creare due file: uno denominato `createtable.php` e l'altro denominato `index.php`.</span><span class="sxs-lookup"><span data-stu-id="06504-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="06504-161">Aprire il file `createtable.php` in un editor di testo o IDE e aggiungere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="06504-161">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="06504-162">Questo codice verrà usato per creare la tabella `registration_tbl` nel database `registration`.</span><span class="sxs-lookup"><span data-stu-id="06504-162">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
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
   
    <span data-ttu-id="06504-163">Si noti che è necessario aggiornare i valori per <code>$user</code> e <code>$pwd</code> con il nome utente di SQL Server locale e la password.</span><span class="sxs-lookup"><span data-stu-id="06504-163">Note that you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="06504-164">In un terminale nella directory radice dell'applicazione digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="06504-164">In a terminal at the root directory of the application type the following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="06504-165">Aprire un Web browser e andare a **http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="06504-165">Open a web browser and browse to **http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="06504-166">Verrà creata la tabella `registration_tbl` nel database.</span><span class="sxs-lookup"><span data-stu-id="06504-166">This will create the `registration_tbl` table in the database.</span></span>
6. <span data-ttu-id="06504-167">Aprire il file **index.php** in un editor di testo o IDE e aggiungere il codice HTML e CSS di base per la pagina (il codice PHP verrà aggiunto nei passaggi successivi).</span><span class="sxs-lookup"><span data-stu-id="06504-167">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
7. <span data-ttu-id="06504-168">All'interno dei tag PHP, aggiungere il codice PHP per la connessione al database.</span><span class="sxs-lookup"><span data-stu-id="06504-168">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="06504-169">Nuovamente, sarà necessario aggiornare i valori per <code>$user</code> e <code>$pwd</code> con il nome utente di MySQL locale e la password.</span><span class="sxs-lookup"><span data-stu-id="06504-169">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="06504-170">Dopo il codice di connessione al database, aggiungere il codice per l'inserimento delle informazioni di registrazione nel database.</span><span class="sxs-lookup"><span data-stu-id="06504-170">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
9. <span data-ttu-id="06504-171">Infine, dopo il codice sopra riportato, aggiungere il codice per recuperare i dati dal database.</span><span class="sxs-lookup"><span data-stu-id="06504-171">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="06504-172">A questo punto è possibile passare a **http://localhost:8000/index.php** per testare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06504-172">You can now browse to **http://localhost:8000/index.php** to test the application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="06504-173">Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="06504-173">Publish your application</span></span>
<span data-ttu-id="06504-174">Dopo aver testato l'applicazione in locale, è possibile pubblicarla nelle app Web di Servizio app di Azure tramite Git.</span><span class="sxs-lookup"><span data-stu-id="06504-174">After you have tested your application locally, you can publish it to App Service Web Apps using Git.</span></span> <span data-ttu-id="06504-175">È tuttavia necessario aggiornare innanzitutto le informazioni di connessione al database nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06504-175">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="06504-176">Usando le informazioni di connessione al database ottenute in precedenza (nella sezione **Ottenere le informazioni di connessione al database SQL**), aggiornare le seguenti informazioni in **entrambi** i file `createdatabase.php` e `index.php` con i valori appropriati:</span><span class="sxs-lookup"><span data-stu-id="06504-176">Using the database connection information you obtained earlier (in the **Get SQL Database connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="06504-177">Nel <code>$host</code>, il valore del Server deve essere preceduto da <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="06504-177">In the <code>$host</code>, the value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="06504-178">A questo punto è possibile configurare la pubblicazione Git e pubblicare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06504-178">Now, you are ready to set up Git publishing and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="06504-179">Questi passaggi sono uguali a quelli riportati alla fine della sezione precedente **Creare un'app Web di Azure e configurare la pubblicazione Git** .</span><span class="sxs-lookup"><span data-stu-id="06504-179">These are the same steps noted at the end of the **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="06504-180">Aprire GitBash (o un terminale, se Git si trova in `PATH`), passare alla directory radice dell'applicazione (la directory **registration** ) ed eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="06504-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application (the **registration** directory), and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="06504-181">Verrà richiesto di specificare la password creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06504-181">You will be prompted for the password you created earlier.</span></span>
2. <span data-ttu-id="06504-182">Passare a **http://[nome app Web].azurewebsites.net/createtable.php** per creare la tabella di database SQL per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06504-182">Browse to **http://[web app name].azurewebsites.net/createtable.php** to create the SQL database table for the application.</span></span>
3. <span data-ttu-id="06504-183">Passare a **http://[nome app Web].azurewebsites.net/index.php** per iniziare a usare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06504-183">Browse to **http://[web app name].azurewebsites.net/index.php** to begin using the application.</span></span>

<span data-ttu-id="06504-184">Dopo aver pubblicato l'applicazione, è possibile iniziare ad apportarvi modifiche e ad usare Git per pubblicarle.</span><span class="sxs-lookup"><span data-stu-id="06504-184">After you have published your application, you can begin making changes to it and use Git to publish them.</span></span> 

## <a name="publish-changes-to-your-application"></a><span data-ttu-id="06504-185">Pubblicazione delle modifiche apportate all'applicazione</span><span class="sxs-lookup"><span data-stu-id="06504-185">Publish changes to your application</span></span>
<span data-ttu-id="06504-186">Per pubblicare le modifiche apportate all'applicazione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="06504-186">To publish changes to application, follow these steps:</span></span>

1. <span data-ttu-id="06504-187">Apportare le modifiche all'applicazione in locale.</span><span class="sxs-lookup"><span data-stu-id="06504-187">Make changes to your application locally.</span></span>
2. <span data-ttu-id="06504-188">Aprire GitBash (o un terminale, se Git si trova in `PATH`), passare alla directory radice dell'applicazione ed eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="06504-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="06504-189">Verrà richiesto di specificare la password creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06504-189">You will be prompted for the password you created earlier.</span></span>
3. <span data-ttu-id="06504-190">Passare a **http://[nome app Web].azurewebsites.net/index.php** per visualizzare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="06504-190">Browse to **http://[web app name].azurewebsites.net/index.php** to see your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="06504-191">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="06504-191">What's changed</span></span>
* <span data-ttu-id="06504-192">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="06504-192">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

