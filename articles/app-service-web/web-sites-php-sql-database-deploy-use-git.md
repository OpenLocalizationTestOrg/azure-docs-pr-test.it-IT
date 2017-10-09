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
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a><span data-ttu-id="6462d-103">Creare un'app web SQL PHP e distribuire tooAzure servizio App tramite Git</span><span class="sxs-lookup"><span data-stu-id="6462d-103">Create a PHP-SQL web app and deploy tooAzure App Service using Git</span></span>
<span data-ttu-id="6462d-104">Questa esercitazione viene illustrato come toocreate PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) che si connette tooAzure Database SQL e come toodeploy tramite Git.</span><span class="sxs-lookup"><span data-stu-id="6462d-104">This tutorial shows you how toocreate a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects tooAzure SQL Database and how toodeploy it using Git.</span></span> <span data-ttu-id="6462d-105">Questa esercitazione presuppone l'esistenza [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server per PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), e [Git] [ install-git] installato nel computer.</span><span class="sxs-lookup"><span data-stu-id="6462d-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="6462d-106">Dopo aver completato questa guida, si disporrà di un'app Web PHP-MySQL in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="6462d-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="6462d-107">È possibile installare e configurare Microsoft Drivers hello, SQL Server Express e PHP per SQL Server per PHP con hello [installazione guidata piattaforma Web di Microsoft](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="6462d-107">You can install and configure PHP, SQL Server Express, and hello Microsoft Drivers for SQL Server for PHP using hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="6462d-108">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6462d-108">You will learn:</span></span>

* <span data-ttu-id="6462d-109">Come toocreate di Azure web app e un Database SQL tramite hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="6462d-109">How toocreate an Azure web app and a SQL Database using hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="6462d-110">Poiché per impostazione predefinita, PHP è abilitata nell'App del servizio Web App, niente di speciale è obbligatorio toorun codice PHP.</span><span class="sxs-lookup"><span data-stu-id="6462d-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="6462d-111">Come toopublish e pubblicare nuovamente l'applicazione tooAzure tramite Git.</span><span class="sxs-lookup"><span data-stu-id="6462d-111">How toopublish and re-publish your application tooAzure using Git.</span></span>

<span data-ttu-id="6462d-112">Seguendo questa esercitazione, verrà creata una semplice applicazione Web di registrazione in PHP,</span><span class="sxs-lookup"><span data-stu-id="6462d-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="6462d-113">un'applicazione Hello verrà ospitata in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="6462d-113">hello application will be hosted in an Azure Website.</span></span> <span data-ttu-id="6462d-114">Di seguito viene riportata una schermata dell'applicazione hello completata:</span><span class="sxs-lookup"><span data-stu-id="6462d-114">A screenshot of hello completed application is below:</span></span>

![Sito Web PHP di Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="6462d-116">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="6462d-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6462d-117">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="6462d-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="6462d-118">Creare un'app Web di Azure e configurare la pubblicazione Git</span><span class="sxs-lookup"><span data-stu-id="6462d-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="6462d-119">Seguire questi toocreate passaggi un'app web di Azure e un Database SQL:</span><span class="sxs-lookup"><span data-stu-id="6462d-119">Follow these steps toocreate an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="6462d-120">Accedi toohello [portale Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6462d-120">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6462d-121">Aprire hello Azure Marketplace facendo hello **New** sull'icona nella parte superiore di hello a sinistra della dashboard hello, fare clic su **Seleziona tutto** tooMarketplace avanti e selezionando **Web e dispositivi mobili**.</span><span class="sxs-lookup"><span data-stu-id="6462d-121">Open hello Azure Marketplace by clicking hello **New** icon on hello top left of hello dashboard, click on **Select All** next tooMarketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="6462d-122">Nel Marketplace hello, selezionare **Web e dispositivi mobili**.</span><span class="sxs-lookup"><span data-stu-id="6462d-122">In hello Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="6462d-123">Fare clic su hello **Web app + SQL** icona.</span><span class="sxs-lookup"><span data-stu-id="6462d-123">Click hello **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="6462d-124">Dopo aver letto descrizione hello di app Web hello + SQL app, selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="6462d-124">After reading hello description of hello Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="6462d-125">Fare clic su ogni parte (**gruppo di risorse**, **App Web**, **Database**, e **sottoscrizione**) e immettere o selezionare i valori per hello richiesto campi:</span><span class="sxs-lookup"><span data-stu-id="6462d-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for hello required fields:</span></span>
   
   * <span data-ttu-id="6462d-126">Immettere un nome di URL a scelta.</span><span class="sxs-lookup"><span data-stu-id="6462d-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="6462d-127">Configurare le credenziali del server di database.</span><span class="sxs-lookup"><span data-stu-id="6462d-127">Configure database server credentials</span></span>
   * <span data-ttu-id="6462d-128">Selezionare hello area più vicina tooyou</span><span class="sxs-lookup"><span data-stu-id="6462d-128">Select hello region closest tooyou</span></span>
     
     ![configurazione dell'app](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="6462d-130">Al termine definizione hello web app, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="6462d-130">When finished defining hello web app, click **Create**.</span></span>
   
    <span data-ttu-id="6462d-131">Quando hello web app è stata creata, hello **notifiche** pulsante farà lampeggiare una verde **successo** e hello tooshow aprire Pannello gruppo di risorse sia hello web app e hello SQL database nel gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-131">When hello web app has been created, hello **Notifications** button will flash a green **SUCCESS** and hello resource group blade open tooshow both hello web app and hello SQL database in hello group.</span></span>
8. <span data-ttu-id="6462d-132">Fare clic sull'icona dell'app web hello nel pannello hello risorsa gruppo blade tooopen hello dell'app web.</span><span class="sxs-lookup"><span data-stu-id="6462d-132">Click hello web app's icon in hello resource group blade tooopen hello web app's blade.</span></span>
   
    ![Gruppo di risorse per app Web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="6462d-134">In **Impostazioni** fare clic su **Distribuzione continua** > **Configurare le impostazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="6462d-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="6462d-135">Selezionare **Archivio Git locale** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6462d-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![Posizione del codice](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="6462d-137">Se in precedenza non è stato configurato un repository Git, è necessario fornire nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="6462d-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="6462d-138">toodo, fare clic su **impostazioni** > **le credenziali di distribuzione** nel pannello dell'app web hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-138">toodo this, click **Settings** > **Deployment credentials** in hello web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="6462d-139">In **impostazioni** fare clic su **proprietà** toosee hello Git URL remoto è necessario toouse toodeploy app PHP in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6462d-139">In **Settings** click on **Properties** toosee hello Git remote URL you need toouse toodeploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="6462d-140">Recuperare le informazioni sulla connessione al database SQL</span><span class="sxs-lookup"><span data-stu-id="6462d-140">Get SQL Database connection information</span></span>
<span data-ttu-id="6462d-141">istanza del Database SQL toohello tooconnect che è collegato tooyour web app, sarà necessario hello informazioni di connessione, specificato al momento della creazione del database hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-141">tooconnect toohello SQL Database instance that is linked tooyour web app, your will need hello connection information, which you specified when you created hello database.</span></span> <span data-ttu-id="6462d-142">hello tooget informazioni di connessione al Database SQL, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="6462d-142">tooget hello SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="6462d-143">Nel pannello del gruppo di risorse hello, fare clic sull'icona del database SQL di hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-143">Back in hello resource group's blade, click hello SQL database's icon.</span></span>
2. <span data-ttu-id="6462d-144">Nel pannello del database SQL di hello, fare clic su **impostazioni** > **proprietà**, quindi fare clic su **Mostra le stringhe di connessione di database**.</span><span class="sxs-lookup"><span data-stu-id="6462d-144">In hello SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Visualizzazione delle proprietà database](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="6462d-146">Da hello **PHP** sezione della finestra di dialogo risultante hello, prendere nota dei valori di hello per `Server`, `SQL Database`, e `User Name`.</span><span class="sxs-lookup"><span data-stu-id="6462d-146">From hello **PHP** section of hello resulting dialog, make note of hello values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="6462d-147">Utilizzare questi valori in un secondo momento quando la pubblicazione del tooAzure di app web PHP servizio App.</span><span class="sxs-lookup"><span data-stu-id="6462d-147">You will use these values later when publishing your PHP web app tooAzure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="6462d-148">Creazione e test dell'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="6462d-148">Build and test your application locally</span></span>
<span data-ttu-id="6462d-149">applicazione di registrazione Hello è una semplice applicazione PHP che consente di tooregister per un evento, fornendo il nome e l'indirizzo e-mail.</span><span class="sxs-lookup"><span data-stu-id="6462d-149">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="6462d-150">Le informazioni sui registranti precedenti vengono visualizzate in una tabella.</span><span class="sxs-lookup"><span data-stu-id="6462d-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="6462d-151">Le informazioni sulle registrazioni vengono archiviate in un'istanza del database SQL.</span><span class="sxs-lookup"><span data-stu-id="6462d-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="6462d-152">un'applicazione Hello è costituito da due file (copiare e incollare codice riportato di seguito):</span><span class="sxs-lookup"><span data-stu-id="6462d-152">hello application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="6462d-153">**index.php**: consente di visualizzare un modulo per la registrazione e una tabella contenente informazioni sui registranti.</span><span class="sxs-lookup"><span data-stu-id="6462d-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="6462d-154">**CreateTable.PHP**: Crea tabella di Database SQL di hello per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-154">**createtable.php**: Creates hello SQL Database table for hello application.</span></span> <span data-ttu-id="6462d-155">Questo file verrà utilizzato una volta sola.</span><span class="sxs-lookup"><span data-stu-id="6462d-155">This file will only be used once.</span></span>

<span data-ttu-id="6462d-156">in locale, un'applicazione hello toorun procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="6462d-156">toorun hello application locally, follow hello steps below.</span></span> <span data-ttu-id="6462d-157">Si noti che questi passaggi presuppongono che si dispone di PHP e SQL Server Express impostare sul computer locale e che è stata attivata hello [estensione PDO per SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="6462d-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled hello [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="6462d-158">Creare un database di SQL Server denominato `registration`.</span><span class="sxs-lookup"><span data-stu-id="6462d-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="6462d-159">È possibile farlo da hello `sqlcmd` prompt dei comandi con questi comandi:</span><span class="sxs-lookup"><span data-stu-id="6462d-159">You can do this from hello `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="6462d-160">Nella directory radice dell'applicazione creare due file: uno denominato `createtable.php` e l'altro denominato `index.php`.</span><span class="sxs-lookup"><span data-stu-id="6462d-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="6462d-161">Aprire hello `createtable.php` file in un editor di testo o un IDE e aggiungere codice hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6462d-161">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="6462d-162">Questo codice sarà utilizzato toocreate hello `registration_tbl` tabella hello `registration` database.</span><span class="sxs-lookup"><span data-stu-id="6462d-162">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
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
   
    <span data-ttu-id="6462d-163">Si noti che sono necessari valori hello tooupdate per <code>$user</code> e <code>$pwd</code> con il nome utente di SQL Server locale e la password.</span><span class="sxs-lookup"><span data-stu-id="6462d-163">Note that you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="6462d-164">In un terminal alla directory radice hello di hello di tipo applicazione hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6462d-164">In a terminal at hello root directory of hello application type hello following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="6462d-165">Aprire un web browser e passare troppo**http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="6462d-165">Open a web browser and browse too**http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="6462d-166">Verrà creata hello `registration_tbl` tabella nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-166">This will create hello `registration_tbl` table in hello database.</span></span>
6. <span data-ttu-id="6462d-167">Aprire hello **index.php** file in un editor di testo o un IDE e aggiungere hello base codice HTML e CSS per la pagina hello (hello codice PHP aggiunto nei passaggi successivi).</span><span class="sxs-lookup"><span data-stu-id="6462d-167">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
7. <span data-ttu-id="6462d-168">All'interno dei tag PHP hello, aggiungere il codice PHP per la connessione database toohello.</span><span class="sxs-lookup"><span data-stu-id="6462d-168">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
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
   
    <span data-ttu-id="6462d-169">Nuovamente, sarà necessario valori hello tooupdate per <code>$user</code> e <code>$pwd</code> con il nome utente di MySQL locale e la password.</span><span class="sxs-lookup"><span data-stu-id="6462d-169">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="6462d-170">Il seguente codice di connessione database hello, aggiungere il codice per l'inserimento di informazioni di registrazione nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-170">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
9. <span data-ttu-id="6462d-171">Infine, il seguente codice hello precedente, aggiungere il codice per recuperare dati dal database hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-171">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="6462d-172">È possibile cercare troppo**http://localhost:8000/index.php** tootest un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-172">You can now browse too**http://localhost:8000/index.php** tootest hello application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="6462d-173">Pubblicare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="6462d-173">Publish your application</span></span>
<span data-ttu-id="6462d-174">Dopo aver testato l'applicazione localmente, è possibile pubblicare App Web del servizio tooApp tramite Git.</span><span class="sxs-lookup"><span data-stu-id="6462d-174">After you have tested your application locally, you can publish it tooApp Service Web Apps using Git.</span></span> <span data-ttu-id="6462d-175">Tuttavia, è necessario innanzitutto informazioni di connessione di database tooupdate hello in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-175">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="6462d-176">Utilizzando le informazioni di connessione database hello ottenuti in precedenza (in hello **informazioni di connessione di Database SQL di ottenere** sezione), aggiornamento hello le seguenti informazioni in **entrambi** hello `createdatabase.php` e `index.php` i file con hello valori appropriati:</span><span class="sxs-lookup"><span data-stu-id="6462d-176">Using hello database connection information you obtained earlier (in hello **Get SQL Database connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="6462d-177">In hello <code>$host</code>, il valore di hello del Server deve essere preceduto da <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="6462d-177">In hello <code>$host</code>, hello value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="6462d-178">A questo punto, si sono pronti tooset la pubblicazione Git e pubblica un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-178">Now, you are ready tooset up Git publishing and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="6462d-179">Si tratta di hello stessi passaggi indicati alla fine hello hello **creare un'app web di Azure e impostare la pubblicazione Git** sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="6462d-179">These are hello same steps noted at hello end of hello **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="6462d-180">Aprire GitBash (o un terminale, se si trova in Git il `PATH`), cambiare directory radice toohello di directory dell'applicazione (hello **registrazione** directory), e hello esecuzione seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="6462d-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application (hello **registration** directory), and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="6462d-181">Verrà richiesto di hello password creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6462d-181">You will be prompted for hello password you created earlier.</span></span>
2. <span data-ttu-id="6462d-182">Sfoglia troppo**http://[web app name].azurewebsites.net/createtable.php** toocreate tabella del database SQL di hello per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-182">Browse too**http://[web app name].azurewebsites.net/createtable.php** toocreate hello SQL database table for hello application.</span></span>
3. <span data-ttu-id="6462d-183">Sfoglia troppo**http://[web app name].azurewebsites.net/index.php** toobegin utilizzando un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6462d-183">Browse too**http://[web app name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

<span data-ttu-id="6462d-184">Dopo aver pubblicato l'applicazione, è possibile iniziare a creare tooit modifiche e utilizzare Git toopublish li.</span><span class="sxs-lookup"><span data-stu-id="6462d-184">After you have published your application, you can begin making changes tooit and use Git toopublish them.</span></span> 

## <a name="publish-changes-tooyour-application"></a><span data-ttu-id="6462d-185">Pubblicare l'applicazione di modifiche tooyour</span><span class="sxs-lookup"><span data-stu-id="6462d-185">Publish changes tooyour application</span></span>
<span data-ttu-id="6462d-186">toopublish cambia tooapplication, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="6462d-186">toopublish changes tooapplication, follow these steps:</span></span>

1. <span data-ttu-id="6462d-187">Apportare modifiche tooyour applicazione localmente.</span><span class="sxs-lookup"><span data-stu-id="6462d-187">Make changes tooyour application locally.</span></span>
2. <span data-ttu-id="6462d-188">Aprire GitBash (o un terminale, it Git è nel `PATH`), modificare le directory toohello radice directory dell'applicazione ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="6462d-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="6462d-189">Verrà richiesto di hello password creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6462d-189">You will be prompted for hello password you created earlier.</span></span>
3. <span data-ttu-id="6462d-190">Sfoglia troppo**http://[web app name].azurewebsites.net/index.php** toosee le modifiche.</span><span class="sxs-lookup"><span data-stu-id="6462d-190">Browse too**http://[web app name].azurewebsites.net/index.php** toosee your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="6462d-191">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="6462d-191">What's changed</span></span>
* <span data-ttu-id="6462d-192">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6462d-192">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

